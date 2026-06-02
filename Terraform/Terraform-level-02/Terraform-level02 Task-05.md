## Task05 - Associate Elastic IP with EC2 Instance Using Terraform

The Nautilus DevOps Team has received a new request from the Development Team to set up a new EC2 instance. This instance will be used to host a new application 
that requires a stable IP address. To ensure that the instance has a consistent public IP, an Elastic IP address needs to be associated with it.
This setup will help the Development Team to have a reliable and consistent access point for their application.

1) Create an EC2 instance named `nautilus-ec2` using any Linux AMI like `Ubuntu`.

2) Instance type must be `t2.micro` and associate an Elastic IP address named `nautilus-eipwith` this instance.

3) Use the `main.tf` file (do not create a separate `.tf` file) to provision the EC2-Instance and Elastic IP.

4) Use the `outputs.tf` file and output the instance name using variable `KKE_instance_name` and the Elastic IP using variable `KKE_eip`.


Notes:

The Terraform working directory is `/home/bob/terraform`.

Right-click under the `EXPLORER` section in VS Code and select `Open in Integrated Terminal` to launch the terminal.

Before submitting the task, ensure that `terraform plan` returns `No changes. Your infrastructure matches the configuration`.

## Answer:

Step01: Create main.tf file and add below content
```

data "aws_ami" "ubuntu" {
  most_recent = true

  owners = ["099720109477"] # Canonical

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-*-amd64-server-*"]
  }
}

resource "aws_instance" "devops_ec2" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = "t2.micro"

  tags = {
    Name = "devops_ec2"
  }
}

resource "aws_eip" "devops_eip" {
  instance = aws_instance.devops_ec2.id
  vpc = true

  tags = {
    Name = "devops_eip"
  }
}

```

Step02: Create outputs.tf file and added below content
```
output "KKE_instance_name" {
    value = aws_instance.nautilus_ec2.tags["Name"]
}

output "KKE_eip" {
    value = aws_eip.nautilus_eip.public_ip
}
```
Step03: Execute the terraform project
```
terraform init
terraform plan
terraform apply
```


### Task is Completed!
