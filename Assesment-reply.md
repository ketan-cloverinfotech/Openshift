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


## LimitRange in Kubernetes / OpenShift
**LimitRange controls the minimum, maximum, and default CPU and memory settings for individual containers or Pods inside a namespace.**
### Practical LimitRange YAML
```
apiVersion: v1
kind: LimitRange
metadata:
  name: dev-limit-range
  namespace: quota-demo
spec:
  limits:
    - type: Container
      min:       # Below this reject the request                                                   
        cpu: 100m
        memory: 128Mi
      max:      # Above this reject the request 
        cpu: "1"
        memory: 1Gi
      defaultRequest:  # When not mentioned in manifest use this 
        cpu: 250m
        memory: 256Mi
      default:                  # this **default** is **default limit** of each container get 
        cpu: 500m
        memory: 512Mi
```

<img width="1536" height="1024" alt="Kubernetes LimitRange Infographic Guide" src="https://github.com/user-attachments/assets/e2262dbc-200a-4c77-b741-ef469b36009e" />
