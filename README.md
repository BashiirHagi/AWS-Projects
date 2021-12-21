# AWS-Projects:  

Hands on AWS Labs to enhance understanding of key AWS services: S3, VPC's, RDS, IAM, RDS, ECS, API Gateway 

  

### Simple Storage Service - S3 : 

  

#### AWS task to create a S3 bucket & change the bucket policy to public   

  

Navigate to the us-east-1 (N.Virginia) region on the AWS console 

  

Click on S3 under Storage services 

  

Create a S3 bucket with a valid bucket name - e.g. myS3bucket-test 

  

#### Upload 2 separate object files to the S3 bucket via the AWS console  

Create bucket > Upload > Add files > Select file from local machine  

  

  

  

#### Change S3 bucket policy to public:  

  

Modify bucket permission to make the S3 bucket files publicly accessible   

  

Paste the below bucket policy under Permmissions > Bucket policy  

``` 

{ 

    "Version": "2012-10-17", 

    "Id": "Policy1635321416121", 

    "Statement": [ 

        { 

            "Sid": "Stmt1635321403959", 

            "Effect": "Allow", 

            "Principal": "*", 

            "Action": "s3:GetObject", 

            "Resource": "arn:aws:s3:::myS3bucket-test/*" 

        } 

    ] 

} 

  
``` 

  

Enter the bucket URL on the browser and the object files are now publicly accessible  


All future S3 file uploads will become public now  

  
  

### Creating and Subscribing to SNS Topics, Adding SNS events to S3 buckets 

#### AWS task to create a SNS topic and subscribing to a S3 bucket event 

  
#### create the SNS topic 
Navigate to the us-east-1 (N.Virginia) region on the AWS console 

Click on Simple Notification services under Application Integration services 

Create a SNS topic by choosing a topic name > choosing standard topic and clicking on Create topic   

The SNS topic has now been created
  


#### Subscribe to the SNS topic 

Click the SNS topic you just created 
Click on Create subscription

Subscription configuration: 
Protocol: Email
Endpoint: Enter your email address 

You will receive an email confirming the subscription to your email 

Click on the email from AWS and click on Confirm Subscription 


#### Create a S3 bucket 

Go to S3 under Storage services

Create a S3 bucket - mytestbucket 

Object ownership: Select ACLs disabled 

Keep other settings as default

Click Create bucket

Save and make a copy of the Amazon Resource Name (ARN)


#### Update the SNS topic Access Ppolicy: 

Navigate to the SNS service

Click on Topics in the left-hand panel

Click on the existing SNS topic

Click Edit > Access Policy 

Enter the SNS topic ARN in the resource section below 

Enter the S3 bucket ARN in the condition section below


``` 

{
  "Version": "2008-10-17",
  "Id": "__default_policy_ID",
  "Statement": [
    {
      "Sid": "__default_statement_ID",
      "Effect": "Allow",
      "Principal": {
        "AWS": "*"
      },
      "Action": [
        "SNS:GetTopicAttributes",
        "SNS:SetTopicAttributes",
        "SNS:AddPermission",
        "SNS:RemovePermission",
        "SNS:DeleteTopic",
        "SNS:Subscribe",
        "SNS:ListSubscriptionsByTopic",
        "SNS:Publish",
        "SNS:Receive"
      ],
      "Resource": "<Your_SNS_Topic_ARN>",
      "Condition": {
        "ArnLike": {
          "aws:SourceArn": "<Your_Bucket_ARN>"
        }
      }
    }
  ]
}

``` 

Click Save changes

  
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

  

Created an EC2 Instance with Amazon Linux 2 AMI 

  

I chose the default VPC, and configured the security inbound rules with port 22 open for all hosts (0.0.0.0/0) 

  

I launched the instance and downloaded the private key file (.pem) to my local machine 

  

I then connected to my EC2 Instance using SSH and performed software installations/updates 

  

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

  

I finally clicked on - Create Alarm to launch the CloudWatch Alarm.  

  

  

  

##### Checking the CloudWatch Alarm Graph 

  

I navigated to the CloudWatch page and clicked on Alarms 

  

I was now able to visualise the alarm I created for CPU Utlization 

  

  

##### Created a CloudWatch Dashboard  

  

I navigated to CloudWatch page and clicked on Dashboard on the left-hand panel  

  

I then clicked on Create Dashboard and provided the following details:  

  

Dashboard name - MyEC2ServerDashboard 

Widget type - Selected Line Graph 

Data Source - Selected Metrics 

Metrics - EC2 > Per-instance Metrics  

  

Clicked on Create Widget and Save dashboard to create the Cloudwatch dashboard 

  

  

### Resizing EBS Volumes for a linux Instance 

  

I provisioned an EC2 Linux instance in the us-east-1 (N.Virginia) region  

  

I configure the storage drive to be – 8GB SSD gp2  

  

I configured the security group inbound rules to allow SSH traffic from all hosts (0.0.0.0/0)  

  

I then launched the downloaded the private key file and laucnhed the instance  

  

#### Modifiying the storage volume  

  

I clicked on the instance storage volume ID - vol-0ef30a3c405ac4606 

I then clicked on Actions > Modify volume  

I increased the Size (GiB) to 20GB and clicked on Modify  

  

Checking the instance volume size  

I connected to the instance using SSH  

I ran the command df-h to check the free disk space and it showed 20GB 

  

  

  

  

  

  

  

  

  

  

 
