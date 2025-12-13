# Task 05: Troubleshoot Docker Container Issue

An issue has arisen with a static website running in a container named nautilus on `App Server 1`<br/> <br/>
To resolve the issue, investigate the following details: <br/>
- Check if the container’s volume `/usr/local/apache2/htdocs` is correctly mapped with the host’s volume `/var/www/html`<br/>
- Verify that the website is accessible on host port `8080` on `App Server 1`. <br/>
- Confirm that the command `curl http://localhost:8080/` works on `App Server 1`

---

## Answer: 

Step 01: SSH into App Server 1
``` bash
ssh banner@stapp01
```
Step02:  Verify the container is running
``` bash
docker ps | grep nautilus
```
Step03 : Mapped the container volume into host volume
``` bash
docker run -d --name nautilus -p 8080:80 -v /var/www/html:/usr/local/apache2/htdocs httpd:latest
```

Step04: Test website
``` bash
curl http://localhost:8080/
```

## Task is complete !
