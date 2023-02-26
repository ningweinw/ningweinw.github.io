# ICT335 Virtual Lab 5: Build a Load Balanced Web Application with Elastic Load Balancing

## Lab Overview
In this lab, we will create a load balanced Web Application with Elastic Network Load Balancer

This lab will reuse the VPC, EC2 launch template and MySQL database from the previous labs.

The architecture is illustrated in the following diagram.  
![](images/Lab5-Arch.png)

## Lab Task Outline
### 1. Preparation
- Start the database

### 2. Create Two Web Servers
- Choose __EC2__ service, __Launch template__, select *lab-ubuntu-template*
- __Actions__, __Launch instance from template__ with the following settings:
  - Number of instances: `2`
  - Network settings: choose *lab-subnet-public1-us-east-1a*
- Two EC2 instances are created
- For each instance, verify the web application URL works: `http://<EC2_DNS_Name>:8080`

### 3. Create Network Load Balancer
- Choose __Load Balancers__, __Create Load Balancer__, select __Network Load Balancer__
  - Name: `lab-lb`
  - Scheme: *internet-facing*
  - Network mapping: select *lab-vpc* and *us-east-1a*, the *lab-subnet-public1-us-east-1a* will be selected automatically
  - Listeners: keep the default listener on TCP port 80
  - Click __Create target group__
    - New target group: `lab-lb-tg`
    - Port: `8080`
    - Advanced health check settings: change interval to *10 seconds*
    - __Next: Register Targets__. Choose both instances, __Include as pending below__
    - __Create target group__
  - Back in the load balancer creation wizard, click the refresh button next to the target group list, select the newly created target group
  - __Create load balancer__
- After *lab-lb* is created, in the __Listeners__ tab, click the target group *lab-lb-tg*
  - In the __Targets__ tab, wait for both instances to show *healthy* status
- Back to the load balancer *lab-lb*, find the DNS, visit the URL `http://<LB_DNS>` and the web application homepage is displayed
- Refresh the URL a few times, observe the host name display changes between the two EC2 instances

### 4. Add One More Web Server to Load Balancer
- Create a new EC2 instance using the launch template *lab-ubuntu-template*. Refer to step #2
- Wait for the new EC2 instance to complete initialization, verify the web application URL on this instance
- Choose the target group *lab-lb-tg*
  - Under __Targets__, click __Register targets__
  - Under __Available instances__, select the newly created EC2 instance, click __Include as pending below__
  - Click __Register pending targets__
- Wait for the __Health status__ of the newly added EC2 instance turns to *healthy*
- Visit the URL `http://<LB_DNS>`, refresh the URL a few times, observe the host name display changes between the three EC2 instances

### 5. Change Web Server State
- Stop one EC2 instance
  - In target group *lab-lb-tg*, observe the target __Health status__. Notice the delay before the staus of the stopped instance changes to *unhealthy*
  - Refresh the load balancer URL, observe the result
- Start the same EC2 instance. Wait for its __Status check__ to complete.
  - In target group *lab-lb-tg*, observe the target __Health status__
  - Refresh the load balancer URL, observe the result

## Lab Cleanup
- Delete the load balancer and target group
- Terminate all EC2 instances
- Stop the database
