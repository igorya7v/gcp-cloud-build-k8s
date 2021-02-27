## Google Cloud Build Deploy to Kuberneted (CI/CD Pipelines)

### App High Level Overview
![Kubernetes Deployment with Google Build](https://github.com/igorya7v/gcp-cloud-build-k8s/blob/main/readme-images/Cloud%20Build%20Deployment%20With%20Kubernetes.svg)

### CI/CD Overview
![CI/CD Overview](https://github.com/igorya7v/gcp-cloud-build-k8s/blob/main/readme-images/CI-CD%20Overview.svg)

### Application Structure
- Application Source Code: [src](https://github.com/igorya7v/gcp-cloud-build-k8s/tree/main/src "src") folder
- Docker file: [Dockerfile](https://github.com/igorya7v/gcp-cloud-build-k8s/blob/main/Dockerfile "Dockerfile")
- CloudBuild Pipeline Configuration: [cloudbuild.yaml](https://github.com/igorya7v/gcp-cloud-build-k8s/blob/main/cloudbuild.yaml "cloudbuild.yaml")


# Deploy Pipeline Flowchart (cloudbuild.yaml)

![Deploy Flow Chart](https://github.com/igorya7v/gcp-cloud-build-k8s/blob/main/readme-images/deploy-flow-chart.svg)
  
  
# Goole Cloud Kuberneted Cluster Setup (Standard/Single-Zone)

##### Ensure that you have enabled the Google Kubernetes Engine API.
```
gcloud projects list
```
##### Use the correct Project ID returned from the previous command.
```
gcloud config set project YOUR_PROJECT_ID
```

##### Set default zone
```
gcloud config set compute/zone us-central1-a
```

##### Enable Google Kubernetes API
```
gcloud services enable container.googleapis.com
```
##### Create a Kubernetes Cluster (GKE)
```
gcloud container clusters create simple-spring-boot-cluster --num-nodes=1
```
##### Get authentication credentials for the cluster (This command configures `kubectl` to use the cluster you created)
```
gcloud container clusters get-credentials simple-spring-boot-cluster
```
Ensure that you have an `Kubernetes Engine Developer` IAM role in your account. 
#####  Deploying an application to the cluster
```
kubectl apply -f simple-spring-boot-app.yaml
```
###  Test the Kubrnetes Deployment
```
kubectl get pods
kubectl get deployment
kubectl get services
```
### After successful deployment, test the simple-spring-boot app
Use Service `EXTERNAL-IP` fro the previous step 
```
curl 35.223.66.77:60000/message
Simple Spring Boot Demo...
```
### Cleaning Up

The Google Cloud resources are not free. To clean them up, run the following:
```
kubectl delete service simple-spring-boot-service
gcloud container clusters delete simple-spring-boot-cluster
```

## TODO
- Speed up CloudBuild Pipeline.
- Define infrustructure as a code for the Standard Kubernetes Cluster (check if any infrustrucure definition is needed for the Autopilot mode) using tools like Google Cloud Deployment Manager (Templates), Teraform, etc.
