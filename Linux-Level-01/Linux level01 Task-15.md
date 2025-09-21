# Task 15 - Timezone Alignment
In the daily standup, it was noted that the timezone settings across the Nautilus Application Servers in the Stratos Datacenter are 
inconsistent with the local datacenter's timezone, currently set to Australia/Perth.

<br/> 

- Synchronize the timezone settings to match the local datacenter's timezone `(Australia/Perth)`.

---

# Answer : 
``` bash
# Step 01 - Login to App server 01
ssh tony@stapp01

# Step 02 - Check current timezone:
timedatectl

# Step 03 - Set timezone to Australia/Perth:
sudo timedatectl set-timezone Australia/Perth

# Step 04 : Verify the change:
timedatectl

You should see:
Time zone: Australia/Perth (AWST, +0800)



```
