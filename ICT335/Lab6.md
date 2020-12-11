# ICT335 Virtual Lab 6: Build a Web Application with Elastic Beanstalk

## Lab Overview
In this lab, we will create a Web Application with Elastic Beanstalk.

This lab will reuse the VPC and MySQL database from the previous labs.

The architecture is illustrated in the following diagram.  
![](images/Lab6-Arch.png)

## Lab Task Outline
### 1. Prepare MySQL to Allow Public Access
The MySQL database created in lab 3 only allows private access in VPC, we need to reconfigure it to allow public access from free tier Beanstalk application.
- Choose __RDS__, select *database-1*, __Modify__
  - In __Connectivity__, select __Additional configuration__. Enable __Publicly accessible__, __Continue__, and complete the modification
- Choose __VPC__, in __Route Tables__, choose the main subnet (with __Main__ column showing *Yes*) of *lab-vpc*
  - __Edit routes__, __Add route__ with the following attributes:
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

## Lab Cleanup
- Delete the Beanstalk application
