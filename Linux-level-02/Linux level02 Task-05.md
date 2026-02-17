## Task05: Linux SSH Authentication

The system admins team of `xFusionCorp Industries` has set up some scripts on `jump host` that run on regular intervals and perform operations on all app servers in `Stratos Datacenter`. To make these scripts work properly we need to make sure the thor user on jump host has password-less SSH access to all app servers through their respective sudo users (i.e `tony` for app server 1). Based on the requirements, perform the following:



Set up a password-less authentication from user `thor` on jump host to all app servers through their respective sudo users.


---

## Answer:
Step01: Create new key-pair on jump host
``` bash
ssh-keygen
```

Step02: Copy this ssh key in to every app servers
``` bash
ssh-copy-id tony@stapp01

ssh-copy-id steve@stapp02

shh-copy-id banner@stapp03
```
Step03: Verify the password-less authentication login 
```bash
ssh tony@stapp01
ssh steve@stapp02
ssh banner@stapp03
```

### Task is Completed!

