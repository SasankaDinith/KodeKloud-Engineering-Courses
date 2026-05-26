## Task01 - Create VPC and Subnet Using Terraform

To ensure proper resource provisioning order, the DevOps team wants to explicitly define the dependency between an AWS VPC and a Subnet. The objective is to 
create a VPC and then a Subnet that explicitly depends on it using Terraform's depends_on argument.

Please complete the following tasks:

1). Create a VPC named `xfusion-vpc`.

2). Create a Subnet named `xfusion-subnet`.

3). Ensure the Subnet uses the `depends_on` argument to explicitly depend on the VPC resource.

4). Create the `main.tf` file (do not create a separate `.tf` file) to provision a VPC and Subnet.

5). Use `variables.tf`, define the following variables:

- `KKE_VPC_NAME` for the VPC name.
- `KKE_SUBNET_NAME` for the Subnet name.

6). Use `terraform.tfvars` to input the names of the VPC and subnet.

7). In `outputs.tf`, output the following:

- `kke_vpc_name`: The name of the VPC.
- `kke_subnet_name`: The name of the Subnet.

Notes:

The Terraform working directory is `/home/bob/terraform`.

Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

Before submitting the task, ensure that `terraform plan` returns `No changes. Your infrastructure matches the configuration`.

## Answer:

Step01: Create main.tf file and add this content
```
resource "aws_vpc" "xfusion_vpc" {
  cidr_block = "10.0.0.0/16"

  tags = { 
    Name = var.KKE_VPC_NAME
  }
}

resource "aws_subnet" "xfusion_subnet" {
  vpc_id     = aws_vpc.xfusion_vpc.id
  cidr_block = "10.0.1.0/24"

  tags = {
    Name = var.KKE_SUBNET_NAME
  }

   depends_on = [aws_vpc.xfusion_vpc]
}
```
Step02: Create variables.tf file and add this content
```
variable "KKE_VPC_NAME" {
   description = "vpc name"
}

variable "KKE_SUBNET_NAME" { 
    description = "subnet name"
}
```

Step03: Create terraform.tfvars file and add this content
```
KKE_VPC_NAME = "xfusion-vpc"
KKE_SUBNET_NAME = "xfusion-subnet"
```
Step04: Create outputs.tf file and add this content
```
output "kke_vpc_name" {
    value = aws_vpc.xfusion_vpc.tags["Name"]
}

output "kke_subnet_name" {
    value = aws_subnet.xfusion_subnet.tags["Name"]
}
```

Step05: Execute the terraform project
```
terraform init
terraform plan
terraform apply
```

### Task is Completed!
