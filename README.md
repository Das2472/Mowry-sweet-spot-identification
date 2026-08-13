# ML-Based Sweet-Spot Identification for the Mowry Formation, Powder River Basin

This repository accompanies the manuscript:

**Das, H. S., Obasi, E. C., & Saraji, S.** *Data-driven Sweet Spot Identification in the Mowry Formation: Integrating Machine Learning and Geostatistical Modeling*

It provides the code, calibration data, calculated outputs, and spatial-analysis inputs supporting a machine-learning and geostatistical workflow for identifying geological and integrated (geological + engineering) sweet spots in the Mowry Formation, Powder River Basin, Wyoming.

## Overview

1. **Machine-learning prediction** — Random Forest models predict TOC, Tmax, S1mod, S2, and FI; PI is derived from S1mod and S2.
2. **Sweet-spot classification** — three complementary schemes:
   - a rule-based deterministic classifier (grades A, B, C, None),
   - unsupervised K-means clustering (petrophysical populations),
   - a continuous Sweet Spot Index (SSI) using Entropy Weight Method weights.
3. **Geostatistical mapping** — depth-averaged, well-level SSI and FI values are interpolated across the basin using kriging, with Inverse Distance Weighting (IDW) as a supplementary comparison.

## Repository contents

| Folder / file | Description |
|---|---|
| `code/ml_models/` | Random Forest modeling scripts for TOC, Tmax, S1mod, S2, and FI |
| `code/kmeans/` | K-means clustering scripts for workflows with FI and without FI |
| `code/geostatistics/` | Kriging and IDW interpolation scripts |
| `calibration_data/` | Calibration datasets containing model inputs and target variables used for model development and evaluation |
| `data/Kriging_GN.xlsx` | Depth-averaged per-well SSI and FI values with coordinates used for kriging and IDW |
| `data/Overlaid_wells.xlsx` | Producing-well and active-permit locations used as overlays in the basin-scale maps |
| `data/prb_boundary/` | Powder River Basin boundary shapefile and associated files used to define the interpolation extent and spatial mask |
| `outputs/` | Calculated model outputs and classification results for all 318 wells |
| `requirements.txt` | Python package dependencies |
| `LICENSE` | Terms of use |

## Output files

- `Outputs_of_all_wells.xlsx` — predicted TOC, Tmax, S1mod, S2, PI, and FI values; observed/calculated values where available; normalized variables; SSI values; rule-based grades; well-level mean values; and depth-analysis results for all 318 wells.

- `KMeans_with_FI_318_wells_interpreted.xlsx` — K-means clustering results and interpreted populations for the integrated workflow including FI.

- `KMeans_without_FI_318_wells_final_interpreted.xlsx` — K-means clustering results and interpreted populations for the geological workflow without FI.

## Calibration data

The `calibration_data/` folder contains the datasets used for development and evaluation of the individual Random Forest models:

- `TOC ML modeling data.xlsx`
- `Tmax modeling data.xlsx`
- `S1 modeling data.xlsx`
- `S2 modeling data.xlsx`
- `The last final FI for modeling.xlsx`

These files contain the corresponding model inputs and calibration targets used in the modeling workflow.

## Spatial-analysis data

The `data/Kriging_GN.xlsx` file contains depth-averaged well-level SSI and FI values together with spatial coordinates used as control points for basin-scale kriging and IDW interpolation.

The `data/Overlaid_wells.xlsx` file contains the producing-well and active-permit locations displayed on the spatial maps.

The `data/prb_boundary/` folder contains the Powder River Basin boundary shapefile and its associated files used to define the interpolation domain and spatial mask.

## Reproducibility notes

- The machine-learning modeling scripts are provided together with the corresponding calibration datasets in `calibration_data/`.
- K-means clustering uses z-score standardization, k-means++ initialization, `n_init = 50`, and `random_state = 42`.
- The kriging scripts use the depth-averaged well-level data in `data/Kriging_GN.xlsx`. Variogram models, trend treatment, and anisotropy parameters are specified within the corresponding scripts.
- The IDW scripts use the same well-level spatial dataset and perform interpolation using the 10 nearest wells with an inverse-distance power of 2.0. Interpolation is performed in the original variable units, after which the interpolated surfaces are normalized to 0–1 for visualization.
- Producing-well and active-permit overlays are obtained from `data/Overlaid_wells.xlsx`.
- The Powder River Basin boundary supplied in `data/prb_boundary/` is used to define the interpolation extent and spatial mask.
- The step in which the trained machine-learning models are applied to the complete 318-well log dataset is not reproduced in this repository because the full multi-well log dataset is not publicly released. The resulting calculated predictions and derived outputs are provided in `outputs/`.

## Data availability

The calibration datasets required for machine-learning model development and evaluation are provided in `calibration_data/`.

The depth-averaged SSI/FI values and well coordinates required for spatial interpolation are provided in `data/Kriging_GN.xlsx`. Producing-well and active-permit locations used in the spatial maps are provided in `data/Overlaid_wells.xlsx`, and the Powder River Basin boundary files used to define the interpolation domain and spatial mask are provided in `data/prb_boundary/`.

The full multi-well log dataset used to generate the basin-wide machine-learning predictions is not publicly released. The resulting calculated predictions, SSI values, and classification outputs for the 318 wells are provided in `outputs/`.

## Requirements

See `requirements.txt`.

Core dependencies:

- Python 3.x
- pandas
- numpy
- scikit-learn
- scipy
- matplotlib
- geopandas
- shapely
- pyproj
- pykrige
- openpyxl

## Citation

If you use or refer to the materials in this repository, please cite the associated publication.

Citation information will be updated following publication of the manuscript.

## Contact

Corresponding author: **Soheil Saraji**, University of Wyoming — ssaraji@uwyo.edu

**Himadri Shakher Das**, University of Wyoming — hdas1@uwyo.edu

## License

See the [LICENSE](LICENSE) file. These materials are provided for transparency and reproducibility of the associated publication; please review the license terms before use.
