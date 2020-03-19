# Declarative Language(YAML)
### Get YAML from cluster
* kubectl get [deployment-name] -o yaml
* kubectl get [service-name] -o yaml
* kubectl get [service-name] -o yaml --export
* kubectl get all -o yaml

### Add Pods to Nodes
https://kubernetes.io/docs/concepts/configuration/assign-pod-node

### Manage cluster with YAML
* kubectl create -f helloworld-deployment.yml
* kubectl apply -f helloworld-deployment.yml
* kubectl delete -f helloworld-service.yml 

### Rolling update and rollback application
* kubectl create -f helloworld-black.yaml --record
* kubectl set image deployment/navbar-deployment helloworld=karthequian/helloworld:blue --record
* kubectl get rs
* kubectl rollout history deployment/navbar-deployment
* kubectl rollout history deployment/navbar-deployment --revision=2
* kubectl annotate deploy/navbar-deployment kubernetes.io/change-cause="change navbar color"
* kubectl rollout undo deployment/navbar-deployment
* kubectl rollout undo deployment/navbar-deployment --to-revision=version

```
  annotations:
    kubernetes.io/change-cause: "change navbar color"
```

### Liveness and Readyness

A readiness probe is used to know when a container is ready to start accepting traffic.

The yaml has the following parameters:
```
readinessProbe:
  # length of time to wait for a pod to initialize
  # after pod startup, before applying health checking
  initialDelaySeconds: 10
  # Amount of time to wait before timing out
  initialDelaySeconds: 1
  # Probe for http
  httpGet:
    # Path to probe
    path: /
    # Port to probe
    port: 80
```

A liveness probe is used to know when a container might need to be restarted.

A liveness probe yaml has the following parameters that need to be filled out:

```
livenessProbe:
  # length of time to wait for a pod to initialize
  # after pod startup, before applying health checking
  initialDelaySeconds: 10
  # Amount of time to wait before timing out
  timeoutSeconds: 1
  # Probe for http
  httpGet:
    # Path to probe
    path: /
    # Port to probe
    port: 80
```

#### Step to check readyness
* Create helloworld-with-bad-readiness-probe.yaml `change port to probe`
* kubectl create -f helloworld-with-bad-readiness-probe.yaml
* kubectl get deployments
* kubectl get pods

#### Step to check liveness
* Create helloworld-with-bad-liveness-probe.yaml `change port to probe`
* kubectl create -f helloworld-with-bad-liveness-probe.yaml
* kubectl describe [pod-name]

#### Pod Lifecycle
https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle