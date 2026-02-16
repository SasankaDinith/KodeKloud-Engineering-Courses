## Task01: Create a Cron Job

The `Nautilus` system admins team has prepared scripts to automate several day-to-day tasks. They want them to be deployed on all app servers in `Strator DC` on a set schdule. Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below:

- Install `cronie` package on all `Nautilus` app servers and start `crond` service
- Add a cron `*/5 * * * * echo hello > /tmp/cron_text` for `root` user

---

## Answer:

Step01: Login to app server01 as root
``` bash
ssh tony@stapp01

sudo su
```

Step02: Install the cronie package 
``` bash
sudo yum install cronie -y
```

Step03: Start and enable the service
```bash
sudo systemctl start crond

sudo systemctl enable crond
```
Step04: Create new crontab and add cron to it

```bash
crontab -e 
```
Add this cron: `*/5 * * * * echo hello > /tmp/cron_text`

type `:wq` and press enter to exit editor

Step05: Verify the cron added 
```bash
crontab -l
```

Continue this process across all app servers ( App server02, App server03)

### Task is Completed!

