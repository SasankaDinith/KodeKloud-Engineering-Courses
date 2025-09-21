# Task 03- Service User Creation without Home Directory


In response to the latest tool implementation at xFusionCorp Industries, the system admins require the creation of a service user account. Here are the specifics: <br/><br/>

- Create a user named mariyam in App Server 2 without a home directory. <br/><br/>

  Note: You can find the infrastructure details by clicking on the Details of all Users and Servers button on the top-right section of the page. <br/><br/>
 ---

# Answer : 

To create a user named mariyam on App Server 2 without a home directory, use the following command:

``` bash
# Forst login to the App server 02
ssh steve@stapp02

# Create user as james without a home directory
sudo useradd -M james

# verify user created or not
id james

```

## Explanation:
- `-M` : Prevents the creation of a home directory.
- `useradd` : Adds the user.
- `mariyam`: The username.


