## Task03 - Install and Configure Tomcat Server

The `Nautilus` application development team recently finished the beta version of one of their Java-based applications,
which they are planning to deploy on one of the app servers in `Stratos DC`. After an internal team meeting, 
they have decided to use the `tomcat` application server. Based on the requirements mentioned below complete the task:


- Install `tomcat` server on `App Server 3`.

- Configure it to run on port `6200`.

- There is a `ROOT.war` file on Jump host at location `/tmp`.

Deploy it on this tomcat server and make sure the webpage works directly on base URL i.e `curl http://stapp03:6200`


---

## Answer:

Step01: Login into app server 03 as root user
```
ssh banner@stapp03
sudo su

```

Step02: Install tomcat server
```
sudo yum install -y tomcat tomcat-webapps tomcat-admin-webapps
```

Step03: Configure Tomcat to Run on Port 6200
```

sudo vi /etc/tomcat/server.xml

Find the default connector (port 8080) --> Change port 8080 → 6200:
```

Step04: Copy ROOT.war from Jump Host to App Server 3
```
scp /tmp/ROOT.war banner@stapp03:/tmp

```

Step05: Deploy the Application (on app server 03)
```
sudo mv /tmp/ROOT.war /var/lib/tomcat/webapps/
```

Step06: Start and enable the tomcat service
```
systemctl start tomcat
systemctl enabe tomcat
```

Step07: Verification
```
curl http://stapp03:3002
```

### Task is Completed!
