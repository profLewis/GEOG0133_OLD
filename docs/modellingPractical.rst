Carbon Modelling Practical
===========================

Introduction
------------

The main purpose of this practical is to allow students to explore a model of the terrestrial carbon. The model implemented is based on that in JULES (Best et al., 2011; Clark et al., 2011) with some minor modifications.  That model is in any case very similar to that of Sellers et al. (1992). You should probably refresh your memory of the Sellers paper.

The style of the practical will be to give you access to a piece of (modelling) code that you can explore. There are set 'experiments' around the codes, e.g. to explore the limiting factors on carbon assimilation at the leaf level under different conditions.

In the last half hour of the session, the course tutor will tell you to stop experimenting and will expect some discussion around the insights gained. You should be prepared to show some figures and possibly tables to support this discussion.


The code
--------

The main computer code is implemented in Python and available `here <photJules.py>`_.

Before running this, you should create a directory 'figures'.

An example use of the model is:

::

    from photJules import *
    import pylab as plt
    
    self = photosynthesis()
    
    def test1(self,n=100,name='a',ipar=200.,Tc=None,x=None,xlabel=None,\
              co2_ppmv=390,C3=True,type='C3 grass',plot=True):
        '''
        low light level, span a temperature range, normal CO2
        '''
      
        self.data = np.zeros(n)
    
        # set plant type to C3
        self.C3 = np.zeros([n]).astype(bool) + C3
    
        self.Lcarbon = np.ones([n]) * 1
        self.Rcarbon = np.ones([n]) * 1
        self.Scarbon = np.ones([n]) * 1
    
        # set pft type
        # options are:
        # 'C3 grass', 'C4 grass', 'Needleleaf tree', 'Shrub'
        # 'Broadleaf tree'
        # Note that if C4 used, you must set the array
        # self.C3 to False
    
        self.pft = np.array([type]*n)
    
        # set up Ipar, incident PAR in (mol m-2 s-1)
        self.Ipar = np.ones_like(self.data) * ipar * 1e-6
        
        # set co2 (ppmv)
        self.co2_ppmv = co2_ppmv*np.ones_like(self.data)
        
        # set up a temperature range (C)
        try:
            if Tc == None:
                self.Tc = Tc or np.arange(n)/(1.*n) * 100. - 30.
            else:
                self.Tc = Tc
        except:
            self.Tc = Tc
        # initialise
        self.initialise()
        # reset defaults
        self.defaults()
    
        # calculate leaf and canopy photosynthesis
        self.photosynthesis()
    
        if plot == True:
            # plot
            plt.clf()
            if x == None:
                x = self.Tc
            plt.plot(x,self.Wc * 1e6,label='Wc')
            plt.plot(x,self.Wl * 1e6,label='Wl')
            plt.plot(x,self.We * 1e6,label='We')
            plt.plot(x,self.W * 1e6,label='W')
            plt.plot(x,self.Al* 1e6,label='Al')
            plt.plot(x,self.Rd* 1e6,label='Rd')
    
            plt.ylabel('assimilation rate (umol CO2 m-2 s-1)')
            if xlabel == None:
                plt.xlabel('temperature (C))')
            else:
                plt.xlabel(xlabel)
            plt.legend(loc='upper right')
            plt.savefig('figures/test1%s.png'%name)
    
    test1(self,name='a')
    



.. figure:: figures/test1a.png
    :align: center
    :target: figures/test1a.png
    :width: 50%

In this example, we plot leaf assimilation (:math:`W`) as a function of temperature for a :math:`CO_2` concentration of 390 ppmv, for a C3 grass for incident PAR of 200 :math:`\mu\,mol\,m^{-2}\,s^{-1}`.

Also shown on the figure are the Rubisco limiting rate (:math:`W_c`), the light limited rate (:math:`W_l`) and the rate of transport of photosynthetic products (for C3, this would be PEPCarboxylase limitation for C4 plants) (:math:`W_e`). As in other models, the rate taken for photosynthesis here is the minimum of these limiting rates (actually in JULES, a blending of the rates, but made close to the minimum here).

Finally, the graph also shows the net leaf assimilation rate :math:`A_l`, which involves water limitation and the subtraction of leaf dark respiration :math:`R_d`.

We can see that at various temperatures, the different limiting rates take over: up until around 19 C it is limited by the rate of transport of photosynthetic products, then by light, for higher temperatures, by Rubisco. In this model, both :math:`W_c` and :math:`W_e` are scaled by the term :math:`V_{cmax}`, the maximal rate of carboxylation, which has a temperature limitation (essentially a maximum and minimum temperature for operation) being 36 C and 0 C for C3 grasses here.

:math:`V_{cmax}` is also dependent on the leaf nitrogen concentration.

The light limiting rate is dependent on the internal leaf :math:`CO_2` pressure, :math:`c_i` and the photorespiration compensation point :math:`\Gamma` that has a temperature dependence. Here, we assume that  :math:`c_i`  is proportionate to  :math:`c_a`, which is related to the external :math:`CO_2` concentration and the atmospheric pressure.

If we increase the light level, we can remove the light limitation:

::

    test1(self,name='b',ipar=500.,co2_ppmv=390)
    



.. figure:: figures/test1b.png
    :align: center
    :target: figures/test1b.png
    :width: 50%

Experiment 1
------------

Use the code test1() to explore the limiting factors for the range of vegetation types (PFTs) available here (see code above). You should be interested in the temperature ranges for each PFT (see also tables of parameters in  Clark et al. 2011) and when the different limiting factors kick in for a reasonable range of light conditions and :math:`CO_2` concentrations.

You should generate some appropriate graphs and tables and be prepared to discuss these at the end of the session.

Diurnal variations
------------------

We now include a model of solar radiation to examine diurnal variations.

::

    # make sure can access pyephem
    
    import sys
    sys.path.append ("/home/ucfajlg/Data/python_libs/pyephem-3.7.5.1-py2.7-linux-x86_64.egg/" )
     
    class sunInfo():
        '''
        A utility to work out some solar information
        '''
        def __init__(self,julianOffset=None):
            '''
            Initialise class
            
            options:
                julianOffset: set to report Julian day with an offset subtracted
                              Format, 'YYYY/M/D' e.g. '2012/1/1'
            '''
            # use the python library ephem
            import ephem
            self.gatech = ephem.Observer()
            if julianOffset != None:
                self.julianOffset = ephem.julian_date(julianOffset)
            else:
                self.julianOffset  = 0.
    
            # http://acrim.com/TSI%20Monitoring.htm
            self.solar = 1361 #W/m2
     
            # PPFD is measured in micromoles/m2/sec
            # (Photosynthetic Photon Flux Density)
    
            # astronomical unit
            # http://neo.jpl.nasa.gov/glossary/au.html
            # we dont need this, but its interesting to know
            self.AU = 149597870.691 * 1e3 # m
    
            # energy content of PAR quanta
            self.EPAR = 220.e-3 # MJmol-1
    
        def sun(self,secs,mins,hours,days,months,years,lats,lons):
            '''
            Utility to set days, months, years, lats, lons
            and calculate max_solar_flux
            '''
            import ephem
            self.julian = []
            self.sza = []
            self.earth_distance = []
    
            for lon in np.atleast_1d(lons):
                self.gatech.lon = str(lon)
                for lat in np.atleast_1d(lats):
                    self.gatech.lat = str(lat)
                    for year in np.atleast_1d(years):
                        for month in np.atleast_1d(months):
                            for day in np.atleast_1d(days):
                                for hour in np.atleast_1d(hours):
                                    for min in np.atleast_1d(mins):
                                        for sec in np.atleast_1d(secs):
                                            self.gatech.date = '%4d/%d/%d %d:%d:%d'%\
                                                (year,month,day,hour,min,int(sec))
                                            v = ephem.Sun(self.gatech)
                                            alt = np.max([0,v.alt * 180./np.pi])
                                            self.sza.append(90. - alt)
                                            jd = ephem.julian_date('%4d/%d/%d'%(year,month,day)) \
                                                     - self.julianOffset
                                            jd += hour/24. + min/60./24. + sec/60./60./24.
                                            self.julian.append(jd)
                                            self.earth_distance.append(v.earth_distance)
            self.julian = np.array(self.julian)
            self.sza = np.array(self.sza)
            self.earth_distance = np.array(self.earth_distance)
            self.solarRad = self.solar/(self.earth_distance*self.earth_distance)
            # Express radiation in mol(photons) / (m^2 s)
            self.solarRad_mol = self.solarRad/self.EPAR
    
        def plot(self,x,y,xname,yname,plotname='sunplot.png'):
            '''
            Plot utility
            '''
            plt.clf()
            plt.xlabel(xname)
            plt.ylabel(yname)
            plt.plot(x,y)
            plt.savefig('figures/' + plotname)
    
    # get sun information
    s = sunInfo(julianOffset='2012/1/1')
    # loop over day (1 Jan 2012) at latitude 52.0
    s.sun(0.,np.array([0.,30.]),np.arange(25),1,1,2012,52.0,0)
    s.plot(s.julian,np.cos((s.sza*np.pi/180.)),'Fraction of day',\
           'Cosine of Solar Zenith angle (degrees)',plotname='sunplot.png')
    
    # assume PAR is 50% of downwelling radiation
    # and atmospheric optical thickness of PAR is 0.2
    # we multiply by cos(solar zenith) here to project
    # onto a flat surface (a 'big leaf')
    
    tau = 0.2
    mu = np.cos((s.sza*np.pi/180.))
    ipar = s.solarRad_mol * 0.5 * np.exp(-tau/mu) * mu  # u mol(photons) / (m^2 s)
                   
    s.plot(s.julian,ipar,'Fraction of day','Indicent PAR radiation (approx. in units u mol(photons) / (m^2 s))',\
           plotname='ipar.png')
     
    test1(self,n=len(ipar),Tc=25.0,name='c',ipar=ipar,co2_ppmv=390,x=ipar,xlabel='incident PAR (umol m-2 s-1)')
    
    # now plot Al + Rd over the day
    s.plot(s.julian,(self.Al+self.Rd)*1.e6,'Fraction of day','assimilation rate (u mol CO2 m-2 s-1)',plotname='Al.png')
    



.. figure:: figures/sunplot.png
    :align: center
    :target: figures/sunplot.png
    :width: 50%

.. figure:: figures/ipar.png
    :align: center
    :target: figures/ipar.png
    :width: 50%

.. figure:: figures/test1c.png
    :align: center
    :target: figures/test1c.png
    :width: 50%

.. figure:: figures/Al.png
    :align: center
    :target: figures/Al.png
    :width: 50%

This is quite an interesting figure ... if the only thing that varies over the day is the solar radiation intensity, then at this time and latitude, the (leaf) assimilation is 'pulse'-like over the day: its is limited by light intensity at high solar zenith angles, then essentially flat. 

Normally, the temperature will vary over the day as well, so we could e.g. assume a dependence on solar zenith angle:

::

    # make temperature a function of cos(solar zenith)
    temp = 35 * mu
    
    test1(self,n=len(ipar),Tc=temp,name='c',ipar=ipar,co2_ppmv=390,x=ipar,xlabel='',plot=None)
    
    s.plot(s.julian,temp,'Fraction of day','Temperature (C)',\
           plotname='temp.png')
    
    
    s.plot(s.julian,(self.Al+self.Rd)*1e6,'Fraction of day','assimilation rate (u mol CO2 m-2 s-1)',\
           plotname='iparT.png')
    



.. figure:: figures/temp.png
    :align: center
    :target: figures/temp.png
    :width: 50%



.. figure:: figures/iparT.png
    :align: center
    :target: figures/iparT.png
    :width: 50%

Now we have dramatically reduced the temperature so we see a general lowering of the assimilation rate, but we also see a change in the shape.

Exercise 2
-----------

Using codes similar to those above, explore diurnal variations in leaf assimilation rate at different latitudes and different times of year, for different PFTs (hint: once you have set this up for one example, it should be easy to run for multiple cases).

If possible, you should try to explain what the limiting factors are in each case (hint: plot terms other that :math:`self.Al`, such as :math:`self.Wc`, :math:`self.Wl`, :math:`self.We`).

It would be interesting to summarise such results by calculating the total (leaf) assimilation over the day (N.B. in the above examples, :math:`A_l` is sampled every half hour over the day: you want a result in :math:`\mu\,\,mol/m^2`).

When performing this experiment, think about other complexities that might arise (e.g. how does the idea of phenology fit into this?)

Canopy scale assimilation
-------------------------

All of the above experimentation was just at the leaf level. We have essentially looked at responses to temperature and light intensity. Of course, in a 'real' canopy, there will be varying amounts of leaf area, so we have to consider how to scale up the leaf-level assimilation to the canopy scale.

Although there are various ways to scale from leaf-level assimilation to the canopy level, we have only implemented what is perhaps the simplest here. This is based on the assumption that there is an acclimatisation of leaf :math:`N` throughout the canopy (Sellers et al., 1992) giving:

.. math:: V_m = V_{m0} \overline{f(L)}


