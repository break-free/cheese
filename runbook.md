# NOTE! THIS DOCUMENTATION IS UNDER CONSTRUCTION

# Pre-requisites for workstations
* Install and configure cloud provider tools (e.g. Azure or AWS CLI)
* Install Docker engine
* Install and configure Kubectl (.kube/config)
* Install Helm (K8 package manager)

# Building and Publishing Containers

## Azure
### Ensure you are using the correct subscription

See Available subscriptions:

`az account list --output table`

Set subscription:

`az account set -s \"<your-azure-account-name>\"`

### Get ACR login server

`az acr list --resource-group Coyote-AKS-TF-RG --query "[].{acrLoginServer:loginServer}" --output table`

### Login to the Registry, ommit the domain

`az acr login --name coyoteacrprodregistry`

## AWS
### Ensure you are in the correct region
See current profile:

`aws configure list`

Set new profile: 

`aws configure`

Set multiple profile: see [AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html)

Alternatively, you can run aws commands with metaparameter `region` e.g. `aws eks list-clusters --region <region>`

### Login to the Registry

`aws ecr get-login` generates a `docker login` command. Run the `docker login` command.

# Dockerize your image
* note - AKS and EKS have different default registry server URLs. They appear as such:
 * AKS - `<repo_name>.azurecr.io`
 * EKS - `<aws_account_id>.dkr.ecr.<region>.amazonaws.com`
## Build and Tag image

Navigate to the root directory of the app, then run the following (mind the period at the end):

`docker build -t <registry_server>/cheddar:v1 .`

Where `cheddar` is the image name, and `v1` is the version.

## Publish Image to registry

`docker push <registry_server>/cheddar:v1`

## Do the same for the others

Build the images:
`docker build -t <registry_server>/stilton:v1 .`
`docker build -t <registry_server>/wensleydale:v1 .`

Then publish the images to the registry

`docker push <registry_server>/stilton:v1`
`docker push <registry_server>/wensleydale:v1`

# Cluster Deployment

## Install nginx
helm install stable/nginx-ingress --name nginx-ingress --set controller.stats.enabled=true --namespace kube-system

## Describes the Ingress Controller
kubectl --namespace kube-system get services -o wide -w nginx-ingress-controller

## Gets services
kubectl get svc

## Deploy ingress

kubectl apply -f ingress.yaml

## Troubleshooting:

kubectl describe pods

