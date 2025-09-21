# Task 13 - Restrict Cron Access

In alignment with security compliance standards, the Nautilus project team has opted to impose restrictions on crontab access. Specifically, only designated users will be permitted to create or update cron jobs.



Configure crontab access on `App Server 2` as follows: 

- Allow crontab access to `ammar` user while denying access to the `jerome` user.




---

# Answer : 

``` bash
# Step 01 - Login to the App server 02
ssh steve@stapp02

# Step 02 - Create or edit /etc/cron.allow
vi /etc/cron.allow (press enter)

then type allowing user name then press esc, then type :wq to exit vi editor.

# Step 02 - Create or edit /etc/cron.deny
vi /etc/cron.deny

then type denying user name then press esc, then type :wq to exit vi editor.

# Step 03 - Verify the process (optional)

cat /etc/cron.allow 
cat /etc/cron.deny 


```


