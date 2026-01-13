## Task01: Git Rebase

The Nautilus application development team has been working on a project repository `/opt/games.git`. This repo is cloned at `/usr/src/kodekloudrepos` on `storage server` in `Stratos DC`. They recently shared the following requirements with DevOps team:



One of the developers is working on `feature` branch and their work is still in progress, however there are some changes which have been pushed into the `master` branch, the developer now wants to `rebase` the `feature` branch with the `master` branch without loosing any data from the `feature` branch, also they don't want to add any merge commit by simply merging the `master` branch into the `feature` branch. Accomplish this task as per requirements mentioned.


Also remember to push your changes once done.


---

## Answer:
Step01: Login to the Stroage server
``` bash
ssh natasha@ststor01
```
Step02: go to /usr/src/kodekloudrepos focler
``` bash
cd /usr/src/kodekloudrepos
```

Step: Type 'ls' command and find games folder and switch it
``` bash
ls

cd games
```

Step: rebase the feature branch
``` bash
git rebase origin/master
```

Step: Push to changes
``` bash
git push --force-with-lease origin feature
```


### Task is Completed!


