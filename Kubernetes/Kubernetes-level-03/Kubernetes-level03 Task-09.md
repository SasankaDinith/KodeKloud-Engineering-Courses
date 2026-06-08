## Task09 - Deploy Iron Gallery App on Kubernetes

There is an iron gallery app that the Nautilus DevOps team was developing. They have recently customized the app and are going to deploy the same on the Kubernetes cluster. Below you can find more details:



1) Create a namespace `iron-namespace-datacenter`

2) Create a deployment `iron-gallery-deployment-datacenter` for iron gallery under the same namespace you created.

- Labels run should be `iron-gallery`.

- Replicas count should be `1`.

- Selector's matchLabels run should be `iron-gallery`.

- Template labels run should be `iron-gallery` under metadata.

- The container should be named as `iron-gallery-container-datacenter`, use `kodekloud/irongallery:2.0` image ( use exact image name / tag ).

- Resources limits for memory should be 100Mi and for CPU should be `50m`.

- First `volumeMount` name should be config, its mountPath should be `/usr/share/nginx/html/data`.

- Second `volumeMount` name should be images, its mountPath should be `/usr/share/nginx/html/uploads`.

- First `volume name` should be config and give it `emptyDir` and second volume name should be `images`, also give it `emptyDir`.

3) Create a deployment `iron-db-deployment-datacenter` for iron db under the same namespace.

- Labels db should be `mariadb`.

- Replicas count should be `1`.
- Selector's matchLabels db should be `mariadb`.

- Template labels `db` should be `mariadb` under metadata.

- The container name should be `iron-db-container-datacenter`, use `kodekloud/irondb:2.0` image ( use exact image name / tag ).

- Define environment, set `MYSQL_DATABASE` its value should be `database_host`, set `MYSQL_ROOT_PASSWORD` and `MYSQL_PASSWORD` value should be with some 
complex passwords for DB connections, and `MYSQL_USER` value should be any custom user ( except root ).
- Volume mount name should be db and its `mountPath` should be `/var/lib/mysql`. Volume `name` should be `db` and give it an `emptyDir`.

4) Create a service for iron db which should be named `iron-db-service-datacenter` under the same namespace. Configure spec as selector's db should be `mariadb`.
`Protocol` should be `TCP`, port and `targetPort` should be `3306` and its type should be `ClusterIP`.

5) Create a service for iron gallery which should be named `iron-gallery-service-datacenter` under the same namespace. Configure `spec` as selector's run should
be `iron-gallery`. Protocol should be `TCP`, `port` and `targetPort` should be `80`, `nodePort` should be `32678` and its type should be `NodePort`.


Note:


We don't need to make connection b/w database and front-end now, if the installation page is coming up it should be enough for now.

The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

## Answer:

Step01: Create namaspace.yaml file and added below content
```
apiVersion: v1
kind: Namespace
metadata:
  name: iron-namespace-datacenter
```

Step02: Create deployment1.yaml file and added below content
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: iron-gallery-deployment-datacenter
  namespace: iron-namespace-datacenter
  labels:
    run: iron-gallery
spec:
  replicas: 1
  selector:
    matchLabels:
      run: iron-gallery
  template:
    metadata:
      labels:
        run: iron-gallery
    spec:
      containers:
      - name: iron-gallery-container-datacenter
        image: kodekloud/irongallery:2.0
        resources:
          limits:
            memory: "100Mi"
            cpu: "50m"
        volumeMounts:
        - name: config
          mountPath: /usr/share/nginx/html/data
        - name: images
          mountPath: /usr/share/nginx/html/uploads
      volumes:
      - name: config
        emptyDir: {}
      - name: images
        emptyDir: {}
```

Step03: Create deployment2.yaml file and added below content
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: iron-db-deployment-datacenter
  namespace: iron-namespace-datacenter
  labels:
    db: mariadb
spec:
  replicas: 1
  selector:
    matchLabels:
      db: mariadb
  template:
    metadata:
      labels:
        db: mariadb
    spec:
      containers:
      - name: iron-db-container-datacenter
        image: kodekloud/irondb:2.0
        env:
        - name: MYSQL_DATABASE
          value: database_host
        - name: MYSQL_ROOT_PASSWORD
          value: "Str0ngR00tP@ssw0rd!"
        - name: MYSQL_USER
          value: gallery_admin
        - name: MYSQL_PASSWORD
          value: "Secur3Us3rP@ss!"
        volumeMounts:
        - name: db
          mountPath: /var/lib/mysql
      volumes:
      - name: db
        emptyDir: {}
```

Step04: Create service1.yaml file and added below content
```
apiVersion: v1
kind: Service
metadata:
  name: iron-db-service-datacenter
  namespace: iron-namespace-datacenter
spec:
  type: ClusterIP
  selector:
    db: mariadb
  ports:
  - protocol: TCP
    port: 3306
    targetPort: 3306
```

Step05: Create service2.yaml file and added below content
```
apiVersion: v1
kind: Service
metadata:
  name: iron-gallery-service-datacenter
  namespace: iron-namespace-datacenter
spec:
  type: NodePort
  selector:
    db: iron-gallery
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
    nodePort: 32678
```

Step06: Execute the yaml files 
```
kubectl apply -f namespace.yaml

kubectl apply -f deployment1.yaml

kubectl apply -f deployment2.yaml

kubectl apply -f service1.yaml

kubectl apply -f service2.yaml
```

### Task is Completed!