where :math:`\overline{f(L)}` is the average fraction of absorbed PAR (as opposed to instantaneous) at leaf area index (LAI) :math:`L`, :math:`V_{m0}` is the 'maximum' (top leaf) assimilation, and :math:`V_m` is the canopy-scale assimilation.

Assuming a homogeneous canopy, the canopy scale PAR use efficiency :math:`\Pi` is:

.. math:: \Pi = \int_{0}^{L} \overline{f(l)}\,dl. = \left[ \frac{1-e^{-\overline{k}L}}{\overline{k}} \right] = \frac{\overline{fAPAR}}{\overline{k}}

where :math:`\overline{fAPAR}` is the (average) fraction of absorbed PAR by the canopy and :math:`\overline{k}` is an effective extinction coefficient:

.. math:: \overline{k} = \left[ \frac{G(\mu)}{\mu} \right] {(1-\omega_l)}^{\frac{1}{2}}

with :math:`\mu` the cosine of the (time mean) solar zenith angle (a path length term), :math:`G(\mu)` the 'Ross' or 'G'-function giving the average normalised leaf projection in the direction of the (time mean) incoming radiation, and :math:`\omega_l` is the leaf single scattering albedo (unity minus leaf absorption) in the PAR region (see Sellers et al., 1992 for more details).

Under these assumptions then, we can calculate canopy scale photosynthesis.

.. math:: GPP = A_l \frac{\overline{fAPAR}}{\overline{k}}

Suppose we have an amount of leaf carbon of 0.07 :math:`kg\,C\,m^{-2}` and a specific leaf density of 0.025 (:math:`kg\, C\,m^{-2}` per unit of LAI) that is constant throughout the canopy (giving a LAI of 0.07/0.025 = 2.8), and a G gunction of 0.5 (e.g. a spherical leaf angle distribution). We can model this as:

::

    # get sun information
    s = sunInfo(julianOffset='2012/1/1')
    
    # loop over day and month at latitude 50.0
    # NB we use the dates 1-366 of January here to avoid month issues
    s.sun(0.,np.array([0.,30.]),np.arange(24)*1.,np.arange(366)+1,1.,2012,50.,0.)
    
    s.plot(s.julian,np.cos((s.sza*np.pi/180.)),'DOY',\
           'Cosine of Solar Zenith angle (degrees)',plotname='sunplot2.png')
    
    # assume PAR is 50% of downwelling radiation
    # and atmospheric optical thickness of PAR is 0.2
    # we multiply by cos(solar zenith) here to project
    # onto a flat surface (a 'big leaf')
    
    tau = 0.2
    mu = np.cos((s.sza*np.pi/180.))
    ipar = s.solarRad_mol * 0.5 * np.exp(-tau/mu) * mu  # u mol(photons) / (m^2 s)
    temp = 35 * mu
    # temperature
    
    s.plot(s.julian,ipar,'DOY','Indicent PAR radiation (approx. in units u mol(photons) / (m^2 s))',\
           plotname='ipar2.png')
    s.plot(s.julian,temp,'DOY','Temperature (C)',plotname='temp2.png')
    
    # run the leaf level model
    test1(self,n=len(ipar),Tc=temp,name='c',ipar=ipar,co2_ppmv=390,plot=None)
    
    # now plot over days the leaf level response
    s.plot(s.julian,(self.Al+self.Rd)*1.e6,'DOY','leaf assimilation rate (u mol CO2 m-2 s-1)',plotname='Al2.png')
    
    # now we want the canopy level response
    
    self.Lcarbon = 0.07 # kg C m-2
    #self.sigmal = 0.025 # kg C m-2 per unit LAI for C3 grass
    # for Needleleaf tree: 0.10
    # for Broadleaf tree: 0.0375
    # for others: 0.05
    self.LAI = self.Lcarbon/self.sigmal
    
    # leaf single scattering albedo
    self.omega = 0.2
    
    self.G = 0.5
    self.mubar = np.mean(mu)
    self.kbar = (self.G/self.mubar)*np.sqrt(1-self.omega)
    self.fapar = 1 - np.exp(-self.kbar * self.LAI)
    print 'mubar =',self.mubar
    print 'kbar =',self.kbar
    print 'fapar=',self.fapar
    # kg C m-2 s-1: conversion factor from Clark et al. 2011
    self.GPP = 0.012 * (self.Al + self.Rd)* self.fapar / self.kbar
    
    # plot this
    s.plot(s.julian,self.GPP*1e6,'DOY','GPP (mg C m-2 s-1)',plotname='Al3.png')
    
    

