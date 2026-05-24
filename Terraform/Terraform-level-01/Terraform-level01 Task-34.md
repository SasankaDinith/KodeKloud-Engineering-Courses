## Task34 - Copy Data to S3 Using Terraform

AWS S3 buckets. They have recently received some data that they intend to copy to one of the S3 buckets.

S3 bucket named `datacenter-cp-6060` already exists. Copy the file `/tmp/datacenter.txt` to s3 bucket `datacenter-cp-6060` using `Terraform`. 
The Terraform working directory is `/home/bob/terraform`. Update the `main.tf` file (do not create a separate `.tf` file) to accomplish this task.

`Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:
Step01: Update the main.tf file content as follows
```
resource "aws_s3_bucket" "my_bucket" {
  bucket = "datacenter-cp-6060"
  acl    = "private"

  tags = {
    Name        = "datacenter-cp-6060"
  }
}


resource "aws_s3_object" "upload_file" {
  bucket = "datacenter-cp-6060"
  key    = "datacenter.txt"
  source = "/tmp/datacenter.txt"

  etag = filemd5("/tmp/datacenter.txt")
}
```

Step02: Execute the main.tf file
```
terraform init
terraform plan
terraform apply
```

### Task is Completed!


