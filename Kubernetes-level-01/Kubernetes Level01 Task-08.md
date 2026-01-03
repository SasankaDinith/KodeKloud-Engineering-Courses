## Task08: Schedule Cronjobs in Kubernetes

The Nautilus DevOps team is setting up recurring tasks on different schedules. Currently, they're developing scripts to be executed periodically. To kickstart the process, they're creating cron jobs in the Kubernetes cluster with placeholder commands. Follow the instructions below:

- Create a cronjob named devops.
- Set Its schedule to something like `*/3 * * * *`. You can set any schedule for now.
- Name the container `cron-devops`.
- Utilize the `nginx` image with `latest` tag (specify as nginx:latest).
- Execute the dummy command `echo Welcome to xfusioncorp!`.
- Ensure the restart policy is `OnFailure`.


Note: The  `kubectl` utility on `jump_host` is configured to work with the kubernetes cluster

---

## Answer:
 Step01: 
 ``` bash
vi cronjob.yaml
```

Step02: Added below cronjob yaml content
``` bash
apiVersion: batch/v1
kind: CronJob
metadata:
  name: devops
spec:
  schedule: "*/3 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: cron-devops
            image: nginx:latest
            imagePullPolicy: IfNotPresent
            command:
            - /bin/sh
            - -c
            - date; echo Welcome to xfusioncorp!
          restartPolicy: OnFailure
```
Step03: Execute cronjob.yaml file
``` bash
kubectl apply -f cronjob.yaml
```

Step04:  Verify the cronjob creation
``` bash
kubectl get cronjob devops
```

### Task is Completed!
