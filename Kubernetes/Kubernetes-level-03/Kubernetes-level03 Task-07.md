## Task07 - Kubernetes LEMP Setup


The Nautilus DevOps team wants to deploy a static website on a Kubernetes cluster. They plan to use Nginx, PHP-FPM, and MySQL for the database. The team has already gathered the requirements
and now wants to make the website live. More details can be found below:

1) Create some secrets for MySQL.
   - Create a secret named `mysql-root-pass` with key/value pairs as below:
```
name: password
value: R00t
```
   - Create a secret named `mysql-user-pass` with key/value pairs as below:
```
name: username
value: kodekloud_joy

name: password
value: Rc5C9EyvbU
```
  - Create a secret named `mysql-db-url` with key/value pairs as below:
```
name: database
value: kodekloud_db6
```
 - Create a secret named mysql-host with key/value pairs as below:
```
name: host
value: 127.0.0.1
```

Note: In this lab, `MySQL` is deployed as a sidecar container in the same Pod as the web container. To avoid connectivity issues with Service-based access in this
lab setup, set the mysql-host secret value to `127.0.0.1`.
The `mysql-service` resource must still be created as required by the task, but the application should connect using localhost.

2) Create a config map `php-config` for `php.ini` with `variables_order = "EGPCS"` data.

3) Create a deployment named `lemp-wp`.

4) Create two containers under it. First container must be `nginx-php-container` using image `webdevops/php-nginx:alpine-3-php7` and second container must be `mysql-container` from image `mysql:5.6`.
Mount `php-config` configmap in nginx container at `/opt/docker/etc/php/php.ini` location.

5) Add some environment variables for both containers:
   - `MYSQL_ROOT_PASSWORD`, `MYSQL_DATABASE`, `MYSQL_USER`, `MYSQL_PASSWORD` and `MYSQL_HOST`. 
   Take their values from the secrets you created. Please make sure to use env field (do not use envFrom) to define the name-value pair of environment variables.

6) Create a node port type service `lemp-service` to expose the web application, nodePort must be `30008`.

7) Create a service for mysql named `mysql-service` and its port must be `3306`.

8) We already have a `/tmp/index.php` file on the `jump-host`.

   - Copy this file into the nginx container under document root i.e `/app` and replace the dummy values for mysql related variables with the environment variables you have set for mysql related parameters. 
   Please make sure you do not hard code the mysql related details in this file, you must use the environment variables to fetch those values.
   - Once done, you must be able to access this website using `Website` button on the top bar, please note that you should see `Connected successfully` message while accessing this page.
  
`Note:` The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.



## Answer:

Step01: Create above 4 secrets
```
kubectl create secret generic mysql-root-pass --from-literal=password=R00t
kubectl create secret generic mysql-user-pass --from-literal=username=kodekloud_joy --from-literal=password=Rc5C9EyvbU
kubectl create secret generic mysql-db-url --from-literal=database=kodekloud_db6
kubectl create secret generic mysql-host --from-literal=host=127.0.0.1

```
Step02: Create cm.yaml file and added below content to it
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: php-config
data:
  php.ini:
    variables_order = "EGPCS"
```
Step03: Execute the cm.yaml file
```
kubectl apply -f cm.yaml
```
Step04: Create deployment.yaml file and added below content to it 
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: lemp-wp
  labels:
    app: lemp-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: lemp-app
  template:
    metadata:
      labels:
        app: lemp-app
    spec:
      volumes:
        - name: php-config-volume
          configMap:
            name: php-config
      containers:
        # First Container: Nginx + PHP-FPM
        - name: nginx-php-container
          image: webdevops/php-nginx:alpine-3-php7
          volumeMounts:
            - name: php-config-volume
              mountPath: /opt/docker/etc/php/php.ini
              subPath: php.ini
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

        # Second Container: Sidecar MySQL Database
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
```
Step04: Execute the deployment.yaml file
```
kubectl apply -f deployment.yaml
```
Step05: Expose the above deployment as Nodeport service type
```
kubectl expose deployment lemp-wp --type=NodePort --name=lemp-service --port=80
```
Step06: Expose the above deployment as mysql service
```
kubectl expose deployment lemp-wp --type=ClusterIP --name=mysql-service --port=3306
```

Step07: Copy /tmp/index.php file into above created pod's nginx container under the /app location
```
kubectl cp /tmp/index.php <pod_name>:/app/index.php -c nginx-php-container
```
Step08: Login to that nginx container
```
kubectl exec -it <pod_name> -- sh
```
Step09: Switch to /app directory and verify it's having copied index.php file
```
cd /app
ls
```
Step10: Modify index.php file
```
<?php
$dbname = $_ENV['MYSQL_DATABASE'];
$dbuser = $_ENV['MYSQL_USER'];
$dbpass = $_ENV['MYSQL_PASSWORD'];
$dbhost = $_ENV['MYSQL_HOST'];

$connect = mysqli_connect($dbhost, $dbuser, $dbpass) or die("Unable to Connect to '$dbhost'");

$test_query = "SHOW TABLES FROM $dbname";
$result = mysqli_query($test_query);

if ($result->connect_error) {
   die("Connection failed: " . $conn->connect_error);
}
  echo "Connected successfully";
```
Step11: Save and exit the editor

Step12: Click the Website button appered on right side lab screen, you can see output as "Connected successfully"


### Task is Completed!
