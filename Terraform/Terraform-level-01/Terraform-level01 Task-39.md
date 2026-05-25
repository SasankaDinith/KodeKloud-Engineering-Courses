## Task39 - Role variable setup using Terraform

The Nautilus DevOps team is automating IAM role creation using Terraform to streamline permissions management. As part of this task, they need to create
an IAM role with specific requirements.

For this task, create an AWS IAM role using Terraform with the following requirements:

The IAM role name `iamrole_javed` should be stored in a variable named `KKE_iamrole`.

Note:

1. The configuration values should be stored in a `variables.tf` file.

2. The Terraform script should be structured with a `main.tf` file referencing `variables.tf`.
The Terraform working directory is `/home/bob/terraform`.

Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01: Create main.tf file and added below content
```
resource "aws_iam_role" "test_role" {
  name = var.KKE_iamrole

  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Action = "sts:AssumeRole"
        Effect = "Allow"
        Sid    = ""
        Principal = {
          Service = "ec2.amazonaws.com"
        }
      },
    ]
  })
}
```

Step02: Create variables.tf file and added  below content
```
variable "KKE_iamrole" {
    type = string
    default = "iamrole_javed"

}
```

Step03: Execute the terraform project
```
terraform init
terraform plan
terraform apply
```

### Task is Completed!
