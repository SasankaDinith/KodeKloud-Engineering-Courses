Task05 - Create Files on App Servers using Ansible

The Nautilus DevOps team is testing various Ansible modules on servers in `Stratos DC`.
They're currently focusing on file creation on remote hosts using Ansible. Here are the details:

a. Create an inventory file `~/playbook/inventory` on jump host and include all app servers.

b. Create a playbook `~/playbook/playbook.yml` to create a blank file `/tmp/app.txt` on `all app servers`.

c. Set the permissions of the `/tmp/app.txt` file to `0655`.

d. Ensure the user/group owner of the `/tmp/app.txt` file is `tony` on `app server 1`, `steve` on `app server 2` and `banner` on `app server 3`.

Note: Validation will execute the playbook using the command `ansible-playbook -i inventory playbook.yml`, so ensure the playbook functions correctly without any additional arguments.

---

Step01:  Switch to playbook folder
```bash
cd ansible
```
Step02:  Create inventory file and added app servers as managed nodes
```bash
[app_servers]
stapp01 ansible_host=stapp01 ansible_user=tony ansible_password='Ir0nM@n'
stapp02 ansible_host=stapp02 ansible_user=steve ansible_password='Am3ric@'
stapp03 ansible_host=stapp03 ansible_user=banner ansible_password='BigGr33n'
```

Step03: Create playbook.yml file and added below content to it
```bash
---
- name: Create blank file on all app servers
  hosts: all
  become: true
  tasks:
    - name: create blank file
      file:
        path: /tmp/app.txt
        state: touch   
        mode: '0655'
        owner: '{{ansible_user}}'
        group: '{{ansible_user}}'
```

Step04: verify the app servers connection
```bash
ansible -i inventory.ini -m ping all
```
Step05: Run the playbook
```bash
ansible-playbook -i inventory playbook.yml
```     

### Task is Completed!



