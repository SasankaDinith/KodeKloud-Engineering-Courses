## Task03: Setup Kubernetes Namespaces and PODs
The Nautilus DevOps team is planning to deploy some micro services on Kubernetes platform. The team has already set up a Kubernetes cluster and now they want to set up some namespaces, deployments etc. Based on the current requirements, the team has shared some details as below:


- Create a namespace named `dev` and deploy a `POD` within it. Name the pod `dev-nginx-pod` and use the `nginx` image with the `latest` tag. Ensure to specify the tag as `nginx:latest`.

Note: The kubectl utility on jump_host is configured to operate with the Kubernetes cluster.

---

## Answer:

Step01: Craete a namespace.yaml file
``` bash
vi namespace.yaml
```
Step02: Added below content to it
``` bash
apiVersion: v1
kind: Namespace
metadata:
  name: dev
---
apiVersion: v1
kind: Pod
metadata:
  name: dev-nginx-pod
  namespace: dev
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
```

Step03: Run the namespace.yaml file
``` bash
kubectl apply -f namespace.yaml
```



### Task is Completed!
