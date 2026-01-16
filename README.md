Fraud Detection Using Machine Learning (PaySim Dataset)
📌 Project Overview

This project focuses on building a machine learning–based fraud detection system for a financial company using a large-scale transactional dataset (PaySim). The goal is to accurately identify fraudulent transactions and propose actionable business strategies based on model insights.

The dataset contains 6.3 million transactions over 30 days, simulated to reflect real-world financial fraud patterns.

📂 Dataset Description

Rows: 6,362,620

Columns: 10 (original) + engineered features

Time Unit: step (1 step = 1 hour, total 744 steps)

Key Columns

type: Transaction type (PAYMENT, TRANSFER, CASH_OUT, etc.)

amount: Transaction amount

oldbalanceOrg, newbalanceOrig: Sender balances

oldbalanceDest, newbalanceDest: Receiver balances

isFraud: Target variable (1 = Fraud, 0 = Legitimate)

isFlaggedFraud: Existing rule-based flag (used only for comparison)

🧹 1. Data Cleaning

Missing Values: None found in the dataset

Outliers: Monetary variables capped at the 99.9th percentile

Multicollinearity:

Diagnosed using VIF

High/infinite VIF values observed due to deterministic balance relationships

No features removed, as tree-based models are robust to multicollinearity

🧠 2. Feature Engineering

To capture fraud behavior effectively, the following features were engineered:

Balance change and balance error features

Merchant vs non-merchant flag

Hour-of-day feature from transaction time

One-hot encoding of transaction types

These features are strongly aligned with known fraud patterns such as TRANSFER → CASH_OUT sequences and balance inconsistencies.

⚖️ 3. Class Imbalance Handling

Fraud rate ≈ 0.13%

Applied SMOTE on training data only to raise fraud proportion to ~5%

Validation data kept at original distribution to reflect real-world conditions

🤖 4. Model Description

Model Used: XGBoost Classifier

Why XGBoost?

Handles large datasets efficiently

Captures non-linear patterns

Robust to multicollinearity

Performs well on imbalanced data

Train–Validation Split:

Time-based split using step

Prevents data leakage

📊 5. Model Performance Evaluation

Due to extreme class imbalance, accuracy was not used as the primary metric.

Metrics Used:

ROC-AUC

Precision, Recall, F1-score

Probability distribution analysis

Result:

ROC-AUC ≈ 0.99

High recall with controlled false positives

The probability distribution shows strong separation between fraud and non-fraud cases.

🔍 6. Key Fraud Predictors

Top indicators of fraud include:

Transaction amount

Balance inconsistencies

TRANSFER and CASH_OUT transaction types

Zero or abnormal destination balances

Unusual transaction timing

These factors align well with real-world financial fraud behavior.

🛡️ 7. Fraud Prevention Strategy

Based on model insights, the following actions are recommended:

Replace static rules with ML-based risk scoring

Monitor and restrict TRANSFER → CASH_OUT chains

Use dynamic probability thresholds

Apply tiered actions:

Low risk → auto-approve

Medium risk → friction (OTP, delay)

High risk → block or manual review

📈 8. Measuring Effectiveness

Post-deployment effectiveness can be measured using:

Reduction in fraud losses

Recall of confirmed fraud cases

False positive rate

Manual review workload

A/B testing against rule-based systems

Continuous monitoring ensures adaptability to evolving fraud patterns.

📁 Project Files

Fraud.ipynb – Complete Jupyter Notebook (code + analysis)

Fraud.csv – Dataset

README.md – Project documentation

✅ Conclusion

This project demonstrates an end-to-end fraud detection pipeline combining data cleaning, feature engineering, machine learning, and business judgment. The solution effectively improves upon traditional rule-based systems and provides a scalable framework for real-world deployment.
