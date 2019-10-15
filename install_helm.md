##All instructions here reference the helm quickstart guide, which can be found here:

https://helm.sh/docs/using_helm/#quickstart-guide

##First, install helm locally in your computer

The instructions depend on your OS. See https://helm.sh/docs/using_helm/#installing-helm

###Choco

1) choco install kubernetes-helm

2) scoop install helm

###Manual

curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.13.10/bin/windows/amd64/kubectl.exe

##Initialize Helm and Install Tiller

###First, ensure you have the correct kubectl context

###Run the following to install Helm and Tiller on the cluster

helm init --history-max 200

###That's it! You should recieve a message About Tiller being installed

