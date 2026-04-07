## Task05 - Ansible Replace Module

There is some data on all app servers in `Stratos DC`. The Nautilus development team shared some requirement with the DevOps
team to alter some of the data as per recent changes they made. The DevOps team is working to prepare an Ansible playbook to accomplish the same.
Below you can find more details about the task.

Write a `playbook.yml` under `/home/thor/ansible` on `jump host`, an `inventory` is already present under `/home/thor/ansible` directory on `Jump host`
itself. Perform below given tasks using this playbook:

 -   We have a file `/opt/data/blog.txt` on `app server 1`. Using Ansible `replace` module replace string `xFusionCorp` to `Nautilus` in that file.

 -   We have a file `/opt/data/story.txt` on `app server 2`. Using Ansible `replace` module replace the string `Nautilus` to `KodeKloud` in that file.

 -   We have a file `/opt/data/media.txt` on `app server 3`. Using Ansible `replace` module replace string `KodeKloud` to `xFusionCorp Industries` in that file.

`Note:` Validation will try to run the playbook using command `ansible-playbook -i inventory playbook.yml`
so please make sure the playbook works this way without passing any extra arguments.


---

## Answer:
Step01: Switch to ansible directory
```
cd ansible
```
Step02: Create playbook.yml file and added below content to it
```
---
- name: Replace string in blog.txt on app server 1
  hosts: app_server1
  become: yes
  tasks:
    - name: Replace xFusionCorp with Nautilus
      replace:
        path: /opt/data/blog.txt
        regexp: 'xFusionCorp'
        replace: 'Nautilus'

- name: Replace string in story.txt on app server 2
  hosts: app_server2
  become: yes
  tasks:
    - name: Replace Nautilus with KodeKloud
      replace:
        path: /opt/data/story.txt
        regexp: 'Nautilus'
        replace: 'KodeKloud'

- name: Replace string in media.txt on app server 3
  hosts: app_server3
  become: yes
  tasks:
    - name: Replace KodeKloud with xFusionCorp Industries
      replace:
        path: /opt/data/media.txt
        regexp: 'KodeKloud'
        replace: 'xFusionCorp Industries'

```

Step03: Run the playbook.yml file
```
ansible-playbook -i inventory playbook.yml
```

### Task is Completed!

