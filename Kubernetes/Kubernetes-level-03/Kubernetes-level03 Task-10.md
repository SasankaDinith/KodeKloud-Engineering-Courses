## Task10 - Fix Python App Deployed on Kubernetes Cluster

One of the DevOps engineers was trying to deploy a python app on Kubernetes cluster. Unfortunately, due to some mis-configuration, the application is not coming up. Please take a look into it and fix the issues.
Application should be accessible on the specified nodePort.



1) The deployment name is `python-deployment-xfusion`, its using `poroko/flask-demo-app` image. The deployment and service of this app is already deployed.

2) nodePort should be `32345` and targetPort should be python flask app's default port.


`Note:` The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

## Answer:

Step01: Check the deployment available on application
```
kubecl get deploy
```

Step02: Open the deployment on edit mode and correct it's container image
```
kubectl edit deploy/python-deployment-xfusion
```

Step03: Check the service available on application
```
kubectl get service
```

Step04: Open the service on edit mode and update it's port and target port as 5000
```
kubectl edit service/python-service-xfusion
```

Step05: Click the App icon appered on right side on screen, you can see output as "Hello World Pyvo 1!"


### Task is Completed!
