# AWS-Projects: 
Hands on AWS Labs to enhance understanding of key AWS services: S3, VPC's, RDS, IAM, RDS, ECS, API Gateway

## Simple Storage Service - S3 :

AWS task to create S3 bucket & change bucket policy to public  

I clicked on S3 under Storage services

I created an S3 bucket in the us-east-1 (N.Virgina) region with a valid bucket name

I uploaded 2 separate object files to the S3 bucket via the AWS console  

I modified object permission to make the S3 bucket publicly accessible  

Changed bucket policy to public to : 

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


## Accessing an S3 bucket with an IAM role

I provisioned an EC2 isntance and attached the S3FullAccess IAM policy to it

I congiured the security group inound rules allowed SSH traffic to the instance


key commands:

chmod 400 S3keys.pem - to make SSH private key secure  

ssh -i S3keys.pem ec2-user@54.236.213.214 - to SSH into EC2 instance  

aws s3 ls - to list the S3 bucket  

Touch AWS.txt - create txt file  

aws s3 mv AWS.txt s3://tes-bucket - to move txt file to S3 bucket  




 
