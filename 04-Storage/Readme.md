# Kubernetes Storage
## Persistence Volume
* kubectl get pv,pvc
* kubectl apply -f Persistence-Volume
* kubectl edit sc/hostpath

change is-default-class to __false__
```
storageclass.kubernetes.io/is-default-class: "false"
```

## Configmap and Secret
### Manage ConfigMap
* kubectl create configmap logger --from-literal=log_level=debug
* kubectl get configmaps
* kubectl get configmap/logger -o yaml
* kubectl edit configmap/logger
* Change YAML to Read log_level

```
    valueFrom:
        configMapKeyRef:
            name: logger #Read from a configmap called log-level
            key: log_level  #Read the key called log_level
```

```
spec:
      containers:
      - name: logreader
        image: karthequian/reader:latest
        env:
        - name: LOG_LEVEL
          valueFrom:
            configMapKeyRef:
              name: logger 
              key: log_level
        volumeMounts:
          - name: config-volume
            mountPath: /app

      volumes:
      - name: config-volume
        configMap:
          name: logger
```

### Manage Secret
* kubectl create secret generic apikey --from-literal=api_key=123456789
* kubectl get secret apikey -o yaml
* kubectl apply -f secretreader-deployment.yaml

```
    valueFrom:
        secretKeyRef:
            name: apikey
            key: api_key
```