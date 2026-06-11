# ⚙️ Setup Guide

Complete this guide before running `sate_downloader.ipynb`.

---

## 1. Python Environment

Make sure you have Python 3.8 or higher installed. It is recommended to use a virtual environment or conda environment to avoid dependency conflicts.

**Using conda (recommended):**
```bash
conda create -n sat_downloader python=3.10
conda activate sat_downloader
```

---

## 2. Install Required Libraries

```bash
pip install earthengine-api geemap geopandas gdal
```

> **GDAL installation note:**  
> GDAL can be tricky to install via pip on Windows. If you face issues, install it via conda instead:
> ```bash
> conda install -c conda-forge gdal
> ```

---

## 3. Google Earth Engine Setup

This project uses the **Google Earth Engine (GEE) Python API** to access satellite imagery. Follow the steps below carefully.

### Step 1 — Create a Google Account
If you don't have one, create a Google account at [https://accounts.google.com](https://accounts.google.com).

### Step 2 — Register for Google Earth Engine
Go to [https://code.earthengine.google.com](https://code.earthengine.google.com) and sign in.  
If this is your first time, you will be asked to register. Choose **"Use with a Cloud Project"**.

### Step 3 — Create a Google Cloud Project
Go to [https://console.cloud.google.com](https://console.cloud.google.com) and:
1. Click **"New Project"**
2. Give it a name (e.g. `satellite-downloader`)
3. Note the **Project ID** — you will need this in the notebook

### Step 4 — Enable the Earth Engine API
In Google Cloud Console:
1. Go to **APIs & Services → Library**
2. Search for **"Earth Engine API"**
3. Click **Enable**

### Step 5 — Authenticate on Your Machine
Run this once in your terminal (with your environment activated):
```bash
earthengine authenticate
```
A browser window will open. Sign in with your Google account and paste the token back into the terminal.

### Step 6 — Add Your Project ID to the Notebook
Open `sate_downloader.ipynb` and in the very first cell, update:
```python
GEE_PROJECT_ID = "YOUR-PROJECT-ID-HERE"
```
Replace with the Project ID you noted in Step 3. For example:
```python
GEE_PROJECT_ID = "satellite-downloader-123456"
```

---

## 4. Set Your Output Folder

In the first cell of the notebook, also update `BASE_OUTPUT_DIR` to a folder on your machine where downloaded imagery will be saved:

**Windows:**
```python
BASE_OUTPUT_DIR = r"C:\Users\YourName\Downloads\satellite_data"
```

**Mac / Linux:**
```python
BASE_OUTPUT_DIR = "/home/yourname/satellite_data"
```

The folder will be created automatically if it doesn't exist.

---

## 5. Shapefile

The India states shapefile (`india_state.shp` and its companion files) is **included in this repository**. You do not need to download anything separately.

Just make sure the `SHAPEFILE_PATH` in the first notebook cell points to the correct location. If you cloned the repo and the shapefile is in the same folder as the notebook, update it like this:

**Windows:**
```python
SHAPEFILE_PATH = r"C:\path\to\cloned\repo\india_state.shp"
```

**Mac / Linux:**
```python
SHAPEFILE_PATH = "/path/to/cloned/repo/india_state.shp"
```

---

## 6. QGIS (Optional — for Visualization)

To visualize the output GeoTIFF, download QGIS from [https://qgis.org](https://qgis.org).

For a clean natural-colour display with Sentinel-2, set the band rendering range in QGIS to:
- **Min:** 0
- **Max:** 3000

---

## Summary Checklist

- [ ] Python environment created and activated
- [ ] All libraries installed (`earthengine-api`, `geemap`, `geopandas`, `gdal`)
- [ ] GEE account registered
- [ ] Google Cloud project created and Earth Engine API enabled
- [ ] `earthengine authenticate` run in terminal
- [ ] `GEE_PROJECT_ID` updated in notebook cell 0
- [ ] `BASE_OUTPUT_DIR` updated in notebook cell 0
- [ ] `SHAPEFILE_PATH` updated in notebook cell 0

Once all boxes are checked, open `sate_downloader.ipynb` and run cells top to bottom.
