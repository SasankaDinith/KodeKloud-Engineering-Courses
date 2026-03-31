## Task01 - Troubleshoot and Create Ansible Playbook

An Ansible playbook needs completion on the `jump host`, where a team member left off. Below are the details:


- The inventory file `/home/thor/ansible/inventory` requires adjustments. The playbook must run on `App Server 3` in Stratos DC. Update the inventory accordingly.

- Create a playbook `/home/thor/ansible/playbook.yml`. Include a task to create an empty file `/tmp/file.txt` on `App Server 3`.

Note: Validation will run the playbook using the command `ansible-playbook -i inventory playbook.yml`. Ensure the playbook works without any additional arguments.

---

## Answer: 

Step01: Open the inventory file and modify it with correct syntax
```bash
vi /home/thor/ansible/inventory
```
Step02: Create playbook in /home/thor/ansible/playbook.yml location and add below content
```bash
---
- name: Create an empty file on App Server 3
  hosts: appservers
  become: false
  tasks:
    - name: Create /tmp/file.txt
      ansible.builtin.file:
        path: /tmp/file.txt
        state: touch
```
Step03: Run the playbook
```bash
ansible-playbook -i inventory playbook.yml
```

### Task is Completed!
