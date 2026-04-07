## Task05: Write a Docker File

As per recent requirements shared by the Nautilus application development team, they need custom images created for one of their projects. Several of the initial testing requirements are already been shared with DevOps team. Therefore, create a docker file `/opt/docker/Dockerfile` (please keep `D` capital of Dockerfile) on `App server 3` in `Stratos DC` and configure to build an image with the following requirements:

- Use `ubuntu` as the base image.

- Install `apache2` and configure it to work on `6200` port. (do not update any other Apache configuration settings like document root etc).

---

## Answer:

Step01: Create the required directory
```bash
sudo mkdir -p /opt/docker
cd /opt/docker
```
Step02: Create the Dockerfile
```bash
sudo vi Dockerfile

```
Step03: Add Dockerfile content
```bash
FROM ubuntu

# Update package list and install Apache
RUN apt-get update && apt-get install -y apache2

# Change Apache listening port to 6200
RUN sed -i 's/Listen 80/Listen 6200/' /etc/apache2/ports.conf

# Expose port 6200
EXPOSE 6200

# Start Apache in foreground
CMD ["apachectl", "-D", "FOREGROUND"]
```
Step04: Build the Docker Image
```bash
sudo docker build -t apache-custom:1.0 .
```
Step05: Run the Docker Container
```bash
sudo docker run -d -p 6200:6200 apache-custom:1.0
```
Step06: Verify the Setup
 ```bash
sudo docker ps

Test Apache access: curl http://localhost:6200

```

### Task is Completed!

