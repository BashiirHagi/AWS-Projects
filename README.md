# AWS-Projects: 
Hands on AWS Labs to enhance understanding of key AWS services: S3, VPC's, RDS, IAM, RDS, ECS, API Gateway

## Simple Storage Service - S3 :

AWS Lab to create S3 bucket & change bucket policy to public  

Clicked on S3 under Storage services

Created an S3 bucket in the us-east-1 (N.Virgina) region with a valid bucket name

Uploaded 2 separate object files to the S3 bucket via the console  

Modified object permission to make the S3 bucket publicly accessible  

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

Entered the bucket URL on browser and the object files were accessible 
