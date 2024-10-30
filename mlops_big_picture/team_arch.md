---
layout: default
title: BridgeAI MLOps Knowledge Hub
---

## Team MLOps Architecture

<h3>The Team's Architecture <a href="https://app.mural.co/t/jmsandbox6893/m/jmsandbox6893/1723564838519/90dee27020222851bf2f8b62c04fd272c25fd1d3?sender=udec36d924fb252f9f2506642" target="_blank">Mural</a>:</h3>

Click on a number icon in the image for a brief description of the process associated with it.

<img src="./assets/mlops_architecture.png" usemap = "#arch" width="839" height="650.64"/>

<!-- intrinsic size - 1980 by 1542; div w and h by 2.36 -->

<!-- href = "./mlops_big_picture/team_arch.html#1-model-development" -->

<map name = "arch">
    <area  alt="Model Development" href="#1-model-development" coords="752,540,10" shape = "circle">
    <area  alt="Models Pushed"  href="#2-models-pushed" coords="606,461,9" shape="circle">
    <area  alt="Model Commit"  href="#3-model-commit" coords="453,597,10" shape="circle">
    <area  alt="Model Registry and Store"  href="#4---6-model-registry-and-store" coords="311,122,9" shape="circle">
    <area  alt="Model Registry and Store"  href="#4---6-model-registry-and-store" coords="406,122,9" shape="circle">
    <area  alt="Model Registry and Store"  href="#4---6-model-registry-and-store" coords="493,123,9" shape="circle">
    <area  alt="Manual Push to Model Server"  href="#7-manual-push-to-model-server" coords="617,110,10" shape="circle">
    <area  alt="Prediction Service"  href="#8-prediction-service" coords="698,155,11" shape="circle">
    <area  alt="User input and Predictions Output"  href="#9-user-input-and-predictions-output" coords="789,222,9" shape="circle">
    <area  alt="User Interaction Data Captured"  href="#10-user-interaction-data-captured" coords="618,190,11" shape="circle">
    <area  alt="Model Monitoring For Decay"  href="#11-model-monitoring-for-decay" coords="712,288,10" shape="circle">
    <area  alt="Scheduler Initiates Training Process"  href="#12-scheduler-initiates-training-process" coords="254,309,10" shape="circle">
    <area  alt="DAG Initiates Docker Instance to be Run"  href="#13-dag-initiates-docker-instance-to-be-run" coords="333,454,8" shape="circle">
    <area  alt="Data Retrieved From S3 Bucket"  href="#14-data-retrieved-from-s3-bucket" coords="208,453,8" shape="circle">
    <area  alt="Data is Preprocessed and Transformed"  href="#15-data-is-preprocessed-and-transformed" coords="323,354,9" shape="circle">
    <area  alt="Features Stored"  href="#16-features-stored" coords="415,303,9" shape="circle">
    <area  alt="Feature Store Fetch"  href="#17-feature-store-fetch" coords="464,364,11" shape="circle">
    <area  alt="Model Created"  href="#18-model-created" coords="543,369,9" shape="circle">
    <area  alt="Model Version Storing"  href="#19-model-version-storing" coords="465,303,9" shape="circle">
    <area  alt="Model Monitor Pull"  href="#20-model-monitor-pull" coords="724,408,12" shape="circle">
    <area  alt="Potential Retrigger"  href="#21-potential-retrigger" coords="680,401,11" shape="circle">
    <area  alt="Industry Data"  href="#22-industry-data" coords="39,142,9" shape="circle">
</map>

## Components

The following explanations apply to the team's MLOps architecture:

### 1. Model Development

Data scientists develop models locally.

### 2. Models pushed

<!-- All models are stored in the artefact store in MLflow.

Data format: `.pth`
Data visibility: High
Frequency of data flow: On demand

For each model, artefact store contains:

- Hyperparameters
- Uniform Resource Identifier (URI)
- `.pth` file -->

All models pushed from local machine are stored in the artefact store in MLflow. The store itself is an S3 bucket, where for each model a `.pth` file, evaluation metrics, hyperparameters (α,β,etc) and Uniform Resource Identifier (URI) are stored.


Data format: `.pth`\
Data visibility: High\
Frequency of data flow: On demand


### 3. Model commit

One chosen algorithm, parameters, data and model development code is finalised and checked into the main branch and baselined.

Data format: `.pth`, `.csv`

### 4 - 6. Model Registry and Store

As models move through MLflow Store:

Data visibility: High\
Frequency of data flow: On demand

4 - The best model is manually chosen to be promoted, and tagged as None.

5 - Manual compliance checks are made, and model is then tagged as Staging.

6 - Model tagged manually as Production based on Comparison / AB testing.

### 7. Manual push to model server

Model manually pushed to Model Server to serve in Production

<!-- explanation of process -->

Frequency of archiving of data: On demand

### 8. Prediction service

Prediction Service is ready to serve users.

<!-- explanation of how -->

Data format: URI\
Data visibility: Low\
Frequency of data flow: Real-time

### 9. User input and predictions output

As user interacts with prediction service, their input is returned to them.

<!-- explanation of process -->

Data format: JSON\
Data visibility: Med\
Frequency of data flow: Real-time

### 10. User interaction data captured

User interaction data is captured and stored in logs database in S3.

<!-- explanation of process -->

### 11. Model monitoring for decay

Model monitoring setup checks model and data for drift or decay.

<!-- explanation of process -->


### 12. Scheduler initiates training process

<!-- explanation of process -->

### 13. DAG initiates docker instance to be run

<!-- explanation of process -->

### 14. Data retrieved from S3 bucket

The data for training, testing and evaluation is retrieved from Amazon S3 bucket.

<!-- explanation of process -->

Data format: `.csv`\
Data visibility: Low\
Frequency of data flow: Based on scheduler or on demand, depending on whether training process is manually retriggered later on.

### 15. Data is preprocessed and transformed

<!-- explanation of process -->

Data format: `.csv`\
Data visibility: Low\
Frequency of data flow: Based on scheduler or on demand, depending on whether training process is manually retriggered later on.


### 16. Features stored

The output of preprocessing is stored in feature store

<!-- explanation of process -->

Data format: `.csv.dvc`\
Data visibility: Low\
Frequency of data flow: Based on scheduler or on demand, depending on whether training process is manually retriggered later on.


### 17. Feature store fetch

Data from feature store is fetched for training and evaluation

<!-- explanation of process -->

Data format: `.csv.dvc`\
Data visibility: High\
Frequency of data flow: Based on scheduler or on demand, depending on whether training process is manually retriggered later on.


### 18. Model created

Model is created and trained against test data using metrics

<!-- explanation of process -->

Data format: `.csv`\
Data visibility: Low\
Frequency of data flow: Based on scheduler 


### 19. Model version storing

Each model version is stored in the database within the model store

<!-- explanation of process -->

Data format: `.pth`\
Data visibility: High\
Frequency of data flow: Based on scheduler

### 20. Model monitor pull

Model monitor pulls new data periodically from S3 and investigates it for decay

<!-- explanation of process -->

<!-- ALL TBC -->

### 21. Potential retrigger

Upon identifying model decay, Data Scientists manually retrigger the retraining process.

<!-- explanation of process -->

<!-- ALL TBC -->

### 22. Industry Data 

Simulated industry data is supplied to the pipeline on-demand

<!-- explanation of process -->

<!-- ALL TBC -->

<!-- <area shape = "circle" coords="" alt="" href = ""> -->