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

By default, it spans two availability zones creating one public subnet and one private subnet in one AZ and an other public subnet in the other AZ. The public subnets are connected to the internet through an internet Gateway and and the private subn<a href=""></a>et is connected to the internet through a Nat Gateway that is connected to one of the public subnets. No inbound traffic is allowed to the private subnet, except through the public subnet (this purpose was achieved through necessary security groups).

### Instances
This stack is dependent on the VPC stack. In this stack, an instance is launched in which the Unified CloudWatch Agent will be installed at it's launch. The agent will be configured to stream logs to CoudWatch Logs and setup some custom metrics defined in the cloudwatchagent-linux-config.json file (you can use your own configuration by giving it the download link to your file in the user data bash script).

### CloudWatch Alarms
This stack applies some basic alarms. You can choose any instance in the parameters on which you want to apply the alarms. An SNS Topic has also been created on which are alarms will be sent. The SNS Topic has an SQS Queue as its endpoint.
