# Gene Expression Classification — ML Models

This repo trains and compares multiple machine learning models on a
gene expression dataset (features selected via `FEATURE_SELECTION.ipynb`),
then uses SHAP to explain the best-performing model.

## Models

| Notebook | Model |
|---|---|
| `ADAboost_2026.ipynb` | AdaBoost |
| `DTC_2026.ipynb` | Decision Tree Classifier |
| `RF_2026.ipynb` | Random Forest |
| `SVC_RBF_2026.ipynb` | Support Vector Classifier (RBF kernel) |
| `SVC_linear_2026.ipynb` | Support Vector Classifier (linear kernel) |
| `XGBOOST_2026.ipynb` | XGBoost |
| `lightGBM_2026.ipynb` | LightGBM |
| `logistic_regression_2026.ipynb` | Logistic Regression |

## Input files - given in the data folder
**lasso_batchy.csv** - main training data (LASSO-selected gene features + labels), used for cross-validation and hyperparameter tuning in every model notebook

**validation_count_matrix.csv** - held-out validation set expression matrix

**LASSO_GENES.txt** - list of genes selected by LASSO, used to subset the validation matrix

## Validation

All models are evaluated using:
- **Stratified K-Fold** cross-validation
- **Repeated Stratified K-Fold** cross-validation

## Model interpretation (SHAP)

**SHAP** is applied to the best-performing model to explain feature
contributions and identify the most important genes for prediction.

- **TreeExplainer** - used for tree-based models (Random Forest, XGBoost,
  LightGBM, AdaBoost, Decision Tree). Fast and exact for these models.
- **KernelExplainer** - used for non-tree models (SVC, Logistic Regression).
  Model-agnostic but slower, so it's run on a smaller background sample.

Both give SHAP values showing how much each gene pushes a prediction
toward disease or control, and are used to rank the top genes.

## Requirements

```
pandas
numpy
scikit-learn
xgboost
lightgbm
shap
matplotlib
```

Install with:
```bash
pip install pandas numpy scikit-learn xgboost lightgbm shap matplotlib
```

## Usage

1. Run `FEATURE_SELECTION.ipynb` to generate the selected gene set.
2. Run any of the model notebooks to train and evaluate that model on the external validation dataset.
3. SHAP analysis is included in every notebook. 
