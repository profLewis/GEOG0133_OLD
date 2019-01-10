The Terrestrial Carbon Cycle
============================

Purpose of this lecture
------------------------
This is the first lecture in the MSC module 'Terrestrial Carbon: modelling and monitoring'. Students 
attending this course come from a range of different disciplines, so the major purpose of this introductory lecture  is to introduce the basic concepts relating to climate and the terrestrial carbon cycle needed for the rest of this course.

In this lecture, we will:

* consider the importance of understanding the science of climate change
* look at basic principles of energy transfer in the earth system
* examine greenhouse gases and their sources
* look in detail at the terrestrial carbon cycle
* provide an overview of relevant biogeochemical processes
* look in some detail at photosynthesis and factors that limit this

There is no practical associated with this lecture, as it is supposed that students will need to do considerable reading to digest this material. There are however a few 'exercises' in python to illustrate a few points along the way. You will not be marked for these. It is suggested that you make sure that you understand the basic concepts first, then if you like, spend a little time doing these.

Terrestrial Climate and Climate Change
--------------------------------------

*"(C)limate change is a defining issue of our generation. Our responses to the challenges of climate change - accurate prediction, equitable adaptation, and efficient mitigation - will influence the quality of life for ... the world, for generations to come."* (`NASA, 2010 <http://science.nasa.gov/media/medialibrary/2010/07/01/Climate_Architecture_Final.pdf>`_).

From the IPCC AR4 (synthesis report) we can state that there is `general agreement among scientists <http://www.ipcc.ch/publications_and_data/publications_ipcc_fourth_assessment_report_synthesis_report.htm>`_ with regard to the following:

**Observed changes in climate and their effects** 

* Warming of the climate system is unequivocal, as is now evident from observations of increases in global average air and ocean temperatures, widespread melting of snow and ice and rising global average sea level
* Observational evidence from all continents and most oceans shows that many natural systems are being affected by regional climate changes, particularly temperature increases.
* There is medium confidence that other effects of regional climate change on natural and human environments are emerging, although many are difficult to discern due to adaptation and non-climatic drivers

**Causes of change** 

* Global GHG emissions due to human activities have grown since pre-industrial times, with an increase of 70% between 1970 and 2004. 
* Global atmospheric concentrations of CO2, methane (CH4) and nitrous oxide (N2O) have increased markedly as a result of human activities since 1750 and now far exceed pre-industrial values determined from ice cores spanning many thousands of years.
* Most of the observed increase in global average temperatures since the mid-20th century is very likely due to the observed increase in anthropogenic GHG concentrations. It is likely that there has been significant anthropogenic warming over the past 50 years averaged over each continent (except Antarctica). 
* Advances since the TAR show that discernible human influences extend beyond average temperature to other aspects of climate. (Note: `TAR is the IPCC Third Assessment Report <http://www.grida.no/publications/other/ipcc_tar/>`_)
* Anthropogenic warming over the last three decades has likely had a discernible influence at the global scale on observed changes in many physical and biological systems. 
 
The Earth's climate can be seen as the result of a complex set of process interactions. To be able to rise to the challenges facing us, we need to better understand and monitor the processes governing climate and the ways in which they interact. 

One way of expressing and trying to understand this is through an Earth System Science approach, in which we recognise and stress the importance of interactions in the way we apply science to tackling this. The inclusion of the Anthrosphere (or Anthroposphere) (`the part of the environment that is made or modified by humans for use in human activities and human habitats <http://en.wikipedia.org/wiki/Anthrosphere>`_) is critical for this view of the Earth's climate as a set of interacting spheres of influence.

.. figure:: figures/home_earth_spheres.jpg
    :align: center

.. raw:: html

    <center>
    <i>The 'spheres' of influence on the climate system. Source: <a href="http://www.icess.ucsb.edu/">Institute for Computational Earth System Science(ICESS)</a>
    </center>
    </i>

------------

It is clear then that the climate system and its dynamics are things that we as scientistc need to better understand, particularly as climate change is something that will affect us all in some way or other.

Energy transfer
---------------

Basic Principles
~~~~~~~~~~~~~~~~

.. figure:: figures/Reykjavik.png
    :align: center
    :width: 30%

.. raw:: html

    <center>
    <i>Midnight sun, Reykjavik, Iceland. </i> (Photo P. Lewis)
    </center>


------------


The Earth's climate is driven by (shortwave) solar radiation. Around 31% of this incoming radiation is reflected by clouds, aerosols and gases in the atmosphere and by the land surface. The remaining 69% is absorbed, with almost 50% of the incoming radiation being absorbed at the Earth surface. 

.. figure:: figures/faq-1-1-figure-1-l.png
    :align: center
    :width: 50%

.. raw:: html

    <center>    
    <i>"Estimate of the Earth's annual and global mean energy balance. Over the long term, the amount of incoming solar radiation absorbed by the Earth and atmosphere is balanced by the Earth and atmosphere releasing the same amount of outgoing longwave radiation. About half of the incoming solar radiation is absorbed by the Earth's surface. This energy is transferred to the atmosphere by warming the air in contact with the surface (thermals), by evapotranspiration and by longwave radiation that is absorbed by clouds and greenhouse gases. The atmosphere in turn radiates longwave energy back to Earth as well as out to space. Original source: Kiehl and Trenberth (1997)." This source <a href="http://www.ipcc.ch/publications_and_data/ar4/wg1/en/faq-1-1-figure-1.html">IPCC</a>
    </center>
    </i>


------------


The shortwave radiation absorbed at the surface is, in the long term, transferred back to the atmosphere, so that around 69% of the incoming energy flux is re-rediated to space as longwave radiation. 

The energy absorbed at the surface drives thermals (`atmospheric convection <http://www.theweatherprediction.com/habyhints/52>`_) and evapo-transpiration (`latent heat transfer: change of state of water <http://www.fao.org/docrep/x0490e/x0490e04.htm>`_). The rest of the energy balance is maintained by thermal (longwave) radiation emitted by the surface, the atmosphere and clouds. 

As part of the energy cycle illustrated above though, a large proportion of the longwave radiation emitted by the surface is re-radiated back to the surface (and absorbed by the surface) by clouds and so-called greenhouse gases. This mechanism, the 'trapping' of longwave radiation in the atmosphere is what naturally maintains the temperature maintained on Earth -- the 'natural greenhouse effect'. Without this, the temperature at the Earth surface and in the atmosphere would be much less that it presently is: if the Earth were an ideal thermally conductive blackbody (that still reflected around 31% of the incoming shortwave radiation) the effective temperature would be around -19 C to emit the same energy flux required to balance the incoming radiation. 


[`Exercises #1: a simple model <aside1.html>`_]

Atmospheric absorption
~~~~~~~~~~~~~~~~~~~~~~

.. figure:: http://upload.wikimedia.org/wikipedia/commons/7/7c/Atmospheric_Transmission.png
    :align: center
    :target: http://upload.wikimedia.org/wikipedia/commons/7/7c/Atmospheric_Transmission.png
    :width: 50%

.. raw:: html

    <center><i>Radiation transmitted by the atmosphere at shortwave and longwave wavelengths</i>

------------



The figure above shows the major absorbing (and scattering, other than aerosols) constituents of the atmosphere for shortwave and longwave wavelengths and their impact on atmospheric transmission. 

Obviously the atmospheric transmission depends on the concentrations of these constituents, but the figures given might be taken as typical. In the Ultraviolet, Ozone is primarily responsible for solar radiation absorption. At visible wavelengths, the main factors are Rayleigh scattering and aerosols. At thermal wavelengths, water vapour and CO2 are the most important constituents. 

`Clouds <http://earthobservatory.nasa.gov/Features/Clouds/>`_ also affect atmospheric transmission. Low, thick cloud primarily reflect shortwave radiation, whereas high thin clouds allow most shortwave radiation through but absorb longwave radiation.

`Aerosols <http://earthobservatory.nasa.gov/Features/Aerosols/page3.php>`_ have a range of complicated effects on radiation. Whilst many aerosols such as sulfates and nitrates reflect most shortwave radiation, black carbon absorbs most of it. Another important role of aerosols is to act as `cloud condensation nuclei <http://www.jameslovelock.org/page35.html>`_ which enable water vapour in the atmosphere to condense and coalesce. Interesting biogenic sources include volatile organic compounds (VOCs) and other materials emitted from forests (`Spracklen et al., 2008 <http://rsta.royalsocietypublishing.org/content/366/1885/4613.full>`_) and `volatile sulphur compounds emitted both by terrestrial and marine biota <http://www.jameslovelock.org/page35.html>`_.

Radiative Forcing
~~~~~~~~~~~~~~~~~

Radiative forcing (RF) is a measure of the *radiative* impact of components of the climate system (e.g. Greenhouse Gases (GHGs)) in terms of a warming impact (if positive). Formally, it is "a measure of the influence a factor has in altering the balance of incoming and outgoing energy in the Earth-atmosphere system and is an index of the importance of the factor as a potential climate change mechanism. ... radiative forcing values are for changes relative to preindustrial conditions defined at 1750 and are expressed in watts per square meter (W/m^2)." (`IPCC AR4 Synthesis Report <http://www.ipcc.ch/pdf/assessment-report/ar4/syr/ar4_syr.pdf>`_). (see also `"Utility of Radiative Forcing, AR4" <http://www.ipcc.ch/publications_and_data/ar4/wg1/en/ch2s2-8.html>`_ and more generally `"AR4 Climate Change 2007: Working Group I: The Physical Science Basis, Chapter 2: Changes in Atmospheric Constituents and in Radiative Forcing" <http://www.ipcc.ch/publications_and_data/ar4/wg1/en/ch2.html>`_). 

An important conclusion of IPCC AR4 is that the most likely value of (net positive) radiative forcing due to anthrogenic sources is about an order of magnitude larger than the estimated radiative forcing from changes in solar irradiance.

`Rockstrom et al. (2009) <http://www.nature.com/nature/journal/v461/n7263/full/461472a.html>`_ propose that "human changes to atmospheric CO2 concentrations should not exceed 350 parts per million by volume, and that radiative forcing should not exceed 1 watt per square metre above pre-industrial levels. Transgressing these boundaries will increase the risk of irreversible climate change, such as the loss of major ice sheets, accelerated sea- level rise and abrupt shifts in forest and agri- cultural systems. Current CO2 concentration stands at 387 p.p.m.v. and the change in radiative forcing is 1.5 W m^-2"

