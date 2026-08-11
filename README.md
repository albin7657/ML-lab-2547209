# Lab 9 – SVM, PCA and LDA

## Machine Learning Lab

This laboratory experiment demonstrates the application of **Support Vector Machine (SVM)** for supervised classification and **Principal Component Analysis (PCA)** for dimensionality reduction. An additional **Linear Discriminant Analysis (LDA)** experiment is performed to compare supervised and unsupervised dimensionality reduction techniques.

---

## Aim

To implement Support Vector Machine (SVM) for classification and Principal Component Analysis (PCA) for dimensionality reduction, and analyse their effectiveness using real-world datasets.

---

## Objectives

* To implement and evaluate the performance of the Support Vector Machine (SVM) classifier.
* To perform hyperparameter tuning for an SVM classifier.
* To evaluate SVM using standard classification metrics.
* To apply PCA for dimensionality reduction.
* To analyse the variance retained by principal components.
* To visualize the PCA-transformed feature space.
* To determine the minimum number of components required to retain at least 95% variance.
* To compare PCA and LDA in terms of dimensionality reduction and class separability.
* To understand the difference between supervised and unsupervised learning techniques.

---

# Part A – Support Vector Machine (SVM)

## Dataset

### UCI Breast Cancer Wisconsin (Diagnostic) Dataset

The Breast Cancer Wisconsin (Diagnostic) dataset is used for binary classification.

**Dataset:**
https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic

### Dataset Characteristics

* **Samples:** 569
* **Features:** 30
* **Classes:** 2
* **Classification Type:** Binary Classification
* **Target Classes:** Malignant and Benign

---

## SVM Tasks

The following tasks are performed:

1. Load the dataset and perform preprocessing.
2. Check for missing values and class distribution.
3. Standardize the numerical features.
4. Split the dataset into training and testing sets using an **80:20 ratio**.
5. Train an SVM classifier using a **Linear Kernel**.
6. Perform hyperparameter tuning using Grid Search and 5-fold cross-validation.
7. Evaluate the final model using:

   * Accuracy
   * Precision
   * Recall
   * F1 Score
   * Confusion Matrix
8. Summarize the model performance.

---

## SVM Methodology

```text
Load Dataset
      ↓
Data Inspection
      ↓
Feature / Target Separation
      ↓
Feature Standardization
      ↓
80:20 Train-Test Split
      ↓
Linear SVM
      ↓
Hyperparameter Tuning
      ↓
Model Evaluation
      ↓
Confusion Matrix
```

The regularization parameter `C` is tuned using the following values:

```text
C = [0.01, 0.1, 1, 10, 100]
```

Five-fold cross-validation is used during hyperparameter tuning.

---

## SVM Results

The best regularization parameter obtained during hyperparameter tuning is:

```text
C = 0.1
```

The tuned Linear SVM achieved the following performance:

| Metric    |      Score |
| --------- | ---------: |
| Accuracy  | **98.25%** |
| Precision | **98.61%** |
| Recall    | **98.61%** |
| F1 Score  | **98.61%** |

### Confusion Matrix

```text
[[41, 1],
 [ 1, 71]]
```

The model correctly classified the majority of the test samples and produced only **2 misclassified samples out of 114 test samples**.

### SVM Observation

The Linear SVM achieved high performance across all evaluation metrics. The results indicate that the standardized features provide good separation between malignant and benign samples.

Hyperparameter tuning identified `C = 0.1` as the best value among the tested parameters based on the cross-validation F1 score.

---

# Part B – Principal Component Analysis (PCA)

## Dataset

### UCI Wine Dataset

The Wine dataset is used for dimensionality reduction and visualization.

**Dataset:**
https://archive.ics.uci.edu/dataset/109/wine

### Dataset Characteristics

* **Samples:** 178
* **Original Features:** 13
* **Classes:** 3
* **Feature Type:** Numerical

---

## PCA Tasks

The following tasks are performed:

1. Load the Wine dataset.
2. Standardize the features.
3. Apply PCA to reduce the dataset from 13 features to 2 principal components.
4. Display the explained variance ratio.
5. Calculate cumulative explained variance.
6. Determine the minimum number of components required to retain at least 95% variance.
7. Visualize the transformed dataset using a two-dimensional scatter plot.
8. Compare the original and transformed datasets in terms of:

   * Number of features
   * Information retained
   * Computational efficiency
9. Interpret the significance of PC1 and PC2.
10. Discuss the advantages, limitations, and applications of PCA.

---

## PCA Methodology

```text
Load Wine Dataset
       ↓
Feature / Target Separation
       ↓
Feature Standardization
       ↓
PCA: 13 → 2 Components
       ↓
Explained Variance Analysis
       ↓
Cumulative Variance
       ↓
95% Variance Analysis
       ↓
2D Visualization
```

---

## PCA Results

### Dimensionality Reduction

The original dataset contains:

```text
178 samples × 13 features
```

After applying PCA with two components:

```text
178 samples × 2 components
```

Therefore:

```text
13 → 2 features
```

This represents an **84.62% reduction in the number of features**.

---

## Explained Variance

The first two principal components retain:

| Principal Component | Explained Variance |
| ------------------- | -----------------: |
| PC1                 |         **36.20%** |
| PC2                 |         **19.21%** |
| **Total**           |         **55.41%** |

Therefore, the first two principal components retain approximately **55.41% of the total variance**.

---

## 95% Variance Requirement

The cumulative explained variance is analysed to determine how many principal components are required to retain at least 95% of the total variance.

| Number of Components | Cumulative Variance |
| -------------------: | ------------------: |
|                    9 |          **94.24%** |
|                   10 |          **96.17%** |

