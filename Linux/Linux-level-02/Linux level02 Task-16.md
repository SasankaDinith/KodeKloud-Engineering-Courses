## Task16: Install and Configure HaProxy LBR
There is a static website running in `Stratos Datacenter`. They have already configured the app servers and code is already deployed there. To make it work properly, they need to configure `LBR` server. There are number of options for that, but team has decided to go with `HAproxy`. FYI, apache is running on port `3004` on all app servers. Complete this task as per below details.


- Install and configure `HAproxy` on `LBR` server using `yum` only and make sure all app servers are added to `HAproxy` load balancer. `HAproxy` must serve on default `http` port (Note: Please do not remove `stats socket /var/lib/haproxy/stats` entry from `haproxy` default config.).

- Once done, you can access the website using `curl http://localhost:80` on the `LBR` server.

---
## Answer:

Step01: Login LBR server as root
```bash
ssh loki@stlb01

sudu su ~
```

Step02: Install the Haproxy package
```bash
yum install haproxy -y
```
Step03: Move to /etc/haproxy folder and open haproxy.cfg file and modify frontend port as 80
```bash

cd /etc/haproxy

vi haproxy.cfg
```

Step04: Login App server 01,02,03 get port numbers and server's IP addresses

Step05: We need to modify haproxy.cfg file content as follows,
```bash
backend app
   balance      roundrobin
   server   stapp01 <App server 01 IP>:<port> check
   server   stapp01 <App server 02 IP>:<port> check
   server   stapp01 <App server 03 IP>:<port> check
#   server   stapp01 <App server 01 IP>:<port> check
```
Step06: save the configurations and exit that file, then enable and start haproxy service
```bash
systemctl enable haproxy

systemctl start haproxy
```

Step07: Verify the process 
```bash
curl http://localhost:80

you can see content as "Welcome to xfusioncrop Industries" as well
```

### Task is Completed!
