---
layout: page
title: Census
---

---

## American Community Survey (ACS) {#acs}
The ACS provides updated demographic statistics used for population estimates and Environmental Justice indicators.  


Minnesota ACS results can be loaded into R using the `tidycensus` package. 
Use the following code to download recent population and income estimates.
```r
# This script downloads American Community Survey (ACS) results for MN
# Load packages
library(tidycensus)

# ACS data requires a Census key
# Visit: http://api.census.gov/data/key_signup.html
census_api_key("Your_API_key")

# View all ACS variables
acs_variables <- load_variables(2015, "acs5", cache = TRUE)

# Download 5-yr population estimates for 2015
pops_2015 <- get_acs(geography = "tract", 
                     state     = "MN", 
                     variables = "B01003_001", 
                     survey    = "acs5", 
                     year      = 2015)

# Download decennial population estimates for 2010
pops_2010 <- get_decennial(geography = "tract", 
                           state     = "MN", 
                           variables = "P0080001", 
                           year      = 2010)

# Download household median income for 2015
med_inc_2015 <- get_acs(geography = "tract", 
                        state     = "MN", 
                        variables = "B19013_001", 
                        survey    = "acs5", 
                        year      = 2015)
```

