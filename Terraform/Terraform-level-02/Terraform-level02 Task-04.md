## Task04 - 

The Nautilus DevOps team wants to provision multiple EC2 instances in AWS using Terraform. Each instance should follow a consistent naming convention and be 
deployed using a modular and scalable setup.

Use Terraform to:

1) Create 3 EC2 instances using the `count` parameter.

2) Name each EC2 instance with the prefix `devops-instance` (e.g., `devops-instance-1`).

3) Instances should be `t2.micro`.

4) The key named should be `devops-key`.

5) Create `main.tf` file (do not create a separate `.tf` file) to provision these instances.

6) Use variables.tf file with the following:
```
KKE_INSTANCE_COUNT: number of instances.
KKE_INSTANCE_TYPE: type of the instance.
KKE_KEY_NAME: name of key used.
KKE_INSTANCE_PREFIX: name of the instnace.
```

7) Use the `locals.tf` file to define a local variable named `AMI_ID` that retrieves the latest Amazon Linux 2 AMI using a data source.

8) Use `terraform.tfvars` to assign values to the variables.

9) Use `outputs.tf` file to output the following:
```
kke_instance_names: names of the instances created.
```

Notes:

The Terraform working directory is `/home/bob/terraform`.

Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

Before submitting the task, ensure that `terraform plan` returns `No changes. Your infrastructure matches the configuration`.


## Answer:

Step01: Create main.tf file and add this content
```

data "aws_ami" "amazon_linux" {
  most_recent = true

  owners = ["amazon"]

  filter {
    name   = "name"
    values = ["amzn2-ami-hvm-*-x86_64-gp2"]
  }
}


resource "aws_instance" "devops_instance" {
  count         = var.KKE_INSTANCE_COUNT
  ami           = local.AMI_ID
  instance_type = var.KKE_INSTANCE_TYPE
  key_name      = var.KKE_KEY_NAME

  tags = {
    Name = "${var.KKE_INSTANCE_PREFIX}-${count.index + 1}"
  }
}
```

Step02: Create variables.tf file and add this content
```
variable "KKE_INSTANCE_COUNT" {
    description = "Instance count need to create"
    type = string
}


variable "KKE_INSTANCE_TYPE" {
    description = "Instance type should be assign"
    type = string
}

variable "KKE_KEY_NAME" {
    description = "Key name that should be assign"
    type = string
}

variable "KKE_INSTANCE_PREFIX" { 
    description = "Instance prefix name"
    type = string
}


```

Step03: Create local.tf file and add this content
```
locals { 
    AMI_ID = data.aws_ami.amazon_linux.id
}
```

Step04: Create terraform.tfvars file and add this content
```
KKE_INSTANCE_COUNT = 3
KKE_INSTANCE_TYPE = "t2.micro"
KKE_KEY_NAME = "devops-key"
KKE_INSTANCE_PREFIX = "devops-instance"
```

Step05: Create outputs.tf file and add this content
```
output "kke_instance_names" {
  value = [
    for instance in aws_instance.devops_instance :
    instance.tags.Name
  ]
}

### Task is Completed!
```