The figure below from IPCC AR4 gives global mean radiative forcings (and 90% confidence intervals (CIs)) for some of the most significant GHGs and other components of the system. We see that the most significant anthropogenic positive RF term is CO2 followed by CH4, Tropospheric O3, Halocarbons, NO2, (natural) Solar irradiance variations, and black carbon effects on snow (lowering snow albedo). On the other hand, there are significant negative RF effects from aerosols (both directly in increasing the shortwave atmospheric albedo and indirectly through increasing cloud cover and cloud albedo) and surface albedo effects due to land use change (increasing albedo, e.g. through deforestation). The `large error bars on some of these components should be noted <http://www.ipcc.ch/publications_and_data/ar4/wg1/en/ch2s2-9-1.html>`_.

 .. figure:: http://www.ipcc.ch/publications_and_data/ar4/wg1/en/fig/figure-ts-5-l.png
    :align: center
    :target: http://www.ipcc.ch/publications_and_data/ar4/wg1/en/figure-ts-5.html
    :width: 50%

.. raw:: html

    <center><i>
    "Figure TS.5. (a) Global mean radiative forcings (RF) and their 90% confidence intervals in 2005 for various agents and mechanisms. Columns on the right-hand side specify best estimates and confidence intervals (RF values); typical geographical extent of the forcing (Spatial scale); and level of scientific understanding (LOSU) indicating the scientific confidence level as explained in <a href="http://www.ipcc.ch/publications_and_data/ar4/wg1/en/ch2s2-9.html">Section 2.9</a>. Errors for CH4, N2O and halocarbons have been combined. The net anthropogenic radiative forcing and its range are also shown. Best estimates and uncertainty ranges can not be obtained by direct addition of individual terms due to the asymmetric uncertainty ranges for some factors; the values given here were obtained from a Monte Carlo technique as discussed in <a href="http://www.ipcc.ch/publications_and_data/ar4/wg1/en/ch2s2-9.html">Section 2.9</a>. Additional forcing factors not included here are considered to have a very low LOSU. Volcanic aerosols contribute an additional form of natural forcing but are not included due to their episodic nature. The range for linear contrails does not include other possible effects of aviation on cloudiness. (b) Probability distribution of the global mean combined radiative forcing from all anthropogenic agents shown in (a). The distribution is calculated by combining the best estimates and uncertainties of each component. The spread in the distribution is increased significantly by the negative forcing terms, which have larger uncertainties than the positive terms. {<a href="http://www.ipcc.ch/publications_and_data/ar4/wg1/en/ch2s2-9-1.html">2.9.1</a>, <a href="http://www.ipcc.ch/publications_and_data/ar4/wg1/en/ch2s2-9-2.html">2.9.2</a>; <a href="http://www.ipcc.ch/publications_and_data/ar4/wg1/en/figure-2-20.html">Figure 2.20</a>} "</i>. This source: <a href="http://www.ipcc.ch/publications_and_data/ar4/wg1/en/figure-ts-5.html">IPCC AR4 WG1</a>

------------

Carbon in the Earth System
--------------------------

Carbon, its name deriving from the Latin *carbo* for charcoal, is the `4th most abundant element in the universe <http://earthobservatory.nasa.gov/Features/CarbonCycle/>`_. It is able to bond with itself and many other elements and forms over 10 million known compounds. It is present in the atmosphere as carbon dioxide (CO2) and other compounds such as methane (CH4), in all natural waters as dissolved CO2, in various carbonates in rocks, and as organic molecules in living and dead organisms in the biosphere (`Encyclopedia of Earth <http://www.eoearth.org/article/Carbon?topic=49557>`_). We have seen above that carbon is also important in radiative forcing directly in terms of `Halocarbons <http://www.ipcc.ch/publications_and_data/ar4/wg1/en/ch2s2-3-4.html>`_ in the atmosphere and `black carbon deposits on snow <http://www.ipcc.ch/publications_and_data/ar4/wg1/en/ch2s2-5-4.html>`_, as well as indirectly elsewhere (e.g. `land cover change <http://www.ipcc.ch/publications_and_data/ar4/wg1/en/ch2s2-5-4.html#2-5-5>`_).


Atmospheric Carbon and Greenhouse Gases
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Blasing (2011) "Recent Greenhouse Gas Concentrations" <http://cdiac.ornl.gov/pns/current_ghg.html>`_ provides a table of greenhouse gases and their recent and pre-industrial atmospheric concentrations. It also provides an indication of the 'Greenhouse Warming Potential (GWP)', atmospheric lifetime and radiative forcing of the various gases. GWP is a measure of the radiative effects of emissions of greenhouse gases relative to an equal mass of CO2 emissions (so the GWP for CO2 is 1). We see that methane have a significantly higher GWP (25) over a 100 year horizon than CO2 but a shorter residency in the atmosphere.


.. figure:: http://www.esrl.noaa.gov/gmd/aggi/aggi_2011.fig2.png
    :align: center
    :target: http://www.esrl.noaa.gov/gmd/aggi/
    :width: 50%


.. raw:: html

    <center>
    <i>
    "Global average abundances of the major, well-mixed, long-lived greenhouse gases - carbon dioxide, methane, nitrous oxide, CFC-12 and CFC-11 - from the NOAA global air sampling network are plotted since the beginning of 1979. These gases account for about 96% of the direct radiative forcing by long-lived greenhouse gases since 1750. The remaining 4% is contributed by an assortment of 15 minor halogenated gases (see text). Methane data before 1983 are annual averages from Etheridge et al. (1998), adjusted to the NOAA calibration scale [Dlugokencky et al., 2005]." This source: <a href="http://www.esrl.noaa.gov/gmd/aggi/">THE NOAA ANNUAL GREENHOUSE GAS INDEX (AGGI)</a>.
    </center>
    </i>


------------

The figure above shows global abundances of CO2, CH4, N2O and major GHG chlorofluorocarbons (CFCs) in the atmosphere since 1979. 

The temporal pattern of atmospheric CO2 shows a significant annual cycle, with a peak in Northern latitude Spring and a trough in Autumn.

.. figure:: http://www.esrl.noaa.gov/gmd/webdata/ccgg/trends/co2_trend_mlo.png
    :align: center
    :target: http://www.esrl.noaa.gov/gmd/ccgg/trends/
    :width: 50%
    

.. raw:: html

    <center>
    <i>
    "The graph shows recent monthly mean carbon dioxide measured at Mauna Loa Observatory, Hawaii.

    The last four complete years of the Mauna Loa CO2 record plus the current year are shown. Data are reported as a dry air mole fraction defined as the number of molecules of carbon dioxide divided by the number of all molecules in air, including CO2 itself, after water vapor has been removed. The mole fraction is expressed as parts per million (ppm). Example: 0.000400 is expressed as 400 ppm.

    In the above figure, the dashed red line with diamond symbols represents the monthly mean values, centered on the middle of each month. The black line with the square symbols represents the same, after correction for the average seasonal cycle. The latter is determined as a moving average of SEVEN adjacent seasonal cycles centered on the month to be corrected, except for the first and last THREE and one-half years of the record, where the seasonal cycle has been averaged over the first and last SEVEN years, respectively.

    The last year of data are still preliminary, pending recalibrations of reference gases and other quality control checks. The Mauna Loa data are being obtained at an altitude of 3400 m in the northern subtropics, and may not be the same as the globally averaged CO2 concentration at the surface. 
    </i>Source: <a href="http://www.esrl.noaa.gov/gmd/ccgg/trends/">NOAA ESRL</a> 


------------


`Carbon dioxide <http://www.epa.gov/climatechange/emissions/co2.html>`_ is emitted as part of the carbon cycle and by anthropgenic activities such as the burning of fossil fuels. We will deal with the carbon cycle below, but briefly examine direct anthropogenic emissions here. 

.. figure:: figures/E6-6.png
    :align: center    
    :target: http://www.epa.gov/climatechange/emissions/co2_human.html
    :width: 50%

.. raw:: html

    <center>
    <i>a breakdown of sources of CO2 emissions in the U.S. in 2006.
    </i> Original source <a href="http://www.epa.gov/climatechange/emissions/usinventoryreport.html">U.S. Greenhouse Gas Emissions Inventory</a>. This source: <a href="http://www.epa.gov/climatechange/emissions/co2_human.html">EPA, Human-Related Sources and Sinks of Carbon Dioxide</a>
    </center>


------------



By far the largest direct anthropogenic source of CO2 emissions is fossil fuel combustion.

The figure below shows estimated global fossil fuel carbon emissions trends since 1750.

.. figure:: http://cdiac.ornl.gov/trends/emis/graphics/global.total.gif
    :align: center
    :target: http://cdiac.ornl.gov/trends/emis/glo.html
    :width: 50%

.. raw:: html

    <center>
    <i>Carbon Emission Estimates</i>
    This source: <a href="http://cdiac.ornl.gov/trends/emis/glo.html">Carbon Dioxide Information Analysis Center</a>
    </center>


------------


The top ten emitting countries for 2008 are China (7031.9), USA (5672.5), India (1742.7), Russian Federation (1708.7), Japan (1208.2), Germany (786.7), Canada (544.1), Iran (538.4), UK (522.9), and South Korea (509.2), which together account for 63% of global emissions (the global figure being 32082.6), with China and the USA alone accounting for nearly 40% of global emissions (all data converted to Tg CO2 equivalent for comparison with the figure above)  (Source of data: `Carbon Dioxide Information Analysis Center <http://cdiac.ornl.gov/trends/emis/tre_tp20.html>`_). 


.. raw:: html

    <center>
    <i>Global Per Capita Carbon Emission Estimates</i>
    This source: <a href="http://cdiac.ornl.gov/trends/emis/glo.html">Carbon Dioxide Information Analysis Center</a>
    </center>

------------



[`Exercises #2: Per capita emissions trends <aside2.html>`_]


