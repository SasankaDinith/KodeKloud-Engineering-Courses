## Task05: Write a docker file

The Nautilus application development team shared static website content that needs to be hosted on the `httpd` web server using a containerised platform. The team has shared details with the DevOps team, and we need to set up an environment according to those guidelines. Below are the details:



a. On `App Server 2` in `Stratos DC` create a container named `httpd` using a docker compose file `/opt/docker/docker-compose.yml` (please use the exact name for file).


b. Use `httpd` (preferably `latest` tag) image for container and make sure container is named as `httpd`; you can use any name for service.


c. Map `80` number port of container with port `5000` of docker host.


d. Map container's `/usr/local/apache2/htdocs` volume with `/opt/data` volume of docker host which is already there. (please do not modify any data within these locations).

---

## Answer:

Step01: Login to the App server 01
``` bash
ssh steve@stapp02
```

Step02: Create a docker compose file
``` bash
sudo vi /opt/docker/docker-compose.yml
```

Step03: Added below configurations to it
``` bash

services:
  web:
    image: httpd:latest
    container_name: httpd
    ports:
      - "5000:80"
    volumes:
      - /opt/data:/usr/local/apache2/htdocs:ro
    restart: unless-stopped
```

Step04: Change the directory & Execute the compose file
``` bash
cd /opt/docker

docker compose up
```

Step05: Verify the created images
``` bash
docker image ls
```

You can see the image is created as well.

### Task is Completed!

