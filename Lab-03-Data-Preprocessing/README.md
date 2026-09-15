# Lab #03: Data Preprocessing & Feature Scaling

This folder contains the complete interactive Jupyter notebooks, standalone Python scripts, visualizations, and documentation for **Lab #03**.

---

## Table of Contents
1. [Overview & Objectives](#1-overview--objectives)
2. [Notebooks & Project Structure](#2-notebooks--project-structure)
3. [Lab Task 1: Image Data Handling & Preprocessing Pipeline](#3-lab-task-1-image-data-handling--preprocessing-pipeline)
   - [Overview & What We Did](#task-1-overview)
   - [Why We Did It (Theoretical Rationale)](#task-1-rationale)
   - [Generated Visualizations](#task-1-visualizations)
4. [Lab Task 2: Feature Scaling on Image Data (StandardScaler vs. MinMaxScaler)](#4-lab-task-2-feature-scaling-on-image-data-standardscaler-vs-minmaxscaler)
   - [Overview & What We Did](#task-2-overview)
   - [Why We Did It (Theoretical Rationale)](#task-2-rationale)
   - [When to Use MinMaxScaler vs. StandardScaler](#when-to-use-each-scaler)
   - [Generated Visualizations](#task-2-visualizations)
5. [How to Run the Notebooks and Scripts](#5-how-to-run-the-notebooks-and-scripts)

---

## 1. Overview & Objectives

In this lab, we demonstrate end-to-end data preprocessing and feature scaling on a multi-class image dataset (**Vehicles**: `cars`, `motorcycles`, `airplanes`), covering:
- Handling missing, corrupted, or 0-byte image files safely with `try-except` blocks.
- Exploring image dimensions, color channels, aspect ratios, and class balance.
- Standardizing image resolutions to uniform tensors ($64 \times 64 \times 3$).
- Converting categorical text labels into binary vectors via **One-Hot Encoding** (`OneHotEncoder`).
- Normalizing pixel values to $[0.0, 1.0]$ using **`MinMaxScaler`**.
- Standardizing pixel distributions to $\mu=0, \sigma=1$ using **`StandardScaler`**.
- Visualizing and interpreting pixel intensity distributions before and after scaling.

---

## 2. Notebooks & Project Structure

```
Lab-03-Data-Preprocessing/
├── lab_03_task1_image_preprocessing.ipynb    # Interactive notebook for Lab Task 1 (Pre-executed)
├── lab_03_task2_feature_scaling.ipynb        # Interactive notebook for Lab Task 2 (Pre-executed)
├── task_01_image_preprocessing.py            # Standalone Python script for Task 1
├── task_02_feature_scaling.py                # Standalone Python script for Task 2
├── README.md                                 # Full lab documentation and theoretical breakdown
├── dataset/                                  # Vehicle image dataset
│   ├── cars/                                 # Car RGB images + corrupted test sample
│   ├── motorcycles/                          # Motorcycle RGB images + 0-byte test sample
│   └── airplanes/                            # Airplane RGB images
└── plots/                                    # High-resolution generated figures
    ├── task_01_class_distribution.png
    ├── task_01_original_vs_preprocessed.png
    ├── task_02_pixel_distributions_comparison.png
    ├── task_02_rgb_channel_distributions.png
    └── task_02_scaled_images_samples.png
```

---

<a id="3-lab-task-1-image-data-handling--preprocessing-pipeline"></a>
## 3. Lab Task 1: Image Data Handling & Preprocessing Pipeline

### Notebook: [`lab_03_task1_image_preprocessing.ipynb`](./lab_03_task1_image_preprocessing.ipynb)
### Script: [`task_01_image_preprocessing.py`](./task_01_image_preprocessing.py)

<a id="task-1-overview"></a>
### What We Did:
1. **Directory Scanning & Verification**: Traversed the `dataset/` directory containing vehicle classes.
2. **Corrupted File Detection**: Tested every file for 0-byte size and corrupted header bytes using `PIL.Image.open()` + `img.verify()`.
3. **Exploratory Metadata Extraction**: Built a summary DataFrame recording original dimensions (ranging from $400\times 300$ to $550\times 367$), aspect ratios, and color channels.
4. **Standardized Resizing**: Resized all valid images to $64 \times 64 \times 3$ using high-quality Bilinear Resampling.
5. **One-Hot Encoding**: Mapped string class names to integers via `LabelEncoder` ($0, 1, 2$) and then binary vectors via `OneHotEncoder` ($[1,0,0], [0,1,0], [0,0,1]$).
6. **Side-by-Side Visualization**: Rendered comparison figures showing raw vs. preprocessed images alongside their encoded vectors.

<a id="task-1-rationale"></a>
### Why We Did It (Theoretical Rationale):
- **Why detect corrupted images?** Machine learning training loops throw fatal exceptions when encountering broken files mid-epoch. Detecting and logging them in advance ensures a robust pipeline.
- **Why resize images?** Machine learning and deep learning algorithms require fixed-size multidimensional tensor inputs (e.g. matrix multiplication requires uniform dimensions).
- **Why One-Hot Encode labels?** If we assign `cars=0`, `motorcycles=1`, `airplanes=2`, mathematical equations in ML models assume an arithmetic ranking (e.g., $cars < motorcycles < airplanes$ or $motorcycles \times 2 = airplanes$). One-Hot Encoding assigns an orthogonal binary vector to each category, eliminating false ordinal bias.

<a id="task-1-visualizations"></a>
### Generated Visualizations:
- **`plots/task_01_class_distribution.png`**: Bar chart showing balanced class counts across vehicle classes.
- **`plots/task_01_original_vs_preprocessed.png`**: Visual comparison grid between raw images of varied shapes and standardized $64 \times 64 \times 3$ preprocessed tensors.

---

<a id="4-lab-task-2-feature-scaling-on-image-data-standardscaler-vs-minmaxscaler"></a>
## 4. Lab Task 2: Feature Scaling on Image Data (StandardScaler vs. MinMaxScaler)

### Notebook: [`lab_03_task2_feature_scaling.ipynb`](./lab_03_task2_feature_scaling.ipynb)
### Script: [`task_02_feature_scaling.py`](./task_02_feature_scaling.py)

<a id="task-2-overview"></a>
### What We Did:
1. **Flattened Image Tensors**: Flattened $(N, 64, 64, 3)$ tensors into a 2D feature matrix $(N, 12288)$ for scikit-learn scalers.
2. **MinMaxScaler (Normalization)**: Rescaled raw pixel values $[0, 255]$ into $[0.0, 1.0]$.
3. **StandardScaler (Standardization)**: Transformed pixel values into standard normal Z-scores centered at $\mu = 0$ with $\sigma = 1$.
4. **Distribution Plotting**: Created 3-panel histograms with KDE curves for overall pixels and a $3\times 3$ grid for individual RGB channels.
5. **Image Rendering Across Scalers**: Displayed raw vs normalized vs standardized image samples.

<a id="task-2-rationale"></a>
### Why We Did It (Theoretical Rationale):
- Raw 8-bit integer pixel intensities ($0$ to $255$) cause gradient explosion and slow convergence in gradient-descent optimizers.
- Scaling puts all features on a uniform scale, preventing features with large numerical magnitudes from dominating the loss function.

<a id="when-to-use-each-scaler"></a>
### When to Use `MinMaxScaler` vs. `StandardScaler`

| Dimension | **`MinMaxScaler` (Normalization)** | **`StandardScaler` (Standardization)** |
| :--- | :--- | :--- |
| **Mathematical Formula** | $$X' = \frac{X - X_{min}}{X_{max} - X_{min}}$$ | $$Z = \frac{X - \mu}{\sigma}$$ |
| **Output Interval** | Strictly bounded in $[0.0, 1.0]$ | Unbounded, centered at $\mu=0$ with $\sigma=1$ |
| **Outlier Sensitivity** | **High**: Outliers compress all valid data points into a narrow sub-range. | **Moderate**: Outliers affect mean/std, but preserve variance without compression. |
| **Best Used When** | 1. **Neural Networks & CNNs**: Activation functions (Sigmoid, Softmax) expect bounded inputs.<br>2. **Image Generation (GANs/VAEs)**: Models reconstructing pixel values in $[0,1]$ or $[-1,1]$.<br>3. Non-parametric models making no distribution assumptions. | 1. **Distance-Based Algorithms**: SVMs with RBF kernel, K-Means Clustering, KNN, PCA.<br>2. **Regularized Linear Models**: Ridge, Lasso, Logistic Regression.<br>3. Features following an approximate Gaussian / Normal distribution. |

<a id="task-2-visualizations"></a>
### Generated Visualizations:
- **`plots/task_02_pixel_distributions_comparison.png`**: 3-panel comparison of Raw ($[0,255]$) vs MinMaxScaler ($[0,1]$) vs StandardScaler ($\mu=0, \sigma=1$).
- **`plots/task_02_rgb_channel_distributions.png`**: $3 \times 3$ grid comparing Red, Green, and Blue channels across all 3 scaling methods.
- **`plots/task_02_scaled_images_samples.png`**: Side-by-side visual renderings of images under each scaling method.

---

## 5. How to Run the Notebooks and Scripts

### Option A: Open Interactive Jupyter Notebooks
Open either of the following notebooks in JupyterLab, VS Code, or Antigravity IDE:
1. `lab_03_task1_image_preprocessing.ipynb`
2. `lab_03_task2_feature_scaling.ipynb`

### Option B: Run Standalone Python Scripts via Terminal
```bash
cd Lab-03-Data-Preprocessing

# Run Task 1 (Image Preprocessing & One-Hot Encoding)
python task_01_image_preprocessing.py

# Run Task 2 (Feature Scaling & Distribution Analysis)
python task_02_feature_scaling.py
```
