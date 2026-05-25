## Task37 - Elastic IP Variable Setup Using Terraform

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. As part of this phased migration approach, 
they need to allocate an Elastic IP address to support external access for specific workloads.

For this task, create an AWS Elastic IP using Terraform with the following requirement:

The Elastic IP name `datacenter-eip` should be stored in a variable named `KKE_eip`. The Terraform working directory is `/home/bob/terraform`.

Note:

The configuration values should be stored in a `variables.tf` file.

The Terraform script should be structured with a `main.tf` file referencing `variables.tf`.

Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01: Create main.tf file and added below content 
```
resource "aws_eip" "datacenter-eip" {
 
  domain   = "vpc"

  tags = {
    Name = var.KKE_eip
  }
}
```
Step02: Create variables.tf file and added below content 
```
variable "KKE_eip" {
   type = string
   default  = "datacenter-eip"
}
```

Step03: Execute the terraform project
```
terraform init
terraform plan
terraform apply
```
### Task is Completed!

