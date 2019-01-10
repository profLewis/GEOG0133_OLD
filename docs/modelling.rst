Terrestrial Ecosystem Modelling
===============================

Purpose of this lecture
------------------------

In the previous lecture, we reviewed some of the important mechanisms for understanding global terrestrial carbon state and dynamics. 
In this lecture, we consider strategies for building mathematical models to represent these concepts.


Land Surface schemes
--------------------

Basic energy and water processes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


The land surface component of a climate or  Earth System model, as well as models used in weather forecast  can be called a 'land surface scheme' (LSS), implemented as a 'land surface model' (LSM). The purpose of such a scheme is to model energy and (e.g. water, carbon) flux interactions at the land surface. The main driver of and LSS is generally consideration of the surface energy balance.


.. math:: R_n = S\downarrow (1 - \alpha) + L \downarrow - L \uparrow


where :math:`\alpha` is the shortwave albedo, :math:`R_n` is the net radiation, :math:`S \downarrow` is the downwelling shortwave radiation and :math:`L \downarrow` and  :math:`L \uparrow` are the downwelling and upwelling longwave radiation respectively. Although these terms balance globally over the long term, they do not do so locally and these energy dynamics drive the Earth climate system.

.. figure:: figures/pitman.png
    :align: center
    :width: 90%

**Source**: Pitman (2003)

In the above figure, showing global averages  of components of the energy balance, the solar radiation is represented as 100 units. Around 31 units are exchanged  as sensible and latent heat fluxes (:math:`H` and :math:`\lambda E` respectively), but the properties of the land surface significantly affect the way these fluxes are partitioned. The land surface also acts to *store* energy on various timescales (diurnal, seasonal, and longer). 

Here, :math:`E` is evapotranspiration (water loss from soil, leaf surfaces and from plant transpiration) (:math:`kg m^{-2} s^{-1}`), and :math:`\lambda` is the latent heat of vapoursiation (:math:`J kg^{-1}`).

The net radiation :math:`R_n` must be balanced by :math:`H` and :math:`\lambda E` and by the soil flux  :math:`G` and the chemical energy flux  :math:`F`  stored in photosynthesis:


.. math:: R_n = H + \lambda E + G + F

We can already see from these equations that changes in e.g. albedo  :math:`\alpha` are likely to alter :math:`H` and :math:`\lambda E` by altering  :math:`R_n`.

.. figure:: figures/pitman2.png
    :align: center
    :width: 90%


**Source**: Pitman (2003)


Being able to model the partition between :math:`H` and :math:`\lambda E`  is important in climate / Earth system models because lower  :math:`\lambda E`   implies a lower flux of water vapour to the atmosphere which implies lower cloudiness and rainfall. Lower  :math:`H`  on the other hand tends to cool the planetary boundary layer and reduce convection.


:math:`H` and :math:`\lambda E`  are turbulent heat  fluxes  (see Monteith and Unsworth, 1990, pp. 123-137 for more details), influenced by the turbulence of the airflow in the `planetary boundary layer <http://en.wikipedia.org/wiki/Planetary_boundary_layer>`_, the lowest part of the atmosphere, which is influenced by the aerodynamic roughness of the surface. 

:math:`H` can be represented as a quasi-diffusive process:

.. math:: H = \frac{T_s - T_r}{r_a} \rho c_p


where :math:`T_s` is the surface temperature,  :math:`T_r` is a reference temperature above the surface,  :math:`r_a`  is the aerodynamic resistance ,  :math:`\rho`  is the density of air, and :math:`c_p`  is the specific heat of air. 

The latent heat is a more complex process but can be represented (e.g. Sellers, 1992) as:

.. math:: \lambda E = \left( \frac{e^* (T_s) - e_r}{r_s + r_a} \right)  \frac{\rho c_p}{\gamma}

where :math:`e^* (T_s)` is the saturated vapour pressure at :math:`T_s`, :math:`e_r` is the vapour pressure at a reference height, :math:`\gamma` is the `psychrometric constant <http://www.fao.org/docrep/X0490E/x0490e07.htm#psychrometric%20constant%20%28g%29>`_ and :math:`r_s` is the bulk surface resistance to the transfer of water from the surface to the air. 


.. figure:: http://www.fao.org/docrep/X0490E/x0490e07.jpg
    :align: center
    :width: 50%

*Simplified representation of the (bulk) surface and aerodynamic resistances for water vapour flow* **Source**: `FAO <http://www.fao.org/docrep/X0490E/x0490e06.htm#%28bulk%29%20surface%20resistance%20%28rs%29>`_


The aerodynamic resistance is inversely dependent upon the wind speed and the logarithm of the surface roughness length, which, in turn, is a function of the drag properties of the land surface (Pitman, 2003). 


The roughness length of the surface over vegetated areas is strongly influenced by vegetation height, so if the vegetation is altered or removed the roughness will decrease: a higher roughness length (e.g. over a forest) permits a greater exchange of turbulent heat fluxes for given meteorological conditions than a lower roughness length  (e.g. grass). 

A roughness (positive -- self-enhancing) feedback can exist  if vegetation conditions are altered (e.g. removing forest and replacing with grass):

.. figure:: figures/pitman5.png
    :align: center
    :width: 90%


**Source**: Pitman (2003)

The factors that affect turbulent energy flows between the land surface and the atmosphere also affect fluxes of materials and gases, a significant one being the flux of CO2 between plants and the atmosphere. This can be given as:

.. math::  F = \frac{c_i - c_a}{r_{st} + r_a}


where :math:`F` is the the CO2 flux density (:math:`kg m^{-2}  s^{-1}`), :math:`c_i` is the internal leaf CO2 concentration, and  :math:`c_a` is the ambient CO2 concentration. Here, :math:`r_{st}` is the stomatal resistance (see below), a measure of the difficulty (or ease) for the vegetation to transpire. The stomatal resistance  is not the same as the bulk surface resistance :math:`r_s` above as :math:`r_{s}` includes the resistance to moisture transfer from  the soil and leaf surface. For a crop or grassland, the bulk surface resistance can be estimated as (`FAO <http://www.fao.org/docrep/X0490E/x0490e06.htm#%28bulk%29%20surface%20resistance%20%28rs%29>`_):

.. math::  r_s = \frac{r_{st}}{LAI_{active}}

where :math:`LAI_{active}` is the active (sunlit) leaf area index, and :math:`r_{st}` is the 'bulk' stomatal resistance  of a well-illuminated leaf.  Note that this approximation does not include evaporative fluxes from the leaf surface or soil however: in land surface schemes this is usually treated more carefully and involves explicit calculation of the individual resistance terms that combine to make the bulk surface resistance.



[`Exercise 3 <aside_PM.html>`_]

Following from the considerations of water fluxes above, the water balance can be represented in a LSS:


.. math:: P = E - R_{drain} - R_{surf} - \Delta S

where :math:`P` is water input to the system (precipitation and snow melt generally, but also translocation of water e.g. in irrigation), :math:`E` is evapotranspiration (water from the surface to the atmosphere through evaporation from the soil and leaf surfaces and transpiration from leaves), :math:`R_{drain}` is a *slow* drainage component of water loss from an area, :math:`R_{surf}` is surface runoff, and :math:`\Delta S` is the change in soil moisture storage.

Note the use of :math:`E` here when considering water fluxes, but :math:`\lambda E` above when considering energy fluxes.


A LSS then, implemented as a LSM, models the energy and water fluxes at the land surface and provides an interface of these to atmospheric modelling.
Usually, this will be done for a set of grid cells, where the inputs and outputs of each cell are considered separately. There is potential for a lateral flow of water
between cells due to the runoff terms in consideration of the water balance and also potentially for snowmelt or other water inputs to the cell.

Basic vegetation growth processes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The pedigree of most  models of  vegetation dynamics used to simulate carbon flows in terrestrial ecosystems models (TEMs) comes from attempts to describe the processes controlling crop growth in computer  codes from the 1960s (Bouman et al., 1996) onwards.  Such models express current knowledge of process using mathematical equations and the coupling of these in (computer) simulation models. We will consider crop models then to outline the basic processes involved.

To understand the basic functioning of such models, we can look at the system diagram of Rabbinge (1993):

.. figure:: figures/Rabbinge.png
    :align: center  



    *"The relationship among potential, attainable and actual yield and defining, limiting and growth reducing factors (Rabbinge, 1993)."* Source: Bouman et al., 1996


A set of defining factors (plant type, CO2, radiation, etc.) describe how the vegetation would grow under conditions where it is not limited by water and nutrient constraint. It will of course respond to variations in the environmental conditions (CO2, radiation, temperature). This provides a model of the *potential growth* of the vegetation under these conditions. The *attainable growth* then is the potential growth modulated by some limiting factors such as water or nutrient availabiliy. The *actual* growth then has some further modulation by  pest, disease etc. or when considering carbon stocks perhaps other reducing factors such as grazing.

One might think at first sight that temperature (or even radiation) ought to be a 'limiting' factor, rather than a 'defining' term: if plants have insufficient temperature or light, they will grow 'sub-optimally'. The main conceptual difference is really to do with how the modelling of process takes place. For crops, the 'limiting resources' (water, nitrogen etc.) are things that intervention by the farmer can affect (e.g. irrigation or fertilizers: yield increasing measures in the diagram), so in crop models it makes sense to separate the environmental factors that one has little ability to control once the crop is planted (except by expensive, experimental measures such as CO2 increase in `FACE experiments <http://climatechangescience.ornl.gov/content/free-air-co2-enrichment-face-experiment>`_) and those that are typically employed to improve yield. Further, we can see the *reducing factors* mentioned as things in which the farmer can intervene (yield protecting measures). So, in crop models, we tend to separate the processes in this way and this feeds through into the philiosphy of many of the more general ecosystem/carbon models.

