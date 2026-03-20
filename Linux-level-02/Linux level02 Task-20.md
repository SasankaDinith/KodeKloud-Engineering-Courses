## Task20: Add Response Headers in Apache

We are working on hardening Apache web server on all app servers. As a part of this process we want to add some of the Apache response headers for security purpose. We are testing the settings one by one on all app servers. As per details mentioned below enable these headers for Apache:

  - Install `httpd` package on `App Server 1` using yum and configure it to run on `3001` port, make sure to start its service.

   - Create an `index.html` file under Apache's default document root i.e `/var/www/html` and add below given content in it.

 `Welcome to the xFusionCorp Industries!`

  -  Configure Apache to enable below mentioned headers:

  `X-XSS-Protection` header with value 1; `mode=block`

 `X-Frame-Options` header with value `SAMEORIGIN`

  `X-Content-Type-Options` header with value `nosniff`

`Note:` You can test using curl on the given app server as LBR URL will not work for this task.

---

## Answer: 

Step01: Login to App server 01 as root user
```bash
ssh tony@stapp01

sudo su
```
Step02: Install the httpd package
```bash
yum install -y httpd
```
Step03: Open the /etc/httpd/conf/httpd.conf file and change the Listen value as 3001

Step04: Enable the httpd service
```bash
systemctl enable --now httpd

systemctl status httpd
```
Step05: Create an index.html file under location  /var/www/html and add `Welcome to the xFusionCorp Industries!` to it
```bash
echo "Welcome to the xFusionCorp Industries!" > /var/www/html/index.html
```
Step06: Create a file as /etc/httpd/conf.d/site.conf and added below content to it
```bash
<VirtualHost *:3001>
  ServerName localhost
  DocumentRoot /var/www/html

  Header set X-XSS-Protection "1; mode=block"
  Header set X-Frame-Options "SAMEORIGIN"
  Header set X-Content-Type-Options "nosniff"

</VirtualHost>
            
```
Step07: Reload the httpd service
```bash
systemctl reload httpd
```

Step08: Verify the process
```bash
curl stapp01:3001
```
It shows as "Welcome to the xFusionCorp Industries!" 


### Task is completed!
