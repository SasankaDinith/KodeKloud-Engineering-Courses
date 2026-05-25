## Task35 - VPC Variable Setup Using Terraform

The Nautilus DevOps team is automating VPC creation using Terraform to manage networking efficiently. As part of this task, they need to create a VPC with 
specific requirements.

For this task, create an AWS VPC using Terraform with the following requirements:

1) The VPC name `nautilus-vpc` should be stored in a variable named `KKE_vpc`.

2) The VPC should have a CIDR block of `10.0.0.0/16`.

Note:

1) The configuration values should be stored in a `variables.tf` file.

2) The Terraform script should be structured with a `main.tf` file referencing `variables.tf`.

3) The Terraform working directory is `/home/bob/terraform`.

4) 2Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01: Create main.tf file and added this content
```
resource "aws_vpc" "nautilus_vpc" {
  cidr_block = var.cidr_block

  tags = {
    Name = var.KKE_vpc
  }
}
```
Step02: Create variables.tf file and added below content
```
variable "KKE_vpc" {
    type = string
    default = "nautilus_vpc"
}

variable "cidr_block" {
    type = string
    default = "10.0.0.0/16"
}
```
Step03: Execute the terraform project
```
terraform init
terraform plan
terraform apply
```

### Task is Completed!
