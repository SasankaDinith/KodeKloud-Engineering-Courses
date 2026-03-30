## Task13: Linux Firewalld Setup

To secure our `Nautilus` infrastructure in `Stratos Datacenter` we have decided to install and configure `firewalld` on all `app servers`. We have Apache and Nginx services running on these apps. Nginx is running as a reverse proxy server for Apache. We might have more robust firewall settings in the future, but for now we have decided to go with the given requirements listed below:


a. Allow all incoming connections on Nginx port, i.e `80`.

b. Block all incoming connections on Apache port, i.e `8080`.

c. All rules must be permanent.

d. Zone should be public.

e. If Apache or Nginx services aren't running already, please make sure to start them.


---

## Answer:
Step01: login app server 01 as root
```bash
ssh tony@stapp01

sudo su
```
Step02: Install firewalld package
```bash
sudo yum install -y firewalld
```

Step03: Start ena enable the firewalld
```bash
sudo systemctl enable firewalld

sudo systemctl start firewalld

sudo systemctl status firewalld
```
Step04:  Allow all incoming connections on Nginx port, i.e 80.
```
sudo firewall-cmd --permanent --add-port=80/tcp
```
Step05:  Block all incoming connections on Apache port, i.e 8080.
```bash
sudo firewall-cmd --permanent --remove-port=8000/tcp
```
Step06: Verify the active rules in the public zone
```bash
firewall-cmd --get-default-zone
```
Step07: Start and enable the httpd 
```bash
systemctl start httpd

systemctl enable httpd

systemctl status httpd
```
Step08: Check nginx status
```bash
systemctl status httpd
```

This entire process done all app servers as well.

### Task is Completed!


