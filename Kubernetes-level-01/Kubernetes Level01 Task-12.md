## Task12: Update Deployment and Service in Kubernetes
An application deployed on the Kubernetes cluster requires an update with new features developed by the Nautilus application development team. The existing setup includes a deployment named nginx-deployment and a service named nginx-service. Below are the necessary changes to be implemented without deleting the deployment and service:


1.) Modify the service nodeport from `30008` to `32165`

2.) Change the replicas count from `1` to `5`

3.) Update the image from `nginx:1.19` to `nginx:latest`

Note: The kubectl utility on `jump_host` is configured to operate with the Kubernetes cluster.

---

## Answer:

Step01: First you need to go to service details as follows
```bash
kubectl describe svc nginx-service
```

Step02: Then go to the edit mode and change nodeport from `30008` to `32165`
``` bash
kubectl edit svc nginx-service
```

Step03: Then go to the edit mode of deployment
``` bash
kubectl edit deploy nginx-deployment
```

Step04: Change the replicas count from `1` to `5` and Update the image from `nginx:1.19` to `nginx:latest`


Step05: Finally you can check updated deployment and service as running below commands
``` bash
kubectl get pods
kubectl get deploy  nginx-deployment
kubectl get svc nginx-service
```
Then you can see 5 pods are running, and service port number is changed to 32165 as well.

### Task is Completed!




