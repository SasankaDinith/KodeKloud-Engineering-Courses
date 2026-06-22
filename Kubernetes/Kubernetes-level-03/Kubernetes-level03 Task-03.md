## Task03 - Init Containers in Kubernetes

There are some applications that need to be deployed on Kubernetes cluster and these apps have some pre-requisites where some configurations need to be 
changed before deploying the app container. Some of these changes cannot be made inside the images so the DevOps team has come up with a solution
to use init containers to perform these tasks during deployment. Below is a sample scenario that the team is going to test first.



1) Create a Deployment named as `ic-deploy-devops`.


2) Configure `spec` as `replicas` should be `1`, labels `app` should be `ic-devops`, template's `metadata` lables `app` should be the same `ic-devops`.


3) The `initContainers` should be named as `ic-msg-devops`, use image `debian` with `latest` tag and use command `'/bin/bash', '-c' and 'echo Init Done - Welcome to xFusionCorp Industries > /ic/blog'`.
 The volume mount should be named as `ic-volume-devops` and mount path should be `/ic`.


4) Main container should be named as `ic-main-devops`, use image `debian` with `latest` tag and use command `'/bin/bash', '-c' and 'while true; do cat /ic/blog; sleep 5; done'`.
The `volume mount` should be named as `ic-volume-devops` and `mount path` should be `/ic`.


5) `Volume` to be named as `ic-volume-devops` and it should be an `emptyDir` type.


`Note:` The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.


## Answer:

Step01: Create deployment.yaml file and added below content
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ic-deploy-devops
  labels:
    app: ic-devops
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ic-devops
  template:
    metadata:
      labels:
        app: ic-devops
    spec:
      volumes:
        - name: ic-volume-devops
          emptyDir: {}
      initContainers:
        - name: ic-msg-devops
          image: debian:latest
          command:
            - /bin/bash
            - -c
            - "echo Init Done - Welcome to xFusionCorp Industries > /ic/blog"
          volumeMounts:
            - name: ic-volume-devops
              mountPath: /ic
      containers:
        - name: ic-main-devops
          image: debian:latest
          command:
            - /bin/bash
            - -c
            - "while true; do cat /ic/blog; sleep 5; done"
          volumeMounts:
            - name: ic-volume-devops
              mountPath: /ic

```

Step02: Execute the yaml file 
```
kubectl apply -f deployment.yaml
```

### Task is Completed!
