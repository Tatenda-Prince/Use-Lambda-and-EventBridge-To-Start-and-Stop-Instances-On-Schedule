# Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule

# Intro 
Boto3 is a Python library for interacting with Amazon Web Services that can be used to improve your skills in automation processes to increase efficiency.

Boto3 is a game changer, allowing you to automate tasks, build custom scripts and manage AWS resources from the command line. Its comprehensive API support for various AWS services has made it easy to integrate Python scripts with AWS.

Today we will create a Lambda function that uses the Boto3 library to automate the task of stopping specific EC2 Instances. The Lambda function would be triggered by a Amazon EventBridge Schedule, which will schedule the function to run at a specific time each day.

# Background
Boto3 provides a Python API for AWS infrastructure services. Using the SDK for Python, you can directly create, update and delete AWS resources using Python scripts.

# AWS Lambda
Lambda is a serverless compute service that runs your code as functions in response to events and automatically manages the underlying compute resources for you.

# AWS EventBridge
EventBridge is also a serverlesss event bus service that makes it easy to connect your applications with data from a variety of sources. It can be used to build an application that reacts to events from SaaS applications, AWS services or Custom applications.

# Use Case
Your DevOps engineering team at TATENDA TECH often uses a development lab to test releases of our application. Your Managers are complaining about the rising cost of the development lab and need to save money by stopping the (for this example) 3 EC2 Instances after all engineers have clocked out.

You need to ensure that only the Development Instances are stopped and make sure nothing in Production is interfered with. We only need to stop running Instances that have the “Environment: Dev” tag.

You’ve decided to use a Lambda function using the Python runtime with EventBridge to schedule the function to run at 7am daily in the morning as no one should be working in the Dev environment until past 5pm in the evening.

# Step 1: Set up Lambda Function and IAM Role
![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/d83384496383f22a3e8901ec3e18497103040e13/Screenshot%202024-12-19%20120614.png)

Select “Author from scratch”, name the function, then choose Python 3.7 or greater Runtime.

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/708d80e0427011d1fe12e747ef407aa4396ee7ef/Screenshot%202024-12-19%20203618.png)

You will then change the default execution role and use an exiting role. To create this role select “IAM Console”.

![imagr alt]()

Click “Create policy”, then select the “JSON” table to edit the policy. Copy and paste the JSON policy below in the policy box, then click “Next:Tags”

![image alt]()





