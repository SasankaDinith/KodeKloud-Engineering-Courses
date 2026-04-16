## Task04 - Linux Network Services

Our monitoring tool has reported an issue in `Stratos Datacenter`. One of our app servers has an issue, as its Apache service is not 
reachable on port `6200` (which is the Apache port). The service itself could be down, the firewall could be at fault, or something else could be causing the issue.


Use tools like `telnet`, `netstat`, etc. to find and fix the issue. Also make sure Apache is reachable from the jump host without compromising any security settings.

Once fixed, you can test the same using command `curl http://stapp01:6200` command from jump host.

`Note:` Please do not try to alter the existing `index.html` code, as it will lead to task failure.

---

## Answer:

Step01: Login into app server 01 as root
```
ssh tony@stapp01

sudo -i
```
Step02: Check the httpd service status (you can see httpd is disable)
```
systemctl status httpd
```
Step03: Check weather any program used port 6200 and show which process ownes it
```
netstat -tunap | grep 6200
```
Step04: Kill the process that found by previous step
```
kill -9 <pid>
```
Step05: Enable the httpd service
```
systemctl enable --now httpd
```
Step06: Add new Iptable rule as follows
```
iptables -I INPUT 1 -p tcp --dport 6200 -j ACCEPT
```

Step07: Check the iptables rules
```
iptables -L
```

Step08: Save iptable rules
```
service iptabels save
```
Step09: Check the connectivity
```
curl http://stapp01:6200
```

### Task is Completed!
