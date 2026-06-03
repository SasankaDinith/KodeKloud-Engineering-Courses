## Task07 - Stream Kinesis Data to CloudWatch Using Terraform

The monitoring team wants to improve observability into the streaming infrastructure. Your task is to implement a solution using Amazon Kinesis and CloudWatch. 
The team wants to ensure that if write throughput exceeds provisioned limits, an alert is triggered immediately.

As a member of the Nautilus DevOps Team, perform the following tasks using Terraform:

1) Create a Kinesis Data Stream: Name the stream `xfusion-kinesis-stream` with a shard count of 1.

2) Enable Monitoring: Enable shard-level metrics for the stream to track ingestion and throughput errors.

3) Create a CloudWatch Alarm: Name the alarm `xfusion-kinesis-alarm` and monitor the `WriteProvisionedThroughputExceeded` metric.
 The alarm should trigger if the metric exceeds a threshold of 1.

4) Ensure Alerting: Configure the CloudWatch alarm to detect write throughput issues exceeding provisioned limits.

5) Create the `main.tf` file (do not create a separate `.tf` file) to provision the Kinesis stream, CloudWatch alarm, and ensure alerting.

6) Create the outputs.tf file with the following variable names to output:
```
kke_kinesis_stream_name for the Kinesis stream name.

kke_kinesis_alarm_name for the CloudWatch alarm name.
```

Notes:

The Terraform working directory is `/home/bob/terraform`.

Right-click under the `EXPLORER `section in `VS Code` and select `Open in Integrated Terminal` to launch the terminal.

Before submitting the task, ensure that `terraform plan` returns `No changes. Your infrastructure matches the configuration`.

## Answer:

Step01: Create main.tf file and added this content
```
resource "aws_kinesis_stream" "xfusion_stream" {
  name             = "xfusion-kinesis-stream"
  shard_count      = 1
  retention_period = 24

  shard_level_metrics = [
    "IncomingBytes",
    "IncomingRecords",
    "WriteProvisionedThroughputExceeded",
    "ReadProvisionedThroughputExceeded",
  ]
}

resource "aws_cloudwatch_metric_alarm" "xfusion_alarm" {
  alarm_name          = "xfusion-kinesis-alarm"
  comparison_operator = "GreaterThanThreshold"
  evaluation_periods  = 1
  metric_name         = "WriteProvisionedThroughputExceeded"
  namespace           = "AWS/Kinesis"
  period              = 60
  statistic           = "Sum"
  threshold           = 1

  dimensions = {
    StreamName = aws_kinesis_stream.xfusion_stream.name
  }
}

```
Step02: Create outputs.tf file and added this content 
```
output "kke_kinesis_stream_name" {
  value = aws_kinesis_stream.xfusion_stream.name
}

output "kke_kinesis_alarm_name" {
  value = aws_cloudwatch_metric_alarm.xfusion_alarm.alarm_name

```

Step03: Execute the terraform project
```
terraform init
terraform plan
terraform apply

```


### Task is Completed!




