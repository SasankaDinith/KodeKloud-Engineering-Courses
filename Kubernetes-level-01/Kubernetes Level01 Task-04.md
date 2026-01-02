## Task01: Set Resource Limits in Kubernetes Pods


The Nautilus DevOps team has noticed performance issues in some Kubernetes-hosted applications due to resource constraints. To address this, they plan to set limits on resource utilization. Here are the details:


- Create a pod named `httpd-pod` with a container named `httpd-container`. Use the `httpd` image with the `latest` tag (specify as `httpd:latest`). Set the following resource limits:

- Requests: Memory: 15Mi, CPU: 100m

- Limits: Memory: 20Mi, CPU: 100m

Note: The kubectl utility on `jump_host` is configured to operate with the Kubernetes cluster.

---

## Answer:

Step01: Create a pod-definition.yaml file
``` bash
vi pod-definition.yaml
```

Step02: Added below pod content 
``` bash
apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod
spec:
  containers:
  - name: httpd-container
    image: httpd:latest
    resources:
      requests:
        memory: "15Mi"
        cpu: "100m"
      limits:
        memory: "20Mi"
        cpu: "100m"
```

Step03: Create a pod
``` bash
kubectl apply -f pod-definition.yaml
```
Step04: Verify the pod creation
``` bash
kubectl get pods httpd-pod
```

### Task is Completed !

