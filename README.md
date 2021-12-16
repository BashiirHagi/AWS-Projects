# AWS-Projects-
Hands on AWS Labs to enhance understanding of key services: S3, VPC's, RDS, IAM, RDS, ECS, API Gateway

## Simple Storage Service - S3 :

Clicked S3 under Storage services

Created an S3 bucket in the us-east-1 (N.Virgina) region

Upload 2 separate object files  

Modified object permission to make the S3 bucket public  

Changed bucket policy to public to : 

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

Tested public object by uploading a file  
