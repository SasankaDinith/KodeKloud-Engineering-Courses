## Task07: Deploy ReplicaSet in Kubernetes Cluster

The Nautilus DevOps team is gearing up to deploy applications on a Kubernetes cluster for migration purposes. A team member has been tasked with creating a ReplicaSet outlined below:

- Create a ReplicaSet using `httpd` image with `latest` tag (ensure to specify as `httpd:latest`) and name it `httpd-replicaset`.
- 
- Apply labels: app as `httpd_app`, type as `front-end`.

- Name the container `httpd-container`. Ensure the replica count is `4`.


Note: The `kubectl` utility on `jump_host` is set up to interact with the Kubernetes cluster.

---

## Answer:
Step01: Create a replicaset.yaml file
``` bash
vi replicaset.yaml
```
Step02: Added below confiduration content to it
``` bash
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: httpd-replicaset
spec:
  replicas: 4
  selector:
    matchLabels:
      app: httpd_app
  template:
    metadata:
      labels:
        app: httpd_app
        type: front-end
    spec:
      containers:
      - name: httpd-container
        image: httpd:latest
        ports:
        - containerPort: 80

```
Step03: Execute to replicaset.yaml file
``` bash
kubectl apply -f httpd-replicaset.yaml

```

Step: Verify the replicaset creation
``` bash
kubectl get replicaset httpd-replicaset

kubectl get pods -l app=httpd_app
```

### Task is Completed!

### Task is Completed!

