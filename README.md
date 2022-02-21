# Basic Multi container Application in kubernetes

In this demo project we are using React client, Node.js backend, PostgreSQL and Nginx for application and Deployment using Kubernetes.

It is a basic application to get inputs as numbers from client and retrieve saved numbers from Database.

#Lets Get Started with the deployment.

## Pre-Requisites
1. Install [minikube](https://minikube.sigs.k8s.io/docs/start/)
2. Install [kubectl](https://kubernetes.io/docs/tasks/tools/)
3. Install [Docker](https://docs.docker.com/desktop/mac/install/)


## Build Container image for application.

In this demo we are using 3 containers

- [db] (Postgres) - Database

- [client](apps/client/Dockerfile) - Client App

- [server](apps/server/Dockerfile) - Server App

### Creating and push images to Dockerhub.
```shell
git clone https://github.com/boobalana/pro.git pro
cd pro/apps

#Build Image for Client
cd client
docker build -t <imagename:version> .
docker push <imagename:version> <repo/imagename:version>

#Build Image for Server
cd ../server
docker build -t <imagename:version> .
docker push <imagename:version> <repo/imagename:version>
```

i will be using following images which are created using above steps.

[Server](https://hub.docker.com/repository/docker/boobalan/pro-server)
[CLIENT](https://hub.docker.com/repository/docker/boobalan/pro-client)
postgres : public postgres image


## Kubernetes Manifest
All Kubernetes Manifest files are under [kubernetes](kubernetes) folder.
```
client-cluster-ip-service.yml
database-persistent-volume-claim.yml
postgres-cluster-ip-service.yml
server-cluster-ip-service.yml
client-deployment.yml
db-secret.yaml
postgres-deployment.yml
server-deployment.yml
```

## Creating multiple Environment.
Here we are going to use [kustomize](https://kustomize.io/) to  deploy Application in 2 Environment (Dev and Prod).

Under infra folder we have kustomize templates to deploy Application in multiple Environments.

Base folder holds all the kubernetes manifest and kustomize file 
overlays will be used to have custom configuration based on Environment. Example here are running 1 replica for dev and 2 replica for Prod
```
cd infra
kubectl create -k overlays/dev
kubectl  get all --namespace=dev
kubectl create -k overlays/prod
kubectl  get all --namespace=prod

```

