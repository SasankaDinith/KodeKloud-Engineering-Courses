## Task01 - Deploy Apache Web Server on Kubernetes CLuster

There is an application that needs to be deployed on Kubernetes cluster under Apache web server. The Nautilus application development team has asked the
DevOps team to deploy it. We need to develop a template as per requirements mentioned below:


1) Create a `namespace` named as `httpd-namespace-devops`.

2) Create a `deployment` named as `httpd-deployment-devops` under newly created namespace. For the deployment use `httpd` image with `latest` tag only and remember 
to mention the tag i.e `httpd:latest`, and make sure replica counts are `2`.

3) Create a service named as `httpd-service-devops` under same namespace to expose the deployment, nodePort should be `30004`.

`Note:` The `kubectl` utility on the controlplane has been configured to work with the Kubernetes cluster.

## Answer:

Step01: Create a namespace.yaml file and added below content
```
apiVersion: v1
kind: Namespace
metadata:
  name: httpd-namespace-devops
```

Step02: Create a deployment.yaml file and added below content
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpd-deployment-devops
  namespace: httpd-namespace-devops
  labels:
    app: httpd_app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: httpd_app
  template:
    metadata:
      labels:
        app: httpd_app
    spec:
      containers:
      - name: httpd-container
        image: httpd:latest
        ports:
        - containerPort: 80
```

Step03: Create a service.yaml file and added below content
```
apiVersion: v1
kind: Service
metadata:
  name: httpd-service-devops
  namespace: httpd-namespace-devops
spec:
  type: NodePort
  selector:
    app: httpd_app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30004
```
Step04: Execute the yaml files
```
kubectl apply -f ns.yaml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### Task is Completed!
