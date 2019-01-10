Data Assimilation practical
=====================================

Introduction
-------------

In this practical, you will get some practical experience of using a Kalman filter for state estimation. 

We develop an example using satellite (MODIS) 500 m resolution reflectance data where we apply kernel-driven BRDF model to perform angular correction with a Kalman filter.

datasets: MODIS reflectance data
---------------------------------

You are provided with python code to extract time series of MODIS (C4 here) reflectance data. The python code is `fireData.py <python/fireData.py>`_. It is designed as a command line tool (i.e. to run from the unix prompt) but youy can also interface to it from python. Before you start, make your directory to work in (NOT in your home dir), cd to this and make a sub-directory called figures. This is where the python codes write figures by default.

::

    '''
    Usage: fireData.py [options]
    
    Options:
      -h, --help            show this help message and exit
      -r ROW, --row=ROW     starting row (y)
      -c COL, --col=COL     starting column (x)
      --nrow=NROWS, --nrows=NROWS
                            number of rows (y)
      --ncol=NCOLS, --ncols=NCOLS
                            number of columns (x)
      -f FILE, --file=FILE  Name for output data file
      -p, --plot            
      --plotfile=PLOTFILE   Name for plotfile
      -v, --verbose         
      -d DATADIR, --datadir=DATADIR
                            Name for input data directory
    '''
    

::

    from fireData import *
    # interface to the 'simple' options using sys.argv 
    # this is the same as would be apossed through from a unix command line
    import sys
    
    sys.argv = 'fireData.py -r 397 -c 295 -p -f data.npz --plotfile=figures/plotFire_397_295.png'.split()
    getrefl()
    
    



.. figure:: figures/plotFire_397_295.png
    :align: center
    :width: 90%


This code loops over the MODIS surfrace reflectance datasets in the directory `DATADIR` (`/data/geospatial_20/plewis/geogg124` by default) and extracts data for all samples from (ROW,COL) to (ROW+NROWS,COL+NCOLS).

If the `-v` flag is set, then feedback on progress is generated (verbose mode). 

If the `-p` flag is set, a plot of the reflectance data is generated (for the first pixel of the area requested).

If the `-f` flag is used, the data are written to a numpy file. This can be handy for experimentation, as you don't need to keep reading the (large) HDF datafiles.


The upper graphs show the reflectance in the 12 MODIS wavebands. Looking at e.g. the red reflectance (659 nm) we see a lack of  data in the early part of the year (cloud cover), then as we start to get lots of samples, the reflectance slowly increases from a low base, with a slight kink in the middle of the time series. Looking at the near infrared (865 nm) we see much the same behaviour. For all bands, we see a some consistent *patterns* of variation, followed by a quite sudden drop in reflectance, then a gradual recovery. The variation in the day to day reflectance is however quite high, most likely simply due to 'BRDF effects': viewing the surface at different angles on different overpasses.

The 'sudden' drop in near infrared is, in this region (`MODIS tile h20v10 <http://nsidc.org/data/docs/daac/mod10_modis_snow/landgrid.html>`_ Zambia and surrounds), indicative of a vegetation fire.

An example `numpy file` is `data.npz <python/data.npz>`_ (Note: you are unlikely to be able to use this as the format is different for different architectures). To load the data from this file:

::

    import numpy as np
    import pylab as plt
    
    infile = 'data.npz'
    data = np.load(infile)
    r = data['reflectance']
    vza = data['vza']
    sza = data['sza']
    raa = data['raa']
    wavebands = data['wavebands']
    mask = data['mask']
    doy = data['doy']
    lclut = data['landCoverLUT']
    lc = data['landcover']
    fireday = data['activeFire']
    try:
        print 'fire:',fireday[0,0]
        print 'Land cover',lc[0,0],lclut[lc[0,0]]
    except:
        pass
    # calculate NDVI
    red = r[:,0,:,:]
    nir = r[:,1,:,:]
    ndvi = np.zeros_like(red)
    ndvi[mask] = (nir - red)[mask]/(nir + red)[mask]
    
    plt.clf()
    plt.figure(2)
    # and now plot it
    plt.plot(doy[mask[:,0,0]],ndvi[mask[:,0,0],0,0],'o')
    plt.xlabel('doy')
    plt.ylabel('NDVI')
    plt.axvline(fireday,ymin=0,ymax=1.,lw=1.5)
    plt.savefig('figures/ndviExample.png')
    

