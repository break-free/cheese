NAME:   nginx-ingress
LAST DEPLOYED: Thu Nov  7 15:53:11 2019
NAMESPACE: kube-system
STATUS: DEPLOYED

RESOURCES:
==> v1/Pod(related)
NAME                                            AGE
nginx-ingress-controller-7cd7f49967-kgl9p       1s
nginx-ingress-default-backend-7596c6d756-mllw5  1s

==> v1/Service
NAME                           AGE
nginx-ingress-controller       1s
nginx-ingress-default-backend  1s

==> v1/ServiceAccount
NAME                   AGE
nginx-ingress          1s
nginx-ingress-backend  1s

==> v1beta1/ClusterRole
NAME           AGE
nginx-ingress  1s

==> v1beta1/ClusterRoleBinding
NAME           AGE
nginx-ingress  1s

==> v1beta1/Deployment
NAME                           AGE
nginx-ingress-controller       1s
nginx-ingress-default-backend  1s

==> v1beta1/Role
NAME           AGE
nginx-ingress  1s

==> v1beta1/RoleBinding
NAME           AGE
nginx-ingress  1s


NOTES:
The nginx-ingress controller has been installed.
It may take a few minutes for the LoadBalancer IP to be available.
You can watch the status by running 'kubectl --namespace kube-system get services -o wide -w nginx-ingress-controller'

An example Ingress that makes use of the controller:

  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    annotations:
      kubernetes.io/ingress.class: nginx
    name: example
    namespace: foo
  spec:
    rules:
      - host: www.example.com
        http:
          paths:
            - backend:
                serviceName: exampleService
                servicePort: 80
              path: /
    # This section is only required if TLS is to be enabled for the Ingress
    tls:
        - hosts:
            - www.example.com
          secretName: example-tls

If TLS is enabled for the Ingress, a Secret containing the certificate and key must also be provided:

  apiVersion: v1
  kind: Secret
  metadata:
    name: example-tls
    namespace: foo
  data:
    tls.crt: <base64 encoded cert>
    tls.key: <base64 encoded key>
  type: kubernetes.io/tls