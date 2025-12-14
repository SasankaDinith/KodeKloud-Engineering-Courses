# Task 02: Git Create Branches
The Nautilus development team shared with the DevOps team requirements for new application development, setting up a Git repository for that project. Create a Git repository on the Storage server in Stratos DC as per the details given below:

- Install the git package using yum on the `Storage server`.

- After that, create/init a git repository named `/opt/beta.git` (use the exact name as asked and make sure not to create a bare repository).

---

## Answer:

Step 1: Login to the storage server
``` bash
ssh natasha@ststor01
```

Step 2: Git installation
```bash
sudo yum install git -y
```

Step 3: Creating/initiating an empty repository
``` bash
sudo mkdir -p /opt/beta.git
```
## Task is Completed !