::

    fire: 169.0
    Land cover 10 Grasslands
    



.. figure:: figures/ndviExample.png
    :align: center
    :width: 90%

The NDVI somewhat reduces the angular effects we saw in the near infrared data above, although there is variation of greater than 0.1 here that we strongly suppose to be solely due to BRDF effects.

The impact of the fire (on DOY 169) is shown quite clearly in the NDVI data, although we notice that the post-fire signal is also rather noisy (variation of greater than 0.1 again). However, if we happened to miss the samples in the week or so following the fire, we might suppose that the subsequent NDVI pattern was just part of the continuing downward trend of NDVI. 

We have seen throughout this course that NDVI data of this sort are currently the mainstay of most satellite-based ecological monitoring, but here we demonstrate what is widely known by very often ignored, that such data can show  broad impacts, provided those impacts are of quite large magnitude, and that the dynamics of the signal needs careful consideration (the drop here is due to *fire* not some phenology signal).

Knowing that this is a grassland in southern Africa here, we would expect breaodly a high NDVI at the start of the year, with a decrease towards the dry season as the amount of green vegetation is reduced (and replaced here by dry grass), then a clearing of this (by fire in this case) and a start at recovery of the signal towards the end of the year. What we see here is explicable, but it is very noisy.


Observation operator
--------------------

If we wish to treat these data better, we could of course just apply some smoothing to the time series. Bt since we strongly suspect that some of the variation we see is caused by BRDF effects, we can attempt to model this to account for this mechanism.

Since we are only at this point interested in describing the BRDF effects, we can use linear kernel models for this purpose. In such models, we consider that the BRDF (or more strictly, the BRF) can be described as a sum of three (typically) achetype scattering functions known as kernels. These are derived from simplifications to radiative transfer theory.

In such a model, we then consider reflectance at some waveband :math:`\lambda` and viewing geometry :math:`\Omega_v` and illumination geometry :math:`\Omega_i`, :math:`R(\lambda,\Omega_v,\Omega_i)` to be:

.. math:: R(\lambda,\Omega_v,\Omega_i) = f_{iso} (\lambda) + f_{vol} (\lambda) k_{vol}(\Omega_v,\Omega_i) + f_{geo} (\lambda) k_{geo}(\Omega_v,\Omega_i)


where :math:`k_{vol}(\Omega_v,\Omega_i)` and :math:`k_{geo}(\Omega_v,\Omega_i)` are the model *kernels*, functions of geometry only, and :math:`f_{iso} (\lambda)`, :math:`f_{vol} (\lambda)` and :math:`f_{geo} (\lambda)` are the *kernel weights* or the model parameters. We can calculate the kernels from knowledge of the viewing and illumination geometries for each observation, but we must solve for (estimate) the kernel weights.

We have a python code `kernels.py <python/kernels.py>`_ that allows calculation of the kernels:


.. plot::
    :include-source:

    from kernels import *
    mimic(doPlot=True,thisSza=[0.0])

.. plot::
    :include-source:

    from kernels import *
    mimic(doPlot=True,thisSza=[30.0])

.. plot::
    :include-source:

    from kernels import *
    mimic(doPlot=True,thisSza=[60.0])




