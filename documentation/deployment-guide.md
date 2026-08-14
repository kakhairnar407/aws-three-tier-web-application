# AWS Three-Tier Web Application — Deployment Guide

## 1. Project Overview

This project demonstrates the deployment of a highly available web application architecture on AWS using Amazon VPC, EC2, Application Load Balancer, NAT Gateway, Internet Gateway, Bastion Host, Target Group, and Security Groups.

The application is deployed across multiple Availability Zones and uses an Application Load Balancer to distribute HTTP traffic between two EC2 application servers.

----------------------------------------------------------------------------------------------------------------------

## 2. AWS Services Used

- Amazon VPC
- Amazon EC2
- Application Load Balancer (ALB)
- Target Group
- Internet Gateway (IGW)
- NAT Gateway
- Route Tables
- Security Groups
- Apache Web Server
- Bastion Host

----------------------------------------------------------------------------------------------------------------------

## 3. Network Architecture

### VPC

VPC CIDR:

`10.0.0.0/16`

The VPC provides the isolated network environment for the application.

### Subnets

The VPC is divided into public and private subnets.

Public subnets are used for internet-facing resources such as the Application Load Balancer and Bastion Host.

Private subnets are used for the application EC2 servers.

----------------------------------------------------------------------------------------------------------------------

## 4. Internet Gateway

An Internet Gateway is attached to the VPC to provide internet connectivity for resources in the public subnets.

The public route table contains a default route:

`0.0.0.0/0 → Internet Gateway`

----------------------------------------------------------------------------------------------------------------------

## 5. NAT Gateway

A NAT Gateway is deployed in a public subnet.

It allows resources in private subnets to initiate outbound internet connections without exposing the private EC2 instances directly to the internet.

Private route tables use:

`0.0.0.0/0 → NAT Gateway`

----------------------------------------------------------------------------------------------------------------------

## 6. Bastion Host

A Bastion Host is deployed in the public subnet.

It provides secure SSH access to the private application servers.

The connection flow is:

Developer → Bastion Host → Private App Server

The application servers are not directly exposed to the internet through SSH.

----------------------------------------------------------------------------------------------------------------------

## 7. Application Servers

Two EC2 instances are deployed as application servers:

- App Server 1
- App Server 2

Apache Web Server is installed on both servers.

Each server hosts a simple web page so that the Application Load Balancer can route requests between them.

----------------------------------------------------------------------------------------------------------------------

## 8. Security Groups

Security Groups are used to control network traffic between the different components.

### Bastion Host Security Group

Allows SSH access from the administrator's trusted IP address.

### Application Server Security Group

Allows required application traffic and SSH access from the Bastion Host.

### Load Balancer Security Group

Allows HTTP traffic on port 80 from clients.

----------------------------------------------------------------------------------------------------------------------

## 9. Target Group

An Application Load Balancer Target Group is created using the EC2 instances as targets.

Protocol:

`HTTP`

Port:

`80`

Health check:

`HTTP /`

Both application servers were registered with the target group.

Final health status:

`2 Healthy`

----------------------------------------------------------------------------------------------------------------------

## 10. Application Load Balancer

An Internet-facing Application Load Balancer is created across the public subnets.

Listener:

`HTTP : 80`

The listener forwards incoming requests to the application target group.

Traffic flow:

Internet → ALB → Target Group → App Server 1 / App Server 2

----------------------------------------------------------------------------------------------------------------------

## 11. Application Validation

The application was tested through the Application Load Balancer DNS name.

The load balancer successfully routed requests to both application servers.

Example responses:

`Welcome to App Server 1`

`Welcome to App Server 2`

This confirmed that the target group and load-balancing configuration were working correctly.

----------------------------------------------------------------------------------------------------------------------

## 12. Troubleshooting Performed

During implementation, several practical issues were encountered and resolved.

### EC2 Public IP Changes

When an EC2 instance was stopped and started, its public IP address changed.

The updated IP address was used for SSH connectivity.

### SSH Private Key Validation

The EC2 private key was checked and converted/used in the required format to establish SSH connectivity.

### Bastion Host Connectivity

The Bastion Host was used as the entry point for connecting to private application servers.

### Application Load Balancer Health Checks

The target group health checks were verified until both application servers showed:

`Healthy`

----------------------------------------------------------------------------------------------------------------------

## 13. Project Outcome

The completed implementation demonstrates:

- AWS VPC networking
- Public and private subnet design
- Secure Bastion Host access
- NAT Gateway configuration
- EC2 application deployment
- Apache web server configuration
- Application Load Balancer configuration
- Target Group health checks
- Security Group configuration
- HTTP traffic distribution across multiple application servers

----------------------------------------------------------------------------------------------------------------------

## 14. Cleanup

After completing the demonstration, AWS resources were deleted/stopped to avoid unnecessary costs.
