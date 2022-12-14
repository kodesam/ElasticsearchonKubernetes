Create PV
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-master-0
spec:
  capacity:
    storage: 30Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
      path: /pv/data-analytics
```
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-master-0
spec:
  capacity:
    storage: 100M
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Recycle
  storageClassName: standard
  hostPath:
      path: /Users/aamirsyed/WorkS/Elastic/data
  ```
### How to Deploy Elasticsearch with Seven Pods Using a Prebuilt Helm Chart ###

Step 1: Add the Bitnami Repository and Deploy the Elasticsearch Chart

1. Add the Bitnami Helm repository with:
```
helm repo add bitnami https://charts.bitnami.com/bitnami
```
2. Install the chart by running:
```
helm install elasticsearch --set master.replicas=3,coordinating.service.type=LoadBalancer bitnami/elasticsearch
```
3. Monitor the deployment with:
```
kubectl get pods
```
Step 3: Test the Connection
1. Forward the connection to port 9200:
```
kubectl port-forward svc/elasticsearch-master 9200
```
2. In another terminal tab, check the connection with:
```
curl localhost:9200
```
