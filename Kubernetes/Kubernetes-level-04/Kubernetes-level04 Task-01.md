## Task01 - Deploy Redis Deployment on Kubernetes

The Nautilus application development team observed some performance issues with one of the application that is deployed in Kubernetes cluster. After looking into number of factors, the team has suggested 
to use some in-memory caching utility for DB service. After number of discussions, they have decided to use Redis. Initially they would like to deploy Redis on kubernetes cluster for testing and later they
will move it to production. Please find below more details about the task:


Create a redis deployment with following parameters:

1) Create a config map called my-redis-config having maxmemory 2mb in redis-config.

2) Name of the deployment should be `redis-deployment`, it should use `redis:alpine` image and container name should be `redis-container`. Also make sure it has only `1` replica.

The container should request for `1` CPU.

Mount `2` volumes:

a. An Empty directory volume called data at path `/redis-master-data`.

b. A configmap volume called redis-config at path `/redis-master`.

c. The container should expose the port `6379`.

Finally, `redis-deployment` should be up and running.

`Note:` The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

## Answer:

Step01: Create a configmap.yaml file and added below content to it
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-redis-config
data:
  redis-config:
    maxmemory 2mb
```
Step02: Execute the configmap.yaml file 
```
kubectl apply -f configmap.yaml
```
Step03: Create a deployment.yaml file and added below content to it
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-deployment
  labels:
    app: redis
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis
  template:
    metadata:
      labels:
        app: redis
    spec:
      containers:
      - name: redis-container
        image: redis:alpine
        ports:
        - containerPort: 6379
        resources:
          requests:
            cpu: "1"
        volumeMounts:
        - name: data
          mountPath: /redis-master-data
        - name: redis-config
          mountPath: /redis-master
      volumes:
      - name: data
        emptyDir: {}
      - name: redis-config
        configMap:
          name: my-redis-config
```
Step04: Execute the deployment.yaml file
```
kubectl apply -f deployment.yaml
```
Step05: Check the deployement status
```
kubectl get deploy
```

### Task is Completed!
