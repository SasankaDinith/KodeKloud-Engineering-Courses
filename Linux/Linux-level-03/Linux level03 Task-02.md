## Task02 - Install And Configure SFTP

Some of the developers from `Nautilus` project team have asked for SFTP access to at least one of the app server in Stratos DC.
After going through the requirements, the system admins team has decided to configure the SFTP server on `App Server 2` server in `Stratos` Datacenter. 
Please configure it as per the following instructions:


- Create a SFTP user `siva` and set its password to `dCV3szSGNA`. There is already a group called ftp, you can utilise the same.

- Password authentication should be enabled for this user.

- SFTP user should only be allowed to make SFTP connections.

---

## Answer:

Step01: Login into app server 02 as root user
```
ssh steve@stapp02
sudo su
```
Step02: Create new user name as "siva" with using "ftp" group
```
sudo useradd -g ftp siva
```
Step03: Set a password into new user
```
passwd siva
```

Step04: Enable the password authentication in new user
```
vi /etc/ssh/sshd_config

(Find a line as Passwordlessauthentication Yes, and uncomment it)
```
Step05: Add below content at the end of sshd_config file
```
Match User siva
    ForceCommand internal-sftp
    PasswordAuthentication yes
    PermitTTY no
    AllowTcpForwarding no
```
Step06: Restart the sshd service
```
systemctl restart sshd
```
Step07: Verification 
```
sftp siva@stapp02
```

### Task is Completed!
