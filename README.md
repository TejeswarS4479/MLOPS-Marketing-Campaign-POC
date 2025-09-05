# Bank Marketing Campaign Response Prediction

## 📌 Project Overview
This project aims to build a **binary classification machine learning model** to predict whether a customer will **subscribe to a term deposit** following a direct marketing phone campaign.

By identifying likely responders, the bank can:
- Reduce **call center costs**
- Improve **conversion rates**
- Optimize **marketing resources**
- Increase **campaign ROI (Return on Investment)**

---

## 📝 Problem Statement
A Portuguese bank runs direct marketing campaigns via phone calls, achieving only **11% success rate**.  
The marketing team needs a predictive model to **improve campaign efficiency by 50%**, while **maintaining or increasing total subscriptions**.

Our goal is to:
- Predict customer response (`yes` or `no`)
- Prioritize high-likelihood customers for targeting
- Deliver actionable insights to marketing teams

---

## 📊 Dataset
- **Source:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/222/bank+marketing)
- **Size:** ~45,000 rows, 20+ features
- **Target Variable:** `y` → whether the customer subscribed (`yes`) or not (`no`)

### Dataset Files in Repo
| File Name     | Purpose |
|---------------|---------|
| `data/bank-full.csv` | Main dataset used for model training/testing |
| `data/bank.csv` | Smaller dataset for **batch scoring** demonstration |

### Key Features
- **Demographics:** Age, job, marital status, education  
- **Financial:** Balance, housing loan, personal loan  
- **Campaign Details:** Number of calls, previous contacts, outcome of previous campaign  
- **Contextual:** Month, day of week, social/economic indicators

---

## 🎯 Performance Targets
| Metric      | Goal |
|-------------|------|
| **Precision** | > 40% (at least 4x better than random targeting if baseline is 10%) |
| **Recall** | Balanced with marketing capacity and revenue capture |
| **AUC-ROC** | > 0.75 |

> *These targets will be fine-tuned after exploratory data analysis and initial model runs.*

---

## ⚙️ Project Workflow

### Steps:
1. **Data Ingestion**
   - Load and inspect dataset
   - Check for class imbalance
2. **Data Preprocessing**
   - Handle categorical and numeric features
   - Scaling numeric features with `StandardScaler`
   - One-hot encoding categorical features
3. **Train/Test Split**
   - 80/20 split using stratification
4. **Baseline Model: Logistic Regression**
   - Implemented with `Pipeline`
   - Threshold tuning for optimal precision-recall trade-off
5. **Batch Scoring**
   - Demonstrate prediction on a separate batch file (`bank.csv`)
6. **Advanced Model: LightGBM + SMOTE**
   - Handle severe class imbalance
   - Find threshold that maintains recall ≥ 0.70
7. **Model Evaluation**
   - Confusion Matrix
   - Precision/Recall curves
   - ROC AUC
8. **Business Validation**
   - Link metrics to business impact

---


---

## 🛠️ Tools & Technologies

| Area            | Tools Used |
|-----------------|------------|
| **Data Engineering** | Pandas, NumPy |
| **Machine Learning** | Scikit-learn, LightGBM, SMOTE (Imbalanced-learn) |
| **Visualization** | Seaborn, Matplotlib |
| **Deployment (future scope)** | SageMaker or Databricks |
| **Version Control** | Git, GitHub |

---

## 🐍 Installation & Setup

### 1. Clone the Repository
```bash
git clone https://github.com/TejeswarS4479/MLOPS-Marketing-Campaign-POC.git
cd MLOPS-Marketing-Campaign-POC

