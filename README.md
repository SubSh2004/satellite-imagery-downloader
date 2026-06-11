# 🛰️ Satellite Imagery Downloader — India

A Python-based pipeline that downloads satellite imagery for any Indian state using **Google Earth Engine (GEE)**, automatically handles tiling, band chunking, merging, and clipping — and produces a single analysis-ready **GeoTIFF**.

No manual downloading. No unzipping. No merging headaches.

---

## 📌 Why This Exists

If you've ever tried downloading satellite data from **Bhoonidhi** or **Copernicus Open Access Hub**, you know the pain:

- Your area is too large — it gets split into dozens of rectangular tiles
- Each tile is a massive zip file — download, wait, download, wait...
- Then unzip every single one
- Then merge the required bands for each tile separately
- Then mosaic all the tiles into one image
- Then clip it to your actual state or area boundary

And if you made one mistake somewhere? Start over.

This tool automates the entire workflow from a single Jupyter notebook.

---

## 🛰️ Supported Satellites

| Satellite | Dataset | Resolution | Bands |
|-----------|---------|------------|-------|
| Sentinel-2 | COPERNICUS/S2_HARMONIZED | 10m / 20m / 60m | B1–B12 |
| Landsat-8 | LANDSAT/LC08/C02/T1_L2 | 30m | SR_B1–SR_B7 |
| Landsat-9 | LANDSAT/LC09/C02/T1_L2 | 30m | SR_B1–SR_B7 |

---

## ✨ Features

- **State-wise AOI** — select any Indian state by name
- **Custom date range** — filter imagery by start and end date
- **Cloud cover filtering** — set a maximum cloud percentage threshold
- **Dynamic band selection** — choose any combination of bands
- **Automatic resolution detection** — uses the finest resolution of your selected bands
- **Smart tiling** — calculates safe tile sizes based on GEE's 48MB download limit
- **Band chunking** — splits bands into chunks of 3 to stay within pixel size limits
- **GDAL merging & mosaicking** — merges chunks and tiles into a single raster
- **State boundary clipping** — clips the final mosaic to the exact state boundary
- **Auto cleanup** — deletes all intermediate files, keeps only the final GeoTIFF

---

## 📁 Output

The final output is a single compressed GeoTIFF:

```
StateName_clipped.tif
```

This file contains all selected bands merged into one raster, clipped exactly to the chosen state's boundary, ready for analysis in QGIS, ArcGIS, or any GIS software.

---

## ⚙️ Setup & Installation

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

### 2. Install Required Libraries

```bash
pip install earthengine-api geemap geopandas gdal
```

### 3. Google Earth Engine Setup

This project uses the GEE Python API. Follow these steps before running the notebook:

**Step 1 — Register a GEE project:**
Go to [https://code.earthengine.google.com](https://code.earthengine.google.com), sign in with your Google account, and create a project.

**Step 2 — Enable the Earth Engine API:**
Go to [Google Cloud Console](https://console.cloud.google.com/), select your project, and enable the **Earth Engine API**.

**Step 3 — Authenticate:**
Run this once in your terminal:
```bash
earthengine authenticate
```
Follow the link, sign in, and paste the token back.

**Step 4 — Update the project ID in the notebook:**
In the first code cell, replace:
```python
ee.Initialize(project='sentinel2-project-498918')
```
with your own project ID:
```python
ee.Initialize(project='YOUR-PROJECT-ID-HERE')
```

### 4. Update the Output Path

In the notebook, find the output path cell and update it to a folder on your machine:
```python
download_path = rf"YOUR\PATH\HERE\{folder_name}"
```

---

## 🗺️ Shapefile

The India states shapefile (`india_state.shp`) is included in this repository. No additional download needed. Just make sure the path in the **AOI Manager** section points to where you cloned the repo on your machine.

---

## 🚀 How to Use

1. Open `AOI_manager.ipynb` in Jupyter Notebook or VS Code
2. Run cells top to bottom
3. When prompted, enter:
   - State name (e.g. `Goa`, `Chandigarh`, `Rajasthan`)
   - Satellite number
   - Band numbers (comma separated)
   - Start and end date
   - Maximum cloud cover percentage
4. The pipeline runs automatically and saves the final GeoTIFF to your output folder

---

## 🖥️ Visualizing in QGIS

Open the output `.tif` in QGIS and set the following for a clean natural-colour display with Sentinel-2:

- **Red band:** B4
- **Green band:** B3
- **Blue band:** B2
- **Min:** 0 | **Max:** 3000

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Python | Core language |
| Google Earth Engine | Satellite data access & processing |
| geemap | GEE Python interface |
| GeoPandas | Shapefile handling & AOI extraction |
| GDAL | Raster merging, mosaicking & clipping |
| QGIS | Visualization |

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).