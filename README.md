 💳 Credit Card Fraud Detection System

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Machine%20Learning-orange)
![XGBoost](https://img.shields.io/badge/XGBoost-Gradient%20Boosting-red)
![Imbalanced-Learn](https://img.shields.io/badge/Imbalanced--Learn-SMOTE-green)

A comprehensive Machine Learning project analyzing **284,807 credit card transactions** to detect fraudulent activity in real-time. This project tackles the challenge of **extreme class imbalance** using **SMOTE** and delivers a robust detection system with **high recall** and **low false alarms**.

---

## 📖 Project Overview

Credit card fraud is a "needle in a haystack" problem where fraudulent transactions are rare (**0.17%**) but financially devastating. This project aims to:

1. **Analyze** transaction patterns to visualize how fraud differs from normal spending using **PCA & t-SNE**.
2. **Handle Imbalance** using **SMOTE** (Synthetic Minority Over-sampling Technique) to prevent model bias.
3. **Train** ensemble classifiers (**Random Forest, XGBoost**) to distinguish fraud from legitimate transactions.
4. **Recommend** risk thresholds for banking systems to minimize customer friction while stopping theft.

### 🔑 Key Insights

- **The 0.17% Challenge:** The dataset is highly skewed. Without intervention (SMOTE), models would predict "Safe" 100% of the time and miss every fraud.
- **Hidden Patterns:** Dimensionality reduction (t-SNE) revealed that while fraud looks random, it actually forms distinct clusters in high-dimensional space.
- **Model Trade-off:** **Logistic Regression** caught the most fraud but flagged too many innocent people. **Random Forest** offered the best "Real-World" performance by virtually eliminating false alarms.

---

## 🛠️ Tech Stack

- **Data Engineering:** Python, Pandas, NumPy
- **Visualization:** Matplotlib, Seaborn (Correlation Heatmaps), Scikit-learn (PCA/t-SNE)
- **Machine Learning:**
  - **Imbalanced-learn:** SMOTE (Synthetic Minority Over-sampling)
  - **Ensemble Models:** Random Forest, XGBoost (for high precision)
  - **Base Model:** Logistic Regression (for baseline comparison)

---

## 📂 Project Structure

```bash
CreditCardFraudDetection/
│
├── src/
│   ├── data_loader.py      # Pipeline: Loads data, scales features, applies SMOTE
│   ├── visualization.py    # Reports: Generates Correlation Heatmap, PCA & t-SNE plots
│   └── model.py            # ML Core: Trains Logistic Regression, RF, and XGBoost
│
├── main.py                 # Entry Point: Runs the full analysis pipeline
├── requirements.txt        # Project Dependencies
├── README.md               # Documentation & Risk Analysis Report
│
└── (Generated Output)
    ├── data/creditcard.csv # The Dataset (Kaggle)
    ├── Figure_1.png        # Class Distribution (Imbalance)
    ├── Figure_2.png        # Feature Correlation Matrix
    └── Figure_3.png        # t-SNE Fraud Clusters
```

---

## 🚀 Installation & Usage

### 1️⃣ Clone & Install Dependencies

```bash
git clone https://github.com/xx-devvv/Credit-Card-Fraud-Detection.git
cd CreditCardFraudDetection
pip install -r requirements.txt
```

### 2️⃣ Setup Data

- Download the dataset from **Kaggle** (https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)
- Place `creditcard.csv` inside the `data/` folder

### 3️⃣ Run Analysis & Training

This single command runs the entire pipeline (**EDA → SMOTE → Training → Evaluation**):

```bash
python main.py
```

---

## 📊 Model Evaluation Results

| Model | Recall (Fraud Capture) | False Alarms (False Positives) | Strength |
|------|--------------------------|--------------------------------|----------|
| Logistic Regression | 92% (High) | ~1,458 (High) | Good at catching fraud, but annoys too many genuine customers. |
| Random Forest | 90% (Balanced) | ~15 (Very Low) | **Champion Model.** Excellent precision; only stops a card when it's truly suspicious. |
| XGBoost | 91% (High) | Low | Powerful gradient boosting alternative with high accuracy. |

**Technical Note:** We prioritized **Random Forest** for the final recommendation because in a banking environment, blocking **1,400+ innocent users** (as Logistic Regression did) causes significant reputation damage.

---

## 📢 Risk Management & Banking Recommendations

Based on our predictive analysis and confusion matrices, we recommend the following deployment strategies:

### 🏛️ Banking Policy

✅ **Tiered Response System**
- **Score > 90% (Red Zone):** Immediate auto-block of the transaction (**Powered by Random Forest**)
- **Score 50–89% (Yellow Zone):** Trigger Step-Up Authentication (**SMS OTP / App Verification**) instead of blocking

✅ **Dynamic Thresholding**
- Adjust the fraud threshold during peak shopping seasons (e.g., **Black Friday**) to reduce false positives when transaction volume spikes.

---

### 🛡️ Security Operations

✅ **Feature Monitoring**
- Correlation analysis showed that **V14, V17, and V12** are the strongest indicators of fraud.
- Security teams should prioritize monitoring these vectors in raw logs.

✅ **Continuous Retraining**
- The t-SNE clusters indicate evolving fraud patterns.
- The model should be retrained **weekly** with new fraud labels to detect novel attack vectors.

---