`Methane <http://www.epa.gov/methane/scientific.html>`_ arises from both natural and anthrogenic sources. 
The annual cycles seen in the figure above are attributed to removal by the hydroxyl radical OH (`ECI, Oxford, "Climate science of methane. <http://www.eci.ox.ac.uk/research/energy/downloads/methaneuk/chapter02.pdf>`_) which is the major mechanism for the breakdown of CH4 in the troposphere.


.. figure:: figures/methane.png
    :align: center
    :target: http://www.eci.ox.ac.uk/research/energy/downloads/methaneuk/chapter02.pdf
    :width: 50%


.. raw:: html

    <center>
    <i>Sources of global methane emissions</i>. This source <a href="http://www.eci.ox.ac.uk/research/energy/downloads/methaneuk/chapter02.pdf">Climate science of methane</a>. See also: <a href="http://www.eci.ox.ac.uk/research/energy/downloads/methaneuk/chapter01.pdf">Methane and climate change</a>.
    </center>

------------



Anthropogenic activity accounts for around 30% of N2O, with tropical soils and oceanic release account for the majority of the remainder (`US Environmental Protection Agency <http://www.epa.gov/nitrousoxide/sources.html>`_).

Whilst natural sources of halocarbons exist, their use as refrigerants, propellants and solvents since the early to middle twentieth century is mainly responsible for the current atmospheric concentrations (`Butler et al. (1999) <http://www.nature.com/nature/journal/v399/n6738/pdf/399749a0.pdf>`_).  The `halocarbons <http://en.wikipedia.org/wiki/Halocarbon>`_ (especially chlorofluorocarbons CFC-12 and CFC-11) have been of major concern for their role in RF (among other impacts) although levels of these are mainly now controlled under the `Montreal Protocol on substances that deplete the Ozone Layer <http://ozone.unep.org/new_site/en/index.php>`_ (see also `AR4 Climate Change 2007: Working Group I: The Physical Science Basis, 2.3.4 Montreal Protocol Gases <http://www.ipcc.ch/publications_and_data/ar4/wg1/en/ch2s2-3-4.html>`_). Despite control, their continued presence in the atmosphere is of continuing concern for `Ozone depletion <http://ozone.unep.org/Publications/912_en.pdf>`_ as well as their role as GHGs.  


Terrestrial Carbon
~~~~~~~~~~~~~~~~~~

This is a course on Terrestrial Carbon. Why then, of all of the factors affecting climate should we be interested in this? 

What we mean by the term 'terrestrial carbon' is the carbon that is stored in the vegetation and soils of the Earth's land surface (so, not that in the oceans or atmosphere for example). The Earth Systems Science view of the climate is that we must maintain a focus on interactions between the different spheres, but we must also understand what processes and interactions go on within each sphere. 

Our focus here on terrestrial carbon is mainly because of the major role it plays in anthropogenic climate change. Additional parts of the context of this course are: the role that terrestrial vegetation plays in biodiversity; and the role of vegetation in providing food and fuel.

To understand the role of carbon in the earth system, we must gain some understanding of the general processes at work. We will consider first the biogeochemichal (concentrating on carbon), and then biogeophysical (albedo and evapotranspiration) processes.

The Carbon Cycle
----------------

.. figure:: http://earthobservatory.nasa.gov/Features/CarbonCycle/images/carbon_cycle.jpg
    :align: center
    :target: http://earthobservatory.nasa.gov/Features/CarbonCycle/
    :width: 50%


.. raw:: html

    <center>
    <i>"This diagram of the fast carbon cycle shows the movement of carbon between land, atmosphere, and oceans. Yellow numbers are natural fluxes, and red are human contributions in gigatons of carbon per year. White numbers indicate stored carbon. (<a href="http://public.ornl.gov/hgmis/gallery/detail.cfm?id=313&topic=&citation=24&general=&restsection=">Diagram</a> adapted from U.S. DOE, <a href="http://genomicscience.energy.gov/">Biological and Environmental Research Information System.</a>)"</i>. Source: <a href="http://earthobservatory.nasa.gov/Features/CarbonCycle/">NASA Earth Observatory</a>
    </i>
    </centre>

------------



The carbon cycle describes the flow of carbon between resevoirs in the Earth system. The largest pools of carbon are fossil carbon, deep ocean and reactive sediments, soil carbon, carbon at the ocean surface, and that in the atmosphere. After these comes that stored in plant biomass. Processes of photosynthesis, respiration and decomposition, as well as gas interchange at the ocean surface move carbon between the different pools. On top of that, we have the impact of anthropogenic emissions, which as we have seen above is injecting around 9 (8.749 using the 2008 figures above) Gigatons of carbon a year into the atmosphere from fossil fuel combustion.

A small aside on units:

8.749 * 3.667 * 1000 = 32082.6 Tg CO2 equivalent which is the figure quoted above. See `CDIAC information on reporting units for details <http://cdiac.ornl.gov/units.html>`_). Using 5.137 x 1018 kg as the mass of the atmosphere (Trenberth, 1981 JGR 86:5238-46), 1 ppmv of CO2 = 2.13 Gt of carbon (`CDIAC FAQ <http://cdiac.ornl.gov/pns/faq.html>`_). So, 8.749 Gt of carbon is equivalent to 4.11 ppmv of CO2. 



.. figure:: http://www.esrl.noaa.gov/gmd/webdata/ccgg/trends/co2_data_mlo_anngr.png
    :align: center
    :target: http://www.esrl.noaa.gov/gmd/ccgg/trends/
    :width: 50%

.. raw:: html

    <center>
    <i>"Annual Mean Growth Rate for Mauna Loa, Hawaii"</i>. This source: <a href="http://www.esrl.noaa.gov/gmd/ccgg/trends/">NOAA Trends in Atmospheric Carbon Dioxide</a>.
    </center>



------------


The annual mean growth rate of CO2 in the atmosphere is around 2 ppmv of CO2, from which it can be inferred that just over 2 ppmv of CO2 must enter other fast pools of carbon.

The figures given by the IPCC in `AR4 <http://www.ipcc.ch/publications_and_data/ar4/wg1/en/ch7s7-es.html>`_ are 4.1 +/- 0.1 GtC y-1 annual mean CO2 growth rate for the period 2000 to 2005 with annual emissions from fossil fuel burning and cement production at 7.2 +/- 0.3 GtC y-1 for that same period. The sink to the ocean carbon pool is estimated as 2.2 +/- 0.5 GtC y-1 and that to  the land pool as 0.9 +/- 0.6 GtC y-1 (0.9 + 2.2 + 4.1 = 7.2).

A view of the carbon cycle with more detail, from the `IPCC AR4 <http://www.ipcc.ch/publications_and_data/ar4/wg1/en/ch7s7-3.html>`_ is:

.. figure:: http://www.ipcc.ch/publications_and_data/ar4/wg1/en/fig/figure-7-3-l.png
    :align: center
    :target: http://www.ipcc.ch/publications_and_data/ar4/wg1/en/figure-7-3.html
    :width: 90%

.. raw:: html

    <center>
    <i>"Figure 7.3. The global carbon cycle for the 1990s, showing the main annual fluxes in GtC yr-1: pre-industrial natural fluxes in black and anthropogenic fluxes in red (modified from Sarmiento and Gruber, 2006, with changes in pool sizes from Sabine et al., 2004a). The net terrestrial loss of 39 GtC is inferred from cumulative fossil fuel emissions minus atmospheric increase minus ocean storage. The loss of 140 GtC from the vegetation, soil and detritus compartment represents the cumulative emissions from land use change (Houghton, 2003), and requires a terrestrial biosphere sink of 101 GtC (in Sabine et al., given only as ranges of 140 to 80 GtC and 61 to 141 GtC, respectively; other uncertainties given in their Table 1). Net anthropogenic exchanges with the atmosphere are from Column 5 AR4 in Table 7.1. Gross fluxes generally have uncertainties of more than +/- 20% but fractional amounts have been retained to achieve overall balance when including estimates in fractions of GtC yr-1 for riverine transport, weathering, deep ocean burial, etc. GPP is annual gross (terrestrial) primary production. Atmospheric carbon content and all cumulative fluxes since 1750 are as of end 1994."</i>
    This source: <a href="http://www.ipcc.ch/publications_and_data/ar4/wg1/en/figure-7-3.html">AR4 Climate Change 2007: Working Group I: The Physical Science</a>
    </center>



------------

We can see from this figure some of the complexities that the numbers above hide. For example, the land sink of around 0.9 +/- 0.6 GtCy-1 is itself composed of a balance between a primary production land sink and a land use change source.

Uncertainties
~~~~~~~~~~~~~

.. figure:: figures/ccycle.png
    :align: center
    :target:  figures/ccycle.png
    :width: 90%

.. raw:: html

    <center>
    <i>"Table 7.1. The global carbon budget (GtC yr-1); errors represent ±1 standard deviation uncertainty estimates and not interannual variability, which is larger. The atmospheric increase (first line) results from fluxes to and from the atmosphere: positive fluxes are inputs to the atmosphere (emissions); negative fluxes are losses from the atmosphere (sinks); and numbers in parentheses are ranges. Note that the total sink of anthropogenic CO2 is well constrained. Thus, the ocean-to-atmosphere and land-to-atmosphere fluxes are negatively correlated: if one is larger, the other must be smaller to match the total sink, and vice versa. "
    </i>Source: <a href="http://www.ipcc.ch/publications_and_data/ar4/wg1/en/ch7s7-3-1-3.html">IPCC AR4</a></center>


------------



.. figure:: figures/quegan.png
    :align: center
    :target:  figures/quegan.png
    :width: 90%

.. raw:: html

    <center>
    <i>Figure showing information from above table for the global carbon cycle for thr 1990, figures in Gt carbon yr-1"
    </i>Source: S. Quegan, BIOMASS: ESA User Consultation Meeting, Lisbon, Portugal, 20-21 Jan 2009
    </center>


------------


