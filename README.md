# Fire Event Priority Prediction for India Using Ensemble Machine Learning

## ML for Social Good – Mission Earth

---

## Problem Statement

India experiences numerous satellite-detected fire and thermal events. Monitoring all detected events with the same level of urgency can make prioritisation difficult.

This project develops an ensemble machine learning system to classify satellite-detected fire events into:

- **Routine Priority**
- **High Priority**

The objective is to support environmental monitoring and response personnel by helping prioritise events for further investigation.

---

## Why Machine Learning?

Machine learning is suitable for this problem because the dataset contains a large number of historical satellite observations with multiple numerical, categorical, temporal, and geographical features. The relationship between these features and the constructed priority class can be complex and non-linear.

Ensemble machine learning models can learn patterns from historical observations and provide consistent predictions for new satellite-detected events. The system is designed to support human prioritisation and does not replace expert judgement or emergency-response decisions.

---

## Intended Beneficiaries

The proposed system can support:

- Environmental monitoring agencies
- Forest and wildlife authorities
- Disaster-response personnel
- Researchers analysing fire activity

The model is intended as a **decision-support system** and not as a fully autonomous emergency-response system.

---

## Measurable Impact

The proposed system aims to support faster prioritisation of large numbers of satellite-detected fire events.

Its machine learning performance is evaluated using:

- ROC-AUC
- F1-score
- Precision
- Recall
- Confusion Matrix

A particularly important measure is the model's ability to correctly identify events labelled as High Priority.

In a real operational setting, the potential impact could be measured by the proportion of High-Priority events correctly identified and the reduction in time required to prioritise large numbers of events for human review.

---

## Dataset

The project uses satellite fire-event observations for India obtained from **NASA FIRMS / MODIS data**.

Each row represents **one satellite-detected thermal event**.

The dataset contains features including:

- Latitude
- Longitude
- Brightness
- Scan
- Track
- Acquisition date
- Acquisition time
- Satellite
- Detection confidence
- Brightness temperature
- Day/Night information
- Fire Radiative Power (FRP)

### Dataset Citation

NASA FIRMS – Fire Information for Resource Management System. Satellite-derived active fire and thermal anomaly observations.

**Dataset source:https://www.kaggle.com/datasets/sherkhan15/indian-wildfire-nasa-dataset-8-years

**Unit of analysis:** One row represents one satellite-detected thermal event.

---

## Dataset Size

- **Records:** 644,255
- **Original Features:** 15

---

## Target Variable

The target variable is:

`high_priority`

- `0` = Routine Priority
- `1` = High Priority

The High-Priority label was created using a Fire Radiative Power (FRP) threshold.

FRP was used to construct the target but was excluded from the model input features to prevent target leakage.

The final target distribution was approximately:

- **Routine Priority:** 74.99%
- **High Priority:** 25.01%

---

## Data Preprocessing

The following data quality checks and preprocessing steps were performed.

### Missing Values

All original variables were audited for missing and NaN values.

No missing values were found in the dataset. Therefore, no imputation or row deletion was required.

Any NaN values visible in the combined statistical summary represented statistics that were not applicable to particular data types and were not missing observations in the original dataset.

### Duplicate Records

The dataset was checked for exact duplicate rows.

- **Duplicate rows found:** 0

Therefore, no records were removed due to duplication.

### Invalid Values

Checks were performed for:

- Invalid latitude values
- Invalid longitude values
- Negative brightness
- Negative scan
- Negative track
- Negative confidence
- Negative Brightness Temperature
- Negative FRP

No invalid values were found in the checks performed.

### Outliers

FRP showed a highly right-skewed distribution.

Extreme FRP values were not blindly removed because unusually large FRP observations may represent meaningful high-intensity fire events rather than data errors.

A logarithmic transformation was used for exploratory visualisation of the FRP distribution.

### Feature Engineering

Temporal features were engineered from acquisition date and time.

Categorical features were encoded using one-hot encoding.

Numerical features were scaled within the machine learning preprocessing pipeline using `RobustScaler`.

---

## Leakage Prevention

A leakage-safe machine learning workflow was used.

The data was split into training, validation, and test sets.

Preprocessing transformations were fitted using the training data and then applied consistently to validation and test data.

The final test set remained untouched during model selection and hyperparameter tuning.

Since FRP was used to derive the target variable, it was excluded from the predictor variables. Including FRP as an input feature would allow the model to directly learn the rule used to construct the target, resulting in target leakage and artificially inflated performance.

---

## Class Imbalance

The final target distribution contained approximately:

- 74.99% Routine-Priority events
- 25.01% High-Priority events

The imbalance was considered during model development using stratified splitting and class-aware modelling where applicable.

---

## Models

The following models were implemented and compared.

### Baseline Model

- Decision Tree Classifier

### Bagging Ensemble

- Random Forest Classifier

### Boosting Ensemble

- AdaBoost Classifier

### Heterogeneous Ensemble

- Stacking Ensemble

Hyperparameter tuning and cross-validation were used during model development.

The stacking approach used heterogeneous base models with a separate meta-model and cross-validation to reduce the risk of information leakage during meta-learning.

---

## Model Evaluation

Models were evaluated using:

- ROC-AUC
- F1-score
- Precision
- Recall
- Confusion Matrix
- ROC Curve

All final model comparisons were performed using the same untouched test set.

---

## Best Model

The **Tuned Random Forest** was selected as the final model based on validation performance.

### Final Test Performance

| Model | ROC-AUC | F1 | Precision | Recall |
|---|---:|---:|---:|---:|
| Decision Tree Baseline | 0.932007 | 0.900422 | 0.906239 | 0.894679 |
| Random Forest (Tuned) | 0.994797 | 0.931307 | 0.922627 | 0.940151 |

The Tuned Random Forest outperformed the Decision Tree baseline on the final untouched test set.

Its ROC-AUC increased from **0.932007** to **0.994797**, while its F1-score increased from **0.900422** to **0.931307**.

The Random Forest also achieved higher recall, improving from **0.894679** to **0.940151**. This means it correctly identified a larger proportion of events labelled as High Priority.

The Tuned Random Forest was therefore selected as the final model.

However, this prediction represents an operational priority classification based on the constructed target and historical satellite observations. It should not be interpreted as an autonomous determination of real-world emergency severity.

---

## Explainability

SHAP was used to explain the behaviour of the final Random Forest model at both:

- **Global level:** Overall feature influence across observations
- **Local level:** Feature contributions to an individual prediction

### Global Explanation

The most influential features included:

1. Brightness
2. Detection Confidence
3. Scan
4. Track

Brightness had the highest overall influence on model predictions. This indicates that the strength of the detected thermal signal was highly important when the model differentiated between Routine-Priority and High-Priority events.

Detection Confidence was also a major contributor. This feature provides information related to the reliability of the detected satellite thermal anomaly and therefore influenced the model's prioritisation decision.

Scan and Track were also influential and describe characteristics related to the satellite observation.

SHAP values explain how the trained model uses the input features. They do not prove that an individual feature physically causes a fire event to become more severe or dangerous.

### Local Explanation

A realistic synthetic fire-event record was passed through the final trained pipeline for a live demonstration.

The model predicted:

- **Prediction:** HIGH PRIORITY
- **Probability of High Priority:** 99.40%

For this prediction, Brightness made the strongest positive contribution toward the High-Priority classification, followed by Detection Confidence.

Some features made comparatively small negative contributions, but these were not sufficient to offset the strong positive evidence.

The local explanation represents the reasoning of the trained machine learning model for this specific input. It should not be interpreted as proof of physical causation.

---

## Ethics and Responsible Use

### Bias and Fairness

Satellite detection quality may vary across geographic regions, environmental conditions, satellite overpass times, and other factors. Model performance should therefore be evaluated across different regions and conditions before operational deployment.

### Privacy

The dataset does not contain directly identifiable personal information.

### Uncertainty

Predicted probabilities represent model estimates and should not be interpreted as certainty.

### False Positives

A false positive may result in unnecessary allocation of monitoring or response resources.

### False Negatives

A false negative may delay attention to an event that may require further investigation.

### Human Oversight

The system should be used as a decision-support tool. Predictions should be verified using additional information, such as local conditions, weather, ground observations, and other reliable sources.

### Deployment Limitations

The model was trained using historical satellite observations from India. Performance may differ for other locations, sensors, environmental conditions, or future fire patterns.

The High-Priority label is an operational proxy based on an FRP threshold rather than an official emergency classification.

The system should not be used as a fully autonomous emergency-response decision-maker.

---

## Installation

Install the required Python libraries:

```bash
pip install pandas numpy matplotlib scikit-learn shap joblib
