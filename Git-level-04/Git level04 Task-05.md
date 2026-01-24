## Task05: Git Setup from Scratch

Some new developers have joined xFusionCorp Industries and have been assigned Nautilus project. They are going to start development on a new application, and some pre-requisites have been shared with the DevOps team to proceed with. Please note that all tasks need to be performed on `storage server` in `Stratos DC`.



a. Install `git`, set up any values for `user.email` and `user.name` globally and create a bare repository `/opt/official.git`.


b. There is an `update` hook (to block direct pushes to the `master` branch) under `/tmp` on `storage server` itself; use the same to block direct pushes to the `master` branch in `/opt/official.git` repo.


c. Clone `/opt/official.git` repo in `/usr/src/kodekloudrepos/official` directory.


d. Create a new branch named `xfusioncorp_official` in repo that you cloned under `/usr/src/kodekloudrepos` directory.


e. There is a `readme.md` file in `/tmp` directory on `storage server` itself; copy that to the repo, `add/commit` in the new branch you just created, and finally push your branch to the `origin`.


f. Also create `master` branch from your branch and remember you should not be able to push to the `master` directly as per the hook you have set up.

---

## Answer:


### Task is Completed!

