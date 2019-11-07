
### Install helm first!

See `install_helm.md`

#Deploy the NGINX ingress via Helm

## Static IP Deployment

### Note that this does not seem to be working at the moment: https://github.com/helm/charts/issues/14668

helm install stable/nginx-ingress \
    --name nginx-ingress \
    --namespace kube-system \
    --set controller.stats.enabled=true \
    --set controller.nodeSelector."beta\.kubernetes\.io/os"=linux \
    --set defaultBackend.nodeSelector."beta\.kubernetes\.io/os"=linux \
    --set controller.service.annotations.service\.beta\.kubernetes\.io/azure-load-balancer-resource-group=Coyote-AKS-TF-RG \
    --set controller.service.loadBalancerIP="52.141.217.91"


## Dynamic/Ephemeral IP allocation

helm install stable/nginx-ingress --name nginx-ingress --namespace kube-system \
    --set controller.stats.enabled=true \
    --set controller.nodeSelector."beta\.kubernetes\.io/os"=linux \
    --set defaultBackend.nodeSelector."beta\.kubernetes\.io/os"=linux \
    --set controller.service.externalTrafficPolicy=Local

## You can watch the deployment with the following command

kubectl --namespace default get services -o wide -w nginx-ingress-controller

Once a public IP address gets populated to the Load Balancer, it should show up under `EXTERNAL-IP`. Point DNS of your domains here.

## Upgrading the config

helm upgrade ngx-ingress stable/nginx-ingress \
    --name nginx-ingress \
    --namespace kube-system \
    --set controller.stats.enabled=true \
    --set controller.nodeSelector."beta\.kubernetes\.io/os"=linux \
    --set defaultBackend.nodeSelector."beta\.kubernetes\.io/os"=linux \
    --set controller.service.externalTrafficPolicy=Local



helm install --namespace kube-system --set controller.service.type="LoadBalancer" --set controller.service.externalTrafficPolicy="Local" --set controller.replicaCount=2 stable/nginx-ingress
