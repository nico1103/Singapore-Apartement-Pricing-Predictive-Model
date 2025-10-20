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
