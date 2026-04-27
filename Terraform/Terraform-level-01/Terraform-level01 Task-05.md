## Task05 - Create VPC with IPv6 Using Terraform

The Nautilus DevOps team is strategically planning the migration of a portion of their infrastructure to the AWS cloud.
Acknowledging the magnitude of this endeavor, they have chosen to tackle the migration incrementally rather than as a single, massive transition. 
Their approach involves creating Virtual Private Clouds (VPCs) as the initial step, as they will be provisioning various services under different VPCs.

For this task, create a VPC named `nautilus-vpc` in the `us-east-1` region with the Amazon-provided IPv6 CIDR block using terraform.

The Terraform working directory is `/home/bob/terraform`. Create the `main.tf` file (do not create a different `.tf` file) to accomplish this task.

`Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01: Create a new file as main.tf

Step02: Added this terraform configuration into that main.tf file
```
resource "aws_vpc" "nautilus_vpc" {
  cidr_block                       = "10.0.0.0/16"
  assign_generated_ipv6_cidr_block = true

  tags = {
    Name = "nautilus_vpc"
  }
}
```

Step03: Execute the main.tf file with using below commands
```
terraform init
terraform apply
```

## Task is Completed!
