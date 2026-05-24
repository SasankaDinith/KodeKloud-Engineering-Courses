## Task30 - Delete EC2 Instance Using Terraform

During the migration process, several resources were created under the AWS account. Some of these test resources are no longer needed at the moment,
so we need to clean them up temporarily. One such instance is currently unused and should be deleted.

1) Delete the ec2 instance named `nautilus-ec2` present in `us-east-1` region using `terraform`. Make sure to keep the provisioning code,
as we might need to provision this instance again later.

2) Before submitting your task, make sure instance is in `terminated` state.

The Terraform working directory is `/home/bob/terraform`.

`Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01: Open the main.tf file and execute below command to delete the EC2 instance
```
terraform destroy
```

Step02: After sucessfully destroying that instance, wait some time to update it's state as terminate

### Task is Completed!





