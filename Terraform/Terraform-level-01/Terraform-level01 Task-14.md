## Task14 - Create IAM User Using Terraform

When establishing infrastructure on the AWS cloud, Identity and Access Management (IAM) is among the first and most critical services to configure. 
IAM facilitates the creation and management of user accounts, groups, roles, policies, and other access controls. The Nautilus DevOps team is currently
in the process of configuring these resources and has outlined the following requirements:

For this task, create an `IAM user` named `iamuser_rose` using terraform. The Terraform working directory is `/home/bob/terraform`. 
Create the `main.tf` file (do not create a different `.tf` file) to accomplish this task.

`Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01: Create main.tf file

Step02: Added this terraform configuration into main.tf file
```
resource "aws_iam_user" "iamuser_rose" {
  name = "iamuser_rose"
  path = "/home/bob/terraform"

  tags = {
    Name = "iamuser_rose"
  }
}

```

Step03: Execute the main.tf file
```
terraform init
terraform apply
```
### Task is Completed!
