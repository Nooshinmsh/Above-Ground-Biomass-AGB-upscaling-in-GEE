# Biomass Upscaling using Landsat 9 and GEDI in Google Earth Engine

This repository contains a Google Earth Engine (GEE) script to support biomass upscaling by integrating **Landsat 9 surface reflectance** data and **GEDI Level 4A** products. The code performs preprocessing, spectral index calculation, compositing, and data export to facilitate large-scale vegetation analysis, including NDVI and other vegetation metrics.

---

# Study Area
The region of interest is defined by a custom shapefile:
- `NK_boundar` uploaded as an Earth Engine asset under:  

#Datasets Used

### Landsat 9 Surface Reflectance (Tier 1, Level 2)
- Collection ID: `LANDSAT/LC09/C02/T1_L2`
- Time range: **January 1, 2021 – December 30, 2021**
- Cloud filtering: **< 20% cloud cover**

### GEDI Level 4A Biomass Data
- Collection: `LARSE/GEDI/GEDI04_A_002`
- One or more specific granules are filtered by region and exported.

---
#Processing Workflow

1. Load shapefile** and filter Landsat 9 images based on:
   - Date range
   - Region of interest
   - Cloud cover threshold

2. Scale Landsat 9 bands** using USGS recommended scaling factors:
   - Optical bands scaled to reflectance
   - Thermal bands scaled to temperature in Kelvin

3. Calculate spectral indices**:
   - NDVI (Normalized Difference Vegetation Index)
   - EVI (Enhanced Vegetation Index)
   - PVI (Perpendicular Vegetation Index)
   - NDBI (Normalized Difference Built-up Index)
   - NBR (Normalized Burn Ratio)
   - NDWI (Normalized Difference Water Index)

4. Create median composite** from the scaled and indexed image collection.

5. Export outputs**:
   - RGB composite image (SR_B4, SR_B3, SR_B2)
   - Spectral indices as separate bands
   - NDVI visualization

6. GEDI Clipping and Export**:
   - Clip selected GEDI Level 4A datasets to ROI
   - Export each as separate Earth Engine assets
   - Merge and export all as a CSV table to Google Drive

---

# Map Layers

- Landsat 9 RGB Composite (`SR_B4`, `SR_B3`, `SR_B2`)
- NDVI Layer (colorized from blue to green)
- Clipped GEDI Level 4A Datasets

---

#Exported Files

| Export Description         | Format  | Location            |
|---------------------------|---------|---------------------|
| Landsat9 Median Composite | GeoTIFF | Google Drive: `GEE_Exports/Landsat9_Median.tif` |
| Landsat9 Spectral Indices | GeoTIFF | Google Drive: `GEE_Exports/Landsat9_Indices.tif` |
| GEDI Clipped Datasets     | EE Asset | `projects/ee-nmashhad/assets/Clipped_GEDI_Dataset_X` |
| GEDI Merged Table         | CSV     | Google Drive: `GEE_Exports/GEDI_Level4A_Merged.csv` |

---



