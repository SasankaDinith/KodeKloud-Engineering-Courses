## Task10 - Create Snapshot Using Terraform

The Nautilus DevOps team has some volumes in different regions in their AWS account. They are going to setup some automated backups so that all important data 
can be backed up on regular basis. For now they shared some requirements to take a snapshot of one of the volumes they have.

Create a snapshot of an existing volume named `nautilus-vol` in `us-east-1` region using `terraform`.

1) The name of the snapshot must be `nautilus-vol-ss`.

2) The description must be `Nautilus Snapshot`.

3) Make sure the snapshot status is `completed` before submitting the task.

The Terraform working directory is `/home/bob/terraform`. Update the `main.tf` file (do not create a separate `.tf` file) to accomplish this task.

`Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer: 

Step01: Update the main.tf file as follows
```
resource "aws_ebs_volume" "k8s_volume" {
  availability_zone = "us-east-1a"
  size              = 5
  type              = "gp2"

  tags = {
    Name        = "nautilus-vol"
  }
}

resource "aws_ebs_snapshot" "nautilus-vol-ss" {
  description = "Nautilus Snapshot"
  volume_id = aws_ebs_volume.k8s_volume.id

  tags = { 
     Name = "nautilus-vol-ss"
  }


}
```
Step02: Execute the main.tf file
```
terraform init
terraform plan
terraform apply
```

### Task is Completed!
