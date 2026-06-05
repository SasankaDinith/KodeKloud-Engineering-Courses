## Task03 - Deploy Nginx Web Server on Kubernetes Cluster

Some of the Nautilus team developers are developing a static website and they want to deploy it on Kubernetes cluster. They want it to be highly available
and scalable. Therefore, based on the requirements, the DevOps team has decided to create a deployment for it with multiple replicas. Below you can find more
details about it:


Create a deployment using `nginx` image with `latest` tag only and remember to mention the tag i.e `nginx:latest`. Name it as `nginx-deployment`. 
The container should be named as `nginx-container`, also make sure replica counts are 3.

Create a `NodePort` type service named `nginx-service`. The `nodePort` should be `30011`.

`Note:` The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

## Answer:

Step01: Create Deployment.yaml file and added below content
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx-app
    type: front-end
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-app
      type: front-end
  template:
    metadata:
      labels:
        app: nginx-app
        type: front-end
    spec:
      containers:
      - name: nginx-container
        image: nginx:latest
        ports:
        - containerPort: 80
```
Step02: Create svc.yaml file and added below content
```
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx-app
    type: front-end
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30011
```
Step03: Execute the deployment and service
```
kubectl apply -f Deployment.yaml svc.yaml
```

### Task is Completed!
