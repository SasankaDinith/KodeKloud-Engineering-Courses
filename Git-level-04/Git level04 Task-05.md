## Task05: Git Setup from Scratch

Some new developers have joined xFusionCorp Industries and have been assigned Nautilus project. They are going to start development on a new application, and some pre-requisites have been shared with the DevOps team to proceed with. Please note that all tasks need to be performed on `storage server` in `Stratos DC`.



a. Install `git`, set up any values for `user.email` and `user.name` globally and create a bare repository `/opt/official.git`.


b. There is an `update` hook (to block direct pushes to the `master` branch) under `/tmp` on `storage server` itself; use the same to block direct pushes to the `master` branch in `/opt/official.git` repo.


c. Clone `/opt/official.git` repo in `/usr/src/kodekloudrepos/official` directory.


d. Create a new branch named `xfusioncorp_official` in repo that you cloned under `/usr/src/kodekloudrepos` directory.


e. There is a `readme.md` file in `/tmp` directory on `storage server` itself; copy that to the repo, `add/commit` in the new branch you just created, and finally push your branch to the `origin`.


f. Also create `master` branch from your branch and remember you should not be able to push to the `master` directly as per the hook you have set up.

---

## Answer:

Step01: Login to the storage server as rool
```bash
ssh natasha@ststor01

sudo su
```

Step02: Update and install git 
```bash
sudo yum update -y

sudo yum install git -y
```

Step03: Set username and email with any values
```bash
git config --global user.name "natasha"
git config --global user.email "natasha@gmail.com"
```

Step04: Create a bare repository
``` bash
cd /opt
sudo git init --bare apps.git
```

Step05: Copy /tmp folder things to /opt/
```bash
sudo cp /tmp/update /opt/apps.git/hooks/
```
Step06: . Clone /opt/apps.git repo in /usr/src/kodekloudrepos/apps directory.
```bash
cd /usr/src/kodekloudrepos/

git clone /opt/apps.git
```

Step07: Switch to apps folder under the /usr/src/kodekloudrepos/
``` bash
cd apps/
```
Step08: Create a new branch "xfusioncorp_apps"
```bash
git checkout -b xfusioncorp_apps
```

Step09: Copy readme.md file into apps folder
```bash
sudo cp /tmp/readme.md .
```
Step10: add, commit in the new branch you just created, and finally push your branch to the origin
```bash
git add .

git commit -m "add readme.md"

git push --set-upstream origin xfusioncorp_apps
```

Step11: Switch to master bransh
```bash
git checkout -b master
```

### Task is Completed!


