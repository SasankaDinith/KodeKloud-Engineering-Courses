## Task09 - Deploy Node App on Kubernetes

The Nautilus development team has completed development of one of the node applications, which they are planning to deploy on a Kubernetes cluster.
They recently had a meeting with the DevOps team to share their requirements. Based on that, the DevOps team has listed out the exact requirements to
deploy the app. Find below more details:


Create a deployment using ``kodekloud/centos-ssh-enabled:node` image, replica count must be `2`.

Create a service to expose this app, the service type must be `NodePort`, targetPort must be `8080` and `nodePort` should be `30012`.

Make sure all the pods are in `Running` state after the deployment.

You can check the application by clicking on `NodeApp` button on top bar.


`You can use any labels as per your choice.`


`Note:` The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

## Answer:

Step01: Create deployment.yaml file and added below content
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: node-deployment
  labels:
    app: node-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: node-app
  template:
    metadata:
      labels:
        app: node-app
    spec:
      containers:
      - name: node-container
        image: kodekloud/centos-ssh-enabled:node
```

Step02: Create service.yaml file and added below content
```
apiVersion: v1
kind: Service
metadata:
  name: node-deployment
spec:
  type: NodePort
  selector:
    app: node-app
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
      nodePort: 30012
```

Step03: Execute the yaml files
```
kubectl apply -f deployment.yaml

kubectl apply -f service.yaml
```

### Task is Completed!




