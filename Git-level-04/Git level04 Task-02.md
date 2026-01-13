## Task02: Manage Git Repositories

A new developer just joined the Nautilus development team and has been assigned a new project for which he needs to create a new repository under his account on Gitea server. Additionally, there is some existing data that need to be added to the repo. Below you can find more details about the task:


Click on the Gitea UI button on the top bar. You should be able to access the `Gitea UI`. Login to Gitea server using username `max` and password `Max_pass123`.


a. Create a new git repository `story_news` under `max` user.


b. SSH into `storage server` using user `max` and password `Max_pass123` and clone this newly created repository under user `max` home directory i.e `/home/max`.


c. Copy all files from location `/usr/data` to the repository and `commit/push` your changes to the master branch. The commit message must be `"add stories"` (must be done in single commit).


d. Create a new branch `max_apps` from `master`.


e. Copy a file `story-index-max.txt` from location `/tmp/stories/` to the repository. This file has a typo, which you can fix by changing the word `Mooose` to `Mouse`. Commit and push the changes to the newly created branch. Commit message must be `"typo fixed for Mooose"` (must be done in single commit).


Note: For these kind of scenarios requiring changes to be done in a web UI, please take screenshots so that you can share it with us for review in case your task is marked incomplete. You may also consider using a screen recording software such as loom.com to record and share your work.``

---

## Answer:

Step01: Click on the Gitea UI button on the top bar. Login to Gitea server using username max and password Max_pass123.

Step02: Create a new git repository story_news under max user.

Step03: SSH into storage server using user max and password Max_pass123 and clone this newly created repository under user max home directory
``` bash
ssh max@ststor01

git clone: :repository url>
```

Step04:  Copy all files from location /usr/data to the repository and commit/push your changes to the master branch. 
``` bash
sudo scp /usr/data/* /story_news

ls

git commit - "add stories"

git push
```

Step05:  Create a new branch max_apps from master.
``` bash
git branch max_apps
```

Step06: Switch to newly created branch
``` bash
git checkout max_apps
```
Step07:  Copy a file story-index-max.txt from location /tmp/stories/ to the repository.
``` bash
sudo scp /tmp/stories/story-index-max.txt .
```
Step08: After open this .txt file in VI editor chanage Mooose to Mouse. Then Commit and push the changes to the newly created branch. 
``` bash
git commit -m "typo fixed for Mooose"

git push

```


### Task is Completed!


