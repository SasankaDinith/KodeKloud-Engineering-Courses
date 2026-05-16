## Task19 - Create SNS Topic Using Terraform

The Nautilus DevOps team needs to set up an SNS topic for sending notifications. They need to create an SNS topic with the following specifications:

1) The topic name should be `devops-notifications`.

Use Terraform to create this SNS topic. The Terraform working directory is `/home/bob/terraform`. Create the `main.tf` file (do not create a different `.tf` file) to accomplish this task.

`Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01:  Create a main.file
Step02:  Added this terraform configuration into main.tf file
```
resource "aws_sns_topic" "devops_notifications" {
  name = "devops-notifications"
}
```
Step03: Execute the main.tf file
```
terraform init
terraform plan
terraform apply
```

### Task is Completed!
