#Cheese APP
##An introduction to container workflows and Kubernetes Deployments

The purpose of this repo is to provide an introduction to working with containers, from local development to a deployment to Kubernetes.

##This repo contains important components needed for local development and to deploy to Kubernetes:

1. The app code itself, which is contained within the `cheese_code` Directory. There are a total of three apps: `Cheddar`, `Stilton`, `Wensleydale`
2. Instructions on how to build the applications, located within each app directory's `Dockerfile`
3. Instructions to run the whole application locally, located in the `docker-compose` file
4. Manifests to deploy both the application and it's required services:
⋅⋅* `ingress.yaml`: Instructions to the Kubernetes Cluster on how to route incoming traffic to the right service
..* `cheese.yaml`: Instructions to the Kubernetes Cluster on where to pull the built applications, their compute requirements, and how they are exposed within the cluster
..* `cheese_services.yaml`: Instructions on how to route incoming connections from the ingress to the right Kubernetes `Pods`