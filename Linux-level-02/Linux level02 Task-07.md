## Task07: Install a package

As per new application requirements shared by the `Nautilus` project development team, several new packages need to be installed on all app servers in `Strator Datacenter`. Most of them are completed except for `git`.

Therefore, install the `git` package on all `app servers.`

---

## Answer:

Step01: Login to app server 01 as root
```bash
ssh tony@stapp01

sudo su
```

Step02: Install to the telnet package
```bash
yum install telnet -y
```

Step03: Verify the package installation
```bash
which telnet
```

This process continue all app servers (02,03) as well



### Task is Completed!

