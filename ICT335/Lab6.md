# ICT335 Virtual Lab 6: Build a Web Application with Elastic Beanstalk

## Lab Overview
In this lab, we will create a Web Application with Elastic Beanstalk.

This lab will reuse the VPC and MySQL database from the previous labs.

The architecture is illustrated in the following diagram.  
![](images/Lab6-Arch.png)

## Lab Task Outline
### 1. Prepare MySQL to Allow Public Access
The MySQL database created in lab 3 only allows private access in VPC, we need to reconfigure it to allow public access from free tier Beanstalk application.
- Choose __RDS__, select *database-1*, start it
  - __Modify__, in __Connectivity__, select __Additional configuration__. Enable __Publicly accessible__, __Continue__, and complete the modification (Choose __Continue__, then __Modify DB instance__)
- Choose __VPC__, in __Route Tables__, perform the following configuration for both *lab-rtb-private2-us-east-1b* and *lab-rtb-private3-us-east-1c*
  - __Edit routes__, __Add route__ with the following attributes, __Save changes__
    - Destination: `0.0.0.0/0`
    - Target: *Internet Gateway*, choose the only record

### 2. Build the Web Application Package
- The web application package [eb-azurevote.zip](https://github.com/ningweinw/ningweinw.github.io/raw/master/ICT335/scripts/eb-azurevote.zip) for Elastic Beanstalk has been provided

### 3. [Optional] Test Web Application Locally
Reference [Deploying a flask application to Elastic Beanstalk](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create-deploy-python-flask.html), set up the Python development environment and run the application locally.

Before running the application, set the required environment variables:
```
export MYSQL_USER=admin
export MYSQL_PASSWORD=<MYSQL_PASSWORD>
export MYSQL_HOST=<MYSQL_HOST>
```

### 4. Deploy the Web Application
- Choose __Elastic Beanstalk__, __Create Application__ with the name: `lab-eb`
- __Platform__: *Python*
- __Upload your code__: *eb-azurevote.zip* downloaded in task 2
- __Configure more options__
    - In the __Software__ panel, __Edit__, create the following __Environment properties__, and __Save__
      - `MYSQL_USER` = `admin`
      - `MYSQL_PASSWORD` = \<MYSQL_PASSWORD\>
      - `MYSQL_HOST` = \<MYSQL_HOST\>
    - In the __Security__ panel, __Edit__
      - For Service role, choose *LabRole*
      - If the environment is in the us-east-1 AWS Region, for EC2 key pair, choose *vockey*
      - For IAM instance profile, choose *LabInstanceProfile*
      - __Save__
- __Create app__
- The Elastic Beanstalk application and environment will be created. When the environment *LabEb-env* is ready, click __Go to environment__, the web application will display.


## Lab Cleanup
- Delete the Beanstalk application
- Delete the database
