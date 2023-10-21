# ICT335 Virtual Lab 2: Build a Virtual Private Cloud (VPC) and Elastic Compute Cloud (EC2) Instance

## Lab Overview
In this lab, we will create a Virtual Private Cloud (VPC) and review its configuration. We will then create a Windows server using the Elastic Compute Cloud (EC2) instance and RDP into it.

The architecture is illustrated in the following diagram.  
![](images/Lab2-Arch.png)

## Lab Task Outline
### 1. Build a Virtual Private Cloud (VPC)
- Choose __VPC__ service, __Create VPC__
  - Select __VPC and more__
  - Under __Auto-generate__, enter VPC prefix: `lab`
  - Under __Number of Availability Zones (AZs)__, select `3`
  - Under __Number of public subnets__, select `3`
  - Under __Number of private subnets__, select `3`
  - Under __NAT gateways__, select `None`
  - Under __VPC endpoints__, select `None`
  - Create VPC
- Review the newly created VPC and its configuration
  - Review the public and private subnets, and their associated route tables
  - Review the routes in the route tables, and the route targets
- In the subnet list, choose *lab-subnet-public1-us-east-1a*, click __Actions__, and __Edit subnet settings__, check __Enable auto-assign public IPv4 address__, __Save__

### 2. Delete unused public subnets
- Choose __VPC__ service, __Subnets__, sort the table by __VPC__ column
- Check *lab-subnet-public2-us-east-1b* and *lab-subnet-public3-us-east-1c*
- Under __Actions__ menu, choose __Delete subnet__
- Ignore the error message, confirm deletion, click __Delete__

### 3. Create a Windows Server
- Choose __EC2__ service, __Create security group__, with the name of `labvm-sg`. Provide a description, choose VPC: *lab-vpc*. Add the following inboud rules:
  - Type: __SSH__, Source: __Anywhere-IPv4__
  - Type: __RDP__, Source: __Anywhere-IPv4__
  - Type: __HTTP__, Source: __Anywhere-IPv4__
  - Type: __Custom TCP__, Port range: `8080`, Source: __Anywhere-IPv4__
- Choose __EC2__ service, __Launch instance__
  - Provide a name: *lab-vm-win-1*
  - Search "windows server 2019", select __Microsoft Windows Server 2019 Base__
  - Select __t2.micro__
  - __Create new key pair__ with the name of `labvm-key`. Take note of the `labvm-key.pem` file that gets downloaded automatically. __Important:__ Keep this file for future labs
  - Edit __Network settings__, select VPC: *lab-vpc*, subnet: *lab-subnet-public1-us-east-1a*
  - Select the existing security group: *labvm-sg*
  - __Launch instance__
- Select the newly created EC2 instance, __Connect__
- Choose __RDP client__ and select __Get password__. Click __Browse__ and select the key file downloaded in the previous step. __Decrypt Password__ and note down the password
- __Download remote desktop file__, open it and login when prompted

## Lab Cleanup
- Terminate the EC2 instance
- Keep the VPC, security group and key pair for the next lab
