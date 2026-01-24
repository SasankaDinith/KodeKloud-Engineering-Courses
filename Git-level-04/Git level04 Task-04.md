## Task04: Git Hook

The Nautilus application development team was working on a git repository `/opt/cluster.git` which is cloned under `/usr/src/kodekloudrepos` directory present on `Storage server` in `Stratos DC`. The team want to setup a hook on this repository, please find below more details:



Merge the `feature` branch into the `master` branch, but before pushing your changes complete below point.

Create a post-update hook in this git repository so that whenever any changes are pushed to the `master` branch, it creates a `release` tag with name `release-2023-06-15`, where `2023-06-15` is supposed to be the current date. For example if today is `20th June, 2023` then the release tag must be `release-2023-06-20`. Make sure you test the hook at least once and create a release tag for today's release.

Finally remember to push your changes.
Note: Perform this task using the natasha user, and ensure the repository or existing directory permissions are not altered.

---

## Answer:

Step01: Switch to the Storage Server
``` bash
ssh natasha@ststor01
```
Step02: Navigate to the Repository
``` bash
cd /usr/src/kodekloudrepos/cluster.git
```
Step03: Check branches and merge feature Branch into master
``` bash
git branch

git checkout master

git merge feature
```

Step04: Create the post-update Hook, and navigate directory to create post-update file
``` bash
sudo vi /opt/cluster.git/hooks/post-update
```

Step05: Add the following script
``` bash
#!/bin/bash
cd /opt/cluster.git
tag=release-$(date "+%Y-%m-%d")
git tag $tag
```

Step06: Make it executable
``` bash
chmod +x /opt/cluster.git/hooks/post-update
```
 Step07: Check git status and push changes
 ``` bash
git status

git push
```



### Task is Completed!




