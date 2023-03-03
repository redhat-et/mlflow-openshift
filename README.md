# MLFlow on OpenShift

This repositry contains steps and guides on how to deploy [MLFlow](https://mlflow.org/) in [OpenShift](https://www.redhat.com/en/technologies/cloud-computing/openshift).

## MLFlow

MLflow is an open source platform to streamline machine learning development, including tracking experiments, packaging code into reproducible runs, and sharing and deploying models. MLflow's current components are:

- [MLflow Tracking](https://mlflow.org/docs/latest/tracking.html): An API to log parameters, code, and results in machine learning experiments and compare them using an interactive UI.
- [MLflow Projects](https://mlflow.org/docs/latest/projects.html): A code packaging format for reproducible runs using Conda and Docker, so you can share your ML code with others.
- [MLflow Models](https://mlflow.org/docs/latest/models.html): A model packaging format and tools that let you easily deploy the same model (from any ML library) to batch and real-time scoring on platforms such as Docker, Apache Spark, Azure ML and AWS SageMaker.
- [MLflow Model Registry](https://mlflow.org/docs/latest/model-registry.html): A centralized model store, set of APIs, and UI, to collaboratively manage the full lifecycle of MLflow Models.

You can find more documentation on their official website at https://mlflow.org/docs/latest/index.html.

## OpenShift

We will be deploying MLFlow on an OpenShift cluster with an [OAuth proxy](https://github.com/openshift/oauth-proxy) i.e a reverse proxy that provides authentication with OpenShift via OAuth and Kubernetes service accounts. OpenShift is a product developed at Red Hat which is a unified platform to build, modernize, and deploy applications at scale. OpenShift brings together tested and trusted services to reduce the friction of developing, modernizing, deploying, running, and managing applications. Built on Kubernetes, it delivers a consistent experience across public cloud, on-premise, hybrid cloud, or edge architecture. Whether you're building new applications or modernizing existing ones, OpenShift supports the most demanding workloads including AI/ML, edge, and more. 

## Deployment
### Pre-Requisites
In order to setup MLFlow on OpenShift you will need the following:
- **OpenShift cluster** with namespace available and sufficient privileges/memory to deploy
- **PostgreSQL database** - for storing MLFlow metadata
- **S3 bucket** - for storing the MLFLow artifacts such as model training files (CSVs)

## Setup Guide
To learn how to setup MLFlow on OpenShift refer to [this guide](https://github.com/hemajv/mlflow-openshift/blob/main/openshift/README.md).
