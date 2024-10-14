---
layout: default
title: BridgeAI MLOps Knowledge Hub
---

# Model Serving Spike Content

<blockquote class="callout callout_info">
<span class="callout-icon">ℹ️</span>
    <br>
    <br>
    This spike lists and compares some open-source model serving options or tools available based on ease of implementation, compatibility with PyTorch/Sklearn, and Kubernetes integration, and provides a recommendation for the most suitable tool for our use case.
    <br>  
    <br> 
    We are particularly looking for real-time or online inference rather than batch inference. <a href="https://learn.microsoft.com/en-us/azure/machine-learning/overview-what-is-azure-machine-learning?view=azureml-api-2" target="_blank">Batch (offline) inference </a>
    processes a large batch of input data at once rather than processing each input data point individually in real time.
</blockquote>

<br>

**Model Serving** vs **Model Deployment**

To make use of a standard definition, the team stuck to the terminology used here in [this blog](https://neptune.ai/blog/ml-model-serving-best-tools){:target="_blank"}.

<blockquote class="callout callout_definition">
<span class="callout-icon">📓</span>
    <br>
    <br>
    <b>Model Serving Runtime</b>: Packaging a trained machine learning model into a container and setting up APIs so it can handle incoming requests. This allows the model to be used in a production environment, responding to data inputs with predictions (inference). <b>BentoML</b>, <b>TorchServe</b>, <b>Tensorflow Serving</b> are examples.
    <br>
    <br>
    <b>Model Serving Platform</b>: An environment designed to dynamically scale the number of model containers in response to incoming traffic. Tools like <b>KServe</b>, <b>Bento Cloud</b>, and <b>Seldon Core</b> are examples of serving platforms. They manage the infrastructure needed to deploy and scale models efficiently, responding to varying traffic without manual intervention.
    <br>
    <br>
    <b>Model Deployment</b>: The process of integrating a packaged model into a serving platform and connecting it to the broader infrastructure, such as databases and downstream services. This ensures the model can access necessary data, perform its intended functions, and deliver inference results to consumers.
</blockquote>

The terms 'model serving' and 'model deployment' are often loosely considered to have the same meaning, and some documents use them interchangeably.

<br>

---

<br>

**Table of Contents**
1. [MLFlow For Model Serving](./mlops_big_picture/serving.html#1-mlflow-for-model-serving)
  - [MLFlow - Model Serving Runtime](./mlops_big_picture/serving.html#mlflow---model-serving-runtime)
  - [MLFlow - Model Serving Platforms](./mlops_big_picture/serving.html#mlflow---model-serving-platforms)
  - [MLFlow - Deploying MLFlow model to Kubernetes](./mlops_big_picture/serving.html#mlflow---deploying-mlflow-model-to-kubernetes)
  - [MLFlow - Summary](./mlops_big_picture/serving.html#mlflow---summary)
2. [Model Serving using FastAPI](./mlops_big_picture/serving.html#2-model-serving-using-fastapi)
  - [FastAPI - Model Serving Runtime](./mlops_big_picture/serving.html#fastapi---model-serving-runtime)
  - [FastAPI - Model Serving Platforms](./mlops_big_picture/serving.html#fastapi---model-serving-platforms)
  - [FastAPI - Deploying MLFlow model to Kubernetes](./mlops_big_picture/serving.html#fastapi---deploying-mlflow-model-to-kubernetes)
  - [FastAPI - Summary](./mlops_big_picture/serving.html#fastapi---summary)
3. [BentoML for Model serving](./mlops_big_picture/serving.html#3-bentoml-for-model-serving)
  - [BentoML - Model Serving Runtime](./mlops_big_picture/serving.html#bentoml---model-serving-runtime)
  - [BentoML - Model Serving Platforms](./mlops_big_picture/serving.html#bentoml---model-serving-platforms)
  - [BentoML - Deploying MLFlow model to Kubernetes](./mlops_big_picture/serving.html#bentoml---deploying-mlflow-model-to-kubernetes)
  - [BentoML - Summary](./mlops_big_picture/serving.html#bentoml---summary)
4. [Summary Table](./mlops_big_picture/serving.html#summary-table)
  - [Questions](./mlops_big_picture/serving.html#questions)
5. [Resources](./mlops_big_picture/serving.html#resources)

---

## 1. MLFlow For Model Serving
MLFlow supports a variety of model deployment targets including Local Infra, AWS Sagemaker, Azure ML, Databricks, Kubernetes, etc. But we will be looking into the Kubernetes deployment here.

### MLFlow - Model Serving Runtime
- MLFlow uses MLServer for creating a serving runtime -- [MLServer — MLServer Documentation](https://mlserver.readthedocs.io/en/latest/){:target="_blank"} 

- By default MLFlow uses Flask, but prefers MLServer for production -- [Deploy MLflow Model as a Local Inference Server — MLflow 2.15.1 documentation](https://mlflow.org/docs/latest/deployment/deploy-model-locally.html#serving-frameworks){:target="_blank"}

- Supports almost all machine learning frameworks and no vendor lock is present here unlike TorchServe or Tensorflow serve

- With simple steps, the url `http://<host>:<port>/invocations` endpoint URL can do predictions

### MLFlow - Model Serving Platforms
- MLFlow native model serving using MLSerer supports [KServe](https://kserve.github.io/website/latest/){:target="_blank"} and [Seldon Core](https://docs.seldon.io/projects/seldon-core/en/latest/){:target="_blank"} both are kubernetes native

- KServe has some example code and more documentation and details from MLFlow side - [Develop ML model with MLflow and deploy to Kubernetes](){:target="_blank"} 
    - Partner documentation from KServe - [MLFlow - KServe Documentation Website](https://mlflow.org/docs/latest/deployment/deploy-model-to-kubernetes/tutorial.html){:target="_blank"}
<br>
<br>

- Seldon core - has got no example code in MLFlow but the partner documentation is also rich - [MLflow Server — seldon-core  documentation](https://docs.seldon.io/projects/seldon-core/en/latest/servers/mlflow.html){:target="_blank"}

<blockquote class="callout callout_info">
<span class="callout-icon">ℹ️</span>
    <br>
    <br>
    The prefered option here when deploying ML models in the MLFlow ecosystem is to use <b>MLServer as serving runtime</b> and <b>Kserve as serving platform</b> which are natively supported by MLFlow.
</blockquote>

<br>

### MLFlow - Deploying MLFlow model to Kubernetes

[Kubernetes Model Deploy: Packaging and Dependencies](https://mlflow.org/docs/latest/deployment/deploy-model-to-kubernetes/tutorial.html#step-5-packaging-the-model-and-dependencies){:target="_blank"}

[KServe install](https://github.com/kserve/kserve#hammer_and_wrench-installation){:target="_blank"}

<div id="myContainer" class="container">
  <a onclick="toggleContentsS_ML_Deploy()"><img src="https://www.svgrepo.com/show/305143/arrow-ios-forward.svg" width="15px" height="15px"> MLFlow - Deploying MLFlow model to Kubernetes</a>
  <div id="myContentsS_ML_Deploy" class="contents">
  <br>
  The prerequisite to deploy a model to kubernetes is packaging the model as MLFlow Model mentioned in <span style="color:#8C1437"><b>Packaging and Dependencies</b></span> (linked above).
  
  <br>
  <br>
  This is what we are already doing during the end of model training process.

  <br>
  <br>

  <blockquote class="callout callout_default">
      An MLflow Model already packages your model and its dependencies, hence MLflow can create either a virtual environment (for local deployment) or a Docker container image containing everything needed to run your model. So we don’t need to bind the dependencies separately.
  </blockquote>

  <br>

  Once we have the model ready, deploying the model to Kserve can be done in two ways (methods linked in Resources); either using a docker image or using a model uri.

  <br>
  <br>

  Summarised steps for the docker image based approach:

  <br>
  <br>

  1. Install the MLServer using
  <br>
  <code>pip install mlflow[extras]</code>

  <br>
  <br>

  2. Install Kserve to the kubernetes cluster (<span style="color:#8C1437"><b>KServe install</b></span> linked above)

  <br>
  <br>

  3. Test the model serving locally,
  <br>
  <code>mlflow models serve -m runs:/{run_id_for_your_best_run}/model -p 1234 --enable-mlserver</code>

  <br>
  <br>

  4. Create a model docker is as simple as
  <br>
  <code>mlflow models build-docker -m runs:/{run_id_for_your_best_run}/model -n {your_dockerhub_user_name}/{mlflow-model-name} --enable-mlserver</code>
  <br>
  <br>

  5. Push the model to docker registry

  <br>
  <br>

  6. Write a deployment configuration yaml file

  <br>
  <br>

  7. Deploy to the kubernetes cluster using kubectl

  <br>
  <br>

  If using the model uri approach, we needs to specify the model URI in a remote storage URI format e.g. <code>s3://xxx</code> or <code>gs://xxx</code>. By default, MLflow stores the model in the local file system, so you need to configure MLflow to store the model in remote storage. Please refer to Artifact Store (linked in Resources) for setup instructions.

  <br>
  <br>

  </div>
</div>
<br>



### MLFlow - Summary
- Supports PyTorch and SKlearn models natively - [MLFlow models - built-in model flavors](https://mlflow.org/docs/latest/models.html#built-in-model-flavors){:target="_blank"}

- Models are already in supported MLFLow models format when the training completes

- Easy integration with kubernetes is provided using KServe or Seldon Core

- Dependencies are already taken care of

- Easy serving and deployment process

<br>

## 2. Model Serving using FastAPI

### FastAPI - Model Serving Runtime
- Manually create a model serving runtime using [FastAPI](https://fastapi.tiangolo.com/){:target="_blank"}

- Containerise the so created FastAPI app to create model endpoints

- Need to create custom consistent endpoint urls

### FastAPI - Model Serving Platforms
- Once the container is ready, any serving platform like Seldon core or KServe(open source) can be used

<blockquote class="callout callout_default">
    The prefered option here is use FastAPI to combine the dependencies and correct model version to create a web serving app and then use <b>Kserve as serving platform to deploy the app.</b>
</blockquote>


<br>

### FastAPI - Deploying MLFlow model to Kubernetes
<div id="myContainer" class="container">
  <a onclick="toggleContentsS_Fast_Deploy()"><img src="https://www.svgrepo.com/show/305143/arrow-ios-forward.svg" width="15px" height="15px"> FastAPI - Deploying MLFlow model to Kubernetes</a>
  <div id="myContentsS_Fast_Deploy" class="contents">

  Model serving and deployment using FastAPI is straightforward and similar to classical s/w deployments.

  The steps involved are as follows;
  <br>
  <br>

  1. <b>Export the Model from MLFlow</b>

  <ul>- Load the model from MLFlow so that it can be loaded by FastAPI application.</ul>

  <ul>- For pytorch models - <code>mlflow.sklearn.load_model</code>(model_uri, dst_path=None)</ul>

  <ul>- For sklearn models - <code>mlflow.sklearn.load_model</code>(model_uri, dst_path=None)</ul>

  <ul>- SKlearn supports several models and it can even support custom models using the <code>mlflow.pyfunc</code> api</ul>

  2. <b>Create a FastAPI Application</b>
    <ul>Build an application to serve the model</ul>

  <pre><code>"""An example bare minimum FastAPI application."""
  
  <span style="color:blue"><b>from</b></span> fastapi <span style="color:blue"><b>import</b></span> FastAPI, HTTPException
  <span style="color:blue"><b>from</b></span> pydantic <span style="color:blue"><b>import</b></span> BaseModel
  <span style="color:blue"><b>import</b></span> numpy <span style="color:blue"><b>as</b></span> np
  <span style="color:blue"><b>import</b></span> mlflow

  app = FastAPI()

  MODEL_URI = "model_uri"

  <span style="color:blue"><b>class</b></span> <span style="color:purple"><b>PredictionRequest</b></span>(BaseModel):
      data: <span style="color:blue">list</span>

  <i># Load the MLFlow model at startup</i>
  model = mlflow.pytorch.load_model(MODEL_URI)

  @app.post("/predict")
  def predict(request: PredictionRequest):
      try:
          input_data = np.array(request.data)
          predictions = model(input_data)
          return {"predictions": predictions.tolist()}
      except Exception as err:
          raise HTTPException(status_code=500, detail=str(err))</code></pre>
  <br>
  3. <b>Containerize the FastAPI Application</b>

  <ul>- List the requirements in a requirements.txt file or using poetry</ul>

  <ul>- Create a Docker image for the FastAPI application with the requirements preinstalled</ul>

  <ul>- Ensure you are exposing the relevant ports and running the app when the container launches using something similar</ul>

  <code>EXPOSE 80</code>
  <br>
  <code>CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80"]</code>
  <br>
  <br>
  4. <b>Deploy the Docker Container to Kubernetes</b>

  <ul>- Use Kubernetes to deploy and manage the container probably using the same KServe method mentioned above</ul>
  </div>
</div>
<br>

### FastAPI - Summary
- Using web frameworks for building API endpoints is the straightforward way to serve models

- Not only MLFlow models, any models can be served using this approach

- Gets more control on the preprocessing and postprocessing here

- Time consuming to create consistent APIs

- Need to capture the dependencies separately for running the model

- Model and its specific versions need to be manually added to the 

- It is hard to automate the serving process

- Involves manual containerisation and then deploying to kubernetes

- Follows similar deployment process to other methods

<br>

## 3. BentoML for Model Serving

<blockquote class="callout callout_default">
    <a href="https://github.com/bentoml/BentoML" target="_blank">BentoML</a> is an open-source model serving library for building performant and scalable AI applications with Python. It comes with everything you need for serving optimization, model packaging, and production deployment.
</blockquote>

“Bentos” is an archive containing all the necessary components to package a model.

### BentoML - Model Serving Runtime
- Manually create a model serving runtime container using the following steps
  - Install BentoML and create a service
  - Build the Bento with your model and service
  - Containerize the Bento using bentoml containerize
  - Push the Docker image to GHCR
- Model loading and inference related logic need to be implemented

### BentoML - Model Serving Platforms
- BentoML recommends [Bento Cloud](https://docs.bentoml.com/en/latest/bentocloud/get-started.html){:target="_blank"} ([a paid service](https://www.bentoml.com/pricing){:target="_blank"}) to deploy models in a kubernetes native manner
- But similar model serving platforms like Seldon Core or KServe (open source) can be used here


### BentoML - Deploying MLFlow model to Kubernetes
<div id="myContainer" class="container">
  <a onclick="toggleContentsS_Ben_Deploy()"><img src="https://www.svgrepo.com/show/305143/arrow-ios-forward.svg" width="15px" height="15px"> BentoML - Deploying MLFlow model to Kubernetes</a>
  <div id="myContentsS_Ben_Deploy" class="contents">
  <br>
  
  1. Install BentoML and Dependencies
  <br>
  <code>pip install bentoml</code>
  <br>
  <br>
  2. Create a BentoML Service
  <br>
  <br>
  Create a BentoML service for your model. Basically wrap the model with an api endpoint similar to the process of doing so using FastAPI. A sample not tested code;
  <br>
  <br>
  <pre><code> <i># sample_service.py</i>
  <br>
  <span style="color:blue"><b>import</b></span> bentoml
  <span style="color:blue"><b>import</b></span> mlflow
  <span style="color:blue"><b>from</b></span> transformers <span style="color:blue"><b>import</b></span> pipeline
  <br>
  model_artefact_path = "model_uri"
  <br>
  model_uri = mlflow.get_artifact_uri(model_artefact_path)
  bento_model = bentoml.mlflow.import_model(
      'mlflow_pytorch_mnist',
      model_uri,
      signatures={'predict': {'batchable': True}}
  )
  <br>
  @bentoml.service(
      resources={"cpu": "2"},
      traffic={"timeout": 10},
  )
  <span style="color:blue"><b>class</b></span> <span style="color:purple">Summarization</span>:
      <span style="color:blue"><b>def</b></span> __init__(self) -> <span style="color:blue">None</span>:
          # Load model into pipeline
          self.model = bento_model
          <br>
      @bentoml.api
      def predict(self, data: str) -> str:
          input_data = np.array(data)
          predictions = self.model(input_data)
          return {"predictions": predictions.tolist()}</code></pre>
  <br>
  3. Build the Bento for the service:
  <br>
  <code>bentoml build -f sample_service.py</code>
  <br>
  <br>
  4. Containerize the Bento - Use BentoML to containerize the built Bento:
  <br>
  <code>bentoml containerize sample_model:latest</code>
  <br>
  <br>
  This command builds a Docker image for the BentoML service.
  <br>
  Now the Docker Container can be run locally
  <br>
  <code>docker run -p 3000:3000 sample_model:latest</code>
  <br>
  <br>
  5. Deploy to Kubernetes with KServe
  <ul>Create a KServe InferenceService YAML file and deploy to kubernetes.</ul>
  <br>
  Here are the advantages and limitations of BentoML as per neptune.ai
  <br>
  <br>
  Advantages:

  <ul><b>Ease of use:</b> BentoML is one of the most straightforward frameworks to use. Since the release of 1.2, it has become possible to build a Bento with a few lines of code.</ul>

  <ul><b>ML Framework support:</b> BentoML supports all the leading machine learning frameworks, such as PyTorch, Keras, TensorFlow, and scikit-learn.</ul>

  <ul><b>Concurrent model execution:</b> BentoML supports fractional GPU allocation (linked in Resources). In other words, you can spawn multiple instances of a model on a single GPU to distribute the processing.</ul>

  <ul><b>Integration:</b> BentoML comes with integrations for ZenML, Spark, MLflow, fast.ai, Triton Inference Server, and more.</ul>

  <ul><b>Flexibility:</b> BentoML is “Pythonic” and allows you to package any pre-trained model that you can import with Python, such as Large Language Models (LLMs), Stable Diffusion, or CLIP.</ul>

  <ul><b>Clear documentation:</b> The documentation is easy to read, well-structured, and contains plenty of helpful examples.</ul>

  <ul><b>Monitoring:</b> BentoML integrates with ArizeAI and Prometheus metrics.</ul>
  <br>
  Key limitations:

  <ul><b>Requires extra implementation:</b> As BentoML is “Pythonic,” you are required to implement model loading and inference methods on your own.</ul>

  <ul><b>Native support for high-performance runtime:</b> BentoML runs on Python. Therefore, it is not as optimal as Tensorflow Serving or TorchServe, both of which run on backends written in C++ that are compiled to machine code. However, it is possible to use the ONNX Python API to speed up the inference time.</ul>
  </div>
</div>
<br>

### BentoML - Summary
- Supports multiple ML frameworks
- Gets more control on the preprocessing and postprocessing here similar to FastAPI
- Time consuming to create consistent APIs but with pre and post processing
- Optimised model serving docker
- Follows similar deployment process to other methods

## Summary Table

Feature | MLFlow | FastAPI | BentoML
--- | --- | --- | ---
Ease of Implementation | Very easy | Easy | Easy
--- | --- | --- | ---
Compatibility with SKlearn and PyTorch | Fully compatible | Fully compatible| Fully compatible
--- | --- | --- | ---
Integration with MLFlow | Native | Need to do manually - Just need to get the model from the MLFlow and use it locally within the FastAPI app | Has MLFLow integration
--- | --- | --- | ---
Dependency management | Yes | Manual | Yes, can do it with the [MLFlow integration](https://docs.bentoml.com/en/1.1/integrations/mlflow.html#additional-tips){:target="_blank"}
--- | --- | --- | ---
Additional components or things to consider | Install either via MLServer (`pip install mlflow[extras]`) or KServe to the Kubernetes cluster | Manually bind dependencies and model versions to a container; Install Kserve to the kubernetes cluster | Install bentoml using `pip install bentoml`; Install Kserve to the kubernetes cluster; NO need to follow [Yatai based installation](https://docs.yatai.io/en/latest/concepts/architecture.html#yatai-architecture){:target="_blank"} if we are using bentoML just for model serving runtime creation
--- | --- | --- | ---
Integration with Kubernetes | Flawless integration with KServe and Seldon Core | Easy integration once we have the container ready with any kubernetes deployment platform | Flawless integration
--- | --- | --- | ---
Recommended | Yes | Can be considered | Yes

<br>
<blockquote class="callout callout_default">
<span class="callout-icon">💭</span>
    <br>
    <br>
    What is recommended?
    <br>
    <br>
    It is better to start with MLFlow based deployment. Once things are in place, or time permits, or if we think the need to include preprocessing steps along with model loading and inference, we could move to the BentoML based approach.
    <br>
    <br>
    This decision is mainly because of the simplicity of the serving option that MLFlow provides and the additional learning/knowledge that BentoML requires. Other than that, the complexities look similar as per the preliminary check.
    <br>
    <br>
    <b>What needs to be changed when moving from mlflow to bentoml later?</b>
    <ul>A bentoml service needs to be written with a consistent endpoint</ul>
      <ul>Need to ensure model versions and dependencies are correctly packed</ul>
    <ul>Create a docker file using bentoml cli instead of mlflow cli</ul>
    <ul>Point the deployment services to use the new docker</ul>
</blockquote>
<br>

---

<br>
<blockquote class="callout callout_warn">
<span class="callout-icon">⚠️</span>
    <br>
    <br>
    Currently, the preprocessing pipeline used in the model training is just being saved locally during the training as an artefact. If we want to use the exact same preprocessing pipeline for inference, we may need to look for an option to log that artefact along with the model, pull it and use it before the inference. Once we have clarity on how is the deployment happening, this can be done without much difficulty.

</blockquote>
<br>

## Questions:

1 - Decision between KServe or Seldon core - Which one is more suitable for our use case?
<br>

  - A comparison - [KServe vs. Seldon Core - Superwise ML Observability](https://superwise.ai/blog/kserve-vs-seldon-core/){:target="_blank"}
  <br>

  - KServe is open source whereas [SeldonCore](https://www.seldon.io/pricing){:target="_blank"} is expensive. And so is [BentoCloud](https://www.bentoml.com/pricing){:target="_blank"}.

## Resources

1. MLFlow serving [Deploy MLflow Model to Kubernetes — MLflow 2.15.1 documentation](https://mlflow.org/docs/latest/deployment/deploy-model-to-kubernetes/index.html){:target="_blank"} 

2.  [Deploying Models to KServe](https://mlflow.org/docs/latest/deployment/deploy-model-to-kubernetes/tutorial.html#step-7-deploying-the-model-to-kserve){:target="_blank"}

3. Kserve - [Home - KServe Documentation Website](https://kserve.github.io/website/latest/){:target="_blank"}

4. Kserve using MLFlow models - [MLFlow - KServe Documentation Website](https://kserve.github.io/website/latest/modelserving/v1beta1/mlflow/v2/){:target="_blank"}

3. [FastAPI](https://fastapi.tiangolo.com/){:target="_blank"} 

4. [FastAPI vs Flask: Comparison Guide for Data Science Enthusiasts](https://analyticsindiamag.com/developers-corner/fastapi-vs-flask-comparison-guide-for-data-science-enthusiasts/){:target="_blank"}

5. [KubeFlow serving options](https://www.kubeflow.org/docs/external-add-ons/serving/overview/){:target="_blank"}

6. KServe installation - [GitHub - kserve/kserve: Standardized Serverless ML Inference Platform on Kubernetes](https://github.com/kserve/kserve#hammer_and_wrench-installation){:target="_blank"}

7. [Best Tools For ML Model Serving](https://neptune.ai/blog/ml-model-serving-best-tools){:target="_blank"}

8. MLFlow BentoML - [MLflow](https://docs.bentoml.com/en/1.1/integrations/mlflow.html){:target="_blank"}

9. BentoML MLFlow dependency management - [MLflow additional tips](https://docs.bentoml.com/en/1.1/integrations/mlflow.html#additional-tips){:target="_blank"}

10. [BentoML fractional GPU allocation](https://github.com/bentoml/BentoML/blob/main/src/_bentoml_impl/server/allocator.py){:target="_blank"}