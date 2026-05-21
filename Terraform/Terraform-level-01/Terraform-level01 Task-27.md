## Task27 - Attach Policy Using Terraform

The Nautilus DevOps team has been creating a couple of services on AWS cloud. They have been breaking down the migration into smaller tasks, allowing for 
better control, risk mitigation, and optimization of resources throughout the migration process. Recently they came up with requirements mentioned below.

An IAM user named `iamuser_kareem` and a policy named `iampolicy_kareem` already exists. Use Terraform to attach the IAM policy `iampolicy_kareem` to the IAM user 
`iamuser_kareem`. The Terraform working directory is `/home/bob/terraform`. Update the `main.tf` file (do not create a separate `.tf` file) to attach the specified IAM policy to the IAM user.

`Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01: Update the main.tf file as adding this part
```
resource "aws_iam_user_policy_attachment" "attachment" {
  user       = aws_iam_user.user.name
  policy_arn = aws_iam_policy.policy.arn
}
```
Step02: Execute the main.tf file
```
terraform init
terraform plan
terraform apply
```
### Task is Completed!