::

    from kernels import *
    import numpy as np
    import pylab as plt
    from scipy.optimize import fmin_l_bfgs_b
    
    #load the data, as above
    infile = 'data.npz'
    data = np.load(infile)
    r = data['reflectance']
    vza = data['vza']
    sza = data['sza']
    raa = data['raa']
    wavebands = data['wavebands']
    mask = data['mask']
    doy = data['doy']
    lclut = data['landCoverLUT']
    lc = data['landcover']
    fireday = data['activeFire']
    
    # calculate the kernels
    k = Kernels(vza[mask],sza[mask],raa[mask],doIntegrals=False)
    
    # data
    red = r[:,0,:,:][mask]
    nir = r[:,1,:,:][mask]
    doys = doy[mask[:,0,0]]
    
    # select some days before the fire
    w = np.where((doys >= 120) * (doys <150))
    
    H = np.matrix([k.Isotropic[w],k.Ross[w],k.Li[w]])
    X = np.zeros(3)
    Y = red[w]
    R = np.eye(len(Y))
    R1 = np.matrix(R*R.T).I
    
    def J_obs(X,H,Y,R1):
        '''
        Cost function
        '''
        Y_hat = np.array((X * np.matrix(H)).T).flatten()
        d = np.matrix(Y - Y_hat)
        e = 0.5 * (d * R1 * d.T)[0,0]
        e_prime = -np.matrix(H) * R1 * d.T
        return e,np.array(e_prime)[:,0]
       
    
    bounds = [(0,1),(0,1),(0,1)] 
    # solve the minimisation problem
    solve = fmin_l_bfgs_b(J_obs,X,args=(H,Y,R1),bounds=bounds)
    X_new = solve[0]
    RMSE = np.sqrt(solve[1])
    
    print "red",X_new,'sd',RMSE
    
    Y_hat = np.array((X_new * np.matrix(H)).T).flatten()
    plt.clf()
    plt.plot(doys[w],Y,'o',label='obs')
    plt.plot(doys[w],Y_hat,'+',label='model')
    plt.legend(loc='best')
    plt.xlabel('doy')
    plt.ylabel('reflectance')
    plt.title('red')
    plt.savefig('figures/kernel1red.png')
    
    plt.clf()
    Y = nir[w]
    solve = fmin_l_bfgs_b(J_obs,X,args=(H,Y,R1),bounds=bounds)
    X_new = solve[0]
    RMSE = np.sqrt(solve[1])
    
    print "nir",X_new,'sd',RMSE
    
    Y_hat = np.array((X_new * np.matrix(H)).T).flatten()
    plt.plot(doys[w],Y,'o',label='obs')
    plt.plot(doys[w],Y_hat,'+',label='model')
    plt.legend(loc='best')
    plt.xlabel('doy')
    plt.ylabel('reflectance')
    plt.title('NIR')
    plt.savefig('figures/kernel1nir.png')
    
    
    

::

    red [ 0.08996554  0.0083535   0.04541085] sd 0.0134497468427
    nir [ 0.44320984  0.39601185  0.        ] sd 0.064310567818
    



If we assume that the model parameters are constant over some time period (e.g. 30 days), then we would expect only a single value for the model parameters.

In this case, we can estimate then with a simple least squares approach:

.. figure:: figures/kernel1red.png
    :align: center
    :width: 90%

.. figure:: figures/kernel1nir.png
    :align: center
    :width: 90%

The modelling over this 30 day period is clearly quite sucessful ... the reflectance at red andf NIR wavelengths varies significantly over this period, but there is no real trend (it looks at first sight like noise). 

By modelling the signal with the kernel models, we are able to describe a significant proportion of the variation in the signal.

In fact, this sort of approach (assuming parameters constant over some temporal window) is a practical and pragmatic solution to the problem of describing the signal dynamics, and this has been the mainstay of satellite products over the last decade or so.

We should however be able to use data assimilation methods to improve on this.

In the example above, when the function is *relatively* static, we found a RMSE (error metric) of 0.013 for the red channel and 0.064 for the NIR. This is a very rough way of estimating the uncertainty in the model and observations, and is probably here an over-estimate as it is not really true that we expect the parameters to be constant over this time period.

An approach we can take to allowing the model parameters to vary in time is to use a Kalman filter. 

To do this, we must define a *process model* :math:`M`. As we saw in the lecture, the simplest form of this is a *zero-order process model*, i.e. we assume tomorrow is the same as today. So, :math:`M = I`. 

We need then to define the uncertainty in this model. This is not straightforward. As we saw previously, this defines the *smoothness* of the model. 

We have a python code `kalman.py <python/kalman.py>`_ that provides an interface to a simple Kalman filter.


