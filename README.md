#NOTE! THIS DOCUMENTATION IS UNDER CONSTRUCTION

#Building and Publishing Containers

##Ensure you are using the correct subscription

See Available subscriptions:

az account list --output table

Set subscription:

az account set -s \"<your-azure-account-name>\"

##Get ACR login server

az acr list --resource-group Coyote-AKS-TF-RG --query "[].{acrLoginServer:loginServer}" --output table

##Login to the Registry, ommit the domain

az acr login --name coyoteacrprodregistry

##Build and Tag image

Navigate to the root directory of the app, then run the following (mind the period at the end):

`docker build -t coyoteacrprodregistry.azurecr.io/cheddar:v1 .`

Where `coyoteacrprodregistry.azurecr.io` is the registry, `cheddar` is the container name, and `v1` is the version.

##Publish Image to registry

`docker push coyoteacrprodregistry.azurecr.io/cheddar:v1`

##Do the same for the others

Build the images:
`docker build -t coyoteacrprodregistry.azurecr.io/stilton:v1 .`
`docker build -t coyoteacrprodregistry.azurecr.io/wensleydale:v1 .`

Then publish the images to the registry

`docker push coyoteacrprodregistry.azurecr.io/stilton:v1`
`docker push coyoteacrprodregistry.azurecr.io/wensleydale:v1`

#Cluster Deployment

##Install nginx
helm install stable/nginx-ingress --name nginx-ingress --set controller.stats.enabled=true --namespace kube-system

##Describes the Ingress Controller
kubectl --namespace kube-system get services -o wide -w nginx-ingress-controller

##Gets services
kubectl get svc

##Deploy ingress

kubectl apply -f ingress.yaml