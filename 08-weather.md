---
layout: page
title: Weather
---

## Weather observations {#wx-obs}
Historical meteorological observations are available from multiple sources. 


### Raw data

1. An internal Tableau workbook provides raw results for Minnesota meteorological stations: [tableau.pca.state.mn.us/#/workbooks/5714](tableau.pca.state.mn.us/#/workbooks/5714)


### Quality assured data

1. The AQI forecast uses a web API provided by [_DarkSky_](https://darksky.net/dev) for current forecast information and quality assured historical observations.


## HYSPLIT wind trajectories {#hysplit}

Wind trajectories are useful for determining the primary sources contributing to elevated air monitoring results. Trajectory results for the air monitoring network are available in [WAIR](#wair) for the years 2007 to 2017. The R package [SplitR](https://github.com/rich-iannone/SplitR) was used to automate HYSPLIT modeling for each air monitoring location.
