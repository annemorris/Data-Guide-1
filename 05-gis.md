---
layout: page
title: GIS
---  

## Where to find MPCA (and other agencies') data?    
Currently the R:\ drive is an excellent collection of spatial data.  In the age of sharing and public data the new [Geospatial Commons](https://gisdata.mn.gov/)  rose to take R-drive's place.  The Geospatial Commons has a home on the L:\ drive so datasets can participate in both internal and external data gatherings.    

You may continue to find useful things in the R-drive but it will eventually be decommissioned.

## Tempo Spatial Data
Many Tempo data elements are available on both internal and external servers.  The R:\MPCA folder is the best collection of internal Tempo GIS data.  A few examples of commonly used layers are below and many others are available.

**env mpca agency interests.gdb**: This layer represents points with Agency activities across all programs.  It is a good starting point for "what is the MPCA doing in this area?"

**env surface water moni tempo.gdb**: This is a base layer of all permit-related surface water monitoring in Tempo.  This is not the same as EQUIS monitoring and is intended for "how many facilities are monitoring in the area?"  This is a large layer and is best used with filters on the program and SI type fields.

**util wastewater facilities.gdb**: These are wastewater treatment (TREA) items with attributes from the most recent permit. Since this layer represents facilities it does not contain discharge monitoring locations.

If you cannot find spatial data of interest on the R-drive check the spatial views in the wh tempo schema.  Submit a MNIT ticket to convert and wh tempo view into a spatial data layer.

ESRI products can connect directly to wh tempo but the filtering and credentials are better handled in other applications. 

## Spatial data services
There are a number of [GIS data services](https://pca-gis02.pca.state.mn.us/arcgis/rest/services) hosted by the MPCA.  These can be consumed by Tableau, ESRI, and other products.  The "base" directory contains custom basemaps intended for use in Tableau.  

The WIMN directory shows sites listed in the What's in My Neighborhood application.

Custom base maps allow more flexible use of spatial data in Tableau.  Most are loaded through the Add WMS Service option.

## MPCA ArcGIS Online Map gallery
ArcGIS online is a portal for interactive mapping applications.  These applications consume spatial data services and support a [variety of presentation styles](http://mpca.maps.arcgis.com/home/index.html).  Consider GIS online maps as an alternative to Tableau dashboards.  Each serves a different audience and both are useful in the right context.
Submit a MNIT ticket to become an author at the MPCA GIS Online page.

## Land use maps {#landuse}
Land use shapefiles are maintained by MPCA GIS technical staff and stored on the agency R-drive at `R:\landuse_landcover`.


## United States Census boundaries {#census}

Copies if the USCB Census shapefiles are stored on the agency R-drive at `R:\Demographics .  This includes the decennial census boundaries but not the 5-year average ACS data.  

Census boundaries can be loaded into R using the `tigris` package to map air data to Census tracts and block groups. Use the following code to map MN boundaries.

```r
# This script downloads shapefiles of Minnesota Census boundaries  
# Load packages
library(tigris)

# Load boundaries
county_bnds <- counties(state = "MN", cb = T)

tract_bnds  <- tracts(state = "MN", cb = T)

bg_bnds     <- block_groups(state = "MN", cb = T)

# Plot 
plot(county_bnds)
```



