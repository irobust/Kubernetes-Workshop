# Adding labels to the application

### Adding labels during build time
* kubectl create -f helloworld-pod-with-labels.yml

### Manage labels
* kubectl get pods --show-labels
* kubectl label [pod-name] app=helloworld `Adding label to rinning pods`
* kubectl label [pod-name] app=helloworldapp --overwrite `Update label`
* kubectl label [pod-name] app- `Delete label`
* kubectl get pods --show-labels `Deploy sample-infrastructure-with-labels.yml first`

### Label selectors
* kubectl get pods --selector env=production
* kubectl get pods --selector dev-lead=karthik
* kubectl get pods --selector dev-lead=karthik
* kubectl get pods -l release-version
* kubectl get pods -l dev-lead=karthik,env=staging
* kubectl get pods -l dev-lead!=karthik,env=staging
* kubectl get pods -l 'release-version in (1.0,2.0)' `Querying also supports the "in" keyword`
* kubectl get pods -l "release-version in (1.0,2.0),team in (marketing,ecommerce)"
* kubectl get pods -l 'release-version notin (1.0,2.0)' `Querying also supports the "notin" keyword`
* kubectl get all --show-labels `also work with services and deployments`
* kubectl delete pods -l dev-lead=karthik

Node Selector
https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node

