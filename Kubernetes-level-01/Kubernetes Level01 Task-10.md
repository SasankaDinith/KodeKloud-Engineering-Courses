## Task10:  Set Up Time Check Pod in Kubernetes

The Nautilus DevOps team needs a time check pod created in a specific Kubernetes namespace for logging purposes. Initially, it's for testing, but it may be integrated into an existing cluster later. Here's what's required:


- Create a pod called `time-check` in the `devops` namespace. The pod should contain a container named `time-check`,
 utilizing the `busybox` image with the `latest` tag (specify as `busybox:latest`).

- Create a config map named `time-config` with the data `TIME_FREQ=4` in the same namespace.

- Configure the `time-check` container to execute the command: `while true; do date; sleep $TIME_FREQ;done`. Ensure the result is written `/opt/sysops/time/time-check.log`.
- Also, add an environmental variable `TIME_FREQ` in the container, fetching its value from the config map `TIME_FREQ` key.

- Create a volume `log-volume` and mount it at `/opt/sysops/time` within the container.

Note: The kubectl utility on jump_host is configured to operate with the Kubernetes cluster.

---

## Answer:

Step01:  Create a pod.yaml file
``` bash
vi pod.yaml
```

Step02: Added below configuration content to it 
``` bash
apiVersion: v1
kind: ConfigMap
metadata:
  name: time-config
  namespace: devops
data:
  TIME_FREQ: "4"
---
apiVersion: v1
kind: Pod
metadata:
  name: time-check
  namespace: devops
spec:
  containers:
  - name: time-check
    image: busybox:latest
    command: ["sh", "-c", "while true; do date >> /opt/sysops/time/time-check.log; sleep $TIME_FREQ; done"]
    env:
    - name: TIME_FREQ
      valueFrom:
        configMapKeyRef:
          name: time-config
          key: TIME_FREQ
    volumeMounts:
    - name: log-volume
      mountPath: /opt/sysops/time
  volumes:
  - name: log-volume
    emptyDir: {}
```

Step03: Create a pod, namespace and configmap
``` bash
kubectl apply -f pod.yaml
```

Step04: Verify the pod creation
``` bash
kubectl get pods -n devops
```

### Task is Completed!
