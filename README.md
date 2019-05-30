# Monitoring EC2 with Unified CloudWatch Agent
> A Cloudformation script in the form of nested stacks that deploys an instance on which CloudWatch Alarms, Custom Metrics and Event rules are configured. The alarms are then sent to an SNS Topic which has an SQS Queue as its endpoint.
## Features:
```
Stream logs to CloudWatch Logs
Setup Custom Metrics on CloudWatch
Send CloudWatch Alarms to SNS Topic
```
## Setup
The infrastructure consists of three nested stacks. Each stack is explained in detail as follows:

### VPC
Being the first stack, it includes the resources necessary for setting up a Virtual Private Cloud (VPC). The VPC is completely customizable and consists of all the necessary parameters.

### Instances
This stack is dependent on the VPC stack. In this stack, an instance is launched in which the Unified CloudWatch Agent will be installed at it's launch. The agent will be configured to stream logs to CoudWatch Logs and setup some custom metrics defined in the cloudwatchagent-linux-config.json file (you can use your own configuration by giving it the download link to your file in the user data bash script).

### CloudWatch Alarms
This stack applies some basic alarms. You can choose any instance in the parameters on which you want to apply the alarms. An SNS Topic has also been created on which are alarms will be sent. The SNS Topic has an SQS Queue as its endpoint.
