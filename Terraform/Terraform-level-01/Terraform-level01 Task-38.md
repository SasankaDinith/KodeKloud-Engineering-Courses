## Task38 - User Variable Setup Using Terraform

The Nautilus DevOps team is automating IAM user creation using Terraform for better identity management.

For this task, create an AWS IAM User using Terraform with the following requirements:

The IAM User name `iamuser_javed` should be stored in a variable named `KKE_user`.
Note:

1. The configuration values should be stored in a `variables.tf` file.

2. The Terraform script should be structured with a `main.tf` file referencing `variables.tf`.
The Terraform working directory is `/home/bob/terraform`.

Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01: Create main.tf file and added below content
```
resource "aws_iam_user" "lb" {
  name = var.KKE_user
  path = "/system/"

  
}
```
Step02: Create variables.tf file and added below content
```
variable "KKE_user" {
    type = string
    default = "iamuser_javed"
}
```

Step03: Execute the terraform project
```
terraform init
terraform plan
terraform apply
```

### Task is Completed!
