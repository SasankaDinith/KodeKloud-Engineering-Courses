## Task04 - Deploy Drupal App on Kubernetes

We need to deploy a Drupal application on Kubernetes cluster. The Nautilus application development team want to setup a fresh Drupal as they will do the installation on their own. Below you can find 
the requirements, they have shared with us.



1.) Configure a persistent volume `drupal-mysql-pv` with `hostPath = /drupal-mysql-data` (`/drupal-mysql-data` directory already exists on the worker Node i.e jump host), `5Gi` of storage and `ReadWriteOnce` access mode.


2.) Configure one PersistentVolumeClaim named `drupal-mysql-pvc` with storage request of `3Gi` and `ReadWriteOnce` access mode.


3.) Create a deployment `drupal-mysql` with `1` replica, use `mysql:5.7` image. Mount the claimed PVC at `/var/lib/mysql`.


4.) Create a deployment `drupal` with `1` replica and use `drupal:8.6` image.


5.) Create a `NodePort` type service which should be named as `drupal-service` and nodePort should be `30095`.


6.) Create a service `drupal-mysql-service` to expose mysql deployment on port `3306`.


7.) Set rest of the configration for deployments, services, secrets etc as per your preferences. At the end you should be able to access the Drupal installation page by clicking on `App` button.


`Note:` The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

## Answer:

Step01: Create pv.yaml file and added below content to it
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: drupal-mysql-pv
  labels:
    type: local
spec:
  storageClassName: manual
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /drupal-mysql-data
```
Step02: Execute the pv.yaml file
```
kubectl apply -f pv.yaml
```
Step03: Create pvc.yaml file and added below content to it
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: drupal-mysql-pvc
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
Step05: Create deployment1.yaml file and added below content to it
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: drupal-mysql
  labels:
    app: mysql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      volumes:
        - name: drupal-mysql-vol
          persistentVolumeClaim:
            claimName: drupal-mysql-pvc
      containers:
      - name: mysql
        image: mysql:5.7
        volumeMounts:
          - mountPath: /var/lib/mysql
            name: drupal-mysql-vol
        ports:
        - containerPort: 3306
        env:
            - name: MYSQL_ROOT_PASSWORD
              value: root_password
            - name: MYSQL_DATABASE
              value: drupal-database
```
Step06: Execute the deployment1.yaml file
```
kubectl apply -f deployment1.yaml
```
Step07: Create deployment2.yaml file and added below content to it
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: drupal
  labels:
    app: drupal
spec:
  replicas: 1
  selector:
    matchLabels:
      app: drupal
  template:
    metadata:
      labels:
        app: drupal
    spec:
      containers:
      - name: drupal
        image: drupal:8.6
        ports:
        - containerPort: 80
```
Step08: Execute the deployment2.yaml file
```
kubectl apply -f deployment2.yaml
```
Step09: Create services.yaml file and added below content to it
```
apiVersion: v1
kind: Service
metadata:
  name: drupal-service
spec:
  type: NodePort
  selector:
     app: drupal
  ports:
    - port: 80
      nodePort: 30095

---

apiVersion: v1
kind: Service
metadata:
  name: drupal-mysql-service
spec:
  type: ClusterIP
  selector:
     app: mysql
  ports:
     - name: mysql
       protocol: TCP
       port: 3306
       targetPort: 3306
```
Step10: Execute the services.yaml file
```
kubectl apply -f services.yaml
```
Step11: Click the App button on the top bar, you can see output as ""


### Task is Completed!
