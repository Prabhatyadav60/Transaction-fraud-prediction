# 💳 Fraud Detection Model

## 📌 Objective

The goal of this project is to develop a machine learning model that predicts fraudulent financial transactions and provides actionable insights for a financial company. The dataset includes over 6 million transactions with various features related to the source and destination of funds.
- `Fraud.csv` – Original dataset (drive-link- https://drive.google.com/file/d/1XKULmZMzUYDCHMI4HxTOtOD2U1b9Lr6g/view?usp=sharing ).
## 📂 Data Overview

- **Dataset Shape:** (6,362,620 rows × 11 columns)  
- **Target Variable:** `isFraud` (1 = Fraudulent, 0 = Legitimate)  
- **Key Features:** `step`, `type`, `amount`, `oldbalanceOrg`, `newbalanceOrig`, `oldbalanceDest`, `newbalanceDest`, `isFraud`, `isFlaggedFraud`

## ⚙️ Feature Engineering

The categorical `type` feature was encoded to create a new feature called `type_enc`. The final features used in the model were: `step`, `amount`, `oldbalanceOrg`, `newbalanceOrig`, `oldbalanceDest`, `newbalanceDest`, and `type_enc`.

**Multicollinearity Analysis (VIF values):**

- step: 1.44  
- amount: 1.73  
- oldbalanceOrg: 284.92  
- newbalanceOrig: 285.58  
- oldbalanceDest: 9.24  
- newbalanceDest: 10.46  

⚠️ Very high VIF values for `oldbalanceOrg` and `newbalanceOrig` indicate potential multicollinearity between these features.

## 🧪 Model Training and Evaluation

Two models were trained and evaluated: Logistic Regression and Random Forest Classifier.

### 🔹 Logistic Regression

- **Accuracy:** 99.86%  
- **Confusion Matrix:**  
  [[16831     0]  
   [   24     6]]  
- **Classification Report:**  
  - Fraud Precision: 1.00  
  - Fraud Recall: 0.20  
  - Fraud F1-score: 0.33  

**Insight:** Despite high overall accuracy, Logistic Regression shows poor recall for fraud detection (only 20%), which is a major concern in fraud use-cases where false negatives are highly undesirable.

### 🔹 Random Forest Classifier

- **Best Hyperparameters:** `max_depth=10`, `min_samples_split=2`, `n_estimators=200`  
- **Accuracy:** 99.89%  
- **ROC AUC Score:** 0.9903  
- **Confusion Matrix:**  
  [[16830     1]  
   [   17    13]]  
- **Classification Report:**  
  - Fraud Precision: 0.93  
  - Fraud Recall: 0.43  
  - Fraud F1-score: 0.59  

**Insight:** Random Forest outperforms Logistic Regression by a large margin in terms of fraud detection recall, F1-score, and AUC score, making it more suitable for deployment.

## 🔍 Insights and Recommendations

- Random Forest is the preferred model for deployment due to its superior recall and AUC performance.  
- Despite class imbalance, the model achieved high fraud detection capability with a ROC AUC above 0.99 and a fraud F1-score of 0.59.  
- The overall accuracy remains high while improving the capture of fraudulent cases.

### ✅ Action Plan

1. **Deploy the Random Forest model** in production for real-time fraud detection.  
2. **Explore resampling techniques** (e.g., SMOTE or undersampling) to further improve recall on minority fraud class.  
3. **Use SHAP values** (already integrated in the notebook) to explain individual predictions and ensure transparency for compliance and trust.  
4. **Continuously monitor false positives** to ensure the customer experience is not negatively impacted by false fraud flags.  
5. **Review multicollinearity** and potentially drop or combine highly correlated features for model stability.

## 📁 Files Included

- `fraud-detection-model.ipynb` – Notebook containing the full code, preprocessing, modeling, evaluation, and interpretability tools.  
- `README.md` – Project documentation (this file).  
  

## 🧠 Future Work

- Set up an API endpoint (e.g., with Flask or FastAPI) to serve real-time predictions.  
- Add more behavioral and time-series features to improve fraud capture.  
- Perform hyperparameter tuning with grid search or Bayesian optimization for further gains.  
- Integrate alert mechanisms or dashboards to visualize fraud detection in real-time.


