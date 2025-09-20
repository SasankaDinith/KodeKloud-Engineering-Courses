# Task 17 - Process Limit Adjustment


In the Stratos Datacenter, our Storage server is encountering performance degradation due to excessive processes held by the nfsuser user. To mitigate this issue, we need to enforce limitations on its maximum processes. Please set the maximum process limits as specified below:



a. Set the soft limit to 1026


b. Set the hard limit to 2026

---

# Answer :

``` bash
# 1. Open the limits configuration file
sudo nano /etc/security/limits.conf

# 2. Add the following lines at the end of the file
nfsuser    soft    nproc    1026
nfsuser    hard    nproc    2026

These lines set:

- Soft limit: 1026 processes
- Hard limit: 2026 processes


 ## Optional: Apply changes immediately
These limits apply on new sessions. To enforce them immediately, you can:

- Log out and back in as nfsuser
- Or restart services that run under nfsuser
```

