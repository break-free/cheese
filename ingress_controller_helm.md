
###Install helm first!

See `install_helm.md`

#Deploy the NGINX ingress via Helm

##Static IP Deployment

helm install stable/nginx-ingress \
    --name nginx-ingress
    --namespace kube-system \
    --set controller.stats.enabled=true \
    --set controller.nodeSelector."beta\.kubernetes\.io/os"=linux \
    --set defaultBackend.nodeSelector."beta\.kubernetes\.io/os"=linux \
    --set controller.service.loadBalancerIP="13.89.138.85"


##Dynamic/Ephemeral IP allocation

helm install stable/nginx-ingress \
    --name nginx-ingress
    --namespace kube-system \
    --set controller.stats.enabled=true \
    --set controller.nodeSelector."beta\.kubernetes\.io/os"=linux \
    --set defaultBackend.nodeSelector."beta\.kubernetes\.io/os"=linux

##You can watch the deployment with the following command

kubectl --namespace default get services -o wide -w nginx-ingress-controller