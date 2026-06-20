## Task02 - Deploy Lamp Stack on Kubernetes Cluster

The Nautilus DevOps team wants to deploy a PHP website on a Kubernetes cluster. They plan to use Apache as the web server and MySQL for the database.
The team has already gathered the requirements and now wants to make the website live. More details can be found below:



1) Create a ConfigMap named `php-config` containing the data `variables_order = "EGPCS"` for the `php.ini` file.

2) Create a Deployment named `lamp-wp`.

3) Within this Deployment, create two containers. The first container should be named `httpd-php-container` and utilize the
image `webdevops/php-apache:alpine-3-php7`. The second container should be named `mysql-container` and use the image `mysql:5.6`. Mount the `php-config` ConfigMap 
in the `httpd` container at the location `/opt/docker/etc/php/php.ini`.

4) Note that secrets have already been created for the following MySQL-related values: MySQL root password, MySQL user, MySQL password, MySQL host, 
and MySQL database. These secrets are securely stored and can be accessed as needed.

5) Add the following environment variables for both containers: `MYSQL_ROOT_PASSWORD`, `MYSQL_DATABASE`, `MYSQL_USER`, `MYSQL_PASSWORD`, and `MYSQL_HOST`.
Ensure that their values are sourced from the secrets created earlier. Please utilize the `env` field (do not use `envFrom`) to define the name-value pairs
of the environment variables.

6) Create a `NodePort` type Service named `lamp-service` to expose the web application, specifying the NodePort as `30008`.

7) Create a Service for MySQL named `mysql-service`, ensuring its port is set to `3306`.

8) A file named `/tmp/index.php` is available on the `jump-host`.

a) Copy this file into the `httpd` container under the Apache document root at `/app`, replacing the dummy values for
MySQL-related variables with the corresponding environment variables you have defined. Ensure that the MySQL-related details are not hardcoded
in this file, and utilize environment variables to retrieve those values.

b) You should be able to access the `index.php` file through NodePort `30008`. Upon accessing this page, the message `Connected successfully` should be displayed.

`Note:` The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.


## Answer

Step01: Create php-config.yaml
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: php-config
data:
  php.ini: |
    variables_order = "EGPCS"
```
Step02: Execute the php-config.yaml file
```
kubectl apply -f php-config.yaml
```

Step03: Create lamp-wp.yaml
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: lamp-wp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: lamp
  template:
    metadata:
      labels:
        app: lamp
    spec:
      containers:

      - name: httpd-php-container
        image: webdevops/php-apache:alpine-3-php7
        ports:
        - containerPort: 80

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

        - name: MYSQL_HOST
          valueFrom:
            secretKeyRef:
              name: mysql-host
              key: host

        volumeMounts:
        - name: php-config-volume
          mountPath: /opt/docker/etc/php/php.ini
          subPath: php.ini

      - name: mysql-container
        image: mysql:5.6

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

        - name: MYSQL_HOST
          valueFrom:
            secretKeyRef:
              name: mysql-host
              key: host

      volumes:
      - name: php-config-volume
        configMap:
          name: php-config
```

Step04: Execute the lamp-wp.yaml
```
kubectl apply -f lamp-wp.yaml
```

Step05: Create service1.yaml
```
apiVersion: v1
kind: Service
metadata:
  name: lamp-service
spec:
  type: NodePort
  selector:
    app: lamp
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30008
```

Step06: Execute the service1.yaml file
```
kubectl apply -f service1.yaml
```

Step07: Create service2.yaml
```
apiVersion: v1
kind: Service
metadata:
  name: mysql-service
spec:
  selector:
    app: lamp
  ports:
  - port: 3306
    targetPort: 3306
```
Step08: Execute the service2.yaml file
```
kubectl apply -f service2.yaml
```

Step09: Copy index.php to httpd container under /app directory
```
kubectl cp /tmp/index.php lamp-wp-6f8b7df9d4-abcde:/app/index.php -c httpd-php-container
```
Step10: Edit index.php
```
kubectl exec -it lamp-wp-6f8b7df9d4-abcde -c httpd-php-container -- sh

vi /app/index.php
```

Step11: Verify the connectivity
```
get Node ip: kubectl get nodes -o wide
Test: curl http://<NODE-IP>:30008/index.php
or,

Click the website button right side on lab screen and you can see "Connected successfully" as output.
```

### Task is Completed!
