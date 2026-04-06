## Task04 - Ansible Unarchive Module

One of the DevOps team members has created a zip archive on `jump host` in `Stratos DC` that needs to be extracted and copied over to all app servers in `Stratos DC`
itself. Because this is a routine task, the Nautilus DevOps team has suggested automating it. We can use Ansible since we have been using it for other automation tasks.
Below you can find more details about the task:

We have an inventory file under `/home/thor/ansible` directory on `jump host`, which should have all the app servers added already.

There is a zip archive `/usr/src/finance/devops.zip` on jump host.

Create a `playbook.yml` under `/home/thor/ansible/` directory on `jump host` itself to perform the below given tasks.

- Unzip `/usr/src/finance/devops.zip` archive in `/opt/finance/` location on all app servers.
- Make sure the extracted data must has the respective sudo user as their `user` and `group` owner, i.e tony for app server 1, steve for app server 2, banner for app server 3.

- The extracted data permissions must be `0777`.

Note: Validation will try to run the playbook using command `ansible-playbook -i inventory playbook.yml` so please make sure playbook works this way, without passing any extra arguments.

---

## Answer: 
Step01: Switch to ansible directory
```bash
cd ansible
```
Step02: Create playbook.yml file under ansible folder and added below content to it
```bash
---
- name: Unzip a file
  hosts: all
  become: yes
  tasks:
    - name: Unzip a file
      unarchive:
        src: /usr/src/finance/devops.zip
        dest: /opt/finance/
        owner: '{{ ansible_user }}'
        group: '{{ ansible_user }}'
        mode: '0777'
```
Step03: Execute the playbook.yml file
```bash
ansible-playbook -i inventory playbook.yml
```

### Task is Completed!
