## Task09: Configure Local Yum repos

The `Nautilus` production support team and security team had a meeting last month in which they decided to use `local yum` repositories for maintaing packages needed for their servers. For now they have decided to configure a `local yum` repo on `Nautilus Backup Server`. This is one of the pending items from last month, so please configure a `local yum` repository on `Nautilus Backup Server` as per details given below.


a. We have some packages already present at location `/packages/downloaded_rpms/` on `Nautilus Backup Server`.

b. Create a yum repo named `yum_local` and make sure to set `Repository ID` to `yum_local`. Configure it to use package's location `/packages/downloaded_rpms/`.

c. Install package `wget` from this newly created repo.

---

## Answer:

Step01: Login to backup server
```bash
ssh clint@stbkp01

sudo su
```

Step02: Switch to `/etc/yum.repos.d` folder
```bash
cd /etc/yum.repos.d
```
Step03: Create a `yum_local.repo` file and add the below content
``` bash
vi yum_local.repo

[yum_local]
name=yum_local
baseurl=file:///packages/downloaded_rpms/
enabled=1
gpgcheck=0
```

Step04: Clean the yum repo
```bash
yum clean all
```

Step05: Check yum repolist
```bash
yum repolist
```
Step06: Install the wget package 
```bash
sudo yum install wget -y
```

### Task is Completed!


