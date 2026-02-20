## Task24: Application Security

We have a backup management application UI hosted on `Nautilus's` backup server in `Stratos DC`.
That backup management application code is deployed under Apache on the backup server itself, and Nginx is running as a reverse proxy on the same server.
Apache and Nginx ports are `8088` and `8099`, respectively. We have iptables firewall installed on this server.
Make the appropriate changes to fulfill the requirements mentioned below:


We want to open all incoming connections to Nginx's port and block all incoming connections to Apache's port. Also make sure rules are permanent.

---
## Answer:

Step01: Login to backup server as root
```bash
ssh clint@stbkp01

sudo su
```

Step02: Enable to iptables
```bash
sudo systemctl enable --now iptables
```

Step03: Verify the status
```bash
sudo systemctl status iptables
```
Step04: Setup allow and block ports
```bash
iptables -A INPUT -p tcp --dport 8099 -j ACCEPT

iptables -A INPUT -p tcp --dport 3003 -j DROP
```
Step05: Verify the iptables rules
```bash
iptables -L
```
### Task is Completed!
