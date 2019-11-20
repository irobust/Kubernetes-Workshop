# Declarative Language(YAML)
### Get YAML from cluster
* kubectl get <deployment-name> -o yaml
* kubectl get <service-name> -o yaml
* kubectl get <service-name> -o yaml --export
* kubectl get all -o yaml

### Add Pods to Nodes
[https://kubernetes.io/docs/concepts/configuration/assign-pod-node/]

### Manage cluster with YAML
* kubectl create -f hello-deployment.yml
* kubectl apply -f hello-deployment.yml
* kubectl delete -f helloworld-service.yml 

### Rolling update and rollback application
* kubectl create -f helloworld-black.yaml --record
* kubectl set image deployment/navbar-deployment helloworld=karthequian/helloworld:blue
* kubectl get rs
* kubectl rollout history deployment/navbar-deployment
* kubectl rollout undo deployment/navbar-deployment
* kubectl rollout undo deployment/navbar-deployment --to-revision=version

### Liveness and Readyness
