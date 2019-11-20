# Kubernetes commnad
## Hello World
We will run one of the most common Docker helloworld applications out there- [https://hub.docker.com/r/karthequian/helloworld/]

### Running your first helloworld
* kubectl get nodes
* kubectl get all
* kubectl run hw --image=karthequian/helloworld --port=80
* kubectl expose <deployment-name> --type=NodePort
* kubectl get svc `Access helloworld application from http://localhost:[random-nodeport]`
* kubectl describe <deployment-name>
* kubectl describe <pod-name> `po/hw-5f6c6f9545-8hwp8`

### Type of Service
* NodePort `flag exposes the deployment outside of the cluster by random port from 30000-32767`
* LoadBalancer `On cloud providers that support load balancers, an external IP address would be provisioned to access the service`
* ClusterIP `flag is only accessible by its internal IP address within the cluster`

###  Troubleshooting
* kubectl logs <pod_name>
* kubectl exec -it <pod-name> /bin/bash `If you have only one contianer`
* kubectl exec -it <pod-name> -c <container-name> /bin/bash


### Scale your helloworld application
* kubectl scale --replicas=3 <deployment-name> `scale up`
* kubectl scale --replicas=1 <deployment-name> `scale down`