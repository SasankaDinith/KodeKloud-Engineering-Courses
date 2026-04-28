## Task12 - Create Public S3 Bucket Using Terraform

As part of the data migration process, the Nautilus DevOps team is actively creating several S3 buckets on AWS. They plan to utilize both private and public S3 
buckets to store the relevant data. Given the ongoing migration of other infrastructure to AWS, it is logical to consolidate data storage within the AWS
environment as well.

-    Create a `public` S3 bucket named `datacenter-s3-8649` using Terraform.

-    Ensure the bucket is accessible publicly once created by setting the proper ACL.

-    The Terraform working directory is `/home/bob/terraform`. Create the `main.tf` file (do not create a different `.tf` file) to accomplish this task.

Notes:

 -  Create the resources only in the `us-east-1` region.
  -  Right-click under the EXPLORER section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.
   - The name of the S3 bucket should be based on `datacenter-s3-8649`.
  -  You can use the `ACL` settings to ensure the bucket is publicly accessible.

## Answer:

Step01: Create main.tf file

Step02: Added this terraform configuration into main.tf file
```
resource "aws_s3_bucket" "datacenter_bucket" {
  bucket = "datacenter-s3-3302"
}

resource "aws_s3_bucket_ownership_controls" "datacenter_bucket_ownership" {
  bucket = aws_s3_bucket.datacenter_bucket.id

  rule {
    object_ownership = "BucketOwnerPreferred"
  }
}

resource "aws_s3_bucket_public_access_block" "datacenter_bucket_public_access" {
  bucket = aws_s3_bucket.datacenter_bucket.id

  block_public_acls       = false
  block_public_policy     = false
  ignore_public_acls      = false
  restrict_public_buckets = false
}

resource "aws_s3_bucket_acl" "datacenter_bucket_acl" {
  depends_on = [
    aws_s3_bucket_ownership_controls.datacenter_bucket_ownership,
    aws_s3_bucket_public_access_block.datacenter_bucket_public_access,
  ]

  bucket = aws_s3_bucket.datacenter_bucket.id
  acl    = "public-read"
}
```

Step03: Execute the main.tf file
```
terraform init
terraform plan
```

### Task is Completed!
