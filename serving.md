---
layout: default
title: BridgeAI MLOps Knowledge Hub
---

# Model Serving Spike Content

>Note:
>This spike lists and compares some open-source model serving options or tools available based on ease of implementation, compatibility with PyTorch/Sklearn, and Kubernetes integration, and provides a recommendation for the most suitable tool for our use case.
>
>We are particularly looking for real-time or online inference rather than batch inference. [Batch inference](https://learn.microsoft.com/en-us/azure/machine-learning/overview-what-is-azure-machine-learning?view=azureml-api-2) processes a large batch of input data at once rather than processing each input data point individually in real time.
<br>

**Model Serving** vs **Model Deployment**

To make use of a standard definition, the team stuck to the terminology used here in [this blog](https://neptune.ai/blog/ml-model-serving-best-tools).

>**Model Serving Runtime**: Packaging a trained machine learning model into a container and setting up APIs so it can handle incoming requests. This allows the model to be used in a production environment, responding to data inputs with predictions (inference). **BentoML**, **TorchServe**, **Tensorflow Serving** are examples.
>
>**Model Serving Platform**: An environment designed to dynamically scale the number of model containers in response to incoming traffic. Tools like KServe, Bento Cloud, and Seldon Core are examples of serving platforms. They manage the infrastructure needed to deploy and scale models efficiently, responding to varying traffic without manual intervention.
>
>**Model Deployment**: The process of integrating a packaged model into a serving platform and connecting it to the broader infrastructure, such as databases and downstream services. This ensures the model can access necessary data, perform its intended functions, and deliver inference results to consumers.
The terms 'model serving' and 'model deployment' are often loosely considered to have the same meaning, and some documents use them interchangeably.

---

**Table of Contents**
1. [MLFlow For Model Serving](#1-mlflow-for-model-serving)\
        [MLFlow - Model Serving Runtime](#mlflow---model-serving-runtime)\
        [MLFlow - Model Serving Platforms](#mlflow---model-serving-platforms)\
        [MLFlow - Deploying MLFlow model to Kubernetes](#mlflow---deploying-mlflow-model-to-kubernetes)\
        [MLFlow - Summary](#mlflow---summary)
2. [Model Serving using FastAPI](#2-model-serving-using-fastapi)\
        [FastAPI - Model Serving Runtime](#fastapi---model-serving-runtime)\
        [FastAPI - Model Serving Platforms](#fastapi---model-serving-platforms)\
        [FastAPI - Deploying MLFlow model to Kubernetes](#fastapi---deploying-mlflow-model-to-kubernetes)\
        [FastAPI - Summary](#fastapi---summary)
3. [BentoML for Model serving](#3-bentoml-for-model-serving)\
        [BentoML - Model Serving Runtime](#bentoml---model-serving-runtime)\
        BentoML - Model Serving Platforms\
        BentoML - Deploying MLFlow model to Kubernetes\
        BentoML - Summary
Summary Table\
        Questions\
References

---

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

---

### MLFlow - Deploying MLFlow model to Kubernetes
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

---

### MLFlow - Summary
Supports PyTorch and SKlearn models natively - [MLFlow models - built-in model flavors](https://mlflow.org/docs/latest/models.html#built-in-model-flavors)

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

<!-- ### FastAPI - Deploying MLFlow model to Kubernetes -->
<!-- <style>
.dropdown {
height: 10%;
width: 10%;
position: fixed;
/* z-index: 1; */
background-color: rgb(24, 137, 105);
overflow-x: hidden;
transition: 0.5s;
padding-top: 60px;
}
</style> -->
<!-- <div id="myDropdown" class="dropdown">
<details>
<summary>FastAPI - Deploying MLFlow model to Kubernetes</summary> -->
<!--All you need is a blank line-->

<!-- test text -->
<!-- </details> -->
<!-- </div> -->

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


## 3. BentoML for Model Serving

>BentoML is an open-source model serving library for building performant and scalable AI applications with Python. It comes with everything you need for serving optimization, model packaging, and production deployment.

“Bentos” is an archive containing all the necessary components to package a model.

### BentoML - Model Serving Runtime
- Manually create a model serving runtime container using the following steps
  - Install BentoML and create a service
  - Build the Bento with your model and service
  - Containerize the Bento using bentoml containerize
  - Push the Docker image to GHCR
- Model loading and inference related logic need to be implemented

### BentoML - Model Serving Platforms
- BentoML recommends Bento Cloud (a paid service) to deploy models in a kubernetes native manner
- But similar model serving platforms like Seldon Core or KServe(open source) can be used here

>So the prefered option here is use BentoML to create a container of for the model serving and then use Kserve as serving platform to deploy the service.

### BentoML - Deploying MLFlow model to Kubernetes

1. Install BentoML and Dependencies

`pip install bentoml`

2. Create a BentoML Service

Create a BentoML service for your model. Basically wrap the model with an api endpoint similar to the process of doing so using FastAPI. A sample not tested code:

```
# sample_service.py
import bentoml
import mlflow
from transformers import pipeline
model_artefact_path = "model_uri"
model_uri = mlflow.get_artifact_uri(model_artefact_path)
bento_model = bentoml.mlflow.import_model(
    'mlflow_pytorch_mnist',
    model_uri,
    signatures={'predict': {'batchable': True}}
)
@bentoml.service(
    resources={"cpu": "2"},
    traffic={"timeout": 10},
)
class Summarization:
    def __init__(self) -> None:
        # Load model into pipeline
        self.model = bento_model
    @bentoml.api
    def predict(self, data: str) -> str:
        input_data = np.array(data)
        predictions = self.model(input_data)
        return {"predictions": predictions.tolist()}
```

3. Build the Bento for the service:

`bentoml build -f sample_service.py`

4. Containerize the Bento - Use BentoML to containerize the built Bento:

`bentoml containerize sample_model:latest`

This command builds a Docker image for the BentoML service.
Now the Docker Container can be run locally

`docker run -p 3000:3000 sample_model:latest`

5. Deploy to Kubernetes with KServe

Create a KServe InferenceService YAML file and deploy to kubernetes.

 

**Here are the advantages and limitations of BentoML as per** [neptune.ai - The experiment tracker for foundation model training](https://neptune.ai/) 

Advantages:
  - **Ease of use:** BentoML is one of the most straightforward frameworks to use. Since the release of 1.2, it has become possible to build a Bento with a few lines of code.
  - **ML Framework support:** BentoML supports all the leading machine learning frameworks, such as PyTorch, Keras, TensorFlow, and scikit-learn.
  - **Concurrent model execution:** [BentoML supports fractional GPU allocation](https://github.com/bentoml/BentoML/blob/main/src/_bentoml_impl/server/allocator.py). In other words, you can spawn multiple instances of a model on a single GPU to distribute the processing.
  - **Integration:** BentoML comes with integrations for ZenML, Spark, MLflow, [fast.ai](https://www.fast.ai/), Triton Inference Server, and more.
  - **Flexibility:** BentoML is “Pythonic” and allows you to package any pre-trained model that you can import with Python, such as Large Language Models (LLMs), Stable Diffusion, or CLIP.
  - **Clear documentation:** The documentation is easy to read, well-structured, and contains plenty of helpful examples.
  - **Monitoring:** BentoML integrates with ArizeAI and Prometheus metrics.

Key limitations:
  - Requires extra implementation: As BentoML is “Pythonic,” you are required to implement model loading and inference methods on your own.
  - Native support for high-performance runtime: BentoML runs on Python. Therefore, it is not as optimal as Tensorflow Serving or TorchServe, both of which run on backends written in C++ that are compiled to machine code. However, it is possible to use the [ONNX Python API](https://docs.bentoml.com/en/latest/reference/frameworks/onnx.html) to speed up the inference time.

### BentoML - Summary
- Supports multiple ML frameworks
- Gets more control on the preprocessing and postprocessing here similar to FastAPI
- Time consuming to create consistent APIs but with pre and post processing
- Optimised model serving docker
- Follows similar deployment process to other methods

## Summary Table
|  | MLFlow | FastAPI | BentoML
| --- | --- | --- | ---
| **Ease of Implementation** | Very easy | Easy | Easy
| --- | --- | --- | ---
| **Compatibility with SKlearn and PyTorch** | Fully compatible | Fully compatible| Fully compatible
| --- | --- | --- | ---
| **Integration with MLFlow** | Native | Need to do manually - Just need to get the model from the MLFlow and use it locally within the FastAPI app | Has MLFLow integration
| --- | --- | --- | ---
| **Dependency management** | Yes | Manual | Yes, can do it with the [MLFlow integration](https://docs.bentoml.com/en/1.1/integrations/mlflow.html#additional-tips)
| --- | --- | --- | ---
| **Additional components or things to consider** | Install either via MLServer (`pip install mlflow[extras]`) or KServe to the Kubernetes cluster | Manually bind dependencies and model versions to a container; Install Kserve to the kubernetes cluster | Install bentoml using `pip install bentoml`; Install Kserve to the kubernetes cluster; NO need to follow [Yatai based installation](https://docs.yatai.io/en/latest/concepts/architecture.html#yatai-architecture) if we are using bentoML just for model serving runtime creation
| --- | --- | --- | ---
| **Integration with Kubernetes** | Flawless integration with KServe and Seldon Core | Easy integration once we have the container ready with any kubernetes deployment platform | Flawless integration
| --- | --- | --- | ---
| **Recommended** | Yes | Can be considered | Yes

>What is recommended?
>
>It is better to start with MLFlow based deployment. Once things are in place, or time permits, or if we think the need to include preprocessing steps along with model loading and inference, we could move to the BentoML based approach.
>
>This decision is mainly because of the simplicity of the serving option that MLFlow provides and the additional learning/knowledge that BentoML requires. Other than that, the complexities look similar as per the preliminary check.
>What needs to be changed when moving from mlflow to bentoml later?
>- A bentoml service needs to be written with a consistent endpoint
>        - Need to ensure model versions and dependencies are correctly packed
>- Create a docker file using bentoml cli instead of mlflow cli
>- Point the deployment services to use the new docker


Currently, the preprocessing pipeline used in the model training is just being saved locally during the training as an artefact. If we want to use the exact same preprocessing pipeline for inference, we may need to look for an option to log that artefact along with the model, pull it and use it before the inference. Once we have clarity on how is the deployment happening, this can be done without much difficulty.


**Questions:**
Q. Decision between KServe or Seldon core - Which one is more suitable for our use case? 
        A comparison - [KServe vs. Seldon Core - Superwise ML Observability](https://superwise.ai/blog/kserve-vs-seldon-core/) 

        KServe is open source whereas [SeldonCore](https://www.seldon.io/pricing) is expensive. And so is [BentoCloud](https://www.bentoml.com/pricing).

## References
1. MLFlow serving [Deploy MLflow Model to Kubernetes — MLflow 2.15.1 documentation](https://mlflow.org/docs/latest/deployment/deploy-model-to-kubernetes/index.html) 

2. Kserve - [Home - KServe Documentation Website](https://kserve.github.io/website/latest/) 

  - Kserve using MLFlow models - [MLFlow - KServe Documentation Website](https://kserve.github.io/website/latest/modelserving/v1beta1/mlflow/v2/) 

3. [FastAPI](https://fastapi.tiangolo.com/) 

4. [FastAPI vs Flask: Comparison Guide for Data Science Enthusiasts](https://analyticsindiamag.com/developers-corner/fastapi-vs-flask-comparison-guide-for-data-science-enthusiasts/) 

5. [KubeFlow serving options](https://www.kubeflow.org/docs/external-add-ons/serving/overview/) 

6. KServe installation - [GitHub - kserve/kserve: Standardized Serverless ML Inference Platform on Kubernetes](https://github.com/kserve/kserve#hammer_and_wrench-installation) 

7. [Best Tools For ML Model Serving](https://neptune.ai/blog/ml-model-serving-best-tools) 

8. MLFlow BentoML - [MLflow](https://docs.bentoml.com/en/1.1/integrations/mlflow.html) 

9. BentoML MLFlow dependency management - [MLflow additional tips](https://docs.bentoml.com/en/1.1/integrations/mlflow.html#additional-tips)