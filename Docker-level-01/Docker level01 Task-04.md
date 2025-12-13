#  04: Copy File to Docker Container

The Nautilus DevOps team possesses confidential data on `App Server 2` in the Stratos Datacenter. <br/>
A container named `ubuntu_latest` is running on the same server. <br/>
Copy an encrypted file `/tmp/nautilus.txt.gpg` from the docker host to the `ubuntu_latest` container located at `/home/.` <br/>
Ensure the file is not modified during this operation.

--- 
# Answer :

Step 01: SSH into App Server 2
``` bash
ssh banner@stapp02
```
Step 02: Verify the container is running
``` bash
sudo docker ps | grep ubuntu_latest
```

Step 03: Use docker cp to copy the file
``` bash
sudo docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/home/
```

Step 04: Verify the file inside the container
``` bash
sudo docker exec ubuntu_latest ls -l /home/
```
You should see nautilus.txt.gpg listed.

## Task is Complete !
