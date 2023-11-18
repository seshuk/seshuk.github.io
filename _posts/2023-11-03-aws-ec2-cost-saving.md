---
layout: post
title: "Shutdown EC2 instances in ASG instead of terminate"
subtitle: "Cloud Cost optimization"
categories: ["Cost Optimisation", "AWS", "Lambda"]
tags:
  - AWS
  - Cost Optimisation
  - Automation
  - Serverless
---

One of the ways to optimize your cloud spending is to shut down EC2 instances that are not in use, especially in non-production environments such as development, testing, or staging. This can save you a significant amount of money on your AWS bill, as you only pay for the resources that you need.

This is especially complicated when an autoscaling group is used to manage the instances. When you scale down the group, the instances are terminated and replaced with new ones when needed. This ensures that you always have the right number of instances running, but it also means that you lose any data stored on the instances when they are terminated. If you want to keep the data and relevant software that is already installed on the instances, you need to manually back it up before terminating the instances.

As such this adds a bit of complexity to the process of shutting down and starting up EC2 instances. Also, manually shutting down and starting up EC2 instances can be tedious and error-prone. A better solution is to automate this process using AWS Lambda, a serverless computing service that lets you run code without provisioning or managing servers.

In this blog post, I will show you how to create a simple Lambda function that shuts down EC2 instances in an autoscaling group at night and starts them up in the morning, based on a predefined schedule. You will also learn how to use CloudWatch Events to trigger the Lambda function at the desired times.

Here are the steps:

1. Create an IAM role for the Lambda function. The role needs to have permissions to list, stop, and start EC2 instances and interact with auto-scaling groups.

2. Create a Lambda function using Python as the runtime. The sample code for the function is shown below. It takes an event parameter that specifies the desired action (`stop` or `start`). The function then iterates over the instances in the auto-scaling group and acts on them.

```python
    asg = boto3.client('autoscaling')
    ec2 = boto3.client('ec2')
    auto_scaling_group_name = 'your-auto-scaling-group'
    # Get the instances in the Auto Scaling group
    response = asg.describe_auto_scaling_groups(
        AutoScalingGroupNames=[auto_scaling_group_name]
    )
    instances = response['AutoScalingGroups'][0]['Instances']
    instance_ids = [instance['InstanceId'] for instance in instances]

    if event['action'] == 'stop':
        # Suspend ReplaceUnhealthy process
        asg.suspend_processes(
            AutoScalingGroupName='your-auto-scaling-group',
            ScalingProcesses=[
                'ReplaceUnhealthy',
            ]
        )
        # Stop instances
        ec2.stop_instances(
            InstanceIds=instance_ids
        )
    elif event['action'] == 'start':
        # Start instances
        ec2.start_instances(
            InstanceIds=instance_ids
        )

        # Resume ReplaceUnhealthy process
        asg.resume_processes(
            AutoScalingGroupName='your-auto-scaling-group',
            ScalingProcesses=[
                'ReplaceUnhealthy',
            ]
        )
```

3. Create two CloudWatch Events rules, one for stopping and one for starting the EC2 instances. You can use cron expressions to define the schedule for each rule. For example, you can use `0 0 * * *` to run the rule every day at midnight UTC, or `0 8 * * 1-5` to run the rule every weekday at 8 AM UTC. For each rule, you need to specify the Lambda function as the target and pass the appropriate event parameter as the input.
4. Test and monitor your Lambda function and CloudWatch Events rules. You can use the CloudWatch console or the AWS CLI to check the logs and metrics of your function and rules. You can also use the AWS CLI to test your function locally before deploying it to AWS.

By following these steps, you can easily automate the shutdown and startup of EC2 instances in non-production environments using AWS Lambda and CloudWatch Events. This will help you reduce your cloud costs and improve your operational efficiency.
