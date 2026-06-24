## Task05 - Manage Secrets in Kubernetes

The Nautilus DevOps team is working to deploy some tools in Kubernetes cluster. Some of the tools are licence based so that licence
information needs to be stored securely within Kubernetes cluster. Therefore, the team wants to utilize Kubernetes secrets to store those secrets.
Below you can find more details about the requirements:



1) We already have a secret key file `news.txt` under the `/opt/` directory. Create a `generic secret` named news, it should contain the password/license-number 
present in `news.txt` file.


2) Also create a `pod` named `secret-nautilus`.


3) Configure pod's spec as container name should be `secret-container-nautilus`, image should be `fedora` with `latest` tag (remember to mention the tag with image).
    Use `sleep` command for container so that it remains in running state. Consume the created secret and mount it under `/opt/cluster` within the container.


4) To verify you can exec into the container `secret-container-nautilus`, to `check` the secret key under the mounted path `/opt/cluster`. Before hitting the Check 
button please make sure pod/pods are in running state, also validation can take some time to complete so keep patience.


`Note:` The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

## Answer:

Step01: Create a generic secret name as news
```
kubectl create secret generic news --form-file=/opt/news.txt
```
Step02: Create pod.yaml file and added below content
```
apiVersion: v1
kind: Pod
metadata:
  name: secret-nautilus
spec:
  volumes:
    - name: secret-volume
      secret:
        secretName: news
  containers:
    - name: secret-container-nautilus
      image: fedora:latest
      command: ["/bin/bash", "-c", "sleep 3600"]
      volumeMounts:
        - name: secret-volume
          mountPath: /opt/cluste
```
Step03: Execute the pod.yaml file 
```
kubectl apply -f pod.yaml
```

### Task is Completed!
