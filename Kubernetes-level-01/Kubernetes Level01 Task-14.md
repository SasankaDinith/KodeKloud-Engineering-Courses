## Task14: esolve VolumeMounts Issue in Kubernetes
We encountered an issue with our Nginx and PHP-FPM setup on the Kubernetes cluster this morning, which halted its functionality. Investigate and rectify the issue:



- The pod name is `nginx-phpfpm` and configmap name is `nginx-config`. Identify and fix the problem.


- Once resolved, copy `/home/thor/index.php` file from the jump host to the `nginx-container` within the nginx document root. After this, you should be able to access the `website` using Website button on the top bar.


Note: The kubectl utility on `jump_host` is configured to operate with the Kubernetes cluster.

---

## Answer:

Step01: Go to the edit mod of pod as  `nginx-phpfpm`
``` bash
kubectl edit pod nginx-phpfpm
```
Step02: Find the mountVolume section and change path as `/var/www/html`

Step03: Delete the pod 
``` bash
kubectl replace --force -f /tmp/kubectl-edit-1099384995.yaml
```

Step03: Copy the index.php file into nginx-container's root user
``` bash
kubectl cp index.php nginx-phpfpm:/index.php -c nginx-container
```
Step04: Go to nginx-container shell
``` bash
kubectl exec -it nginx-phpfpm -c nginx-container -- /bin/bash
```
Step: Check whether index.php file exists
```bash
ls -al
```
Step06: Copy this index.php file into /var/www/html folder
``` bash
cp index.php /var/www/html
```
Step07: Go to that folder and check index,php exists or not
``` bash
cd /var/www/html

ls
```

Step08: Verifying the process as click website button apper on right side, now you can see it's worked

### Task is Completed!
