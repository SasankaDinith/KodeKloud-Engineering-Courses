## Task02 - Kubernetes Sidecar Containers

Since containers are running on the same Pod, we can use a shared emptyDir volume to read and write logs.


1) Create a pod named `webserver`.

2) Create an `emptyDir` volume named `shared-logs`.

3) Create a regular container in the `webserver` pod from the `nginx:latest` image named `nginx-container`, and an init container from the `ubuntu:latest` image named `sidecar-container`.

4) Add the following command to the `sidecar-container "sh","-c","while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done"`

5) Mount the `shared-logs` volume in both containers at `/var/log/nginx`. Ensure all containers are in a running state.

Note: The kubectl utility on the `jump-host` has been configured to work with the Kubernetes cluster.

## Answer:

Step01: Create pod.yaml file
```
vi pod.yaml
```
Step02: Added below content to pod.yaml
```
apiVersion: v1
kind: Pod
metadata:
  name: webserver
spec:
  volumes:
    - name: shared-logs
      emptyDir: {}
  initContainers:
    - name: sidecar-container
      image: ubuntu:latest
      restartPolicy: Always
      command: ["sh", "-c", "while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done"]
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx
  containers:
    - name: nginx-container
      image: nginx:latest
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx
```

Step03: Execute the pod.yaml file
```
kubectl apply -f pod.yaml
```

### Task is Completed!
