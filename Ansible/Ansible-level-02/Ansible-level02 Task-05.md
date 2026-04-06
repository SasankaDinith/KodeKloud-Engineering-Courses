## Task05 - Ansible Blockinfile Module

The Nautilus DevOps team wants to install and set up a simple `httpd` web server on all app servers in `Stratos DC`. Additionally,
they want to deploy a sample web page for now using Ansible only. Therefore, write the required playbook to complete this task. Find more details about the task below.


We already have an inventory file under `/home/thor/ansible` directory on `jump host`. Create a `playbook.yml` under `/home/thor/ansible` directory on `jump host` itself.

 - Using the playbook, install `httpd` web server on all app servers. Additionally, make sure its service should up and running.

- Using `blockinfile` Ansible module add some content in `/var/www/html/index.html` file. Below is the content:

   ```
   Welcome to XfusionCorp!

   This is  Nautilus sample file, created using Ansible!

   Please do not modify this file manually!
   ```

 - The `/var/www/html/index.html` file's user and group `owner` should be `apache` on all app servers.

 - The `/var/www/html/index.html` file's permissions should be `0655` on all app servers.

Note:

i. Validation will try to run the playbook using command `ansible-playbook -i inventory playbook.yml` so please make sure the playbook works this way without passing any extra arguments.

ii. Do not use any custom or empty `marker` for `blockinfile` module.

---

## Answer: 

Step01: Switch to ansible folder
```bash
cd ansible
```

Step02: Create playbook.yml file and added below content to it
```bash
---
- name: Install httpd webs server on all app servers
  hosts: all
  become: yes
  tasks:
    - name: install httpd 
      yum:
        name: httpd
        state: present

    - name: httpd running and up
      service:
        name: httpd
        state: started

    - name: create index.html file on all app servers and modify details
      file:
        path: /var/www/html/index.html
        state: touch
        owner: apache
        group: apache

    - name: Modify index.html file permissions
      file:
        path: /var/www/html/index.html
        mode: '0655'

    - name: adding content to index.html file
      blockinfile:
        path: /var/www/html/index.html
        block: |
          Welcome to XfusionCorp!
          This is  Nautilus sample file, created using Ansible!
          Please do not modify this file manually!
        create: true
          
```

Step03: Execute the playbook.yml file
```bash
ansible-playbook -i inventory playbook.yml
```

Step04: Verify the tasks in each app server
```bash
systemctl status httpd

cat /var/www/html/index.html

ls -al /var/www/html/index.html
```

### Task is Completed!
