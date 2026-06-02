## Task06 - 

The Nautilus DevOps team needs to create an AMI from an existing EC2 instance for backup and scaling purposes. The following steps are required:

1) They have an existing EC2 instance named `xfusion-ec2`.

2) They need to create an AMI named `xfusion-ec2-am`i from this instance.

3) Additionally, they need to launch a new EC2 instance named `xfusion-ec2-new` using this AMI.

4) Update the `main.tf` file (do not create a different or `separate.tf` file) to provision an AMI and then launch an EC2 Instance from that AMI.

5) Create an outputs.tf file to output the following values:
```
KKE_ami_id for the AMI ID you created.
KKE_new_instance_id for the EC2 instance ID you created.
```

Notes:

The Terraform working directory is `/home/bob/terraform`.

Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

Before submitting the task, ensure that `terraform plan` returns `No changes. Your infrastructure matches the configuration`.

## Answer:
Step01: Update the main.tf file as follows
```


data "aws_instances" "existing" {
  filter {
    name   = "tag:Name"
    values = ["xfusion-ec2"]
  }
}


resource "aws_instance" "ec2" {
  ami           = "ami-0c101f26f147fa7fd"
  instance_type = "t2.micro"
  vpc_security_group_ids = [
    "sg-a537aaa701cd5183c"
  ]

  tags = {
    Name = "xfusion-ec2"
  }
}

resource "aws_ami_from_instance" "xfusion_ec2_ami" {
  name               = "xfusion-ec2-ami"
  source_instance_id = data.aws_instances.existing.ids[0]

  tags = {
    Name = "xfusion-ec2-ami"
  }
}

resource "aws_instance" "xfusion_ec2_new" {
  ami           = aws_ami_from_instance.xfusion_ec2_ami.id
  instance_type = "t2.micro"

  
  vpc_security_group_ids = [
    "sg-a537aaa701cd5183c"
  ]


  tags = { 
    Name = "xfusion-ec2-new"
  }

  depends_on = [aws_ami_from_instance.xfusion_ec2_ami]

}
```

Step02: Create outputs.tf file and add this content
```
output "KKE_ami_id" {
    value = aws_ami_from_instance.xfusion_ec2_ami.id
}

output "KKE_new_instance_id" {
    value = aws_instance.xfusion_ec2_new.id

}
```

## Step03: Exeure the terraform project
```
terraform init
terraform plan
terraform aoply
```

### Task is Completed!
