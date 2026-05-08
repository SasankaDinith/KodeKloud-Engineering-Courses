## Task17 - Create DynamoDB Table Using Terraform

The Nautilus DevOps team needs to set up a DynamoDB table for storing user data. They need to create a DynamoDB table with the following specifications:

1) The table name should be `datacenter-users`.

2) The primary key should be `datacenter_id` (String).

3) The table should use `PAY_PER_REQUEST` billing mode.

Use `Terraform` to create this `DynamoDB` table. The Terraform working directory is `/home/bob/terraform`.
Create the `main.tf` file (do not create a different `.tf` file) to create the DynamoDB table.

`Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer: 

Step01: Create a main.tf file

Step02: Added below terraform configuration into main.tf file
```
resource "aws_dynamodb_table" "datacenter-users" {
    name           = "datacenter-users"
    billing_mode   = "PAY_PER_REQUEST"
    
    hash_key       = "datacenter_id"

    
    attribute {
      name = "datacenter_id"
      type = "S"
    }


    tags = {
      Name        = "datacenter-users"
      Environment = "production"
    }


}
```

Step03: Execute the main.tf file 
```
terraform init
terraform plan
terraform apply
```


### Task is Completed!
