# Task01: Pull Docker Image

Nautilus project developers are planning to start testing on a new project. As per their meeting with the DevOps team, they want to test containerized environment application features. As per details shared with DevOps team, we need to accomplish the following task:

- Pull `busybox:must` image on `App Server 1` in Stratos DC and re-tag (create new tag) this image as `busybox:blog`.

---

## Answer:

Step01: Login to App server 01
```bash
ssh tony@stapp01
```
Step02: Pull the docker image as busybox:must
``` bash
docker pull busybox:must
```
Step03: Re-tag image to busybox:blod
```bash
docker tag busybox:must busybox:blog
```

## Task is Completed !

