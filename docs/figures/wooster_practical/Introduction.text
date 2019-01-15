> ***Practical Class Module: Terrestrial Environmental Change 1***
>
> **Introduction to Remotely Sensed Fire Datasets and the IPCC
> Greenhouse Gas Inventory Process**

Introduction
============

> The purpose of this exercise is to provide you with some initial
> practical experience of the sort of products that are obtained on
> vegetation fires and biomass burning from Earth orbiting satellites,
> and an overview of how these fit into the IPCC Greenhouse Gas (GHG)
> Inventory Process. Those of you who do the module in *Remote Sensing*
> next semester will gain a fuller understanding of how these products
> are produced, but this level of understanding is not necessarily
> required if you wish to use the products in inventory or other
> analysis procedures such as this. If you do not complete this
> practical work in class you should ensure you go back and finish the
> rest in the coming days.
>
> **Learning objectives** are to gain an understanding of the process by
> which countries calculate and report their GHG emissions to the IPCC,
> and of some of the remotely sensed fire datasets that can be of use in
> these and other calculations.

By the end of this practical you should:
========================================

-   Understand the basis of the IPPCC process for estimating GHG
    emission from vegetation fires, and be able to use the basic
    spreadsheets involved in this calculation.

-   Understand the basics of Active Fire and Burned Area datasets and
    how they are derived from remote sensing observations, appreciating
    their main advantages and disadvantages

-   Use the ENVI Image analysis system to;

    -   Display image files

    -   Display vector files

    -   Perform simple mathematical operations on image datasets

