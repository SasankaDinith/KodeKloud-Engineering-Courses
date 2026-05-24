## Task29 - Delete Backup from S3 Using Terraform

The Nautilus DevOps team is currently engaged in a cleanup process, focusing on removing unnecessary data and services from their AWS account. 
As part of the migration process, several resources were created for one-time use only, necessitating a cleanup effort to optimize their AWS environment.

A S3 bucket named `devops-bck-16620` already exists.

1) Copy the contents of `devops-bck-16620` S3 bucket to `/opt/s3-backup/` directory on `terraform-client` host (the landing host once you load this lab).

2) Delete the S3 bucket `devops-bck-16620`.

3) Use the AWS CLI through Terraform to accomplish this task—for example, by running AWS CLI commands within Terraform. The Terraform working directory is `/home/bob/terraform`.
   Update the `main.tf` file (do not create a separate `.tf` file) to accomplish this task.

`Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01: Update the main.tf file such as follows
```

resource "null_resource" "s3_backup_and_cleanup" {

  # Step 1: Copy S3 bucket contents to local directory
  provisioner "local-exec" {
    command = <<EOT
      mkdir -p /opt/s3-backup &&
      aws s3 sync s3://datacenter-bck-22925 /opt/s3-backup/
    EOT
  }

  # Step 2: Delete all objects inside the bucket
  provisioner "local-exec" {
    command = "aws s3 rm s3://datacenter-bck-22925 --recursive"
  }

  # Step 3: Delete the S3 bucket itself
  provisioner "local-exec" {
    command = "aws s3api delete-bucket --bucket datacenter-bck-22925"
  }
}

```

Step02: Execute the main.tf file
```
terraform init
terraform apply
terraform plan
```

## Task is Completed!

