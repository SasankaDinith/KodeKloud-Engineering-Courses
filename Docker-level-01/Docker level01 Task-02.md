# Task 02 - Deploy Nginx Container on Application Server


The Nautilus DevOps team is conducting application deployment tests on selected application servers. They require a nginx container deployment on Application Server 2. Complete the task with the following instructions:


On Application Server 2 create a container named nginx_2 using the nginx image with the alpine tag. Ensure container is in a running state.

---

# Answer : 

```bash
# Step 01 - First login to the App server 02
ssh steve@stapp01

# Step 02 - Create a docker container name nginx_2 using nginx image with alpine tag.
docker run --name nginx_2 -d nginx:alpine

# Step 03 - Ensure container is in a running state
docker ps -a

You can see running containers as well.

```
## Task is Completed !

