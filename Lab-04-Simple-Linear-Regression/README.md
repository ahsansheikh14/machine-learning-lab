# Lab #04: Simple Linear Regression

This folder contains the complete solutions, dataset, pre-executed interactive Jupyter Notebook, visualizations, and documentation for **Lab #04**.

---

## Table of Contents
1. [Overview & Objectives](#1-overview--objectives)
2. [Dataset Description](#2-dataset-description)
3. [Mathematical Formulas Implemented from Scratch](#3-mathematical-formulas-implemented-from-scratch)
4. [Generated Visualizations](#4-generated-visualizations)
5. [Model Evaluation & Discussion of Coefficients](#5-model-evaluation--discussion-of-coefficients)
6. [How to Run the Notebook](#6-how-to-run-the-notebook)

---

## 1. Overview & Objectives
- Implemented **Simple Linear Regression from Scratch** in Python using Ordinary Least Squares (OLS) equations.
- Verified scratch calculations against **Scikit-Learn (`LinearRegression`)**.
- Performed an 80/20 train/test split.
- Evaluated performance using **SSE, MAE, MSE, RMSE, and $R^2$**.
- Generated **2 distinct visualization plots** for the Training Set and Test Set.

---

## 2. Dataset Description
We use the benchmark `Salary_Data.csv` dataset (30 observations):
- **Independent Variable ($X$)**: `YearsExperience` (1.1 to 10.5 years)
- **Dependent Target ($Y$)**: `Salary` ($37,731 to $122,391)

---

## 3. Mathematical Formulas Implemented from Scratch

| Parameter / Metric | Formula |
| :--- | :--- |
| **Slope ($\beta_1$)** | $$\beta_1 = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sum (x_i - \bar{x})^2}$$ |
| **Intercept ($\beta_0$)** | $$\beta_0 = \bar{y} - \beta_1 \bar{x}$$ |
| **Prediction Equation** | $$\hat{y} = \beta_0 + \beta_1 x$$ |
| **Sum of Squared Errors (SSE)** | $$\text{SSE} = \sum (y_i - \hat{y}_i)^2$$ |
| **Mean Squared Error (MSE)** | $$\text{MSE} = \frac{1}{n} \sum (y_i - \hat{y}_i)^2$$ |
| **Root Mean Squared Error (RMSE)** | $$\text{RMSE} = \sqrt{\text{MSE}}$$ |
| **Coefficient of Determination ($R^2$)** | $$R^2 = 1 - \frac{\text{SSE}}{\text{SST}} = 1 - \frac{\sum (y_i - \hat{y}_i)^2}{\sum (y_i - \bar{y})^2}$$ |

---

## 4. Generated Visualizations

1. **`plots/graph_01_training_set_regression.png`**:
   - Scatter plot of training data points ($n=24$) with fitted blue regression line.
   - Shows strong linear alignment ($R^2 = 0.9412$).
2. **`plots/graph_02_test_set_regression.png`**:
   - Scatter plot of unseen test points ($n=6$) evaluated against the fitted regression line.
   - Shows residual error bars and high generalization accuracy ($R^2 = 0.9882$).

---

## 5. Model Evaluation & Discussion of Coefficients

### Coefficients:
- **Intercept ($\beta_0 = 26780.10$)**: Baseline salary with 0 years experience.
- **Slope ($\beta_1 = 9312.58$)**: Expected annual salary increase per additional year of experience.

### Performance Summary:

| Metric | Training Set ($n=24$) | Test Set ($n=6$) |
| :--- | :--- | :--- |
| **MAE** | $5,017.37 | $2,446.17 |
| **MSE** | $36,365,140.54 | $12,820,728.43 |
| **RMSE** | $6,030.35 | $3,580.60 |
| **$R^2$ Score** | **$0.9412$ ($94.12%$)** | **$0.9882$ ($98.82%$)** |

---

## 6. How to Run the Notebook
Open [`lab_04_simple_linear_regression.ipynb`](./lab_04_simple_linear_regression.ipynb) in VS Code, JupyterLab, or Antigravity IDE and click **Run All**.
