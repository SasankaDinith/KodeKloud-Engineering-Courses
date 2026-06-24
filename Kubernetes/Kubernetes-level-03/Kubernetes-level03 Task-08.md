## Task08 - Kubernetes Troubleshooting

One of the Nautilus DevOps team members was working on to update an existing Kubernetes template. Somehow, he made some mistakes in the template and it is
failing while applying. We need to fix this as soon as possible, so take a look into it and make sure you are able to apply it without any issues. Also,
do not remove any component from the template like pods/deployments/volumes etc.


`/home/thor/mysql_deployment.yml` is the template that needs to be fixed.


`Note:` The `kubectl` utility on the jump-host has been configured to work with the Kubernetes cluster.

## Answer:

Step01: Open the mysql_deployment.yml file and correct it's issues
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mysql-pv
  labels:
    type: local
spec:
  storageClassName: standard
  capacity:
    storage: 250Mi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
  persistentVolumeReclaimPolicy: Retain
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pv-claim
  labels:
    app: mysql-app
spec:
  storageClassName: standard
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 250Mi
---
apiVersion: v1
kind: Service
metadata:
  name: mysql
  labels:
    app: mysql-app
spec:
  type: NodePort
  ports:
    - targetPort: 3306
      port: 3306
      nodePort: 30011
  selector:
    app: mysql-app
    tier: mysql
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-deployment
  labels:
    app: mysql-app
spec:
  selector:
    matchLabels:
      app: mysql-app
      tier: mysql
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: mysql-app
        tier: mysql
    spec:
      containers:
        - image: mysql:5.6
          name: mysql
          env:
            - name: MYSQL_ROOT_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mysql-root-pass
                  key: password
            - name: MYSQL_DATABASE
              valueFrom:
                secretKeyRef:
                  name: mysql-db-url
                  key: database
            - name: MYSQL_USER
              valueFrom:
                secretKeyRef:
                  name: mysql-user-pass
                  key: username
            - name: MYSQL_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mysql-user-pass
                  key: password
          ports:
            - containerPort: 3306
              name: mysql
          volumeMounts:
            - name: mysql-persistent-storage
              mountPath: /var/lib/mysql
      volumes:
        - name: mysql-persistent-storage
          persistentVolumeClaim:
            claimName: mysql-pv-claim

```

Step02: Execute the mysql_deployment.yml file 
```
kubectl apply -f mysql_deployment.yml
```

### Task is Completed!