The table and figure above illustrate what is currently known about both the magnitudes and uncertainties of what the global carbon cycle fluxes were in the 1990s. The increase in atmospheric carbon is less than that emitted from burning fossil fuels as discussed above. The balance is made up of net flows to the ocean and land. The largest uncertainty is in the net terrestrial uptake even though this is the smallest component of the flux. The land sink involves emissions from fire and land use change and a land carbon sink which has the greatest uncertainty of the sub components(0.9 to 4.3 Gt carbon yr-1). Estimates stocks of land carbon are also shown, which indicate a terrestrial vegetation pool of around 600 Gt of carbon (similar order of magnitude to that in the atmosphere) and a much larger but less mobile (on decadal to annual time scales) soil and detritus pool. 

.. figure:: figures/quegan2.png
    :align: center
    :target:  figures/quegan2.png

.. raw:: html

    <center>
    <i> This figure shows current estimates of the carbon cycle for the 1990s. Where available, error bars are given. The cycle is a balance between emissions from anthropogenic sources and changes in the pools of the components of the carbon cycle. The anthropogenic source list is incomplete here as it does not include land use change (mainly tropical deforestation). The AR4 contains no estimate of uncertainty on this (figures above), just a range. The figures illustrated here show both the 'low' estimate of land use change fluxes, implying a low(ish) residual carbon sink, and the 'high' estimates, implying a high residual sink. The large 'uncertainty' (range of estimates) for the land use change flux therefore dominate the total error budgets. The residual sink term is mainly implied from estimates of the land use change term, although this certainly contains some uptake into global biomass.
    </i>Source: S. Quegan, BIOMASS: ESA User Consultation Meeting, Lisbon, Portugal, 20-21 Jan 2009
    </center>

------------


.. figure:: figures/quegan3.png
    :align: center
    :target:  figures/quegan3.png

.. raw:: html

    <center>
    <i> This figure gives an indication of the uncertainty in carbon emissions that is due to uncertainty in knowledge of biomass (ca. 1 Gt carbon yr-1) due to the way in which biomass and land use change fluxes are currently calculated
    </i>Source: S. Quegan, BIOMASS: ESA User Consultation Meeting, Lisbon, Portugal, 20-21 Jan 2009
    </center>


------------


Biogeochemical processes
-------------------------

Net Ecosystem CO2 flux
~~~~~~~~~~~~~~~~~~~~~~~
As we saw in the figure above, the global annual flux of carbon to the atmosphere from microbial respiration and decomposition is thought to be around 120 Gt of carbon per year. This is approximately balanced by the process of photosynthesis that currently draws down around 123 Gt of carbon per year, including around 3 Gt attributed to anthropogenic inputs into the atmosphere that goes into the land sink.

We can consider CO2 fluxes at the `ecosystem <http://www.globalchange.umich.edu/globalchange1/current/lectures/kling/ecosystem/ecosystem.html>`_ level:

.. figure:: figures/gto_si01_0206_1.png
    :align: center
    :target: http://img.kb.dk/tidsskriftdk/gif/gto/gto_si01-IMG/gto_si01_0206_1.jpg
    :width: 50%


.. raw:: html

    <center>
    <i>
    Diurnal variations in CO2 flux over some different vegetation canopies (source: <a href="http://www.tidsskrift.dk/visning.jsp?markup=&print=no&id=72553">Soegaard, 1999</a>)
    </center>
    </i>


------------


The figure above shows typical diurnal variations in CO2 fluxes over some vegetation canopies. The measure given is Net Ecosystem CO2 flux (units: umol m-2 s-1) (multiply by `0.0227223667617 <http://www.convertunits.com/from/moles+CO2/to/grams>`_ to get grams of CO2 m-2 s-1). During the daytime, the fluxes are positive (i.e. there is a flow from the atmosphere to the ecosystem) and at nighttime, the flux is negative (so the ecosystem loses CO2 to the atmosphere). The CO2 gained by the ecosystem over the day then is the integral of this flux, which is known as the net ecosystem productivity (NEP) (usually measured as g C m-2 y-1) (Note that the negative of this measure, net ecosystem exchange (NEE) is sometimes used).

What processes contriute to NEP then? The main positive contribution to this is Gross Primary Productivity (GPP) which is the amount of carbon (per unit area per unit time) taken up by green vegetation in the ecosystem, which is simply the photosynthetic rate (at the ecosystem level) Photosynthesis involves the use of (solar) energy to convert CO2 and H20 to glucose (C6H12O6) and oxygen (O2). Plants use (metabolise) energy (burn carbohydrates) to maintain growth, reproduction and other life processes. This is the process of (autotrophic) respiration, which releases CO2 (and water) to the atmosphere. 

The ecosystem GPP minus plant respiration losses is known as the net primary productivity (NPP), which is effectively the rate of biomass production. The ratio of NPP to GPP is known as the `carbon use efficiency (CUE) <http://www.nature.com/scitable/knowledge/library/terrestrial-primary-production-fuel-for-life-17567411>`_. This is the fraction of carbon absorbed by an ecosystem that is used in biomass production, and is quite similar across ecosystems, typically assumed to be around 0.5. DeLucia et al. (2007) for example confirm an average value of 0.53 across many forest ecosystems, but they note that individual values of CUE can range from 0.23 to 0.83.

.. figure:: figures/CUE.png
    :align: center
    :target: http://www.google.com.mx/url?sa=t&rct=j&q=carbon%20use%20efficiency&source=web&cd=1&ved=0CB0QFjAA&url=http%3A%2F%2Fwww.life.illinois.edu%2Fdelucia%2FGCB_1365.pdf&ei=xRcOT9TjEcTEsQKelrniBQ&usg=AFQjCNFSOD1vZsAP1iKJmHgO6PAb5mzAxg&sig2=1_vtYt9hg1ANExckO-x44A&cad=rja
    :width: 50%


