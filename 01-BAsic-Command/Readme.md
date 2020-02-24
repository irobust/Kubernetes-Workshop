# Kubernetes commnad
## Hello World
We will run one of the most common Docker helloworld applications out there- https://hub.docker.com/r/karthequian/helloworld/

### Running your first helloworld
* kubectl cluster-info
* kubectl get nodes
* kubectl get all
* kubectl run hw --image=karthequian/helloworld --port=80
* kubectl expose [deployment-name] --type=NodePort
* kubectl get svc `Access helloworld application from http://localhost:[random-nodeport]`
* kubectl describe [deployment-name]
* kubectl describe [pod-name] `po/hw-5f6c6f9545-8hwp8`
* kubectl port-forward [pod-name] 8080:80

### Type of Service
* NodePort `flag exposes the deployment outside of the cluster by random port from 30000-32767`
* LoadBalancer `On cloud providers that support load balancers, an external IP address would be provisioned to access the service`
* ClusterIP `flag is only accessible by its internal IP address within the cluster`

###  Troubleshooting
* kubectl logs <pod_name>
* kubectl exec -it [pod-name] /bin/bash `If you have only one contianer`
* kubectl exec -it [pod-name] -c [container-name] /bin/bash


### Scale your helloworld application
* kubectl scale --replicas=3 [deployment-name] `scale up`
* kubectl scale --replicas=1 [deployment-name] `scale down`

### Web-based Kubernetes user interface
* kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml
* kubectl proxy
* http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/
* kubectl describe secret -n kube-system
* Login with service account token

#### Read more
* https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard
* https://github.com/kubernetes/dashboard

### Switch context
* kubectl config current-context
* kubectl config get-contexts
* kubectl config use-context [context-name]
* kubectl config view
* cat ~/.kube/config

### Working with Namespace
* kubectl get namespaces
* kubectl run nginx --image=nginx --namespace=[insert-namespace-name-here]
* kubectl get pods --namespace=kube-system
* kubectl get pods -n kube-system
* kubectl config view | grep namespace
* kubectl config set-context --current --namespace=[insert-namespace-name-here]
* kubectl create namespace [insert-namespace-name-here]
* kubectl delete namespaces [insert-some-namespace-name] `Warning: Delete everything under namespace`