::

    mubar = 0.21142981203
    kbar = 2.11518702688
    fapar= [ 0.99732157  0.99732157  0.99732157 ...,  0.99732157  0.99732157
      0.99732157]
    



.. figure:: figures/sunplot2.png
    :align: center
    :target: figures/sunplot2.png
    :width: 50%

.. figure:: figures/ipar2.png
    :align: center
    :target: figures/ipar2.png
    :width: 50%

.. figure:: figures/temp2.png
    :align: center
    :target: figures/temp2.png
    :width: 50%

.. figure:: figures/Al2.png
    :align: center
    :target: figures/Al2.png
    :width: 50%

.. figure:: figures/Al3.png
    :align: center
    :target: figures/Al3.png
    :width: 50%


The Net Ecosystem Productivity needs the plant respiration terms to be subtracted from the GPP. This is typically split into mainenance and growth respiration: :math:`R_{pm}` and :math:`R_{pg}` respectively. In Jules,  :math:`R_{pg}`  is assumed to be a fixed fraction of NPP:

.. math:: R_p = R_{pm} + R_{pg}

.. math:: R_{pg} = r_g \Pi_G

where :math:`\Pi_G` is the GPP (the canopy scale assimilation). In Jules, :math:`r_g` is set to 0.25 for all PFTs (Clark et al., 2011). Leaf maintenance respiration in Jules is the (moisture-modified, through a term :math:`\beta` that we have not dealt with here) canopy dark respiration (i.e. canopy-scaled). Root and stem respiration are set to depend on the nitrogen concentrations of the root and stem relative to the leaf nitrogen.

Since we have not introduced stem and root biomass yet, we will assume here that leaf, root and (respiring) stem biomass (:math:`L`, :math:`R` and :math:`S` respectively) we will assume these terms equal for the moment, since we only require their relative amounts:

.. math:: R_pm = 0.012\,\,R_{dc} \left( \beta + \frac{N_r + N_s}{N_l} \right)

where:

:math:`N_x` is the Nitrogen concentration of biomass component :math:`x` and the factor :math:`0.012` converts units (see Clark et al., 2011).

.. math:: N_l = n_m L
.. math:: N_r = n_m R \mu_{rl}
.. math:: N_s = n_m S \mu_{sl}

where :math:`\mu_{xl}` is the relative Nitrogen concentartion of biomass component :math:`x` to leaf Nitrogen (assumed 1.0 here). :math:`beta` is 1.0 for unstressed conditions. So:

.. math:: R_pm = 0.012\,\,R_{dc} \left( \beta + \frac{R + S}{L} \right) = 0.036\,\,R_{dc}  

::

    # NPP calculation
    self.rg = 0.25
    # scale Rd up to canopy here
    self.Rpm = 0.036 * self.Rd * self.fapar / self.kbar
    self.PiG = 0.012*(self.Al - self.beta * self.Rd) * self.fapar / self.kbar
    self.Rpg = self.rg * (self.PiG - self.Rpm)
    # ensure non negative
    self.Rpg[self.Rpg<0] = 0.
    self.Rp = self.Rpm + self.Rpg
    # NPP: self.Pi
    self.Pi = self.PiG - self.Rp
    
    s.plot(s.julian,self.Pi*1e6,'DOY','NPP (mg C m-2 s-1)',plotname='NPP.png')
    


.. figure:: figures/NPP.png
    :align: center
    :target: figures/NPP.png
    :width: 50%


The annual integral of NPP then is:

::

    print 'mean NPP =',np.mean(self.Pi) * 24 * 60 * 60 *1e3,'g C m-2 day-1'
    print 'mean GPP =',np.mean(self.PiG) * 24 * 60 * 60 * 1e3,'g C m-2 day-1'
    
    # n seconds in year
    nsec = 366 * 24 * 60 * 60.
    integral = np.mean(self.Pi) * nsec * 1e3 # g C m-2 yr-1
    print 'NPP = ',integral * 1e3,'g C/m2/yr'
    
    # The total land surface area of the Earth is around 0.292 * 510072000 km^2
    # http://chartsbin.com/view/wwu
    # so if this were the mean, we would have
    
    print 'Global NPP (rough est.) =',0.292 * 510072000 * integral *1e-9,' GT C yr-1'
    

::

    mean NPP = 1.71250944775 g C m-2 day-1
    mean GPP = 2.74500944105 g C m-2 day-1
    NPP =  626778.457878 g C/m2/yr
    Global NPP (rough est.) = 93.3530253375  GT C yr-1
    



