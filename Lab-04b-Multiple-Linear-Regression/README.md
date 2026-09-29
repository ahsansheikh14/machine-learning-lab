# Lab #04b: Multiple Linear Regression

This folder contains the complete dataset, pre-executed interactive Jupyter Notebook, visualizations, and documentation for **Lab #04b: Multiple Linear Regression**.

---

## Table of Contents
1. [Overview & Objectives](#1-overview--objectives)
2. [Dataset Description](#2-dataset-description)
3. [Mathematical Formulation](#3-mathematical-formulation)
4. [Generated Visualizations](#4-generated-visualizations)
5. [Model Evaluation & Detailed Discussion of Coefficients](#5-model-evaluation--detailed-discussion-of-coefficients)
6. [How to Run the Notebook](#6-how-to-run-the-notebook)

---

## 1. Overview & Objectives
In this lab, we build a **Multiple Linear Regression (MLR)** model to predict company **Profit** using three independent predictor variables:
- `RD_Spend` ($X_1$)
- `Marketing_Spend` ($X_2$)
- `Operational_Cost` ($X_3$)

### Key Highlights:
- **80% Training ($n=40$) / 20% Testing ($n=10$)** split.
- **Exploratory Correlation Analysis** and scatter plots of each predictor vs. Profit.
- Model fitting with Scikit-Learn `LinearRegression`.
- Comprehensive evaluation (**$R^2$, MAE, MSE, RMSE**) on both training and testing subsets.
- Detailed interpretation of regression coefficients ($eta_0, eta_1, eta_2, eta_3$) and business insights.

---

## 2. Dataset Description
The dataset [`startup_investment_data.csv`](./startup_investment_data.csv) contains 50 startup records:

| Feature | Role | Type | Range | Description |
| :--- | :--- | :--- | :--- | :--- |
| **`RD_Spend` ($X_1$)** | Predictor | Continuous ($) | $\$0 - \$165,349$ | Research and Development expenditure |
| **`Marketing_Spend` ($X_2$)** | Predictor | Continuous ($) | $\$0 - \$471,784$ | Marketing and advertising budget |
| **`Operational_Cost` ($X_3$)** | Predictor | Continuous ($) | $\$51,283 - \$182,646$ | Operational and administrative overhead |
| **`Profit` ($Y$)** | **Target** | Continuous ($) | $\$14,681 - \$192,262$ | Net profit generated |

---

## 3. Mathematical Formulation

$$Y = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \beta_3 X_3 + \epsilon$$

### Fitted Model Equation:
$$\text{Profit} = 50296.22 + 0.8057 \times (\text{RD\_Spend}) + 0.0268 \times (\text{Marketing\_Spend}) - 0.0270 \times (\text{Operational\_Cost})$$

---

## 4. Generated Visualizations

1. **`plots/feature_relationships_scatter.png`**:
   - 3-panel scatter plots showing how R&D Spend, Marketing Spend, and Operational Cost relate to Profit with fitted trendlines.
2. **`plots/correlation_heatmap.png`**:
   - Annotated correlation matrix highlighting the strong $0.973$ correlation between R&D Spend and Profit.
3. **`plots/actual_vs_predicted_fit.png`**:
   - Scatter plot of Actual vs. Predicted Profit on unseen test startups with the ideal $45^\circ$ fit line ($R^2 = 0.9514$).
4. **`plots/residual_error_plot.png`**:
   - Diagnostic residual plot showing errors randomly scattered around zero.

---

## 5. Model Evaluation & Detailed Discussion of Coefficients

### Coefficients & Significance:

| Coefficient | Parameter | Value | Interpretation & Business Significance |
| :--- | :--- | :--- | :--- |
| **Intercept** | $\beta_0$ | **$50,296.22** | Baseline profit if all spending categories are $\$0$. |
| **`RD_Spend`** | $\beta_1$ | **$+0.8057$** | **Most Influential:** Every $\$1$ spent on R&D yields **$+\$0.8057$** in net profit (holding other factors constant). |
| **`Marketing_Spend`** | $\beta_2$ | **$+0.0268$** | Every $\$1$ spent on Marketing yields **$+\$0.0268$** in profit. |
| **`Operational_Cost`** | $\beta_3$ | **$-0.0270$** | Every $\$1$ spent on Operations slightly reduces profit by **$-\$0.0270$**. |

### Performance Summary:

| Evaluation Metric | Training Set ($80\%, n=40$) | Test Set ($20\%, n=10$) |
| :--- | :--- | :--- |
| **$R^2$ Score** | **$0.9497$ ($94.97\%$)** | **$0.9514$ ($95.14\%$)** |
| **Mean Absolute Error (MAE)** | $\$6,613.68$ | $\$6,897.23$ |
| **Root Mean Squared Error (RMSE)** | $\$9,198.42$ | $\$8,965.34$ |

---

## 6. How to Run the Notebook
Open [`lab_04b_multiple_linear_regression.ipynb`](./lab_04b_multiple_linear_regression.ipynb) in VS Code, JupyterLab, or Antigravity IDE and click **Run All**.
