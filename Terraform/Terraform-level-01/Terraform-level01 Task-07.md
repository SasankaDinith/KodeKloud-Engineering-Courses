## Task07 - Create EC2 Instance Using Terraform

The Nautilus DevOps team is strategizing the migration of a portion of their infrastructure to the AWS cloud. Recognizing the scale of this undertaking, 
they have opted to approach the migration in incremental steps rather than as a single massive transition. To achieve this, they have segmented large tasks 
into smaller, more manageable units.

For this task, create an EC2 instance using `Terraform` with the following requirements:

   - The EC2 instance must use the value `devops-ec2` as its Name tag, which defines the instance name in AWS.

   - Use the `Amazon Linux` `ami-0c101f26f147fa7fd` to launch this instance.

   - The Instance type must be `t2.micro`.

   - Create a new `RSA` key named `devops-kp`.

   - Attach the default (available by default) security group.

   - The Terraform working directory is `/home/bob/terraform`. Create the `main.tf` file (do not create a different `.tf` file) to provision the instance.

  ` Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

  ## Answer: 

  Step01: Create a main.tf file

  Step02: Added this terraform configurations into main.tf file
  ```
resource "tls_private_key" "devops-kp" {
  algorithm = "RSA"
  rsa_bits  = 4096
}

resource "aws_key_pair" "devops-key" {
    key_name = "devops-key"
    public_key = tls_private_key.devops-kp.public_key_openssh

}

resource "aws_instance" "devops-ec2" {
    ami = "ami-0c101f26f147fa7fd"
    instance_type = "t2.micro"
    key_name = aws_key_pair.devops-key.key_name

    tags = {
        Name = "devops-ec2"
    }
}

  ```
Step03: Execute the terraform file 
```
terraform init
terraform apply
```

### Task is Completed!
