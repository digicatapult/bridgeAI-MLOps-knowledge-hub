---
layout: default
title: BridgeAI MLOps Knowledge Hub
---

# Model Monitoring

**Table of Contents**
1. [Model Monitoring](./mlops_big_picture/monitoring.html#1-model-monitoring)
      - [Data Drift](./mlops_big_picture/monitoring.html#11-data-drift)
      - [Concept Drift](./mlops_big_picture/monitoring.html#12-concept-drift)
      - [Target Drift](./mlops_big_picture/monitoring.html#13-target-drift)
2. [Data Drift with Evidently Explained](./mlops_big_picture/monitoring.html#2-data-drift-with-evidently-explained)
      - [Steps](./mlops_big_picture/monitoring.html#21-steps)
      - [General Steps](./mlops_big_picture/monitoring.html#22-general-steps)
      - [Key Questions Before Retraining](./mlops_big_picture/monitoring.html#23-key-questions-before-retraining)
      - [Possible Action Items Based on Data Drift Detection](./mlops_big_picture/monitoring.html#24-possible-action-items-based-on-data-drift-detection)
      - [Testing Before Pushing a Newly Trained Model to Production](./mlops_big_picture/monitoring.html#25-testing-before-pushing-a-newly-trained-model-to-production)
3. [Data Drift for the House Price Prediction Use Case](./mlops_big_picture/monitoring.html#3-data-drift-for-the-house-price-prediction-use-case)
4. [Resources](./mlops_big_picture/monitoring.html#resources)



## 1. Model Monitoring
Building a machine learning model is just the beginning. Once you deploy that model into the real world, it faces many challenges that can affect its predictive performance (Model Drift) and require continuous monitoring. Model Drift refers to the decay of the ML model quality over time. Simply put, it is a way of saying “the model quality got worse” or “the model no longer serves its purpose.” Model Drift doesn't pinpoint a specific cause; it's just an observation that the model no longer works as well as it used to. The model decay might happen due to various reasons, including [data drift](https://www.evidentlyai.com/ml-in-production/data-drift){:target="_blank"}, data quality issues, or concept drift. [What is concept drift in ML, and how to detect and address it](https://www.evidentlyai.com/ml-in-production/concept-drift){:target="_blank"}


Below are the 2 Model Drifts discussed widely by “many industry experts”.
- Data Drift
- Concept Drift



**Note:**
- To establish a monitoring strategy refer to the <span style="color:#8C1437"><b>Establishing the monitoring strategy</b></span> section from the link: [Model monitoring for ML in production: a comprehensive guide](https://www.evidentlyai.com/ml-in-production/model-monitoring){:target="_blank"} 


- Model monitoring architectures refer to the <span style="color:#8C1437"><b>Model monitoring architectures</b></span> section from the same link



### 1.1 Data Drift
Data drift is a change in the statistical properties and characteristics of the input data. It occurs when a Machine Learning model is in production, as the data it encounters deviates from the data the model was initially trained on or earlier production data. 

[What is data drift in ML, and how to detect and handle it](https://www.evidentlyai.com/ml-in-production/data-drift){:target="_blank"}

Data Drift Detection methods:

- Summary statistics

- Statistical tests 

- Distance metrics

- Rule-based checks



### 1.2 Concept Drift
Concept Drift implies a change in the learned relationships between the input features. Model Drift is often caused by Concept Drift. 

[What is concept drift in ML, and how to detect and address it](https://www.evidentlyai.com/ml-in-production/concept-drift){:target="_blank"} 



### 1.3 Target Drift
Occurs when the goal or target of your prediction changes.



## 2. Data Drift with Evidently Explained
Two datasets are used to evaluate whether there is a Data Drift.

1. **Reference data** refers to the dataset that serves as the baseline or standard for comparison. This is typically the dataset that the Machine Learning model was trained on or a dataset from a previous period that is considered stable and representative of normal conditions.

2. **Current data** refers to the new or recent dataset that is being evaluated for drift. This is the dataset that has been collected more recently, possibly after the model was deployed or during ongoing operations.

<br>

### 2.1 Steps

[Data Drift Code Practice](https://github.com/evidentlyai/ml_observability_course/blob/main/module2/data_drift_deep_dive.ipynb){:target="_blank"}

<div id="myContainer" class="container">
  <a onclick="toggleContentsM_Drift()"><img src="https://www.svgrepo.com/show/305143/arrow-ios-forward.svg" width="15px" height="15px"> Steps</a>
  <div id="myContentsM_Drift" class="contents">
  <br>

  1. Load the Reference data (depending on the use case, if dataset is huge, it can be a subset or samples drawn from the dataset) as a DataFrame
        <br>
        <br>
  2. Load the Current data (depending on the use case, if dataset is huge, it can be a subset or samples drawn from the dataset) as a DataFrame
        <br>
        <br>
  3. Data Drift can be chosen for individual features (numerical as well as categorical features) or for all the features in the dataset used in Step 1 and Step 2.
        <br>
        <br>

  4. Choose a statistical test by which data drift needs to be analysed such as <b>'chisquare'</b> <b>'jensenshannon'</b>, <b>'wasserstein'</b> etc (list of all statistical tests are provided here - https://docs.evidentlyai.com/user-guide/customization/options-for-statistical-tests). The statistical tests can be chosen for individual metrics as well.
        <br>
        <br>
        
  5. Use any of the Data Drift methods such as DatasetDriftMetric, this metric provides a overall summary of the drift detected from the comparison between the Reference data and the Current data.
        <br>
        <br>
  6. Method “DataDriftTable“ generates a table which compares drift between individual features of the Reference data and the Current data.
        <br>
        <br>
  7. The results from the report generated can be saved as a json or a html file.
        <br>
        <br>
  8. Evidently also supports creating your own statistical test and using it in the drift detection methods.

  </div>
</div>
<br>

**Note:**

How much of data needed in the Reference data and the Current data? (Refer to Evidently’s documentation)

- Depends on the use case

- The decision taken by the DS’s and the business

- The trial and error analysis of the outcomes of Model Monitoring

- The decision taken can be refined once again based on the outcomes as it is an iterative process



### 2.2 High Level Process
In general an organisation who wants to analyse drift would have to:

1. Have data continuously flowing from the upstream, i.e. daily/weekly/monthly.

2. Have prior to model monitoring implementation, depending on the use case have a detailed discussion as to how model monitoring is to be performed, what drift detection has to be implemented, what input features are required for analysis.

3. Have a plan on when to schedule Model Monitoring i.e daily/weekly/monthly

4. Have the action item once a drift has been detected.

5. The above is not an exhaustive list, these change as per use case.



### 2.3 Key Questions before Retraining 
- How much overall Data Drift is acceptable?

- How much Data Drift for each individual features is acceptable?

- Before Retraining with the new data, can data be manually labelled? So that we can test the model’s accuracy/error rate

[To retrain, or not to retrain? Let's get analytical about ML model updates](https://www.evidentlyai.com/blog/retrain-or-not-retrain){:target="_blank"}

**Note:** 

Retraining is required when there is a significant Drift detected and how sensitive will be the model’s prediction if no action is taken when a Drift is detected.



### 2.4 Possible Action Items based on Data Drift detection
- Update the model i.e training the model with old data (can drop some of the historical data) + new data (delta) **without changing** any of the model’s algorithm or the hyperparameters used. Evaluate the performance of the newly created model against the validation and the test data.

- Retrain the model i.e training the model with old data (can drop some of the historical data) + new data (delta) by **experimenting** with new set of hyperparameters **or changing** the algorithm used to build the model itself. Evaluate the performance of the newly created model against the validation and the test data.

**Note:** 

The above 2 training points mentioned above are performed in the local/Dev environment for the Deploy Model solution.



### 2.5 Testing before Pushing a Newly Trained Model to Production
- Prepare the test dataset ideally which is a combination of old model’s test data + new data (neither of the model should have seen this data during training). Use the same test dataset to evaluate the performance of the newly trained model and the existing production model.

- If the accuracy/error of the existing production model’s performance on the test dataset is not good, then the newly trained model could become the production model.

- The existing production model is archived.

- Deployment patterns of newly trained model will be covered in another Spike.

 

[Evaluating Model Performance: Key Metrics to Assess Before Transitioning to Production](https://medium.com/@stefanmii/evaluating-model-performance-key-metrics-to-assess-before-transitioning-to-production-345ee51241d0){:target="_blank"}



## 3 Data Drift for the House Price Prediction Use Case
1. Make sure the Reference data and the Current data  (Section 2.1) is available in S3/any storage location

2. Manually trigger the Data Drift DAG from Airflow.

3. Based on the Drift Report that is generated, a DS analyses the Drift Report and decides whether to Update or Retrain the model manually (as discussed in Section 2.4). 

An implementation of Data Drift is given here:

[ml_observability_course/module2/data_drift_deep_dive.ipynb at main · evidentlyai/ml_observability_course](https://github.com/evidentlyai/ml_observability_course/blob/main/module2/data_drift_deep_dive.ipynb){:target="_blank"}

[Understanding Data Drift and Model Drift: Drift Detection in Python](https://www.datacamp.com/tutorial/understanding-data-drift-model-drift){:target="_blank"}. 

Also refer to the FAQs section from the link provided above.



## Resources
**Model Monitoring, Data Drift & Concept Drift**

[Evidently AI - A complete guide to ML in production](https://www.evidentlyai.com/ml-in-production){:target="_blank"}

<br>

**Drift Detection**

[Data drift parameters - Evidently Documentation](https://docs.evidentlyai.com/user-guide/customization/options-for-statistical-tests){:target="_blank"}

[Data drift algorithm - Evidently Documentation](https://docs.evidentlyai.com/reference/data-drift-algorithm){:target="_blank"}

[ML Observability Course Repo](https://github.com/evidentlyai/ml_observability_course/tree/main/docs/book/ml-observability-course/module-2-ml-monitoring-metrics){:target="_blank"}

<br>

**Statistical Tests Explained**

[Data drift parameters - Evidently Documentation](https://docs.evidentlyai.com/user-guide/customization/options-for-statistical-tests){:target="_blank"} 

[Which test is the best? We compared 5 methods to detect data drift on large datasets](https://www.evidentlyai.com/blog/data-drift-detection-large-datasets){:target="_blank"} 

[A Comprehensive Guide on How to Monitor Your Models in Production](https://neptune.ai/blog/how-to-monitor-your-models-in-production-guide){:target="_blank"}

<br>

**Mitigation after Drift Detection**

[Medium - Drift in Machine Learning](https://towardsdatascience.com/drift-in-machine-learning-e49df46803a){:target="_blank"}

[Data Drift Code Practice](https://github.com/evidentlyai/ml_observability_course/blob/main/module2/data_drift_deep_dive.ipynb){:target="_blank"}