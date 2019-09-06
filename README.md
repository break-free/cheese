#NOTE! THIS DOCUMENTATION IS UNDER CONSTRUCTION

##Install nginx
helm install stable/nginx-ingress --name nginx-ingress --set controller.stats.enabled=true --namespace kube-system

##Describes the Ingress Controller
kubectl --namespace kube-system get services -o wide -w nginx-ingress-controller

##Gets services
kubectl get svc

##Deploy ingress

kubectl apply -f ingress.yaml