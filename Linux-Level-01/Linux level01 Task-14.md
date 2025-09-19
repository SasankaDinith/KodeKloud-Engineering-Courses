# Task 14 - Default GUI Boot Configuration

With the installation of new tools on the app servers within the Stratos Datacenter, certain functionalities now necessitate graphical user interface (GUI) access. <br/><br/>



- Adjust the default runlevel on all App servers in Stratos Datacenter to enable GUI booting by default. It's imperative not to initiate a server reboot after completing this task.

- ---

# Answer : 
 ```bash

# Step 01 : Check current default target
systemctl get-default

# Step 02 : Set default target to GUI (graphical.target):
sudo systemctl set-default graphical.target

# Step 03 : Verify the process
systemctl get-default

```

✅ Result:
This change ensures that the system will boot into GUI mode by default on the next reboot, but since you're instructed not to reboot, the current session will remain unchanged until the next system start.
