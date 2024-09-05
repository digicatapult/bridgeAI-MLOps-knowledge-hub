---
layout: default
---

1. Relevant skills and roles
2. Understanding of architecture components (horizon scan with links to other pages/repos on MLOps architecture)

# Architecture Overview

The components of an MLOps workflow, otherwise known as its architecture, vary depending on the scope and restraints of a given project. Generally, the following components make up the average MLOps workflow:

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

### Design Decisions: 
For the Pre-built MLOps pipeline created by the team, a deploy-as-model approach was taken. As such, the architecture followed by the team comprises a model registry with human intervention for stage tags, model deployment, model monitoring, data storing and retrieval, and finally data and feature engineering.

It is important to note that the components and workflow differ; the components themselves comprise the architecture, but the workflow (the order in which the components are used to create an MLOps pipeline) can vary. For further insight on the typical structure of an MLOps workflow, you can refer to the following resources:
* [MLOps Stack Canvas](https://ml-ops.org/content/mlops-stack-canvas)
* [MLOps Architecture Guide](https://neptune.ai/blog/mlops-architecture-guide)
* [MLOps Workflow by Databricks](https://docs.databricks.com/en/machine-learning/mlops/mlops-workflow.html)


# Model training and registry

Tool | Description | Scalability | Cost Effectiveness | Flexibility | Accessibility | Integrated Features
--- | --- | --- | --- | --- | --- | ---
MLflow | MLflow is a versatile, expandable, open-source platform for managing workflows and artifacts across the machine learning lifecycle | Supports distributed training and can scale with underlying infrastructure eg Kubernetes | Open-source allows for more control over expenses; depends on underlying infrastructure | Modular design with components for tracking experiments, packaging artifacts into reproducible runs and deploying models; scalable depending on underlying infrastructure | Platform-agnostic; supports multiple languages and frameworks | Stage transition tags; model lineage; model file versioning; model packaging 
--- | --- | --- | --- | --- | --- | ---
AWS Sagemaker | Amazon SageMaker is a fully managed machine learning (ML) service. With SageMaker, data scientists and developers can quickly and confidently build, train, and deploy ML models into a production-ready hosted environment | Fully managed and automatically scales to handle large datasets and complex models | PAYG model; comes with automatic model tuning to optimise costs | Supports multiple frameworks and offers built-in algorithms and jupyter notebooks for development | Fully integrated with AWS, allowing for ease of utilisation of other AWS services | No stage transition tags; limited model lineage; model file versioning; limited model packaging
