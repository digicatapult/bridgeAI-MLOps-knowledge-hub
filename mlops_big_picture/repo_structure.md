---
layout: default
title: BridgeAI MLOps Knowledge Hub
---

## Project Repository Usage Guide

### Introduction

This page was designed to give users an in-depth walkthrough of how to set up each repository that acts as a component of our architecture. It begins with the GitOps infrastructure setup, then details the setup process for the data ingestion, model training, model deployment, prediction service, and drift monitoring components of the team's architecture.

### Stage 1

To use the toolbox to run the example MLOPs pipeline, we should start with the infrastructure repo.

For local [Kind](https://kind.sigs.k8s.io/){:target="_blank"} infrastructure, use the repo [bridgeAI-gitops-infra](https://github.com/digicatapult/bridgeAI-gitops-infra){:target="_blank"}. The below are a summary of the steps extracted from the [README](https://github.com/digicatapult/bridgeAI-gitops-infra/tree/main/flux){:target="_blank"} of the repo. Go through the README for details.
<br>
<br>

**1.1** Install the prerequisites mentioned [here](https://github.com/digicatapult/bridgeAI-gitops-infra/tree/main/flux){:target="_blank"} in the readme of above repo.
- For installation on MAC if using homebrew the installation link is below:
    - [Install Homebrew](https://mac.install.guide/homebrew/3){:target="_blank"} 

- Once brew is installed use the command below to install the required software’s. This will install all the prerequisite softwares:
    - `brew install kind kubectl fluxcd/tap/flux@2.2 gnupg jq gh`

- Install Docker for mac using [this link](https://docs.docker.com/desktop/install/mac-install/){:target="_blank"} for Mac. Use the recommended option. Be sure you have admin rights when doing this.

Docker should be up and running as can be seen in the green bar in the bottom left corner.

<img src="./assets/docker_interface.png">

<br>
<br>

**1.2** Setup a CLASSIC github personal access token that has `repo` and `package:read` permissions

In your GitHub account, go to Settings > Developer settings > Personal access tokens > Tokens (classic), and select "Generate new token", then “Generate new token (classic)”.

When you go to generate a new classic token, you should see a list of permissions. Fill it as per the image below.

<img src="./assets/PAT_help.png">

<br>
<br> 

Once this is done clone your git repo and export the token generated above to your repo using below commands in 1.3.

**1.3** From the terminal, clone your repo and set the `GITHUB_TOKEN` variable: 
1. `git clone https://github.com/digicatapult/bridgeai-gitops-infra`
2. `cd bridgeai-gitops-infra`
3. `export GITHUB_TOKEN=<your github token>`

<br>

**1.4** Select the GitOps branch you wish to track and run `./flux/scripts/install-flux.sh -b <branch>`.

Once your on your branch make sure docker is up and running and run below scripts:

`./scripts/add-kind-cluster.sh`

`./scripts/install-flux.sh`

Once the above have completed, you will be able to access the following


<table>
  <tr>
    <th>Name</th>
    <th>Link</th>
    <th>Notes</th>
  </tr>

  <tr>
    <td>AirFlow UI [local KIND cluster]</td>
    <td>http://localhost:3080/airflow</td>
    <td>Username: admin Password: admin</td>
  </tr>

  <tr>
    <td>MLFlow UI [local KIND cluster]</td>
    <td>http://localhost:3080/mlflow</td>
    <td>No credentials needed. <br><br> MLFLOW_TRACKING_URI that need to be set at client side is http://localhost:3080/</td>
  </tr>

  <tr>
    <td>MinIO [local KIND cluster]</td>
    <td>http://127.0.0.1:9001</td>
    <td>Run <code>kubectl port-forward svc/mlflow-minio 9001 -n default</code> before trying to access the UI. <br><br> Username: admin Password: password</td>
  </tr>
  </table>
<br>


If After running the flux script if you get an <span style="color:#8C1437"><b>error</b></span> then check your version of flux and uninstall it, delete all clusters and rerun both scripts.

1. `brew install fluxcd/tap/flux@2.2`

2. `kind delete clusters bridgeai-gitops-infra`

After running these rerun both scripts

1. `./scripts/add-kind-cluster.sh`

2. `./scripts/install-flux.sh`

Once this is successfully done run the URLs in the table above to check if they are functional.
<br>
<br>

The next stages involve using the AirFlow UI to trigger the DAGs in the right order.

<br>

## Stage 2 - Data Ingestion
Before you begin, et the right airflow variables required for the DAG. The defaults are listed [here](https://github.com/digicatapult/bridgeAI-airflow-DAGs/tree/main/dags/regression_data_ingestion){:target="_blank"}. Do this only if you are installing airflow for the first time from the repo directly. 

**2.1** For local installation when following steps above just add the two variables below. You can check how to add variables from [Airflow's Documentation](https://airflow.apache.org/docs/apache-airflow/stable/howto/variable.html){:target="_blank"}.

1. `mlflow_tracking_username` = `mlflow-prod-user`

2. `mlflow_tracking_password` = `password`

**2.2** Trigger the `data_ingestion_dag` from the airflow UI. The source code that this DAG uses is from [this](https://github.com/digicatapult/bridgeAI-regression-model-data-ingestion/){:target="_blank"} repository.

**2.3** Note - you can monitor the tasks in the DAG, the logs etc from the UI while it is running.

**2.4** Once the DAG execution has completed, you are expected to see a new data version like `data-v1.3.0`  in the [Tags section of the repository](https://github.com/digicatapult/bridgeAI-regression-model-data-ingestion/tags){:target="_blank"}.

**2.5** Make sure the new data version is configured in the data_version variable to the new data version in step 2.4 after the DAG has executed. **This may change for multiple users on local only depending on their clusters and it would have to be updated accordingly.**

<br>

## Stage 3 - Model Training
Set the right airflow variables required for the DAG. The defaults are listed [here](https://github.com/digicatapult/bridgeAI-airflow-DAGs/tree/main/dags/regression_model_training){:target="_blank"}.

**3.1** Trigger the `model_training_dag` from the airflow UI. The source code that this DAG uses is from [this](https://github.com/digicatapult/bridgeAI-regression-model-training){:target="_blank"} repository.

**3.2** You can monitor the tasks in the DAG, the logs etc from the UI while it is running.

**3.3** Once the model training has been completed, the experiment must be available in the MLFlow UI.

**3.4** You can register the model and promote the model etc using the MLFlow UI. Refer the demo recording for details.

<br>

## Stage 4 - Preparing the Model for Deployment
Set the right airflow variables required for the DAG. The defaults are listed [here](https://github.com/digicatapult/bridgeAI-airflow-DAGs/tree/main/dags/generate_model_image_to_deploy){:target="_blank"}.

**4.1** Trigger the `create_model_image_to_deploy_dag` from the airflow UI. The source code that this DAG uses is from [this](https://github.com/digicatapult/bridgeAI-model-baseimage){:target="_blank"} repository.

**4.2** You can monitor the tasks in the DAG, the logs etc from the UI while it is running.

**4.3** Once this DAG execution is completed, the model image will be pushed to the container registry.

<br>

<b>Pushing images to dockerhub registry from local KIND cluster</b>

1. Create a [dockerhub](https://hub.docker.com/){:target="_blank"} account if you don’t have one.
2. Create an [access token](https://docs.docker.com/security/for-developers/access-tokens/){:target="_blank"}.
3. Create a Kubernetes secret with the name `ecr-credentials`.



<pre><code>kubectl create secret docker-registry ecr-credentials \
                --namespace=default \
                --docker-server=https://index.docker.io/v1/ \
                --docker-username=dockerhub_username \
                --docker-password=dckr_pat_token</code></pre>

<br>

4. If an earlier same named secret exists, you can delete it using `kubectl delete secret ecr-credentials -n default`. Once created verify that it exists by `kubectl describe secret ecr-credentials -n default`.

5. Before running the DAG `create_model_image_to_deploy_dag`, modify the airflow variable `docker_registry_for_model_image` to the dockerhub username that used to create the secret.

6. Now you should be able to run the dag and see the updated docker image getting pushed to the name `mlflow_built_image_name` , and tag `mlflow_built_image_tag` specified in the airflow variable.

<br>

## Stage 5 - Model Deployment

<!-- this section is a WIP. -->

We use the above generated image to deploy the model using [Kserve](https://kserve.github.io/website/latest/){:target="_blank"}. You need not update the image name or tag unless it is required to do so. Otherwise, it will deploy the specified image with the `latest` tag. To do the deployment, it is essentially running the kubernetes command `kubectl apply -f kserve-inference.yaml`, where the `kserve-inference.yaml` looks like below.



<pre><code>apiVersion: "serving.kserve.io/v1beta1"
kind: "InferenceService"
metadata:
  name: "house-price"
  annotations:
      serving.kserve.io/deploymentMode: RawDeployment
      serving.kserve.io/disableIngressCreation: "true"
      serving.kserve.io/disableIstioVirtualHost: "true"
spec:
  predictor:
    minReplicas: 1
    maxReplicas: 1
    containers:
      - name: "house-price"
        image: "058264114863.dkr.ecr.eu-west-2.amazonaws.com/bridgeai-mlops:latest"
        ports:
          - containerPort: 8080
            protocol: TCP
        env:
          - name: PROTOCOL
            value: "v2"
        resources:
          requests:
            memory: "4Gi"
            cpu: "2"
          limits:
            memory: "5Gi"
            cpu: "4"</code></pre>
 

<br>

Note: If you are using local KIND cluster, you might need to use the dockerhub image that you set <span style="color:#8C1437">previously</span>. You should use `image: <dockerhub_username>/<mlflow_built_image_name>:<mlflow_built_image_tag>`, rather than using `image: "058264114863.dkr.ecr.eu-west-2.amazonaws.com/bridgeai-mlops:latest"`.

<br>

## Stage 6 - Prediction Service
<!-- This is still work in progress. Once done, you will be able to access the swagger UI of the prediction service without going through the below steps. -->

Unlike most of the other stages, this one is not a DAG. You need to refer to this repo [here](https://github.com/digicatapult/bridgeAI-prediction-service){:target="_blank"} for the source code and instructions.

**6.1** Clone the repo: `git clone https://github.com/digicatapult/bridgeAI-prediction-service`

**6.2** Since the backend database needed for this is not yet available on your local system, run `docker compose up -d` from the **root** of the above cloned directory.

**6.3** Follow the instructions provided in the [README](https://github.com/digicatapult/bridgeAI-prediction-service?tab=readme-ov-file#how-to-start-the-service){:target="_blank"} on how to start the service.

Now you will be able to access the swagger ui and query the model deployed at `http://localhost:8000/swagger`.

<br>

## Stage 7 - Drift Monitoring
Set the right airflow variables required for the DAG. The defaults are listed [here](https://github.com/digicatapult/bridgeAI-airflow-DAGs/tree/main/dags/drift_monitoring){:target="_blank"}.

Note that you may need two different versions of the data to generate the drift report, the default values indeed point to two different versions of the data tagged with `data-v1.0.0` and `data-v1.1.0` which are generated using the source data [old](https://raw.githubusercontent.com/renjith-digicat/random_file_shares/main/HousingData-old.csv){:target="_blank"} and [new](https://raw.githubusercontent.com/renjith-digicat/random_file_shares/main/HousingData-new.csv){:target="_blank"}, respectively.

**7.1** Trigger the `drift_monitoring_dag` from the airflow UI. The source code that this DAG uses is from [this](https://github.com/digicatapult/bridgeAI-drift-monitoring){:target="_blank"} repository.

**7.2** You can monitor the tasks in the DAG, the logs etc from the UI while it is running.

**7.3** Once you are done with this DAG execution, the report will be uploaded in the specified S3 bucket. For the local KIND cluster, it is the MinIO bucket which can be found at the `evidently-reports` by default.

**7.4** You can download the HTML [drift](https://www.evidentlyai.com/ml-in-production/concept-drift){:target="_blank"} report generated using [evidently](https://www.evidentlyai.com/){:target="_blank"}.

<br>

## FAQs
1. The infrastructure code has been successfully executed, but the airflow/mlflow UIs are not yet available, what should I do?
    - Wait for some more time as the kubernetes pods are getting created for the same. You can inspect the pods status by running `kubectl get pods` from the terminal. To get the events from the cluster, run `kubectl events --watch`.

2. How to register/promote/add alias to a model in MLFlow?
    - You can use the MLFlow UI to do that. For more details refer the official documentation or follow the instructions in the demo recordings. Official documentation for MLflow's model registry is linked [here](https://mlflow.org/docs/latest/model-registry.html#:~:text=To%20set%20aliases%20and%20tags,in%20the%20model%20verison%20table.){:target="_blank"}.

3. How to set airflow variables?
    - Follow the instructions here to set the airflow variables using the UI (documentation linked [here](https://www.astronomer.io/docs/learn/airflow-variables#:~:text=Using%20the%20Airflow%20UI%E2%80%8B,Import%20Variables%20from%20a%20file.){:target="_blank"}), or follow the demo recordings. 