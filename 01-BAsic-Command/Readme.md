# Kubernetes commnad
## Moving from docker to kubernetes
* https://kompose.io
* kompose convert
* kompose convert -f docker-compose.yml
* kompose convert --out .k8s (create directory first)
* kompose convert --replicas=3

## Hello World
We will run one of the most common Docker helloworld applications out there- https://hub.docker.com/r/karthequian/helloworld/

### Useful resources
* https://kubernetes.io/docs/setup/
* https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/03-compute-resources.md

### Manual Installation
* https://www.katacoda.com/courses/kubernetes/getting-started-with-kubeadm
* https://labs.play-with-k8s.com

#### Run at master
* kubeadm config images pull
* kubeadm init --apiserver-advertise-address $(hostname -i) --pod-network-cidr [CIDR]
* kubectl apply -f https://raw.githubusercontent.com/cloudnativelabs/kube-router/master/daemonset/kubeadm-kuberouter.yaml
* kubeadm token create --print-join-command
* kubeadm token list
* openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //'

#### Run at Worker
* kubeadm join [MasterIPAddress]:6443 --token [TOKEN] --discovery-token-ca-cert-hash [CERT:HASH]


### Minikube Installation
* https://minikube.sigs.k8s.io/docs/start/
* minikube start
* List of drivers https://minikube.sigs.k8s.io/docs/drivers/
* kubectl run [deployment-name] --image=karthequian/helloworld --port=80
* minikube service [deployment-name]
* minikube dashboard
* minikube addons list
* minikube addons enable [plugin-name]
* minikube addons disable [plugin-name]

### Running your first helloworld
* kubectl cluster-info
* kubectl get nodes
* kubectl get all
* kubectl run [deployment-name] --image=karthequian/helloworld --port=80
* kubectl expose deploy/[deployment-name] --type=NodePort
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
* kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.3.1/aio/deploy/recommended.yaml
* kubectl proxy
* http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login
* kubectl describe secret -n kube-system
* Login with service account token

#### Read more
* https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard
* https://github.com/kubernetes/dashboard

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
