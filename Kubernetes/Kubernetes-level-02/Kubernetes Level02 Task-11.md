## Task11 - Fix issue with LAMP Environment in Kubernetes

One of the DevOps team members was trying to install a WordPress website on a LAMP stack, which is deployed on a Kubernetes cluster. It was working well,
and we could see the installation page a few hours ago. However, something seems to have gone wrong with the stack after the website went down. 
Please look into the issue and fix it:



FYI, the deployment name is `lamp-wp` and it is using a service named `lamp-service`. Apache is using the default `HTTP` port, and the NodePort is `30008`. 
From the application logs, it has been identified that the application is facing some issues connecting to the database, in addition to other problems.
Additionally, there are some environment variables associated with the pods, such as `MYSQL_ROOT_PASSWORD`, `MYSQL_DATABASE`, `MYSQL_USER`, `MYSQL_PASSWORD`, 
and `MYSQL_HOST`

Also, do not attempt to delete or modify any other existing components, such as deployment names, service names, types, labels, secrets and so on.


`Note:` The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

