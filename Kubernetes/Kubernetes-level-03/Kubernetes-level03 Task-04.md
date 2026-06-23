## Task 04 - Persistent Volumes in Kubernetes

The Nautilus DevOps team is working on a Kubernetes template to deploy a web application on the cluster. There are some requirements to create/use persistent 
volumes to store the application code, and the template needs to be designed accordingly. Please find more details below:


1) Create a `PersistentVolume` named as `pv-datacenter`. Configure the `spec` as storage class should be `manual`, set capacity to `5Gi`, set access mode to `ReadWriteOnce`, 
volume type should be `hostPath` and set path to `/mnt/itadmin` (this directory is already created, you might not be able to access it directly, so you need not
to worry about it).

2) Create a `PersistentVolumeClaim` named as `pvc-datacenter`. Configure the `spec` as storage class should be `manual`, request `2Gi` of the storage, set access mode to
`ReadWriteOnce`.

3) Create a `pod` named as `pod-datacenter`, mount the persistent volume you created with claim name `pvc-datacenter` at document root of the web server, the container
within the pod should be named as `container-datacenter` using image `nginx` with `latest` tag only (remember to mention the tag i.e `nginx:latest`).

4) Create a node port type `service` named `web-datacenter` using node port `30008` to expose the web server running within the pod.

Note: The kubectl utility on the jump-host has been configured to work with the Kubernetes cluster.

## Answer:

Step01: Create pv.yaml file and added below content
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-datacenter
spec:
  storageClassName: manual
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/devops
```

Step02: Execute the pv.yaml file
```
kubectl apply -f pv.yaml
```

Step03: Create pvc.yaml file and added below content 
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-datacenter
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 3Gi
```
Step04: Execute the pvc.yaml file
```
kubectl apply -f pvc.yaml
```

Ste05: Create pod.yaml file and added below content 
```
apiVersion: v1
kind: Pod
metadata:
  name: pod-xfusion
  labels:
    app: web-server
spec:
  volumes:
    - name: storage-volume
      persistentVolumeClaim:
        claimName: pvc-xfusion
  containers:
    - name: container-xfusion
      image: httpd:latest
      volumeMounts:
        - name: storage-volume
          mountPath: /usr/local/apache2/htdocs
```

Step06: Execute the pod.yaml file
```
kubectl apply -f pod.yaml
```

Step07: Create svc.yaml file and added below content
```
apiVersion: v1
kind: Service
metadata:
  name: web-xfusion
spec:
  type: NodePort
  selector:
    app: web-server
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008
```
Step08: Execute the svc.yaml file
```
kubectl apply -f svc.yaml
```

### Task is Completed!
