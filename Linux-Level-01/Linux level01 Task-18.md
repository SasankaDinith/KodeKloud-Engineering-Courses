# Task 18 - SElinux Installation and Configuration

Following a security audit, the xFusionCorp Industries security team has opted to enhance application and server security with SELinux. To initiate testing, the following requirements have been established for App server 2 in the Stratos Datacenter:



- Install the required `SELinux` packages.

- Permanently disable SELinux for the time being; it will be re-enabled after necessary configuration changes. <br/>

- Permanently disable SELinux for the time being; it will be re-enabled after necessary configuration changes. <br/>

- No need to reboot the server, as a scheduled maintenance reboot is already planned for tonight.  <br/>


- Disregard the current status of SELinux via the command line; the final status after the reboot should be disabled. <br/>

---

# Answer : 
``` bash
# Firstly login to  the App server 02
ssh steve@stapp02.stratos.xfusioncorp.com

#  Install SELinux Packages
sudo yum install -y selinux-policy selinux-policy-targeted

# Permanently Disable SELinux
sudo vi /etc/selinux/config

Change the line: SELINUX=enforcing to: SELINUX=disabled

# Ignore Current SELinux Status
getenforce




```


But as per instructions, disregard the current status — the important thing is that SELinux will be disabled after reboot.
