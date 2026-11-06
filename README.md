# Machine Learning IV — Project Analytics Dashboard

**Student:** Atharv M Bennur  
**Roll number:** 224010  
**Course:** Bachelor of Computer Applications

## Project structure

```text
Machine_Learning_IV/
├── Notebook/
│   └── 224010_AtharvBennur_ML_Project.ipynb
├── Datasets/
│   ├── Iris.csv
│   ├── CAR DETAILS FROM CAR DEKHO.csv
│   ├── Mall_Customers.csv
│   └── StudentPerformanceFactors.csv
├── Dashboard/
│   └── index.html
├── ML_IV_Presentation.pptx
└── README.md
```

The supplied `StudentPerformanceFactors-selected-columns.csv` is also retained in `Datasets/`; the notebook and dashboard use the full `StudentPerformanceFactors.csv`.

## Open the dashboard

Open `Dashboard/index.html` directly in a modern browser. It is a standalone HTML5 page with inline CSS, JavaScript, and chart data exported from an execution of the project notebook. No server, build step, external chart library, or CSV access is required. Use the sidebar to switch among the overview and four project views; use **Print / Save PDF** for a report.

## Run the notebook

1. Open `Notebook/224010_AtharvBennur_ML_Project.ipynb` in VS Code with the Jupyter extension, or upload it to Google Colab.
2. Run cells in order and select the requested CSV at each dataset prompt: `Iris.csv`, `CAR DETAILS FROM CAR DEKHO.csv`, `Mall_Customers.csv`, and `StudentPerformanceFactors.csv`.
3. Continue through the evaluation and prediction cells to generate the notebook's tables and plots. The notebook uses training-only cross-validation for model selection and reserves its 20% test split for final evaluation.

## Measured results embedded in the dashboard

The dashboard reports the supplied notebook's held-out results:

- **Iris:** Logistic Regression and tuned KNN each achieved 93.3% accuracy.
- **Car price:** Selected log-target Linear Regression achieved test R² = 0.519. The assignment target of R² ≥ 0.75 is **not met**; the result is shown without adjustment.
- **Mall customers:** K-Means with K = 5 achieved a silhouette score of 0.555.
- **Student performance:** Linear Regression achieved test R² = 0.770; Random Forest Regressor achieved 0.682. Linear Regression was selected using training-only cross-validation.

The notebook was executed against the supplied CSV files when the dashboard was prepared. Scores can vary if data or software versions change.