which is certainly an over-estimate by a factor of about 2 because we have assumed high LAI grasslands everywhere on the land surface, but is at least the right order of magnitude.

Experiment 3
------------

We have shown here how to introduce LAI (or leaf C) into the scaling up to canopy GPP, and also how respiration terms in a model such as Jules can be calculated, which allows us to estimate canopy NPP.

The next parts of a model of this sort include partitioning of the NEP among biomass pools and applying phenological controls.

You could assume a simple, fixed proportion of partitioning of assimilates (e.g. 1/3 to leaf, root and (respiring) stem biomass pools (i.e. each day, if NPP is positive, you add 1/3 of the NPP (integrated over 24 hours = 24*60*60 seconds) to the leaf carbon pool (self.Lcarbon)). This then increases the LAI.

Since the canopy scaling model here is very simple, it turns out to be just a scalar to :math:`A_l`, so you can first calculate  :math:`A_l` over each day of the year, then, starting at the begining of the time series, start to accumulate carbon (and produce LAI). This gives you a dynamic LAI model (albeit at this moment one that is not controlled by phenology) that you can then use for each daily sample to scale from leaf to canopy GPP and NPP. The only other term that you **need** to include is a leaf biomass loss (a leaf shedding term, and usually shedding terms for the other pools of carbon). In Jules, this is achieved by defining a leaf turnover rate :math:`\gamma_{lm}` which is temperature controlled but set to 0.25 (per year) for C3 grasses if the temperature is above a threshold (see p.710 of Clark et al.). We could (very simply) assume then a rate of leaf biomass loss of :math:`0.25\,\,L/(366)` per *day* (although in Jules, the rate is based on the maximum seasonal leaf biomass, but we use the actual leaf biomass :math:`L` here).

This final exercise then, is to build a dynamic vegetation model, one that 'grows' leaf carbon by calculating NPP, allocating a proportion of this to the leaf C pool at the end of each day, then losing a proportion (:math:`0.25\,\,L/(366)`) as litterfall. This should be quite feasible given the codes above, though you might not finish it in this session. If you do complete this, you will find it a very satisfying exercise ... to have created a model of growing plants that links the concepts we have discussed. Although this is a slightly simplified model, it is **not** greatly less sophisticated than the models currently used in DGVMs, and you can learn a lot by building and trying out a model of this sort.

Once you have built the model, demonstrate its application for some given latitude and (ideally) multiple PFTs.


Experiment 4
-------------

Whilst it is an interesting exercise to build and use models of the sort we have created here, there are many flaws with such models. Think carefully about what insights you have gained into both the strengths and weaknesses of such models. You should read the references below carefully to see what criticisms there are in those papers (e.g. complexities about leaf to canopy scaling). You should also think carefully about the role that 'fixed' parameters for each PFT have in such models, bearing in mind what has been learned from plant traits databases such as that of Kattge et al., (2011) that was covered in the lecture on Terrestrial Ecosystem Modelling.




References 
----------

P. J. Sellers, J. A. Berry, G. J. Collatz, C. B. Field, and E G. Hall (1992) Canopy Reflectance, Photosynthesis, and Transpiration. III. A Reanalysis Using Improved Leaf Models and a New Canopy Integration Scheme, REMOTE SENS ENVIRON 42 187-216 (1992)

M. J. Best, M. Pryor, D. B. Clark, G. G. Rooney, R .L. H. Essery, C. B. Menard, J. M. Edwards, M. A. Hendry, A. Porson, N. Gedney, L. M. Mercado, S. Sitch, E. Blyth, O. Boucher, P. M. Cox, C. S. B. Grimmond, and R. J. Harding (2011) The Joint UK Land Environment Simulator (JULES), model description Part 1: Energy and water fluxes, Geosci. Model Dev., 4, 677-699, 2011

D. B. Clark, L. M. Mercado, S. Sitch, C. D. Jones, N. Gedney, M. J. Best, M. Pryor, G. G. Rooney, R. L. H. Essery, E. Blyth, O. Boucher, R. J. Harding, C. Huntingford, and P. M. Cox (2011) The Joint UK Land Environment Simulator (JULES), model description Part 2: Carbon fluxes and vegetation dynamics, Geosci. Model Dev., 4, 701-722, 2011

[Also note: Kattge, J., et al. (2011), TRY: a global database of plant traits. Global Change Biology, 17: 2905-2935. doi: 10.1111/j.1365-2486.2011.02451.x]