-   Be able to search and order various fire datasets from online
    sources, such as the Fire Information for Resource Management System
    (FIRMS;
    [[http://maps.geog.umd.edu/firms/]{.underline}).](http://maps.geog.umd.edu/firms/))

-   Be able to access and interrogate the ATSR World Fire Atlas
    ([[http://wfaa-dat.esrin.esa.int/]{.underline})](http://wfaa-dat.esrin.esa.int/))
    to view long-term nighttime active fire data collected by the ATSR
    series of sensors.

Files
=====

> In your working directory, you are supplied with a number of files --
> these are:
>
> **IPCC\_GHG\_LULUCF\_merged.pdf --** the ***IPCC Good Practice
> Guidance Manual*** for estimating GHG Emissions from Land Use,
> Land-Use Change and Forestry. GHG emissions from open vegetation fires
> fall within this category.
>
> **Anx\_3A\_1\_Data\_Tables.pdf** -- Annex from the ***IPCC Good
> Practice Guidance Manual*** for estimating GHG Emissions from Land
> Use, Land-Use Change and Forestry. Page 3.179 -- 3.181 provides
> information necessary for calculating GHG emissions from open
> vegetation fires.
>
> **UNFCCC\_Software\_Manual.pdf** - the ***UNFCC GHG Inventory
> Software*** manual.
>
> **3C1c\_Biomass Burning GL.xls** - MS EXCEL file: Part of the UNCFF
> Inventory templates
>
> **Greece\_fires\_aug09.kml** -- burned area data of the 2007 Greek
> Fires
>
> **200909021445.img** - this is a spectral subset of an image captured
> by the SEVIRI sensor onboard the geostationary Meteosat satellite that
> images Africa and Europe every 15 minutes. Some details on SEVIRI can
> be found here:
> [[http://www.esa.int/msg/pag4.html]{.underline}](http://www.esa.int/msg/pag4.html)
>
> **ModisBurnedArea\_by\_country\_landuse\_vegetation.xls** - MS EXCEL
> file recoding the area burned in African countries based on the MODIS
> "burned area" product (see below)
>
> **MCD45A1.A2008214.h19v10.005.2008279131907.hdf** -- a MODIS "burned
> area" MCD45
>
> product file. This file is from year 2008, day of year 214 (which is
> 2^nd^ August). This file contains the data from the tile h19v10 --
> which is located in Southern Africa, and mostly over Angola.

![](media/media/image1.png){width="4.833419728783902in"
height="2.6068744531933508in"}

> *Figure 1: Tile locations representing the coverage of the MODIS Land
> Data Products (h19v10 covers the region around Angola for example).*

Practical Instructions
======================

> **3.1 The IPCC GHG Emissions Inventory Process**
>
> Load the IPCC Good Practice Guidance Manual in a PDF reader (by
> clicking on it) and goto Chapter 3 (Section 3.48; page 95 Headed
> "**GREENHOUSE GAS EMISSIONS FROM BIOMASS BURNING"**. This section
> covers emissions from biomass burning activity in areas where the land
> use remains the same (e.g. burns in forest remaining as forest after
> the burn; e.g. burning for land management) and also areas where the
> land use is changed (e.g. forest being cleared to use as cropland;
> e.g. burning for land use conversion).
>
> \[Note LUCF stands for Land Use Change and Forestry\].
>
> You can see that Equation 3.2.20 essentially states that the IPCC
> recommends use of the "standard" emissions estimation procedure to
> estimate GHG emissions from these types of fire, which we covered in
> our lecture:

Quantity of GHG released (L~fire~) = Area Burnt (A) (Equation 1)
================================================================

> **x Available Fuel Mass (B)**
>
> **x Fraction of Biomass Combusted (C)**
>
> **x Emissions Factor of the GHG (D)**
>
> Where
>
> L~fire~ is expressed in tonnes A is expressed in ha
>
> B is expressed in kg of dry matter per ha
>
> C is expressed as a unitless value from 0.0 to 1.0
>
> D is expressed as grammes of the GHG released per kg of dry matter
> burned
>
> \[Note the IPCC call factor C the Combustion Efficiency, which can be
> confusing as this also relates to another term in fire science -- the
> term Combustion Completeness would more correct.\]
>
> Immediately after Equation 3.2.20 in the document there is discussion
> on the accuracy of the estimates. This in part depends upon the data
> available to perform the calculation, which determines the level of
> detail (the so-called Tier Level) of the calculation. The following
> Figure shows the flowchart recommended by the IPCC to determine at
> which Tier Level to perform the calculation of GHG emissions \[in this
> diagram land use category FF means Forest Land remaining as Forest
> Land etc.\].
>
> If no more detailed data are available then the calculation of GHG
> emissions is done a "Tier 1" level for example, using primarily
> default data on fire activity levels and emissions factors.
>
> \[Note under the heading "3.2.1.4.24. Uncertainty assessment" the IPCC
> classify an uncertainty in fire activity data (i.e. burned area) of 20
> -- 30 % as "relatively small"...so it is apparent that great precision
> is not expected in these data\].

![](media/media/image2.jpeg){width="3.3373720472440946in"
height="4.333333333333333in"}

> *Figure 2: Decision tree for identification of appropriate tier-level
> for land remaining in the same land use category (example given for
> forest land remaining as forest land; also called FF).*
>
> The IPCC provide a set of computer-based tools to guide individual in
> country reporting of GHG emissions. These include simple MS EXCEL
> templates that guide users through the reporting process.
>
> Load up the XLS file ***3C1c\_Biomass Burning GL.xls*** into MS Excel
> to see one example of this type of template for GHG emissions from
> burning in grassland. You can see cells for all the
>
> parameters contained within the standard emissions equation (Equation
> 1) quoted above (Columns D, E and F). Columns I, J, K and L indicate
> that these individual terms should be multiplied together to obtain
> the final emissions estimates from fire, again as expressed in
> Equation 1 above.
>
> This rather simple process is the basis for the reporting of GHG
> Emissions from Land Use, Land- Use Change and Forestry, but how are
> the values for the parameters obtained?
>
> Look at the **IPCC Annex document Anx\_3A\_1\_Data\_Tables.pdf** and
> you will find on pages
>
> 3.179 -- 3.181 the information necessary for ascribing appropriate
> values to the B, C and D parameters of the above equation as a
> function of land cover and landuse. Take a look at some of the values
> for the parameters, and see by what magnitude they vary. Do they look
> realistic -- for example compare values for forest and grassland
> categories?
>
> The final piece of information - on burned area -- usually comes from
> remote sensing. The remainder of the practical will examine this data
> source.

Examining Remote Sensing Data on Biomass Burning
================================================

> You are going to use a piece of professional data analysis software
> called **ENVI**; the "***Environment for Visualizing Images***" to
> examine these data. It is a widely used computer package -- that is
> highly customizable and able to cope with many types of information.
>
> Load up ENVI from the *Start button* or by clicking on the *desktop
> icon.*

Active Fire Data
================

> These are essentially records of where a fire was identified to be
> actively burning at the time the image data were collected, with the
> detection based on infrared radiant "heat" signatures. **Advantages**
> of this type of data is that it operates day and night, is very
> sensitive to even rather small (sub-pixel) sized fires, and that it
> can detect the presence of a fire in real-time for use e.g. in
> forecasting of pollution plumes. **Disadvantages** are that clouds
> mask active fires from view, and if the fire is not capable of being
> "seen" by the sensor when it is actually burning (due to cloud-cover
> or just that it is extinguished before the satellite overpass) then it
> will not be present in the active fire record.
>
> Use *File/Open Image File* to load the file ***200909021445.img*** -
> this is a Meteosat SEVIRI full disk image taken on 2 Sept 2009 at
> 14:45 UTC -- close to the peak of the daytime fire activity during the
>
> southern African dry season. Meteosat is a geostationary satellite
> that views the entire Earth disk (Africa, Europe and part of South
> America) every 15 minutes. You can read about Meteosat and the SEVIRI
> imager it carries here
> [[http://www.esa.int/msg/pag4.html]{.underline}](http://www.esa.int/msg/pag4.html)
>
> In the SEVIRI image you will see the *Available Bands List* appear --
> and it is apparent that this image subset contains only three "bands"
> of information (the original SEVIRI imagery actually contains 12 bands
> of data; but the images are very large to work with). Our subset of
> data contains the brightness temperature (BT) data from the SEVIRI MIR
> (3.8 µm) spectral channel, the brightness temperature (BT) data from
> the TIR (10.8 µm) spectral channel, and the brightness temperature
> difference between these. You should remember from the lecture that
> the BT is a measure of the pixels temperature, based on the amount of
> thermal radiation being received from it in the particular spectral
> channel.
>
> Click on the *TIR\_BT* band and the *"Gray Scale"* radio button and
> then click *"Load Band"* at the bottom of the *Available Bands List*
> window. You will see the Meteosat full disk TIR image appear. Move the
> small red box in the *Scroll window* over southern Africa -- and you
> will see this part of the image appear in the main *Display Window*
> (and a zoomed version of a subsection of it appear in the *Zoom
> window*). Since this is a daytime image the land is warmer than the
> ocean (brighter in this rendition). Clouds are the coldest objects in
> the scene.
>
> ![](media/media/image3.jpeg){width="2.6879582239720037in"
> height="2.9895833333333335in"}
>
> *Figure 3: Meteosat SEVIRI TIR image, with Southern Africa boxed.*
>
> In the *Display Window* if you select *Enhance* and then *\[Image\]
> Linear 2%* a histogram "contrast" stretch will be applied to the
> displayed data in order to attempt to maximize the image contrast. You
> should be able to see patterns associated with lakes, clouds and
> rivers, which will be cooler than the land surface at this time. No
> obvious fires are apparent though.
>
> Now click on *New Display* in the *Available Bands List* window, and
> use the above procedure to instead display the MIR\_BT image.
> Histogram stretch it and you should clearly see some very bright
> pixels. In the Display window use *Tools/Cursor Location/Value* to
> display the pixel brightness temperatures. Confirm that the BT values
> of the fire pixels are much higher than those of the ambient
> background pixels, for the reasons we talked about in the lecture and
> that Figure 4 also indicates (i.e. that fires emit radiation much more
> intensely in the MIR than in the TIR spectral region; and so show up
> much more clearly against the background in the MIR).
>
> ![](media/media/image4.jpeg){width="5.185679133858268in"
> height="4.34in"}
>
> *Figure 4: Planck function plots for backbody emitters at a range of
> temperatures, from ambient (\~ 300 K) to those in vegetation fires (\~
> 1000 K). The approximate wavelength range of the SEVIRI MIR (3.7 µm)
> and TIR (10.8 µm) spectral channels are shown. On this y-asis scale,
> emission at ambient wavelengths is seen to be close to the zero level,
> but in fact peaks around the location of the TIR spectral band (at
> around 10 W/m²/sr/µm). By contrast, the wavelength of peak emission
> from vegetation fires is seen to be located close to the MIR spectral
> band, where around 4000 W/m²/sr/µm are emitted.*
>
> On the Display Window menu goto *Tools/Link/Link Displays* and
> "*link"* Display Windows 1 and 2. Now when you move about either of
> the windows the other will move to display the matching data. Confirm
> that pixels that clearly show fires in the MIR spectral band (as a
> high BT pixel value -- here displayed as a "bright" pixel) in general
> do not show a very strong "fire" signal in the TIR spectral band. You
> might want to load the *BT Difference image* (which record the BT
> difference between the MIR BT and TIR BT of a pixel) to confirm this.
> This "diff' image highlights the fire pixels very well, and suppresses
> the influence of ambient background variations due to elevation
> changes for example (since such elevation of landcover variations will
> affect the MIR and TIR BT values similarly, whereas a fire will affect
> the MIR value much more significantly due to its peak emission
> wavelength lying in that waveband; Figure 4). However, you can also
> see that areas of cloud cover can be a problem for fire detection
> algorithms -- as they too have high MIR-TIR BT difference values.
> Cloudy pixels are usually masked out using other tests based on
> visible and TIR channel thresholding.
>
> Data such as these are used to produce operational "fire products"
> that can be used as input into the IPCC process. Lets check the
> performance of the operational SEVIRI fire detection algorithm -- used
> at the EUMETSAT Land Satellite Applications Facility identify active
> fire pixels and measure their emitted power (you can read the product
> details at
> [[http://landsaf.meteo.pt/]{.underline}](http://landsaf.meteo.pt/) and
> click on "Fire Radiative Power -- Pixel".
>
> We also have a vector (shapefile) that shows the locations of all the
> active fire pixels detected by the automated fire detection scheme in
> this imaging slot. We can view this now and compare it to the MIR BT
> data. First, in ENVI, *close* all the display windows apart from
> Display 1 -- which should still be showing the MIR BT data.
>
> On the Display Window Menu use *Overlay/Vectors* and then *File/Open
> Vector File* to open the Shape File:
> **HDF5\_LSASAF\_MSG\_FRP-PIXEL-ListProduct\_SAfr\_200909021445.shp**
>
> \[You will need to change the "type of file" to *"Shapefile (\*.shp)"*
> in the open file dialogue window\]. Just click OK to accept all the
> defaults in the Vector Import dialogue window.
>
> Click the *Current Layer* colour square to change the colour of the
> vector points to another colour that is easier to see (e.g. red) and
> then press *Apply*. Now click "off' in the top right of the Vector
> Parameters window so you can scroll around the image window.
>
> Confirm to yourself that the fire pixel locations are reliably
> detected by the active fire detection algorithm used in the LandSAF
> FRP Pixel product. This is most clearly done using the Zoom Window --
> where you can click on the + and -- symbols to zoom in and out. You
> should find that the location of the detected fire pixels match well
> with the pixels showing increased MIR brightness temperatures.
> However, you might quite easily be able to find some pixels where the
> MIR BT signature looks like the pixel might contain a fire, but where
> the fire detection algorithm has not detected one (i.e. a likely
> omission error). Errors of commission (i.e. false detections) should
> be quite low though (\< 10%).
>
> Timeseries of active fire data like this can be used to estimate the
> area burned for input into the IPCC GHG Emissions estimation procedure
> (essentially by calculating the number of discrete fire pixels that
> occur in an area of interest). However, in these types of
> grassland-dominated or woodland environments a better type of product
> from which to estimate burned area is likely to be one based on
> detection of reflectance changes due to burning. We will examine this
> type of product next.

ATSR World Fire Atlas (WFA) Long-Term Active Fire Data Record
=============================================================

> The ATSR series of polar orbiting satellite sensors has delivered the
> longest-running data record of active fire detections currently
> available, starting from 1995 to the present period. The record is
> termed the World Fire Atlas (WFA) and is derived via a very simple
> thresholding algorithm applied to nighttime observations made in the
> ASTR MIR spectral band. Though fires are generally much more active by
> day than by night, these observations do provide a reasonable data
> source from which the seasonality and interannual variability of fire
> in any particular region can be determined. Another positive point is
> that the WFA is very simple to use, and there is a web interface that
> is very easily understood
> ([[http://wfaa-dat.esrin.esa.int/]{.underline}).](http://wfaa-dat.esrin.esa.int/))
> A user guide for this can be found at
> [[http://wfaa-dat.esrin.esa.int/wfa\_user\_guide.pdf]{.underline}](http://wfaa-dat.esrin.esa.int/wfa_user_guide.pdf)
> and the web interface allows selection of the data from a single
> county, graphing of total annual active fire counts for that country
> over many years, examination of a single year in terms of monthly
> active fire count (to examine seasonality) and also export of ascii
> data containing the hotspot locations and dates. A paper using the WFA
> data can be found at
> [[http://www.atmos-chem-phys.net/8/1911/2008/acp-8-1911-2008.html]{.underline}](http://www.atmos-chem-phys.net/8/1911/2008/acp-8-1911-2008.html)
> and a paper on some of the issues to take into consideration with this
> dataset is [http://www.atmos-chem-]{.underline}
> [phys.org/6/1409/2006/acp-6-1409-2006.html]{.underline} . Take some
> time now to select a fire-affected country and examine the different
> possibilities for display of the ATSR WFA data record. First select
> the continent and country, then on the upper left hand side the date
> range and lower left hand side the output format. Finally press
> "Search" to display the data record.

Burned Area Products
====================

> These are essentially records of where a fire was identified to have
> burned the landscape, with the detection based on changes in the
> reflectance (or "colour") of the surface. In the lecture we saw that
> when an area of vegetation burns, its spectral reflectance generally
> falls since the vegetation is partly removed and the ground surface
> becomes at least partly covered by a layer of dark char. The
> advantages and disadvantages of this type of product are in some ways
> opposite to the active fire products you examined previously.
> **Advantages** of burned area products are primarily that they are a
> direct estimate of the actually burned area for use in Equation 1, and
> that secondly if clouds mask the surface from view during a particular
> satellite overpass, then it is quite likely that the burned area can
> still be detected on the next overpass (in fact in some environments
> it can be detected for many weeks or even months). **Disadvantages**
> are that they are often not very sensitive to small burns, and that
> since they only respond to changes in surface reflectance caused by
> the fire -- they only really provide useful data after the fire has
> happened (so do not provide "real time" information). They also only
> provide usable data during daytime overpasses.
>
> As we discussed in the lecture, the sore of spectral reflectance
> signature change associated with burning can be quite reliably
> detected by sophisticated algorithms trained to look for such temporal
> changes. In Figure 5 below, you can see the "darker" colour signature
> of the imaged burned area, and in the spectral reflectance time series
> you can see how the pixel that burns around day 274 experiences a
> sharp decrease in reflectance ((open triangles) compared to the pixel
> that does not (closed triangles).

![](media/media/image5.jpeg){width="1.898371609798775in"
height="1.8416666666666666in"}![](media/media/image6.jpeg){width="4.350488845144357in"
height="1.3933333333333333in"}

> *Figure 5: Planck function plots for backbody emitters at a range of
> temperatures, from ambient (\~ 300 K) to those in vegetation fires (\~
> 1000 K). The approximate wavelength range of the SEVIRI MIR (3.7 µm)
> and TIR (10.8 µm) spectral channels are shown. On this y-asis scale,
> emission at*
>
> One of the most commonly used burned area products is that produced
> from the MODIS sensor. You can read some background about MODIS at
> [[http://afis.meraka.org.za/wamis/modis\_basics.php]{.underline}](http://afis.meraka.org.za/wamis/modis_basics.php)
>
> The MODIS burned area product (MCD45) is a "Level 3" gridded 500m
> product, meaning that it represents heavily processed information
> produced from MODIS data via use of a dedicated set of algorithms,
> rather than "raw" MODIS data. It is produced in the standard MODIS
> *Land Tile* format in sinusoidal projection. Each tile has fixed
> earth-location, as shown in the first figure in this practical
> handout, and covers an area of approximately 1200 x 1200 km (10° x 10°
> at the equator). The product defines for each 500 m pixel within the
> tile the approximate day of burning -- identified via changes in
> spectral reflectance such as that shown in Figure 5. The MCD45 product
> is obtained from processing combined MODIS-TERRA and MODIS-AQUA 500m
> land surface reflectance data, and is stored in Hierarchical Data
> Format (HDF) -- a common data format used for science datasets.
>
> More info:
> [[http://modis-fire.umd.edu/MCD45A1.asp]{.underline}](http://modis-fire.umd.edu/MCD45A1.asp)
>
> User guide:
> [[http://modis-fire.umd.edu/documents/MODIS\_Burned\_Area\_Users\_Guide\_1.1.pdf]{.underline}](http://modis-fire.umd.edu/documents/MODIS_Burned_Area_Users_Guide_1.1.pdf)
>
> To explore use of the MODIS MCD45 Burned Area product product, have
> ENVI running and Click on *File -- Open External File -- Generic
> Format -- HDF.* This opens HDF files (i.e. in this case the individual
> MODIS MCD45 tile data of burned area).
>
> The HDF format file supplied contains the following datasets relating
> to burned area in one file. Select the *"Burn Date"* dataset and click
> OK. This will display the estimated date of the burn (i.e. in the
> Figure 5 example day 274) data as an item in the *Available Bands*
> window. From here it can be displayed in an image window.

![](media/media/image7.png){width="1.7020877077865266in"
height="2.455415573053368in"}

> *Figure 6: The HDF datasets contained in the example MCD45 file
> provided.*
>
> Display the *Burn Date* dataset with ENVI as you did with the previous
> Meteosat SEVIRI imagery. You should see it as an apparent binary
> (black/white) tile of data covering part of southern Africa - with
> ocean to the west of the scene, and some lakes mainly in the south.
>
> Use the *Tools/Cursor Location/Value* command from the *Display
> Window* menu to check the digital number (DN) given to these pixels,
> you should see it as a very large value (10000 or 9999) whereas the
> background land surface is given a value of zero. Actually this
> dataset contains the map of burned area, where each pixel is coded
> with the day of the year on which it was detected as being burnt (so a
> value from 1 to 365) but you just cannot see it as displayed here
> since the contrast stretch automatically being applied to the data is
> essentially making all these pixels appear black on the computer
> monitor. This is because the contrast has to encompass the display of
> numbers from 0 to 10000.
>
> We can use some simple mathematical operations to deal with this
> problem. On the ENVI main menu goto *Basic Tools* and then *Band
> Math*. In the "*enter the expression"* dialogue box type in the
> mathematical expression **(b1 lt 400)\*b1** \[where "lt" stands for
> "less than"\]
>
> In this expression, b1 represents the variable (band of data) you are
> going to process and the expression essentially says:
>
> *"Take the band of data (b1) and where a pixel has a value of less
> than 400 (i.e. a burnt or a non- burned land pixel, rather than a lake
> or ocean pixel) give it the value of 1, otherwise give it a value of
> 0. Then multiply this by the original data values."*
>
> Essentially then this should provide a dataset very similar to the
> original data, but with the 9999 and 10000 values removed.
>
> Click OK and select the *"Burn Date"* as the variable *b1* and choose
> to *"Output the result to Memory"* (rather than "File"). The output
> from this operation should appear in the *Available Bands List*. Now
> *Display* it in a new display window.
>
> The image will very likely initially appear black, but if you select
> *Enhance-Histogram* and then *\[Scroll\] Linear 2%* you should see a
> large number of burned areas appear. Move the red box around the
> *Scroll Window* until the *Display Window* shows one of the areas most
> affected by burning. Each pixel here represents an area of around 500
> m x 500 m on the ground -- so these burns are rather large, and there
> are very many of them. You can see just what a large proportion of
> this environment burns each year.
>
> Each burnt pixel is coded by the day it burnt. You can best display
> this using a *colour palette*. Onthe display window goto *Tools/Colour
> Mapping/Envi Colour Tables*. Scroll down to the end of the *Colour
> Table* list to find the *Rainbow + White* colour table and highlight
> it. Then move the *"stretch bottom"* slider to the right - this
> controls how the values in the file are translated to colours in the
> colour table. You should be able to adjust the display so that you can
> see the different dates on which each pixel burnt by its displayed
> colour -- and some of the larger burns you can see the daily
> progression of the burn as the fire evolved.
>
> Now load the EXCEL file:
> **ModisBurnedArea\_by\_country\_landuse\_vegetation.xls** this stores
> the amount of burned land detected by the MODIS burned area product by
> African country, and also by vegetation type and landuse -- exactly
> the information that the IPCC GHG Emissions Inventory process that we
> examined earlier requires.
>
> Load up the **"SummarybyCountry"** worksheet in EXCEL and look at the
> country of **Angola** -- the location of the MODIS Burned Area product
> you were just examining. You can see that Angola has a land area of
> almost 2.8 million km² and that on average 27% of it burns every year
> - equivalent to just over a 4 year mean fire return interval. Going to
> the **summary\_byCountryVegLanduse** worksheet and you can see that a
> landuse/landcover map has been used with a GIS to break down this
> total burned area into different vegetation classes (grassland, forest
> etc) and different landuse types (cultivated lands, protected areas
> etc). This is the last piece of information required by the different
> stages of the IPCC Inventory process -- and now the emissions
> inventory equation can be completely parameterised for each land use
> class.
>
> Should you wish to examine or use more "Burned Area" data, the best
> way to obtain these MODIS Burned Area products is listed at
> [[http://modis-fire.umd.edu/index.html]{.underline}](http://modis-fire.umd.edu/index.html)
> (click on Burned Area Products at top, and then "Get Data" at left).
> Early generations of the MCD45 product had provisional product
> maturity status, but this is common and the validation and
> intercomparison exercises are ongoing and the product performance is
> increasing with each new version.
>
> For now we will see how to get some other forms of remotely sensed
> fire data -- from a system called FIRMS.

Accessing Other Remote Sensing Fire Information
===============================================

> The Fire Information for Resource Management System (**FIRMS**):
> [[http://maps.geog.umd.edu/firms/]{.underline}](http://maps.geog.umd.edu/firms/)
> provides information on global fire activity for use in resource
> assessment. Soon these data should also be available via the FAO
> Global Fire Information Management System. For more information see:
> [[http://maps.geog.umd.edu/firms/readmore.htm]{.underline}](http://maps.geog.umd.edu/firms/readmore.htm)
>
> For now we can concentrate on use of the data from FIRMS. These
> systems offer a variety of downloadable data on fire, mostly again
> taken from the MODIS sensor and concentrating on "active fire" rather
> than "burned area" datasets.
>
> The MODIS active fire products are available in a variety of
> easy-to-use data formats. The data themselves are similar to the
> Meteosat SEVIRI active fire data you used earlier, albeit from
> observations made every \~ 6 hrs from MODIS' polar orbit rather than
> every 15 minutes from Meteosats geostationary orbit. The formats
> include:

a.  Shapefiles of fire locations from the past 48 hours and past 7 days

b.  Daily text files of fire locations via ftp site for the past two
    months

c.  Daily/weekly/near real-time CSV/text files of fire locations via
    email alerts

> Another site where a version of these same data are available via a
> quick web interface is called the Web Fire Mapper.
>
> Before examining the FIRMS data, take a look at the Web Fire Mapper
> at:
> [[http://firefly.geog.umd.edu/firemap/]{.underline}](http://firefly.geog.umd.edu/firemap/)
> and try to find on which continents a large amount of fire activity is
> taking place currently (this will depend primarily on the time of
> year, since fire activity has a marked seasonality related to
> climate). Whilst you search, select "Blue Marble" as the background
> image (this is a global colour composite produced from MODIS imagery
> that quite nicely shows the patterns of vegetation over the land
> surface). This will provide you with an idea of the vegetation
> conditions, for example with "brown/bare" areas having insufficient
> fuel to carry a strong fire.
>
> Once you have found a suitable location of fire activity, try
> accessing the FIRMS system to download some vector (**shapefiles)**
> relevant to these fire locations. You can do so for the past 24 hrs,
> 48 hrs or 7 days and can examine the data in ENVI as you did
> previously for the Meteosat SEVIRI-derived active fire shapefiles
>
> **Goto**
> [[http://maps.geog.umd.edu/firms/shapes.htm]{.underline}](http://maps.geog.umd.edu/firms/shapes.htm)
> and select the area you have identified as being fire-affected at the
> present time. Select the 24 hrs, 48 hrs or 7 day product to *download*
> the ZIP file - and then extract the contents of the ZIP file to your
> temporary working directory.
>
> Now goto *ENVI* once again and use *File/Open Vector File* (with file
> types set to **Shapefile**). Select the **\*.shp** file you just
> unzipped and click OK to accept all the default *Vector Parameters*.
> You should see vector points (**white crosses)** appear at locations
> where fires were identified by MODIS to be burning within the period
> you selected. If you chose to *download the text version* you could
> check the lat/long location of these fires in a *text editor* or
> *spreadsheet*. However, we can get an idea where they are by using a
> vector file of *Country Boundaries*.
>
> In the *Available Vectors List* window, goto *Options* and *Create
> World Boundaries*. Select *Politcal (Low Res)* and *Coastlines (Low
> Res)* -- which are numbers 4 and 5 in the list -- and also select the
> output to *"memory"* rather than to a file.
>
> Click OK. Then choose to display all the layers you have made by
> selecting *"Select All Layers"* in the *Available Vectors List* -- and
> then *Load Selected*.
>
> Choose to load these in a new *Vector Window*. You will see the world
> map, together with the fires.
>
> Now in the menu of this *Vector Window* goto *Options, Select Active
> Layer* and ensure the *Active Fire layer* is selected, rather than the
> world map. Then goto *Edit* and *View/Edit/Query Attributes* to see a
> list of the active fire detections and their various parameters
> (location, time, signal strength etc). These are the detailed
> information on each fire detection, that is also available in the text
> file version of the same dataset if you prefer.
>
> Finally, there is also a **Google Earth KML** version of the same data
> available from FIRMS:
> [[http://maps.geog.umd.edu/firms/kml.htm]{.underline}.](http://maps.geog.umd.edu/firms/kml.htm)
>
> KML format data of burned areas are also available, for example from
> the **European Forest Fire Information System (EFIS),** which can be
> found at [[http://effis-]{.underline}](http://effis-/)
> [viewer.jrc.ec.europa.eu/wmi/viewer.html]{.underline}
>
> Load up the example you have been supplied with -
> **Greece\_fires\_aug09.kml** in ***Google Earth*** -- it contains
> burned area vector format data of the 2007 Greek Fires, derived from
> the MODIS MCD45 Burned Area product. Compare it visually with the
> original MODIS burned area product data,
>
> shown on the image of Greece below:

![](media/media/image8.jpeg){width="4.634324146981627in"
height="5.716666666666667in"}

> *Figure 7: Burned area map of the 2007 Greek fires, derived from the
> MODIS Burned Area Product (MCD45). Figure taken from Boschetti et al
> (2008).*

References:
===========

> Boschetti, Luigi, Roy, David, Barbosa, Paulo, Boca, Roberto and
> Justice, Chris (2008) A MODIS assessment of the summer 2007 extent
> burned in Greece, *International Journal of Remote Sensing*, 29, 2433
> -- 2436.
