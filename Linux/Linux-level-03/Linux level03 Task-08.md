## Task08 - Linux Process Troubleshooting

The production support team of xFusionCorp Industries has deployed some of the latest monitoring tools to keep an eye on every service, application, etc. running on the systems. One of the monitoring systems reported about Apache service unavailability on one of the app servers in `Stratos DC`.


Identify the faulty app host and fix the issue. Make sure Apache service is up and running on all app hosts. They might not have hosted any code yet on these servers, so you don't need to worry if Apache isn't serving any pages. Just make sure the service is up and running. Also, make sure Apache is running on port `5004` on all app servers.

---

## Answer:

Step01: Login to app server 01 as root
```
ssh tony@stapp01

sudo -i
```
Step02: Check the httpd service status
```
systemctl ststus httpd
```
Step03: Find the process of which 5004 port assign
```
ss -tunap | grep 5004
```
Step04: Kill the process by PID
```
kill -9 <PID>
```
Step05: Restart and enable the httpd service
```
systemctl restart httpd
systemctl enable --now httpd
```
Step06: Check the connection
```
curl -Ik http://stapp01:5004
```

### Task is Completed!
