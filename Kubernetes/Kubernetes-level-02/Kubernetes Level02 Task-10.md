## Task10 - Troubleshoot Deployment issues in Kubernetes

Last week, the Nautilus DevOps team deployed a redis app on Kubernetes cluster, which was working fine so far. This morning one of the team members 
was making some changes in this existing setup, but he made some mistakes and the app went down. We need to fix this as soon as possible. Please take a look.



The deployment name is `redis-deployment`. The pods are not in running state right now, so please look into the issue and fix the same.


`Note:` The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

## Answer:

Step01: Check the pod's current status
```
kubectl get pods
```

Step02: Open the redis-deployment with edit mode
```
kubectl edit deployment redis-deployment
```
Step03: Modify the image name and configmap name, save and exit

Step04: Again checks the pod's status
```
kubectl get pods
```


### Task is Completed!
