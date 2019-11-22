# Istio Installation
## Install Istioctl
    - Download from https://github.com/istio/istio/releases
    - Add Environment Variables (Path)
## เนื่องจาก template ที่ได้มาตอน download istio ต้องการ  Ram
    ```
    resources:
    requests:
        cpu: 500m
        memory: 2048Mi
    ```
 
### แก้ปัญหาโดยการเพิ่ม ram ให้กับ Docker ก่อนถึงจะ start ได้
* เปิด Docker for windows ไปที่ Preferences เลือก Tab Advances
* เพิ่มเป็น 4G
* Run คำสั่ง kubectl apply -f install/kubernetes/istio-demo.yaml (ไฟล์อยู่ใน folder ที่ download มาจาก Istio)
 
### Run คำสั่งนี้เพื่อสร้าง istio จาก template ที่ helm มีให้ (ปรับ memory เป็น 512Mi)
```
    helm template install/kubernetes/helm/istio (ไฟล์อยู่ใน folder ที่ download มาจาก Istio)
        --name istio --namespace istio-system
        --set pilot.resources.requests.memory="512Mi" | kubectl apply -f -
    *** kubectl apply -f - เป็นการ apply โดยใช้ output จากคำสั่งก่อนหน้า ****
    
    หรือปรับ config ต่างๆตามนี้
    helm install install/kubernetes/helm/istio --name istio
        --namespace istio-system
        --set gateways.istio-ingressgateway.type=NodePort
        --set gateways.istio-egressgateway.type=NodePort
        --set sidecarInjectorWebhook.enabled=false
        --set global.mtls.enabled=false
        --set tracing.enabled=true | kubectl apply -f -
```

## Check การติดตั้งตามนี้
* kubectl api-resources | grep istio
* kubectl get crd | grep istio
* kubectl get gateway
* kubectl get svc -n istio-system
* kubectl get pod -n istio-system
 
## ทำการ Inject Proxy เข้าไปใน samples/helloworld/helloworld.yaml(ได้มาจากตอน Download Istio) ด้วยคำสั่งนี้
* istioctl kube-inject -f hostname.yaml | kubectl apply -f -
 
## จะเห็นว่าใน 1 pod มี 2 container
* kubectl get pods 