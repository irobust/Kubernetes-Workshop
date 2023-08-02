# Kubernetes Installation
## Local Installation
### Minikube
* https://minikube.sigs.k8s.io/docs/start/
* minikube start
* List of drivers https://minikube.sigs.k8s.io/docs/drivers/
* kubectl run [deployment-name] --image=karthequian/helloworld --port=80
* minikube service [deployment-name]
* minikube dashboard
* minikube addons list
* minikube addons enable [plugin-name]
* minikube addons disable [plugin-name]

### Kind
* kind create cluster
* kind create cluster --name [ชื่อ cluster]
* kind create cluster --config kind-config.yaml
* kind get clusters
* kind delete cluster
* kubectl cluster-info --context kind-[ชื่อ cluster]

## On-premise Installation
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

#### Useful resources
* https://kubernetes.io/docs/setup/
* https://github.com/kelseyhightower/kubernetes-the-hard-way/blob/master/docs/03-compute-resources.md
