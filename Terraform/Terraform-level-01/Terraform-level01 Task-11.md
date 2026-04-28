## Task11 - Create Alarm Using Terraform

The Nautilus DevOps team is setting up monitoring in their AWS account. As part of this, they need to create a CloudWatch alarm.
Using `Terraform`, perform the following:
Task Details:

1. Create a CloudWatch alarm named `nautilus-alarm`.
2. The alarm should monitor CPU utilization of an EC2 instance.
3. Trigger the alarm when CPU utilization exceeds 80%.
4. Set the evaluation period to 5 minutes.
5. Use a single evaluation period.
Ensure that the entire configuration is implemented using `Terraform`. The Terraform working directory is `/home/bob/terraform`. Create the `main.tf` file (do not create a different `.tf` file) to accomplish this task.
`Note:` Right-click under the `EXPLORER` section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

## Answer:

Step01: Create main.tf file

Step02: Added this terraform configuration into that file
```
resource "aws_cloudwatch_metric_alarm" "nautilus_alarm" {
  alarm_name          = "nautilus-alarm"
  comparison_operator = "GreaterThanThreshold"
  evaluation_periods  = 1
  metric_name         = "CPUUtilization"
  namespace           = "AWS/EC2"
  period              = 300
  statistic           = "Average"
  threshold           = 80

  alarm_description = "This alarm monitors EC2 CPU utilization and triggers when it exceeds 80%"

}

```

Step03: Execute the main.tf file
```
terraform init
terraform apply
```

### Task is Completed!
