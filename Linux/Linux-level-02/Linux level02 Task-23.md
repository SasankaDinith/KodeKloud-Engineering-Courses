## Task23: Linux LogRotate

The `Nautilus` DevOps team is ready to launch a new application, which they will deploy on app servers in `Stratos Datacenter`. They are expecting significant traffic/usage of `squid` on app servers after that. This will generate massive logs, creating huge log files. To utilise the storage efficiently, they need to compress the log files and need to rotate old logs. Check the requirements shared below:


a. In all app servers install `squid` package.

b. Using `logrotate` configure `squid` logs rotation to monthly and keep only 3 rotated logs.

(If by default log rotation is set, then please update configuration as needed)

---

## Answer: 

Step01: Login app server 01 as root user
```bash
ssh tony@stapp01

sudo su
```

Step02: Install squid packaage
```bash
yum install -y squid
```

Step03: Enable the squid service
```bash
systemctl enable squid
```
Step04: Modify the /etc/logrotate.d/squid file as follws
```
/var/log/squid/*.log {
    monthly
    rotate 3
    compress
    delaycompress
    notifempty
    missingok
    nocreate
    sharedscripts
    postrotate
      # Asks squid to reopen its logs. (logfile_rotate 0 is set in squid.conf)
      # errors redirected to make it silent if squid is not running
      /usr/sbin/squid -k rotate 2>/dev/null
    endscript
}

```

This process continue all app servers.

### Task is conpleted!