::

    from kernels import *
    import numpy as np
    import pylab as plt
    
    #load the data, as above
    infile = 'data.npz'
    data = np.load(infile)
    r = data['reflectance']
    vza = data['vza']
    sza = data['sza']
    raa = data['raa']
    wavebands = data['wavebands']
    mask = data['mask']
    doy = data['doy']
    lclut = data['landCoverLUT']
    lc = data['landcover']
    fireday = data['activeFire']
    #mask[doy < 110,0,0] = False
    # calculate the kernels
    k = Kernels(vza[mask],sza[mask],raa[mask],LiType='Dense',RossHS=False,doIntegrals=False)
    
    # data
    red = r[:,0,:,:][mask]
    nir = r[:,1,:,:][mask]
    doys = doy[mask[:,0,0]]
    
    H = np.matrix([k.Isotropic,k.Ross,k.Li])
    X = np.zeros(3)
    Y = red[0]
    R_red = np.eye(1) * 0.005**2
    R_nir = np.eye(1) * 0.02**2
    # observation uncertainty
    
    # model
    M = np.eye(3)
    # model uncertainty
    Q_red =  np.eye(3) * 0.0006**2
    Q_red[1,1] = Q_red[2,2] = 0.00006**2
    
    Q_nir = np.eye(3) * 0.006**2
    Q_nir[1,1] = Q_nir[2,2] = 0.0006**2
    
    # initial conditions
    x0_red = np.array([0.08996554, 0.0083535, 0.04541085])
    x0_nir = np.array([0.44320984, 0.3960118, 0. ])
    C_red = np.eye(3) * 0.2**2
    C_nir = np.eye(3) * 0.5**2
    
    import kalman
    
    # red
    kfr = kalman.Kalman(red,x0_red,C_red,R_red,M,Q_red,H,doys)
    
    # do a kernel set for angular normalisation
    vzan = np.zeros_like(kfr.alldoys)
    szan = vzan + np.mean(vza[mask])
    kernelnorm = Kernels(vzan,szan,vzan,LiType='Dense',RossHS=False,doIntegrals=False)
    
    plt.clf()
    kfr.run()
    plt.ylim(0,0.15)
    plt.errorbar(kfr.alldoys,kfr.x[:,0],yerr=np.sqrt(kfr.C[:,0,0]),fmt='ro',label='fiso')
    plt.errorbar(kfr.alldoys,kfr.x[:,1],yerr=np.sqrt(kfr.C[:,1,1]),fmt='bo',label='fvol')
    plt.errorbar(kfr.alldoys,kfr.x[:,2],yerr=np.sqrt(kfr.C[:,2,2]),fmt='go',label='fgeo')
    plt.legend(loc='best')
    plt.savefig('figures/kernelsKFred.png')
    
    plt.clf()
    rednorm = kfr.x[:,0]+kfr.x[:,1]*kernelnorm.Ross+kfr.x[:,2]*kernelnorm.Li
    plt.plot(kfr.alldoys,rednorm)
    plt.savefig('figures/kernelsKFnormred.png')
    
    plt.clf()
    plt.plot(kfr.sample_doys,kfr.y,'o',label='obs')
    plt.plot(kfr.sample_doys,kfr.fwd,'+',label='fwd')
    plt.legend(loc='best')
    plt.savefig('figures/kernelsKFfwdred.png')
    
    # nir
    plt.clf()
    kfn = kalman.Kalman(nir,x0_nir,C_nir,R_nir,M,Q_nir,H,doys)
    kfn.run()
    plt.ylim(0,0.7)
    plt.errorbar(kfn.alldoys,kfn.x[:,0],yerr=np.sqrt(kfn.C[:,0,0]),fmt='ro',label='fiso')
    plt.errorbar(kfn.alldoys,kfn.x[:,1],yerr=np.sqrt(kfn.C[:,1,1]),fmt='bo',label='fvol')
    plt.errorbar(kfn.alldoys,kfn.x[:,2],yerr=np.sqrt(kfn.C[:,2,2]),fmt='go',label='fgeo')
    plt.legend(loc='best')
    plt.savefig('figures/kernelsKFnir.png')
    
    plt.clf()
    nirnorm = kfn.x[:,0]+kfn.x[:,1]*kernelnorm.Ross+kfn.x[:,2]*kernelnorm.Li
    plt.ylim(0,0.25)
    plt.plot(kfn.alldoys,nirnorm)
    plt.savefig('figures/kernelsKFnormnir.png')
    
    plt.clf()
    plt.plot(kfn.sample_doys,kfn.y,'o',label='obs')
    plt.plot(kfn.sample_doys,kfn.fwd,'+',label='fwd')
    plt.legend(loc='best')
    plt.savefig('figures/kernelsKFfwdnir.png')
    
    # ndvi
    ndvinorm = (nirnorm-rednorm)/(nirnorm+rednorm)
    plt.clf()
    plt.ylim(0,1)
    plt.plot(kfn.alldoys,ndvinorm)
    plt.savefig('figures/kernelsKFnormndvi.png')
    



This then, is a data assimilation. We have assumed particular values for :math:`Q` and :math:`R`, but other than not knowing the relative balance of these two terms (and of course, and off-diagonal uncertainties) we have a perfectly viable DA system which is able to produce estimates of the model parameters for each time step. 

