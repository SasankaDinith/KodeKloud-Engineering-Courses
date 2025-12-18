# Task02: Docker Update Permissions

One of the Nautilus project developers need access to run docker commands on `App Server 1`. This user is already created on the server. Accomplish this task as per details given below:

- User `anita` is not able to run docker commands on `App Server 1` in Stratos DC, make the required changes so that this user can run docker commands without `sudo`.

---
## Answer:

Step01: Login to the App server 01
``` bash
ssh tony@stapp01
```
Step02: Check the group Docker have enable users 
``` bash
gatent group docker
```
Step03: Set user anita to group Docker
```bash
sudo usermod -aG docker anita
```

## Task is Completed !
