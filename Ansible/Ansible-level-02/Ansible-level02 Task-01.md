## Task01 - Ansible Ping Module Usage

The Nautilus DevOps team is planning to test several Ansible playbooks on different app servers in `Stratos DC`. Before that, some pre-requisites must be met.
Essentially, the team needs to set up a password-less SSH connection between Ansible controller and Ansible managed nodes.
One of the tickets is assigned to you; please complete the task as per details mentioned below:

a. `Jump host` is our Ansible controller, and we are going to run Ansible playbooks through `thor` user from `jump host`.

b. There is an inventory file `/home/thor/ansible/inventory` on `jump host`. Using that inventory file test `Ansible ping` from `jump host` to `App Server 3`,
make sure ping works.

---

## Answer:

Step01: Switch to ansible directory on jump host
```bash
cd ansible
```
Step02: Open the inventory file in VI editor, and added below content 
```bash
stapp01 ansible_host=stapp01 ansible_user=tony ansible_ssh_pass=Ir0nM@n
stapp02 ansible_host=stapp02 ansible_user=steve ansible_ssh_pass=Am3ric@
stapp03 ansible_host=stapp03 ansible_user=banner ansible_ssh_pass=BigGr33n
```
Step03: Create ssh key on jump host
```bash
ssh-keygen -t rsa -b 4096
```
Step04: Copy thi ssh-key into app server 03
```bash
ssh-copy-id banner@stapp03
```

Step05: Verify the password less access 
```bash
ssh banner@stapp03
```
Step06: Check the ping connectivity 
```bash
ansible -i inventory -m ping stapp03
```

### Task is Completed!
