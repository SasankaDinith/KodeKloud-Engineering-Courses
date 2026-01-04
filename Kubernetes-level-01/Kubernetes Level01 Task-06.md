## Task06: Revert Deployment to Previous Version in Kubernetes
Earlier today, the Nautilus DevOps team deployed a new release for an application. However, a customer has reported a bug related to this recent release. Consequently, the team aims to revert to the previous version.


- There exists a deployment named `nginx-deployment`; initiate a rollback to the previous revision.

Note: The `kubectl` utility on `jump_host` is configured to interact with the Kubernetes cluster.

---


## Answer:

Step01: Rollout previous updates
``` bash
kubectl rollout undo deployment/nginx-deployment

```
Step02: Monitor the status of the rollback
``` bash
kubectl rollout status deployment/nginx-deployment
```
### Task is Completed!
