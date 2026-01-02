## Task01: Deploy Pods in Kubernetes Cluster

The Nautilus DevOps team is diving into Kubernetes for application management. One team member has a task to create a pod according to the details below:


- Create a pod named `pod-httpd` using the `httpd` image with the `latest` tag. Ensure to specify the tag as `httpd:latest`.

- Set the app label to `httpd_app`, and name the container as `httpd-container`.

Note: The kubectl utility on jump_host is configured to operate with the Kubernetes cluster.


---

## Answer:

Step01: Create a pod.yaml file with above requirments
``` bash
vi pod.yaml
```
Step02: Added below yaml content to it
``` bash
apiVersion: v1
kind: Pod
metadata:
  name: pod-httpd
  labels:
    app: httpd_app
spec:
  containers:
  - name: httpd-container
    image: httpd:latest
    ports:
    - containerPort: 80
```
Step03: Create a pod
``` bash
kubectl apply -f pod.yaml
```
Step04: Verify the pod
```bash
kubectl get pods
```


### Task is Completed!
