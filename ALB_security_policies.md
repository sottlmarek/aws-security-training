# AWS Elastic Load Balancer Task: Configure a Secure TLS Policy

## Objective

Create an AWS Elastic Load Balancer (ELB) that uses a secure TLS policy to ensure encrypted traffic between clients and the load balancer. This task will help you understand how to work with AWS ELB and TLS policies to enhance the security of your applications.

## Prerequisites

-   Basic understanding of AWS Elastic Load Balancers, security groups, and TLS/SSL protocols.
-   An AWS account with access to the EC2, ELB services, and IAM.

## Task Description

You will set up an Application Load Balancer (ALB) in front of a set of web servers to distribute incoming web traffic securely. The ALB must use a secure TLS policy to enforce encrypted communication.

### Step 1: Prepare Your Environment

1.  **Launch EC2 Instances**: Launch two EC2 instances that will serve as your backend web servers. For simplicity, you can use Amazon Linux AMI and install a basic web server like Apache or Nginx on each instance.
2.  **Security Group for EC2 Instances**: Ensure the security group attached to these instances allows inbound traffic on the HTTP port (80) from the ELB.

### Step 2: Create an Application Load Balancer

1.  **Navigate to the EC2 Dashboard** and select "Load Balancers" under the "Load Balancing" section.
2.  **Click "Create Load Balancer"** and choose "Application Load Balancer".
3.  **Configure the Load Balancer**:
    -   Name your ALB appropriately.
    -   Set up the network settings to place your ALB in the correct VPC and subnets.
    -   For listeners, set up an HTTPS listener on port 443. You will configure the secure TLS policy in the next steps.

### Step 3: Configure a Secure TLS Policy

1.  **Choose a Certificate**: For the HTTPS listener, you need an SSL/TLS certificate. You can request a new certificate using AWS Certificate Manager (ACM) or import an existing one.
2.  **Select a Secure TLS Policy**: When setting up the listener, choose a predefined security policy for TLS. AWS provides several policies, and for this task, select a policy that enforces TLS 1.2 or higher, such as `ELBSecurityPolicy-TLS-1-2-Ext-2018-06`.
3.  **Configure the Security Group for ALB**: Ensure the ALB's security group allows inbound HTTPS traffic on port 443 from the internet and outbound traffic to your EC2 instances.

### Step 4: Register Targets and Test

1.  **Register Targets**: In the ALB configuration, add your EC2 instances to a target group to receive traffic from the ALB.
2.  **Review and Create**: Review your ALB configuration and create the ALB.
3.  **Test Your Setup**: After the ALB is deployed, test accessing your web servers through the ALB's DNS name using HTTPS. Ensure that the connection is secure and the TLS policy is enforced.

## Deliverables

-   The configuration details of your Application Load Balancer, including the chosen TLS policy.
-   A screenshot showing the ALB's listener configuration with the HTTPS protocol and secure TLS policy.
-   Evidence of a secure connection to your web servers through the ALB, such as a browser screenshot displaying the HTTPS lock symbol and the TLS version used.
-   How the policy can be improved pro provide FIPS compliance. 

## Evaluation Criteria

-   Successful creation of an Application Load Balancer with an HTTPS listener.
-   Correct application of a secure TLS policy that enforces TLS 1.2 or higher.
-   Proper configuration of security groups to allow secure traffic flow between the ALB and the EC2 instances.
-   Verification of a secure connection to the web servers through the ALB.
