# Task 05 - Temporary User Setup with Expiry

As part of the temporary assignment to the Nautilus project, a developer named javed requires access for a limited duration. To ensure smooth access management, a temporary user account with an expiry date is needed. Here's what you need to do:<br/><br/>

- Create a user named javed on App Server 3 in Stratos Datacenter. Set the expiry date to 2024-03-28, ensuring the user is created in lowercase as per standard protocol.<br/><br/>

Note: You can find the infrastructure details by clicking on the Details of all Users and Servers button on the top-right section of the page.<br/><br/>

---

## Answer : 

To create a temporary user account named javed on App Server 3 in the Stratos Datacenter with an expiry date of 2024-03-28, use the following command:

``` bash
# First login to App server 03
ssh banner@stapp03

# Create a user james with expiry date as 2024-03-28
sudo useradd -e 2024-03-28 javed

# verify that user created or not
chage -l james 

```

## Explanation:
- `useradd` : Command to create a new user.
- `-e 2024-03-28` : Sets the account expiry date to March 28, 2024.
- `javed` : Username (in lowercase, as per protocol).

