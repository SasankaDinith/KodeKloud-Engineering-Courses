## Task36 - Security Group Variable Setup Using Terraform

The Nautilus DevOps team is enhancing infrastructure automation and needs to provision a Security Group using Terraform with specific configurations.

For this task, create an AWS Security Group using `Terraform` with the following requirements:

The Security Group name nautilus-sg should be stored in a variable named `KKE_sg`.
Note:

1. The configuration values should be stored in a `variables.tf` file.

2. The Terraform script should be structured with a `main.tf` file referencing `variables.tf`.
3. The Terraform working directory is `/home/bob/terraform`.

4. Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.


## Answer:

Step01: Create main.tf file and added below content to it
```
variable "region" {
  description = "AWS region"
  default     = "us-east-1"
}

variable "KKE_sg" {
  description = "Security Group name"
  default     = "nautilus-sg"
}

variable "vpc_id" {
  description = "VPC ID where Security Group will be created"
}


```
Step02: Create variables.tf file and added below content to it
```
resource "aws_security_group" "nautilus_sg" {
  name        = var.KKE_sg
  description = "Security group for Nautilus DevOps team"
  vpc_id      = var.vpc_id

  # Example ingress rule (Allow SSH)
  ingress {
    description = "Allow SSH"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  # Example egress rule (Allow all outbound)
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = var.KKE_sg
  }
}


```
Step03: Execute the terraform project
```
terraform init
terraform plan
terraform apply
```
### Task is Completed!
