# Data Notes

## Landsat Surface Temperature Band
- Source: USGS EarthExplorer (https://earthexplorer.usgs.gov/)
- Acquired: 28th January 2026 (Path 191, Row 055) and 5th February 2026 (Path 191, Row 056)
- Downloaded: 12th September, 2026
- Composite of 2 scenes — no single scene covers Lagos state fully, so scenes were mosaicked
- Band: ST_B10 (Surface Temperature) only, Collection 2 Level-2
- Cloud cover: 16%
- Dry season window (Oct 2025–Apr 2026), consistent with reduced cloud cover for the region
- Mosaic seam between the two path/rows may introduce edge artifacts — check for discontinuities along the seam line before running zonal stats

## Nigeria Administrative Boundaries (HDX COD-AB Nigeria Admin 0-3)
- Source: HCX (https://data.humdata.org/dataset/cod-ab-nga)
- Downloaded: 12th September, 2026
- Admin 1: 37 States
- Admin 2: 774 Local Government Areas
- Admin 3: 714 Wards — partial national coverage
- Source agencies: Office for the Surveyor General of the Federation (OSGOF), eHealth Africa, UN Cartographic Section
- Dataset reviewed for accuracy and completeness: 30th October 2025
- Valid for use by the humanitarian community since: 17th April 2019
- Lagos AOI is a subset clipped from this national file — ward-level (Admin 3) coverage within Lagos not yet verified against the partial national coverage; confirm ward count for Lagos before using as zonal stat units

## Nigeria Gridded Population Estimate
- Source: Grid3 / Worldpop (https://wopr.worldpop.org/download/611)
- Downloaded: 12th September, 2026
- Published: 29th August 2025 (v3.0)
- Resolution: ~100m (3 arc-second) gridded population raster
- CRS: EPSG:4326 — will need reprojection to EPSG:32632 to match project CRS
- Produced by WorldPop (University of Southampton) under GRID3 Phase 2, scaled to UN WPP July 2025 national population projections
- License: CC BY 4.0
- Modelled estimates, not official government statistics — use for context/weighting, not as ground truth
