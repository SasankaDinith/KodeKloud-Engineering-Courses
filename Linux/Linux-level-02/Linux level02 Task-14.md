## Task14: Linux Postfix Mail Server

`xFusionCorp Industries` has planned to set up a common email server in `Stork DC`. After several meetings and recommendations they have decided to use `postfix` as their mail transfer agent and `dovecot` as an `IMAP/POP3` server. We would like you to perform the following steps:


1. Install and configure `postfix` on `Stork DC` mail server.

2. Create an email account `yousuf@stratos.xfusioncorp.com` identified by `B4zNgHA7Ya`.

3. Set its mail directory to `/home/yousuf/Maildir`.

4. Install and configure `dovecot` on the same server.

---

## Answer:

Step01: Login to mail server as root user
```
ssh groot@stmail01
sudo su
```
Step02: Update the system and install postfix package
```
yum update -y && yum install dovecot postfix -y
```

Step03: Modifiy the main.cf file content as follows
```
vi /etc/postfix/main.cf

Find the first myhostname line,  first remove the comment that and replace "mail.stratos.xfusioncorp.com " into it's value

Remove 3rd myhostname line and  replace "stratos.xfusioncorp.com " into it's value

Find the 2nd myorigin line, then uncomment that

Find the first inet_interface line and uncomment that, and add comment 4th inet_interface line

Find the mydestination line and added at the end of first destination line as $mydomain

Find home_mailbox line and uncomment it's 2nd line

Exit the vi editor
```

Step04: Enable the postfix service
```
systemctl enable --now postfix

systemctl status postfix
```

Step05: Open the /etc/   file and modify that file as below
```

Find disable_plaintext line and uncomment it, and  change value as no

Find auth_mechanism line and add that line value at the end as login

Exit the vi editor
```

Step06: 
```
Find the mail_location line with empty value line, then add this "maildir:~/Maildir" as it's value.
```

 
### Task is Completed!

