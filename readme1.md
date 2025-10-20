Singapore Apartment Resale Price — Predictive Model (2017–2022)

Turn real government data into clear price predictions.
This project builds a regression model to estimate Singapore HDB resale prices using features like floor area, storey range, town, flat model, and distance to CBD/MRT (2017–2022 data).

Result: A simple, interpretable pipeline—One-Hot Encoding + Linear Regression—consistently delivered the strongest generalization on held-out data: ~0.82 R² with ~$63k MAE.

Why this project stands out

Real, official data (2017–2022) engineered into model-ready features

Methodical comparisons: encoding strategies (OHE vs Label), polynomial degrees, and hyperparameters

Lean, interpretable winner: Linear Regression + OHE outperformed more complex variants while remaining easy to explain

Clear takeaways for non-ML stakeholders: which factors move price and by how much

Data & Features

Source: Singapore government resale apartment data (2017–2022)

Key engineered features:

closest_mrt_dist (km), cbd_dist (km)

town, storey_range, flat_model (categorical)

floor_area_sqm, years_remaining (numeric)

The notebook contains full cleaning and preprocessing steps.

Approach
             ┌────────────────────────────────────────────────────┐
Data Source ─►  Load & Clean  ─►  Feature Engineering  ─►  Split  │
             └────────────────────────────────────────────────────┘
                                             │(train/test)
                                             ▼
                 ┌───────────────────────────────────────────────┐
                 │  Encode categoricals (OHE / Label)            │
                 │  Try polynomial degrees (1, 2, …)             │
                 │  Train Linear Regression                      │
                 │  Evaluate (MAE, MSE, R²)                      │
                 └───────────────────────────────────────────────┘
                                             ▼
                              Select best config (OHE + degree 1)

Experiments & Results (rounded)
Encoding	Degree	Train MAE	Train R²	Test MAE	Test R²
One-Hot	1	≈ 54.3k	≈ 0.883	≈ 63.1k	≈ 0.822
Label	2	≈ 61.2k	≈ 0.848	≈ 65.0k	≈ 0.808

Why OHE + Linear Regression?
One-hot encoding exposes per-category offsets that align with linear regression’s assumptions. That lets the model learn distinct price lifts/drops for each town, storey range, and flat model without forcing arbitrary ordinality (a problem for label encoding). The result: higher R² and lower MAE on test data, with coefficients that are easy to interpret.

Repository structure
.
├── Project.ipynb            # Full workflow: prep → modeling → evaluation
├── 20_record_per_town.csv   # Sample data slice used by the notebook
├── Group E final.pptx.pdf   # Slides with experiment tables & visuals
└── README.md

How to use (high-level)

Open Project.ipynb to see data prep, feature engineering, encoding comparisons, and model evaluation.

The notebook cells can be run top-to-bottom to reproduce results with the included sample CSV (or point to the full dataset if you have it).

If you’d like full “clone-and-run” instructions with a requirements.txt, say the word and I’ll add them.

Interpreting the model

Global signal: Larger floor area and certain towns / flat models push prices up; longer years_remaining sustains value.

Location signal: Shorter distance to CBD/MRT generally raises predicted price.

Explainability: Linear coefficients provide transparent, per-feature contributions (ideal for stakeholders).

Ethics, provenance & limits

Data is from official Singapore government sources (publicly available).

Predictions reflect historical relationships (2017–2022) and do not constitute financial advice.

Out-of-distribution shifts (policy changes, economic shocks) can reduce accuracy; periodic retraining is recommended.

Future improvements

Add regularization (Ridge/Lasso) for stability across splits

Explore tree-based baselines (RF/XGBoost) with careful leakage prevention

Calibrate prediction intervals for decision-grade uncertainty

Expand feature set (amenities density, school proximity, renovation proxies)
             
             ┌────────────────────────────────────────────────────┐
Data Source ─►  Load & Clean  ─►  Feature Engineering  ─►  Split  │
             └────────────────────────────────────────────────────┘
                                             │(train/test)
                                             ▼
                 ┌───────────────────────────────────────────────┐
                 │  Encode categoricals (OHE / Label)            │
                 │  Try polynomial degrees (1, 2, …)             │
                 │  Train Linear Regression                      │
                 │  Evaluate (MAE, MSE, R²)                      │
                 └───────────────────────────────────────────────┘
                                             ▼
                              Select best config (OHE + degree 1)
