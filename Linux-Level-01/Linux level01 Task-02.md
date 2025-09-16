# Task 02- Group Creation and User Assignment

The system admin team at xFusionCorp Industries has streamlined access management by implementing group-based access control. Here's what you need to do: <br/><br/>

1. **Create a group** named `nautilus_sftp_users` across **all App servers** within the Stratos Datacenter.  <br/><br/>
2. **Add the user** `sonya` into the `nautilus_sftp_users` group on all App servers.If the user does not exist, create it first.<br/><br/>

Note: You can find the infrastructure details by clicking on the Details of all Users and Servers button on the top-right section of the page.<br/><br/>

---
# Answer : 

In this task you need to log all app servers and do this whole process each one by one. 

## Steps & Commands

Run the following commands on **each App server**:

```bash
# 1️⃣ Create the group (if it doesn’t already exist)
sudo groupadd -f nautilus_sftp_users

# 2️⃣ Create the user 'sonya' if it does not exist
  sudo useradd -m -s /bin/bash sonya

# 3️⃣ Add 'sonya' to the group
sudo usermod -aG nautilus_sftp_users sonya

# 4️⃣ Verify membership
id sonya

```

This process repeat all app servers.

## Verification : 
After executing the above commands on each App server:

```bash
grep nautilus_sftp_users /etc/group
is sonya
```
You should see `nautilus_sftp_users` listed and `sonya` as a member.


