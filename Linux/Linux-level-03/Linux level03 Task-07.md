## Task07 - Configure protected directories in Apache

`xFusionCorp Industries` has hosted several static websites on `Nautilus Application Servers` in `Stratos DC`.
There are some confidential directories in the document root that need to be password protected. 
Since they are using `Apache` for hosting the websites, the production support team has decided to use `.htaccess` with basic `auth`.
There is a website that needs to be uploaded to `/var/www/html/dba` on `Nautilus App Server 3`. However, we need to set up the authentication before that.

- Create `/var/www/html/dba` directory if doesn't exist.

- Add a user `ammar` in `htpasswd` and set its password to `8FmzjvFU6S`.

- There is a file `/tmp/index.html` present on `Jump Server`. Copy the same to the directory you created,
  please make sure default document root should remain `/var/www/html`. Also website should work on URL `http://<app-server-hostname>:80/dba/`
  
---

## Answer:

Step01: Copy the /tmp/index.html file into stapp02's /tmp location
```
scp /tmp/index.html banner@stapp03:/tmp
```

Step02: Login app server 03 as root
```
ssh banner@stapp03

sudo su
```

Step03: Create new folder as /var/www/html/dba
```
sudo mkdir /var/www/html/dba
```


Step04: Move /tmp/index.html file into that newly created folder
```
sudo mv /tmp/index.html /var/www/html/dba
```
Step05: Create new user as ammar
```
useradd ammar
```
Step06: Set that user as htaccess
```
htpasswd -c /var/www/html/.htaccess ammar
```
Step07: Start and enable the httpd service
```
systemctl start httpd
systemctl enable --now httpd 
```
Step08: Check the connection
```
curl http://stapp03:80/dba/
```

### Task is Completed!
