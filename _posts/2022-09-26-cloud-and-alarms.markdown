---
title:  "Cloud And Alarms"
subtitle: "Scaling by CloudWatch Alarms "
author: "Lib"
avatar: "img/authors/wferr.png"
image: "img/d.jpg"
date:   2022-09-26 12:12:12
---

<p style="font-size: 15px;">Dedicated to all beginners very curious because you will have .many doubts at the end.
sincerely lib</p>

### Previous requirements

- AWS Coung 
- Ec2 
- CloudWatch

## SQS


why we use SQS?

Because is a message service queue.


## Steps

Create traffic request for an instance 

[script](https://github.com/libialany/aws-notas/blob/main/SQS/send_messages.py)

Create scale-out and scale-in alarms using SQS 

Go to CloudWatch> Alarms>Create alarm

The metric to choose is: ApproximateNumberOfMessagesVisible metric.

Settings are: 

> scale-in to get activated 

Conditions:
Greater 500 messages but it has to check every minute.

> scale-out to get activated 

Conditions:
Lower 400 messages but it has to check every minute.

Observe the Auto Scaling Group's 

Create Autoscalings Groups

Go to EC2>Auto Scaling Groups>EC2 Autoscaling Group.

Type is: Simple Scaling 
Scaling Policy Name : Scale In/out# you have to choose one

Take action:
Add/remove 1 instance and then wait 60 seconds # you have to choose one

You need to create 2 Auto Scaling Group's.


### Conclusion

Improve a service app by setting alarms and policies.

Next Lab: Creating an Auto Scaling Group and Application Load Balancer in AWS

🤪