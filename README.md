# Sim-JEB Hybrid Model

This project applies **machine learning** and **deep learning** to predict displacements in mechanical brackets under load, using **CAE** data of Jet Engine bracket **Sim-JEB dataset**.

---

## Dataset Overview

Each record includes:
- Geometry features:
  - `num_vertices`, `num_faces`, `volume`, `surface_area`, `average_edge_length`, etc.
- Stress and displacement measures:
  - `max_ver_stress`, `max_hor_stress`, `max_dia_stress`, `max_tor_stress`
  - `max_ver_magdisp`, `max_hor_magdisp`, `max_dia_magdisp`
- Bracket category (`block`, `beam`, `arch`, etc.)

**Targets (Predicted):**
- `max_ver_magdisp`
- `max_hor_magdisp`
- `max_dia_magdisp`

---

## Workflow

1. **Data Preprocessing**
   - Outlier removal
   - PCA (optional)
   - One-hot encoding
   - Standardization
   - Train/Validation/Test split

2. **Models Trained**
   - **XGBoost** (`MultiOutputRegressor`)
   - **MLPRegressor**
   - **Keras Neural Network**

3. **Hybrid Ensemble**
   - Stack predictions of all 3 models
   - Train a **Linear Regression meta-model**
   - Final prediction from meta-model output

---

## Performance Summary

| Model           | Val RMSE | Val R² | Test RMSE | Test R² |
|-----------------|----------|--------|-----------|---------|
| **XGBoost**     | ~0.27    | ~0.92  | ~0.38     | ~0.83   |
| **MLPRegressor**| ~0.31    | ~0.89  | ~0.45     | ~0.79   |
| **Keras NN**    | ~0.29    | ~0.90  | ~0.42     | ~0.81   |
| **Hybrid 🏆**    | ~0.31    | ~0.91  | ~0.31     | ~0.88   |

The **hybrid model** achieved the best generalization.

---

## Visualizations

- **Actual vs Predicted** scatter plots
- **Comparison Bar Charts** for RMSE and R²

---

## Saving & Loading Models

All trained models are saved:
- **XGBoost:** `xgb_model.pkl`
- **MLPRegressor:** `mlp_model.pkl`
- **Keras NN:** `keras_nn_model.h5`
- **Meta-Model:** `meta_model.pkl`

You can load them anytime to make predictions without retraining.

---

⭐ Feel free to star this repository if you find it helpful!
