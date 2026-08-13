# ML-Based Sweet-Spot Identification for the Mowry Formation, Powder River Basin

This repository accompanies the manuscript:

**Das, H. S., Obasi, E. C., & Saraji, S.** *[Data-driven Sweet Spot Identification in the Mowry Formation: Integrating Machine Learning and Geostatistical Modeling]

It provides the code, calibration data, and calculated outputs supporting a
machine-learning and geostatistical workflow for identifying geological and
integrated (geological + engineering) sweet spots in the Mowry Formation,
Powder River Basin, Wyoming.

## Overview

1. **Machine-learning prediction** — Random Forest models predict TOC, Tmax,
   S1mod, S2, and FI; PI is derived from S1mod and S2.
2. **Sweet-spot classification** — three complementary schemes:
   - a rule-based deterministic classifier (grades A, B, C, None),
   - unsupervised K-means clustering (petrophysical populations),
   - a continuous Sweet Spot Index (SSI) using Entropy Weight Method weights.
3. **Geostatistical mapping** — depth-averaged, well-level SSI and FI values are
   interpolated across the basin using Ordinary Kriging, with Inverse Distance
   Weighting (IDW) as a supplementary comparison.

## Repository contents

| Folder / file | Description |
|---|---|
| `code/ml_models/` | Random Forest training scripts (TOC, Tmax, S1mod, S2, FI) |
| `code/kmeans/` | K-means clustering notebooks (with FI, without FI) |
| `code/geostatistics/` | Kriging scripts (SSI without FI, SSI with FI, FI) and IDW script |
| `calibration_data/` | Calibration-well data (inputs + targets) used to train the models |
| `data/Kriging_GN.xlsx` | Per-well SSI and FI values with coordinates, used as input for kriging and IDW |
| `outputs/` | Calculated model outputs and classification results for all 318 wells |
| `requirements.txt` | Python package dependencies |
| `LICENSE` | Terms of use |

### Output files
- `Outputs_of_all_wells.xlsx` — predicted properties, SSI values, and rule-based
  grades for all 318 wells (see sheet descriptions within the file).
- `KMeans_with_FI_318_wells_interpreted.xlsx` — K-means clusters and interpreted
  populations (integrated workflow, with FI).
- `KMeans_without_FI_318_wells_final_interpreted.xlsx` — K-means clusters and
  interpreted populations (geological workflow, without FI).

## Reproducibility notes

- The Random Forest training and evaluation code is fully reproducible using the
  calibration data in `calibration_data/`.
- K-means clustering uses z-score standardization, k-means++ initialization,
  `n_init = 50`, and `random_state = 42`; results are reproducible across runs.
- The kriging and IDW scripts reproduce the basin-scale maps using the per-well
  SSI/FI values and coordinates in `data/Kriging_GN.xlsx`. Variogram models and
  anisotropy parameters are specified within each script.
- The step in which the trained models are applied to the full 318-well log dataset
  to generate the per-well predictions is **not** reproduced here, because the full
  multi-well log data is not publicly released (see Data availability). The resulting
  calculated outputs are provided in `outputs/`.

## Data availability

The **calibration-well data** required to train and evaluate the models is included
in `calibration_data/`. The **per-well SSI/FI values and coordinates** used for
mapping are provided in `data/Kriging_GN.xlsx`. The **full multi-well log dataset**
(bulk density, gamma ray, and resistivity logs for all wells) is not publicly
released and remains with the authors; it is available from the corresponding author
on reasonable request. The **basin-wide calculated outputs** are provided in `outputs/`.

## Requirements

See `requirements.txt`. Core dependencies: Python 3.x, pandas, numpy, scikit-learn,
pykrige, geopandas, scipy, matplotlib, shapely, pyproj, openpyxl.

## Citation

If you refer to this work, please cite the associated publication (details above).

## Contact

Corresponding author: **Soheil Saraji**, University of Wyoming — [ssaraji@uwyo.edu]
Himadri Shakher Das — [hdas1@uwyo.edu]

## License

See the [LICENSE](LICENSE) file. These materials are provided for transparency and
reproducibility of the associated publication; please review the license terms before
any use.
