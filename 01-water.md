---
layout: page
title: Water
---

---

![](https://c1.staticflickr.com/1/600/23162395351_fbd8d6a019_h.jpg){: width="90%"}


The MPCA collects water data for ambient monitoring and point source regulation. There are several sources of _water data_ and all are substantial, so you will want to refine your search.  

Ambient data are collected and stored by both the Watershed (EQUIS) and Watershed Pollutant Load Monitoring Network (Hydstra) programs.    

Regulated parties submit wastewater data to the Regulated Services Portal (RSP) and it is transferred to the MPCA permitting database (TEMPO).

## Wastewater

### **Monitoring data types**

Wastewater facilities are issued federal (**NPDES**) or state (**SDS**) permits.  Federal permits discharge to a surface water and state permits do not.  Both types of permits are required to submit monitoring data to the PCA.   

Facilities collect data and report data on daily, monthly, quarterly, and annual time periods.    

**Discharge Monitoring Reports (DMRs)** are the most common submittal and contain information influent and effluent results for each facility. The values can be monthly, quarterly, or yearly data.  Tempo contains data from 1998-present and pre-1998 information is available in a different format from the EPA PCS database.    

**Monitoring data categories**

Monitoring data are reported for surface discharge (**SD**), influent/internal waste (**WS**), groundwater monitoring (**GW**), ambient surface water (**SW**), and land application (**LA**) stations.  

**Sample values** are the daily samples used to calculated DMR results.  These are submitted along with DMRs and typically stored as attachments in the permitting database.  Digital sample values exist after 2014 and pre-2014 values are stored in scanned supplemental forms.    

### **Where to find data?**   
Currently the most comprehensive source of wastewater data is the [Wastewater Data Browser.](https://www.pca.state.mn.us/data/wastewater-data-browser)  This application focuses on monthly DMRs but also contains facility and station details.  The "Download Data" button for the Data Browser is in the lower right corner of the application

The DMR data have been available to the public for many years but the MPCA updated to a new reporting software in 2015 with more filtering capability.

There are a few things to consider when using wastewater monitoring data.  No data source is perfect and with thousands of stations and millions of reported values there may be erroneously reported data.  While the MPCA makes reasonable effort to ensure data accuracy, the MPCA does not warrant the accuracy or completeness for any implied data uses.    

#### Facilities, permits, and requirements
The MPCA does not currently publish wastewater permits externally.  Since permit holders are required to submit a DMR each month the Data Browser is an effective tool for mapping facility locations.  

The application contains spatial data for each facility and station so users can identify facilities monitoring for a pollutant of interest.  The map on the application is very basic but the coordinates are part of the tabular exports for use in desktop mapping software.

Adjusting the filter to only show Flow provides a list of active wastewater permits within the defined time period.  Facilities are required to submit a DMR each month even if they did not discharge any wastewater.  The view "Facility Coordinates Flow" contains a list of facilities by waste and flow type with outfall locations.  The "Station by Watershed" data view is very similar but focuses on watershed and sub-watershed boundaries.

The view "Facility Monitoring Parameter" provides details and locations of limits and monitoring requirements.  These data are intended for generating pollutant limits and monitoring maps.


#### Monitoring results
Monthly monitoring results are available on the "Reported values over time" view as a line graph, or in the DMR Bulk Export sheet as a tabular download.  The Bulk Export is intended for use in spreadsheet or modeling software.   

The Wastewater Data Browser is updated quarterly and shows values "as reported."  It not intended for checking monthly submittal status and will typically be 1-3 months behind the current month.   

Daily sample values are available digitally after 2014 and available through the MPCA [Information Request form.](https://www.pca.state.mn.us/about-mpca/information-requests])
Prior to the 2014 eDMR project the majority of sample values were stored as scanned pdfs or Excel files.    

### Details about wastewater data    


#### Permits and stations
Historically location data were reported by PLS sections and as technology improved the permit application requested coordinates.  A coordinate improvement project in 2009 corrected 85% of the municipal SD stations.  Non-SD stations are still a work in progress, as are industrial SD stations.  Facility and station coordinates should **always** be reviewed.

#### Monitoring results    
Monitoring data are not automatically entered in the database from lab results.  The DMR form contains calculations for monthly average, total, and percent removal so operators calculate and enter data each month.  This introduces the possibility for calculation and transcription errors.  As data are reviewed facilities can revise (amend) DMRs with correct values.    

The most common and significant reporting error is the missing flow decimal point.  Facilities are required to report in million gallons per day (mgd) but smaller facilities often report a value of gallons.  This type of error incorrectly increases flow values and makes subsequent analysis incorrect.    

Other less common errors are concentration decimal points, switching monthly totals with averages, and not using all 30 days for monthly loading values.    
#### Loading calculations    
The MPCA performs pollutant loading calculations to estimate loads from the monthly flow and concentration data.  These loading estimates are mostly used in annual reports to visualize statewide and regional trends.  The data are processed and manipulated to get a consistent and full multi-parameter dataset.  

This manipulation requires a reference table pairing the correct flow station and type to the corresponding concentration.  There are rules to exclude suspected outliers.  Since not all facilities have full concentration datasets some loading values use annual average concentration or a categorical assumption from similar facilities.    

The resulting loads are assigned a confidence category indicating "Observed, Estimated from sample, or Estimated."

Loading data are used in the [MPCA Pollution Reports](https://www.pca.state.mn.us/about-mpca/legislative-resources) and are not currently published in a data application.


## Watersheds    
The [Watershed Pollutant Load Monitoring (WPLMN)](https://www.pca.state.mn.us/wplmn/overview) program collects ambient data for many streams and rivers.  It is a collaborative process and the group uses [FLUX32](https://www.pca.state.mn.us/wplmn/flux32) to calculate daily loads.    

Ambient watershed loads are available at the daily, annual, and average scales in a [Tableau application.](https://www.pca.state.mn.us/wplmn/data-viewer)    

Comparing ambient and point source pollutant loads is a tempting endeavor but should only be done with the necessary data stipulations.  Annual comparisons lose the impact on local stream conditions because wastewater's influence is greatest during summer months.  Stream flow is lower in late summer and oxygen levels decrease with increasing temperature so fish and aquatic insects are more easily stressed.
