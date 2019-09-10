Latest recommended Kubernetes version for AKS is v1.13.10. The latest verison of Kubernetes is v1.15.1. Using a newer version of kubectl can lead to problems when making API calls, so you will need to downgrade your kubectl version to match what is in your cluster.

For Windows:

curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.13.10/bin/windows/amd64/kubectl.exe

For Mac:

curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.13.10/bin/darwin/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

For Linux:

curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.13.10/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl