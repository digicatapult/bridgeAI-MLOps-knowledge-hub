---
layout: default
title: BridgeAI MLOps Knowledge Hub
---

# Training Pipeline Content

**Table of Contents**
1. [Introduction](#1-introduction)
2. [Team Implementation](#2-team-implementation)
3. [Evaluation](#3-evaluation)\
        [Apache Airflow](#apache-airflow)\
        [Prefect](#prefect)
4. [Resources](#resources)

<br>

## 1. Introduction

The team chose Airflow as its [DAG](https://airflow.apache.org/docs/apache-airflow/stable/core-concepts/dags.html){:target="_blank"} implementation software because it is:

- Widely used in the community based on the GitHub stars of a repository (denoting the quality of a project)
- Being contributed to by more users (reflected in Forks of repositories)
- Straightforward to set up: [Helm Chart for Apache Airflow — helm-chart Documentation](https://airflow.apache.org/docs/helm-chart/stable/index.html){:target="_blank"}

<p>On the other hand, to run Prefect the official Helm chart requires additional configurations to be setup: <a href="https://docs.prefect.io/3.0/get-started/index" target="_blank">Welcome to Prefect - Prefect</a></p>

**Note:** Kubeflow does not have an official Helm chart. 

<br>

## 2. Team Implementation

Each of the links below will direct you to one of our repos for each process, which comes with a `README` to direct you on how to set up each process:

➡️ [Testing DAGs on Local Kind Cluster](https://github.com/digicatapult/bridgeAI-airflow-DAGs){:target="_blank"}

➡️ [Data Ingestion DAG](https://github.com/digicatapult/bridgeAI-airflow-DAGs/blob/main/dags/regression_data_ingestion/README.md){:target="_blank"}

➡️ [Model Training DAG](https://github.com/digicatapult/bridgeAI-airflow-DAGs/blob/main/dags/regression_model_training/README.md){:target="_blank"}

➡️ [Drift Monitoring DAG](https://github.com/digicatapult/bridgeAI-airflow-DAGs/blob/main/dags/drift_monitoring/README.md){:target="_blank"}

<br>

## 3. Evaluation

### Apache Airflow

<blockquote class="callout callout_definition">
<span class="callout-icon">📓</span>
    <br>
    <br>
    Airflow is an open source workflow orchestration tool used for orchestrating distributed applications. It works by scheduling jobs across different servers or nodes using DAGs (Directed Acyclic Graphs). A DAG is the core concept of Airflow, collecting Tasks together, organised with dependencies and relationships to say how they should run.
</blockquote>

\
**Features**
- Free
- Ease for Helm chart setup
- supports the creation of dynamic workflows through Directed Acyclic Graphs (DAGs), enabling users to define complex dependencies and task relationships. Also viable for retraining/A-B testing or CI/CD


### Prefect

<blockquote class="callout callout_definition">
<span class="callout-icon">📓</span>
    <br>
    <br>
    Prefect decreases negative engineering by building a DAG structure with an emphasis on enabling positive with an orchestration layer for the current data stack.
</blockquote>

\
**Features**
- Paid
- To run Prefect, the official Helm chart requires additional configurations to be setup.
- Python package that makes it easier to design, test, operate, and construct complicated data applications. It has a user-friendly API that doesn’t require any configuration files or boilerplate. It allows for process orchestration and monitoring using best industry practices.

<br>

## Resources

1. [Airflow](https://airflow.apache.org/){:target="_blank"} 

2. [Prefect](https://www.prefect.io/){:target="_blank"} 