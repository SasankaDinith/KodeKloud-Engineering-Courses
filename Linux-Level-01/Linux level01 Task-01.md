# Task 01: Create a Custom Apache User


In response to heightened security concerns, the xFusionCorp Industries security team has opted for custom Apache users for their web applications. Each user is tailored specifically for an application, enhancing security measures. Your task is to create a custom Apache user according to the outlined specifications: <br/>

a. Create a user named `kirsty` on `App server 2` within the Stratos Datacenter. <br/>  <br/> 
b. Assign a unique UID `1027` and designate the home directory as `/var/www/kirsty`. <br/> <br/> 

Note: You can find the infrastructure details by clicking on the Details of all Users and Servers button on the top-right section of the page.

---


# Answer

In response to heightened security concerns, xFusionCorp Industries requires a dedicated Apache user for each web application.  
This example shows how to create a custom user **kirsty** on **App Server 2** with a specific UID and home directory.

## Task Requirements
- **User name:** `kirsty`  
- **UID:** `1027`  
- **Home directory:** `/var/www/kirsty`  

## Steps / Commands

```bash
# 1. SSH into App Server 2
ssh steve@stapp02.stratos.xfusioncorp.com

# 2. Create the user 'kirsty' with UID 1027 and custom home directory
sudo useradd -u 1027 -d /var/www/kirsty -m kirsty

# 3. (Optional) Set a password for the new user
sudo passwd kirsty

# 4. Verify the user details
id kirsty
getent passwd kirsty
ls -ld /var/www/kirsty
```


## Explanation
- **Assigns UID 1027:** `-u 1027`  
- **Creates the home directory if it doesn’t exist:** `-m`  
- **Set the home directory:** `-d /var/www/kirsty`  
