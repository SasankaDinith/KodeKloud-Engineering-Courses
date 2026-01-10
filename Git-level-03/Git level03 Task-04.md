## Task04: Git Clean

The Nautilus application development team was working on a git repository `/usr/src/kodekloudrepos/apps` present on `Storage server` in `Stratos DC`. One of the developers mistakenly created a couple of files under this repository, but now they want to clean this repository without adding/pushing any new files. Find below more details:



- Clean the `/usr/src/kodekloudrepos/apps` git repository without `adding/pushing` any new files, make sure `git status` is clean.

---

## Answer:
Step01: Login to storge server
``` bash
ssh natasha@ststor01
```

Step02: Navigate the repository 
```bash
cd /usr/src/kodekloudrepos/apps
```

Step03: Clean the repository
``` bash
git clean -f
```
Step04: Verify the process
``` bash
git status
```
So now you can see the `git status` is clean.


### Task is Completed!

