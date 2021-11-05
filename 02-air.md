---
layout: page
title: Air
---

This section includes air monitoring, air emissions and air modeling data.

---

![](https://c1.staticflickr.com/3/2905/14291435282_00e80785e9_h.jpg){:width="90%"}


* Add table of contents
{:toc}

## Monitoring 


### Current AQI observations {#aqi-now}

Air data for the entire United States is at your finger tips. _EPA's AirNow_ maintains a public repository of current air monitoring data at https://files.airnowtech.org/. 

_Data retrieved from AirNow is preliminary and may change following quality assurance._



### Active air monitors {#monitors}

A map of MPCA's air monitoring network is available at [Minnesota air monitoring sites](https://www.pca.state.mn.us/air/minnesota-air-monitoring-sites).

A list of active AQI monitoring locations around the United States are published to [_AirNow_](https://files.airnowtech.org/?prefix=airnow/today/) in the `monitoring_site_locations.dat` file.



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

```{r pull all the data}

##packages
library(tidyverse)
library(openair)
library(ggplot2)
library(RcppRoll)
library(lubridate)
library(DT)
options(scipen = 999)

ufp <- read.csv("X:/Programs/Air_Quality_Programs/Air Monitoring Data and Risks/6 Air Data/UFP Processing/Data File/r_checked_rules.csv", stringsAsFactors = F)
```
- __Download raw data__:

```{r get ftp ufps}
##Pull and Process UFP Instrument Data

##libraries
library(tidyverse)
library(reshape2)
#library(taskscheduleR)
library(lubridate)
library(XML)
library(RCurl)

options(scipen = 999)

###########################
###Create Current Table of out of bounds limits
parameters <- c("ChargerCurrent", "SheathFlow", "SheathTemperature", "20-30 nm", "30-50 nm", "50-70 nm", "70-100 nm", "100-200 nm", ">200 nm")
hi_limit <- c(1050, 21, 40, 22603, 14447, 7239, 5268, 4874, 1064)
low_limit <- c(950, 19, 10, 0, 0, 0, 0, 0, 0)

control_limits <- data.frame(parameters = parameters, hi_limit = hi_limit, low_limit = low_limit, stringsAsFactors = FALSE)

#########################
##Set up the ftp site
airvis_link <- "ftp://airvis:mpca@34.216.174.58/airvision/"
##For next time you're looking for UFP data - The new FTP address has these numbers: @34.216.61.109/airvision/ 
#############################
##Pull in pre-automated data (files with data to March 7, 2018)
setwd("X:/Programs/Air_Quality_Programs/Air Monitoring Data and Risks/6 Air Data/UFP Processing/AirVision Data")

ufp_files <- list.files()
ufp_temp <- data.frame()

for(i in ufp_files){
airvis_df   <- read_delim(i, delim = "\t", col_names = FALSE, skip = 4, na = c("", "NA"), trim_ws = TRUE)
col_names_df   <- read_delim(i, delim = "\t", n_max = 3, col_names = FALSE, skip = 1, na = c("", "NA"), trim_ws = TRUE)
col_names_df <- filter(col_names_df, !is.na(X2))
col_names_t <- as.data.frame(t(col_names_df))
col_names_list <- paste0(col_names_t$V1, "_", col_names_t$V2)
colnames(airvis_df) <- col_names_list
ufp_temp <- rbind(airvis_df, ufp_temp)
print(i)
print(length(is.na(airvis_df$NA_Date)))
}

#############################
##Pull in newest file on FTP site
##Air vision is timing out before hte files can download, so I am manually saving files to this X drive location: X:\Programs\Air_Quality_Programs\Air Monitoring Data and Risks\6 Air Data\UFP Processing\AirVision Data

##file_name_new <- paste0("962_UFP_", year(Sys.Date()), format(Sys.Date(),"%m"), "12.TXT")
#airvis_df_new   <- read_delim(paste0(airvis_link, file_name_new), delim = "\t", col_names = FALSE, skip = 4, na = c("", "NA"), trim_ws = TRUE)
#col_names_df_new   <- read_delim(paste0(airvis_link, file_name_new), delim = "\t", n_max = 3, col_names = FALSE, skip = 1, na = c("", "NA"), trim_ws = TRUE)

#col_names_df_new <- filter(col_names_df_new, !is.na(X2))
#col_names_t_new <- as.data.frame(t(col_names_df_new))
#col_names_list_new <- paste0(col_names_t_new$V1, "_", col_names_t_new$V2)
#colnames(airvis_df_new) <- col_names_list_new

#ufp_temp <- rbind(ufp_temp, airvis_df_new)
#ufp_temp <- unique(ufp_temp)

##########################
##Save interim dataset for rule script
write_csv(ufp_temp, "X:/Programs/Air_Quality_Programs/Air Monitoring Data and Risks/6 Air Data/UFP Processing/Data File/ufp_data_raw.csv")
```

- __Quality check the data__:

```{r data validation}
##libraries
library(tidyverse)
library(openair)
library(ggplot2)
library(RcppRoll)
library(lubridate)
library(car)
library(DT)
options(scipen = 999)

ufp <- read.csv("X:/Programs/Air_Quality_Programs/Air Monitoring Data and Risks/6 Air Data/UFP Processing/Data File/r_checked_rules.csv", stringsAsFactors = F)


##Check for drift
reportable_data <- ufp %>% 
  filter(Null_Code != "AN",
         !Size %in% c("ChargerCurrent", "SheathFlow", "SheathTemperature")) 
sizes <- unique(reportable_data$Size)
reportable_data$year <- year(reportable_data$Date)
years <- unique(year(reportable_data$Date))
reportable_data$quarter <- quarter(reportable_data$Date)
quarters <- unique(quarter(reportable_data$Date))
reportable_data$quarter_year <- paste0(quarter(reportable_data$Date), "_", year(reportable_data$Date))

levene_function = function(Result, quarter_year, row, col) {
  if(length(unique(quarter_year)) < 2){
    return(NA)} 
  data = data.frame(Result = Result, quarter_year = quarter_year)
  return(leveneTest(Result ~ as.factor(quarter_year), data = data)[row,col])
}

leak_table_unfiltered <- data.frame()
for(i in max(years):max(years)-1:length(years)){
  for(j in i + 1){
    data = data.frame()
    data <- filter(reportable_data, !is.na(Result), year %in% c(i, j))
    data <- data %>% group_by(Size, quarter) %>% 
      summarise(fvalue_levene = levene_function(Result, quarter_year, 1,2), 
                pval_levene = levene_function(Result, quarter_year, 1,3), 
                deg_free_levene = levene_function(Result, quarter_year, 2,1),
                Year_1 = min(year), 
                Year_2 = max(year),
                Mean_Year_1 = mean(Result[year == min(year)], na.rm = T),
                Mean_Year_2 = mean(Result[year == max(year)], na.rm = T)) %>% ungroup()
    leak_table_unfiltered  <- rbind(leak_table_unfiltered,data)
  }
}
leak_table <- filter(leak_table_unfiltered, abs(Year_1 - Year_2) == 1)


write_csv(leak_table, "X:/Programs/Air_Quality_Programs/Air Monitoring Data and Risks/6 Air Data/UFP Processing/Data Validation Tool/levene_table.csv")

###################################
##Check for repeats--sticky values

repeat_data <- group_by(reportable_data, year, Size) %>% 
  arrange(year, Size, Date) %>% 
  mutate(Previous_Result = lag(Result, 1), 
         Two_Results_Prior = lag(Result, 2),
         Three_Results_Prior = lag(Result, 3),
         Four_Results_Prior = lag(Result, 4)) %>% ungroup()
repeat_data <- mutate(repeat_data, 
        Repeat_Test = ifelse(round(Result, digits = 4) == round(Previous_Result, digits=4) & round(Previous_Result, digits = 4) == round(Two_Results_Prior, digits = 4) & round(Two_Results_Prior, digits = 4) == round(Three_Results_Prior, digits = 4) & round(Three_Results_Prior, digits = 4) == round(Four_Results_Prior, digits = 4), "TRUE", "FALSE"))


write_csv(repeat_data, "X:/Programs/Air_Quality_Programs/Air Monitoring Data and Risks/6 Air Data/UFP Processing/Data Validation Tool/repeat_table.csv")

######################################################
##Pull together the data validation tables and the original large data table

##add quarter year variables for the join on leak table
ufp <- mutate(ufp, quarter_year = paste0(quarter(Date), "_", year(Date)))

leak_table <- leak_table %>%
  select(Size, quarter, fvalue_levene, pval_levene, deg_free_levene, Year_1, Year_2) %>%
  gather(analysis_year, year, Year_1:Year_2) %>%
  mutate(quarter_year = paste0(quarter, "_", year))

big_table <- left_join(ufp, leak_table, by = c("Size" = "Size", "quarter_year" = "quarter_year"))

##add variables for the join on repeat table
repeat_table <- repeat_data %>%
  select(Date, Size, year, quarter, quarter_year, Repeat_Test) %>%
  unique()

big_table <- left_join(big_table, repeat_table, by = c("Size" = "Size", "Date" = "Date", "quarter" = "quarter", "year" = "year", "quarter_year" = "quarter_year"))

write.csv(big_table, "X:/Programs/Air_Quality_Programs/Air Monitoring Data and Risks/6 Air Data/UFP Processing/Data File/r_checked_rules.csv", row.names = FALSE)

write.csv(big_table[, c("Date", "Size", "Flags", "Null_Code", "Result")], "X:/Programs/Air_Quality_Programs/Air Monitoring Data and Risks/6 Air Data/UFP Processing/Data File/ufp_data_qualifiers.csv", row.names = FALSE)

```

### PAHs near facilities

- __Download PAH data__:

```{r get facilities}
##Load Packages
library(tidyverse)
library(RODBC)
library(lubridate)
#library(rmarkdown)

##Set working Directory
setwd("X:/Programs/Air_Quality_Programs/Air Focus Areas/EPA Community Scale Monitoring of PAHs Project/Data Analysis/Data Processing") 

###################################################################
##Pull In Data. Data are from an Access Table Named All Results. This query relates the concentration sheets provided by MDH, MPCA field sheets, a Site Information Table and a time summarizing sheet. 
###################################################################
conn = "X:/Programs/Air_Quality_Programs/Air Focus Areas/EPA Community Scale Monitoring of PAHs Project/Data Management/MPCA_MDH_DNRE Data/PAHs_Air_EPA_Grant.accdb"
conn = odbcConnectAccess2007(conn) ##Connect to the ACCESS database
alldata = sqlFetch(conn, "All Results", stringsAsFactors=FALSE) # read a table
qcdata = sqlFetch(conn, "QC Results", stringsAsFactors=FALSE)
siteinfo = sqlFetch(conn, "Site Information", stringsAsFactors=FALSE)
pahinfo = sqlFetch(conn, "PAH Information", stringsAsFactors=FALSE)
odbcClose(conn) # close the connection to the file

alldata <- unique(alldata)
alldata=as.data.frame(alldata, stringsAsFactors=FALSE)

names(alldata) <- str_replace_all(str_trim(names(alldata)), " ", "_")
```


### PAHs in residential neighborhoods and rural areas

- __Download more PAH data__:

```r{get communities}
##Pull in packages
library(tidyverse)
library(RODBC)
library(lubridate)

##Set working Directory
setwd("X:/Programs/Air_Quality_Programs/Air Monitoring Data and Risks/Community Air Monitoring Project/Facility Focused PAH Project/Data Processing and Analysis/Data Processing") 

###################################################################
##Pull In Data. Data are from an Access Table Named All Results. This query relates the concentration sheets provided by MDH, MPCA field sheets, a Site Information Table and a time summarizing sheet. 
###################################################################
conn = "X:/Programs/Air_Quality_Programs/Air Monitoring Data and Risks/Community Air Monitoring Project/Facility Focused PAH Project/Data Management/PAH Data/PAHs_Air_Facility_Fenceline.accdb"
conn = odbcConnectAccess2007(conn) ##Connect to the ACCESS database
alldata = sqlFetch(conn, "All Results", stringsAsFactors=FALSE) # read a table
qcdata = sqlFetch(conn, "QC Results", stringsAsFactors=FALSE)
siteinfo = sqlFetch(conn, "Site Information", stringsAsFactors=FALSE)
pahinfo = sqlFetch(conn, "PAH Information", stringsAsFactors=FALSE)
odbcClose(conn) # close the connection to the file

alldata <- unique(alldata)
alldata=as.data.frame(alldata, stringsAsFactors=FALSE)

names(alldata) <- str_replace_all(str_trim(names(alldata)), " ", "_")

```


### Silica sand monitoring data

- __Download monitoring around silica sand processing facilities and mines__:

```{r silica sand data}
library(tidyverse)
library(RODBC)

db_path <- "X:/Agency_Files/Emerging Issues/Silica Sand/Ambient Air Monitoring Data/Frac Sand Mine and Processing Ambient Air Data.accdb"
table_name <- "Monitor Locational Information"
table_name_2 <- "Measured Concentrations"
table_name_3 <- "Winona Daily PM25 and Met Data"
table_name_4 <- "Facility Information"

si_db <- odbcConnectAccess2007(db_path)
monitors <- sqlFetch(si_db, table_name, rownames = F, stringsAsFactors = F)
measurements <- sqlFetch(si_db, table_name_2, rownames = F, stringsAsFactors = F)
winona <- sqlFetch(si_db, table_name_3, rownames = F, stringsAsFactors = F)
facilities <- sqlFetch(si_db, table_name_4, rownames = F, stringsAsFactors = F)
odbcClose(si_db) 


```


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



