Task02 - 

The Nautilus Application development team wanted to test some applications on app servers in `Stratos Datacenter`.
They shared some pre-requisites with the DevOps team, and packages need to be installed on app servers.
Since we are already using Ansible for automating such tasks, please perform this task using Ansible as per details mentioned below:


  - Create an inventory file `/home/thor/playbook/inventory` on `jump host` and add all app servers in it.

  - Create an Ansible playbook `/home/thor/playbook/playbook.yml` to install `samba package` on all  `app servers` using Ansible `yum` module.

  - Make sure user `thor` should be able to run the playbook on `jump host`.

Note: Validation will try to run playbook using command ansible-playbook -i inventory playbook.yml so please make sure playbook works this way,
without passing any extra arguments.

---

## Answer:

Step01: Switch to playbook folder
```bash
cd playbook
```

Step02: Create an inventory file /home/thor/playbook/inventory on jump host and add all app servers in it.
```bash
vi inventory

stapp01 ansible_host=stapp01 ansible_user=tony ansible_ssh_pass=Ir0nM@n
stapp02 ansible_host=stapp02 ansible_user=steve ansible_ssh_pass=Am3ric@
stapp03 ansible_host=stapp03 ansible_user=banner ansible_ssh_pass=BigGr33n
```

Step03: Create an Ansible playbook /home/thor/playbook/playbook.yml to install samba package on all  app servers using  yum module.
```bash
vi playbook.yml

---
- name: Install samba on app servers
  hosts: app_servers
  become: yes
  tasks:
    - name: Install samba package
      yum:
        name: samba
        state: present
```

Step04: Execute the playbook

```bash
ansible-playbook -i inventory playbook.yml
```

### Task is Completed!
