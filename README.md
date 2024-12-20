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
This code uses the “boto3” Python library to interact with AWS services. In the “lambda_handler” function, So that we are able stop our running Instance.

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

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/760c685a2b4fa7fc5d197c77b368978adc7460ef/Screenshot%202024-12-19%20205355.png )

Next, we will click “Deploy” to deploy the function’s code to the Lambda service.

![images alt]( https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/ea9dd31771b0a2c323d753657003f7266f1a53bf/Screenshot%202024-12-19%20205655.png)

For “Test event action”, select “Create a new event”, then name the event. We can use the JSON code below to test our Lambda function.

Click “Save” to save the Test event.

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/720474360da34b4baca36e016969813ecc3e7ff2/Screenshot%202024-12-19%20205738.png )

The second test ran successfully and as you can see below our Instance was sterted up again using a lambda function.

![image alt]( https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/b5973f73c3aedc7fa7b0a1786b16327566484a47/Screenshot%202024-12-19%20205756.png)

Now that we’ve set up and created our Lambda function and also tested its successful functionality, we can now proceed to Step 3 — Using EventBridge to schedule our function to run at a set time of the day and days of the week.

# Step 3: Create an EventBridge Schedule to schedule the Lambda function

Navigate to EventBridge, select “EventBridge Schedule” then click “Create Rule”.

Name and describe (optional) your schedule and set “Schedule group” to default.

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/f18ebbc57eca4b586cf4556f8ed0226858785c3d/Screenshot%202024-12-19%20211010.png)

The Trigger start-server-mornning was successfully added to function start-EC2-Instance.The Function is now receiving event from the trigger.

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/1e1d7672bfda0fad6cddebec39e630be517c0010/Screenshot%202024-12-19%20211035.png)

We are going to create another event for Stop-EC2-Instance

![image alt]( https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/766610a43ad0a1181a8d7049578bae2d9adace1e/Screenshot%202024-12-19%20211838.png)

The Trigger Stop-EC2-Instance was successfully added to function Stop-EC2-Instance.The Function is now receiving event from the trigger.

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/e6cd10c30aadb2c3753aa6ed6093b2f2fb705086/Screenshot%202024-12-19%20211900.png)

Now we can check our rule by navigating to cloudwatch under Events we can see both our rules that we created.

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/e6cd10c30aadb2c3753aa6ed6093b2f2fb705086/Screenshot%202024-12-19%20211900.png)

# Success!
You’ve successful created a Lambda function that stops all Development EC2 Instances and integrated it with Amazon EventBridge to schedule the function to run at a specified time.

# More Insights

In your Lambda Function, select the “Monitor” tab, then click “View CloudWatch logs”.

in the CloudWatch window, you should see that the last event log stream’s “last event time” matches with the time we set from EventBridge, which was the last time the Lambda function was invoked.

Further more, if you select the Lambda function’s log stream, you can see more detailed information when the Lambda function was executed.

![imaged](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/498ccddbeb0bb9d3c66b50ee28c1dc20d10522b4/Screenshot%202024-12-19%20213440.png)

![image alt](https://github.com/Tatenda-Prince/Use-Lambda-and-EventBridge-To-Start-and-Stop-Instances-On-Schedule/blob/46f59aba8076d532426bbcc4602e1cd2add6d185/Screenshot%202024-12-19%20213821.png )

# Congratulations!
You’ve reached the end. You’ve created a Lambda function triggered by an Amazon EventBridge schedule, which schedules the function to run at a specific time each day.
















 






