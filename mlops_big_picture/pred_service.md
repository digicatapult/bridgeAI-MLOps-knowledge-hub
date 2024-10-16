---
layout: default
title: BridgeAI MLOps Knowledge Hub
---

## Prediction Service

The team proposed the use of FastAPI over Flask for prediction service API following a quick <span style="color:#8C1437"><b>comparison</b></span> of FastAPI vs Flask from **[here](https://www.netguru.com/blog/python-flask-versus-fastapi){:target="_blank"}** and **[here](https://www.turing.com/kb/fastapi-vs-flask-a-detailed-comparison){:target="_blank"}**, with focus on the built in automatic swagger UI documentation support and data validation support.

The definitions of Flask and FastAPI are linked in the [Resources](#resources) section at the bottom of this page.

### Starting the Prediction Service

**Note:** The repository can be accessed [here](https://github.com/digicatapult/bridgeAI-prediction-service){:target="_blank"}


1. Install the requirements `poetry install`

1. Set/update the environment variables (listed at the [bottom](./mlops_big_picture/pred_service.html#variables) of this page)

2. Run the following for database migration: `poetry run alembic upgrade head`

2. Start the API server `uvicorn src.main:app --host 0.0.0.0 --port 8000 --reload` (Ctrl + C to stop)

3. Set up the <b>MODEL_PREDICTION_ENDPOINT</b> environment variable to point to the regression model prediction endpoint.

4. Access the swagger ui here - `http://localhost:8000/swagger`

5. The API documentations is available here - `http://localhost:8000/api-docs`


### Variables
<table>
  <tr>
    <th>Variable</th>
    <th>Default Value</th>
    <th>Description</th>
  </tr>

  <tr>
    <td>MODEL_PREDICTION_ENDPOINT</td>
    <td>
    <code>http://localhost:5001/invocations</code>
    </td>
    <td>
    The endpoint URL for making model prediction requests.
    </td>
  </tr>

  <tr>
    <td>POSTGRES_HOST</td>
    <td>
    <code>localhost</code>
    </td>
    <td>
    The hostname or IP address of the PostgreSQL server.
    </td>
  </tr>

  <tr>
    <td>POSTGRES_USER</td>
    <td>
    <code>admin</code>
    </td>
    <td>
    The username for authenticating to the PostgreSQL database.
    </td>
  </tr>

  <tr>
    <td>POSTGRES_PASSWORD</td>
    <td>
    <code>password</code>
    </td>
    <td>
    The password for authenticating to the PostgreSQL database.
    </td>
  </tr>

  <tr>
    <td>POSTGRES_DB</td>
    <td>
    <code>bridgeai</code>
    </td>
    <td>
    The name of the PostgreSQL database to connect to.
    </td>
  </tr>

  <tr>
    <td>POSTGRES_PORT</td>
    <td>
    <code>5432</code>
    </td>
    <td>
    The port number on which the PostgreSQL server is listening.
    </td>
  </tr>

  </table>
<br>

### Resources

1. [What is Flask?](https://www.netguru.com/blog/python-flask-versus-fastapi#a-brief-overview-of-flask){:target="_blank"}

1. [What is FastAPI?](https://www.netguru.com/blog/python-flask-versus-fastapi#an-introduction-to-fastapi){:target="_blank"}
