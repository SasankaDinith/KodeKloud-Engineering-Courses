# Task 02: Clone Git Repository on Storage Server
The DevOps team created a Git repository at `/opt/games.git`. The Nautilus application team needs a working copy of this repository on the Storage Server at   `/usr/src/kodekloudrepos`. 

Requirements:

- Perform the clone as the natasha user. <br/>
- Do not modify repository contents or change permissions on existing directories. <br/>
- Clone `/opt/games.git` into `/usr/src/kodekloudrepos` in a way that results in a subdirectory named after the repo (e.g., /usr/src/kodekloudrepos/games).

---

# Answer

1) Switch to the natasha user
``` bash
ssh natasha@hostname
```

2) Navigate to the target directory
``` bash
cd /usr/src/kodekloudrepos
```

3) Clone the bare repository into a subdirectory named after the repo (games)

``` bash
git clone /opt/games.git

```

This will create /usr/src/kodekloudrepos/games automatically because git clone uses the repo name as the folder name by default.

