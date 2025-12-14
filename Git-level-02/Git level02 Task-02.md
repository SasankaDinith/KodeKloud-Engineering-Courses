# Task 02: Git Create Branches

Nautilus developers are actively working on one of the project repositories, `/usr/src/kodekloudrepos/official` Recently, they decided to implement some new features in the application, and they want to maintain those new changes in a separate branch. Below are the requirements that have been shared with the DevOps team:

- On Storage server in Stratos DC create a new branch `xfusioncorp_official` from `master` branch in `/usr/src/kodekloudrepos/official` git repo.
- Please do not try to make any changes in the code.

---
## Answer:

Step01: login to server
``` bash
 ssh natasha@ststor01
```

Step02: Go to the repository
``` bash
cd /usr/src/kodekloudrepos/official
```

Step03: Create new brnach on master branch
``` bash
git switch -c xfusioncorp_official
```

Step04: Verify the branch was created from master
``` bash
git branch
```

## Task is Completed !
