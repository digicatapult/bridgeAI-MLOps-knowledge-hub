---
layout: default
title: BridgeAI MLOps Knowledge Hub
---

## Prediction Service Content

The team proposed the use of FastAPI over Flask for prediction service API following a quick comparison of FastAPI vs Flask from [here](https://www.netguru.com/blog/python-flask-versus-fastapi){:target="_blank"} and [here](https://www.turing.com/kb/fastapi-vs-flask-a-detailed-comparison){:target="_blank"}, with focus on the built in automatic swagger ui documentation support and data validation support.

## Starting the Prediction Service

1. Install the requirements `poetry install`

2. Start the server `uvicorn src.main:app --host 0.0.0.0 --port 8000 --reload` (Ctrl + C to stop)

3. Set up the <span style="color:#FBD2DF"><b>MODEL_PREDICTION_ENDPOINT</b></span> environment variable to point to the regression model prediction endpoint.

4. Access the swagger ui here - `http://localhost:8000/swagger`

5. The API documentations is available here - `http://localhost:8000/api-docs`