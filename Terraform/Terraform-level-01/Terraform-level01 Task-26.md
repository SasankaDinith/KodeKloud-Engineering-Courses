## Task26 - Attach Elastic IP Using Terraform

The Nautilus DevOps team has been creating a couple of services on AWS cloud. They have been breaking down the migration into smaller tasks, 
allowing for better control, risk mitigation, and optimization of resources throughout the migration process. Recently they came up with requirements mentioned below.

There is an instance named `xfusion-ec2` and an elastic-ip named `xfusion-ec2-eip` in `us-east-1` region. Attach the `xfusion-ec2-eip` elastic-ip to the `xfusion-ec2` instance using `Terraform` only.
The Terraform working directory is `/home/bob/terraform`. Update the `main.tf` file (do not create a separate `.tf` file) to attach the specified Elastic IP to the instance.

`Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01: Modify the main.tf file as adding this part
```
resource "aws_eip_association" "eip_assoc" {
  instance_id   = aws_instance.xfusion-ec2.id
  allocation_id = aws_eip.xfusion-ec2-eip.id
}
```
Step025: Execute the main.tf file
```
terraform init
terraform plan
terraform apply
```

### Task is Completed!
