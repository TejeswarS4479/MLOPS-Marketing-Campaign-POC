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

This repository demonstrates a complete **end-to-end machine learning workflow** for the classic **Bank Marketing dataset**, built on **Databricks** with **MLflow** integration.  
It covers:

- Data ingestion and preprocessing
- Model training using:
  - Logistic Regression
  - LightGBM with **SMOTE** for class imbalance
- Experiment tracking with **MLflow**
- Model registration and versioning
- Real-time deployment with **Databricks Model Serving**
- REST API consumption for predictions

---

## Table of Contents
1. [Project Overview](#project-overview)  
2. [Architecture](#architecture)  
3. [Technologies Used](#technologies-used)  
4. [Dataset](#dataset)  
5. [Setup Instructions](#setup-instructions)  
6. [Steps Performed](#steps-performed)  
    - [A. Notebook Steps](#a-notebook-steps)
    - [B. Databricks Steps Outside the Notebook](#b-databricks-steps-outside-the-notebook)
7. [REST API Endpoint](#rest-api-endpoint)  
8. [Folder Structure](#folder-structure)  
9. [Future Enhancements](#future-enhancements)

---

## Architecture

```
+--------------------+
|  Raw Bank Data     |
| (bank-full.csv)    |
+---------+----------+
          |
          v
+--------------------+
|  Databricks Notebook |
|  - Data Preprocessing |
|  - Logistic Regression |
|  - LightGBM + SMOTE    |
+---------+----------+
          |
          v
+-----------------------+
| MLflow Experiment Tracking |
+---------+-----------------+
          |
          v
+-----------------------+
| MLflow Model Registry |
+---------+-------------+
          |
          v
+-----------------------+
| Databricks Model Serving |
+---------+-------------+
          |
          v
+-----------------------+
| REST API Consumer (Python) |
+---------------------------+
```

---

## Technologies Used

| Component            | Technology Used           |
|---------------------|---------------------------|
| Data Processing      | Pandas, NumPy, Scikit-learn |
| Visualization        | Matplotlib, Seaborn       |
| Modeling             | Logistic Regression, LightGBM |
| Imbalance Handling   | SMOTE (Imbalanced-learn)  |
| Experiment Tracking  | MLflow                     |
| Deployment           | Databricks Model Serving   |
| Pipeline Orchestration | Databricks Runtime ML   |
| API Requests         | Python Requests Library   |

---

## Dataset

The project uses the **Bank Marketing dataset**, which contains information on customers and past marketing campaigns.

- **Source:** UCI Machine Learning Repository  
- **Target Variable:** `y`  
  - `yes` → customer subscribed  
  - `no` → customer did not subscribe

Key features include:
- **Demographics:** age, marital status, education  
- **Financial Info:** balance, housing loan, personal loan  
- **Campaign Info:** contact method, previous outcome, campaign duration  

---

## Setup Instructions

### Prerequisites
- Databricks workspace with **Databricks Runtime ML**
- Python 3.10+
- Access to MLflow Model Registry
- Personal Access Token for Databricks REST API

---

### 1. Clone the Repository
```bash
git clone https://github.com/<your-username>/bank-marketing-ml-pipeline.git
cd bank-marketing-ml-pipeline
```

---

### 2. Install Required Packages
Install dependencies locally (for running outside Databricks):

```bash
pip install -r requirements.txt
```

Typical dependencies:
```text
pandas
numpy
scikit-learn
matplotlib
seaborn
lightgbm
imbalanced-learn
mlflow>=3.0
```

---

### 3. Import Notebook into Databricks (Optional - If the notebook exists outside of Databricks)
- Go to Databricks → Workspace → Import  
- Upload the provided notebook:  
  `bank_marketing_ml_workflow.ipynb`

---

## Steps Performed

### A. Notebook Steps

The notebook walks through:

1. **Data Loading**
   - Load `bank-full.csv` from Databricks Volumes. Refer to this [link.](https://docs.databricks.com/gcp/en/volumes/utility-commands)

2. **Data Preprocessing**
   - Identify categorical and numeric columns.
   - Apply:
     - `StandardScaler` → numeric features
     - `OneHotEncoder` → categorical features

3. **Handling Imbalanced Data**
   - Explore target class imbalance.
   - Use **SMOTE** for balancing in LightGBM.

4. **Model Training**
   - Logistic Regression pipeline
   - LightGBM + SMOTE for improved recall and precision

5. **Metrics Evaluation**
   - Precision, Recall, F1 Score, ROC AUC
   - Confusion matrix and threshold tuning

6. **Experiment Tracking with MLflow**
   - Log:
     - Parameters
     - Metrics
     - Artifacts (plots, model files)

7. **Model Registration**
   - Register best model (`LightGBM + SMOTE`) into MLflow Model Registry.

8. **Batch Scoring**
   - Perform scoring on another dataset (`bank.csv`).

---

### B. Databricks Steps Outside the Notebook

These steps are performed directly in the Databricks UI or CLI:

1. **Create MLflow Experiment**
   - Navigate to **Experiments → Create**.
   - Path used:  
     ```
     /Users/tejeswar.seerapu@modak.com/bank_marketing_experiment
     ```

2. **Create Model Serving Endpoint**
   - Go to **Serving → Create Endpoint**.
   - Select registered model: `bank_marketing_model_registry`.
   - Configure:
     - Cluster size
     - Scaling policy
   - Deploy to production.

3. **Set Model Alias**
   ```python
   from mlflow.tracking import MlflowClient

   client = MlflowClient()
   client.set_registered_model_alias(
       name="workspace.default.bank_marketing_model_registry",
       alias="prod",
       version=1
   )
   ```
   If you don’t use aliases, you need to refer to the model by version number every time.
      ```
         mlflow.pyfunc.load_model("models:/bank_marketing_model_registry/1")
      ```
   
   If you deploy a new version (2), you must manually update all code, endpoints, or pipelines that reference version 1.
   A model alias acts like a permanent pointer or tag (e.g., prod, staging, dev) to a specific model version.
   Now, any service that loads the model using the alias:
      ```
         mlflow.pyfunc.load_model("models:/workspace.default.bank_marketing_model_registry@prod")
      ```

4. **Serve the Model**
   - Click on the above created model under **Models** section and click on **Serve this model** option.
   - Create an endpoint by entering details of name, version, compute etc and save the endpoint URL for later use. 

5. **Consume REST API**
   - Generate a Databricks **Personal Access Token (PAT)**.
      - Go to User Profile → Settings → User → Developer → Access Tokens → Manage, then click "Generate New Token".
      - Enter a comment, generate the token, and copy it immediately as it cannot be viewed later.
   - Start and Call the model endpoint for real-time predictions:
     ```python
     import requests, json
     import pandas as pd

     url = "https://<databricks-instance>/serving-endpoints/bank_marketing_model_endpoint/invocations"
     headers = {
         "Authorization": "Bearer <your-token>",
         "Content-Type": "application/json",
     }

     raw_data = [{
         "age": 45,
         "balance": 1200,
         "day": 15,
         "duration": 300,
         "campaign": 1,
         "pdays": 999,
         "previous": 0,
         "job": "admin.",
         "marital": "married",
         "education": "secondary",
         "default": "no",
         "housing": "yes",
         "loan": "no",
         "contact": "cellular",
         "month": "may",
         "poutcome": "unknown"
     }]

      df = pd.DataFrame(raw_data)
      transformed_data = preprocessor.transform(df)
      final_json = {
         "dataframe_records": pd.DataFrame(transformed_data.toarray()).to_dict(orient="records")
      }
      # ---------------------------
      # Sending request to Databricks model serving endpoint
      # ---------------------------
     response = requests.post(url, headers=headers, data=final_json)
     print("Status Code:", response.status_code)
     print("Response JSON:", response.json())
     ```


---

## Folder Structure

```
bank-marketing-ml-pipeline/
│
├── bank_marketing_ml_workflow.ipynb    # Main Databricks notebook
├── README.md                                   # Project documentation
├── requirements.txt                            # Python dependencies
└── data/                                       # (Optional) Local dataset storage
    ├── bank-full.csv
    └── bank.csv
```

---

## REST API Endpoint

- **Endpoint Name:** `bank_marketing_model_endpoint`  
- **Method:** POST  
- **Input Format:** JSON (records array)  
- **Output:** Predicted class & probability

---

## Future Enhancements

- Implement **Hyperparameter tuning** with HyperOpt or Optuna
- Add **Databricks Workflows** for full MLOps automation
- Enable **monitoring with Databricks Model Monitor**
- Automate **feature engineering with Feature Store**

## 🐍 Installation & Setup

### 1. Clone the Repository
```bash
git clone https://github.com/TejeswarS4479/MLOPS-Marketing-Campaign-POC.git
cd MLOPS-Marketing-Campaign-POC