# Setup Guide

You can follow these instructions to deploy and setup MLFlow on OpenShift.

## Pre-Requisites

To start you will need the following:
* **OpenShift cluster** with namespace available and sufficient privileges/memory to deploy
* **PostgreSQL database** - for storing MLFlow metadata
* **S3 bucket** - for storing the MLFLow artifacts such as model training files (CSVs)

***Note***: If you don't have s3 configured, by default MLFlow will log the artifacts to its pod memory. The con of this is that the artifacts will only persist for as long as the pod is "alive". Hence, we recommend having a long term solution such as s3.

## Instructions

### MLFlow Deployment

**Step 1**: Create a new project in your OpenShift cluster and provide a suitable name. You can either use the web console UI to do this or using the `oc` CLI by running `oc new-project <project-name>`.

<img width="676" alt="Screenshot 2023-02-28 at 10 27 24 AM" src="https://user-images.githubusercontent.com/7343099/221952209-4e8cc300-a224-4ade-b70b-833b26a561e3.png">

**Step 2**: Create a service account by navigating to `User Managment -> ServiceAccounts -> Create Service Account`. You can provide the service account name as `mlflow`. Once the service account is created, you will need to provide additional privileges to it so that it can be used by MLFlow to write to the pod (for storing artifats) by running: `oc adm policy add-scc-to-user privileged -z <service-account-name> -n <project-name>`. If you don't have sufficient acces to run this command, reach out to the cluster admin admin request them to run the command.

<img width="1295" alt="Screenshot 2023-02-28 at 10 49 22 AM" src="https://user-images.githubusercontent.com/7343099/221952299-9c4de5ba-20c1-4815-8bda-2a6088a9149f.png">

**Step 3**: We can now create the MLFlow deployment by navigating to `Workloads -> Deployments -> Create Deployment`. Copy and paste the [deployment](https://github.com/hemajv/mlflow-openshift/blob/main/openshift/mlflow-server-deployment.yaml) file. You will need to edit the following fileds in the yaml file:
- In [the spec](https://github.com/hemajv/mlflow-openshift/blob/main/openshift/mlflow-server-deployment.yaml#L15) **provide the service account name** that you created above in step 3.
- In [the spec](https://github.com/hemajv/mlflow-openshift/blob/main/openshift/mlflow-server-deployment.yaml#L27) **provide your PostgreSQL database configurations** (db user, db password, db name, the project/namespace name where it is deployed)
Once the necessary fields are edited click on `Create`.

<img width="1277" alt="Screenshot 2023-02-28 at 10 52 39 AM" src="https://user-images.githubusercontent.com/7343099/221952396-6e81c906-574f-4797-9bda-cc6477d9b13f.png">

 **Step 4**: If successful, you will now see a deployment created when you navigate to `Workloads -> Deployments`. You should see the deployment `mlflow-server` created.
 
 <img width="1428" alt="Screenshot 2023-02-28 at 10 53 26 AM" src="https://user-images.githubusercontent.com/7343099/221952510-842da0fd-b4e7-45ac-8f17-6cb89ee8ae76.png"> 
 
 ### MLFlow Service
 
 
