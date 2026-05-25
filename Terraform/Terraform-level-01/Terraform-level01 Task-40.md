## Task40 - Policy Variable Setup Using Terraform


The Nautilus DevOps team is automating IAM policy creation using Terraform to enhance security and access management. As part of this task, they need to 
create an IAM policy with specific requirements.

For this task, create an AWS IAM policy using Terraform with the following requirements:

The IAM policy name `iampolicy_jim` should be stored in a variable named `KKE_iampolicy`.
Note:

The configuration values should be stored in a `variables.tf` file.

The Terraform script should be structured with a `main.tf` file referencing `variables.tf`.

The Terraform working directory is `/home/bob/terraform`.

Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:
Step01: Create main.tf file and added below content
```
resource "aws_iam_policy" "policy" {
  name        = var.KKE_iampolicy
  path        = "/"
  description = "My test policy"

  
  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [
      {
        Action = [
          "ec2:Describe*",
        ]
        Effect   = "Allow"
        Resource = "*"
      },
    ]
  })
}
```

Step02: Create variables.tf file and added below content
```
variable "KKE_iampolicy" {
    type = string
    default = "iampolicy_javed"
}
```
Step03: Execute the terraform project
```
terraform init
terraform plan
terraform apply
```

### Task is Completed!
