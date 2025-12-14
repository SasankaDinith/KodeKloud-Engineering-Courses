# Task 03: Git Merge Branches

The Nautilus application development team has been working on a project repository `/opt/demo.git`. This repo is cloned at `/usr/src/kodekloudrepos` on `storage server` in Stratos DC. They recently shared the following requirements with DevOps team:

- Create a new branch nautilus in `/usr/src/kodekloudrepos/demo` repo from master and copy the `/tmp/index.html` file (present on storage server itself) into the repo. 

- Further, add/commit this file in the new branch and merge back that branch into `master` branch.
  
- Finally, push the changes to the origin for both of the branches.

---

## Answer:

Step01: Login to the server
``` bash
ssh natasha@ststor01
```

Step02: Navigate to the Repository
``` bash
cd /usr/src/kodekloudrepos/demo
```
Step03: Ensure You Are on master
``` bash
git checkout master
```
Step04: Create a New Branch nautilus from master
``` bash
git checkout -b nautilus master

```
Step05: Copy index.html into the Repo
``` bash
cp -f /tmp/index.html ./index.html
```
Step06: Stage and Commit the File
``` bash
git add index.html
git commit -m "Add index.html from /tmp on nautilus branch"

```
Step07: Push the nautilus Branch to Remote
``` bash
git push -u origin nautilus
```
Step08: Merge nautilus Back into master
``` bash

git checkout master
git merge nautilus
```
Step09: Push master to Remote
``` bash
git push origin master
```

## Task is Completed !


