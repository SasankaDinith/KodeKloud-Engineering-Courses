## Task04 - Copy Data to App Servers using Ansible
The Nautilus DevOps team needs to copy data from the `jump host` to all `application servers` in `Stratos DC` using Ansible. Execute the task with the following details:

a. Create an inventory file `/home/thor/ansible/inventory` on `jump_host` and add all application servers as managed nodes.

b. Create a playbook `/home/thor/ansible/playbook.yml` on the jump host to copy the `/usr/src/data/index.html` file to all application servers, placing it at `/opt/data`.

`Note:` Validation will run the playbook using the command `ansible-playbook -i inventory playbook.yml`.
Ensure the playbook functions properly without any extra arguments.

---

## Answer:

Step01: Switch to ansible folder
```bash
cd ansible
```

Step02: Create inventory file and added app servers as managed nodes
```bash
[app_servers]
stapp01 ansible_host=stapp01 ansible_user=tony ansible_password='Ir0nM@n'
stapp02 ansible_host=stapp02 ansible_user=steve ansible_password='Am3ric@'
stapp03 ansible_host=stapp03 ansible_user=banner ansible_password='BigGr33n'
```

Step03: Create playbook.yml file and added below content to it
```bash
---
- name: Copy the data
  hosts: all
  become: yes

  tasks:
   - name: "copying files"
     ansible.builtin.copy:
       src: /usr/src/devops/index.html
       dest: /opt/devops
```

Step04: verify the app servers connection 
```
ansible -i inventory.ini -m ping all
```

Step05: Run the playbook
```bash
ansible-playbook -i inventory playbook.yml
```

### Task is Completed!
