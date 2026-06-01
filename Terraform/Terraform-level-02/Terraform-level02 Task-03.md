## Task03 - Replace Existing EC2 Instance via Terraform

To test resilience and recreation behavior in Terraform, the DevOps team needs to demonstrate the use of the `-replace` option to forcefully recreate an 
EC2 instance without changing its configuration. Please complete the following tasks:

1) Use the Terraform CLI `-replace` option to destroy and recreate the EC2 instance `datacenter-ec2`, even though the configuration remains unchanged.

2) Ensure that the instance is recreated successfully.


Notes:

1) The new instance created using the `-replace` option should have a different instance ID than the previously provisioned instance.

2) The Terraform working directory is `/home/bob/terraform`.

3) Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

4) Before submitting the task, ensure that `terraform plan` returns `No changes. Your infrastructure matches the configuration`.

## Answer:

Step01: Open the terminal and execute below commands one by one
```
terraform plan -replace="aws_instance.datacenter_ec2"

terraform apply -replace="aws_instance.datacenter_ec2"
```


### Task is Completed!
