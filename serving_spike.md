---
layout: default
title: DAG Spike
parent: Team Journey - Requirements and Research
order: 2
---

[<Back](index.md)

### [Model Serving Spike Content](https://digicatapult.atlassian.net/wiki/spaces/MLOps/pages/2575171585/Deploy+Model+Solution+Architecture)

```
Note:
This spike lists and compares some open-source model serving options or tools available based on ease of implementation, compatibility with PyTorch/Sklearn, and Kubernetes integration, and provides a recommendation for the most suitable tool for our use case.

We are particularly looking for real-time or online inference rather than batch inference. [Batch inference](https://learn.microsoft.com/en-us/azure/machine-learning/overview-what-is-azure-machine-learning?view=azureml-api-2) processes a large batch of input data at once rather than processing each input data point individually in real time.
```

**Model Serving** vs **Model Deployment**

To stick to a standard definition, I am sticking to the terminology used here in [this blog](https://neptune.ai/blog/ml-model-serving-best-tools).

```
Model Serving Runtime: Packaging a trained machine learning model into a container and setting up APIs so it can handle incoming requests. This allows the model to be used in a production environment, responding to data inputs with predictions (inference). **BentoML**, **TorchServe**, **Tensorflow Serving** are examples.

Model Serving Platform: An environment designed to dynamically scale the number of model containers in response to incoming traffic. Tools like KServe, Bento Cloud, and Seldon Core are examples of serving platforms. They manage the infrastructure needed to deploy and scale models efficiently, responding to varying traffic without manual intervention.

Model Deployment: The process of integrating a packaged model into a serving platform and connecting it to the broader infrastructure, such as databases and downstream services. This ensures the model can access necessary data, perform its intended functions, and deliver inference results to consumers.
```


The terms 'model serving' and 'model deployment' are often loosely considered to have the same meaning, and some documents use them interchangeably.

**Table of Contents**
1. [MLFlow For Model Serving](serving_spike#MLFlow-For-Model-Serving)\
        MLFlow - Model Serving Runtime\
        MLFlow- Model Serving Platforms\
        MLFlow - Deploying MLFlow model to Kubernetes\
        MLFlow - Summary
2. Model Serving using FastAPI\
        FastAPI - Model Serving Runtime\
        FastAPI - Model Serving Platforms\
        FastAPI - Deploying MLFlow model to Kubernetes\
        FastAPI - Summary
3. BentoML for Model serving\
        BentoML - Model Serving Runtime\
        BentoML - Model Serving Platforms\
        BentoML - Deploying MLFlow model to Kubernetes\
        BentoML - Summary
Summary Table\
        Questions\
References

# 1. MLFlow For Model Serving
MLFlow supports a variety of model deployment targets including Local Infra, AWS Sagemaker, Azure ML, Databricks, Kubernetes, etc. But we will be looking into the Kubernetes deployment here.

**MLFlow - Model Serving Runtime**
- MLFlow uses MLServer for creating a serving runtime - [MLServer — MLServer Documentation](https://mlserver.readthedocs.io/en/latest/) 

- By default MLFlow uses Flask, but prefers MLServer for production - [Deploy MLflow Model as a Local Inference Server — MLflow 2.15.1 documentation](https://mlflow.org/docs/latest/deployment/deploy-model-locally.html#serving-frameworks) 

- Supports almost all machine learning frameworks and no vendor lock is present here unlike TorchServe or Tensorflow serve

- With simple steps, the url http://<host>:<port>/invocations endpoint URL can do predictions