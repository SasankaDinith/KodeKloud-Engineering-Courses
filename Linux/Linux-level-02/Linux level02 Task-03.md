## Task03: Linux Collaborative Directories
The Nautilus team doesn't want its data to be accessed by any of the other groups/teams due to security reasons and want their data to be strictly accessed by the `sysadmin` group of the team.



Setup a collaborative directory `/sysadmin/data` on `app server 2` in `Stratos Datacenter`.


The directory should be group owned by the group `sysadmin` and the group should own the files inside the directory. The directory should be `read/write/execute` to the user and group owners, and `others` should not have any access.

---

## Answer:

Step01: Login to the app server 02 as root
``` bash
ssh banner@stapp02

sudo su
```

Step02: Check whether sysadmin folder exists
```bash
getent group | grep sysadmin
```

Step03: Create new folder inside sysadmin folder
``` bash
sudo mkdir -p /sysadmin/data
```

Step04: Setup the new folder ownership
```bash
chown -R root:sysadmin /sysadmin/data
```

Step05: Change the permissions of folder
```bash
sudo chmod 770 /sysadmin/data
```
Step06:  Verify the permissions/changes
``` bash
sudo ls -l /sysadmin
```

### Task is Completed!

