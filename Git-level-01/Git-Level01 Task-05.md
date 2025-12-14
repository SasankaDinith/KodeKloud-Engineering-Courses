# Task05 : Delete Git Branch

The Nautilus developers are engaged in active development on  one of the project repositories located at `/usr/src/kodekloudrepos/games/`
During testing, sevaral test branches were created, and now they require cleanup.
Here are the requiremnts provided to the DevOps team:

- on the  `Storage server` in Stratos DC, delete a branch named `xfusioncrop_games` from the  `/usr/src/kodekloudrepos/games/` Git repository.

---

## Answer

Step01: Navigate to the repository and check status
``` bash
cd /usr/src/kodekloudrepos/games/
git status
```

Step02: See if the branch exists (local and/or remote)
``` bash
git branch
```

Step03: Delete the local branch
``` bash
git branch -D xfusioncrop_games
```

## Task is Completed !
