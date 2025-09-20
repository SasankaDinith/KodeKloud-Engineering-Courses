# Task 07 - Secure Root SSH Access


Following security audits, the xFusionCorp Industries security team has rolled out new protocols, including the restriction of direct root SSH login.



- Your task is to disable direct SSH root login on all app servers within the Stratos Datacenter.

---

# Answer : 

``` bash
#Step 01 : Login to each App servers,
ssh user@hostname

#Step 02 : Edit the SSH configuration file
sudo vi /etc/ssh/sshd_config

# Step 03 :

Locate the line:
**PermitRootLogin yes**

and change it to:
**PermitRootLogin no**

#Step 04 : Save and exit the file (:wq in vi)

# Step 05 : Restart the SSH service to apply changes:
sudo systemctl restart sshd

And also ypu can check the status od SSH service
sudo systemctl status sshd
```

🔒 Verification:
To confirm root login is disabled: ssh root@server-ip

You should see a "Permission denied" message.



