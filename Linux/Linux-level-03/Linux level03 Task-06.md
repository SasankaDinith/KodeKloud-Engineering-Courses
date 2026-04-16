## Task06 - Linux Nginx as Reverse Proxy

Nautilus system admin's team is planning to deploy a front end application for their backup utility on Nautilus Backup Server,
so that they can manage the backups of different websites from a graphical user interface. They have shared requirements to set up the same;
please accomplish the tasks as per detail given below:


a. Install `Apache` Server on `Nautilus Backup Server` and configure it to use `3002` port (do not bind it to 127.0.0.1 only, keep it default i.e let Apache listen on server's IP, hostname, localhost, 127.0.0.1 etc).

b. Install `Nginx` webserver on Nautilus Backup Server and configure it to use `8091`.

c. Configure Nginx as a reverse proxy server for Apache.

d. There is a sample index file `/home/thor/index.html` on `Jump Host`, copy that file to Apache's document root.

e. Make sure to start `Apache` and `Nginx` services.

f. You can test final changes using curl command, e.g `curl http://<backup server IP or Hostname>:8091`.

---

## Answer:

Step01: Login to backup server as root user
```
ssh clint@stbkp01

sudo su
```

Step02: Install apache and nginx into backup server
```
yum update -y && yum install -y httpd nginx
```
Step03: Configure the apache port as 3002 and nginx port 8091
```
vi /etc/httpd/conf/httpd.conf
(Update the Listen port value as 3002)

vi /etc/nginx/nginx.conf
(update listen port as 8091)

Added this part below the root value

location / {
      proxy_pass http://stbkp01:8091
}
```

Step04: Move index.html file into apache's root 
```
mv /tmp/index.html /var/www/html
```
Step05: Start Apache and Nginx services
```
systemctl enable --now httpd
systemctl start httpd

systemctl enable --now nginx
systemctl start nginx
```
Step06: Check the connection
```
curl http://stbkp01:8091
```


### Task is Completed!
