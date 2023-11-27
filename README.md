Today, we will discuss the deployment of MongoDB and MongoDB Express on Kubernetes, a popular container orchestration platform.
# k8s-confugrations
# MongoDB and MongoDB Express Deployment on Kubernetes

This repository provides Kubernetes configurations for deploying MongoDB and MongoDB Express. Follow the steps below to set up and run the deployment.

## Prerequisites

- Kubernetes cluster (local or cloud-based)
- `kubectl` command-line tool installed and configured

## Deploying MongoDB

1. Create a MongoDB Secret:

   ```bash
   kubectl create secret generic mongo-credentials \
     --from-literal=MONGO_ROOT_USERNAME=admin \
     --from-literal=MONGO_ROOT_PASSWORD=pass \
     --from-literal=MONGO_DATABASE=ME_CONFIG_MONGODB_SERVER

Deploy MongoDB:
kubectl apply -f mongodb-deployment.yaml

Expose MongoDB Service:
kubectl expose deployment mongodb-deployment \
  --name=mongodb-service \
  --port=27017 \
  --target-port=27017 \
  --type=LoadBalancer

  Deploying MongoDB Express
Create a ConfigMap for MongoDB Express:
kubectl create configmap mongo-express-config \
  --from-literal=ME_CONFIG_MONGODB_SERVER=mongodb-service \
  --from-literal=ME_CONFIG_MONGODB_PORT=27017
  
Deploy MongoDB Express:
kubectl apply -f mongo-express-deployment.yaml
Adjust the YAML file (mongo-express-deployment.yaml) according to your requirements.

Expose MongoDB Express Service:
kubectl expose deployment mongo-express-deployment \
  --name=mongo-express-service \
  --port=8081 \
  --target-port=8081 \
  --type=LoadBalancer
  
Wait for the external IP to be assigned:
kubectl get service mongo-express-service
Accessing MongoDB Express
Visit http://<external-ip>:8081 in your web browser, and use the provided basic authentication credentials (username: admin, password: pass) to access MongoDB Express.

Feel free to customize the configurations and explore additional options based on your application's needs.
