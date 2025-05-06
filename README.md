# 🌌 Light Pollution Risk Modeling and Satellite Image Analysis

This project combines **satellite imagery processing** and **multi-factor modeling** to evaluate and visualize light pollution risk across global locations. Two independent modeling pipelines are included, supported by sensitivity testing and unsupervised learning techniques like PCA.

---

## 📁 Repository Structure

### `satellite_map_process/` – *Image-based Light Clustering*

Processes satellite images to extract light distribution features.

#### Contents:
- `data/` — Raw satellite images (PNG format), one per location.
- `result/` — Output figures showing clustering results and silhouette scores.
- `main.py` — Core script for:
  - Extracting the red channel of nightlight images
  - Thresholding to identify light sources
  - Applying KMeans/DBSCAN to cluster light distributions
  - Saving per-location metrics and cluster visualizations
- `result.csv` — Contains average light intensity, standard deviation, clutter score, and number of light clusters.
- `result_train.csv` — Processed training subset (if used).

---

### `model/` – *Multi-Indicator Light Pollution Modeling*

Implements two models to estimate light pollution severity using environmental and socioeconomic indicators.

#### Core Files:
- `collect.csv` — Input dataset with features like ANL, PM, POP, GDP, ULI, etc.
- `old_weight.npy` — Saved TOPSIS weight vector from Model 1 (for reproducibility).

#### Model 1 (`v1_model.py`):
- Uses **8 raw indicators** and applies:
  - Entropy-based weighting
  - TOPSIS ranking
  - PCA for variance visualization
- Outputs:
  - `testscore.xlsx` or equivalent score file
  - `pca_model1_plot.png` — PCA plot of all locations

#### Model 2 (`v2_model.py`):
- Derives **3 refined indicators**:
  - Unit Light Intensity
  - Development Level (GDP–population–energy)
  - Clutter Level
- Includes:
  - Data correction via Pearson correlation
  - TOPSIS scoring
  - PCA visualization
- Outputs:
  - `score.csv` — Final pollution scores per location
  - `pca_model2_plot.png` — PCA projection using 3-factor model

#### Additional:
- `sensitivity.ipynb` — Sensitivity analysis of Model 2 by altering UIL and observing score responsiveness.

---

## 📊 Key Features

- 🛰 Satellite-based clutter & cluster analysis
- 📈 Two ranking models using entropy + TOPSIS
- 📉 PCA visualization of variance structure
- 🧪 Sensitivity analysis to test model robustness

---

## 💡 How to Run

### Satellite Image Processing & Modeling:
```bash
cd satellite_map_process
python main.py

cd model
python v1_model.py      # Run Model 1 (8-indicator)
python v2_model.py      # Run Model 2 (refined 3-indicator)

