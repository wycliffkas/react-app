A basic React app deployed to Kubernetes using Helm.

## Run the application locally
1. [Clone the repo](#1-clone-the-repo)
2. [Run the application](#2-run-the-application)

### 1. Clone the repo

Clone the repo locally. In a terminal, run:

```
$ git clone https://github.com/wycliffkas/react-app.git
```

### 2. Run the application
- Install [Node.js](https://nodejs.org/en/)
- Run `npm install` if you use npm or `yarn` if you use yarn inorder to install the dependencies
- Run `yarn start` to launch the app which will automatically launch the app in the browser.

## Run the application using Docker
1. [Build the image](#1-build-the-image)
2. [Run the image](#2-run-the-image)
3. [Push the image to the container registry](#3-push-the-image-to-the-container-registry)

## Prerequisites:
1. [Create Docker account](https://cloud.docker.com/)

2. [Create a repository on docker hub](https://docs.docker.com/docker-hub/)

3. [Install Docker CLI](https://docs.docker.com/install/)

### 1. Build the image

In a terminal, run:
```
$ docker build -t gcr.io/<PROJECT_ID>/<IMAGE_NAME>:<tag> .
```

Your image should be listed by running:

```
$ docker images
```

### 2. Run the image

In a terminal, run:

```
$ docker run -p 3000:3000 -d gcr.io/<PROJECT_ID>/<IMAGE_NAME>
```

### 3. Push the image to the container registry

In a terminal, run:

```
$ gcloud docker -- push gcr.io/<PROJECT_ID>/<IMAGE_NAME>:<tag>
```

## Run the application on Kubernetes

1. [Deploy the application](#1-deploy-the-application)
2. [Create a service](#2-create-a-service)

## Prerequisites

1. [Create an account with GCP](https://cloud.google.com)

2. [Install Google Cloud SDK](https://cloud.google.com/sdk/)

3. Install Kubernetes Client.
```
$gcloud components install kubectl
```

4. Create a GCP project.
```
$gcloud config set project <PROJECT_ID>
```

5. Create cluster
```
$gcloud container clusters create <CLUSTER_NAME> --zone <ZONE>
```

6. Connect your kubectl client to your cluster
```
$ gcloud container clusters get-credentials <CLUSTER_NAME> --zone <ZONE>
```

### 1. Deploy the application

```
$ kubectl create -f deployment.yaml
```

To check how many pods are running on Kubernetes run the command:
```
kubectl get pods
```

Expose the app to the web by setting the port. Run the command:

```
$ kubectl expose deployment/<DEPLOYMENT_NAME> —-port=3000 —-type=NodePort
```

### 2. Create a service

```
kubectl create -f service.yaml

```

To list all services. Run the command:

```
kubectl get services

```

## Create Helm chart 

1. [create chart](#1-build-image)
2. [Deploy chart](#2-deploy-chart)

## Prerequisites
1. [Install Helm](https://github.com/helm/helm/releases)

### 1. create chart

In a terminal, run:
```
$ helm create <chart-name>

```

### 2. deploy chart

In a terminal, run:
```
$ helm install <RELEASE_NAME> <CHART_NAME>

```

In a terminal, run the command below to see what was deployed:
```
$ kubectl get all

```

The hosted application can be accessed [here](http://35.193.221.108:3000/)