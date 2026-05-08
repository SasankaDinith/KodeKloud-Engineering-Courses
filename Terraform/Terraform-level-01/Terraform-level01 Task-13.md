## Task13 - Create Private S3 Bucket Using Terraform

As part of the data migration process, the Nautilus DevOps team is actively creating several S3 buckets on AWS using Terraform.
They plan to utilize both private and public S3 buckets to store the relevant data. Given the ongoing migration of other infrastructure to AWS, 
it is logical to consolidate data storage within the AWS environment as well.

Create an S3 bucket using Terraform with the following details:

1) The name of the S3 bucket must be `xfusion-s3-24599`.

2) The S3 bucket must block all `public` access, making it a private bucket.

The Terraform working directory is `/home/bob/terraform`. Create the `main.tf` file (do not create a different `.tf` file) to accomplish this task.

Notes:

Use Terraform to provision the S3 bucket.
Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.
Ensure the resources are created in the `us-east-1` region.
The bucket must have block public access enabled to restrict any public access.

## Answer:

Step01: Create a main.tf file

Step02: Added below terraform configuration
```
resource "aws_s3_bucket" "xfusion_s3_24599" {
  bucket = "xfusion-s3-24599"

  tags = {
    Name        = "xfusion_s3_24599"

  }
}

resource "aws_s3_bucket_public_access_block" "example" {
  bucket = aws_s3_bucket.xfusion_s3_24599.id

  block_public_acls       = true
  block_public_policy     = true
  ignore_public_acls      = true
  restrict_public_buckets = true
}


```

Step03: Execute the main.tf file
```
terraform init
terraform plan
terraform apply
```


### Task is Completed!
