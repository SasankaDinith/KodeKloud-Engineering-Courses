# Task 06 - Linux User Data Transfer

Due to an accidental data mix-up, user data was unintentionally mingled on Nautilus `App Server 3` at the `/home/usersdata` location by the Nautilus production support team in Stratos DC. To rectify this, specific user data needs to be filtered and relocated. Here are the details:



Locate all files (excluding directories) owned by user siva within the `/home/usersdata` directory on `App Server 3`. Copy these files while preserving the directory structure to the `/news` directory. <br/>

--- 
# Answer :
``` bash
# To accomplish the task of locating and copying all files (excluding directories) owned by user siva from /home/usersdata to /news on Nautilus App Server 3, while preserving the directory structure, you can use the following Linux command:

find /home/usersdata -type f -user siva -exec cp --parents {} /news \;

```
Explanation:
- find /home/usersdata: Starts searching from the specified directory.
- -type f: Ensures only files are selected (not directories).
- -user siva: Filters files owned by the user siva.
- -exec cp --parents {} /news \;: Copies each file to /news, preserving the directory structure relative to /home/usersdata.
