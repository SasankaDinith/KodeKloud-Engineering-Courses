## Task09: Create Countdown Job in Kubernetes

The Nautilus DevOps team is crafting jobs in the Kubernetes cluster. While they're developing actual scripts/commands, they're currently setting up templates and testing jobs with dummy commands. Please create a job template as per details given below:


- Create a job named `countdown-xfusion`.

- The spec template should be named `countdown-xfusion` (under metadata), and the container should be named `container-countdown-xfusion`

- Utilize image `fedora` with `latest` tag (ensure to specify as `fedora:latest`), and set the restart policy to `Never`.

- Execute the command  `sleep 5`

Note: The `kubectl` utility on `jump_host` is set up to operate with the Kubernetes cluster.

---

## Answer:

Step01: Create a file called countdown.yaml
``` bash
vi countdown.yaml
```
Step02: Added below configuration content to it
``` bash
apiVersion: batch/v1
kind: Job
metadata:
  name: countdown-xfusion
spec:
  template:
    metadata:
      name: countdown-xfusion
    spec:
      containers:
      - name: container-countdown-xfusion
        image: fedora:latest
        command: ["sleep", "5"]
      restartPolicy: Never
```
Step03: Execute to countdown.yaml file
``` bssh
kubectl apply -f countdown.yaml
```

Step04: Verify the process
``` bash
kubectl get jobs
```

### Task is Completed!
