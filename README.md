# Lagos Urban Heat Islands 

Mapping surface heat patterns across Lagos using satellite thermal imagery, and testing how much of that pattern is explained by vegetation loss.

## Background

As anyone who has been in Lagos these past couple of months can tell you, Lagos is getting hotter, and not evenly. Some areas like Mushin, Ajegunle, Oshodi feel noticeably hotter than their coastal counterparts like Lekki and other more rural regions of the state. The urban heat island effect caused by impervious surfaces, lost wetlands and tree cover, building density trapping heat is a well-documented phenomenon. This project builds a map of where it's worst, using freely available satellite data rather than ground sensors.

## Data sources

| Dataset | Purpose | Source |
|---|---|---|
| Landsat 8/9 Collection 2 Level-2 (Band 10 ST, Bands 4/5) | Surface temperature + NDVI | [USGS EarthExplorer](https://earthexplorer.usgs.gov) / [Google Earth Engine](https://earthengine.google.com)|
| Lagos ward boundaries | Zonal statistics units | [GADM](https://gadm.org), Lagos State Open Data, or [GRID3](https://data.grid3.org) LGA boundaries|
| WorldPop Nigeria population raster | Context  | [worldpop.org](https://worldpop.org) |
