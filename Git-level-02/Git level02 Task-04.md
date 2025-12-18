# Task 04: Git Manage Remotes

The xFusionCorp development team added updates to the project that is maintained under `/opt/apps.git` repo and cloned under `/usr/src/kodekloudrepos/apps`
Recently some changes were made on Git server that is hosted on Storage server in Stratos DC. The DevOps team added some new Git remotes, so we need to update remote on `/usr/src/kodeklodrepos/apps` repository as per details mentioned below:

- In `/usr/src/kodekloudrepos/apps` repo add a new remote dev apps and point it to `/opt/xfusioncorp_apps.git` repository.
- There is a file `/tmp/index.html` on same server; copy this file to the repo and add/commit to `master` branch.
- Finally pushmaster branch to this new remote origin.

---
## Answer:

Step01: Go to the repository
``` bash
cd /usr/src/kodekloudrepos/apps
```
Step02: Check the current branch
``` bash
git branch --show-current
```
Step03: Add the new remote
``` bash
git remote add dev_apps /opt/xfusioncorp_apps.git
```
Step04: Copy the file into the repo
``` bash
cp /tmp/index.html .
```
Step05:  Stage and commit the file
``` bash
git add index.html

git commit -m "Added index.html"
```
Step06: Push the master branch to the new remote
``` bash
git push dev_apps master
```
## Task is Completed !



