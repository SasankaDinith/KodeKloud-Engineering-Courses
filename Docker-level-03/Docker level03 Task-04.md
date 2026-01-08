## Task04: Save, Load and Transfer Docker Image

One of the DevOps team members was working on to create a new custom docker image on `App Server 1` in `Stratos DC`. He is done with his changes and image is saved on same server with name `cluster:nautilus`. Recently a requirement has been raised by a team to use that image for testing, but the team wants to test the same on `App Server 3`.
So we need to provide them that image on `App Server 3` in `Stratos DC`.


a. On `App Server 1` save the image `cluster:nautilus` in an archive.


b. Transfer the image archive to `App Server 3`.


c. Load that image archive on `App Server 3` with same name and tag which was used on `App Server 1`.


Note: Docker is already installed on both servers; however, if its service is down please make sure to start it.


---

## Answer:
Step01: Login to the App server01
``` bash
ssh tony@stapp01
```

Step: Check the docker images
```bash
docker image ls
```
Step03: Save the cluster:nautilus image as archive under the /tmp folder
``` bash
docker save -o /tmp/nautilus.tar cluster:nautilus
```

Step04:  Copy the tar file on App server 03
``` bash
scp /tmp/nautilus.tar banner@stapp03:/tmp
```
Step05: Login on App server02 & switch to root user

``` bash
ssh banner@stapp03

sudo su
```

Step06: Start Docker service if its not active
``` bash
systemctl start docker
systemctl status docker
```

Step07: Load that image archive 
```bash
 docker load -i nautilus.tar
```
Step08: Validate the task by docker images
``` bash
docker image ls
```

Now you can see passing image to app server 03 from app server 01


### Task is Completed!

