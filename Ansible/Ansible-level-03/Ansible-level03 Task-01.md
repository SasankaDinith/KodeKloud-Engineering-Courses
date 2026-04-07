## Task01 - Creating Soft Links Using Ansible






---

## Answer:

Step01: Switch to ansible directory
```
cd ansible
```
Step02: Create playbook.yml file and added below content to it
```
---
- name: Create empty file on app server01
  hosts: stapp01
  become: yes
  tasks:
    - name: create empty file
      file:
        path: /opt/data/blog.txt
        owner: tony
        group: tony
        state: touch
    - name: Create symbolic link
      file:
        src: /opt/data
        dest: /var/www/html
        state: link

- name: Create empty file and symbolic link on app server 02
  hosts: stapp02
  become: yes
  tasks:
    - name: create empty file
      file:
        path: /opt/data/story.txt
        owner: steve
        group: steve
        state: touch
    - name: Create symbolic link
      file:
        src: /opt/data
        dest: /var/www/html
        state: link

- name: Create empty file and symbolic link on app server 03
  hosts: stapp03
  become: yes
  tasks:
    - name: create empty file
      file:
        path: /opt/data/media.txt
        owner: banner
        group: banner
        state: touch
    - name: Create symbolic link
      file:
        src: /opt/data
        dest: /var/www/html
        state: link

```
Step03: Run the playbook.yml file
```
ansible-playbook -i inventory playbook.yml
```

### Task is Completed!
