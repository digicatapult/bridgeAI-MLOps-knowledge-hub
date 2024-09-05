<!-- ---
layout: default
--- -->

# Model Serving Spike Content

>Note:
>This spike lists and compares some open-source model serving options or tools available based on ease of implementation, compatibility with PyTorch/Sklearn, and Kubernetes integration, and provides a recommendation for the most suitable tool for our use case.
>
>We are particularly looking for real-time or online inference rather than batch inference. [Batch inference](https://learn.microsoft.com/en-us/azure/machine-learning/overview-what-is-azure-machine-learning?view=azureml-api-2) processes a large batch of input data at once rather than processing each input data point individually in real time.\
**Model Serving** vs **Model Deployment**

To stick to a standard definition, I am sticking to the terminology used here in [this blog](https://neptune.ai/blog/ml-model-serving-best-tools).

>**Model Serving Runtime**: Packaging a trained machine learning model into a container and setting up APIs so it can handle incoming requests. This allows the model to be used in a production environment, responding to data inputs with predictions (inference). **BentoML**, **TorchServe**, **Tensorflow Serving** are examples.
>
>**Model Serving Platform**: An environment designed to dynamically scale the number of model containers in response to incoming traffic. Tools like KServe, Bento Cloud, and Seldon Core are examples of serving platforms. They manage the infrastructure needed to deploy and scale models efficiently, responding to varying traffic without manual intervention.
>
>**Model Deployment**: The process of integrating a packaged model into a serving platform and connecting it to the broader infrastructure, such as databases and downstream services. This ensures the model can access necessary data, perform its intended functions, and deliver inference results to consumers.\
The terms 'model serving' and 'model deployment' are often loosely considered to have the same meaning, and some documents use them interchangeably.\

**Table of Contents**
1. [MLFlow For Model Serving](#1-mlflow-for-model-serving)\
        [MLFlow - Model Serving Runtime](#mlflow---model-serving-runtime)\
        [MLFlow - Model Serving Platforms](#mlflow---model-serving-platforms)\
        [MLFlow - Deploying MLFlow model to Kubernetes](#mlflow---deploying-mlflow-model-to-kubernetes)\
        [MLFlow - Summary](#mlflow---summary)
2. [Model Serving using FastAPI](#2-model-serving-using-fastapi)\
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

## 1. MLFlow For Model Serving
MLFlow supports a variety of model deployment targets including Local Infra, AWS Sagemaker, Azure ML, Databricks, Kubernetes, etc. But we will be looking into the Kubernetes deployment here.

### MLFlow - Model Serving Runtime
- MLFlow uses MLServer for creating a serving runtime -- [MLServer — MLServer Documentation](https://mlserver.readthedocs.io/en/latest/) 

- By default MLFlow uses Flask, but prefers MLServer for production -- [Deploy MLflow Model as a Local Inference Server — MLflow 2.15.1 documentation](https://mlflow.org/docs/latest/deployment/deploy-model-locally.html#serving-frameworks) 

- Supports almost all machine learning frameworks and no vendor lock is present here unlike TorchServe or Tensorflow serve

- With simple steps, the url `http://<host>:<port>/invocations` endpoint URL can do predictions

### MLFlow - Model Serving Platforms
MLFlow native model serving using MLSerer supports KServe and Seldon Core both are kubernetes native

KServe has some example code and more documentation and details from MLFlow side - Develop ML model with MLflow and deploy to Kubernetes — MLflow 2.15.1 documentation 

Partner documentation from KServe - MLFlow - KServe Documentation Website 

Seldon core - has got no example code in MLFlow but the partner documentation is also rich - MLflow Server — seldon-core  documentation

<!-- ### MLFlow - Deploying MLFlow model to Kubernetes -->
<details>
<summary>MLFlow - Deploying MLFlow model to Kubernetes</summary>
<br>
The prerequisite to deploy a model to kubernetes is packaging the model as MLFlow Model mentioned here. This is what we are already doing during the end of model training process.

An MLflow Model already packages your model and its dependencies, hence MLflow can create either a virtual environment (for local deployment) or a Docker container image containing everything needed to run your model. So we don’t need to bind the dependencies separately.

Once we have the model ready, deploying the model to Kserve can be done in two ways as mentioned here; either using a docker image or using a model uri.

Summarised steps for the docker image based approach from the above link:

Install the MLServer using

`pip install mlflow[extras]`

Install Kserve to the kubernetes cluster

GitHub - kserve/kserve: Standardized Serverless ML Inference Platform on Kubernetes 

Test the model serving locally,

`mlflow models serve -m runs:/<run_id_for_your_best_run>/model -p 1234 --enable-mlserver`

Create a model docker is as simple as 

`mlflow models build-docker -m runs:/<run_id_for_your_best_run>/model -n <your_dockerhub_user_name>/<mlflow-model-name> --enable-mlserver`

Push the model to docker registry

Write a deployment configuration yaml file

Deploy to the kubernetes cluster using kubectl

If using the model uri approach, we needs to specify the model URI in a remote storage URI format e.g. s3://xxx or gs://xxx. By default, MLflow stores the model in the local file system, so you need to configure MLflow to store the model in remote storage. Please refer to Artifact Store for setup instructions.

Since the detailed steps in the above mentioned document are self explanatory, not adding much information here.
</details>


### MLFlow - Summary
Supports PyTorch and SKlearn models natively - MLFlow models - built-in model flavors

Models are already in supported MLFLow models format when the training completes

Easy integration with kubernetes is provided using KServe or Seldon Core

Dependencies are already taken care of

Easy serving and deployment process

## 2. Model Serving using FastAPI

### FastAPI - Model Serving Runtime
Manually create a model serving runtime using FastAPI

Containerise the so created FastAPI app to create model endpoints

Need to create custom consistent endpoint urls

### FastAPI - Model Serving Platforms
Once the container is ready, any serving platform like Seldon core or KServe(open source) can be used

So the prefered option here is use FastPI to combine the dependencies and correct model version to create a web serving app and then use Kserve as serving platform to deploy the app.
FastAPI - Deploying MLFlow model to Kubernetes

### Deploying MLFlow model to Kubernetes


### FastAPI - Summary
Using web frameworks for building API endpoints is the straightforward way to serve models

Not only MLFlow models, any models can be served using this approach

Gets more control on the preprocessing and postprocessing here

Time consuming to create consistent APIs

Need to capture the dependencies separately for running the model

Model and its specific versions need to be manually added to the 

It is hard to automate the serving process

Involves manual containerisation and then deploying to kubernetes

Follows similar deployment process to other methods