The models we are interested in here are *dynamic*, as the state variables develop as a function of *time*. Many of these models are *hierarchical* because they consider the (eco)system as a hierarchy of organisational units (cell, leaf, canopy etc.) and the model then integrates these lower level processes. We can also call these models *'state variable based'* in that they represent and store the dynamics of some set of weights (state variables, such as leaf area) that are updated at each time step of the system by rate variables (e.g. carbon flux).


One main difference between *crop growth* models and those we will more generally consider in modelling terrestrial carbon are that the focus on the former is on estimating *yield* from the crop, rather than other terms that may be important in carbon modelling such as total CO2 stocks or fluxes. In a general sense though, the structure of most such models is similar.

.. figure:: figures/bouman1.png
    :align: center  



    *"Diagram of the relations in a typical School of de Wit crop growth model (SUCROS) for potential production. Boxes indicate state variables, valves rate variables. circles auxiliary variables, solid lines (arrows) the flow of matter and dotted lines the flow of information."* Source: Bouman et al., 1996 


The diagram above shows a typical crop model structure, although as we have said this is similar for most ecosystem models.

The main state variable here is the *pool* of structural biomass, which is also represented as a set of pools in different plant organs (leaves, stems, roots and storage organs). The fundamental process within such a model then is the production of this pool of stuctural biomass and its allocation to organ pools. The other state variable here is the *development stage* which strongly affects the  allocation rate from the 'structural biomass' pool to the different organs. It also impacts plant *structure* although this is not generally explicitly considered in such models.

The biogeochemical *processes* represented here are photosynthesis, respiration (maintenance and growth) and the development rate which controls the 'stage of development' of the crop. Note that *only* states and processes directly involving the plant are considered in such a crop growth model (i.e. we do not consider what happens to/in the soil).



Some land surface schemes
~~~~~~~~~~~~~~~~~~~~~~~~~~~


**First generation models**

There have been several generations of LSMs. The 'first generation' (Pitman, 2003), from the  late 1960s, treated the basic processes described above and were a major step forward in  climate modelling. These models used simple bulk aerodynamic transfer formulations and tended to use uniform and prescribed surface parameters, including water-holding capacity, albedo and roughness length and had a static representation of vegetation, and tended not to include canopy resistance in estimation of surface resistance.

One other weakness of these models was that they did not really provide a framework for some of the other flux transfers that were found to be important in climate models, such as CO2 flux.

There were various attempts to add complexity to these models, although this was not always done in a systematic way that demonstrated improved model performance from this added complexity (Pitman, 2003). 


.. figure:: figures/pitman8.png
    :align: center
    :width: 90%


**Source**: Pitman (2003)

**Second generation models**

From the late 1970s, new concepts were added to these models such as multi-layer (two initially) representations of soil for moisture and temperature calculations, and the representation of vegetation as a single bulk layer.

.. figure:: figures/pitman9.png
    :align: center
    :width: 90%


**Source**: Pitman (2003)

