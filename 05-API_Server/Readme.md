# Kubernetes API Server
### Get definition references
* kubectl explain pods
* kubectl explain pod.spec
* kubectl explain pod.spec.containers
* kubectl api-resources --api-group=apps
* kubectl api-resources --namespaced=false
* kubectl explain deployment | head
* kubectl explain deployment --api-version apps/v1beta2 | head
* kubectl explain deployment --api-version apps/v1 | head
* kubectl api-versions | sort | more

### Basic concept API Object and API Server
* kubectl proxy --port 8888
* kubectl get po -v 9 `Track request and response`
* kubectl auth can-i get po
* curl http://localhost:8001/api/v1/namespaces/default/pods/hello-world
* curl http://localhost:8001/api/v1/namespaces/default/pods/hello-world/log 

