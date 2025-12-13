# Task03: Delete Docker Container

A container named `kke-container` was created by one of the Nautilus project developers on `App Server 2`. It was solely for testing purposes and now requires deletion. Execute the following task: <br/>

Delete the `kke-container` on `App Server 2` in Stratos DC.

---

# Answer:

Step 01:  SSH into App Server 2
``` bash
ssh banner@stapp02
```

Step 02: Check the container exists (Optional)
``` bash
docker ps -a | grep kke-container
```

Step 03: Stop the container (if running)
``` bash
docker stop kke-container
```
Step 04: Remove the container
``` bash
docker rm kke-container
```

## Task is complete !
