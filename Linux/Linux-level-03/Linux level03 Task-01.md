## Task01 - Apache Redirects

The Nautilus devops team got some requirements related to some Apache config changes.
They need to setup some redirects for some URLs. There might be some more changes need to be done. Below you can find more details regarding that:


1.) `httpd` is already installed on `app server 2`. Configure Apache to listen on port `3000`.

2.) Configure Apache to add some redirects as mentioned below:

  - Redirect `http://stapp02.stratos.xfusioncorp.com:<Port>/` to `http://www.stapp02.stratos.xfusioncorp.com:<Port>/` i.e `non www` to `www`.
    This must be a permanent redirect i.e `301`

- Redirect `http://www.stapp02.stratos.xfusioncorp.com:<Port>/blog/` to `http://www.stapp02.stratos.xfusioncorp.com:<Port>/news/`.
  This must be a temporary redirect i.e `302`.


---

## Answer:
Step01: Login into app server 02 as root user
```
ssh steve@stapp02

sudo -i
```

Step02: Configure apache to listen on port 3000 
```
vi /etc/httpd/conf/httpd.conf

(Find a line with port number, then change it to 3000)
```

Step03: Configure Apache to add some redirects
```
Open the file as : vi /etc/httpd/conf.f/main.conf

(Added below redirects into main.conf file)

<VirtualHost *:3000>
ServerName stapp02.stratos.xfusioncorp.com:3000/
Redirect 301 / http://www.stapp02.stratos.xfusioncorp.com:3000/
</VirtualHost>

<VirtualHost *:3000>
ServerName http://www.stapp02.stratos.xfusioncorp.com:3000/blog/
Redirect 302 / http://www.stapp02.stratos.xfusioncorp.com:3000/news/
</VirtualHost>

```

Step04 :Restart the httpd service
```
systemctl restart httpd
```

### Task is Completed!
