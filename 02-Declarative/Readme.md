# Declarative Language(YAML)
### Get YAML from cluster
* kubectl get <deployment-name> -o yaml
* kubectl get <service-name> -o yaml
* kubectl get <service-name> -o yaml --export
* kubectl get all -o yaml

### Manage cluster with YAML
* kubectl create -f hello-deployment.yml
* kubectl apply -f hello-deployment.yml
* kubectl delete -f helloworld-service.yml 

### Add Pods to Nodes
[https://kubernetes.io/docs/concepts/configuration/assign-pod-node/]

