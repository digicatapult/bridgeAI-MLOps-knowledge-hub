---
layout: default
title: BridgeAI MLOps Knowledge Hub
---

## Where did the journey start? How were the design decisions made across the pipeline for each component?

Our journey towards the creation of an end-to-end MLOps pipeline began as an extension of our [AI Adoption Assessment](https://iuk.ktn-uk.org/opportunities/ai-adoption-assessment-toolkit-from-digital-catapult/){:target="_blank"} initiative completed in collaboration with BridgeAI. We believed that in order to make the implementation of MLOps as viable as possible for users, we would need to create an end-to-end pipeline for users that they could adjust to suit their requirements and scope, rather than simply provide instructions on how to create one. 

We decided on different tools for different components of our pipeline such as registry, data versioning and model monitoring by conducting research on optimal tools based on our requirements. This research is covered in the pages underneath <span style="color:#8C1437"><b>"MLOps: The Big Picture"</b></span>, and is grounded in the evaluation of sets of tools per component that were suitable for implementing into our pipeline. More information on alternative tools we considered can be found in the [Horizon Scan](./corporate_perspective/prerequisites.html#horizon-scan){:target="_blank"} of this hub.

Some components (being data store, prediction service, monitoring) did not have formal research conducted, and were instead decided on because they are widely used in the industry and therefore have in-depth documentation/community notes.

Our final tech stack upon deliberating, with links to corresponding pages in this hub:
1. [Data versioning](./mlops_big_picture/versioning.html){:target="_blank"}: DVC
2. [Training pipeline](./mlops_big_picture/DAG.html){:target="_blank"}: Airflow
3. [Model serving](./mlops_big_picture/serving.html){:target="_blank"}: MLflow
4. [Prediction service](./mlops_big_picture/pred_service.html){:target="_blank"}: Swagger
5. [Model monitoring](./mlops_big_picture/monitoring.html){:target="_blank"}: EvidentlyAI
6. [GitOps](./mlops_big_picture/gitops.html){:target="_blank"}: Flux


## What were the requirements for our ML model and the MLOps pipeline?

We wanted to demonstrate an end-to-end, open source, pre-made MLOps pipeline. We opted for keeping our execution of this simple by creating a deploy-model pipeline only, rather than creating variations of the pipeline (eg deploy-code), which we would share with startups as a starting point.

Our base requirements:
1. The pipeline should be made of open source tools, to keep it cost-friendly and help with experimentation
2. We should have a Minimum Viable MLOps pipeline with basic automation that users can then build on using the information provided in the hub, and other resources linked throughout the hub

 

