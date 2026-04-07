## Task04 : Update Git Repository with Sample HTML File

The Nautilus development team has initiated a new project development, establishing various Git repositories to manage each project's source code. Recently, a repository named `/opt/blog.git` was created. The team has provided a sampl `index.html` file located on the jump host under the `/tmp` directory. This repository has been cloned to `/usr/src/kodekloudrepos` on the `storage server` in the Stratos DC.

- Copy the sample `index.html` file from the `jump host` to the `storage server` placing it within the cloned repository at `/usr/src/kodekloudrepos/blog`.

- Add and commit the file to the repository.

- Push the changes to the `master` branch.

---

## Answer:

Step01: Copy index.html from Jump Host
```bash
ls /tmp/index.html

scp /tmp/index.html storage-server:/tmp/
```
Step02: Move File into Cloned Repository (Storage Server)
```bash
cd /usr/src/kodekloudrepos/blog

mv /tmp/index.html .
```
Step03: Add the File to Git
```bash
git add index.html
```
Step04: Commit the Changes
```bash
git commit -m "Added sample index.html file"
```
Step05: Push to Master Branch
```bash
git push origin master
```
Step06: Verification 
```bash
git log --oneline
```

### Task is Completed!
