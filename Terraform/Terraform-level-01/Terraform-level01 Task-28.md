## Task28 - Enable S3 Versioning Using Terraform




## Answer:

Step01: Update the main.tf file such as follows
```
resource "aws_s3_bucket" "s3_ran_bucket" {
  bucket = "datacenter-s3-28828"


  tags = {
    Name        = "datacenter-s3-28828"
  }
}

resource "aws_s3_bucket_acl" "example" {
  bucket = aws_s3_bucket.s3_ran_bucket.id
  acl    = "private"
}

resource "aws_s3_bucket_versioning" "versioning_example" {
  bucket = aws_s3_bucket.s3_ran_bucket.id
  versioning_configuration {
    status = "Enabled"
  }
}
```
Step02: Execute the main.tf file 
```
terraform init
terraform plan
terraform apply
```

### Task is Completed!
