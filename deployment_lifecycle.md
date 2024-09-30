---
layout: default
title: BridgeAI MLOps Knowledge Hub
---

## Deployment Service Life Cycle

The following graphic summarises the Deployment Service Life Cycle, which can be followed by <span style="color:#8C1437"><b>startups</b></span> and <span style="color:#8C1437"><b>larger organisations</b></span> alike:

<img class="center" alt="Deployment Service Life Cycle" src="https://github.com/hema-dc/ML-Deployment/assets/93590728/9ff383ea-12b0-43a2-88c7-98a1537093b9">

<br>

While the considerations for startups and larger organisations are generally similar, they do <span style="color:#8C1437">vary</span> slightly. The considerations per step of the Deployment Service Life Cycle framework for <span style="color:#8C1437">both types of organisations</span> are listed below:

<br>
<table>
  <tr>
    <th></th>
    <th>Startups</th>
    <th>Larger Organisations</th>
  </tr>

  <tr>
    <td><b>Gather</b></td>
    <td>
    <br>
    The requirements, goals and objectives
    <br>
    <br>
    Understand the AI/ML use case(s)
    <br>
    <br>
    Understand the current infrastructure requirements
    <br>
    <br>
    Understand the deployment expectations (Budget, timescales, resources)
    <br>
    <br>
    </td>
    <td>
    As with startups, but including understand the AI/ML use case(s) <span style="color:#8C1437">and their connectivity to organisational strategy</span>.
    </td>
  </tr>

  <tr>
    <td><b>Assess</b></td>
    <td>
    <br>
    Current AI/ML model
    <br>
    <br>
    Maturity of the code
    <br>
    <br>
    Current available infrastructure
    <br>
    <br>
    Current data pipeline (if any)
    <br>
    <br>
    Data dependencies
    <br>
    <br>
    Size of the current dataset
    <br>
    <br>
    If current data is real or synthetic
    <br>
    <br>
    The data source for model in production
    <br>
    <br>
    Skills availability within the organisation
    <br>
    <br>
    </td>
    <td>
    As with startups, but including:
    <br>
    <br>
    <span style="color:#8C1437">Past AI/ML models</span> (if any) already in production
    <br>
    <br>
    The MLOps <span style="color:#8C1437">Maturity</span> level
    <br>
    <br>
    The <span style="color:#8C1437">scalability</span> requirements.
    </td>
  </tr>

  <tr>
    <td><b>Plan / Design</b></td>
    <td scope="row" colspan="2" class="centered">
    <br>
    Potential deployment pipeline
    <br>
    <br>
    Deployment strategy
    <br>
    <br>
    Metrics to be monitored
    <br>
    <br>
    </td>
  </tr>

  <tr>
    <td><b>Implement</b></td>
    <td scope="row" colspan="2" class="centered">
    <br>
    Deploy the model
    <br>
    <br>
    Review the deployment strategy
    <br>
    <br>
    </td>
  </tr>

  <tr>
    <td><b>Evaluate / Review</b></td>
    <td scope="row" colspan="2" class="centered">
    <br>
    <br>
    Monitor the metrics of the model
    <br>
    <br>
    Observability - Model health, Data health and Service health
    <br>
    <br>
    </td>
  </tr>

  </table>