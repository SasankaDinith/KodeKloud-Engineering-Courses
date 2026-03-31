## Task02 - Create Ansible Inventory for App Server Testing

The Nautilus DevOps team is testing Ansible playbooks on various servers within their stack. They've placed some playbooks under `/home/thor/playbook/`
directory on the `jump host` and now intend to test them on `app server 1` in Stratos DC.
However, an inventory file needs creation for Ansible to connect to the respective app. Here are the requirements:

a. Create an ini type Ansible inventory file `/home/thor/playbook/inventory` on `jump host`.

b. Include `App Server 1` in this inventory along with necessary variables for proper functionality.

c. Ensure the inventory hostname corresponds to the `server name` as per the wiki, for example `stapp01` for `app server 1` in `tratos DC`.

`Note:` Validation will execute the playbook using the command `ansible-playbook -i inventory playbook.yml`.
Ensure the playbook functions properly without any extra arguments.

---

## Answer: 

Step01: Create inventory file under the /home/thor/playbook/inventory location and added below content 
```bash
stapp01 ansible_user=tony ansible_ssh_pass=Ir0nM@n ansible_ssh_common_args='-o StrictHostKeyChecking=no'

```
Step02: Run the playbook
```bash
ansible-playbook -i inventory playbook.yml
```
Step03: Verify the httpd installtion with login app server 01
```bash

ssh tony@stapp01

sudo systemctl status httpd
```

### Task is Completed!


