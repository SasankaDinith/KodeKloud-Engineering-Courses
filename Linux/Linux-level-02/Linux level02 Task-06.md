## Task06: Linux Find Command
During a routine security audit, the team identified an issue on the Nautilus App Server. Some malicious content was identified within the website code. After digging into the issue they found that there might be more infected files. Before doing a cleanup they would like to find all similar files and copy them to a safe location for further investigation. Accomplish the task as per the following requirements:



a. On `App Server 2` at location `/var/www/html/blog` find out all files (not directories) having `.js` extension.


b. Copy all those files along with their `parent directory structure` to location `/blog` on same server.


c. Please make sure not to copy the entire `/var/www/html/blog` directory content.
---

## Answer:

Step01: Login to the app server02
``` bash
ssh steve@stapp02
```
Step02: Switch to root directory
``` bash
cd /
```

Step03: Find out all files having `.js` extension at `/var/www/html/blog` location
``` bash
find /var/www/html/blog -type f -name "*.js"
```
Step04: Copy them with directory structure preserved
```bash
find /var/www/html/blog -type f -name "*.js" -exec cp --parents {} /blog \;
```

### Task is Completed!

