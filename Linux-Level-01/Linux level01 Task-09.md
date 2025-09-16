# Task 09 - Script Execution Permissions

In a bid to automate backup processes, the xFusionCorp Industries sysadmin team has developed a new bash script named xfusioncorp.sh. While the script has been distributed to all necessary servers, it lacks executable permissions on App Server 3 within the Stratos Datacenter.<br/><br/>

- Your task is to grant executable permissions to the /tmp/xfusioncorp.sh script on App Server 3. Additionally, ensure that all users have the capability to execute it.<br/><br/>

---

## Answer : 

To grant executable permissions to the /tmp/xfusioncorp.sh script on App Server 3, and ensure all users can execute it, run the following command:

``` bash
# Login to App server 3
ssh banner@stapp03

# To grant executable permissions to the /tmp/xfusioncorp.sh script
sudo chmod +x /tmp/xfusioncorp.sh
sudo chmod a+x /tmp/xfusioncorp.sh

# Verify the permissions with
ls -l /tmp/xfusioncorp.sh

# It should show something like:
-rwxr-xr-x 1 root root ... /tmp/xfusioncorp.sh


```

## Explanation:
- `chmod +x` : Adds execute permission for the file owner.
- `chmod a+x` : Ensures all users (owner, group, others) have execute permission.
