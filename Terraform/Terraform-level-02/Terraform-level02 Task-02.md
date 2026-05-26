## Task02 - Launch EC2 in Private VPC Subnet Using Terraform


The Nautilus DevOps team is expanding their AWS infrastructure and requires the setup of a private Virtual Private Cloud (VPC) along with a subnet. 
This VPC and subnet configuration will ensure that resources deployed within them remain isolated from external networks and can only communicate within the VPC.
Additionally, the team needs to provision an EC2 instance under the newly created private VPC. This instance should be accessible only from within the VPC, 
allowing for secure communication and resource management within the AWS environment.

1). Create a VPC named `nautilus-priv-vpc` with the CIDR block `10.0.0.0/16`.

2). Create a subnet named `nautilus-priv-subnet` inside the VPC with the CIDR block `10.0.1.0/24` and auto-assign IP option must not be enabled.

3). Create an EC2 instance named `nautilus-priv-ec2` inside the subnet and instance type must be `t2.micro`.

4). Ensure the security group of the EC2 instance allows access only from within the VPC's CIDR block.

5). Create the `main.tf` file (do not create a separate `.tf` file) to provision the VPC, subnet and EC2 instance.

6). Use `variables.tf` file with the following variable names:

- `KKE_VPC_CIDR` for the VPC CIDR block.
- `KKE_SUBNET_CIDR` for the subnet CIDR block.
  
7). Use the `outputs.tf` file with the following variable names:

- `KKE_vpc_name` for the name of the VPC.
- `KKE_subnet_name` for the name of the subnet.
- `KKE_ec2_private` for the name of the EC2 instance.

Notes:

1). The Terraform working directory is `/home/bob/terraform`.

2). Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

3). Before submitting the task, ensure that `terraform plan` returns `No changes. Your infrastructure matches the configuration`.


## Answer:

Step01: Create main.tf file and add this content
```
resource "aws_vpc" "nautilus_priv_vpc" {
    cidr_block = var.KKE_VPC_CIDR


    tags = { 
        Name = "nautilus-priv-vpc"
    }
}

resource "aws_subnet" "nautilus_priv_subnet" {
    vpc_id     = aws_vpc.nautilus_priv_vpc.id
    cidr_block = var.KKE_SUBNET_CIDR
    map_public_ip_on_launch = false

     tags = {
        Name = "nautilus-priv-subnet"
   
     }

}


resource "aws_security_group" "nautilus_priv_sg" {
  name        = "nautilus-priv-sg"
  description = "Allow access only within VPC"
  vpc_id      = aws_vpc.nautilus_priv_vpc.id

  ingress {
    description = "Allow all within VPC"
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["10.0.0.0/16"]
  }

  egress {
    description = "Allow all outbound within VPC"
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["10.0.0.0/16"]
  }

  tags = {
    Name = "nautilus-priv-sg"
  }
}


data "aws_ami" "amazon_linux" {
  most_recent = true
  owners      = ["amazon"]

  filter {
    name   = "name"
    values = ["amzn2-ami-hvm-*-x86_64-gp2"]
  }
}

resource "aws_instance" "nautilus_priv_ec2" {
    ami = data.aws_ami.amazon_linux.id
    instance_type = "t2.micro"
    subnet_id = aws_subnet.nautilus_priv_subnet.id
  
    vpc_security_group_ids      = [aws_security_group.nautilus_priv_sg.id]
    associate_public_ip_address = false


    tags = {
        Name = "nautilus_priv_ec2"
    }
}
```

Step02: Create variables.tf file and add this content
```
variable "KKE_VPC_CIDR" {
    type = string
    default = "10.0.0.0/16"
}

variable "KKE_SUBNET_CIDR" {
    type = string
    default = "10.0.0.0/24"
}
```

Step03: Create outputs.tf file and add this content
```
output "KKE_vpc_name" {
    value = aws_vpc.nautilus_priv_vpc.tags["Name"]
}

output "KKE_subnet_name" {
    value = aws_subnet.nautilus_priv_subnet.tags["Name"]
}

output "KKE_ec2_private" {
    value = aws_instance.nautilus_priv_ec2.tags["Name"]
}
```

Step05: Execute the terraform project
```
terraform init
terraform plan
terraform apply
```

### Task is Completed!