These models represented the vegetation-soil system as something that interacts with the atmosphere, and had more complex representations of albedo (e.g. splitting the downwelling component into that in visible wavelengths (strongly absorbed by vegetation) and longer wavelengths. A significant advance in these models was the incorporation of  satellite observations (e.g. Sellers et al., 1994). Other advances include: the inclusion of momentum transfer concepts; and some form of explicit biophysical control on evaporation (Pitman, 2003), connecting CO2 uptake and water loss through stomatal opening.

Most of these models then has a representation of stomatal conductance :math:`g_{st}`, the reciprocal of stomatal resistance  :math:`r_{st}` which , based on empirical evidence is generally modelled as:

.. math:: g_{st} = F(PAR) [ f(\delta e) f(T) f(\psi_l)] 

where :math:`PAR` is the 'photosynthetically active radiation', i.e. the downwelling shortwave radiation at visible wavelengths where it is absorbed by plants for use in photosynthesis, :math:`\delta e` is humidity, :math:`T` is temperature, and :math:`\psi_l` is the `leaf water potential <http://en.wikipedia.org/wiki/Water_potential>`_.

Another feature of  these LSSs is their more complex soil moisture parameterisations and the incorporation of relatively sophisticated snow sub-models.


**Third generation LSMs**

One of the major advances of the so-called third generation models, developed in the 1990s and beyond  is their connection of the leaf stomatal conductance and carbon assimilation by leaves. In second generation models, :math:`g_{st}` was only used to model transpiration, but it now became a key concept in estimating canopy photosynthesis, using the approach of Farquhar et al. (1980) and Farquhar and von Caemmerer (1982). Details of this model are dealt with below, but the essentials of the method are some semi-mechanistic model of stomatal conductance from the net leaf  assimilation rate :math:`A_n` and the calculation of math:`A_n` a as the minimum of potential assimilation under different limitations with leaf respiration subtracted.

.. figure:: figures/pitman10.png
    :align: center
    :width: 90%

**Source**: Pitman (2003)

Typical methods for scaling these processes from the leaf to canopy include assuming that leaf nitrogen concentrations (and the photosynthetic enzyme Rubisco) are proportional throughout the canopy  (e.g. Sellers et al., 1992b).

Since carbon assimilation is calculated in these models, it is now possible to consider other canopy processes such as the allocation of carbon to different pools (leaves, wood etc.) and also to consider the turnover of these pools in emitting carbon to the atmosphere  (e.g. accumulation or loss of soil carbon). It also provides the link to *grow* vegetaion dynamically rather than to specify e.g. plant LAI. Thus, these models have the potential to respond to climate change due to e.g. increased CO2 concentrations, as well as variations in water (and to a limited extent, nutrient) availability.

As Pitman (2003) stresses, the most identifiable element of these third generation models is their ability to model carbon.

.. figure:: figures/pitman11.png
    :align: center
    :width: 90%

**Source**: Pitman (2003)

One particular feature one can note is the concentration of national resources into 'national' land surface schemes, perhaps because of the way these models are tied to national meteorological (as well as climate modelling) efforts. Such land surface schemes include `JULES (Joint UK Land Environment Simulator) <http://www.jchmr.org/jules/>`_ in the UK, `Orchidee <http://orchidee.ipsl.jussieu.fr/>`_ in France, and `JSBACH <http://www.google.com.mx/url?sa=t&rct=j&q=jsbach%20model&source=web&cd=1&ved=0CBoQFjAA&url=http%3A%2F%2Fissmes.enes.org%2Fuploads%2Fmedia%2F7Reick_JSBACH.pdf&ei=xwsfT_mAHqm62wX_0sWNDw&usg=AFQjCNHJZDkuqHS-ocmLuvgvtcIvK3XR1A&sig2=c32x1m7jYW0aK3WFmba0hQ&cad=rja>`_ (Jena Scheme for Biosphere Atmosphere Coupling in Hamburg) in Germany.


Summary
~~~~~~~

In this section, we have outlined the main processes in land surface schemes and models and highlighted the interplay of radiation and water.

We have introduced some core concepts in vegetation processes, in the context of crop models and see how vegetation growth can be modelled as a potential amount of carbon assimilation that is then limited by factors such as water and nutrient availability as well as being reduced by pests, disease etc.

We have also traced the development of various land surface schemes, highlighting that the current suite of models importantly incorporates carbon assimilation and allocation and allows dynamic vegetation to be modelled.

Global vegetation modelling
----------------------------

In his course, our focus is on linking measurements from Earth Observation and other sources with models of terrestrial carbon at regional and global scales. The motivation for models here then is to express current understanding of the controls on carbon dynamics as embedded in Earth System  / Terrestrial Ecosystem models. The role of observations is to test and constrain these models to enable: (i) monitoring of terrestrial carbon dynamics; (ii) improved prognostic models. The main focus of the modelling and monitoring is on Net Primary Productivity (NPP).


We can distinguish several types of models : terrestrial biogeochemical models (TBMs) which simulate fluxes of carbon, water and nitrogen coupled within terrestrial ecosystems; and dynamic global vegetation models (DGVMs) which further couple these processes interactively with changes in ecosystem structure and composition (competition among different plant functional types) (Prentice et al.  2001). 

A particular class of models, known as Production efficiency models (PEMs) will be examined here, particularly because they are / can be closely aligned with global observations from satellites. Other than these, we will concentrate on DGVMs as these are the models most commonly used in large LSS modelling efforts.



Dynamic Global Vegetation Models
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Dynamic global vegetation models (DGVMs) seek to model  global biogeochemical fluxes and vegetation dynamics to improve understanding of the dynamics of the terrestrial bioshphere and its interacrions with other components of the Earth system. They are generally *process-based* models, in that they attempt to develop a view of the system by modelling the underlying processes.


.. figure:: figures/dgvm.png
    :align: center
    :width: 50%

**Source:**  `Cramer et al. <http://www.pik-potsdam.de/~kirsten/dgvm_overview.pdf>`_


The main components of a DGVM are: establishment, productivity and competition for resources, resource allocation, growth, disturbance and mortality. DGVMs can be *forced* i.e. run with trends of CO2, climate and land use from observations or *scenarios* or run interactively within climate models to analyse feedbacks.

Clearly many simplifications have to be made to do this sort of modelling at a global scale. This is partly from having to have suitable sets of parameters to describe the processes globally (model parameters) and partly for computational reasons. The trend is to include more complexity as time goes by in these models, as computational resources increase and our understanding of processes and our ability to parameterise the models improves.

The ability to model vegetation dynamics is an important aspect of DGVMs in that it allows for prognostic and paleo use, this also means that the design of DGVMs is geared towards modelling *potential* vegetation. Anthrogenic influences then, such as changes in land use are incorporated by forcing these effects (e.g. prescribing land cover/PFT) on top of the dynamic ('natural' / 'potential') modelling.

DGVMs have been developed from the 1990s in response to the need for models to investigate the responses of vegetation to environmental change at time scales from seconds to centuries and from the local to global scale (Woodward and Lomas, 2004). A non-exclusive list of DGVMs developed in the 1990s and early 2000s is:

*    LPJ - Germany, Sweden
*    IBIS - Integrated Biosphere Simulator - U.S.
*    MC1 - U.S.
*    HYBRID - U.K.
*    SDGVM - U.K.
*    SEIB-DGVM - Japan
*    TRIFFID - U.K.
*    VECODE - Germany
*    CLM-DVGM - U.S.

Peng (2000) provides a useful review of such models as they stood in the year 2000 that students should follow up for background information. 

An overview of the main characteristics of some of the available DGVMs is provided in the table below:

.. figure:: figures/sitch.png
    :align: center
    :width: 90%

.. figure:: figures/sitch2.png
    :align: center
    :width: 90%


.. figure:: figures/sitch3.png
    :align: center
    :width: 90%



**Source**: Sitch et al. (2008)


Plant Functional Types
~~~~~~~~~~~~~~~~~~~~~~~

One important abstraction made in DGVMs is the idea of *plant functional types* (PFTs). This is a way in which global parameterisations can be simplified, by assuming that the responses to resources annd climate of groups of plant types will be similar and so they can be lumped together. It recognises that we cannot model  all plant species at a global scale and is a pragmatic response to this in defining a more limited set of *functional types* that can be grouped together. 

One might try to do this based on a simple *biome* description, but one soon finds that many difficulties arise when considering biomes with complex structures and mixtures, such as savanna or mixed forest where different plants in the biome have very different responses to light, different phenologies etc.

.. figure:: http://www.cgd.ucar.edu/tss/clm/pfts/igbp.gif
    :align: center
    :width: 50%


**Source:** `NCAR <http://www.cgd.ucar.edu/tss/clm/pfts/index.html>`_

.. figure:: http://www.cgd.ucar.edu/tss/clm/pfts/biome-vs-pft.gif
    :align: center
    :width: 50%


**Source:** `NCAR <http://www.cgd.ucar.edu/tss/clm/pfts/index.html>`_


Box (1996) suggests the following requirements for PFTs. They should:

* represent the world's most important plant types;
* characterize them through their functional behavior;
* and provide complete, geographically representative coverage of the world's land areas

and discusses the various schools of thought on how these groupings should be arrived at. 

One set of PFTs arrived at by Box is:

.. figure:: figures/pft.png
    :align: center

**Source:** Box (1996)

Other groupings of PFTs have been used, for instance that suggested by Bonan et al. (2002), one motivation here being linking to land cover classes defined in global land cover datasets supplemented by climatic zoning based on precipitation, and temperature/Growing degree days (GDD, see below):

.. figure:: figures/pft2.png
    :align: center
    :width: 90%

**Source:** Bonan et al. (2002)

Quaife et al. (2008) examined the impact of different land cover schemes for applying the mapping from land cover to PFT:

.. figure:: figures/quaife.png
    :align: center
    :width: 50%


*Proportions (from left to right) of the C3 grass, crop, deciduous broadleaf and evergreen needleleaf Plant Functional Types (PFTs) across Great Britain according to (a) LCM2000 (b) GLC2000 (c) MODIS-BGC (d) MODIS- PFT (e) MODIS-UMD (f) MODIS-IGBP (g) MODIS-LAI/ fAPAR.* **Source:** Quaife et al. (2008)

For context, the values of GPP, NEP and NPP are given for teh UK, assuming the land surface is covered with a single PFT.

.. figure:: figures/quaife2.png
    :align: center
    :width: 80%


Differences in NPP (:math:`gC m^{-2}`) are shown:


.. figure:: figures/quaife3.png
    :align: center
    :width: 50%


so at any location, the impact of land cover uncertainties and the mapping used from land cover to PFT can have a significant impact on model calculations of carbon fluxes (the range of differences in NPP is 133 :math:`gC m^{-2}`).

The current status of these models then includes a set of *parameters* describing vegetation functioning and other characteristics for each of these broad PFT classes, e.g. (`NCAR <http://www.cgd.ucar.edu/tss/clm/pfts/pft-physiology.htm>`_).

There are many criticisms that can be applied to this approach and there are clearly complexities (those to do with the assignment of a particular PFT to a location, and those concerning the parameterisation of a PFT across broad areas for example), but it should be seen as a pragmatic response to the need to run the DGVMs globally. 

One direction that this area of DGVM research is going in is in developing and using `a global plant trait  database: TRY <http://www.try-db.org/pmwiki/index.php>`_  which can allow the sorts of data that field ecologists measure on plant traits to be linked to what could be used in DGVMs (Kattge et al., 2011).  


.. figure:: figures/try.png
    :align: center

**Source**: Kattge et al., 2011

Because of the large number of samples involved, distributions of these traits can now be more fully explored. Early interesting findings include analysis of the fraction of variance explained by PFT or species for key traits:

.. figure:: figures/try2.png
    :align: center

**Source**: Kattge et al., 2011


here, we can see that for example for specific leaf area (SLA, one-sided leaf area per leaf dry mass) about 40% of the variation in SLA that exists in the database occurs between PFTs, also the variation in the mean between PFTs is similar to the within PFT variation for this trait. 

.. figure:: figures/try3.png
    :align: center

**Source**: Kattge et al., 2011

The figure above shows frequency distributions of SLA for different PFTs. For some (e.g. needle leaf deciduous) the distribution is quite narrow (but a relative small sample number here) but for most, it is wide. Interestingly, the figure also shows the values of SLA used in different global vegetation models (in red) showing the very wide range of values assumed across different models.  

How 'good' are these models?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Prentice (2011)  <http://www.pik-potsdam.de/news/events/greencyclesii/programme/20.5.2011/prentice/index_html>`_ provides a critique of current efforts in DGVMs, where he argues particularly for more/better model benchmarking. This can be done by comparing model outputs (not just carbon stocks and fluxes, but other measures such as vegetation greennesss or runoff) with *measurements*. A significant internation effort to coordinate such benchmarking is the International Land Model Benchmarking - `iLAMB <http://www.ilamb.org/>`_.

Our current understanding of how good these models are comes from sources such as the Carbon-Land Model Intercomparison Project - `C-LAMP <http://www.climatemodeling.org/c-lamp/>`_ which included an analysis of the biogeochemical models CASA', CN (Randerson et al., 2009). Among these models, global carbon sinks for the 1990s differed by a factor of 2, and the magnitude of net carbon uptake during the growing season in temperate and boreal forest ecosystems was under-estimated, probably due to delays in the timing of maximum LAI. In the tropics, the models overestimated carbon storage in woody biomass based on comparison with datasets from the Amazon.

Another source of information is straight model intercomparisons such as  that of Sitch et al. (2008) which performed an intercomparison of five DGVMs. Whilst such work does not include much comparison with measurements, they are useful for understanding the agreement and divergence of current DGVMs under future climate scenarios.

One comparison in this study was with the best current estimates of global land carbon budgets for the 1980s and 1990s:

.. figure:: figures/sitcht2.png
    :align: center
    :width: 90%

**Source**: Sitch et al. (2008)

Major findings are:

* All models estimates are within the range of current knowledge of these budgets and relatively close to the mean IPCC values. The models were also in general agreement about the cumulative land uptake over the last 50 years.
* They also simulated the correct sign of response to ENSO events but differed markedly in magnitude.
* All five DGVMs have similar response of productivity to elevated atmospheric CO2 in agreement with field observations
* The DGVMs are in less agreement in the way they respond to changing climate.
* All models suggest a release of land carbon in response to climate, implying a significant positive climate-carbon cycle feedback in each case. This response is mainly due to a reduction in NPP and a decrease in soil residence time in the tropics and extra-tropics, respectively.

.. figure:: figures/sitchf3.png
    :align: center
    :width: 90%

**Source**: Sitch et al. (2008)

.. figure:: figures/sitchf3a.png
    :align: center
    :width: 90%

Zoom in of lower right panel of above. **Source**: Sitch et al. (2008)

We see, for example significant scatter on the year to year responses of the models when considering the land-atmospherie carbon exchange, particularly for ENSO years, although the general trends are similar (hence the level of agreement noted above for decadal or longer integrals).

.. figure:: figures/sitch9.png
    :align: center
    :width: 90%

**Source**: Sitch et al. (2008)

Significant disagreement exists between the models on NPP response to climate in the tropics and soil respiration response to climate in the extra-tropics. In the above figure we see the NPP response to elevated CO2 and the sensitivity of some other terms to temperature.

Uncertainty in future cumulative land uptake associated with land processes is large and equivalent to over 50 years of anthropogenic emissions at current levels.

We can see from these various analyses that whilst there are certain (important) areas of agreement among the current DGVMs, significant uncertainty remains in iestimating current carbon budgets and predicting future ones. Improvements in these models is of great importance to understanding possible climate changes and impacts.


Summary
~~~~~~~

In this section, we have noted that the two main types of model we are interested in are DGVMs and PEMs.

We have outlinedsome of the main features of DGVMs and discussed some of the concepts they employ, such as PFTs. 

We have also considerd how we can tell how good these models are.

Production efficiency models
-----------------------------

Overview of the 'Monteith' approach
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the production efficiency approach to modelling NPP (or GPP) (the 'Monteith' approach, (Monteith, 1972, 1977)), a linear relationship is assumed between (non limited) canopy photosynthesis and absorbed PAR (Photosynthetically Active Radiation, i.e. the amount of shortwave radiation that is absorbed by the canopy).


.. math::

    GPP  = PAR \times   f_{PAR}  \times  (\epsilon \times  C_{drm}) \times  scalars


.. math::

   NPP = GPP - R_a


Here, :math:`GPP` is the Gross Primary Productivity (:math:`g C m^{-2}`), :math:`\epsilon` is the 'light use efficiency' (LUE)  (g dry matter per MJ PAR), :math:`C_{drm}` is the carbon content of dry matter (0.45 :math:`gC g^{-1}`), :math:`f_{PAR}` is  the fraction of PAR absorbed by the canopy (also known as fAPAR), and :math:`PAR` is Photosynthetically Active Radiation (:math:`MJ m^{-2}`) or the downwelling shortwave radiation multipled by the the PAR fraction  of direct and diffuse illumination taken together. 

The :math:`scalars` represent multiplicative  environmental constraints that are typically meteorologically derived (i.e. limiting factors).

:math:`NPP` is the Net Primary Productivity (:math:`g C m^{-2}`) and :math:`R_a` is the autotrophic respiration (:math:`g C m^{-2}`).

The obvious attraction of this approach is that it is simple and that it caputures the 'main effect' that carbon assimilation increases with increasing PAR absorption in the absence of limiting factors (including such limits as scalars). An additonal (strong) attraction that we shall see is that fAPAR is potentially accessible from satellite data, so a major part of the model can be friven by observations globally.

Although such a linear relationship between PAR and photosynthesis does not exist at the leaf level, at the canopy level it is generally observed and can be a reasonable and simple model of GPP.

For crops (with sufficient nutrients and water) the LUE can remain constant over the full range of light intensity. For other vegetation types such as forests, it can be more complex and depend on other factors such as species, stand ageand  soil fertility.

A useful review of some of the major current PEMs and  an analysis of some of their deficiencies is provided by McCallum et al. (2009).

They review six PEMs (see McCallum et al. for brief descriptions of the unique features of each of the models):

.. figure:: figures/mccallum1.png
    :align: center

    **Source**: McCallum et al. (2009)

LUE is often assumed constant in these models, e.g. constant globally in CASA or per biome via a land cover map as in MOD17. GLO-PEM does not assume a constant LUE.

Although all models make use of satellite data (primarily in the estimation of fAPAR), most also require climate data (for APAR and to drive limiting scalars). Only GLO-PEM runs on only satellite data (with the exception of attribution of C3 and C4 plants). 

As we shall see in a following lecture, satellite-derived fAPAR is essentially an 'measurement' (though it is not actually a direct measurement). It is of necessity an estimate of fAPAR at the time of the satellite overpass and under the atmospheric  conditions  of the 'measurement'. Since the conditions need to be clear of clouds for measurement, it may be thought of as being primarily a clear sky, or direct-radiation dominated measure. It is known that under diffuse conditions, the capacity of a canopy to absorb shortwave radiation (i.e. the  fAPAR) tends to be higher, particularly for forest canopies. Do, even though the PAR may be lower under diffuse/cloudy conditions, the fAPAR may be higher than the 'clear sky' fAPAR.

Key findings of the review by McCallum et al. are:

* LUE should not be assumed constant, but should vary by PFTs
* Results are strongly dependent on the climate drivers used for particular models (which also complicates intercomparison)
* Further use of satellite data iwould alleviate the need for many or all climate drivers.
* PEMs should consider incorporating diffuse radiation, especially at daily resolution 
* PEMs should also consider the need to account for GPP saturation when radiation is high

Cramer et al. (1999) compared seventeen global models of NPP, including PEMs and mechanistic models. 

.. figure:: figures/cramer19991.png
    :align: center
    :width: 90%

.. figure:: figures/cramer19992.png
    :align: center
    :width: 90%

    **Source**: Cramer et al. (1999)

There was broad general agreement among the models in global seasonal variations in NPP (range of variation around 50% of the lowest value with two outliers excluded), and generally quite low coefficient of variations of NPP spatially, except for a few areas.

.. figure:: figures/cramer19993.png
    :align: center
    :width: 90%

.. figure:: figures/cramer19994.png
    :align: center
    :width: 90%

    **Source**: Cramer et al. (1999)

.. figure:: figures/cramer19995.png
    :align: center
    :width: 90%

    **Source**: Cramer et al. (1999)

These results are claimed to be 'relatively good' considering this is a relatively poorly understood variable,and one thing the study highlights is degree of our current uncertainty of this quantity. Within this range of spread then, the PEMs performed no more poorly than other models and PEMs should be considered a viable semi-independent approach for NPP monitoring.


Summary
~~~~~~~~

An overview of the PEM approach is presented. The key idea here is that non-limited carbon assimilation can be assumed a linear function of the capacity of a canopy to absorb shortwave (specifically PAR) radiation and the amount of downwelling PAR. 

These models are particularly useful as they can be largely driven by observations (or rather fAPAR, derived from satellite observations).

Several key issues in the use of such models are highlighted, but these models seem to perform 'quite well' in comparison to mechanistic approaches.

Since these models are driven by observations, they cannot directly be used in prognostic mode.



Phenology
-----------

Crop Phenology
~~~~~~~~~~~~~~~
In a broader sense, we see the idea of *development stage* mentioned above for  crops as simply one way of representing the plant `phenology <http://en.wikipedia.org/wiki/Phenology>`_. In crop models, this is usually quite detailed. One example of this is the `Zadok <http://www.fao.org/DOCREP/006/X8234E/x8234e05.htm>`_ scale:



.. figure:: http://www.fao.org/DOCREP/006/X8234E/x8234e04.jpg
    :align: center


"the external Zadoks stages of the plant (red) and the two internal stages, double ridges and terminal spikelet (check the vertical text). It shows when the shoot components are initiated, grow and die (green boxes) and when the yield components are formed (bars)".* Source: `FAO <http://www.fao.org/DOCREP/006/X8234E/x8234e05.htm>`_

This describes the 'timing' (or rather sequencing) of the different stages of growth of a crop such as wheat. This sort of scale and diagram is useful for farmers in understanding and modellers in expressing the allocation of resources in the crop and when yield is determined.  


A simplified version of a crop phenology model involves the following phases:

**Germination**

Seed germination has a strong temperature dependence in crops. The duration of this phase is usually expressed then as the time over which the sum of `growing degree days (GDD) <http://en.wikipedia.org/wiki/Growing-degree_day>`_ must reach some threshold value. GDD is useful  for understanding some other stages of development. 

.. figure:: http://upload.wikimedia.org/wikipedia/en/math/e/d/b/edb99f9b6612dc70d600b3f74c2f5d58.png
    :align: center


The GDD for a particular day is  usually modelled as the mean of the minimum and maximum temperature minus some base temperature (typically 10 C). This is then summed over time from planting and, in the absence of other 'stress' factors (e.g. lack of water or pests) will be characteristic of the length of the germination period.


**Initial spread**

During this phase, the production of biomass is dependent on the proportion of radiation intercepted by green leaves, in the absence of other stress factors. The amount of biomass production per unit ground area then is a function of leaf area index (LAI, one sided leaf area per unit ground area, dimensionless (:math:`m^2 m^{-2}`)). LAI is the product of the leaf biomass pool per unit area (in kg m-2) and the specific leaf area  (SLA, one-sided area of a fresh leaf divided by its oven-dry mass, expressed in :math:`m^2 kg^{-1}`) assuming SLA constant over the plant.  As LAI growth then, the rate of biomass production increases so biomass production is close to exponential.

**Full coverage** 

When the canopy reaches full coverage, adding more leaf area does not greatly increase the radiation intercpetion so growth is dependent more strongly on incident radiation and respiration rate. Some plants (crops especially)  then switch resource allocation from leaf production to generative growth or storage.

**Allocation to storage organs** 

In this stage, biomass allocation goes into storage organs. Whilst the leaves remain intact the biomass production rate will be similar to the previous phase.

**Ripening** 
Although in many crops leaves continually die as new ones are produced at the top of the canopy, in the ripening phase, biomass production is essentially terminated as all leaves senesce and no new ones are produced.

Phenology
~~~~~~~~~~


.. figure:: http://www.uwgb.edu/biodiversity/phenology/arbo_seasons2009_04gf_canopy120.jpg
    :align: center

.. figure:: http://www.uwgb.edu/biodiversity/phenology/arbo_seasons2009_02gf120.jpg
    :align: center

Images of forest phenology. **Source**: `UWGB <http://www.uwgb.edu/biodiversity/phenology/>`_

All plants, to some extent experience daily and seasonal variations in environmental conditions. Plants then tend to adjust their behaviour to  these variations. There are diurnal variations in light, temperature and water. Many plants then exhibit `cirdadian rhythms <http://en.wikipedia.org/wiki/Circadian_rhythm#In_plants>`_ (24 hour cycles) for example in stomatal opening (Chapin et al., 2002 Ch. 6).

Plants in temperate climates experience strong seasonal variations in environment and generally exhibit a predictable pattern of phenology: they put more resources into leaf production at certain times, flowers at others etc. Often this is  a response to `photoperiod <http://en.wikipedia.org/wiki/Photoperiodism>`_ where e.g. leaf `senescence <http://en.wikipedia.org/wiki/Plant_senescence>`_ begins and photosynthesis is reduced when day length is reduced or other environmental factors give cues to the onset of winter. To prepare for this, plants will tend to shift resources (nutrients, carbohydrates, water) from leaves  to other organs to prevent their loss from the plant.  These resources can then be used to initiate growth in the next season.

This 'phasing' by plants covers many aspects of plant growth and development, for instance allocation rates. When carbohydrates are produced in primary production, they are allocated to different pools (leaves, roots, wood etc.). Different plants have different patterns of allocation, e.g. deciduous or annual plants must allocate to leaf (for light) and roots (for water and nutrients)  production early on, but evergreen plants already have leaves and so can put more resources into root production in the early season. When the growing season is short (e.g. Arctic tundra) storage of resources form one season to more rapidly start photosynthesis in the next season become more important.



**Tissue turnover**

Although plants gain carbohydrate through photosynthesis, they must also use some of it for respiration to maintain current organs and mechanisms and also for new growth.  In the previous lecture we saw that the balance between these gives what we call the net primary productivity. If this starts to become negative (i.e. it *costs* more to the plant to keep some organs  such as leaves that they contribute to photosynthesis) then it can be advantageous for plants to  lose biomass e.g. by shedding leaves. This is an important mechanism for plants as it gives then *control* over this balance. 

`Senescence  <http://en.wikipedia.org/wiki/Plant_senescence>`_  is the programmed breakdown of tissues in a plant which allows plants to reduce the impact of e.g. unproductive leaves. One upshot of this is that it allows plants to *explore* new space. For example, in grasses a relatively constant rate of leaf senescence allows maintenance costs associated with lower (early) leaves to be reduced as new leaves are produced higher in the canopy. 

There is a danger of the loss of important resources (e.g. nutrients) when shedding leaves or other organs. Plants therefore tend to transfer soluble nutirents out ofsenescing tissue (`resorption <http://www.sciencedirect.com/science/article/pii/S0378112708000145>`_) and are able to maintain around half of the phosphorus, nitrogen and potassium from leaves at senescence (Chapin, 1992, Ch. 8).

It is interesting to note the relationship between Nitrogen Use Efficiencey (NUE), the ratio of dry mass to nitrogen in litter fall (Chapin et al., Ch. 8) and the nitrogen lost in litterfall:

.. figure:: figures/ChapinCh8-1.png
    :align: center
    :width: 50%

*"Relationship between the amount of nitrogen in litterfall and nitrogen use efficiency (ratio of dry mass to nitrogen in that litterfall). Each symbol is a different stand, including conifer forests (C), temperate deciduous forests (D), tropical evergreen forests (T), mediterranean ecosystems (M), and temperate forests dominated by nitrogen fixers (N). Redrawn from Vitousek (1982)."* Source: Chapin et al. 2002 , Ch. 8

Plants on less fertile soils tend to be more efficient at using nitrogen than those on more fertile soils.  NUE cab be  increased by reducing tissue turnover times (e.g. keeping leaves longer: so plants with lower leaf turnoverand higher NUE have a competitive advantage in nutrient poor soils) but this tends to imply a trade-off with the capacity to capture nutrients and carbon (Chapin et al. 2002 , Ch. 8) so is not a universal advantage.

Another part of the value of senescence is that it allows plants to shed parasites, pathogens and herbivores. By shedding leaves and roots then, then plants can respond to such *attacks* if their impact is likely damaging.

Other episodic factors that  lead to loss of biomass  include fire, wind storms etc. Whilst these can lead to severe impacts and nutrient losses to a plant, they also play a wider role in the ecosystem e.g. by providing gaps in a canopy or increasing heterogeneoity of nutirent resources (Chapin, 1992, Ch. 6).


Mechanisms of phenology and evidence of changes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


**extratopics**

We have seen above that temperature and photoperiod (day length relative to night length) are important concepts for plant growth and development and it is harly surprising that phenology is generally controlled by these environmental cues.

Using photoperiod as well as temperature is particularly important in humid extratropical areas where there are large temperature fluctuations from year to year  as it stops plants picking up on temperature at the 'wrong' time of year (Korner and Basler, 2010).

Because the photoperiod is  the same in winter and autumn, plants need a cue that winter is over. This is often obtained from the dose of low temperatures experienced by the plant, and amounts to a 'chilling' requirement by some plants before spring bud burst (Korner and Basler, 2010. The 'phasing' of the signals seems to be: chilling requirement which enable photoperiod sensitivity, then response to temperature.i For plants that have a chilling requirement then, bud break can be delayed by mild temperatures.

.. figure:: figures/chilling.png
    :align: center

    **Source**: Korner and Basler  2010



Burrows et al. 2011 analysed global temperature trends over the period 1960-2009 and have noted the  following patterns of advance in Spring temperatures and delay in autumn temperatures. 


.. figure:: figures/b1.png
    :align: center
    :width: 50%

.. figure:: figures/b2.png
    :align: center
    :width: 50%

"Seasonal shift (days/decade) is the change in timing of monthly temperatures, shown for April (top), representing Northern Hemisphere spring and Southern Hemisphere fall and October (bottom): positive where timing advances, negative where timing is delayed. Cross-hatching shows areas with small seasonal temperature change (<0.2 C/month), where seasonal shifts may be large." **Source**: Burrows et al. 2011

Plant responses to such climatic variables means that phenology is likely to change under climate change, and there is already much evidence for this.

.. figure:: figures/defilia.png
    :align: center

    **Source**: Defilia and Clot, 2005

Our evidence for phenological changes comes from a combination of ground observations of this sort, flux towers,  and satellite observations.

Until relatively recently there has been  little work linking these two sources of information, partly due to a spatial paucity of ground data until recent years and partly because of complexities in matching the scales of the observations (Liang et al., 2011; Studer et al., 2007; White et al., 2009).

A useful `white paper on phenology by Friedl et al. is available here <http://www.google.com.mx/url?sa=t&rct=j&q=phenology_friedl_whitepaper.pdf&source=web&cd=1&ved=0CCEQFjAA&url=http%3A%2F%2Flandportal.gsfc.nasa.gov%2FDocuments%2FESDR%2FPhenology_Friedl_whitepaper.pdf&ei=yZAhT5HBM8WIsQK5lcygCQ&usg=AFQjCNEEl8ElupuBrnXcbM1qeuLGRdIJew&sig2=A3oSgEAXaQc3AwYJKQJY5A&cad=rja>`_.


Models of phenology
~~~~~~~~~~~~~~~~~~~~

**Logistic function of time**

One of the most simple models for tracking phenology that has been extensively applied to satellite data is a logistic function of time:

.. math:: y(t)  = \frac{c}{1 + e^{a + bt}}+d

This is used for instance by Zhang et al., 2003 for tracking the dynamics of MODIS vegetation index data. The model is fitted to the VI data and transition date metrics calculated:

.. figure:: figures/zhang1.png
    :align: center

.. figure:: figures/zhang3.png
    :align: center

    **Source**: Zhang et al., 2003

Such processing provides valuable spatial datasets of information related to phenology:

.. figure:: figures/zhang.png
    :align: center

    **Source**: Zhang et al., 2003
 
and alows the tracking of dynamics of the phenology metrics over time. Generally a model of this sort is used to derive *data* that are then used to model phenology.

**(Growing) Degree day model**


The simplest form of model that can be used prognostically then is a simple GDD model. Note that such models are only appropriate where temperature is a limiting factor in plant growth (the extratopics). Note that this does not include any account of chilling days or photoperiod.  In this, approach some phenological metric such as spring greenup is used to calibrate parameters of a GDD model. The model can be phrased as:


.. math:: GDD = \sum_{T>T_{base}} (T - T_{base})

where :math:`T_{base}` is a base or 'critical' temperature and :math:`T` is the air temperature (C) (e.g. at 2 m).

Some options exist after this point for implementation of such a model. They key is to identify  some threshold value of GDD :math:`F^*` that corresponds to the metric of interest. Most typically this is simply a GDD threshold. The sum of GDD generally starts from 1 January for the Northern hemisphere and 1 July for the Southern hemisphere to act as a consistent baseline.


Sobrino et al.. (2011) used a double logistic function of the same form for mapping changes in spring date timing trends for global vegetation:

.. figure:: figures/sobrino.png
    :align: center

    **Source**: Sobrino et al.. (2011)

Another approach is to use day of year (DOY) as a additional model parameter. Fisher et al. (2007) for example allow the GDD threshold to vary spatially but attempted to calibrate a model where the starting DOY of the summation and the base temperature were constant over a wide area. An interesting feature of that study is its consideration of  some of the complexities in using satellite data for phenology modelling. They compared  a calibration of a spring warming model for predicting the date of half maximum greenness, calibrated with satellite data over deciduous forests in New England. Whilst a calibration of the model was achieved:

.. figure:: figures/fisher.png
    :align: center

    **Source**: Fisher et al. (2007)

a comparison with a null model (i.e. using mean values) against the model driven with climatological data showed little improvement over the use of the model.  

A more detailed analysis of the data showed that it was not the model *per se* at fault, but thecalibration and application of it to a broad PFT.  They found that when the model was applied  at a more specific level (northern (beech- maple-birch) and central (oak-hickory) hardwood forests)  different responses to climate were observed and conclude that conclude that spatial location and species composition are critical factors for predicting the phenological response to climate change.

.. figure:: figures/fisher2.png
    :align: center
    :width: 90%

    **Source**: Fisher et al. (2007)

Generally, satellite observations based on visible and near infrared wavelengths are used for monitoring phenology, but Picard et al. (2005) used an uindex based on near infrared and middle infrared which is more sensitive to water content that vegetation greeness. 
This was found to  be particularly useful for the study area (Siberia) as the metric used (NDWI) decreases during snowmelt then increases around the date of bud burst.


**models including chilling**

Picard et al. (2005) outline three main approaches for including chilling effects in bud burst models along with other focings (mainly temperature):

* sequential models: forcing only starts when the chilling requirement is met
* parallel models:  chilling and forcing accumulated in parallel and critical values then applied to both
* alternating models: the temperature :math:`F^*` is a decreasing function of chilling.

.. figure:: figures/picard.png
    :align: center

    **Source**: Picard et al. (2005) 

They found that uncertainty from the bud burst date calibration had an impact of only around  8% of mean NPP, and suggest that the calibrated model is accurate enough for carbon budget calculations.


**tropics** 

In tropical areas, simulating and understanding phenology is complicated (Bradley et al., 2011) as in places like the Amazon temperature is generally not thought to be limiting. Rather then, water availability is often more of a control when there is a strong seasonal cycle in precipitation. This is not a simple response however because trees with deep roots may have access to water reserves and show no pronounced annual variation. 

There is evidence of enhanced tree mortality and decrease in growth however when Amazonian rain forests are exposed to a longer and more intense moisture deficit than normal (Phillips et al., 2009).

The state of phenology models in DGVMs for tropical areas  then is at present rather weak and an area of active research.

**Phenology in DGVMs**

Unsurprisingly, phenology in DGVMs is more complex that just the determination of bud burst. In `JULES <http://www.jchmr.org/jules/science/vegetation.html>`_ for example, it is dealt with in terms of a leaf mortality rate that is assumed to be a function of temperature. Other rules such as a constant rate of dropping leaves are implemented when the daily mean value of leaf turnover reaches twice its minimum value. In JULES budburst occurs  at the same rate when leaf mortality drops back below this threshold. This then is a form of temperature dependence similar to those outlined above with an implict chilling requirement, but the parameters are clearly not the same as those considered above.

Clark et al. 2011  describe this in more detail. It is found that the model described above is not sufficient to produce realistic vegetation phyenology and so a variable :math:`p` is introduced that describes the phenological status of the vegetation as the ratio :math:`LAI/LAI_{max}` where :math:`LAI` is the current LAI and :math:`LAI_{max}` is the seasonal maximum LAI.

Summary
~~~~~~~

Vegetation phenology is seen to be an important concept in monitoring, modelling and understanding vegetation dynamics and its response to climate variations. There is a growing amount of observational data on phenology at various scales and more recent attempts to reconcile measures at different scales. 

It is likely that for some areas  at least, species specific (or slighly broader groupings of species) parameterisations of phenology need to be considerdd rather than just broad PFT definitions.

Most phenology analysis is done using simple degree day models, although some analyses also consider chilling requirements.

Phenology models in DGVMs may be phrased rather differently to those used in most analyses. Whilst maintaining a required 'mechanistic approach', current DGVM phenology models are not entirely satisfactory.

Modelling photosynthesis
------------------------

Overview of the 'Farquhar' approach
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the 'Farquhar' approach (Farquhar et al. 1980), the non-limited photosynthetic rate :math:`A_0` is calculated for a fixed value of intercellular CO2 concentration :math:`C_{i,0}` (Knorr, 1998). The actual carbon assimilation rate :math:`A:` at the leaf level depends on the actual  intercellular CO2 concentration :math:`C_{i}`. For the C3 pathway it is calculated as a function of the electron transport limited rate :math:`J_E` and a carboxylating rate :math:`J_C` controlled by the enzyme Rubisco (units :math:`mol(CO_2)m^{-2}s{-1}`) and the leaf 'dark' respiration rate :math:`R_d`:

.. math::

    A = min\{J_C ; J_E \} - R_d


where:


.. math::
    
    J_C = V_m \frac{C_i-\Gamma_{*}}{C_i+K_C(1+\frac{O_x}{K_O})}

    J_E = J \frac{C_i-\Gamma_{*}}{4(C_i-2\Gamma_{*})}



.. figure:: figures/chapin1.png
    :align: center
    :target: figures/chapin1.png

*"Relationship of net photosynthetic rate to photosynthetically active radiation and the processes that limit photosynthesis at different irradiances. The linear increase in photosynthesis in response to increased light (in the range of light limitation) indicates relatively constant light use efficiency. The light compensation point is the minimum irradiance at which the leaf shows a net gain of carbon."* **Source**: `Chapin, 2011, PTEEChap5.ppt, fig. 5.5 <http://sites.google.com/a/alaska.edu/f-stuart-chapin-terry/home/powerpoints-principles-of-ecosystem-ecology>`_


.. figure:: http://www.johnmorris.com.au/files/images/licor/li6400xt%20co2%20response%20curves.jpg
    :align: center
    :target: http://www.johnmorris.com.au/Photosynthesis-Analysers/LI-6400XT-Portable-Photosynthesis-System.aspx?pd=25369&CategoryID=12

*"Figure of the photosynthetic response to increasing CO2. Glycine max (soybean) leaf was excised from experimental-garden grown plant and then light acclimated at 1500 µmol m-2 s-1 (saturating) in a lab. Experimental data (circles) was modeled using the equations of Farquhar, von Caemmerer and Berry (1980) for maximum velocity of carboxlation (VCmax, black line) and the maximum electron transport rate for RuBP regeneration (Jmax, cyan line). The intercellular CO2 (Ci) at which photosynthesis transitions from VC-limited to J-limited is 216 µmol CO2 mol-1 air. Stomatal limitation to photosynthesis (l ) is the effect of the stomata resistance restricting photosynthesis decreasing CO2 available for photosynthesis at growth CO2 concentration."* **Source**: `johnmorris.com <http://www.johnmorris.com.au/Photosynthesis-Analysers/LI-6400XT-Portable-Photosynthesis-System.aspx?pd=25369&CategoryID=12>`_

Here, :math:`\Gamma_{*}` (:math:`mol(CO_2) mol(air)^{-1}`) is the CO2 compensation point without leaf respiration, :math:`K_C` is the Michaelis-Menton constant for CO2 (:math:`mol(CO_2) mol(air)^{-1}`), :math:`O_x` is the oxygen concentration (0.21 :math:`mol(O_2) mol(air)^{-1}`), :math:`K_O` is the Michaelis-Menton constant for O2 (:math:`mol(O_2) mol(air)^{-1}`), and :math:`J` is  the electron transport rate:


.. math::

    J = \frac{\alpha I J_{max}}{\sqrt{J_{max}^2 + \alpha^2 I^2}}


with :math:`I = I_{PAR}/E_{PAR}` where :math:`I_{PAR}` (:math:`Wm^{-2}`) is the PAR absorption rate :math:`E_{PAR}` the energy content of PAR quanta (220 :math:`kJ mol^{-1}`), :math:`J_{max}` the maximum electron transport rate, (:math:`mol(CO_2) m^{-2} s^{-1}` and :math:`\alpha` the efficiency of photon captupre (0.28).

The 'Michaelis-Menton' constants depend on vegetation temperature (:math:`T` in :math:`K`):


.. math::

    K_C = K_{C,0} exp(\frac{E_C }{R T} \frac{T_0}{T_1})

    K_O = K_{O,0} exp(\frac{E_O} {R T} \frac{T_0}{T_1})


where :math:`K_{C,0}` and :math:`K_{O,0}` are the maximum Michaelis-Menton values for CO2 and O2 respectively :math:`460 x 10^{-6} mol(CO_2) mol(air)^{-1}` and :math:`330 x 10 ^{-3} mol(O_2) mol(air)^{-1}`), :math:`E_C` is the activation energy for :math:`K_C` (:math:`59396 J mol^{-1}`), :math:`E_O` is the activation energy for :math:`K_O` (:math:`35948 J mol^{-1}`), :math:`T_1` is 25 :math:`C` in `K` (i.e. 25 + 273.15)  and :math:`T_0` is the vegetation temperature relative to 25 :math:`C` (i.e. :math:`T - T_1`). :math:`R` is the gas constant (8.314 :math:`J mol^{-1} K^{-1}`).

The maximum electron transport rate :math:`J_{max}` is modelled as the electron transport rate  :math:`J` at 25  :math:`C` with a temperature dependence. :math:`J` at 25  :math:`C`  is modelled as :math:`J_0 * NSCL`  where :math:`NSCL` is a Nitrogen scaling factor at maximum carboxylation rate and maximum electron transport rate.

.. math::

    J_{max} = E_{transport}  * NSCL * (T - 273.15)/25.


This is the basic model of photosynthesis used in most DGVMs (with some variations).


Stomatal conductance
~~~~~~~~~~~~~~~~~~~~~

Plants regulate CO2 uptake and water loss through the regulation of the size of stomatal openings (mainly in leaves). The stomatal conductance, the reciprocal of stomatal resistance, is the flux of water vapour or CO2 per unit driving force. The usual interpretation is that when plants decrease stomatal  conductance (increase resistance) to minimise water loss, photosynthesis declines redcuing the efficiency at which plants convert light to carbohydrates (Chapin et al., 2002).

.. figure:: figures/stomata.png
    :align: center
    :target: figures/stomata.png
    :width: 50%

.. raw:: html

    <centre>
    "Cross-section of a leaf, showing the diffusion pathways of CO2 and H2O into and out of the leaf, respectively. Length of the horizontal arrows outside the leaf is proportional to wind speeds in the boundary layer" </i>Source: <a href="http://sites.google.com/a/alaska.edu/f-stuart-chapin-terry/home/powerpoints-principles-of-ecosystem-ecology">Chapin, 2011, PTEEChap5.ppt, fig. 5.18</a>
    </centre>

Jones (1998) reviews and criticises models of stomatal control of photosynthesis and transpiration. A number of possible (not necessarily exclusive) hypotheses for the role of stomata are considered in the various approaches. These include:

* stomata operate in such a way as to minimize water loss relative to the amount of CO2 uptake  (as above)
* the prime role of stomata might be to avoid damaging plant water deficits (e.g. avoidance of `cavitation <http://www.mcnallyinstitute.com/01-html/1-3.html>`_)
* stomatal control of transpiration has a role in maintaining leaf temperature within an optimal range

The hypotheses one puts forward about the potential role (or roles) of stomatal dynamics clearly have the potential for influence on conclusions one might draw about future climates, as these hypotheses lead to particular model forms being used in TEMs.

.. figure:: figures/jones.png
    :align: center
    :target: figures/jones.png


Source: Jones 1998

Understanding the control of stomata is complicated because of the various feedback mechanisms involves (figure above).

There are a number of models available to describe the response of leaf stomatal conductance (G, mm s-1 or sometimes mmol m-2 s-1). This include the empirical model of Jarvis (1976) which requires a large number of parameters  through to semi-empircal approaches such as that of Jones (1983).

Despite such debates, most TEMs seem to use semi-empircal approaches to modelling stomatal conductance as a compromise between complexity and the number of parameters and other mechanisms required.  Typical of these is  the approach used in the Bethy model (Knorr, 1997) and the subsequent `JSBACH model <http://www.mpimet.mpg.de/en/wissenschaft/land-im-erdsystem/globale-vegetationsmodellierung/jsbach-publikationen.html>`_, as well as the Triffid model (`Cox, 2001 <http://www.google.com.mx/url?sa=t&rct=j&q=triffid+cox&source=web&cd=9&ved=0CF0QFjAI&url=http%3A%2F%2Fwww.met.rdg.ac.uk%2Fphdtheses%2FThe%2520Dynamic%2520Response%2520of%2520the%2520Global%2520Atmosphere-Vegetation%2520coupled%2520System.pdf&ei=BxAXT-DLCYqasgL9wa34AQ&usg=AFQjCNGWDnCKZmUmVP6W8AMBI29evjUW2g&sig2=lpAlozDG7byM8_VJ-4VKug&cad=rja>`_) and the subsequent `JULES <http://www.google.com.mx/url?sa=t&rct=j&q=triffid%20jules&source=web&cd=1&ved=0CBoQFjAA&url=http%3A%2F%2Fwww.jchmr.org%2Fjules%2Fmedia%2Fmeetings%2F2008-01%2F2008_Fisher_TRIFFID.pdf&ei=fxAXT-6BDcOJsAKKrPn_AQ&usg=AFQjCNFUy2x03kHHWuUhyT1TC9_wEIlZQg&sig2=HiioZqjqgTz8XFqQj_k-RA&cad=rja>`_ implementation, following Jones, 1983 for *maximum* (i.e. unstressed) *canopy* stomatal conductance, *Gc0* (Knorr, 2000):

.. figure:: figures/knorr1.png
    :align: center

which is considered a function of leaf temperature (Tk, K), non-water-limited net leaf CO2 uptake rate(Ac0, umol m-2 s-1), Ca the atmospheric CO2 concentration (355 umol(CO2)/mol(air)) and standard non-stressed leaf- internal CO2 concentration, (Ci,0). R is the gas constant (8.3145 J/mol K, so units: kg m-2 s-2 mol-1 K-1), and p is the air pressure of the standard atmosphere (Pa, i.e. kg m-1 s-2), so that Gc0 is given in m/s (Knorr, 2000). The factor of 1.6 accounts for the different molecular diffusivities of water and carbon dioxide.


In Triffid, Ci0 is assumed a function of internal partial pressure of CO2 and the leaf surface humidity deficit:

.. figure:: figures/triiffid1.png
    :align: center

where the symbol ci is now used in place of Ci0 and Gamma is the internal partial pressure of CO2 at which photosynthesis just balances photorespiration ( the photorespiration compensation point), D* is the humidity deficit at the leaf surface, and F0 and Dc are vegetation specific parameters:

.. figure:: figures/triffid.png
    :align: center

In Bethy, the equation above is interpreted as a linear relationship between Gc0 and Ac0, i.e. between the maximum stomatal conductance and the maximum photosynthetic rate and the following equation used (after Schultze et al., 1994):

.. figure:: figures/bethy5.png

with Gc0 in mm s-1 and Ac0 in umol(CO2) m-2 s-1. This leads to the assumption (Knorr, 1998) that for C3 plants, Ci0 = 0.87Ca and for C4 plants Ci0 = 0.67 Ca (interpreting data from Schultze et al., 1994).


Water limitations on stomatal conductance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Most models place an additional limitation on Ac0, thence on stomatal conductance if soil water limits photosynthesis (and so stomata close). In Bethy/JSBACH, this is:

.. figure:: figures/knorr2.png
    :align: center


where be is assumed to change with soil water status in such a way that during the course of a day, the transpiration rate, Et, does not exceed a root supply rate, S, described by (Knorr, 2000):

.. figure:: figures/knorr3.png
    :align: center

:math:`b_e` is thereby set each day either to 0 if Et never exceeds S, or to a value where S = Et at the time of highest atmospheric demand, assumed at 13:00 h. Ws is the soil water content, adjusted to take soil freezing into account and cw an empirical parameter representing root density. (this, verbatim from Knorr, 2000).
Above, es(Ta) is the saturation pressure at the actual temperature (Ta) and ea is the actual vapour pressure exerted by the water in the air, the difference between these two being the `vapour pressure deficit (VPD) or saturation deficit <http://www.fao.org/docrep/X0490E/x0490e07.htm>`_ which is a measure of the evaporative capacity of the air. These terms are usually expressed in kPa. 


Scaling to canopy stomatal conductance
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are several hypotheses about how leaf stomatal  conductance scales to an equivalent canopy stomatal  conductance. In models such as `SDGVM <http://ctcd.group.shef.ac.uk/science/vegmodels/part2.html>`_ and triffid/JULES, it is assumed that canopy stomatal  conductance increases with increasing leaf area index (LAI). In triffid/JULES and most other models:

.. figure:: figures/triiffidscale1.png
    :align: center

where :math:f_{PAR}` is the fraction of incident 'PAR' radiation (shortwave radiation used in photosynthesis) absorbed by the canopy, L is the LAI and k is a geometric term representing leaf projection (and also clumping) -- an extinction coefficient for the canopy (typically set to 0.5). 

The rationale for this is that incident PAR decreases over the vertical extent of the canopy so stomatal conductance might be considered  to also decrease as it is linked to assimilation rates which will decrease in this way. 


Summary
~~~~~~~~~

In this section, we have outlined the 'Farquar' approach to modelling photosynthesis, that is used in this or related forms in most DGVMs.

The model relates the carbon assimilation rate to the the minimum of two potentially limiting factors, the electron transport limiting rate and a carboxylating rate, with leaf 'dark' respiration subtracted. This model has been seen to operate well at the leaf level and is relatively simple to implement and parameterise.

An important facet of this model for climate studies is that it relates carbon assimilation to ambient CO2 concentrations.

We have also outlined some concepts about what controls stomatal conductance. This is an important concept because it can limit carbon assimilation and relates to water use by the leaf (transpiration).



Conclusions
-------------

In this lecture, we have gone into more detail than the previous lecture in considering processes in vegetation canopies (and their interface to the atmosphere and soils). 

Specifically, we have outlined land surface schemes and models as the 'containers' (in e.g. an Earth system model) for models of vegetation process. In doing this, we considered carefully energy and water balances.

We outlined some basic cncepts in vegetation growth, using crop models as an example, and reviewed the development of current LSMs, highlighting the inclusion of carbon fluxes in the current generation.

We reviewed the structure of DGVMs, and considerd in detail PFTs and parameterisation of DGVMs, highlighting trait databases as a useful source of information on this

We also looked into how well we can tell DGVMs are operating, concluding that the current generation show a significant amount of scatter, but they agree broadly in some key areas.

We then looked at PEMs as a viable (more data-driven) approach to modelling NPP. We saw that again there is a lot of scatter in NPP estimates, but those produced by the PEMs are broadly in agreement with those from the DGVMs and other more mechanistic approaches.

We examined the idea of phenology in some detail, highlighting the mechanisms and modelling approaches. 

We then presented some of the basic equations for photosynthesis and stiomatal condictance as used in most DGVMs

References
-----------

Where first author is given in **bold** reading the text is strongly reccomended for this course.

* Bonan, G.B, S. Levis, L. Kergoat, and K.W. Oleson, 2002: `Landscapes as patches of plant functional types: an integrating concept for climate and ecosystem models. Global Biogeochem. Cycles, VOL. 16, NO. 2, 10.1029/2000GB001360, 2002 <http://www.cgd.ucar.edu/tss/clm/pfts/pfts.pdf>`_
* **Box., E.O.** 1996, Plant Functional Types and Climate at the Global Scale, Journal of Vegetation Science, Vol. 7, No. 3 (Jun., 1996), pp. 309-320 
* Bradley et al. 2011, Relationships between phenology, radiation and precipitation in the Amazon region, Global Change Biology Volume 17, Issue 6, pages 2245-2260, June 2011
* Farquhar, G.D., S. von Caemmerer, and J.A. Berry (1980). A Biochemical Model of Photosynthetic CO2 Assimilation in Leaves of C3 species. Planta 149:78-90. [`download <http://scholar.google.com.mx/scholar_url?hl=en&q=http://www.geo.utexas.edu/courses/387H/LAID_papers/Farquhar_etal1980.pdf&sa=X&scisig=AAGBfm32YGPZTIiCDrsrnI-XMp3AZJay1w&oi=scholarr>`_]
* Farquhar GD, von Caemmerer S. 1982. Modeling of photosynthetic response to environmental conditions. In Physiological Plant Ecology. II. Water Relations and Carbon Assimilation, Lange OL, Nobel PS, Osmond CB, Ziegler H (eds). Encyclopedia of Plant Physiology, vol. 12B, Springer-Verlag: New York; 549-587.
* Bouman, B.A.M. ; van Keulen, H. ; van Laar, H.H. ; Rabbinge, R. (1996)  The School of de Wit crop growth simulation models: A pedigree and historical overview, Agricultural Systems, 1996, Vol.52(2), p.171-198
* Burrows, Michael T ; Schoeman, David S ; Buckley, Lauren B ; Moore, Pippa ; Poloczanska, Elvira S ; Brander, Keith M ; Brown, Chris ; Bruno, John F ; Duarte, Carlos M ; Halpern, Benjamin S ; Holding, Johnna ; Kappel, Carrie V ; Kiessling, Wolfgang ; O'Connor, Mary I ; Pandolfi, John M ; Parmesan, Camille ; Schwing, Franklin B ; Sydeman, William J ; Richardson, Anthony J, The pace of shifting climate in marine and terrestrial ecosystems, Science (New York, N.Y.), Nov, 2011, Vol.334(6056), p.652-5
* **D. B. Clark**, L. M. Mercado, S. Sitch, C. D. Jones, N. Gedney, M. J. Best, M. Pryor, G. G. Rooney, R. L. H. Essery, E. Blyth, O. Boucher, R. J. Harding, C. Huntingford, and P. M. Cox (2011) The Joint UK Land Environment Simulator (JULES), model description: Part 2: Carbon fluxes and vegetation dynamics, Geosci. Model Dev., 4, 701-722, 2011, doi:10.5194/gmd-4-701-2011
* Cramer W, Kicklighter DW, Bondeau A, Moore Iii B, Churkina G, Nemry B, Ruimy A, Schloss AL: Comparing global models of terrestrial net primary productivity (NPP): Overview and key results. Global Change Biology 1999, 5:1-15.
* Defilia and Clot, 2005, Phytophenological trends in the Swiss Alps, 1951-2002, Meteorologische Zeitschrift, Vol. 14, No. 2, 191-196 (April 2005)
* Fisher, JI ; Richardson, AD ; Mustard, JF, 2007, Phenology model from surface meteorology does not capture satellite-based greenup estimations, lobal change biology, 2007 MAR, Vol.13(3), p.707-721
* Jarvis, P.G. (1976) `The interpretation of variations in leaf water potential and stomatal conductance found in canopies in the field <http://rstb.royalsocietypublishing.org/content/273/927/593.full.pdf+html>`_ . Philosophical Trans- actions of the Royal Society of London, Series B, 273, 593-610.
* Jones, H.G. (1983) Plants and microclimate. 323 pp. Cambridge University Press, Cambridge, UK. (also `1992 <http://www.amazon.co.uk/Plants-Microclimate-Quantitative-Environmental-Physiology/dp/0521425247/ref=sr_1_fkmr1_1?ie=UTF8&qid=1326907523&sr=8-1-fkmr1>`_)
* Jones, H.G. (1998) `Stomatal control of photosynthesis and transpiration <http://www.google.com.mx/url?sa=t&rct=j&q=stomatal%20control%20of%20photosynthesis%20and%20transpiration&source=web&cd=2&ved=0CCoQFjAB&url=http%3A%2F%2Fwww.ipicyt.edu.mx%2Fstorage-sipicyt%2Fmaterialposgrado%2FStomatalContPsn-clsPS.pdf&ei=e_0WT8j_Mu3KsQKFpqynAg&usg=AFQjCNEvJWZjVLBkWPJb90OOd3T7Mecjhg&sig2=1momBiUiVzDZ2wQE-0TyfA&cad=rja>`_ J. Exp. Bot. (1998) 49(Special Issue): 387-398 doi:10.1093/jxb/49.Special_Issue.387 
* **Chapin, F.S**, Matson, P.A., and Mooney, H.A., (2002) Principles of Terrestrial Ecosystem Ecology, Springer: Chapters 5 and 6 . (see also: `preview of 2011 book <https://sites.google.com/a/alaska.edu/f-stuart-chapin-terry/home/powerpoints-principles-of-ecosystem-ecology/current-text-principles-of-terrestrial-ecosystem-ecology>`_.
* **Kattge, J.**, et al. (2011), TRY: a global database of plant traits. Global Change Biology, 17: 2905-2935. doi: 10.1111/j.1365-2486.2011.02451.x
* Knorr, W. (1997) Satellite remote sensing and modelling of the global CO2 exchange of land vegetation: a synthesis study. Max-Planck-Institut fur Meteorologie Examensarbeit Nr. 49, 185 pp. ISSN 0938-5177 (in German and English), Max-Planck-Institut fur Meteorologie, Hamburg, Germany. (`available online <http://quest.bris.ac.uk/publications/knorr/thesis/thesis.html>`_ ).
* Knorr, W. (2000) Annual and interannual CO exchanges of the terrestrial biosphere: process-based simulations and uncertainties, Global Ecology & Biogeography (2000) 9, 225-252
* **Korner and Basler,** 2010, Phenology Under Global Warming, Science 19 March 2010: 1461-1462.DOI:10.1126/science.1186473 
* Liang, LA ; Schwartz, MD ; Fei, SL, 2011, Validating satellite phenology through intensive ground observation and landscape scaling in a mixed seasonal forest, Remote sensing of environment, 2011 JAN 17, Vol.115(1), p.143-157
* **McCallum, I.,** et al., 2009, Satellite-based terrestrial production efficiency modeling, `Carbon Balance and managementi, 4:8 doi:10.1186/1750-0680-4-8 <http://www.cbmjournal.com/content/pdf/1750-0680-4-8.pdf>`_
* Monteith JL: Solar radiation and productivity in tropical ecosystems.  J Appl Ecol 1972, 9:747-766.
* Monteith JL: Climate and the efficiency of crop production in Britain.  Philos Trans R Soc London, Ser B 1977, 281:277-294.
* Jeffrey Morisette, Mark Schwartz (Lead Author);C Michael Hogan (Topic Editor) `"Phenology" <http://www.eoearth.org/article/Phenological_Research>`_ . In: Encyclopedia of Earth. Eds. Cutler J. Cleveland (Washington, D.C.: Environmental Information Coalition, National Council for Science and the Environment).
* **Peng, C.**  (2000)  From static biogeographical model to dynamic global vegetation model: a global perspective on modelling vegetation dynamicsi, Ecological Modelling, Volume 135, Issue 1, 25 November 2000, Pages 33–54
* Phillips OL, Aragano LEOC, Lewis SL et al. (2009) Drought sensitivity of the Amazon rainforest. Science, 323, 1344-1347.
* Picard, G., Quegan, S., Delabert, N., Lomas, M.R., Le Toan, T., Woodward, F.I. (2005) Bud-burst modelling in Siberia and its impact on quantifying the carbon budget, Global Change Biology 11 (2005) 2164-2176
* **Pitman, A.J,** (2003) THE EVOLUTION OF, AND REVOLUTION IN, LAND SURFACE SCHEMES DESIGNED FOR CLIMATE MODELS, Int. J. Climatol. 23: 479-510 (2003)
* **Prentice et al.**  The Carbon Cycle and Atmospheric Carbon Dioxide, 2001, `IPCC AR3 WG1 <http://www.ipcc.ch/ipccreports/tar/wg1/pdf/TAR-03.PDF>`_
* Quaife, T., S. Quegan, M. Disney, P. Lewis, M. Lomas, and F. I. Woodward (2008), `Impact of land cover uncertainties on estimates of biospheric carbon fluxes, Global Biogeochem. Cycles, 22, GB4016, doi:10.1029/2007GB003097. <http://www2.geog.ucl.ac.uk/~mdisney/papers/quaife_et_al_land_cover.pdf>`_ 
* **Randerson, James T.**, Forrest M. Hoffman, Peter E. Thornton, Natalie M. Mahowald, Keith Lindsay, Yen-Huei Lee, Cynthia D. Nevison, Scott C. Doney, Gordon Bonan, Reto Stockli, Curtis Covey, Steven W. Running, and Inez Y. Fung. September 2009. `Systematic Assessment of Terrestrial Biogeochemistry in Coupled Climate-Carbon Models. <http://www.climatemodeling.org/c-lamp/pubs/Randerson_GCB_2009.pdf>`_  Global Change Biology, 15(9):2462-2484. doi:10.1111/j.1365-2486.2009.01912.x. See also `Supporting Information. <http://www.climatemodeling.org/c-lamp/pubs/Randerson_GCB_2009_SupportingInfo.pdf>`_
* Reed, at el., 2009. Remote Sensing Phenology: Status and the Way Forward, in Noormets, A. Phenology of Ecosystem Processes: Application in Global Change Research. Springer, Dordrecht, pp. 275.
* Sellers PJ. 1992.  Biophysical models of land surface processes. In Climate System Modelling, Trenberth KE (ed.). Cambridge University Press.
* **Sellers PJ,** Berry JA, Collatz GJ, Field CB, Hall FG. 1992b. `Canopy reflectance, photosynthesis and transpiration. III. A reanalysis using improved leaf models and a new canopy integration scheme. Remote Sensing of the Environment 42: 187-216. <http://www.google.com.mx/url?sa=t&rct=j&q=canopy%20reflectance%2C%20photosynthesis%20and%20transpiration.%20iii.%20a%20reanalysis&source=web&cd=1&ved=0CCYQFjAA&url=http%3A%2F%2Famazonpire.org%2FPDF%2Ffc2009%2Freadings%2FSellers_1992_RSE.pdf&ei=IFsgT8uoBu3CsQKkpLmhDg&usg=AFQjCNGNYjTPYFSPZ0KCNjnApXXOvW9S8Q&sig2=H83PVd5Bqo0AAf8b__FKtg&cad=rja>`_
* Sellers PJ, Tucker CJ, Collatz GJ, Los SO, Justice CO, Dazlich DA, Randall DA. 1994. A global 1 degree by 1 degree  NDVI data set for climate studies. Part 2: the generation of global fields of terrestrial biophysical parameters from the NDVI. International Journal of Remote Sensing 15: 3519-3545.
* **Sitch S,** Huntingford C, Gedney N, Levy PE, Lomas M, Piao S, Betts R, Ciais P, Cox P, Friedlingstein P, Jones CD, Prentice IC, Woodward FI (2008) Evaluation of the terrestrial carbon cycle, future plant geography and climate-carbon cycle feedbacks using 5 Dynamic Global Vegetation Models (DGVMs). Global Change Biology 14:2015-2039, doi:10.1111/j.1365-2486.2008.01626.x
* Schwartz, M.D and Hanes J.M. 2010, Continental-scale phenology: warming and chilling, Int. J. Climatol. 30: 1595-1598 (2010)
* Sobrino, JA., Yves Julien, Luis Morales, 2011, Changes in vegetation spring dates in the second half of the twentieth century, International Journal of Remote Sensing , Vol. 32, Iss. 18, 2011
* Studer, S. ; Stockli, R. ; Appenzeller, C. ; Vidale, P. ; Vidale, L. 2007, A comparative study of satellite and ground-based phenology , International Journal of Biometeorology, 2007, Vol.51(5), p.405-414
* White, M. A., et al. (2009), Intercomparison, interpretation, and assessment of spring phenology in North America estimated from remote sensing for 1982-2006, Glob. Change Biol., 15(10), 2335-2359.
* **Woodward, F.I.**  Lomas, M.R. (2004) `Vegetation dynamics - simulating responses to climatic change, Biol. Rev. 79, 643-670 <http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.170.1584&rep=rep1&type=pdf>`_
* Zhang, X. Y., Friedl, M. A., Schaaf, C. B., Strahler, A. H., Hodges, J. C. F., Gao, F., et al. (2003). Monitoring vegetation phenology using MODIS. Remote Sensing of Environment, 84, 471-475.
