## Task03 - Git Stash

The Nautilus application development team was working on a git repository `/usr/src/kodekloudrepos/news` present on `Storage server` in Stratos DC.
One of the developers stashed some in-progress changes in this repository, but now they want to restore some of the stashed changes.
Find below more details to accomplish this task:



- Look for the stashed changes under `/usr/src/kodekloudrepos/news` git repository, and restore the stash with `stash@{1}` identifier.
Further, commit and push your changes to the `origin`.

---

## Answer:

Step01: Navigate to the repository directory
``` bash
cd /usr/src/kodekloudrepos/news
```

Step02: Verify the stashes (optional but recommended)
``` bash
git stash list
git stash show stash@{1}
```

Step03: Apply the specific stash
``` bash
git stash apply stash@{1}
```

Step04: Stage and commit the changes
``` bash
git add .
git commit -m "Restored stashed changes from stash@{1}"
```

Step05: Push the changes to the origin
``` bash
git push origin <branch>
```


### Task is Completed!
