# Lab #02: Exploratory Data Analysis (EDA)

This folder contains the complete solutions, Python scripts, visualizations, and documentation for **all 3 tasks** of Lab #02.

---

## Table of Contents
1. [Overview & Objectives](#1-overview--objectives)
2. [What is Exploratory Data Analysis (EDA)?](#2-what-is-exploratory-data-analysis-eda)
3. [Dataset Description](#3-dataset-description)
4. [Lab Task #o1: Finding & Identifying Outliers in Plots](#4-lab-task-o1-finding--identifying-outliers-in-plots)
   - [Code Walkthrough & Line-by-Line Explanation](#code-walkthrough-task-o1)
   - [Generated Plots & Identified Outliers](#plots--outliers-task-o1)
5. [Lab Task #01: Full EDA Overview, Summary Statistics & Distributions](#5-lab-task-01-full-eda-overview-summary-statistics--distributions)
   - [Code Walkthrough & Line-by-Line Explanation](#code-walkthrough-task-01)
   - [Generated Plots & Initial Observations](#plots--observations-task-01)
6. [Lab Task #02: Subset Selection, Advanced Visualizations & Interpretation](#6-lab-task-02-subset-selection-advanced-visualizations--interpretation)
   - [Code Walkthrough & Line-by-Line Explanation](#code-walkthrough-task-02)
   - [Advanced Visualizations & Detailed Interpretations](#plots--interpretations-task-02)
7. [How to Run All Tasks](#7-how-to-run-all-tasks)

---

## 1. Overview & Objectives

In this lab, we demonstrate how to perform systematic **Exploratory Data Analysis (EDA)** on structured data using Python (`pandas`, `numpy`, `matplotlib`, and `seaborn`).

### All 3 Lab Tasks are Completed:
- **Lab Task #o1:** Find a dataset with outliers, plot graphs (Box Plots and Annotated Scatter Plots), and identify/label those outliers in the plots.
- **Lab Task #01:** Provide a complete overview of the dataset (size, shape, data types), calculate & display comprehensive summary statistics (mean, median, std, min, max, IQR), visualize distributions (histograms, box plots, scatter relationships), and discuss observations and patterns.
- **Lab Task #02:** Select a meaningful subset of variables (`Square_Footage`, `Bedrooms`, `Bathrooms`, `House_Age`, `Location_Score`, `Price`), create advanced visualizations (**Correlation Heatmap**, **Pairwise Scatterplots / Pairplot**, and **Time Series Plot**), and provide in-depth interpretations.

---

## 2. What is Exploratory Data Analysis (EDA)?

**Exploratory Data Analysis (EDA)** is the critical initial investigation performed on data to:
1. Discover patterns, trends, and relationships.
2. Spot anomalies, erroneous entries, and extreme **outliers**.
3. Test underlying hypotheses and assumptions.
4. Extract key variables that have the highest predictive capability.

---

## 3. Dataset Description

We use the Housing Market & Property Valuation Dataset ([`housing_data.csv`](file:///c:/Users/ahsan/machine-learning-lab/Lab-02-Exploratory-Data-Analysis/housing_data.csv)) consisting of 250 sales records across 7 features:

| Feature | Data Type | Description |
| :--- | :--- | :--- |
| `Date` | Datetime / String | Date of property transaction |
| `Square_Footage` | Numeric (`float64`) | Total living space in square feet |
| `Bedrooms` | Discrete (`int64`) | Total number of bedrooms (2 to 5) |
| `Bathrooms` | Discrete (`int64`) | Total number of bathrooms (1 to 4) |
| `House_Age` | Discrete (`int64`) | Age of property in years (1 to 39) |
| `Location_Score` | Numeric (`float64`) | Quality rating of neighborhood (1.0 to 10.0) |
| `Price` | Numeric (`float64`) | Property sale price in USD ($) |

---

## 4. Lab Task #o1: Finding & Identifying Outliers in Plots

### Script: [`task_01_outlier_detection.py`](file:///c:/Users/ahsan/machine-learning-lab/Lab-02-Exploratory-Data-Analysis/task_01_outlier_detection.py)

<a id="code-walkthrough-task-o1"></a>
### Line-by-Line Code Explanation:

```python
# 1. Imports
import os
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```
- `os`: Used for directory operations (e.g. creating `plots/`).
- `pandas`: Used for tabular data manipulation and quartile calculations.
- `matplotlib.pyplot` & `seaborn`: Visualization libraries.

```python
# 2. Load the dataset
csv_path = "housing_data.csv"
df = pd.read_csv(csv_path)
```
- Loads the dataset containing genuine market records and outlier properties.

```python
# 3. Calculate IQR & Outlier Fences
q1_price = df['Price'].quantile(0.25)          # 25th percentile (Q1)
q3_price = df['Price'].quantile(0.75)          # 75th percentile (Q3)
iqr_price = q3_price - q1_price                # Interquartile Range
lower_price = q1_price - 1.5 * iqr_price       # Lower Threshold
upper_price = q3_price + 1.5 * iqr_price       # Upper Threshold
```
- Any price $< \$203,644.12$ or $> \$678,771.12$ is flagged as an outlier.

```python
# 4. Boxplots highlighting outliers with diamond markers & fence lines
sns.boxplot(y=df['Price'], flierprops={'marker': 'D', 'markerfacecolor': 'red', 'markersize': 9})
axes[0].axhline(upper_price, color='darkred', linestyle='--', label='Upper Fence')
axes[0].axhline(lower_price, color='darkblue', linestyle='--', label='Lower Fence')
```
- Visually draws boxplots and plots outlier markers in bold red diamonds.

```python
# 5. Scatterplot with callout arrows and boxes for each outlier
for idx in all_outlier_idx:
    plt.annotate(
        f"Outlier #{idx}\n({sq:,.0f} sqft, ${pr:,.0f})",
        xy=(sq, pr), xytext=(sq + 150, pr + 35000),
        arrowprops=dict(facecolor='black', arrowstyle='->', lw=1.2),
        bbox=dict(boxstyle="round,pad=0.3", fc="#ffeedd", ec="red")
    )
```
- Draws text callout boxes with direct arrows pointing to each outlier.

<a id="plots--outliers-task-o1"></a>
### Generated Plots & Identified Outliers:
- **`plots/task_o1_boxplots_outliers.png`**: Boxplots showing IQR fences and outliers.
- **`plots/task_o1_scatter_outliers_annotated.png`**: Scatterplot with annotated outlier callout arrows.
- **Identified Outlier Points:**
  - **Index 15:** $5,800\text{ sq ft}$, priced at $\$1,450,000$ (Upper extreme luxury estate).
  - **Index 72:** $1,100\text{ sq ft}$, priced at $\$980,000$ (Overpriced compact property in ultra-prime location).
  - **Index 140:** $2,102\text{ sq ft}$, priced at $\$85,000$ (Lower bound distressed fixer-upper).
  - **Index 210:** $6,200\text{ sq ft}$, priced at $\$1,580,000$ (Mansion upper bound outlier).

---

## 5. Lab Task #01: Full EDA Overview, Summary Statistics & Distributions

### Script: [`task_01_dataset_eda.py`](file:///c:/Users/ahsan/machine-learning-lab/Lab-02-Exploratory-Data-Analysis/task_01_dataset_eda.py)

<a id="code-walkthrough-task-01"></a>
### Line-by-Line Code Explanation:

```python
# 1. Inspect Dimensions and Data Types
print(f"Total Rows: {df.shape[0]}, Total Columns: {df.shape[1]}")
print(df.info())
print(df.head())
```
- `df.shape`: Outputs `(250, 7)`.
- `df.info()`: Lists all columns, non-null counts, and memory footprint ($13.80\text{ KB}$).
- `df.head()`: Displays first 5 rows of data.

```python
# 2. Compute Full Summary Statistics
summary = df.describe().T
summary['median'] = df.median(numeric_only=True)
summary['variance'] = df.var(numeric_only=True)
summary['IQR'] = summary['75%'] - summary['25%']
print(summary[['count', 'mean', 'median', 'std', 'min', '25%', '75%', 'max', 'IQR']])
```
- Calculates all key statistical indicators of central tendency and spread.

```python
# 3. Create 2x3 Histograms with Kernel Density Estimation (KDE)
fig, axes = plt.subplots(2, 3, figsize=(15, 9))
for i, col in enumerate(features_to_plot):
    sns.histplot(df[col], kde=True, ax=axes[i//3, i%3], color=colors[i], bins=16)
```
- Plots frequency distribution histograms for all 6 numeric variables.

```python
# 4. Scatter Plots with Linear Regression Trendlines
sns.regplot(data=df, x='Square_Footage', y='Price', ax=axes[0], color='#1f77b4', line_kws={'color':'crimson'})
sns.regplot(data=df, x='Location_Score', y='Price', ax=axes[1], color='#2ca02c', line_kws={'color':'crimson'})
```
- Explores pairwise relationships with red fitted regression lines.

<a id="plots--observations-task-01"></a>
### Key Initial Observations:
1. **Normal Distribution:** `Square_Footage` follows a symmetric distribution centered at $\approx 2,027\text{ sq ft}$.
2. **Right-Skewed Distribution:** `Price` is skewed right due to the high-value luxury property sales.
3. **Primary Relationship:** `Square_Footage` exhibits a tight positive linear relationship with `Price`.

---

## 6. Lab Task #02: Subset Selection, Advanced Visualizations & Interpretation

### Script: [`task_02_advanced_visualizations.py`](file:///c:/Users/ahsan/machine-learning-lab/Lab-02-Exploratory-Data-Analysis/task_02_advanced_visualizations.py)

<a id="code-walkthrough-task-02"></a>
### Line-by-Line Code Explanation:

```python
# 1. Select subset of variables and parse date
df['Date'] = pd.to_datetime(df['Date'])
subset_columns = ['Square_Footage', 'Bedrooms', 'Bathrooms', 'House_Age', 'Location_Score', 'Price']
subset_df = df[subset_columns]
```
- Extracts the subset DataFrame for multivariate analysis.

```python
# 2. Correlation Matrix and Heatmap
corr = subset_df.corr()
sns.heatmap(corr, annot=True, fmt=".2f", cmap="coolwarm", vmin=-1, vmax=1, square=True)
```
- Computes Pearson correlation matrix and renders it as an annotated heatmap.

```python
# 3. Pairwise Scatterplots (Pairplot)
g = sns.pairplot(
    df[['Square_Footage', 'House_Age', 'Location_Score', 'Price']], 
    diag_kind='kde', 
    kind='reg'
)
```
- Creates an $n \times n$ matrix of pairwise scatterplots with regression lines and diagonal KDE density plots.

```python
# 4. Time Series Analysis with 7-Day & 30-Day Moving Averages
df_sorted = df.sort_values('Date').copy()
df_sorted['Price_7D_MA'] = df_sorted['Price'].rolling(window=7, min_periods=1).mean()
df_sorted['Price_30D_MA'] = df_sorted['Price'].rolling(window=30, min_periods=1).mean()

plt.plot(df_sorted['Date'], df_sorted['Price'], alpha=0.35, color='gray', label='Daily Transaction Price')
plt.plot(df_sorted['Date'], df_sorted['Price_7D_MA'], color='#023e8a', linewidth=2, label='7-Day Moving Avg')
plt.plot(df_sorted['Date'], df_sorted['Price_30D_MA'], color='#d90429', linewidth=2.5, linestyle='--', label='30-Day Trend')
```
- Tracks property transactions sequentially over time with moving average trend lines.

<a id="plots--interpretations-task-02"></a>
### In-Depth Interpretations:
1. **Correlation Heatmap:**
   - **`Square_Footage` vs `Price` ($r = +0.83$):** Dominant positive linear driver of home value.
   - **`Location_Score` vs `Price` ($r = +0.36$):** Substantial premium for top-tier neighborhoods.
   - **`House_Age` vs `Price` ($r = -0.11$):** Negative relationship reflecting age depreciation.
2. **Pairwise Scatterplots:**
   - Shows tight clustering along the regression line for square footage vs price, while age vs price shows broad dispersion.
3. **Time Series Analysis:**
   - The moving average stays level between $\$420,000$ and $\$460,000$, showing market stability across the time window.

---

## 7. How to Run All Tasks

Open your terminal or Command Prompt and run:

```bash
cd Lab-02-Exploratory-Data-Analysis

# Run Lab Task #o1 (Outlier Detection & Annotation)
python task_01_outlier_detection.py

# Run Lab Task #01 (Full EDA, Statistics & Distributions)
python task_01_dataset_eda.py

# Run Lab Task #02 (Advanced Visualizations & Interpretations)
python task_02_advanced_visualizations.py
```

All 7 generated figures are automatically saved inside the [`plots/`](file:///c:/Users/ahsan/machine-learning-lab/Lab-02-Exploratory-Data-Analysis/plots) directory:
- `plots/task_o1_boxplots_outliers.png`
- `plots/task_o1_scatter_outliers_annotated.png`
- `plots/task_01_feature_histograms.png`
- `plots/task_01_feature_boxplots.png`
- `plots/task_01_scatter_relationships.png`
- `plots/task_02_correlation_heatmap.png`
- `plots/task_02_pairwise_scatterplots.png`
- `plots/task_02_timeseries_plot.png`
