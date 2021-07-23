---
layout: page
title: Greenhouse gas emissions
---

---
* Add table of contents
{:toc}

Greenhouse gas emissions are estimated in a variety of spreadsheets housed on the X-drive. Methods vary depending on data, and include facility process level emissions and fuel consumption, top-down fuel consumption, activity data, demographics, and modeled data.

Staff contact: Anne Claflin, Angela Hawkins

# Statewide summary data
https://www.pca.state.mn.us/air/greenhouse-gas-emissions-data 

# Facility GHG emissions - CEDR (Rapids)
CEDR may be accessed through the ISO launch pad or by connecting to the server through Tableau, R, etc. 

## Database via Tableau
- Server: deltaw.pca.state.mn.us
- Schema: RAPIDS

All tables, column names, data types, comments, keys, and relationships are documented here:
http://rainier.pca.state.mn.us/documentation/DataDictionary/DELTAW/RAPIDS/tables.html

- Double check that it is `W` and NOT `T`

## Database via R

```r
library(RODBC) # package needed to access Oracle DeltaW database

# Open DELTA connection and set to `deltaw`
# ask someone for the username and password
deltaw <- odbcConnect("DeltaW", uid=" ", pwd=" ") 

# list tables
tbls_all <- RODBC::sqlTables(deltaw)
tbls_rapids <- RODBC::sqlTables(deltaw, schema = "SUPERAPIDS")

# Run a custom query
## This query loads the reference table for the pollutant - CAS number table from the SUPERAPIDS air emissions inventory database.
pollutants <- RODBC::sqlQuery(deltaw, "Select * from SUPERAPIDS.REF_MATERIAL_CODES", max = 2000)
```

## CEDR application
The application can look up individual facilities, but it is often more useful to export tables.

### To export data from CEDR:

- File > Export > Rapids 3 > Select Inventory tables 
- Open with Excel, rename and save as .xlsx
- Copy sheet to clean the data and save raw version

These inventory tables are necessary:

* Table Description // File Extension
* Inv Inventory Process Activities	// ACP
* Inv Emission Units // EMU
* Inv Processes	// PRO
* Inv Sources	// SRC
* Inv Process Emissions	// PEM

### Notes on CEDR tables
In the table *Inventory Process Activities*, rename the data field *MATERIAL CODE* as *ACTIVITY MATERIAL CODE.* This helps distinguish it as the fuel consumed or other activity, as opposed to the other *MATERIAL CODE* in the *Process Emissions* table. Rename that one *EMISSIONS MATERIAL CODE*

When working with activity data, be very careful to avoid double counting. This can occur when adding up sources if the throughput is duplicated for each pollutant or if the throughput is reported in multiple units (volume, heat, equipment, work). 

### Post-processing
Lots, including standardizing fuels, standardizing all throughput units to volumes, and separating blended biofuels into fossil and bio components.

**Blended fuels** 
CEDR cannot split biofuel and fossil fuel portions of blended fuels (biodiesel, gasoline, etc). This must be done outside of CEDR. Be aware of differences in GHGs when accessing CEDR.

1.	Separate Diesel and distillate throughput
2.	Relabel as DIESEL FUEL BLEND
3.	Label any exempt sources as DIESEL FUEL EXEMPT
4.	Use biodiesel mandate to set biofuel proportion
5.	Duplicate data and calculate BIODIESEL PORTION and DIESEL FOSSIL PORTION
6.	Change source to Calculated from CEDR
7.	Copy biodiesel and fossil data back into spreadsheet 
8.	Exclude the fuel blends from analysis

# Top-down 
The data we have from facilities is only a portion of the greenhouse gas emissions in the state. In some cases it is mostly complete (electricity generation) and in others we know there are gaps. We use total fuel consumption from federal and state data sources, subtract what is known from facilities, and assign the unknown consumption to sectors.

# Modeled data
On-road transportation emissions are modeled in MOVES.

Landfill emissions are modeled in LandGEM.

# Methods and data sources
A table of sources for the inventory methodology, emission factors, and activity data is available on the X drive here: <xdrive\Programs\Air_Quality_Programs\Climate Change\Inventory Files\Active Files\Methods Tables.xlsx>

Improvements to the technical support document and data accessibility are in progress. 
