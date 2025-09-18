# Task 08 - Data Backup for Developer


Within the Stratos DC, the Nautilus storage server hosts a directory named `/data`, serving as a repository for various developers non-confidential data. Developer kareem has requested a copy of their data stored in `/data/kareem`. The System Admin team has provided the following steps to fulfill this request:



- a. Create a compressed archive named `kareem.tar.gz` of the `/data/kareem` directory.

- b. Transfer the archive to the `/home` directory on the Storage Server.

  ---

  # Answer :

  ```bash

  # Step a: Create a compressed archive of /data/kareem
  tar -czvf kareem.tar.gz /data/kareem

  -c: Create a new archive
  -z: Compress the archive using gzip
  -v: Verbose output (optional, shows progress)
  -f: Specifies the filename of the archive
  
  
  This will create kareem.tar.gz in your current working directory.

  

  # Step b: Transfer the archive to /home on the Storage Server
  mv kareem.tar.gz /home/

  ```
