# Marketing Analytics ML Project: Bank Marketing Campaign Response Prediction

## Description
Build a binary classification model to predict whether customers will subscribe to a term deposit after a direct marketing campaign (phone calls). 
This helps banks optimize their marketing resources and improve campaign ROI by targeting the most likely respondents.

## Problem Statement
A Portuguese bank runs direct marketing campaigns with only 11% success rate, requiring significant call center resources. 
The marketing team needs to identify customers most likely to subscribe to term deposits, aiming to improve campaign efficiency by 50% while maintaining or increasing overall subscription numbers.

## Dataset
**Bank Marketing Dataset**  
**URL:** [https://archive.ics.uci.edu/dataset/222/bank+marketing](https://archive.ics.uci.edu/dataset/222/bank+marketing)  
**Size:** ~45,000 contacts with 20+ features  
**Features:** Customer demographics, economic indicators, previous campaign history, call details, social/economic context  
**Target:** Subscription to term deposit (yes/no)

## Primary Deliverable
Binary classification model for campaign response prediction.

## Performance Targets
Below targets should be calibrated after initial data exploration.

### Model Performance:
- **Precision:** Target to be set based on actual baseline conversion rate that exists in the data and business ROI requirements.  
  *Example: >40% (4x better than random targeting if suppose baseline rate is 10%)*
- **Recall:** Balance between campaign capacity and revenue capture (determine after cost-benefit analysis)
- **AUC-ROC:** >0.75 (demonstrates meaningful predictive power)

### Business Validation:
- Campaign efficiency improvement vs. current targeting method
- Cost per acquisition reduction
- Revenue impact per marketing dollar spent

## Tools

### Data Engineering:
- Databricks Notebooks / AWS SageMaker Studio Notebooks: Interactive development (Python, SQL, Scala, R)
- Delta Lake / AWS Lake Formation: Data lakehouse with ACID transactions
- Apache Spark / AWS Glue: Distributed data processing and feature engineering
- Databricks SQL / Amazon Athena: Analytics and data exploration

### Machine Learning:
- Databricks ML Runtime / SageMaker ML Instances: Pre-configured ML environments
- MLflow / SageMaker Experiments: Built-in experiment tracking and model registry
- AutoML / SageMaker Autopilot: Automated model training and tuning
- UC Feature Store / SageMaker Feature Store: Centralized feature management

### MLOps & Deployment:
- Databricks Workflows / SageMaker Pipelines: Job scheduling and orchestration
- Model Serving / SageMaker Endpoints: Real-time and batch inference endpoints
- Unity Catalog / AWS Data Catalog: Data governance and lineage
- Databricks Repos / SageMaker Git Integration: Version control with repos

## Complete ML Workflow in Databricks/SageMaker Studio
- **Data Ingestion:** Databricks notebooks + Delta Lake / SageMaker Processing + S3
- **Data Processing:** Spark DataFrames + SQL / SageMaker Processing + Pandas/Spark
- **Feature Engineering:** Feature Store / SageMaker Feature Store
- **Model Training:** MLflow experiments / SageMaker Training Jobs
- **Model Evaluation:** MLflow model comparison / SageMaker Model Monitor
- **Model Deployment:** Model serving endpoints / SageMaker Endpoints
- **Monitoring:** MLflow or Databricks Monitor / SageMaker Model Monitor + CloudWatch
- **Orchestration:** Databricks Workflows / SageMaker Pipelines + Step Functions

## Dataset location:
[Bank Marketing - UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/222/bank+marketing)  

## Recommended ML Course (on Plural Sight by Janani Ravi)
[Building Machine Learning Models on Databricks](https://www.pluralsight.com/courses/building-machine-learning-models-databricks)  
