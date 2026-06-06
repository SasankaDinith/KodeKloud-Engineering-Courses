## Task05 - Rolling Updates And Rolling Back Deployments in Kubernetes


There is a production deployment planned for next week. The Nautilus DevOps team wants to test the deployment update and rollback on Dev environment first 
so that they can identify the risks in advance. Below you can find more details about the plan they want to execute.



Create a namespace `datacenter`. Create a deployment called `httpd-deploy` under this new namespace, It should have one container called `httpd`,
use `httpd:2.4.27` image and `2` replicas. The deployment should use `RollingUpdate` strategy with `maxSurge=1`, and `maxUnavailable=2`. Also create a
`NodePort` type service named `httpd-service` and expose the deployment on `nodePort: 30008`.


Now upgrade the deployment to version `httpd:2.4.43` using a rolling update.


Finally, once all pods are updated undo the recent update and roll back to the previous/original version.


Note:

a. The kubectl utility on the jump-host has been configured to work with the Kubernetes cluster.


b. Please make sure you only use the specified image(s) for this deployment and as per the sequence mentioned in the task description. 
If you mistakenly use a wrong image and fix it later, that will also distort the revision history which can eventually fail this task.

## Answer:

Step01: Create a namespace.yaml file and added below content
```
apiVersion: v1
kind: Namespace
metadata:
  name: datacenter
```

Step02: Create a deployment.yaml file and added below content
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpd-deploy
  namespace: datacenter
  labels:
    app: httpd
spec:
  replicas: 2
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 2
  selector:
    matchLabels:
      app: httpd
  template:
    metadata:
      labels:
        app: httpd
    spec:
      containers:
      - name: httpd
        image: httpd:2.4.27
        ports:
        - containerPort: 80
```

Step03: Create a service.yaml file and added below content
```
apiVersion: v1
kind: Service
metadata:
  name: httpd-service
  namespace: datacenter
spec:
  type: NodePort
  selector:
    app: httpd
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30008

```
Step04: Execute the yaml files
```
kubectl apply -f namespace.yaml deployment.yaml service.yaml
```

### Task is Completed!
