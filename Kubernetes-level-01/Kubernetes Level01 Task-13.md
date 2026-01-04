## Task13: Deploy Highly Available Pods with ReplicationController
The Nautilus DevOps team is establishing a ReplicationController to deploy multiple pods for hosting applications that require a highly available infrastructure. Follow the specifications below to create the ReplicationController:


- Create a ReplicationController using the `nginx` image with `latest` tag, and name it `nginx-replicationcontroller`.

- Assign labels app as `nginx_app`, and type as `front-end`. Ensure the container is named `nginx-container` and set the replica count to `3`.

- All pods should be running state `post-deployment`.


Note: The kubectl utility on `jump_host` is configured to operate with the Kubernetes cluster.

---

## Answer:

Step01: Create a yaml file as replicaset.yaml
``` bash
vi replicaset.yaml
```

Step02: Added below configurations to it 
``` bash
apiVersion: v1
kind: ReplicationController
metadata:
  name: nginx-replicationcontroller
spec:
  replicas: 3
  selector:
    app: nginx_app
  template:
    metadata:
      labels:
        app: nginx_app
        type: front-end
    spec:
      containers:
      - name: nginx-container
        image: nginx:latest
        ports:
        - containerPort: 80
```
Step03: Execute to replicaset.yaml file
``` bash
kubectl apply -f replicaset.yaml
```

Step04: Verify the created replicaset and pods
``` bssh
kubectl get rc
kubectl get pods -l app=nginx_app
```


### Task is Completed!
