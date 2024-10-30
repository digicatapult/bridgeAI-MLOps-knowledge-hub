---
layout: default
title: BridgeAI MLOps Knowledge Hub
---


## Relevant Skills and roles

### Table of Contents
1. [Roles](#roles)
2. [Skills](#skills)
3. [Architecture Overview](#architecture-overview)
4. [Design Decisions](#design-decisions)
5. [Horizon Scan](#horizon-scan)
  - [Data Store and Retrieval](#data-store-and-retrieval)
  - [Data and Feature Engineering](#data-and-feature-engineering)
  - [Model Training and Registry](#model-training-and-registry)
  - [Model Deployment and Serving](#model-deployment-and-serving)
  - [Model Monitoring](#model-monitoring)
  - [GitOps](#gitops)
  - [Horizon Scan Embed](#horizon-scan-embed)
6. [Resources](#resources)

### Roles

The roles required to create and deploy an MLOps pipeline can vary, though our team consists of:

- Data scientists
- Data analysts
- DevOps engineers
- Machine Learning Engineers
- Domain experts/business translators

### Skills

Required skills include knowledge of:

- Scripting languages (e.g. Python)
- Cloud solutions (e.g. AWS, Azure, GCP)
- CI/CD pipeline implementation and Infrastructure as Code (e.g. Terraform)
- Data stores (e.g. AWS S3)
- Machine learning algorithms (e.g. Logistic Regression) and frameworks (e.g. PyTorch, SK-Learn)
- DAG software (e.g. Airflow)
- Logging and monitoring tools (e.g. Evidently AI)
- Containerization (with Kubernetes, Docker)


## Architecture Overview

The components of an MLOps workflow, otherwise known as its architecture, can vary depending on the scope and restraints of a given project. 

Generally, the following components make up the average MLOps workflow:

1. Data store and retrieval
    * These can include databases for structured or unstructured data, data lakes, APIs and files (eg `.csv`, `.parquet`)

2. Data and feature engineering
    * This step involves the use of Directed Acyclic Graphs (DAGs) to group and automate tasks organised with dependencies and relationships dictating how they should run. These can come with timing intervals, timeouts, etc.

3. Model training and registry 
    * This step involves the use of relevant tools for model versioning, storage, testing, and eventually model deployment subject to approval. 
    * When different iterations of models are tested, the model, its data and its hyperparameters are stored for future reference. Model registries can also store information like metadata and the lineage of a given model.

4. Model deployment 
    * When the appropriate model is selected, it is then manually pushed to the model server to serve in production. Serving a model is the act of making it accessible to end users, typically via API.

5. Model monitoring
    * Upon a model being deployed, relevant tools are then used to monitor its performance and detect occurrences of model drift, and logging

## Design Decisions: 
For the pre-built MLOps pipeline created by the team, a [deploy-as-model](https://docs.databricks.com/en/machine-learning/mlops/deployment-patterns.html){:target="_blank"} approach was taken. As such, the architecture followed by the team comprises a model registry with human intervention for stage tags, model deployment, model monitoring, data storing and retrieval, and finally data and feature engineering.

It is important to note that the components and workflow differ; the components themselves comprise the architecture, but the workflow (the order in which the components are used to create an MLOps pipeline) can vary. For further insight on the typical structure of an MLOps workflow, you can refer to the following resources:
* [MLOps Stack Canvas](https://ml-ops.org/content/mlops-stack-canvas){:target="_blank"}
* [MLOps Architecture Guide](https://neptune.ai/blog/mlops-architecture-guide){:target="_blank"}
* [MLOps Workflow by Databricks](https://docs.databricks.com/en/machine-learning/mlops/mlops-workflow.html){:target="_blank"}


## Horizon Scan

Below are sets of comparisons for tools you can use for each component of your MLOps pipeline. The criteria for evaluation was derived using the team's [requirements](./mlops_big_picture/requirements_research.html){:target="_blank"}, which you may also wish to consider using for your own pipeline. Each horizon scan per component comes with the team's design decision for the component.

<!-- short paragraph on why a certain selection of tools for evaluation. -->

### Data Store and Retrieval

<div id="myContainer" class="container">
  <a onclick="toggleContentsPre_Store()"><img src="https://www.svgrepo.com/show/305143/arrow-ios-forward.svg" width="15px" height="15px"> Data Store and Retrieval</a>
  <div id="myContentsPre_Store" class="contents">
  <br>

  <table>
  <tr>
    <th></th>
    <th>AWS S3</th>
    <th>APIs</th>
    <th>Data Lakes</th>
    <th>Databases</th>
  </tr>

  <tr>
    <td><b>Description</b></td>
    <td>Amazon Simple Storage Service is an object storage service allowing users to store and protect any amount of data for a range of use cases, such as data lakes, backup and restore, and big data analytics</td>
    <td>An application programming interface is a way for two or more computer programs or components to communicate with each other. It is a type of software interface, offering a service to other pieces of software.</td>
    <td>A data lake is a system or repository of data stored in its natural/raw format, usually object blobs or files</td>
    <td>A database is an organised collection of data or a type of data store based on the use of a database management system, the software that interacts with end users, applications, and the database itself to capture and analyse the data.</td>
  </tr>

  <tr>
    <td><b>Scalability</b></td>
    <td>Highly scalable without human intervention</td>
    <td>Ability to enable scalable communication between systems</td>
    <td>Optimal for large amount of structured and unstructured data without predefined schemas</td>
    <td>NoSQL/cloud databases/etc are designed for scaling. Others not so much</td>
  </tr>

  <tr>
    <td><b>Cost Effectiveness</b></td>
    <td>PAYG model</td>
    <td>Option to reduce costs via modular system design for reuse of existing components/code</td>
    <td>Often more cost effective than DBs for storing large amounts of data</td>
    <td>Cloud based - PAYG</td>
  </tr>

  <tr>
    <td><b>Security</b></td>
    <td>Built in features including IAM policies and bucket policies, either can involve RBAC, keys, encryption</td>
    <td>Option to implement robust authentication (eg OAuth, API keys) and authorization mechanisms to control access to data</td>
    <td>Option to implement security measures like access controls and encryption</td>
    <td>User auth, RBAC, encryption</td>
  </tr>

  <tr>
    <td><b>Accessibility</b></td>
    <td>Data can be accessed from anywhere via HTTP/HTTPS, allowing for smooth data retrieval via APIs for features like real-time data retrieval. S3 can also  also centralised</td>
    <td>Supports real-time data retrieval and updates</td>
    <td>Centralised repository making data accessible to different teams within an organisation</td>
    <td>Optimized query engines and indexes for efficient data access; easy integration with most applications and BI tools</td>
  </tr>

  <tr>
    <td><b>Flexibility</b></td>
    <td>Agnostic to file types and other storage formats; high fault tolerance (99.9%); allows different software systems to communicate via APIs</td>
    <td>Allows different software systems to communicate regardless of underlying technology stack (via REST, SOAP)</td>
    <td>Store data in raw format across wide range of file types</td>
    <td>Supports various data models eg relational, document, key-value</td>
  </tr>

  </table>
  <br>
  <br>

  <b>Design decisions:</b>
  <br>

  The team chose Amazon S3 as the data storage system. Digital Catapult is already using AWS for a few other projects and our technologists are comfortable with this technology.
  <br>
  <br>
  An evaluation of feature store software the team considered using, and decided on, can be found in the Resources section of this page.

  </div>
</div>
<br>

### Data and Feature Engineering (Training) Pipeline
<div id="myContainer" class="container">
  <a onclick="toggleContentsPre_FeatEng()"><img src="https://www.svgrepo.com/show/305143/arrow-ios-forward.svg" width="15px" height="15px"> Data and Feature Engineering</a>
  <div id="myContentsPre_FeatEng" class="contents">
  <br>

  <table>

  <tr>
    <th></th>
    <th>Apache</th>
    <th>Prefect</th>
  </tr>

  <tr>
    <td><b>Description</b></td>
    <td>Airflow is an open source workflow orchestration tool used for orchestrating distributed applications. It works by scheduling jobs across different servers or nodes using DAGs (Directed Acyclic Graphs). A DAG is the core concept of Airflow, collecting Tasks together, organised with dependencies and relationships to say how they should run</td>
    <td>Prefect decreases negative engineering by building a DAG structure with an emphasis on enabling positive with an orchestration layer for the current data stack</td>
  </tr>

  <tr>
    <td><b>Cost Effectiveness</b></td>
    <td>Free</td>
    <td>Paid</td>
  </tr>

  <tr>
    <td><b>Flexibility</b></td>
    <td>Supports the creation of dynamic workflows through Directed Acyclic Graphs (DAGs), enabling users to define complex dependencies and task relationships. Also viable for retraining/A-B testing/CICD</td>
    <td>Python package that makes it easier to design, test, operate, and construct complicated data applications. It has a user-friendly API that doesn’t require any configuration files or boilerplate. It allows for process orchestration and monitoring using best industry practices.</td>
  </tr>

  <tr>
    <td><b>Scalability</b></td>
    <td>Ease for Helm chart setup.</td>
    <td>To run Prefect, the official Helm chart requires additional configurations to be setup.</td>
  </tr>

  </table>
  <br>

  </div>
</div>
<br>

### Model Training and Registry
<div id="myContainer" class="container">
  <a onclick="toggleContentsPre_TrainReg()"><img src="https://www.svgrepo.com/show/305143/arrow-ios-forward.svg" width="15px" height="15px"> Model Training and Registry</a>
  <div id="myContentsPre_TrainReg" class="contents">
  <br>

  <table>
  <tr>
    <th></th>
    <th>MLflow</th>
    <th>AWS SageMaker</th>
  </tr>

  <tr>
    <td><b>Description</b></td>
    <td>MLflow is a versatile, expandable, open-source platform for managing workflows and artifacts across the machine learning lifecycle</td>
    <td>Amazon SageMaker is a fully managed machine learning (ML) service. With SageMaker, data scientists and developers can quickly and confidently build, train, and deploy ML models into a production-ready hosted environment	</td>
  </tr>

  <tr>
    <td><b>Scalability</b></td>
    <td>Supports distributed training and can scale with underlying infrastructure eg Kubernetes</td>
    <td>Fully managed and automatically scales to handle large datasets and complex models.</td>
  </tr>

  <tr>
    <td><b>Cost Effectiveness</b></td>
    <td>Open-source allows for more control over expenses; depends on underlying infrastructure</td>
    <td>PAYG model; comes with automatic model tuning to optimise costs</td>
  </tr>

  <tr>
    <td><b>Flexibility</b></td>
    <td>Modular design with components for tracking experiments, packaging artifacts into reproducible runs and deploying models; scalable depending on underlying infrastructure.</td>
    <td>Supports multiple frameworks and offers built-in algorithms and jupyter notebooks for development.</td>
  </tr>

  <tr>
    <td><b>Accessibility</b></td>
    <td>Platform-agnostic; supports multiple languages and frameworks</td>
    <td>Fully integrated with AWS, allowing for ease of utilisation of other AWS services</td>
  </tr>

  <tr>
    <td><b>Integrated Features</b></td>
    <td>Stage transition tags; model lineage; model file versioning; model packaging</td>
    <td>No stage transition tags; limited model lineage; model file versioning; limited model packaging</td>
  </tr>
  </table>

  </div>
</div>
<br>


### Model Deployment and Serving
<div id="myContainer" class="container">
  <a onclick="toggleContentsPre_DeplServ()"><img src="https://www.svgrepo.com/show/305143/arrow-ios-forward.svg" width="15px" height="15px"> Model Deployment and Serving</a>
  <div id="myContentsPre_DeplServ" class="contents">
  <br>

  <table>
  <tr>
    <th></th>
    <th>MLflow</th>
    <th>BentoML</th>
    <th>FastAPI</th>
  </tr>

  <tr>
    <td><b>Description</b></td>
    <td>MLflow is a versatile, expandable, open-source platform for managing workflows and artifacts across the machine learning lifecycle</td>
    <td>BentoML is a model serving framework for building AI applications with Python. It can be installed as a library with pip, or through Yatai for Kubernetes. Yatai is the Kubernetes deployment operator for BentoML.</td>
    <td>FastAPI is a modern, fast (high-performance), web framework for building APIs with Python based on standard Python type hints.</td>
  </tr>

  <tr>
    <td><b>Model Dependency Management</b></td>
    <td>Seamless</td>
    <td>Yes, through MLflow integration</td>
    <td>Manual</td>
  </tr>

  <tr>
    <td><b>Compatibility with SKLearn and PyTorch</b></td>
    <td>Fully compatible with both</td>
    <td>Fully compatible with both</td>
    <td>Fully compatible with both</td>
  </tr>

  <tr>
    <td><b>Flexibility</b></td>
    <td>Flawless integration via KServe for Kubernetes</td>
    <td>Same as MLflow, via BentoCloud.</td>
    <td>Seamless once container set up through any Kubernetes deployment platform.</td>
  </tr>
  </table>

  </div>
</div>
<br>

### Model Monitoring
<div id="myContainer" class="container">
  <a onclick="toggleContentsPre_Monit()"><img src="https://www.svgrepo.com/show/305143/arrow-ios-forward.svg" width="15px" height="15px"> Model Monitoring</a>
  <div id="myContentsPre_Monit" class="contents">
  <br>

  <table>
  <tr>
    <th></th>
    <th>Evidently.AI</th>
    <th scope="col" colspan="2">Prometheus & Grafana</th>
  </tr>

  <tr>
    <td><b>Description</b></td>
    <td>Evidently.ai, a powerful open-source tool, simplifies ML Monitoring by providing pre-built reports and test suites to track data quality, data drift, and model performance</td>
    <td>Prometheus is an open-source systems monitoring and alerting toolkit originally built at SoundCloud. Prometheus collects and stores its metrics as time series data, i.e. metrics information is stored with the timestamp at which it was recorded, alongside optional key-value pairs called labels.</td>
    <td>Grafana is a multi-platform open source analytics and interactive visualization web application. It can produce charts, graphs, and alerts for the web when connected to supported data sources.</td>
  </tr>

  <tr>
    <td><b>Hardware metrics</b></td>
    <td>Yes</td>
    <td scope="row" colspan="2" class="centered">Limited, for both</td>
  </tr>

  <tr>
    <td><b>Model performance in production</b></td>
    <td>Yes</td>
    <td scope="row" colspan="2" class="centered">No, for both</td>
  </tr>
  </table>

  </div>
</div>
<br>

### GitOps
<div id="myContainer" class="container">
  <a onclick="toggleContentsPre_GitOps()"><img src="https://www.svgrepo.com/show/305143/arrow-ios-forward.svg" width="15px" height="15px"> GitOps</a>
  <div id="myContentsPre_GitOps" class="contents">
  <br>

  <table>
  <tr>
    <th></th>
    <th>Argo CD</th>
    <th>Flux</th>
  </tr>

  <tr>
    <td><b>Description</b></td>
    <td>Argo CD is a declarative, GitOps continuous delivery tool for Kubernetes.</td>
    <td>Flux is a set of continuous and progressive delivery solutions for Kubernetes that are open and extensible.</td>
  </tr>

  <tr>
    <td><b>Architecture</b></td>
    <td>Standalone application with a built-in UI and dashboard.</td>
    <td>Set of controllers that run within Kubernetes.</td>
  </tr>

  <tr>
    <td><b>User interface</b></td>
    <td>Yes</td>
    <td>More CLI-centric</td>
  </tr>

  <tr>
    <td><b>Security</b></td>
    <td>Role-Based Access Control (RBAC) function, single sign-on (SSO), and multi-user support.</td>
    <td>RBAC function, selective resource access, and SSO provisions.</td>
  </tr>
  </table>

  </div>
</div>
<br>

### Horizon Scan Embed

<div id="myContainer" class="container">
  <a onclick="toggleContents_PDF_Embed()"><img src="https://www.svgrepo.com/show/305143/arrow-ios-forward.svg" width="50px" height="15px"> Horizon Scan</a>
  <div id="myContents_PDF_Embed" class="contents">
    <iframe src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSxWt7W4SBFvWG4oS91RtQ6-HVzMMNvw7b5IgqwShkeqbqFaZvBp6ElhCexbDv2cg/pubhtml?gid=2066554602&amp;single=true&amp;widget=true&amp;headers=false" width="780" height="1100"></iframe>
  </div>
</div>

<!-- <embed src="./assets/horizon_scan.pdf" width="780" height="1100"> -->

## Resources

1. [Feature store software evaluation and decision](./mlops_big_picture/versioning.html){:target="_blank"}

1. [Neptune.ai](https://neptune.ai/blog/mlops-engineer){:target="_blank"}

2. [MLOps.org](https://ml-ops.org/){:target="_blank"}

3. [Databricks Docs](https://docs.databricks.com/){:target="_blank"}

4. [Prometheus](https://prometheus.io/){:target="_blank"}

5. [Grafana](https://grafana.com/){:target="_blank"}

6. [AWS](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html){:target="_blank"}

7. [Evidently AI](https://www.evidentlyai.com/){:target="_blank"}

8. [BentoML](https://www.bentoml.com/){:target="_blank"}

9. [MLflow](https://mlflow.org/){:target="_blank"}

10. [Airflow](https://airflow.apache.org/){:target="_blank"}

11. [Prefect](https://www.prefect.io/){:target="_blank"}

12. [What is an API?](https://aws.amazon.com/what-is/api/){:target="_blank"}

13. [What is a data lake?](https://www.snowflake.com/guides/what-data-lake/){:target="_blank"}

14. [What is a database?](https://www.oracle.com/in/database/what-is-database/){:target="_blank"}

15. [Argo vs Flux](https://blog.aenix.io/argo-cd-vs-flux-cd-7b1d67a246ca){:target="_blank"}