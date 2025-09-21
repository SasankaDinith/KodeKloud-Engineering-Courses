# Task 10 - File Permission Correction


After conducting a security audit within the Stratos DC, the Nautilus security team discovered misconfigured permissions on critical files.
To address this, corrective actions are being taken by the production support team. Specifically, the file named `/etc/hostname` 
on Nautilus `App 2 server` requires adjustments to its Access Control Lists (ACLs) as follows: <br/> <br/>


- 1. The file's user owner and group owner should be set to root. <br/> <br/>

- 2. `Others` should possess `read only` permissions on the file. <br/> <br/>

- 3. User `anita` must not have any permissions on the file. <br/> <br/>

- 4. User `rod` should be granted `read only` permission on the file. <br/> <br/>

---

# Answer : 

``` bash
# Step 01 - login to the App server 02
ssh steve@stapp01

# Step 02 - Set user and group owner to root:
sudo chown root:root /etc/hostname

# Step 03 - Set permissions so "others" have read-only access:
sudo chmod o=r /etc/hostname

# Step 04 - Remove all permissions for user anita:
sudo setfacl -m u:anita:--- /etc/hostname

# Step 05 - Grant read-only permission to user rod:
sudo setfacl -m u:rod:r-- /etc/hostname

# Step 06 - (Optional) Verify the ACLs:
sudo getfacl /etc/hostname

Sample expected output:

file: /etc/hostname
owner: root
group: root
user:anita:---
user:rod:r--
group::---
mask::r--
other::r--

```

