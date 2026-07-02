## Task03 - Kubernetes Nginx and PhpFPM Setup

The Nautilus Application Development team is planning to deploy one of the php-based applications on Kubernetes cluster. As per the recent discussion with DevOps team, they have decided to use nginx and phpfpm.
Additionally, they also shared some custom configuration requirements. Below you can find more details. Please complete this task as per requirements mentioned below:


1.) Create a service to expose this app, the service type must be `NodePort`, nodePort should be `30012`.

2.) Create a config map named `nginx-config` for `nginx.conf` as we want to add some custom settings in nginx.conf.


  a.) Change the default port `80` to `8093` in `nginx.conf`.
  
  b.) Change the default document root `/usr/share/nginx` to `/var/www/html` in `nginx.conf`.
  
  c.) Update the directory index to `index  index.html index.htm index.php` in `nginx.conf`.


3.) Create a pod named `nginx-phpfpm `.


a.) Create a shared volume named `shared-files` that will be used by both containers `(nginx and phpfpm)` also it should be a `emptyDir` volume.


b.) Map the ConfigMap we declared above as a volume for nginx container. Name the volume as `nginx-config-volume`, mount path should be `/etc/nginx/nginx.conf` and subPath should be `nginx.conf`


c.) Nginx container should be named as `nginx-container` and it should use `nginx:latest` image. PhpFPM container should be named as `php-fpm-container` and it should use `php:8.1-fpm-alpine` image.


d.) The shared volume shared-files should be mounted at `/var/www/html` location in both containers. Copy `/opt/index.php` from `jump host` to the `nginx` document root inside the nginx container, once done you can access the app using `App` button on the top bar.


Before clicking on `finish` button always make sure to check if all pods are in `running` state.


`You can use any labels as per your choice.`


`Note:` The `kubectl` utility on `jump-host` has been configured to work with the kubernetes cluster.

## Answer:

Step01: Create deployment.yaml file and added below content to it
```
apiVersion: v1
kind: Service
metadata:
  name: httpd-service
spec:                         
  type: NodePort
  selector:
    app: nginx-app           
  ports:
    - protocol: TCP
      port: 80
      nodePort: 30012
      targetPort: 8091
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: nginx-config
data:
  nginx.conf: |
    events {}
    http {
        server {
            listen 8091;
            index index.html index.htm index.php;
            root /var/www/html;

            location / {
                try_files $uri $uri/ /index.php?$query_string;
            }

            location ~ \.php$ {
                include fastcgi_params;
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
                fastcgi_pass 127.0.0.1:9000; # Fixed: Capitalized on shared network namespace
            }
        }
    }
---
apiVersion: v1
kind: Service
metadata:
  name: php-fpm-service
spec:
  type: ClusterIP
  selector:
    app: php-app              
  ports:
    - protocol: TCP
      port: 9000
      targetPort: 9000
---
apiVersion: v1
kind: Pod
metadata:
  name: nginx-phpfpm
  labels:
    app: nginx-app
spec:
  containers:
    - name: nginx-container
      image: nginx:latest
      imagePullPolicy: IfNotPresent
      volumeMounts:
        - name: nginx-config-volume
          mountPath: /etc/nginx/nginx.conf
          subPath: nginx.conf
        - name: shared-files
          mountPath: /var/www/html
    - name: php-fpm-container
      image: php:8.1-fpm-alpine
      volumeMounts:
        - name: shared-files
          mountPath: /var/www/html
  restartPolicy: Always
  volumes:
    - name: shared-files
      emptyDir: {}
    - name: nginx-config-volume
      configMap:
        name: nginx-config    

```
Step02: Execute the deployment.yaml file
```
kubectl apply -f deployment.yaml
```

Step03: Copy /opt/index.php from jump host to the nginx document root inside the nginx container
```
kubectl cp /opt/index.php nginx-phpfpm:/var/www/html -c nginx-container
```
Step04: Verify the index.php file available under the nginx root 
```
kubectl exec -it nginx-phpfpm -- cat /var/www/html/index.php
```

Step05: Click the App button on the top bar, you can see it shows as "It works!"


### Task is Completed!