Therefore, the minimum number of principal components required to retain at least 95% of the total variance is:

```text
10 Components
```

Thus, PCA can reduce the original 13 features to 10 components while retaining at least 95% of the total variance.

---

## Original vs PCA-Transformed Dataset

| Parameter            | Original Dataset | PCA Dataset |
| -------------------- | ---------------: | ----------: |
| Number of Samples    |              178 |         178 |
| Number of Features   |               13 |           2 |
| Information Retained |             100% |      55.41% |
| Feature Reduction    |                — |      84.62% |
| Dimensionality       |             High |         Low |

The reduction in the number of features can improve computational efficiency for subsequent machine learning operations because fewer dimensions need to be processed.

---

# Extra Credit – Linear Discriminant Analysis (LDA)

## Aim

Apply Linear Discriminant Analysis (LDA) to the same Wine dataset and reduce it to two linear discriminants. Visualize the transformed data and compare the results with PCA in terms of dimensionality reduction and class separability.

---

## LDA Methodology

Since the Wine dataset contains three classes, the maximum number of LDA components is:

```text
C - 1 = 3 - 1 = 2
```

Therefore, the dataset is reduced from:

```text
13 features → 2 linear discriminants
```

LDA uses the class labels and focuses on maximizing class separability.

---

## PCA vs LDA – Dimensionality Reduction

| Feature           | PCA               | LDA                         |
| ----------------- | ----------------- | --------------------------- |
| Learning Type     | Unsupervised      | Supervised                  |
| Uses Class Labels | No                | Yes                         |
| Original Features | 13                | 13                          |
| Reduced Features  | 2                 | 2                           |
| Feature Reduction | 84.62%            | 84.62%                      |
| Main Objective    | Maximize variance | Maximize class separability |

Both PCA and LDA reduce the original dataset from 13 features to 2 dimensions.

However, they perform dimensionality reduction for different purposes.

### PCA

PCA identifies directions that capture the maximum variance without considering class labels.

### LDA

LDA uses class labels and identifies directions that maximize separation between different classes.

---

## Class Separability

The Silhouette Score is used to quantitatively compare class separability in the PCA and LDA transformed spaces.

| Method | Reduced Features | Silhouette Score |
| ------ | ---------------: | ---------------: |
| PCA    |                2 |       **0.5262** |
| LDA    |                2 |       **0.6632** |

A higher Silhouette Score indicates better separation between the classes.

In this experiment:

```text
PCA = 0.5262
LDA = 0.6632
```

Therefore, **LDA provides better class separability than PCA** for the Wine dataset.

---

## Overall Observations

### SVM

The Linear SVM classifier achieved excellent classification performance on the Breast Cancer Wisconsin Diagnostic dataset.

The tuned model achieved:

* **98.25% Accuracy**
* **98.61% Precision**
* **98.61% Recall**
* **98.61% F1 Score**

Only two samples were incorrectly classified in the test set.

### PCA

PCA reduced the Wine dataset from 13 features to 2 principal components.

The first two components retained **55.41% of the total variance**, while **10 components** were required to retain at least 95% of the total variance.

### LDA

LDA also reduced the Wine dataset from 13 features to 2 dimensions.

However, LDA provided better class separation than PCA based on the Silhouette Score:

```text
LDA = 0.6632
PCA = 0.5262
```

This demonstrates the difference between PCA's variance-preserving objective and LDA's class-separation objective.

---

# Technologies and Libraries

The experiment was implemented using **Python** and the following libraries:

* NumPy
* Pandas
* Matplotlib
* Scikit-learn
* Jupyter Notebook

### Major Scikit-learn Components

```python
sklearn.datasets
sklearn.preprocessing
sklearn.svm
sklearn.model_selection
sklearn.metrics
sklearn.decomposition
sklearn.discriminant_analysis
```

---

# Requirements

Install the required libraries using:

```bash
pip install numpy pandas matplotlib scikit-learn
```

---

# How to Run

### 1. Open the project in VS Code

Open the project folder in Visual Studio Code.

### 2. Install the dependencies

```bash
pip install numpy pandas matplotlib scikit-learn
```

### 3. Open the Jupyter Notebook

Open:

```text
lab9.ipynb
```

in VS Code.

### 4. Select the Python Kernel

Select the Python environment containing the required libraries.

### 5. Run the Notebook

Run the notebook cells sequentially from top to bottom.

---

# Project Structure

```text
Lab-9/
│
├── lab9.ipynb
└── README.md
```

---

# Key Concepts Demonstrated

* Supervised Learning
* Unsupervised Learning
* Binary Classification
* Support Vector Machine
* Linear Kernel
* Hyperparameter Tuning
* Cross-Validation
* Classification Metrics
* Confusion Matrix
* Feature Standardization
* Principal Component Analysis
* Explained Variance
* Cumulative Explained Variance
* Dimensionality Reduction
* Linear Discriminant Analysis
* Class Separability
* Silhouette Score

---

# Conclusion

This laboratory demonstrated the practical application of Support Vector Machine (SVM), Principal Component Analysis (PCA), and Linear Discriminant Analysis (LDA).

The Linear SVM achieved high classification performance on the Breast Cancer Wisconsin Diagnostic dataset after feature standardization and hyperparameter tuning.

PCA successfully reduced the Wine dataset from 13 features to 2 principal components for visualization while retaining 55.41% of the total variance. Further analysis showed that 10 components were required to retain at least 95% of the variance.

LDA provided the same two-dimensional reduction as PCA but achieved better class separability based on the Silhouette Score.

Overall, the experiment demonstrates the practical applications of **SVM for supervised classification, PCA for dimensionality reduction and variance preservation, and LDA for supervised dimensionality reduction and class separability analysis**.
