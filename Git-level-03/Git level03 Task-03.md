## Task03: Git hard reset
The Nautilus application development team was working on a git repository `/usr/src/kodekloudrepos/demo` present on `Storage server` in `Stratos DC`. This was just a test repository and one of the developers just pushed a couple of changes for testing, but now they want to clean this repository along with the commit history/work tree, so they want to point back the `HEAD` and the branch itself to a commit with message `add data.txt file`. Find below more details:



- In `/usr/src/kodekloudrepos/demo` git repository, reset the git commit history so that there are only two commits in the commit history i.e `initial commit` and `add data.txt file`.


Also make sure to push your changes.

---

## Answer:

Step01: SSH into storgae server
```bash
ssh natasha@ststor01
```

Step02: Navigate to the repository directory:
``` bash
cd /usr/src/kodekloudrepos/demo
```

Step03: View the commite history
``` bash
git log --oneline
```
Step04: Reset the current branch to the hash of the second commie
``` bash
git reset --hard <commit_hash>
```
Step05: Force push the changes to the remote repository
``` bash
git push --force
```


### Task is Completed!

