## Task22 - CloudFormation Template Deployment Using Terraform


The Nautilus DevOps team is working on automating infrastructure deployment using AWS CloudFormation. As part of this effort, they need to create a CloudFormation stack 
that provisions an S3 bucket with versioning enabled.

Create a CloudFormation stack named `xfusion-stack` using `Terraform`. This stack should contain an S3 bucket named `xfusion-bucket-10131` as a resource,
and the bucket must have versioning enabled. The Terraform working directory is `/home/bob/terraform`. Create the `main.tf` file 
(do not create a different `.tf` file) to accomplish this task.

`Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01: Create main.tf file

Step02: Added this terraform configuration into main.tf file
```

resource "aws_cloudformation_stack" "xfusion_stack" {
  name = "xfusion-stack"

  template_body = <<STACK
{
  "AWSTemplateFormatVersion": "2010-09-09",
  "Resources": {
    "XfusionBucket": {
      "Type": "AWS::S3::Bucket",
      "Properties": {
        "BucketName": "xfusion-bucket-10131",
        "VersioningConfiguration": {
          "Status": "Enabled"
        }
      }
    }
  }
}
STACK
}
```

Step03: Execute the main.tf file
```
terraform init
terraform plan
terraform apply
```

### Task is Completed!

