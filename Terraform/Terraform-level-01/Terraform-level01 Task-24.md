## Task24 - 

The Nautilus DevOps team needs to store sensitive data securely using AWS Secrets Manager. They need to create a secret with the following specifications:

1) The secret name should be `xfusion-secret`.

2) The secret value should contain a key-value pair with `username: admin` and `password: Namin123`.

3) Use `Terraform` to create the secret in AWS Secrets Manager.

The Terraform working directory is `/home/bob/terraform`. Create the `main.tf` file (do not create a different `.tf` file) to accomplish this task.

Note: Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01: Create main.tf file

Step02: Added this terraform configuration into main.tf file
```
resource "aws_secretsmanager_secret" "xfusion_secret" {
  name = "xfusion-secret"
  
}

resource "aws_secretsmanager_secret_version" "example" {
  secret_id     = aws_secretsmanager_secret.xfusion_secret.id
  secret_string = jsonencode({
    username = "admin",
    password = "Namin123"
  })

}

```
Step03: Execute the main.tf file
```
terrform init
terraform plan
teraaform apply 
```
