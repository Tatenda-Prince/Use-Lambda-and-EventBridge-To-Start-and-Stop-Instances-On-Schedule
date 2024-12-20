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

![imagr alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/308979191b655372eaf5f3d395badf87008bc510/Screenshot%202024-12-19%20203639.png)

Click “Create policy”, then select the “JSON” table to edit the policy. Copy and paste the JSON policy below in the policy box, then click “Next:Tags”

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/7ef95345b9d53aa3ab5ea8792d9c1f6e83dc46ad/Screenshot%202024-12-19%20202513.png)

Continue by clicking “Next: Review”. Name the policy, then click “Create policy”.

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/7bee3bd21fc28bd95b19f40b9593cda3412b9c48/Screenshot%202024-12-19%20202821.png)

Head back to create the role. Make sure to refresh the policies to include the new policy just created. Now search for the policy, select it, then click “Next:Tags”.

Continue to “Review”. Name and describe the role, then click “Create role”.

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/6700f376bd53ed566467bbd1f3b375f51710912f/Screenshot%202024-12-19%20203156.png)

Head back to the Lambda’s “Create function” window. Refresh the existing roles, select the role previously created, then click “Create Function”.

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/308979191b655372eaf5f3d395badf87008bc510/Screenshot%202024-12-19%20203639.png)

# Step 2: Deploy and Test Lambda Function
This code uses the “boto3” Python library to interact with AWS services. In the “lambda_handler” function, we loop through all Instances to get their current state and tags.

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/e5c65fdcec12a5957765919bcf2a19f46cff6305/Screenshot%202024-12-19%20204150.png)

Next, we will click “Deploy” to deploy the function’s code to the Lambda service, then click “Test” to test out the function based on a test case.

For “Test event action”, select “Create a new event”, then name the event. We can use the JSON code below to test our Lambda function.

Click “Save” to save the Test event.

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/ffb84c76794c7ea3ce9a5793a018008994354632/Screenshot%202024-12-19%20204330.png)

We can now test our function by clicking ‘Test”. A “success” response, along with other details from the function execution in the function logs should display in the “Executing results” tab.

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/205a7e8ce3180956b0454f228970de5d1ad39538/Screenshot%202024-12-19%20205012.png)

Our Instance has been successfully stopped using a lambda function as you can see below:

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/d4e598e1a070958dff1021caf16309992c02395c/Screenshot%202024-12-19%20205153.png)

Now that we have managed stop our EC2 instance are going to create another lambda function to start our previously stopped instance.

![image alt]( )


Now that we’ve set up and created our Lambda function and also tested its successful functionality, we can now proceed to Step 3 — Using EventBridge to schedule our function to run at a set time of the day and days of the week.







 






