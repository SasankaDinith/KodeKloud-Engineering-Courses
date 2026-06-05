## Task07 - Deploy Grafana on Kubernetes Cluster



The Nautilus DevOps teams is planning to set up a Grafana tool to collect and analyze analytics from some applications.
They are planning to deploy it on Kubernetes cluster. Below you can find more details.



1.) Create a deployment named `grafana-deployment-nautilus` using any `grafana` image for `Grafana app`. Set other parameters as per your choice.


2.) Create `NodePort` type service with nodePort `32000` to expose the app.


`You do not need to make any configuration changes inside the Grafana app once deployed; just make sure you can access the Grafana login page.`


`Note:` The `kubectl` utility on the `jump-host` has been configured to work with the Kubernetes cluster.

## Answer: 

Step01: Create deployment.yaml file and added below content
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-deployment-nautilus
  labels:
    app: grafana
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      containers:
        - name: grafana-container-nautilus
          image: grafana/grafana:latest
          imagePullPolicy: IfNotPresent
          ports:
          - containerPort: 3000
            name: http-grafana
          resources:
            requests:
              memory: "512Mi"
              cpu: "250m"
            limits:
              memory: "1Gi"
              cpu: "500m"
```

Step02: Create service.yaml file and added below content
```
apiVersion: v1
kind: Service
metadata:
  name: grafana-service-nautilus
spec:
  type: NodePort
  selector:
    app: grafana
  ports:
    - port: 3000
      targetPort: 3000
      nodePort: 32000
```

Step03: Execute the yaml files
```
kubectl apply -f deployment.yaml service.yaml
```

### Task is Completed!
