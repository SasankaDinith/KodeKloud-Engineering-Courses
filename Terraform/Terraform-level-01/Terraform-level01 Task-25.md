## Task25 - Change Instance Type Using Terraform


decide to change the instance type. Please make sure the Status check is completed (if it's still in Initializing state) before making any changes to the instance.

Change the instance type from `t2.micro` to `t2.nano` for `devops-ec2` instance using terraform.

Make sure the EC2 instance `devops-ec2` is in running state after the change.

The Terraform working directory is `/home/bob/terraform`. Update the `main.tf` file (do not create a separate `.tf` file) to change the instance type.

`Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer

Step01: Modify the main.tf file as instance type "t2.micro" into "t2.nano"

Step02: Execute the updated main.tf file
```
terraform init
terraform plan
terraform apply 
```

### Task is Completed!
