# Kubernetes commnad
## Hello World
We will run one of the most common Docker helloworld applications out there- [https://hub.docker.com/r/karthequian/helloworld/]

### Running your first helloworld
* kubectl get nodes
* kubectl get all
* kubectl run hw --image=karthequian/helloworld --port=80
* kubectl expose deploy/hello --type=NodePort
* kubectl get svc `Access helloworld application from http://localhost:[nodeport]`
* kubectl describe deploy/hello
* kubectl describe po/hw-5f6c6f9545-8hwp8

### 