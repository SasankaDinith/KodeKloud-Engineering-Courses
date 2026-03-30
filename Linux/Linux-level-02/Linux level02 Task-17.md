## Task17: Haproxy LBR Troubleshooting

`xFusionCorp Industries` has an application running on Nautlitus infrastructure in `Stratos Datacenter`. The monitoring tool recognised that there is an issue with the `haproxy` service on the `LBR` server. That needs to fixed to make the application work properly.


Troubleshoot and fix the issue, and make sure `haproxy` service is running on the `Nautilus LBR` server. Once fixed, make sure you are able to access the website by running the command `curl http://stlb01:80/` in the terminal.

---

## Answer:

Step01: Login to LBR server as root
```bash
ssh loki@stlb01

sudo -i
```
Step02: Check the haproxy status 
```bash
systemctl status haproxy
```

Step03: Open the /etc/haproxy/haproxy.cfg file 
```bash
vi /etc/haproxy/haproxy.cfg
```
Step04: Modify some parts of this file

Change round -> roundrobin

Then save and exit the file

Step05: Restart and enable the haproxy service
```bash
systemctl restart haproxy

systemctl enable haproxy
```

Step06: Verify the website is runnig
```bash
curl http://stlb01:80/
```

### Task is completed!
