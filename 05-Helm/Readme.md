# Helm3
## Installation
* curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
* helm version --short
* helm env

## Migrate from helm2
* helm plugin install 2to3
* helm plugin ls

## Find Repository
* helm hub search redis

## Add repository
* helm repo add stable https://kubernetes-charts.storage.googleapis.com/
* helm repo ls
* helm repo delete stable
* helm search repo redis

## Chose helm chart 
* helm show chart stable/redis `(show = inspect)`
* helm show readme stable/redis
* helm search repo fabric8
* helm repo add fabric8 https://fabric8.io/helm
* helm repo add incubator https://kubernetes-charts-incubator.storage.googleapis.com/
* helm search repo | grep -c 'incubator/'

## Deploy the chart
* kubectl create ns redis
* helm install my-redis stable/redis --namespace redis
* helm ls
* watch kubectl get deployments,pods,services -n redis

## Create Persistence Volume
* kubectl apply -f pv.yaml
* mkdir /mnt/data1 /mnt/data2 /mnt/data3 --mode=777

## Custom chart
* helm create app-chart
* tree app-chart
* helm install my-app ./app-chart --dry-run --debug
* helm install my-app ./app-chart --dry-run --debug --set image.pullPolicy=Always
* helm install my-app ./app-chart --set image.pullPolicy=Always
* helm upgrade my-app ./app-chart --install --reuse-values --set service.type=NodePort
* kubectl patch service my-app-app-chart --type='json' --patch='[{"op": "replace", "path": "/spec/ports/0/nodePort", "value":31111}]'

## Destroy
* helm delete my-redis

## Other
* helm search repo | wc -l

