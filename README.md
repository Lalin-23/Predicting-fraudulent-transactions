# 🔍 Fraud Detection Using Machine Learning (PaySim Dataset)

## 📌 Overview
This repository contains an **end-to-end machine learning solution** for detecting fraudulent financial transactions using the **PaySim dataset**.  
The project demonstrates **data cleaning, feature engineering, model development, evaluation, and business-driven fraud prevention strategies**.

The solution is designed to mirror **real-world fraud detection challenges**, including extreme class imbalance and time-dependent transaction behavior.

---

## 📊 Dataset
- **Dataset:** PaySim (Simulated Financial Transactions)
- **Rows:** 6,362,620
- **Time Span:** 30 days (1 step = 1 hour, total 744 steps)

### Key Columns
| Column | Description |
|------|------------|
| `type` | Transaction type (TRANSFER, CASH_OUT, PAYMENT, etc.) |
| `amount` | Transaction amount |
| `oldbalanceOrg`, `newbalanceOrig` | Sender balances |
| `oldbalanceDest`, `newbalanceDest` | Receiver balances |
| `isFraud` | Target variable (1 = Fraud, 0 = Legitimate) |
| `isFlaggedFraud` | Existing rule-based fraud flag (used only for comparison) |

---

## 🧹 Data Cleaning
- Verified **no missing values**
- Outliers in monetary variables capped at the **99.9th percentile**
- Multicollinearity assessed using **VIF**
  - High/infinite VIF values observed due to deterministic balance relationships
  - No features removed, as **tree-based models are robust to multicollinearity**

---

## 🧠 Feature Engineering
- Balance change and balance error indicators
- Merchant vs non-merchant transaction flag
- Hour-of-day feature derived from transaction time
- One-hot encoding of transaction types

These features capture known fraud behaviors such as **TRANSFER → CASH_OUT sequences** and **balance inconsistencies**.

---

## ⚖️ Class Imbalance Handling
- Fraud rate ≈ **0.13%**
- Applied **SMOTE** on training data only (fraud ≈ 5%)
- Validation data retained original class distribution

---

## 🤖 Model
- **Algorithm:** XGBoost Classifier
- **Why XGBoost?**
  - Handles large-scale data efficiently
  - Robust to multicollinearity
  - Captures non-linear fraud patterns
  - Performs well on highly imbalanced datasets

- **Train–Validation Strategy:**  
  Time-based split using transaction steps to prevent data leakage

---

## 📈 Model Evaluation
Accuracy is not used due to class imbalance.

### Metrics Used
- ROC-AUC
- Precision, Recall, F1-score
- Probability distribution analysis

**Result:**  
- ROC-AUC ≈ **0.99**
- Strong separation between fraudulent and legitimate transactions

---

## 🔑 Key Fraud Indicators
- High transaction amounts
- Balance inconsistencies
- TRANSFER and CASH_OUT transaction types
- Zero or abnormal destination balances
- Unusual transaction timing

These indicators align with real-world financial fraud behavior.

---

## 🛡️ Fraud Prevention Strategy
- Replace static rules with **ML-based dynamic risk scoring**
- Monitor **TRANSFER → CASH_OUT** transaction chains
- Apply probability-based thresholds
- Tiered response system:
  - Low risk → Auto-approve
  - Medium risk → Friction (OTP, delay)
  - High risk → Block or manual review

---

## 📏 Measuring Effectiveness
Post-deployment effectiveness can be measured using:
- Reduction in fraud losses
- Recall of confirmed fraud cases
- False positive rate
- Manual review workload
- A/B testing against rule-based systems

---

## 📁 Repository Structure
