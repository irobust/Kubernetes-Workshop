# Declarative Language(YAML)
### Get YAML from cluster
* kubectl get [deployment-name] -o yaml
* kubectl get [service-name] -o yaml
* kubectl get [service-name] -o yaml --export
* kubectl get all -o yaml
* kubectl get po -o json
* kubectl get po/[pod-name] -o jsonpath="{.spec.clusterIP}"
* kubectl get po -o jsonpath="{.items[0].spec.clusterIP}"

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

### Liveness, Readiness and StartupProbe
The yaml has the following parameters:

Sometimes, you have to deal with legacy applications that might require an additional startup time on their first initialization
```
startupProbe:
  httpGet:
    path: /
    port: 80
  failureThreshold: 3
  periodSeconds: 10
  initialDelaySeconds: 30
```

A readiness probe is used to know when a container is ready to start accepting traffic.
```
readinessProbe:
  initialDelaySeconds: 10
  initialDelaySeconds: 1
  httpGet:
    path: /
    port: 80
```

A liveness probe is used to know when a container might need to be restarted.
```
livenessProbe:
  initialDelaySeconds: 10
  timeoutSeconds: 1
  httpGet:
    path: /
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

### Set up probes
```
livenessProbe:
    exec:
    command:
    - sh
    - -c
    - "zookeeper-ready 2181"

livenessProbe
    httpGet:
        path: /
        port: 80

livenessProbe
    tcpSocket:
        port: 3306
```

#### Pod Lifecycle
https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle