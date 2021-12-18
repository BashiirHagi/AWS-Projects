# AWS-Projects: 
Hands on AWS Labs to enhance understanding of key AWS services: S3, VPC's, RDS, IAM, RDS, ECS, API Gateway

### Simple Storage Service - S3 :

AWS task to create S3 bucket & change bucket policy to public  

I clicked on S3 under Storage services

I created an S3 bucket in the us-east-1 (N.Virgina) region with a valid bucket name

I uploaded 2 separate object files to the S3 bucket via the AWS console  

I modified object permission to make the S3 bucket publicly accessible  

Changed bucket policy to: 

```
{ 
   "Id": "Policy1", 
   "Version": "2012-10-17", 
   "Statement": [ 
      { 
         "Sid": "Stmt1", 
         "Action": [ 
            "s3:GetObject" 
         ], 
         "Effect": "Allow", 
         "Resource": "arn:aws:s3:::mys3bucket-test 

/*", 
         "Principal": "*" 
      } 
   ] 
} 
```

I entered the bucket URL on the browser and the object files were now accessible


### Creating and Subscribing to SNS Topics, Adding SNS events to S3 bucket

I created a SNS topic by clicking on SNS > choosing standard topic and clicking on Create topic  

I created a S3 bucket  

I subscribed the S3 bucket to the SNS topic and chose my email as the endpoint – bashiir_20@hotmail.co.uk  

I then made an image upload to the S3 bucket triggering the SNS topic  

I received a notification via email about the S3 upload action


### Accessing an S3 bucket with an IAM role

I provisioned an EC2 isntance and attached the S3FullAccess IAM policy to it

I congiured the security group inound rules allowed SSH traffic to the instance


##### key commands:

chmod 400 S3keys.pem - to make SSH private key secure  

ssh -i S3keys.pem ec2-user@54.236.213.214 - to SSH into EC2 instance  

aws s3 ls - to list the S3 bucket  

Touch AWS.txt - to create text (.txt) file  

aws s3 mv AWS.txt s3://test-bucket - to move the text file to the S3 bucket


### Relational Database Service (RDS)

I clicked on Databases and then Relational Database services (RDS)

I provisioned a RDS MySQL database providing details such as name, login credentials, instance class and storage type 

I then installed MYSQL workbench on my local machine to use to connect to my cloud server 

I connected to the RDS database on AWS by using the DNS address and port no (3306) of the instance. 

I used the username and password configured during the database setup 

Successful connection was established to the RDS database


### Virtual Private Cloud (VPC) - public and private subnets

I created a VPC under Network & Content delivery services  

I then created a public and private subnet inside the VPC and assigned a IP address to them. 

I assigned the subnets to the VPC network 

I then created the internet gateway and attached it to the VPC

I then created a route table and connected the private and public subnets to it  

I added a route on the route table to allow traffic to the internet gateway (IGW) with target 0.0.0.0/0. Instances in the public and private subnet will be able to connect to the internet now. 



### CloudWatch for resource monitoring. created CloudWatch alarms and Dashboards

Create an EC2 Instance with Amazon Linux 2 AMI

I chose the default VPC, and configured security inbound rules with port 22 open for all hosts (0.0.0.0/0)

I laucned the instance and downloaded the private key file (.pem) to my local machine

I then SSH into the EC2 Instance and pefromed software instllations/updates

##### Key Commands: 
- sudo yum update -y
- sudo amazon-linux-extras install epel -y
- sudo yum install stress -y 


##### Created a SNS Topic
Navigated to the us-east-1 (N.Virginia) region

Then went to Simple Notification Service (SNS) under Application Integration services

Clicked on Topics and completed the details by providing a Type (standard), Nmae and Display name

Clicked on create topic


##### Subscribed to the SNS Topic
I went to the SNS topic I had just created by blicking the topic name

i then clicked on Create subscription

I then provided the SNS details - Topic ARN, Protocol (Email) and endpoint - bashiir_20hotmail.co.uk

I then clicked on Confirm subscription


##### Check EC2 CPU Utilization Metrics in CloudWatch Metrics
I navigated to Cloudwatch services under Management & Governance service

Clicked on All Metrics on the left-hand panel

The metrics were now visible for the EC2 instance I provisioned 


##### Create CloudWatch Alarm

I navigated to Cloudwatch services under Management & Governance service
I clicked on Alarms on the left-hand panel
I then clicked on Create alarm to begin provisioning the alarm
In the specify metric & conditons page I: 

- Clicked on select metric > EC2 
- selected Per-Instance Metrics
- Chose the CPU-Utilization metric

I then configured the arm with the following details:
For metric period I selected for 1 minute
For CPU Utilization I selected Choose Greater
Valiue: 30

In the configure actions page under the Notifications page: 
- I chose In Alarm as the Alarm state trigger 
- Selected my SNS topic for SNS topic

In the Add a description page I entered a unique name - MyServerCPUUtilizationAlarm

I then clicked on review my alarm before creating it. 

I finaly clicked on - Create Alarm to launch the CloudWatch Alarm. 


##### Testing CloudWatch Alarm by Stressing CPU Utilization. 

##### Checking For an Email from the SNS Topic. 

##### Checking the CloudWatch Alarm Graph 

##### Create a CloudWatch Dashboard. 



 



 
