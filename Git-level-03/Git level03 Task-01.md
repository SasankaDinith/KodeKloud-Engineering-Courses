## Task01: Git Cherry Pick

The Nautilus application development team has been working on a project repository `/opt/ecommerce.git`. This repo is cloned at `/usr/src/kodekloudrepo`s on `storage server` in `Stratos DC`. They recently shared the following requirements with the DevOps team:



There are two branches in this repository, `master` and `feature`. One of the developers is working on the `feature` branch and their work is still in progress, however they want to merge one of the commits from the feature branch to the `master` branch, the message for the commit that needs to be merged into `master` is `Update info.txt`. Accomplish this task for them, also remember to push your changes eventually.


---

## Answer:
Step01: Login to storage server as root
```bash
ssh natasha@ststor01

sudo su
```

Step02: Change the directory to `/usr/src/kodekloudrepos`
``` bash
cd /usr/src/kodekloudrepos
```
Step03: Check the content of direcotory and go that directory
``` bash
ls
cd ecommerce/
```

Step04: Check the git branches having this directory
``` bash
git branch
```
Step05: Check the git logs about commits and copy the commit hash of `Update info.txt` commit
``` bash
git log --oneline
```

Step06: Switch to the master branch
```
git checkout master
```

Step07: Use cherry pick command
``` bash
git cherry-pick <commit_hash>
```

Step08: Push to the changes
``` bash
git push
```


### Task is Completed!


