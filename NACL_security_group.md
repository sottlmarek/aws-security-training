# Understanding and Practicing with NACLs and Security Groups

## Objective

The goal of this task is to deepen your understanding of the differences between Network Access Control Lists (NACLs) and Security Groups in AWS. By completing this task, you will learn how to effectively apply NACLs and Security Groups to control access and traffic flow to and from your AWS resources.

## Prerequisites

-   Basic understanding of AWS VPC, Subnets, EC2 Instances, and AWS security best practices.
-   An active AWS account with permissions to create and modify VPCs, Subnets, Security Groups, and NACLs.

## Task Overview

You will set up a simple network architecture within a VPC and apply both NACLs and Security Groups to demonstrate their functionalities and differences.

### Part 1: Set Up Your Environment

1.  **Create a VPC**: Create a new VPC in your AWS account.
2.  **Create Subnets**: Within your VPC, create two subnets: Subnet-A and Subnet-B.
3.  **Launch EC2 Instances**: Launch two EC2 instances, placing one in Subnet-A and the other in Subnet-B.

### Part 2: Apply Security Groups

1.  **Create Security Groups**: Create two Security Groups: SG-A and SG-B.
    -   SG-A allows inbound SSH traffic from your IP address.
    -   SG-B allows inbound ICMP (ping) traffic from SG-A.
2.  **Assign Security Groups**: Assign SG-A to the EC2 instance in Subnet-A, and SG-B to the EC2 instance in Subnet-B.

### Part 3: Configure NACLs

1.  **Modify Default NACL**: Modify the default NACL associated with your VPC to deny all inbound and outbound traffic.
2.  **Create Custom NACLs**: Create two NACLs: NACL-A and NACL-B.
    -   NACL-A allows inbound and outbound SSH traffic from your IP address.
    -   NACL-B allows inbound and outbound ICMP traffic from the CIDR block of your VPC.
3.  **Associate NACLs**: Associate NACL-A with Subnet-A and NACL-B with Subnet-B.

### Part 4: Test and Analyze

1.  **SSH Access**: Attempt to SSH into the EC2 instance in Subnet-A. Record your observations.
2.  **Ping Test**: From the EC2 instance in Subnet-A, attempt to ping the EC2 instance in Subnet-B. Record your observations.

## Deliverables

-   A diagram of your network setup, including the VPC, subnets, EC2 instances, Security Groups, and NACLs.
-   A brief explanation of your observations from the SSH access and ping test attempts, highlighting how Security Groups and NACLs behaved in each scenario.

## Evaluation Criteria

-   Correct implementation of VPC, Subnets, EC2 instances, Security Groups, and NACLs.
-   Successful demonstration of the functional differences between Security Groups and NACLs based on the tests conducted.
-   Clear and concise documentation of your setup, tests, and observations.