The results for the red waveband are:

.. figure:: figures/kernelsKFred.png
    :align: center
    :width: 90%

.. figure:: figures/kernelsKFfwdred.png
    :align: center
    :width: 90%

.. figure:: figures/kernelsKFnormred.png
    :align: center
    :width: 90%


and for the NIR:

.. figure:: figures/kernelsKFnir.png
    :align: center
    :width: 90%

.. figure:: figures/kernelsKFfwdnir.png
    :align: center
    :width: 90%

.. figure:: figures/kernelsKFnormnir.png
    :align: center
    :width: 90%

and then for NDVI:

.. figure:: figures/kernelsKFnormndvi.png
    :align: center
    :width: 90%


So, even with rather rough estimates of what the various uncertainties are, we are able to use the BRDF models (the observation operator) in a DA system to dramatically 'clean up' the signal. The *real* changes in surface properties are now much more apparent, both in the orginal reflectance data and in the NDVI. We can even discern a small drop in red reflectance at the time of the fire here.

It is clear from the NIR results in particular that we appear to have *over-smoothed* the function, i.e. we have assumed too small a model uncertainty (relative to the observation uncertainty) at and after the fire event. We can spot that  because the residuals after the fire appear to be rather larger than those before the fire.


Reverse filtering
-------------------

Of course, we can run the filter in the opposite direction to above (see `daPractical2.py <python/daPractical2.py>`_) and this will likely produce rather different results:

e.g. for the NIR:

.. figure:: figures/kernelsKFnir2.png
    :align: center
    :width: 90%

.. figure:: figures/kernelsKFfwdnir2.png
    :align: center
    :width: 90%

.. figure:: figures/kernelsKFnormnir2.png
    :align: center
    :width: 90%

and then for NDVI:

.. figure:: figures/kernelsKFnormndvi2.png
    :align: center
    :width: 90%


Again, here, we would suppose that the filtrering has over-smoothed the model parameters after the fire even (in reverse time order ... so before the fire): we can see that the residuals before the fire are higher than those after the fire (which we 'fitted to' first).

The normalised reflectance plot here shows the result for both the forward and reverse filter, which is quite interesting.

We would trust the modelling before the fire best from the forward filter, and after the fire from the reverse filter.  Interestingly, the fireday is very well mapped as the local maximum in the reverse filter and the local minimum in the forward filter.


It is of interest then to look at what happens around the time of the fire, which we can do by looking at the difference between the forward and backward filters.

.. figure:: figures/kernelsKFnormnir3.png
    :align: center
    :width: 90%

Following the observation above then, the fire day is very well highlighted by the difference between the forward and reverse filters. The magnitude of this gives an estimate of the magnitude of the step change, but we can see that it is surely an under-estimate.

This feature is also highlighted if we calculate the statistical difference (:math:`(x_f - x_r)^T (C_f^{-1} + C_r^{-1}) (x_f - x_r)`) which shows that according to this measure and the assumed statistics, these parameters are *different* throughout.

.. figure:: figures/kernelsZ2.png
    :align: center
    :width: 90%


Exercises
----------

* Explore using a Kalman filter DA approach for normalising angular effects in BRDF data, as in the example above. You will want to consider pixels other than the one shown here. You will also want to change the various uncertainties to understand the impact these have.
* Consider why the Kalman filter above gives somewhat different results when run in formward and backward mode. What use might such information be put to (e.g. in detecting sudden changes in the signal such as fire-affected areas)? How should you combine the state variables (:math:`x`) form the forward and backward sweeps? (hint: you should know how to combine uncertainties and how to use uncertainties to get a better estimate of the mean when you have two samples). If you feel capable of modifying the python code, you could try to implement your ideas.
* In fact, if you do a naive combination of the forward and reverse filters, you are unlikely to get the optimal estimate in this case. This is essentially because, as we have shown above, we are over-smoothing the model around the fire event (i.e. assuming the expectation of change to be too small). What then could be done to improve that? (hint: although we define the model uncertainty :math:`Q` as constant here, there is no reason that it should be so really).
* An issue we haven't really dealt with here is how to estimate the various uncertainties.  How could you estimate the relative uncertainty between the model and the observations (some reading around the lecture material shjould give you ideas)?
* We have deliberately chosen a simple (empirical) process model here. How would you redesign the system to work with a biogeochemical process model? What state vectors would you want the DA to affect? would a Kalman filter be appropriate?

