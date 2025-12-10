# Task 01 : Set Up Git Repository on Storage Server

The Nautilus development team has provided requirements to the DevOps team for a new application development project, specifically requesting the establishment of a Git repository. Follow the instructions below to create the Git repository on the Storage server in the Stratos DC: <br/>

Utilize yum to install the git package on the `Storage Server` <br/>
Create a bare repository named `/opt/news.git` (ensure exact name usage).<br/>

---

# Answer

### 1) Install Git via yum
```bash

sudo yum install -y git
git --version

```

### 2) Create the bare repository at /opt/news.git

```bash

# Create the directory (if /opt exists already, mkdir will just create news.git)
sudo mkdir -p /opt/news.git

# Initialize as a bare repository (no working tree)
sudo git init --bare /opt/news.git

```
### 3) Set ownership and permissions (optional)

``` bash

sudo chown -R devops:devops /opt/news.git
sudo chmod -R 775 /opt/news.git


```
