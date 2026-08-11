# Lab 9 – SVM, PCA and LDA

## Machine Learning Lab

This laboratory experiment demonstrates the application of **Support Vector Machine (SVM)** for supervised classification and **Principal Component Analysis (PCA)** for dimensionality reduction. An additional **Linear Discriminant Analysis (LDA)** experiment is performed to compare supervised and unsupervised dimensionality reduction techniques.

---

## Aim

To implement Support Vector Machine (SVM) for classification and Principal Component Analysis (PCA) for dimensionality reduction, and analyse their effectiveness using real-world datasets.

---

## Objectives

- To implement and evaluate the performance of the Support Vector Machine (SVM) classifier.
- To perform hyperparameter tuning for an SVM classifier.
- To evaluate SVM using standard classification metrics.
- To apply PCA for dimensionality reduction.
- To analyse the variance retained by principal components.
- To visualize the PCA-transformed feature space.
- To determine the minimum number of components required to retain at least 95% variance.
- To compare PCA and LDA in terms of dimensionality reduction and class separability.
- To understand the difference between supervised and unsupervised learning techniques.

---

# Part A – Support Vector Machine (SVM)

## Dataset

### UCI Breast Cancer Wisconsin (Diagnostic) Dataset

The Breast Cancer Wisconsin (Diagnostic) dataset is used for binary classification.

**Dataset:**  
https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic

### Dataset Characteristics

- Samples: **569**
- Features: **30**
- Classes: **2**
- Classification Type: **Binary Classification**
- Target Classes:
  - Malignant
  - Benign

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
   - Accuracy
   - Precision
   - Recall
   - F1 Score
   - Confusion Matrix
8. Summarize the model performance.

---

## SVM Methodology

The SVM implementation follows these steps:

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
