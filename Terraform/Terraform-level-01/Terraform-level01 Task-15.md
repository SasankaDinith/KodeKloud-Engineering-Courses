## Task15 - Create IAM Group Using Terraform

The yousuf DevOps team has been creating a couple of services on AWS cloud. They have been breaking down the migration into smaller tasks, allowing for better
control, risk mitigation, and optimization of resources throughout the migration process. Recently they came up with requirements mentioned below.

Create an IAM group named `iamgroup_yousuf` using terraform.

The Terraform working directory is `/home/bob/terraform` Create the `main.tf` file (do not create a different `.tf` file) to accomplish this task.

`Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01: Create a main.tf file

Step02: Added this terraform configuration into main.tf file
```
resource "aws_iam_group" "iamgroup_yousuf" {
  name = "iamgroup_yousuf"
  path = "/home/bob/terraform"
}
```
Step03: Execute the main.tf file
```
terraform init
terraform plan
terraform apply
```

### Task is Completed!
