# Task 03- Linux User Setup with Non-Interactive Shell


Create a user named javed with a non-interactive shell on App Server 3.


---
# Answer : 

To create a user named javed with a non-interactive shell on App Server 3, you can use the following command on that server:

## Steps & Commands

Run the following commands on **each App server**:

```bash
# login to App server 03
ssh banner@stapp03

# Create a user wuth non-interactive shell
sudo useradd -s /sbin/nologin javed 
```
## Explanation:

- `sudo` : Runs the command with administrative privileges.
- `useradd` : Creates a new user.
 - `-s /sbin/nologin` : Sets the shell to a non-interactive shell, preventing the user from logging in interactively.