.. raw:: html

    <center>
    <i>
    "The relationship between net primary production (NPP) and gross primary production (GPP) for different forest types. Closed symbols represent values of GPP that were derived from estimates of NPP and Ra; open symbols represent values of GPP that were estimated independently from NPP. Symbols for the different forest types are: boreal (circles), West Coast Maritime (triangles), temperate conifer (squares), temperate deciduous (diamonds), temperate mixed (inverted triangles), and Tropical (stars). The intercept of the relationship between NPP and derived estimates of GPP (solid line) was significantly lower than the intercept for the relationship between NPP and independent estimates of GPP (dashed line; see results in paper for details)"
    (source: <a href="http://www.google.com.mx/url?sa=t&rct=j&q=carbon%20use%20efficiency&source=web&cd=1&ved=0CB0QFjAA&url=http%3A%2F%2Fwww.life.illinois.edu%2Fdelucia%2FGCB_1365.pdf&ei=xRcOT9TjEcTEsQKelrniBQ&usg=AFQjCNFSOD1vZsAP1iKJmHgO6PAb5mzAxg&sig2=1_vtYt9hg1ANExckO-x44A&cad=rja">DeLucia et al. (2007), GCB</a>
    </center>
    </i>



------------


Similarly, `Zhang et al. (2009)  <http://www.google.com.mx/url?sa=t&rct=j&q=global+npp&source=web&cd=10&ved=0CFgQFjAJ&url=http%3A%2F%2Fcrssa.rutgers.edu%2Fpeople%2Fzhangyang%2FPaper%2Fzhang_Geb.pdf&ei=Yx8OT7P-AcSbsgKzxbXSBQ&usg=AFQjCNE_2hq0Qr8oFcxxybzFu2h-Y-RwLg&sig2=ZH-XiBGvlvJ8Dt-6kSWxCQ&cad=rja>`_ showed that CUE exhibited a pattern depending on the main climatic characteristics such as temperature and precipitation and geographical factors such as latitude and altitude.

.. figure:: figures/CUEZhang.png
    :align: center
    :target: http://www.google.com.mx/url?sa=t&rct=j&q=global+npp&source=web&cd=10&ved=0CFgQFjAJ&url=http%3A%2F%2Fcrssa.rutgers.edu%2Fpeople%2Fzhangyang%2FPaper%2Fzhang_Geb.pdf&ei=Yx8OT7P-AcSbsgKzxbXSBQ&usg=AFQjCNE_2hq0Qr8oFcxxybzFu2h-Y-RwLg&sig2=ZH-XiBGvlvJ8Dt-6kSWxCQ&cad=rja


.. raw:: html

    <center>
    <i>Global spatial pattern of the average NPP/GPP ratio.</i>
    This source: <a href="http://www.google.com.mx/url?sa=t&rct=j&q=global+npp&source=web&cd=10&ved=0CFgQFjAJ&url=http%3A%2F%2Fcrssa.rutgers.edu%2Fpeople%2Fzhangyang%2FPaper%2Fzhang_Geb.pdf&ei=Yx8OT7P-AcSbsgKzxbXSBQ&usg=AFQjCNE_2hq0Qr8oFcxxybzFu2h-Y-RwLg&sig2=ZH-XiBGvlvJ8Dt-6kSWxCQ&cad=rja">Zhang et al. GCB 2009</a>


------------



.. figure:: figures/CUEZhang2.png
    :align: center
    :target: http://www.google.com.mx/url?sa=t&rct=j&q=global+npp&source=web&cd=10&ved=0CFgQFjAJ&url=http%3A%2F%2Fcrssa.rutgers.edu%2Fpeople%2Fzhangyang%2FPaper%2Fzhang_Geb.pdf&ei=Yx8OT7P-AcSbsgKzxbXSBQ&usg=AFQjCNE_2hq0Qr8oFcxxybzFu2h-Y-RwLg&sig2=ZH-XiBGvlvJ8Dt-6kSWxCQ&cad=rja



.. raw:: html

    <center>
    This source: <a href="http://www.google.com.mx/url?sa=t&rct=j&q=global+npp&source=web&cd=10&ved=0CFgQFjAJ&url=http%3A%2F%2Fcrssa.rutgers.edu%2Fpeople%2Fzhangyang%2FPaper%2Fzhang_Geb.pdf&ei=Yx8OT7P-AcSbsgKzxbXSBQ&usg=AFQjCNE_2hq0Qr8oFcxxybzFu2h-Y-RwLg&sig2=ZH-XiBGvlvJ8Dt-6kSWxCQ&cad=rja">Zhang et al. GCB 2009</a>
    </center>


------------



NPP varies over the year as the factors affecting the processes involed (essentially, light, temperature and water availability) vary over the growing seasdon.  Nutrient availability also affects NPP but this is likely to vary over longer time periods. NPP can very quite significantly from one year to the next and over decadal timescales depending on climatic factors.


.. figure:: http://www.nature.com/scitable/content/ne0000/ne0000/ne0000/ne0000/17650031/f3_gough_ksm.jpg
    :align: center
    :target: http://www.nature.com/scitable/knowledge/library/terrestrial-primary-production-fuel-for-life-17567411


.. raw:: html

    <center>
    <i>
    "Patterns of terrestrial NPP at different timescales in a temperate forest: Daily net primary production (NPP) changes during the growing season in response to climate variables including solar radiation and precipitation, while the duration of NPP during the growing season (i.e., spring green-up to autumn leaf fall) is largely a function of photoperiod. Annual NPP changes from one year to the next in response to longer-term trends in climate, including shifts in total solar radiation caused by differences in cloud cover from year to year. Decadal patterns of NPP track changes in ecological succession (Gough et al. 2007, 2008).". </i>This source: <a href="http://www.nature.com/scitable/knowledge/library/terrestrial-primary-production-fuel-for-life-17567411">Gough, C. M. (2011) Terrestrial Primary Production: Fuel for Life. Nature Education Knowledge 2(2):1</a>
    </center>



------------

NPP varies quite considerably between biomes. The following table shows (what are assumed) typical values of GPP, total Global NPP and NPP per unit area for the main biomes.

.. figure:: figures/NPP.png
    :align: center
    :target: http://www.nature.com/scitable/knowledge/library/terrestrial-primary-production-fuel-for-life-17567411
    :width: 90%

.. raw:: html

    <center>
    Source: <a href="http://www.nature.com/scitable/knowledge/library/terrestrial-primary-production-fuel-for-life-17567411">Gough, C. M. (2011) Terrestrial Primary Production: Fuel for Life. Nature Education Knowledge 2(2):1</a>
    </center>



------------


Globally then, the most productive biomes are tropical forests, savannah and grassland which together accound for around half of global NPP, and the predominance of the tropics can be seen in the figure below. But per unit area, tropical and temperate forests are the most productive.



.. figure:: http://eoimages.gsfc.nasa.gov/images/globalmaps/data/MOD17A2_M_PSN/MOD17A2_M_PSN_2006-07.JPEG
    :align: center
    :target: http://earthobservatory.nasa.gov/GlobalMaps/view.php?d1=MOD17A2_M_PSN
    :width: 90%


------------


.. figure:: http://earthobservatory.nasa.gov/GlobalMaps/images/colorbars/modis_npp.png
    :align: center
    :width: 90%

.. raw:: html

    <center><i>
    Global NPP for July 2006
    </i></centre>


------------


.. figure:: http://eoimages.gsfc.nasa.gov/images/globalmaps/data/MOD13A2_M_NDVI/MOD13A2_M_NDVI_2006-07.JPEG
    :align: center
    :target: http://earthobservatory.nasa.gov/GlobalMaps/view.php?d1=MOD13A2_M_NDVI
    :width: 90%



------------

.. figure:: http://earthobservatory.nasa.gov/GlobalMaps/images/colorbars/modis_ndvi.png
    :align: center
    :width: 90%


.. raw:: html

    <center><i>
    Global NDVI July 2006
    </i></centre>



------------



.. figure:: http://eoimages.gsfc.nasa.gov/images/globalmaps/data/CERES_NETFLUX_M/CERES_NETFLUX_M_2006-07.JPEG
    :align: center
    :target: http://earthobservatory.nasa.gov/GlobalMaps/view.php?d1=CERES_NETFLUX_M
    :width: 90%



------------


.. figure:: http://earthobservatory.nasa.gov/GlobalMaps/images/colorbars/ceres_net.gif
    :align: center
    :width: 90%



.. raw:: html

    <center><i>
    Global Net Radiation July 2006
    </i></centre>



------------



.. figure:: http://eoimages.gsfc.nasa.gov/images/globalmaps/data/MOD11C1_M_LSTDA/MOD11C1_M_LSTDA_2006-07.JPEG
    :align: center
    :target: http://earthobservatory.nasa.gov/GlobalMaps/view.php?d1=MOD11C1_M_LSTDA
    :width: 90%

------------



.. figure:: http://earthobservatory.nasa.gov/GlobalMaps/images/colorbars/modis_lst_gm.gif
    :align: center
    :width: 90%


.. raw:: html

    <center><i>
    Global Land surface temperature July 2006
    </i></centre>

------------


.. figure:: http://eoimages.gsfc.nasa.gov/images/globalmaps/data/TRMM_3B43M/TRMM_3B43M_2006-07.JPEG
    :align: center
    :target: http://earthobservatory.nasa.gov/GlobalMaps/view.php?d1=TRMM_3B43M
    :width: 90%


------------


.. figure:: http://earthobservatory.nasa.gov/GlobalMaps/images/colorbars/trmm_rainfall_gm.gif
    :align: center
    :width: 90%


.. raw:: html

    <center><i>
    Total rainfall July 2006
    </i></centre>


------------


The figures above show global NPP distribution and related climatic and land surface properties for Northern hemisphere summer. The dataset 'NDVI' broadly shows the abundance of vegetation, which relates to the capacity of vegetation to photosynthesise. The primary driver of GPP (so NPP in broad terms) is the amount of vegetation and the amount of downwelling solar radiation. Although we do not have an image of the latter here, it is broadly inline with the net radiation shown. As a rough approximation then, we can see that the product of the first two datasets after NPP would give  the spatial patterns of NPP. There are of course many more subtle controls on NPP that we will consider later, but clearly these would include temperature range and water availability.

In Northern hemisphere summer then, NPP is most stongly spatially weighted  to the Northern hemisphere because of these various drivers.

.. figure:: http://eoimages.gsfc.nasa.gov/images/globalmaps/data/MOD17A2_M_PSN/MOD17A2_M_PSN_2006-12.JPEG
    :align: center
    :target: http://earthobservatory.nasa.gov/GlobalMaps/view.php?d1=MOD17A2_M_PSN

------------



.. figure:: http://earthobservatory.nasa.gov/GlobalMaps/images/colorbars/modis_npp.png
    :align: center

.. raw:: html

    <center><i>
    Global NPP for December 2006
    </i></centre>


------------



.. figure:: http://eoimages.gsfc.nasa.gov/images/globalmaps/data/MOD13A2_M_NDVI/MOD13A2_M_NDVI_2006-12.JPEG
    :align: center
    :target: http://earthobservatory.nasa.gov/GlobalMaps/view.php?d1=MOD13A2_M_NDVI


------------



.. figure:: http://earthobservatory.nasa.gov/GlobalMaps/images/colorbars/modis_ndvi.png
    :align: center

.. raw:: html

    <center><i>
    Global NDVI December 2006
    </i></centre>

------------



.. figure:: http://eoimages.gsfc.nasa.gov/images/globalmaps/data/CERES_NETFLUX_M/CERES_NETFLUX_M_2006-12.JPEG
    :align: center
    :target: http://earthobservatory.nasa.gov/GlobalMaps/view.php?d1=CERES_NETFLUX_M


------------


.. figure:: http://earthobservatory.nasa.gov/GlobalMaps/images/colorbars/ceres_net.gif
    :align: center


.. raw:: html

    <center><i>
    Global Net Radiation December 2006
    </i></centre>


------------


.. figure:: http://eoimages.gsfc.nasa.gov/images/globalmaps/data/MOD11C1_M_LSTDA/MOD11C1_M_LSTDA_2006-12.JPEG
    :align: center
    :target: http://earthobservatory.nasa.gov/GlobalMaps/view.php?d1=MOD11C1_M_LSTDA


------------

.. figure:: http://earthobservatory.nasa.gov/GlobalMaps/images/colorbars/modis_lst_gm.gif
    :align: center

.. raw:: html

    <center><i>
    Global Land surface temperature December 2006
    </i></centre>

------------



.. figure:: http://eoimages.gsfc.nasa.gov/images/globalmaps/data/TRMM_3B43M/TRMM_3B43M_2006-12.JPEG
    :align: center
    :target: http://earthobservatory.nasa.gov/GlobalMaps/view.php?d1=TRMM_3B43M


------------


.. figure:: http://earthobservatory.nasa.gov/GlobalMaps/images/colorbars/trmm_rainfall_gm.gif
    :align: center

.. raw:: html

    <center><i>
    Total rainfall December 2006
    </i></centre>



------------


In Northern hemisphere winter, the distribution of NPP shifts to the Southern hemisphere, for the same reasons as indicated above. 

.. figure:: http://gaim.unh.edu/Products/Reports/Report_5/NPP_gifs/npp_fig6.gif
    :align: center
    :target: http://gaim.unh.edu/Products/Reports/Report_5/

.. raw:: html

    <center><i>
    "Comparison of the latitudinal distribution of the median (solid line), and 10th and 90th percentiles (dotted lines) of areally- weighted mean annual net primary productivity estimated by fifteen models within a 0.5o latitudinal band."</i>
    Source: <a href="http://gaim.unh.edu/Products/Reports/Report_5/">Cramer et al., 1995, "IGBP/GAIM REPORT SERIES REPORT #5" </a>

------------



.. figure:: http://gaim.unh.edu/Products/Reports/Report_5/NPP_gifs/npp_fig8.gif
    :align: center
    :target: http://gaim.unh.edu/Products/Reports/Report_5/

.. raw:: html

    <center><i> 
    "Relative distribution (%) of global annual net primary productivity across latitudes and months."</i>
    Source: <a href="http://gaim.unh.edu/Products/Reports/Report_5/">Cramer et al., 1995, "IGBP/GAIM REPORT SERIES REPORT #5" </a>


------------

Since the total landmass (and in particular the vegetated landmass) in the Southern hemisphere is less than that of the Northern hemisphere, global NPP  comes predominantly from Northern latitudes. Referring back to the plots of the annual cycle of atmospheric CO2 above, we noted a peak in May and a trough  in October, largely then in response to global NPP increases in Spring and decreases in Autumn: the larger NPP in Northern hemisphere summer gradually decreases the atmospheric CO2 concentration. This is however complicated by the timing and spatial distribution of other CO2 sources and sinks.


Net Ecosystem Productivity
~~~~~~~~~~~~~~~~~~~~~~~~~~

The NEP then is NPP minus other losses to the atmosphere. These will generally include respiration by heterotrophs (organisms --  fungi, animals and bacteria in the soil), but there may be other losses to the ecosystem such as through harvesting or fire.  

.. figure:: http://www.globalfiredata.org/pics/GFED3_carbon_emissions.jpg
    :align: center
    :target: http://www.globalfiredata.org/pics/GFED3_carbon_emissions.jpg

.. raw:: html

    <center><i>
    "Annual carbon emissions (as g C m-2 year-1), averaged over 1997-2009. These emissions estimates are build combining burned area data from above with a biogeochemical model (CASA-GFED) that estimates fuel loads and combustion completeness for each monthly time step. These fuel loads are based on satellite derived information on vegetation characteristics and productivity to estimate carbon input, and carbon outputs through heterotrophic respiration, herbivory, and fires."</i>
    Source: <a href="http://www.globalfiredata.org/">globalfiredata.org</a>
    </center>


------------

.. An interesting `NASA study <http://www.gsfc.nasa.gov/topstory/2004/0624hanpp.html>`_ has looked at human appropriation of land-based net primary production. 
    .. figure:: http://eoimages.gsfc.nasa.gov/images/imagerecords/4000/4600/HANPP_1982-98.jpg
    :align: center
    :target: http://eoimages.gsfc.nasa.gov/images/imagerecords/4000/4600/HANPP_1982-98.jpg
     .. raw:: html
    <center>
    Source: <a href="http://earthobservatory.nasa.gov/IOTD/view.php?id=4600">NASA earthobservatory</a>
    The figure above gives some idea of the disparities between the demand for NPP and where it occurs.     The study estimated that around 20% of annual NPP is required by humans.
    The average accumulation of carbon over large areas and/or long time periods is called `net biome productivity <http://www.ipcc.ch/ipccreports/tar/wg2/204.htm>`_ (NBP).


Anthropogenic and wildfire carbon emissions (as well as ocean and soil fluxes) as well as atmospheric circulation also significantly affect the global distribution of CO2, so the global patterns of CO2 are not as 'simple' as just the NPP fluxes. 

.. figure:: http://www.esrl.noaa.gov/gmd/webdata/ccgg/CT2010/co2wx/glb/co2wx_hammer-glb_20060715.png
    :align: center
    :target: http://www.esrl.noaa.gov/gmd/ccgg/carbontracker/co2weather.php?region=glb&date=2006-07-15#imagetable


------------


.. figure::  http://www.esrl.noaa.gov/gmd/webdata/ccgg/CT2010/co2wx/glb/co2wx_hammer-glb_20061215.png
    :align: center
    :target: http://www.esrl.noaa.gov/gmd/ccgg/carbontracker/co2weather.php?region=glb&date=2006-12-15#imagetable


.. raw:: html

    <center><i>"CO2 weather. We depict the daily average of the pressure-weighted mean mole fraction of carbon dioxide in the free troposphere as modeled by CarbonTracker. Units are micromoles of CO2 per mole of dry air (μmol mol-1), and the values are given by the color scale depicted under the graphic. The "free troposphere" in this case is levels 5 through 10 of the TM5 model before 2005, and levels 6 through 10 after (due to an improvement in the vertical resolution for 2006 onwards). This corresponds to about 1.2km above the ground to about 5.5km above ground, or in pressure terms, about 850 hPa to about 500 hPa. Gradients in CO2 concentration in this layer are due to exchange between the atmosphere and the earth surface, including fossil fuel emissions, air-sea exchange, and the photosynthesis, respiration, and wildfire emissions of the terrestrial biosphere. These gradients are subsequently transported by weather systems, even as they are gradually erased by atmospheric mixing."
    </i> Source: <a href="http://www.esrl.noaa.gov/gmd/ccgg/carbontracker/co2weather.php">NOAA carbontracker</a>


------------


Photosynthesis
~~~~~~~~~~~~~~~

What photosynthesis achieves is to fix solar energy. This is then used to support plant growth and produce organic matter that in turn supports animals and soil microbes. It is the primary mechanism for carbon (and chemical energy) input to ecosystems.

.. figure:: figures/141-1.jpg
    :align: center
    :target: http://www.cmg.colostate.edu/gardennotes/141.html


------------


.. figure:: figures/141-2.jpg
    :align: center
    :target: http://www.cmg.colostate.edu/gardennotes/141.html


.. raw:: html


    <center><i>
    In photosynthesis, the plant uses water and nutrients from the soil, and carbon dioxide from the air with the sun's energy to create photosynthates.  Oxygen is releases as a byproduct.
    </i></center>
    <a href="http://www.cmg.colostate.edu/gardennotes/141.html">Source: Colorado State University</a>

------------


In essence, what it does is to split (proportionately) 12 water molecules (H20) and produce 6 molecules of oxygen gas (O2) and 6 of H20. Carbon dioxide is reduced to glucose (C6H12O6) which is the basic material from which other biochemical constituents of biomass are synthesised (Grace, 2001). Note that the additional 6H2O are omitted in the figure above which does not include transpiration. 

Transpiration in plants is part of the water cycle and provides around `10% of the moisture found in the atmosphere <http://ga.water.usgs.gov/edu/watercycletranspiration.html>`_.  Transpiration `uses around 90% of the water that enters the plant <http://www.cmg.colostate.edu/gardennotes/141.html>`_ (the rest being used in cell growth and photosynthesis). Most transpiration water loss takes place in the stomata of the leaves. The guard cells of the stomata open to allow CO2 diffusion from the air for photosynthesis.
In that sense, it can be thought of as the "cost" associated with the opening of the stomata to allow the diffusion of carbon dioxide gas from the air.

Stomatal conductance, (e.g. in mmol m-2 s-2) is a measure of the rate of passage of carbon dioxide (CO2) exiting, or water vapor entering through the stomata of a leaf. The term `conductance <http://www.allaboutcircuits.com/vol_1/chpt_5/4.html>`_ comes from analogy with electrical circuitry. It is controlled by the guard cells of t
he leaf stomata and controls transpiration rates and CO2 diffusion rates (along with gradients of water vapour and CO2).

`Transpiration serves three main roles <http://www.cmg.colostate.edu/gardennotes/141.html>`_:

* movement of minerals (from the roots: xylem) and sugars (from photosynthesis: phloem) throughout the plant.
* cooling (loss of heat energy through transpiration)
* maintenance of turgor pressure in plant cells for plant structure and the functioning of guard cells in the stomata to regulate  water loss and CO2 uptake.

.. figure:: http://www.pcsd.k12.ny.us/bwoods/Regents%20Biology/Chapter%2019%20Plant%20Function/Chapte9.jpg
    :align: center
    :target: http://www.pcsd.k12.ny.us/bwoods/Regents%20Biology/Chapter%2019%20Plant%20Function/Chapter%2019%20Plant%20Structure%20and%20FunctionHome.htm

.. raw:: html

    <center>This Source: <a href="http://www.pcsd.k12.ny.us/bwoods/Regents%20Biology/Chapter%2019%20Plant%20Function/Chapter%2019%20Plant%20Structure%20and%20FunctionHome.htm"> pcsd.k12.ny.us </a>. Original source unknown.


--------

.. figure:: http://ga.water.usgs.gov/edu/graphics/wctranspirationwatertable.gif
    :align: center
    :target: http://ga.water.usgs.gov/edu/watercycletranspiration.html

.. raw:: html


    <center><i>
    "In many places, the top layer of the soil where plant roots are located is above the water table and thus is often wet to some extent, but is not totally saturated, as is soil below the water table. The soil above the water table gets wet when it rains as water infiltrates into it from the surface, But, it will dry out without additional precipitation. Since the water table is usually below the depth of the plant roots, the plants are dependent on water supplied by precipitation. As this diagram shows, in places where the water table is near the land surface, such as next to lakes and oceans, plant roots can penetrate into the saturated zone below the water table, allowing the plants to transpire water directly from the groundwater system. Here, transpiration of ground water commonly results in a drawdown of the water table much like the effect of a pumped well (cone of depression)." </i> Source: <a href="http://ga.water.usgs.gov/edu/watercycletranspiration.html">USGS</a>
    </center>

------------



There are three types of photosynthesis mechanisms in plants: C3, C4 and CAM. Plants that use the CAM mechanism include cacti and orchids that are adapted to extremely hot and dry environments. We will concentrate on C3 and C4 plants here because of their greater global significance.

`C3 plants <http://www.biology-online.org/dictionary/C3_plant>`_ use the `Calvin cycle <http://hyperphysics.phy-astr.gsu.edu/hbase/biology/calvin.html#c1>`_ for fixing CO2. 

.. figure:: http://hyperphysics.phy-astr.gsu.edu/hbase/biology/imgbio/calc3.gif
    :align: center
    :target: http://hyperphysics.phy-astr.gsu.edu/hbase/biology/phoc.html

.. raw:: html


    <center><i>
    "In the first step of the cycle CO2 reacts with RuBP to produce two 3-carbon molecules of 3-phosphoglyceric acid (3-PGA). This is the origin of the designation C3 or C3 in the literature for the cycle and for the plants that use this cycle. The entire process, from light energy capture to sugar production occurs within the chloroplast. The light energy is captured by the non-cyclic electron transport process which uses the thylakoid membranes for the required electron transport."</i>
    Source: <a href="http://hyperphysics.phy-astr.gsu.edu/hbase/biology/phoc.html">GSU</a>

------------

Around 85% of plants use this mechanism, including wheat, barley, potatoes and sugar beet and `most trees <http://hyperphysics.phy-astr.gsu.edu/hbase/biology/phoc.html>`_. C3 plants cannot grow in hot climates because the enzyme RuBisCO involved in catalyzing carboxylation of RuBP incorporates more oxygen into RuBP as temperatures increase, leading to a process called `photorespiration <http://en.wikipedia.org/wiki/Photorespiration>`_ and a net loss of carbon (and nitrogen) that can act as a limit to growth. C3 plants are also sensitive to water availability.

`C4 plants <http://en.wikipedia.org/wiki/C4_carbon_fixation>`_ (and `CAM plants <http://en.wikipedia.org/wiki/Crassulacean_acid_metabolism>`_) operate more efficiently than C3 plants under conditions of drought, high temperatures, and nitrogen or CO2 limitation. They do this by bypassing the photorespiration pathway and efficiently delivering CO2 to the RuBisCO enzyme. 

.. figure:: http://hyperphysics.phy-astr.gsu.edu/hbase/biology/imgbio/kranzm.gif
    :align: center
    :target: http://hyperphysics.phy-astr.gsu.edu/hbase/biology/phoc.html

.. raw:: html


    <center><i>
    "C4 plants almost never saturate with light and under hot, dry conditions much outperform C3 plants. They use a two-stage process were CO2 is fixed in thin-walled mesophyll cells to form a 4-carbon intermediate, typically malate (malic acid). The reaction involves phosphoenol pyruvate (PEP) which fixes CO2 in a reaction catalyzed by PEP-carboxylate. It forms oxaloacetic acid (OAA) which is quickly converted to malic acid. The 4-carbon acid is actively pumped across the cell membrane into a thick-walled bundle sheath cell where it is split to CO2 and a 3-carbon compound. This CO2 then enters the Calvin cycle in a chloroplast of the bundle sheath cell and produces G3P and subsequently sucrose, starch and other carbohydrates that enter the cells energy transport system. " </i> Source: <a href="http://hyperphysics.phy-astr.gsu.edu/hbase/biology/phoc.html">GSU</a>
    </center>



------------


C4 plants include maize and sugarcane. Although  only a small proportion of flowering plants use this mechanism for carbon fixation, they are responsible for around `25%  of photosynthesis on land <http://users.rcn.com/jkimball.ma.ultranet/BiologyPages/C/C4plants.html>`_.


Respiration
~~~~~~~~~~~
In (autotrophic) respiration, plants convert the sugars made during photosynthesis back into CO2 and water, and release energy in the process.

.. figure:: figures/141-4.jpg
    :align: center
    :target: http://www.cmg.colostate.edu/gardennotes/141.html


------------


Oxygen is taken up in this process. The energy released from respiration is used by the plant for growth and maintenance of existing material. It consumes between 25% and 75% of all of the carbohydrates generated in photosynthesis. 


Limitations to photosynthesis at the leaf level
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


The main factors affecting net photosynthesis at the leaf level are: (i) light limitation; (ii) CO2 limitation; (iii) nitrogen limitation and photosynthetic capacity; (iv) water limitation; (v) temperature effects; and (vi) pollutants. (see pp.105-115 of Chapin et al. 2002)

**light limitation**

Light response curves measures plants response to light intensity. 

.. figure:: figures/chapin1.png
    :align: center
    :target: figures/chapin1.png


.. raw:: html

    <centre>
    "Relationship of net photosynthetic rate to photosynthetically active radiation and the processes that limit photosynthesis at different irradiances. The linear increase in photosynthesis in response to increased light (in the range of light limitation) indicates relatively constant light use efficiency. The light compensation point is the minimum irradiance at which the leaf shows a net gain of carbon.  "
    </i>Source: <a href="http://sites.google.com/a/alaska.edu/f-stuart-chapin-terry/home/powerpoints-principles-of-ecosystem-ecology">Chapin, 2011, PTEEChap5.ppt, fig. 5.5</a>
    </centre>


At low to moderate light levels, leaves have a near linear response to light intensity. The rate of change of net photosynthesis in this region to irradiance is the `quantum yield of photosynthesis <http://www.annualreviews.org/doi/pdf/10.1146/annurev.pp.09.060158.000245>`_. This is similar for all C3 plants (in the absence of environmental stresses) at around 6% (Chapin et al., 2002). At higher light levels, saturation occurs as the efficiency of the photosynthetic mechanism is reduced. At higher levels still, net photosynthesis can decline as a result of photorespiration as described above.

Plants have some capacity to respond to changes in light conditions over time scales of days to months, such as by having leaves in more direct sunlight with more cell layers and higher photosynthetic capacity than shade leavesi by `acclimation <http://en.wikipedia.org/wiki/Acclimatization>`_ or `adaptation <http://www.sciencedaily.com/releases/2011/01/110131161344.htm>`_ over longer time periods. Respiration rate depends on tissue protein content (Chapin et al., 2002, ch. 6) so shade leaves with low photosynthetic capacity generally have a lower protein content to minimise respiration losses. 

When upscaling light limitations to the canopy or ecosystem scale, the leaf area index (LAI) is a major constraint. In effect, the lower the LAI, the lower the radiation intercepted by the vegetation. Radiation interception is often approximated through Beer's law:

::


    I = I0 exp(-k L)

where I is the radiation intensity intercepted, I0 is that at the top of the canopy, k is an extinction coefficient (a function of leaf angle distribution and clumping) and L is the LAI.

Assuming only first order interactions then gives the proprtion of radiation intercepted over the canopy, I/I0 as:

::

    I/I0 = 1 -  exp(-k L)


so that for L = 0, no radiation is intercepted, and as L increases, so the proportion intercepted does as well. We shall return to consideration of this in later lectures, but for the moment we can suppose this simple relationship showing general principles.

**CO2 limitation**

Although we have noted spatial and temporal variations in CO2 concentrations, the variation is in fact only quite small, being of the order of 4% (Chapin et al., 2002) and insufficient to cause significant regional variations in photosynthesis.  Further, although photosynthesis locally depletes the CO2 pool, it is not to a sufficient extent that it significantly affects  the amount available. 

.. figure:: figures/chapin2.png
    :align: center
    :target: figures/chapin2.png


.. raw:: html

    <centre>
    "Relationship of the net photosynthetic rate to the CO2 concentration inside the leaf. Photosynthetic rate is limited by the rate of CO2 diffusion into the chloroplast in the initial (left-hand side) linear portion of the CO2 response curve and by biochemical processes at higher CO2 concentrations. The CO2 compensation point is the minimum CO2 concentration at which the leaf shows a net gain of carbon.  "</i>
    Source: <a href="http://sites.google.com/a/alaska.edu/f-stuart-chapin-terry/home/powerpoints-principles-of-ecosystem-ecology">Chapin, 2011, PTEEChap5.ppt, fig. 5.10</a>
    </centre>

The response curve of net photosynthesis to CO2 concentration inside the leaf of a C3 plant is shown above. At low levels, CO2 diffusion limits photosynthesis. With current atmospheric CO2 levels of around 390 ppmv most C3 plants would show an increase in photosynthetic rate with further increases. The magnitude of this is however uncertain due to plant acclimation and other factors. 

Over the long term, it is likely that *indirect* effects of elevated CO2 concentrations may be more important than increased net photosynthesis rates (Chapin et al., 2002), such as thoise arising from changes to the water cycle. 

C4 plants are relatively unresponsive to changing CO2 concentrations, which could possibly affect their competitaveness with C3 plants with rising CO2, but again, indirect effects are likely to be important and are hard to predict.

**Nitrogen limitation and photosynthetic capacity**

Photosynthetic capacity is the photosynthetic rate per unit leaf mass (in unstressed conditions). It isan important cocept as it can be thought of as the 'carbon gaining potential per unit of biomass invested in leaves' ((Chapin et al., 2002; p. 110). This measure is found to be highly positively correlated with leaf nitrogen *concentration*, because a large proportion of the nitrogen in leaves is used in photosynthetic enzymes:

.. figure:: figures/chapin3.png
    :align: center
    :target: figures/chapin3.png


.. raw:: html

    <centre>
    <i>
    "Relationship between leaf nitrogen concentration and maximum photosynthetic capacity (photosynthetic rate measured under favorable conditions) for plants from Earth's major biomes. Circles and the solid regression line are for 11 species from six biomes using a common methodology. Crosses and the dashed regression line are data from the literature. Redrawn from Reich et al. (1997)."
    </i>
    Source: <a href="http://sites.google.com/a/alaska.edu/f-stuart-chapin-terry/home/powerpoints-principles-of-ecosystem-ecology">Chapin, 2011, PTEEChap5.ppt, fig. 5.11</a>
    </centre>

The leaf nitrogen concentration can be affected by such factors as high nitrogen concentrations in soils which is why nitrogen fertilizers can be so effective) or whether the plants are `nitrogen-fixing <http://www.biology.ed.ac.uk/research/groups/jdeacon/microbes/nitrogen.htm>`_ through symbiosis with nitrogen-fixing bacteria in the soils.

We can also note that high photosynthetic capacities  (asociated with high leaf N concentrations) have higher *maximum* stomatal conductance. This allows such plants to gain carbon rapidly (n the absence of environmental stresses), at the cost of higher water loss.

.. figure:: figures/chapin4.png
    :align: center
    :target: figures/chapin4.png


.. raw:: html

    <centre>
    <i>
    "Relationship between leaf nitrogen concentration and maximum stomatal conductance of plants from Earth's major biomes. Each point and its standard error represent a different biome: bc, broad-leafed crops; ce, cereal crops; co, evergreen conifer forest; dc, deciduous conifer forest; df, tropical dry forest; gl, grassland; mo, monsoonal forest; sc, sclerophyllous shrub; sd, dry savanna; sw, wet savanna; tc, tropical tree crop; td, temperate deciduous broadleaved forest; te, temperate evergreen broadleaved forest; tr, tropical wet forest; tu, herbaceous tundra. Redrawn from Schulze et al. (1994)."
    </i>
    Source: <a href="http://sites.google.com/a/alaska.edu/f-stuart-chapin-terry/home/powerpoints-principles-of-ecosystem-ecology">Chapin, 2011, PTEEChap5.ppt, fig. 5.12</a>
    </centre>



A further observation relating to leaf N is that the higher the leaf N concentration, the shorter the leaf lifespan. Leaves with shorter lifspans tend to have lower specific leaf area (SLA, the leaf surface area per unit of biomass) (i.e. long-lived leaves are more dense), so higher leaf N concentration correlates with higher SLA.

.. figure:: figures/chapin5.png
    :align: center
    :target: figures/chapin5.png


.. raw:: html

    <centre>
    <i>
    "The effect of leaf lifespan on photosynthetic capacity, leaf nitrogen concentration, and specific leaf area. Symbols as in Fig. 5.13. Redrawn from Reich et al. (1997)"
    </i>
    Source: <a href="http://sites.google.com/a/alaska.edu/f-stuart-chapin-terry/home/powerpoints-principles-of-ecosystem-ecology">Chapin, 2011, PTEEChap5.ppt, fig. 5.13</a>
    </centre>


According to Chapin et al. (2002, p. 112) then, "there is only modest variation in photosynthetic capacity *per unit leaf area* because leaves with a high photosynthetic capacity per unit leaf biomass aalso have a high SLA". The Photosynthetic capacity per unit area (Parea) then (g cm-2 s-1) is a useful ecosystem-scale measure.


**Water limitation**

Water limitation reduces the capacity of leaves to match CO2 supply with light availability (Chapin et al., 2002, p. 113). Water stress is manifested as a decrease in leaf relative water content (`RWC <http://www.plantstress.com/Methods/RWC.htm>`_). Decreasing RWC progressively decreases stomatal conductance which slows CO2 assimilation (lower photosynthetic capacity) (Lawlor, 2002), although different studies show different responses for RWC between 100% and 70% (type 1 and 2 responses below).

.. figure:: http://aob.oxfordjournals.org/content/89/7/871/F1.large.jpg
    :align: center
    :target: http://aob.oxfordjournals.org/content/89/7/871.full
    :width: 50%

.. raw:: html

    <centre>
    <i>
    "A, Schematic of the basic responses of actual photosynthetic rate (A) in air (360 umol CO2 m-2s-1) and potential photosynthetic rate (Apot) measured at elevated CO2 concentration, to relative water content (RWC). Type 1 and 2 responses of Apot are shown. In the Type 1 response, Apot is unaffected until a 20-30 % decrease in RWC occurs, when it becomes metabolically limited. In Type 2, the change is linear, showing progressive metabolic limitation. In both types in well-watered leaves, photosynthetic rate (A) is stimulated by elevated CO2. Elevated CO2 maintains A at the potential rate (Apot) in the Type 1 response as RWC decreases; but at RWC below approx. 80 % Apot decreases in Type 1. Elevated CO2 simulates A progressively less as RWC decreases in Type 2, showing that Apot is inhibited. B, Scheme of the changes in CO2 inside the leaf (Ci) during steady-state A, as stomatal conductance (gs) decreases with falling RWC, associated with Type 1 or Type 2 photosynthetic response (1 with Ci decreasing to compensation point; 2 with Ci decreasing but not to compensation point). The equilibrium compensation point, Gamma, associated with Type 1 response is indicated. There are differences between experiments, with Ci not decreasing, or decreasing somewhat, or substantially. This may reflect different methods of assessing Ci."
    </i>Source: <a href="http://www.google.com.mx/url?sa=t&rct=j&q=water%20stress%20impacts%20on%20photosynthesis%20leaf&source=web&cd=4&ved=0CEYQFjAD&url=http%3A%2F%2Faob.oxfordjournals.org%2Fcontent%2F89%2F7%2F871.full&ei=mFwPT-byN4-BsgK_56T5Aw&usg=AFQjCNHxbp6Juudxaf5T4_kQzyn-0LzbCg&sig2=nk2IrpjmG_YeldiBzksCLA&cad=rja">Lawlor, 2002</a>
    </center>

In plants that are acclimated and adapted to dry conditions, plants reduce photosynthetic capacity and leaf N concentrations to give a low stomatal conductance that conserves water (Chapin et al., 2002, p. 113). Such plants also minimse leaf area (shedding or lower leaf production rates) to minimise water loss. Some such plants also minimise shortwave radiation absorption by higher reflectance at the leaf surface and or by having more vertically-inclined (erectophile) leaves.


**Temperature effects**


Extreme temperatures limit carbon uptake (Chapin et al., 2002, p. 114-115).

.. figure:: figures/chapin6.png
    :align: center
    :target: figures/chapin6.png 
    :width: 50%


.. raw:: html

    <centre>
    <i>
    "Temperature response of photosynthesis in plants from contrasting temperature regimes. Species include antarctic lichen (Neuropogon acromelanus), a cool coastal dune plant (Ambrosia chamissonis), an evergreen desert shrub (Atriplex hymenelytra), and a summer-active desert perennial (Tidestromia oblongifolia). Redrawn from Mooney (1986)."
    Source: <a href="://sites.google.com/a/alaska.edu/f-stuart-chapin-terry/home/powerpoints-principles-of-ecosystem-ecology">Chapin, 2011, PTEEChap5.ppt, fig. 5.19</a>
    </centre>

The figure above shows some typical response curves for plants adapted to different temperature regimes though, which means that what is considered extreme varies considerably between different plant types.

**Pollutants**

Finally, we mention pollutants (such as sulfur dioxide SO2) and Ozone (O3) in limiting photosynthesis. The main mechanism is by the pollutants entering and damaging the photosynthetic machinery (Chapin et al., 2002, p. 115). Plants can respond to this by reducing stomatal conductance to balance CO2 uptake with this reduced capacity, which also reducesthe entry of further pollutants.


Summary
-------

In this lecture, we have:

* considered the importance of understanding the science of climate change
* looked at basic principles of energy transfer in the earth system
* examined greenhouse gases and their sources
* looked in detail at the terrestrial carbon cycle
* provided an overview of relevant biogeochemical processes
* looked in some detail at photosynthesis and factors that limit this

Reading for this lecture
------------------------

This course cannot cover all aspects of climate science and related biological, chemical and physical/meteorological aspects in great detail. The emphasis of the course is on students developing an understanding of monitoring and modelling terrestrial carbon, so we provide only a brief overview of other aspects.

For further reading, some references are provided. Students are encouraged to fill the gaps in their knowledge in other areas using:

* IPCC Fourth Assessment Report: Climate Change 2007: `Working Group I: The Physical Science Basis <http://www.ipcc.ch/publications_and_data/ar4/wg1/en/contents.html>`_ and for a brief overview, the `IPCC FAQs <http://www.ipcc.ch/publications_and_data/ar4/wg1/en/faqs.html>`_.
* Monteith, J.L. and Unsworth, M., (2007), `Principles of Environmental Physics <http://www.amazon.co.uk/Principles-Environmental-Physics-John-Monteith/dp/0125051034/ref=sr_1_1?ie=UTF8&qid=1325699791&sr=8-1>`_, Academic Press
* Allen, R.G et al., 1998, `Crop evapotranspiration - Guidelines for computing crop water requirements - FAO Irrigation and drainage paper 56 <http://www.fao.org/docrep/X0490E/X0490E00.htm>`_ for a good practical guide to Agrometeorology, and a wider range of agricultural (and societal) documents in the `FAO Corporate Document Repository <http://www.fao.org/documents/en/docrep.jsp>`_.
* `AIP essay on Simple Models of Climate Change <http://www.aip.org/history/climate/simple.htm>`_
* Grace, J., (2001) Carbon Cycle, in *Encyclopedia of Biodiversity*, Vol. 1, Academic Press
* `Stevens, A. (2011) Introduction to the Basic Drivers of Climate. Nature Education Knowledge 2(2):6 <http://www.nature.com/scitable/knowledge/library/introduction-to-the-basic-drivers-of-climate-13368032>`_
* `Forseth, I. (2010) Terrestrial Biomes. Nature Education Knowledge 1(8):12 <http://www.nature.com/scitable/knowledge/library/terrestrial-biomes-13236757>`_
* `Stevens, A. N. (2011) Factors Affecting Global Climate. Nature Education Knowledge 2(1):5 <http://www.nature.com/scitable/knowledge/library/factors-affecting-global-climate-17079163>`_
* `Gough, C. M. (2011) Terrestrial Primary Production: Fuel for Life. Nature Education Knowledge 2(2):1 <http://www.nature.com/scitable/knowledge/library/terrestrial-primary-production-fuel-for-life-17567411>`_
* Chapin, F.S, Matson, P.A., and Mooney, H.A., (2002) Principles of Terrestrial Ecosystem Ecology, Springer (see also: `preview of 2011 book <https://sites.google.com/a/alaska.edu/f-stuart-chapin-terry/home/powerpoints-principles-of-ecosystem-ecology/current-text-principles-of-terrestrial-ecosystem-ecology>`_.
* Lawlor, D.W. (2002) Limitation to Photosynthesis in Water-stressed Leaves: Stomata vs. Metabolism and the Role of ATP, Ann Bot (2002) 89 (7): 871-885. `doi: 10.1093/aob/mcf110 <http://aob.oxfordjournals.org/content/89/7/871.full>`_


Texts of particular importance to this lecture are:

* Chapin, F.S, Matson, P.A., and Mooney, H.A., (2002) Principles of Terrestrial Ecosystem Ecology, Springer: Chapters 5 and 6 . (see also: `preview of 2011 book <https://sites.google.com/a/alaska.edu/f-stuart-chapin-terry/home/powerpoints-principles-of-ecosystem-ecology/current-text-principles-of-terrestrial-ecosystem-ecology>`_.
* Rockstrom, Johan; Steffen, Will; Noone, Kevin; Persson, Asa; Chapin, F. Stuart; Lambin, Eric F.; et al., TM; Scheffer, M et al. (2009). `"A safe operating space for humanity". Nature 461 (7263): 472-475. doi:10.1038/461472a <http://www.nature.com/nature/journal/v461/n7263/full/461472a.html>`_
* FAO Global Forest Resource Assessment 2010 [`pdf <http://www.fao.org/docrep/013/i1757e/i1757e.pdf>`_]
* Forests and Climate Change: Forcings, Feedbacks, and the Climate Benefits of Forests, G.B. Bonan, Science 320, 1444 (2008), DOI: 10.1126/science.1155121
* `Contribution of Working Groups I, II and III to the Fourth Assessment Report of the Intergovernmental Panel on Climate Change, Core Writing Team, Pachauri, R.K. and Reisinger, A. (Eds.), IPCC, Geneva, Switzerland. pp 104 <http://www.ipcc.ch/publications_and_data/publications_ipcc_fourth_assessment_report_synthesis_report.htm>`_
