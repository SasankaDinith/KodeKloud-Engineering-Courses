## Task20 - Create SSM Parameter Using Terraform

The Nautilus DevOps team needs to create an SSM parameter in AWS with the following requirements:

1) The name of the parameter should be `nautilus-ssm-parameter`.

2) Set the parameter type to `String`.

3) Set the parameter value to `nautilus-value`.

4) The parameter should be created in the `us-east-1` region.

5) Ensure the parameter is successfully created using `terraform` and can be retrieved when the task is completed.

The Terraform working directory is `/home/bob/terraform`. Create the `main.tf` file (do not create a different `.tf` file) to accomplish this task.

`Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01: Create main.tf file
Step02: Add this terraform configuration into main.tf file
```
resource "aws_ssm_parameter" "nautilus_ssm_parameter" {
  name  = "nautilus-ssm-parameter"
  type  = "String"
  value = "nautilus_value"
}
```
Step03: Execute the main.tf file
```
terraform init
terraform plan
terraform apply
```
Step04: Verify the parameter exists
```
aws ssm get-parameter --name nautilus-ssm-parameter --region us-east-1
```

### Task is Completed!


