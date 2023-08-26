# ICT335 Virtual Lab 1: AWS Academy Overview, Build a Static Website with Simple Storage Service (S3)

## Lab Overview
In this lab, we will first have an overview of the AWS Academy, and then create a static website using the Simple Storage Service (S3).
### Walk through all lab scenarios

## Lab Task Outline
### 1. AWS Academy
- Sign in on [AWS Academy](https://www.awsacademy.com/vforcesite/LMS_Login)
- Locate and choose course: __AWS Academy Learner Lab [53194]__
- Browse the modules, read the Student Guide on how to use the lab environment
- Click module __Learner Lab__, get familiar with the layout
- Click __Start Lab__
- After the lab is started, click __AWS__ to access the AWS console

![image](https://user-images.githubusercontent.com/43491290/149454038-2dc880e8-d469-44c9-8800-abd8a34414e1.png)

### 2. Build a Static Website with Simple Storage Service (S3)
The architecture is illustrated in the following diagram.  
![](images/Lab1-Arch.png)
  - Choose __S3__ service, __Create bucket__
    - Keep the default *us-east-1* region
    - Uncheck __Block all public access__
    - Check the acknowledgement
  - Select the newly created bucket, enable __Static website hosting__ in __Properties__ tab
    - Enter `index.html` for __Index document__ and `error.html` for __Error document__
  - Download the [zip file](https://github.com/ningweinw/ningweinw.github.io/raw/master/ICT335/scripts/AWSEducateS3.zip) containing the static website files, unzip, and __Upload__ the two files to the bucket
    - Under __Properties__ -> __Tags__, add the following tag: key=*public*, value=*yes*
  - Select object *index.html*, try to access the static website using __Object URL__, observe the access error
  - Enable public access. In bucket's __Permissions__ tab -> __Bucket policy__, click __Edit__, enter the following policy, replace *<Bucket_Name>* with the name of the newly created S3 bucket, __Save changes__.
  ```
  {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Principal": "*",
        "Action": "s3:GetObject",
        "Resource": "arn:aws:s3:::<Bucket_Name>/*",
        "Condition": {
          "StringEquals": {
            "s3:ExistingObjectTag/public": "yes"
          }
        }
      }
    ]
  } 
  ```
  - Try to access the static website again, the webpage displays successfully

## Lab Cleanup
- Delete all the objects in the S3 bucket
- Keep the bucket for the future labs
