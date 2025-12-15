# Task 04: Git Manage Remotes

The xFusionCorp development team added updates to the project that is maintained under `/opt/apps.git` repo and cloned under `/usr/src/kodekloudrepos/apps`
Recently some changes were made on Git server that is hosted on Storage server in Stratos DC. The DevOps team added some new Git remotes, so we need to update remote on `/usr/src/kodeklodrepos/apps` repository as per details mentioned below:

- In `/usr/src/kodekloudrepos/apps` repo add a new remote dev apps and point it to `/opt/xfusioncorp_apps.git` repository.
- There is a file `/tmp/index.html` on same server; copy this file to the repo and add/commit to `master` branch.
- Finally pushmaster branch to this new remote origin.

---
## Answer:

Step 1: Go to the repository
``` bash
cd /usr/src/kodekloudrepos/apps
```


