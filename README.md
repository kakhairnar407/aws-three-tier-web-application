# AWS Three-Tier Web Application

A hands-on AWS cloud project demonstrating a secure and scalable web application architecture using Amazon VPC, EC2, Application Load Balancer, NAT Gateway, Bastion Host, Target Groups, Route Tables, and Security Groups.

## Architecture

![AWS Three-Tier Architecture](architecture/aws-three-tier-architecture.png)

## Project Overview

The project demonstrates how to deploy a web application across public and private subnets within an Amazon VPC.

An internet-facing Application Load Balancer receives HTTP requests and distributes traffic across two EC2 application servers running Apache Web Server.

A Bastion Host provides controlled SSH access to the private application servers, while a NAT Gateway provides outbound internet connectivity for resources in private subnets.

## AWS Services Used

- Amazon VPC
- Amazon EC2
- Application Load Balancer (ALB)
- Target Groups
- Internet Gateway
- NAT Gateway
- Route Tables
- Security Groups
- Apache Web Server
- Bastion Host

## Network Configuration

| Component | Configuration |
|---|---|
| AWS Region | ap-south-1 (Mumbai) |
| VPC CIDR | 10.0.0.0/16 |
| Application Protocol | HTTP |
| Application Port | 80 |
| Load Balancer | Application Load Balancer |
| Target Type | EC2 Instances |
| Health Check | HTTP / |

## Architecture Flow

```text
Internet
   |
   v
Internet Gateway
   |
   v
Application Load Balancer
   |
   v
Target Group
   |
   +--------------------+
   |                    |
   v                    v
App Server 1        App Server 2
(Private Subnet)    (Private Subnet)
   |
   +---- Apache Web Server

**For administration:

Administrator
     |
     v
Bastion Host
(Public Subnet)
     |
     v
Private App Servers

For outbound connectivity from private resources:

Private App Servers
        |
        v
   NAT Gateway
        |
        v
Internet Gateway
        |
        v
    Internet

**Key Implementation Steps**
Created an Amazon VPC with CIDR 10.0.0.0/16.
Created public and private subnets across Availability Zones.
Configured Internet Gateway and public route tables.
Created a NAT Gateway for private subnet outbound connectivity.
Created security groups for the ALB, Bastion Host, and application servers.
Launched a Bastion Host in a public subnet.
Launched two EC2 application servers in private subnets.
Installed and configured Apache Web Server on the application servers.
Created an Application Load Balancer.
Created a Target Group using the two EC2 application servers.
Configured an HTTP listener on port 80.
Verified target health checks.
Confirmed both application servers became healthy.
Tested application access through the ALB.
Verified responses from both application servers.
Application Validation

The application was successfully tested through the Application Load Balancer.
Example responses:

Welcome to App Server 1
and
Welcome to App Server 2
The successful responses confirmed that the ALB was able to route traffic to the registered healthy EC2 targets.

**Security Design**

The project uses AWS Security Groups to control traffic between components.

ALB accepts HTTP traffic on port 80.
Application servers accept application traffic from the ALB.
SSH access to private application servers is performed through the Bastion Host.
Private application servers are not directly exposed to the internet.
NAT Gateway is used for outbound connectivity from private resources.

**Troubleshooting**

During implementation, practical issues were resolved involving:

EC2 public IP changes after stopping and starting instances.
SSH connectivity through the Bastion Host.
Private key format and SSH authentication.
Security Group rules.
Application Load Balancer target registration.
Target Group health checks.
Verifying application responses from both EC2 servers.

**Project Screenshots**

Implementation screenshots are available in the screenshots directory.

**The screenshots demonstrate**

VPC and subnet configuration
EC2 instances
Security Groups
NAT Gateway
Target Group
Healthy application targets
Application Load Balancer
Application responses from both servers

**Documentation**

Detailed deployment steps are available in the deployment guide.

Skills Demonstrated
AWS Cloud Networking
VPC Architecture
Public and Private Subnets
EC2
Application Load Balancing
NAT Gateway
Route Tables
Security Groups
Linux
Apache
SSH
Cloud Troubleshooting
AWS Infrastructure Deployment


**Project Status**
Completed
This project was created as a hands-on AWS cloud infrastructure and networking implementation.
