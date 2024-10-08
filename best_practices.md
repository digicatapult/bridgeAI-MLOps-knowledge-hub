---
layout: default
title: BridgeAI MLOps Knowledge Hub
---

## MLOps Best Practices


<blockquote class="callout callout_info">
<span class="callout-icon">ℹ️</span>
    <br>
    <br>
    While best practices for MLOps is technically covered in the <a href="https://digicatapult.github.io/bridgeAI-MLOps-knowledge-hub/prerequisites.html" target="_blank">Prerequisites</a> section, separate elaboration on these principles is required given their importance.
</blockquote>
<br>

Within best practices for MLOps, there are a number of other areas where principles must be considered in order to implement an optimal AI/ML offering. The following considerations can be expanded on by clicking on them:

* [Objective and Metric Best Practices](#objective-and-metric-best-practices)
* [Infrastructure Best Practices](#infrastructure-best-practices)
* [Data Best Practices](#data-best-practices)
* [Model Best Practices](#model-best-practices)
* [Code Best Practices](#code-best-practices)


### Objective and Metric Best Practices

Before embarking on the design and implementation of an AI/ML offering, you must first have clearly defined business objectives. 

These include identifying your 'problem' to ensure that the ML Model is necessary, collecting data that aligns with your objective, and developing clear and scalable metrics. With regard to developing metrics, it is important to ensure that the process put in place to meet your business goal is reviewed thoroughly and regularly, as automation will address areas in which the current process faces challenges.

The [Deployment Service Life Cycle framework](https://digicatapult.github.io/bridgeAI-MLOps-knowledge-hub/deployment_lifecycle.html){:target="_blank"} provided contains a table of considerations to adequately clarify your business objectives, resource constraints (funding, time, in/tangible resources), and AI/ML use cases.

<!-- for this and all others - 3 sentences to get the point across, expand after everything is blurted out. -->

### Infrastructure Best Practices

The right infrastructure must be in place to support the model <span style="color:#8C1437"><b>before</b></span> you invest time into constructing it. Best practice here includes creating a model that is self-sufficient and allows the infrastructure to be independent of it. This way, multiple features can be integrated later on. 

Key best practices when designing the infrastructure include selecting the right infrastructure components (from a range of containers, orchestration tools, software environments, CI/CD tools), deciding between cloud-based and on-premise infrastructure, and ensuring that the infrastructure is scalable. 

When deciding between cloud-based and on-premise infrastructure, three main points organisations should consider <span style="color:#8C1437">alongside</span> their scope, requirements and constraints are whether their choice of infrastructure is:

- <span style="color:#8C1437">cost effective</span> in terms of time and funding, 
- <span style="color:#8C1437">low-maintenance</span>, and 
- <span style="color:#8C1437">easily scalable</span>. 

Cloud-based architecture falls under all three of these criteria, with cloud solution providers like AWS, Azure and GCP having pre-made ML-specific infrastructure elements. 

While on-premise infrastructure can be costly when it comes to maintenance and scalability, it provides high levels of control and security over data, systems and software maintenance.

Idealy, the scalability of your infrastructure should be configured in such a way that it enables you to continue testing your model's features without affecting the deployed model. An optimal approach for this would be microservices architecture.

### Data Best Practices

The quality of the model is contingent on the data that is properly processed and fed into it. To ensure that your model is of strong quality, you must consider:

- The quantity of your data, in that having copious amounts allows for better model performance. If you have minimal data available, you can use **[transfer learning](https://aws.amazon.com/what-is/transfer-learning/){:target="_blank"}** to gather data.
- Proper implementation of data pre-processing, feature engineering, and data validation as part of the ML workflow and for re-training, 
- The implementation of exploratory data analysis for sanity and validation checks, and the implementation of model logging and monitoring processes in order to identify when to stop the pipeline's execution and address anomalies.
- Documentation/storage of the data's features for use throughout the ML lifecycle.

### Model Best Practices

With the objectives, metrics, infrastructure and data ready or in place, the ideal model can then be chosen. Best practices surrounding model creation comprise:

- Developing a <span style="color:#8C1437">robust model</span>,
- Developing and <span style="color:#8C1437">documenting</span> model <span style="color:#8C1437">training metrics</span>,
- <span style="color:#8C1437">Finetuning</span> the model that will be served, and
- <span style="color:#8C1437">Monitoring</span> and optimizing the model's training.

Developing a robust model involves implementing appropriate validation, testing and monitoring processes for your model's pipeline. It is also crucial that you have defined and created usable test cases (i.e. criteria for deciding on an optimal model based on chosen training metrics) for your model's training.

The development and documentation of your model's training metrics can be executed with platforms such as MLflow. Additionally, the use of data derived from serving your model (where possible) to train your models will make the model easier to deploy, as this way the data is trained for more accurate outputs given realistic vs simulated inputs, subject to data/model/concept drift not arising.

Finally, given that the model must be retrained regularly, having an optimized training strategy will be ideal especially to account for fluctuations in model accuracy with the initial training batch. 

### Code Best Practices

The code that is written must execute effectively at all stages of your pipeline. All relevant actors in your MLOps team (<span style="color:#8C1437">examples of actors</span> can be found in the **[Skills, Roles and Tools](https://digicatapult.github.io/bridgeAI-MLOps-knowledge-hub/prerequisites.html#roles){:target="_blank"}** page) must be able to read, write or execute model codes. 

Where unit tests will evaluate individual features, continuous integration implementations will test the pipeline as a whole to guarantee that changes in the code will not break the model.

Best practice for writing your code include:

- Following <span style="color:#8C1437">naming conventions</span> for variables 
- Ensuring quality in the form of <span style="color:#8C1437">readability</span> and the ability of others to <span style="color:#8C1437">maintain</span> and <span style="color:#8C1437">extend</span> the code subject to changes in requirements
- Writing <span style="color:#8C1437">productionised</span> code
- Deploying models <span style="color:#8C1437">in containers</span> for easier integration
- <span style="color:#8C1437">Automating</span> unit and integration tests wherever possible

<!-- The best practices (or <span style="color:#8C1437"><b>principles</b></span>) on MLOps are:
- Automation
- Continuous X
- Versioning
- Experiment Tracking
- Testing
- Monitoring

Some <span style="color:#8C1437"><b>core considerations</b></span> for each principle as it relates to the the three levels where changes can take place (in your data, algorithm and code) include:

<img src="mlops_principles.png">
Source: [MLOps.org](https://ml-ops.org/content/mlops-principles#summary-of-mlops-principles-and-best-practices){:target="_blank"}

## Considerations for a Well-Architected Framework

While this does not contain a strict set of guidelines, the [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html){:target="_blank"} is a reliable resource for evaluating whether specific architecture aligns well with cloud best practices. The pillars of the framework (each with their own set of additional considerations) are:

- Operational excellence
- Security
- Reliability
- Performance efficiency
- Cost optimization
- Sustainability -->

## Resources

1. [MLOps.org](https://ml-ops.org/content/mlops-principles){:target="_blank"}

2. [AWS Well-Architected Framework Guide](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html){:target="_blank"}

3. [ML Best Practices: A Comprehensive List](https://www.zucisystems.com/blog/machine-learning-best-practices-a-comprehensive-list/#1){:target="_blank"}

4. [What is Transfer Learning](https://aws.amazon.com/what-is/transfer-learning/){:target="_blank"}