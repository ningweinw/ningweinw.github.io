# ICT335 Virtual Lab 1: AWS Academy Overview, Build a Static Website with Simple Storage Service (S3)

## Lab Overview
In this lab, we will first have an overview of the AWS Academy, and then create a static website using the Simple Storage Service (S3).

## Lab Task Outline
### 1. AWS Academy
- Sign in on [AWS Academy](https://www.awsacademy.com/LMS_Login)
- Locate and choose course: __AWS Academy Learner Lab - Foundation Services [13164]__
- Browse the modules, read the Student Guide on how to use the lab environment
- Click module __Learner Lab - Foundational Services__, get familiar with the layout
- Click __Start Lab__
- After the lab is started, click __AWS__ to access the AWS console

![image](https://user-images.githubusercontent.com/43491290/149454038-2dc880e8-d469-44c9-8800-abd8a34414e1.png)

### 2. Build a Static Website with Simple Storage Service (S3)
The architecture is illustrated in the following diagram.  
![](images/Lab1-Arch.png)
  - Choose __S3__ service, __Create bucket__
  - Select the newly created bucket, enable __Static website hosting__ in __Properties__ tab
    - Enter `index.html` for __Index document__ and `error.html` for __Error document__
  - Download the [zip file](http://tinyurl.com/s3static) containing the static website files, unzip, and __Upload__ the two files to the bucket
  - Select object *index.html*, try to access the static website using __Object URL__, observe the access error
  - Enable public access
    - Review __Account settings for Block Public Access__
    - Uncheck __Block all public access__ in bucket's __Permissions__ tab
    - In bucket's __Objects__ tab, select both objects, click __Action__ and select __Make public__
    - Review the ACL settings in each object's __Permissions__ tab
  - Try to access the static website again, the webpage displays successfully

## Lab Cleanup
- Delete all the objects in the S3 bucket
- Keep the bucket for the future labs
