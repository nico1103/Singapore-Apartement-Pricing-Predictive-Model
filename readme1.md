# 🏙️ Singapore Apartment Resale Price — Predictive Model (2017–2022)

A machine learning model that predicts **Singapore HDB resale prices** using real government data (2017–2022).  
Built to test multiple regression pipelines — the winning setup combined **One-Hot Encoding + Linear Regression**, delivering strong accuracy with interpretability.

> 🎯 **Result:** ~0.82 R² on test data with ~\$63 K MAE.

---

## ✨ Highlights
- Used **official Singapore government data** with 7 engineered features  
- Compared **encoding methods** (One-Hot vs Label) and **polynomial degrees**  
- Found that simplicity beats complexity — linear regression generalized best  
- Transparent model: clear coefficients, strong real-world interpretability  

---

## 📊 Key Results

| Encoding | Degree | Train R² | Test R² | Test MAE |
|:--|:--:|:--:|:--:|:--:|
| 🟩 **One-Hot** | **1** | **0.883** | **0.822** | **≈ 63 K** |
| Label | 2 | 0.848 | 0.808 | ≈ 65 K |

> One-Hot Encoding aligned best with linear regression’s assumptions, allowing category effects (town, storey, model type) to be cleanly captured.

---
<details>
<summary>🧩 Interpreting the model</summary>

- Global signal: Larger floor area and certain towns / flat models push prices up; longer years_remaining sustains value.  
- Location signal: Shorter distance to CBD/MRT generally raises predicted price.  
- Explainability: Linear coefficients provide transparent, per-feature contributions (ideal for stakeholders).

</details>

<details>
<summary>📘 Data, Ethics & Context</summary>

- **Source:** Singapore government resale apartment datasets (2017–2022)  
- **Features:**
  - Categorical: `town`, `storey_range`, `flat_model`
  - Numerical: `floor_area_sqm`,`closest_mrt_dist`, `cbd_dist`, `years_remaining`
- **Ethics:** Predictions are educational and should not be used for financial decisions.  
- **Limitations:** Model reflects historical data; retraining is recommended as housing policies evolve.

</details>

<details>
<summary>🚀 Future Ideas</summary>

- Add **regularized regressors** (Ridge/Lasso) for smoother coefficients  
- Try **tree-based models** with feature importance comparison  
- Build a small **Streamlit dashboard** for interactive predictions  
- Include **uncertainty intervals** for stakeholder confidence  
</details>

---

⭐ *Built with Python, pandas, scikit-learn, and curiosity about what truly drives housing prices in Singapore.*
