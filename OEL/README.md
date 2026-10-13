# Exploring Predictive Analysis with Regression (OEL)

**Course:** AIC 301 — Machine Learning Lab  
**University:** Bahria University, Islamabad Campus  
**Date:** October 2024  

---

## 📌 Project Overview
This project develops and evaluates predictive regression models on the **Medical Cost Personal Dataset** from Kaggle to predict individual health insurance charges (`charges` in USD).

### Key Highlights:
1. **Real-world Kaggle Dataset:** 1,338 observations, 7 features.
2. **Exploratory Data Analysis (EDA):** Discovered that smoking is the primary determinant of healthcare costs ($r = 0.79$), followed by age ($r = 0.30$) and BMI ($r = 0.20$), with a severe compound risk interaction between BMI and smoking.
3. **Data Preprocessing:** One-hot encoded categorical variables (`sex`, `smoker`, `region`) avoiding the dummy variable trap with `drop_first=True`, and created an 80/20 train-test partition ($N_{\text{train}}=1,070$, $N_{\text{test}}=268$, `random_state=42`).
4. **Model 1 — Multiple Linear Regression (MLR):** Fitted a baseline linear plane on all 8 encoded features.
5. **Model 2 — Polynomial Regression (Degree 2):** Expanded the feature space to 44 quadratic and interaction terms to capture non-linear curvature and risk compounding.
6. **Diagnostic Analysis:** Evaluated residual plots, actual vs. predicted scatter charts, and standard regression metrics ($R^2$, MSE, RMSE, MAE).

---

## 📊 Performance Comparison Summary

| Metric | Multiple Linear Regression | Polynomial Regression (Degree 2) | Improvement / Difference |
| :--- | :---: | :---: | :---: |
| **Train $R^2$ Score** | 74.19% | 84.34% | +10.15% |
| **Test $R^2$ Score** | **78.36%** | **86.66%** | **+8.30%** 🏆 |
| **Test Mean Squared Error (MSE)** | 33,596,915.85 | 20,712,805.99 | **-38.3% error reduction** |
| **Test Root Mean Squared Error (RMSE)** | **$5,796.28** | **$4,551.13** | **-$1,245.15 error per person** |
| **Test Mean Absolute Error (MAE)** | **$4,181.19** | **$2,729.50** | **-$1,451.69 error per person** |

---

## 📁 Repository Structure

```
OEL/
│
├── oel_regression_analysis.ipynb   # Complete, fully-executed, self-contained Jupyter Notebook
├── insurance.csv                   # Kaggle Medical Cost dataset (1,338 rows)
├── README.md                       # Comprehensive documentation & lab report
└── plots/                          # High-resolution saved diagnostic visualizations
    ├── 01_charges_distribution.png
    ├── 02_feature_distributions.png
    ├── 03_categorical_distributions.png
    ├── 04_scatter_features_vs_charges.png
    ├── 05_boxplots.png
    ├── 06_correlation_heatmap.png
    ├── 07_mlr_performance_diagnostics.png
    ├── 08_poly_performance_diagnostics.png
    └── 09_model_metric_comparison.png
```

---

## 🔍 Key Findings & Reflection

1. **Why Polynomial Regression Won:**
   - Real-world health costs scale non-linearly with age ($age^2$).
   - High BMI combined with smoking ($bmi \times smoker\_yes$) produces exponential risk, not simple addition.
   - Polynomial Regression flattened out the residual streaks seen in the linear model's diagnostics.
2. **Challenges Overcome:**
   - Avoided the dummy variable trap via `drop_first=True`.
   - Prevented data leakage by fitting polynomial transformation strictly on the training partition.
