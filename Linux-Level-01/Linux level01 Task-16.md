# Task 16 - Firewall Configuration

The Nautilus system admins team has rolled out a web UI application for their backup utility on the Nautilus backup server within the Stratos Datacenter. This application operates on port 5003, and firewalld is active on the server. To meet operational needs, the following requirements have been identified:



- Allow all incoming connections on port `5003/tcp`. Ensure the zone is set to public.

  ---

# Answer :

```bash
# Step01 : Check the active zone (to confirm it's public):
firewall-cmd --get-active-zones

# Step02 : Add the port to the public zone permanently:
sudo firewall-cmd --zone=public --add-port=5003/tcp --permanent

# Step03 : Reload firewalld to apply changes:
sudo firewall-cmd --reload

# Step04 : Verify the port is open in the public zone:
firewall-cmd --zone=public --list-ports



This will ensure that the web UI application running on port 5003 is accessible and compliant with the firewall settings.


```

