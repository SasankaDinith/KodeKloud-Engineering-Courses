## Task14 - Provision IAM User with Terraform

The Nautilus DevOps team is experimenting with Terraform provisioners. Your task is to create an IAM user and use a local-exec provisioner to log a 
confirmation message.

1) Create an IAM user named `iamuser_kareem`.

2) Use a `local-exec` provisioner with the IAM user resource to log the message `KKE iamuser_kareem has been created successfully!` to a file called 
`KKE_user_created.log` under `home/bob/terraform`.

3) Create the `main.tf` file (do not create a separate `.tf` file) to provision an IAM user.

4) Use `variables.tf` file with the following:

- `KKE_USER_NAME`: name of the IAM user.
 
5) Use `terraform.tfvars` to input the name of the IAM user.

6) Use `outputs.tf` file with the following:

- `kke_iam_user_name`: name of the IAM user.

Notes:

The Terraform working directory is `/home/bob/terraform`.

Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

Before submitting the task, ensure that `terraform plan` returns No changes. Your infrastructure matches the configuration.

## Answer
