---
layout: page
title: Air
---

---

![](https://c1.staticflickr.com/3/2905/14291435282_00e80785e9_h.jpg){:width="90%"}

This section includes air monitoring, air emissions and air modeling data.

* Add table of contents
{:toc}

## Monitoring 


### Current AQI observations {#aqi-now}

Air data for the entire United States is at your finger tips. _EPA's AirNow_ maintains a public repository of current air monitoring data at https://files.airnowtech.org/. 

_Data retrieved from AirNow is preliminary and may change following quality assurance._



### Active air monitors {#monitors}

A map of MPCA's air monitoring network is available online at [Minnesota air monitoring sites](https://www.pca.state.mn.us/air/minnesota-air-monitoring-sites).

A list of all active AQI monitoring locations around the United States are published to [_AirNow_](https://files.airnowtech.org/?prefix=airnow/today/) in the `monitoring_site_locations.dat` file.



### Retrieving data from AQS {#AQS}

The Air Quality System (AQS) contains ambient air pollution data collected by EPA, state, local, and tribal air pollution control agencies from over thousands of monitors. AQS also contains meteorological data, descriptive information about each monitoring station (including its geographic location and its operator), and data quality information.

__Options for retrieving data__:

- Registered users can access the AQS database via a web application at [https://www.epa.gov/aqs](https://www.epa.gov/aqs). 
- The __AQS Data Mart__ provides a convenient web API to access data stored in the AQS database. See the [AQS Data Mart](https://aqs.epa.gov/aqsweb/documents/data_mart_welcome.html).
    - Note the AQS Data Mart also requires a user name and password.These are not the same as your AQS User Account. Follow the instructions on the [Data Mart](https://aqs.epa.gov/aqsweb/documents/data_mart_welcome.html) page to request an account. 
    - The `RQAMD` package allows users to query the AQS Data Mart in R. See [RQAMD](https://github.com/ebailey78/raqdm) on Github.



### Retrieving MPCA data from LIMS {#lims}
The LIMS database is the primary data warehouse for AQ monitoring activities at the MPCA. The LIMS system is being retired and replaced. To ease data accessibilty during this transition LIMS data are available for download via an internal Tableau workbook at [http://tableau.pca.state.mn.us/#/workbooks/3342](http://tableau.pca.state.mn.us/#/workbooks/3342). 


### Retrieving continuous data from AirVision {#AirVision}
AirVision is the data acquistion and temporary storage database for continuous air monitoring data. Data collected in AirVision is transfered to LIMs and AQS for final data storage. If you need the most recent monioring observations and would like to access continuous data before it has been transfered to the final data repository you can run reports from AirVision.

To run reports, the AirVision client must be installed on your computer and you need an user account. Contact the Air Monitoring Supervisor to request credentials. Alternatively, an AirVision administator can create a report task that will generate a data report and send it to a specified location (FTP site or e-mail). 



### Retrieving data from the MPCA WAIR database {#wair}
The WAIR database provides a queryable local copy of select air quality data extracted from multiple data sources. This database is managed by Margaret McCourtney. Contact Margaret to request login credentials. 

See the [WAIR Data Dictionary](http://rainier.pca.state.mn.us/documentation/DataDictionary/wair/index.html) for available data tables.



### Air toxics

View and download summarized air toxics monitoring data results from the online [Air Toxics Data Explorer](https://www.pca.state.mn.us/air/air-toxics-data-explorer).



### Ultrafines {#ultrafine}

Want to learn more about ultrafine particles?

- __Explore the summarized data__:
- __Download raw data__:


### PAHs near facilities

- __Download PAH data__:


### PAHs in residential neighborhoods and rural areas

- __Download more PAH data__:






## Emissions


### MN Emissions Inventory {#mn-ei}
Every year all facilities (stationary point sources) report criteria pollutant emissions and every three years facilities report air toxics emissions. The EPA and the state of Minnesota emissions inventory team also calculate and report emissions for all other types of emissions sources such as mobile, non-road mobile, and area sources. These non-point emissions are reported every three years with the air toxics emissions. The Minnesota emission inventory is the foundation of MNRISKS. These emissions levels are reported in several data tools on the MPCA website. Their data and the visualization tools can be found on the following website [https://www.pca.state.mn.us/air/emissions-data](https://www.pca.state.mn.us/air/emissions-data).



### EPA National Emission Inventory (NEI) {#nei}
The National Emissions Inventory (NEI) provides air toxics and criteria and air toxic pollutant emissions for the entire U.S. on the same schedule as described in the Minnesota Emissions Inventory section. This information can be found at the [NEI](https://www.epa.gov/air-emissions-inventories/national-emissions-inventory-nei) website.


### Facility locations {#fac-coords}
The most recent compilation of coordinates for facilities with an air permit was performed for the 2017 emission inventory. This data is available in the `INV_SOURCES` table found in the _RAPIDS_ schema of MPCA's _DELTA_ database. These data can also be accessed from the `WH_TEMPO` schema by querying the "AI_METADATA" table.


### Facility emissions

[Explore point source emissions](https://www.pca.state.mn.us/air/point-source-air-emissions-data) 


### All sources emissions

[Explore all sources emissions](https://www.pca.state.mn.us/air/statewide-and-county-air-emissions) 


### GHG emissions

[Explore GHG emissions](https://www.pca.state.mn.us/greenhouse-gas-emissions-data) 




## Modeling


### NATA modeling {#nata}
The National Air Toxics Assessment is a nationwide air modeling effort to provide air concentrations and risks for all U.S. census tracts. These results may be pulled from a map project or data tables at [NATA](https://www.epa.gov/national-air-toxics-assessment). After each inventory is completed the Minnesota statewide cumulative air pollution model is compared to these results.



### MNRISKS statewide risk modeling {#mnrisks}
MNRISKS is the statewide cumulative air pollution model that is produced by MPCA every three years with the air toxics emissions inventory publication. The model itself produces point estimates for air concentrations and potential human health risks for hundreds of air pollutants across Minnesota. The model also incorporates a date and transport component that produces multi-pathway risk results. Census block group averaged results are available on MPCA's [Air modeling and human health](https://www.pca.state.mn.us/air/air-modeling-and-human-health) webpage.

<br>


### Downscaler modeling results for Ozone and PM2.5 {#downscale}
Downscaled data _(a blend of modeling and monitoring results)_ are provided by the CDC in cooperation with the EPA for the pollutants ozone and PM-2.5. Daily predicitons are available for each Census tract throughout the country for the years 2001 to 2013.

- CDC information about this platform is available online at [https://ephtracking.cdc.gov/showAirData.action](https://ephtracking.cdc.gov/showAirData.action).
- Data from this platform can be downloaded from the EPA at [https://www.epa.gov/air-research/downscaler-model-predicting-daily-air-pollution](https://www.epa.gov/air-research/downscaler-model-predicting-daily-air-pollution).
- Data filtered to Minnesota results is available in the folder: `X:\Programs\Air_Quality_Programs\Air Monitoring Data and Risks\6 Air Data\EPA Downscaler Modeling`.


### CMAQ Ozone modeling {#cmaq}

The Community Multiscale Air Quality Modeling System (CMAQ) is defined by EPA as:

> an active open-source project of the EPA that consists of a suite of programs for conducting air quality model simulations. CMAQ combines current knowledge in atmospheric science and air quality modeling, and an open-source framework to deliver fast, technically sound estimates of ozone, particulates, air toxics and acids deposition.


The information and data from this platform can be found at [CMAQ](https://www.epa.gov/cmaq).



