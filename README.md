# SPHEREx Sky Viewer

A local web application for exploring real NASA SPHEREx infrared sky data, comparing observation epochs, and inspecting moving or variable objects in the sky.

This repository contains the project code, backend data-processing utilities, generated sky data, and supporting documentation developed for the NASA Space Apps Challenge Ho Chi Minh City 2026.

## Overview

The project combines:

- a browser-based sky viewer for SPHEREx cutouts and real WISE/NEOWISE data
- a 3D welcome/sky exploration experience
- a lightweight Python backend for serving data and proxying external archive access
- astronomical utilities for Gaia, SIMBAD, and ephemeris data
- project documentation covering mission context, system architecture, and scientific rationale

The app is designed to help users browse real astronomical images, inspect multiple epochs, and identify sources that move or vary over time.

## Project structure

```text
.
├── README.md
├── LICENSE
├── requirements.txt
├── skills-lock.json
├── backend/
│   ├── README.md
│   ├── main.py
│   ├── fits_pipeline.py
│   ├── pre_cache.py
│   └── cache/
├── css/
│   └── style.css
├── data/
│   └── benchmarks.json
├── documentation/
│   ├── README.md
│   ├── 05.NASA Data & Resources.md
│   ├── competitor_and_gap_analysis.md
│   ├── CSA (Canadian Space Agency).md
│   ├── 00-strategy-and-gap-analysis/
│   ├── 01-hackathon-rules/
│   ├── 02-spherex-mission/
│   ├── 03-panstarrs-wiseview/
│   └── 04-system-architecture/
├── Pan-STARRS/
│   ├── Pan-STARRS + WiseView analysis.md
│   ├── Pan-STARRS gaps survey.md
│   └── Pan-STARRS initial implementation.md
├── research/
│   ├── astro-composition.md
│   ├── build_compact_benchmarks.py
│   ├── query_gaia.py
│   ├── sample_cutout.fits
│   ├── test_panstarrs_pipeline.py
│   ├── test_spherex_clean.py
│   └── test_spherex_tap.py
├── viewer/
│   ├── README.md
│   ├── index.html
│   ├── welcome.html
│   ├── serve.py
│   ├── gaia_live.py
│   ├── spherex_live.py
│   ├── wise_live.py
│   ├── star_info.py
│   ├── constellation_bounds.tsv
│   ├── gaia_cache/
│   ├── spherex_cache/
│   ├── sky/
│   └── tools/
└── documentation/
```

## Main application

The user-facing interface is located in `viewer/`.

- `viewer/welcome.html` opens the introductory sky experience
- `viewer/index.html` hosts the main SPHEREx viewer
- `viewer/serve.py` starts the local server and exposes the browser API endpoints
- `viewer/spherex_live.py` loads SPHEREx frames and related metadata
- `viewer/gaia_live.py` loads Gaia DR3 sources in the current field
- `viewer/wise_live.py` loads real WISE/NEOWISE frames when available
- `viewer/star_info.py` resolves object metadata and structure for star cards and object details

The web app is intended to run locally and serves static frontend assets while proxying data requests to the astronomy archives.

## Scientific and data context

The project is centered around NASA's SPHEREx mission and related open astronomical archives.

### Data sources used in the project

- NASA/IPAC IRSA SPHEREx image products
- Gaia DR3 source catalog data
- SIMBAD object metadata and name resolution
- JPL Horizons ephemerides used by the sky and time-based experiences
- WISE / NEOWISE image data for comparison and long-term monitoring workflows

### Core scientific use cases

- inspect real SPHEREx exposures by detector band (`D1` to `D6`)
- compare multiple epochs to identify motion or surprise changes
- inspect stars and targets with proper motion or variability
- view metadata associated with observed fields
- browse a sky guide and object-driven exploration flow

## Backend processing

The Python backend in `backend/` includes a FITS pipeline for scientific cleaning and denoising of SPHEREx cutouts.

Key pieces:

- `backend/fits_pipeline.py` contains the FITS processing logic
- `backend/main.py` exposes a FastAPI endpoint layer for processed observation data
- `backend/pre_cache.py` provides batch pre-caching for known target coordinates

The pipeline is focused on processing SPHEREx Level-2 cutouts and preparing cleaned image data for visualization.

## Project documentation

Detailed documentation is stored in `documentation/`.

Major sections include:

- `documentation/README.md` — project documentation index
- `documentation/00-strategy-and-gap-analysis/` — strategy and competitor analysis
- `documentation/01-hackathon-rules/` — challenge rules and presentation strategy
- `documentation/02-spherex-mission/` — mission and SPHEREx technical background
- `documentation/03-panstarrs-wiseview/` — Pan-STARRS and WiseView analysis
- `documentation/04-system-architecture/` — system design and scientific architecture

Additional technical notes and research artifacts are located in `research/` and `Pan-STARRS/`.

## Requirements

The project depends on Python packages listed in `requirements.txt`.

Required packages include astronomical and scientific libraries such as:

- NumPy
- Astropy
- Astroquery
- Matplotlib
- SciPy
- Requests
- Pillow
- reproject
- FastAPI
- Uvicorn

The repository also includes generated static/cache data used by the viewer to support local offline demonstrations.

## Quick start

### 1. Install dependencies

```bash
python -m pip install -r requirements.txt
```

### 2. Start the app

From the repository root:

```bash
cd viewer
python serve.py
```

This starts a local web server and opens the project in the default browser by default.

The app serves:

- the welcome sky at `/`
- the main viewer at `/index.html`
- API routes under `/api/...`

## Useful project scripts

The repository contains helper scripts to regenerate astronomy data and validation checks.

Examples:

```bash
python tools/build_targets.py
python tools/build_hr_data.py
python tools/build_sky_data.py
python tools/build_ephemeris.py
node tools/test_astro.mjs
node tools/test_constellations.mjs
node tools/test_hz.mjs
```

These scripts are used to build or validate the sky data, target positions, and astronomical calculations used by the viewer.

## License

This project is licensed under the MIT License.

See `LICENSE` for the full text.

## Notes

- This repository was developed around a NASA Space Apps Challenge workflow and includes challenge-oriented documentation and analysis artifacts.
- The repository contains both real-data integration and local demo/cache assets.
- Certain data-heavy features rely on archive access and generated datasets, so first loads may take longer depending on network and cache state.

## Summary

SPHEREx Sky Viewer is a local astronomy exploration and visualization project that brings together SPHEREx, Gaia, SIMBAD, and related sky data into a browser-based interactive experience. Its primary goal is to help users explore real sky imagery, compare observations across time, and visually identify interesting celestial changes and motion in a scientifically grounded workflow.
