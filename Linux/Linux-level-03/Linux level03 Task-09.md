## Task09 - PAM Authentication For Apache

We have a requirement where we want to password protect a directory in the Apache web server document root. We want to password protect `http://<website-url>:<apache_port>/protected/` URL as per the following requirements (you can use any `website-url` for it like `localhost` since there are no such specific requirements as of now). Setup the same on App server 3 as per below mentioned requirements:


a. We want to use basic authentication.

b. We do not want to use `htpasswd` file based authentication. Instead, we want to use `PAM` authentication, i.e `Basic Auth + PAM` so that we can authenticate with a Linux user.

c. We already have a user `siva` with password `ksH85UJjhb` which you need to provide access to.

d. You can test the same using a curl command from jump host `curl http://<website-url>:<apache_port>/protected/`.

---

## Answer:
Step01: Login app server 03 as root
```
```
