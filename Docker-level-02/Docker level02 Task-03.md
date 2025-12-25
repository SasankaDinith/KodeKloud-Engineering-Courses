# Task03: Create a Docker Image From Container

One of the Nautilus developer was working to test new changes on a container. He wants to keep a backup of his changes to the container. A new request has been raised for the DevOps team to create a new image from this container. Below are more details about it:

- Create an image `ecommerce:nautilus` on `Application Server 2` from a container `ubuntu latest` that is runing on same server.

## Answer:

Step01: Login to the App server 2
``` bash
ssh steve@stapp02
```
Step02: Find the container name or ID
```bash
docker ps
```
Step03: Create the image from that container
``` bash
docker commit <container_id_or_name> ecommerce:nautilus
```
Step04: Check the new image
```bash
docker images
```

### Task is Completed !
