# 🎾 Play Tennis Classification using Machine Learning

A machine learning project that predicts whether a person will **play tennis** based on weather conditions using the **Play Tennis** dataset. The project implements multiple classification algorithms and compares their performance using standard evaluation metrics.

---

## 🚀 Features

- 📂 Load and preprocess the Play Tennis dataset
- 🔄 Encode categorical features using **Label Encoding**
- 📊 Split the dataset into **80% training** and **20% testing**
- 🤖 Train a **Categorical Naive Bayes** classifier
- 📈 Evaluate model performance using:
  - Accuracy
  - Confusion Matrix
  - Classification Report
- 🎯 Predict a custom weather instance
- 📉 Display prediction probabilities
- ⚖️ Compare the performance of:
  - Categorical Naive Bayes
  - Decision Tree
  - Logistic Regression
  - Support Vector Machine (SVM)

---

## 📁 Project Structure

```
Play-Tennis-Classification/
│── play_tennis.csv
│── Lab8.ipynb
```

---

## 📊 Dataset

The dataset contains weather conditions used to predict whether tennis will be played.

| Feature | Values |
|---------|--------|
| Outlook | Sunny, Overcast, Rain |
| Temperature | Hot, Mild, Cool |
| Humidity | High, Normal |
| Wind | Weak, Strong |
| Play (Target) | Yes / No |

---

## 🛠️ Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Jupyter Notebook

---

## 📦 Installation

Clone the repository:



Install the required packages:


---

## ▶️ Running the Project

### Using Jupyter Notebook

```bash
jupyter notebook Lab8.ipynb
```

### Using Python

```bash
python Lab8.py
```

---

## 📈 Models Implemented

| Model | Purpose |
|------|---------|
| Categorical Naive Bayes | Main classification model |
| Decision Tree | Performance comparison |
| Logistic Regression | Performance comparison |
| Support Vector Machine | Performance comparison |

---

## 📊 Evaluation Metrics

The models are evaluated using:

- Accuracy Score
- Confusion Matrix
- Precision
- Recall
- F1-Score
- Prediction Probabilities

---

## 🎯 Sample Prediction

**Input**

| Feature | Value |
|---------|-------|
| Outlook | Sunny |
| Temperature | Cool |
| Humidity | High |
| Wind | Strong |

The notebook predicts:

- ✅ Whether the person will play tennis
- 📊 Probability of each class

---

## 📷 Sample Output

The notebook generates:

- Encoded Dataset
- Model Accuracy
- Confusion Matrix
- Classification Report
- Single Sample Prediction
- Prediction Probabilities
- Model Comparison Table

---

## 📚 Learning Outcomes

This project demonstrates:

- Data preprocessing
- Label Encoding
- Supervised Machine Learning
- Model Evaluation
- Probability Prediction
- Comparison of Classification Algorithms

---

## 📌 Future Improvements

- Perform hyperparameter tuning
- Use cross-validation
- Visualize the confusion matrix
- Add ROC and Precision-Recall curves
- Experiment with larger datasets

---



**Albin Thomas**

MCA Student | CHRIST (Deemed to be University)

---
