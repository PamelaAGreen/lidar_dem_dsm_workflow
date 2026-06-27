# LiDAR DEM / DSM Processing Workflow

A Python-based workflow for processing large drone LiDAR point clouds into DEM, DSM, and nDSM raster products using open-source tools.

## Why I built this

I originally developed this prototype while working in consulting, where drone LiDAR processing using proprietary software was often time-consuming, highly manual, and more expensive than it needed to be. The goal was to explore whether a more automated, reproducible workflow could reduce both total processing time and the amount of user interaction required, helping teams move data through analysis faster while also avoiding unnecessary project budget overhead.

This repository is a **prototype** built to test large drone LiDAR datasets and evaluate a more efficient processing approach. It was always intended as a starting point for further development rather than a finished production package.

## What it does

This notebook processes raw airborne or drone LiDAR point clouds (`.las` / `.laz`) into:

- **DEM** (Digital Elevation Model)
- **DSM** (Digital Surface Model)
- **nDSM** (normalized DSM / above-ground height surface)

The workflow includes:

- LiDAR metadata inspection and CRS extraction
- Tiling and buffered tiling for large datasets
- Local outlier filtering
- Ground / non-ground classification using Cloth Simulation Filtering (CSF)
- Per-tile DEM and DSM generation using TIN-based interpolation
- Mosaicking of tile rasters into final outputs
- DEM void identification, fill mask creation, and first-pass void filling
- DEM / DSM grid alignment before nDSM generation
- Basic tile-level QA summaries

## Current status

This is an **early prototype / proof of concept** designed to test performance and workflow structure on very large drone LiDAR datasets. It is useful as a transparent reference workflow, but it should still be considered under active development.

A few parts were intentionally kept simple in this version, especially:

- DEM void filling
- QA / validation outputs
- user configuration and packaging
- more advanced urban / vegetation handling

## How to run it

This project is currently organized as a Jupyter Notebook workflow.

1. Clone the repository
2. Create and activate a virtual environment
3. Install the required Python packages
4. Place your input `.las` or `.laz` file in the expected data directory
5. Update the configuration cell as needed
6. Run the notebook from top to bottom

A future version may split the workflow into reusable modules or a command-line pipeline.

## Inputs and outputs

**Input**
- Raw LiDAR point cloud in `.las` or `.laz` format

**Main outputs**
- `dem_raw.tif`
- `dem_filled.tif`
- `dem_fill_mask.tif`
- `dsm_final.tif`
- `ndsm_final.tif`

Additional intermediate products and tile-level summaries are also created during processing.

## What I learned

- Large drone LiDAR workflows benefit substantially from **tiling, buffering, and automated intermediate handling**.
- Open-source Python tools can reproduce much of the core DEM / DSM workflow typically done in proprietary desktop software.
- Automating preprocessing and raster generation reduces repeated manual effort and makes the workflow easier to review, test, and improve.
- Even in a prototype, explicit handling of CRS, grid alignment, and void filling matters if the outputs are going to be trusted downstream.
- Tile-level summaries are useful for catching classification issues early, especially when testing different CSF settings or preprocessing thresholds.

## Stack

- Python
- Jupyter Notebook
- laspy
- whitebox_workflows
- CSF-3DFin
- rioxarray
- rasterio
- xarray
- numpy
- scipy
- geopandas
- shapely

## Notes

This repository is intended as an open, inspectable prototype for LiDAR processing experimentation and workflow development. It is best suited for users who are comfortable working in Python and who want a transparent alternative to more manual LiDAR processing workflows.

## License

This prototype is licensed under the MIT License so that others can freely use, adapt, and integrate it into their own workflows. As a courtesy, please avoid reselling the repository as-is without meaningful changes, and always retain clear attribution to the original author in derivative work. Contributions and improvements are welcome.