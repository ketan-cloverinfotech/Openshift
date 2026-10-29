## What is ResourceQuata.


<img width="1774" height="887" alt="Kubernetes ResourceQuota Infographic Guide" src="https://github.com/user-attachments/assets/fb01a3af-1051-4e90-9e4b-9efd98f88438" />

### Manifest file
```
apiVersion: v1
kind: ResourceQuota
metadata:
  name: dev-resource-quota
  namespace: quota-demo
spec:
  hard:
    requests.cpu: "2"
    limits.cpu: "4"
    requests.memory: 4Gi
    limits.memory: 8Gi
    pods: "10"
    persistentvolumeclaims: "5"
    requests.storage: 50Gi
    services: "5"
    configmaps: "10"
    secrets: "20"
```
