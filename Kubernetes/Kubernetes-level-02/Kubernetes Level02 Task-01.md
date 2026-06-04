## Task01 - Kubernetes Shared Volumes

We are working on an application that will be deployed on multiple containers within a pod on Kubernetes cluster. There is a requirement to share a volume among 
the containers to save some temporary data. The Nautilus DevOps team is developing a similar template to replicate the scenario. Below you can find more details 
about it.


1). Create a pod named `volume-share-datacenter`.


2). For the first container, use image `ubuntu` with `latest` tag only and remember to mention the tag i.e `ubuntu:latest`, container should be named as
`volume-container-datacenter-1`, and run a `sleep` command for it so that it remains in running state. Volume `volume-share` should be mounted at path `/tmp/blog`.


3). For the second container, use image `ubuntu` with the `latest` tag only and remember to mention the tag i.e `ubuntu:latest`, container should be named as
`volume-container-datacenter-2`, and again run a `sleep` command for it so that it remains in running state. Volume `volume-share` should be mounted at path `/tmp/cluster`.


4). Volume name should be `volume-share` of type `emptyDir`.


5). After creating the pod, exec into the first container i.e `volume-container-datacenter-1`, and just for testing create a file `blog.txt` with the content
`Welcome to xFusionCorp Industries` under the mounted path of first container i.e `/tmp/blog`.


6). The file `blog.txt` should be present under the mounted path `/tmp/cluster` on the second container `volume-container-datacenter-2` as well, since they are
using a shared volume.


Note: The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

## Answer:

Step01: Create a yaml file as pod.yaml 
```
vi pod.yaml
```
Step02: Added below content to pod.yaml file
```
apiVersion: v1
kind: Pod
metadata:
  name: volume-share-datacenter
spec:
  containers:
    - name: volume-container-datacenter-1
      image: ubuntu:latest
      command: ["/bin/sh", "-c", "sleep 3600"]
      volumeMounts:
        - name: volume-share
          mountPath: /tmp/blog
    - name: volume-container-datacenter-2
      image: ubuntu:latest
      command: ["/bin/sh", "-c", "sleep 3600"]
      volumeMounts:
        - name: volume-share
          mountPath: /tmp/cluster
  volumes:
    - name: volume-share
      emptyDir: {}
```

Step03: Run the pod.yaml to create a pod
```
kubectl apply -f pod.yaml
```

Step04: Exec into the first container and create file as blog.txt with the content Welcome to xFusionCorp Industries under the mounted path of first container i.e /tmp/blog.
```
kubectl exec -it volume-share-datacenter -c volume-container-datacenter-1 --sh -c "echo 'Welcome to xFusionCorp Industries' > /tmp/blog/blog.txt"
```

Step05: Check the second container's /tmp/clutser location having blog.txt file 
```
kubectl exec -it volume-share-datacenter -c volume-container-datacenter-2 -- cat /tmp/cluster/blog.txt
```

### Task is Completed!
