# Data Preparation Note — Week 3

**Project:** Lagos State AOI — Land Surface Temperature & Population Exposure Analysis
**Date:** 20 September 2026

---

## 1. CRS and Preparation

**Source CRS (as received):**

| Layer | Source CRS |
|---|---|
| Landsat ST_B10 (2 scenes) | Native UTM (WGS84 datum) |
| HDX Admin Boundaries (COD-AB Nigeria) | EPSG:4326 |
| WorldPop Gridded Population (v3.0) | EPSG:4326 |

**Working CRS chosen:** `EPSG:32632` — WGS 84 / UTM Zone 32N

**Why:** Lagos State sits within UTM Zone 32N. The analysis requires area- and distance-based measurements (population-weighted heat exposure, per-ward zonal statistics), which need a projected CRS in metres rather than geographic degrees. A geographic CRS (EPSG:4326) would distort these calculations.

**What was reprojected and clipped:**

- **Study Area:** Lagos State boundary, extracted from the HDX Nigeria Admin 1 layer.
- **Landsat ST_B10:** Two scenes — Path 191/Row 055 (acquired 28 Jan 2026) and Path 191/Row 056 (acquired 5 Feb 2026) — mosaicked, reprojected to EPSG:32632, then clipped to the Lagos AOI.
- **HDX Admin Boundaries:** Admin 1 (state boundary) and Admin 3 (wards) subsets extracted from the national file, reprojected to EPSG:32632, clipped to Lagos.
- **WorldPop Gridded Population:** Reprojected from EPSG:4326 to EPSG:32632, clipped to the Lagos AOI.

**File format:** All processed layers saved as GeoPackage (`.gpkg`) — a single SQLite container that keeps geometry, attributes, and CRS metadata together in one file, avoiding the multi-file fragility of Shapefiles.

---

## 2. Quality Checks

| # | Check | Result |
|---|---|---|
| 1 | **CRS verification** — confirmed EPSG:32632 reported on all three processed layers via QGIS layer properties | *[state: pass / issue found]* |
| 2 | **Area check** — computed Lagos State area from reprojected boundary vs. published figure (~3,577 km², NBS/Lagos State Govt) | *[state your computed value and the delta]* |
| 3 | **Ward coverage check** — HDX Admin 3 has partial national coverage; verified Lagos ward count in the clipped subset against the expected ~377 wards across Lagos's 20 LGAs | *[state count found; note any missing LGAs]* |
| 4 | **Population raster alignment** — confirmed WorldPop raster fully overlaps the Lagos AOI post-reprojection with no NoData gaps at the clip edge; confirmed nearest-neighbour resampling was used (appropriate for count data) | *[state: pass / issue found]* |

---

## 3. Problems Found

- **Partial ward coverage:** HDX Admin 3 (wards) is only partially complete nationally. If any Lagos wards are missing from the clipped subset, zonal statistics will need to fall back to Admin 2 (LGA) units for those areas. *[state: resolved / flagged, pending]*
- **Cloud cover:** Landsat scenes carry 16% cloud cover. Cloud-masked pixels within the Lagos AOI may affect ST_B10 values at their edges. *[state whether the QA band was checked and any pixels excluded]*

---

## 4. Output Location

Analysis-ready GeoPackage files:

```
data/processed/lagos_lst.gpkg          # Landsat ST_B10, mosaicked, reprojected, clipped
data/processed/lagos_admin.gpkg        # Admin 1 + Admin 3 boundaries, reprojected, clipped
data/processed/lagos_population.gpkg   # WorldPop gridded population, reprojected, clipped
```
