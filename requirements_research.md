---
layout: default
title: BridgeAI MLOps Knowledge Hub
---

## What were the requirements for our ML model and the MLOps pipeline?

We wanted to demonstrate an end-to-end, open source, pre-made MLOps pipeline. We opted for keeping our execution of this simple by creating a deploy-model pipeline only, rather than creating variations of the pipeline (eg deploy-code), which we would share with startups as a starting point.

Our base requirements:
1. The pipeline should be made of open source tools, to keep it cost-friendly and help with experimentation
<!-- 2. The level of MLOps maturity we aimed for in the ML maturity assessment and why -->
3. We should have a Minimum Viable MLOps pipeline with basic automation


## Where did the journey start? How were the design decisions made across the pipeline for each component?

We decided on different tools for different components of our pipeline such as registry, data versioning and model monitoring by conducting spikes (research) for optimal tools based on our requirements. This research is covered in the pages underneath <span style="color:#8C1437"><b>"MLOps: The Big Picture"</b></span>.

Some components did not have formal spikes, and were instead decided on because they are widely used in the industry and therefore have in-depth documentation/community notes.

<!-- 1. Spike on DAG tools
2. Spike on model registry tools
3. Spike on Data Versioning tools
4. Containerisation - understanding Docker and Kubernetes
5. Spike on model monitoring
6. How we decided on using S3 for storage -->