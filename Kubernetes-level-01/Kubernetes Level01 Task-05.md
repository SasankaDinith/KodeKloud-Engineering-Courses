## Task05: Execute Rolling Updates in Kubernetes
An application currently running on the Kubernetes cluster employs the nginx web server. The Nautilus application development team has introduced some recent changes that need deployment. They've crafted an image nginx:1.19 with the latest updates.


- Execute a rolling update for this application, integrating the `nginx:1.19` image. The deployment is named `nginx-deployment`.

- Ensure all pods are operational post-update.

Note: The `kubectl` utility on `jump_host` is set up to operate with the Kubernetes cluster

---

## Answer:

Step01: Identify your container name:
``` bash
kubectl describe deployment nginx-deployment
```
Step02: Start the rolling update 
``` bash
kubectl set image deployment/nginx-deployment nginx-container=nginx:1.19
```
Step03: Check the status about rolling update 
``` bash
kubectl rollout status deployment/nginx-deployment
```
Step04: Check the new image in pods
``` bash
kubectl get pods
```



### Task is Completed!
