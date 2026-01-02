## Task02: Deploy Applications with Kubernetes Deployments

The Nautilus DevOps team is delving into Kubernetes for app management. One team member needs to create a deployment following these details:


- Create a deployment named `httpd` to deploy the application `httpd` using the image `httpd:latest` (ensure to specify the tag)

Note: The `kubectl` utility on `jump_host` is set up to interact with the Kubernetes cluster.

---
## Answer:

Step01: Create a deployment with above requirements
``` bash
kubectl create deployment httpd --image=httpd:latest
```
Step02: Verify the deployment creation
``` bash
kubectl get deployments
```
### Task is Completed!
