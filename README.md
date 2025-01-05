# AWS 3-Tier Web Application Deployment

This repository provides a comprehensive guide for deploying a dynamic web application on AWS using a 3-tier architecture. The solution leverages AWS services such as EC2, S3, RDS, and an Application Load Balancer to address the challenges of scalability, high availability, and secure data management for dynamic web applications.

---

## Business Problem

### Problem Overview

Businesses that manage dynamic web applications often face several key challenges:

1. **Scalability**: Ensuring the application handles increasing traffic without compromising performance.
2. **High Availability**: Minimizing downtime and ensuring consistent access.
3. **Data Security and Management**: Protecting sensitive data and maintaining database integrity.
4. **Cost Management**: Balancing infrastructure costs while handling traffic spikes effectively.

### Proposed Solution

The proposed solution implements a **3-tier architecture** that separates the web (presentation), application (logic), and database (storage) layers. It leverages AWS services to ensure:
- **Scalability** with EC2 Auto Scaling and Application Load Balancers.
- **High Availability** through multiple availability zones (AZs) and load balancing.
- **Data Security** using private subnets, secure RDS instances, and IAM role management.
- **Cost Optimization** by dynamically scaling infrastructure based on demand.

---

## Solution Architecture

The 3-tier architecture consists of three core layers:

1. **Web Tier**: Handles user requests, deployed on EC2 instances behind an Application Load Balancer.
2. **Application Tier**: Processes logic and business rules on separate EC2 instances.
3. **Database Tier**: Manages data in an RDS (Relational Database Service) instance, secured within a private subnet.

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [1. S3 Bucket Setup](#1-s3-bucket-setup)
- [2. VPC and Networking Setup](#2-vpc-and-networking-setup)
- [3. EC2 Instances Setup](#3-ec2-instances-setup)
- [4. RDS and Data Migration](#4-rds-and-data-migration)
- [5. Application Load Balancer](#5-application-load-balancer)
- [6. Website Installation](#6-website-installation)
- [7. DNS and SSL Setup](#7-dns-and-ssl-setup)
- [8. Auto Scaling Group and SNS Setup](#8-auto-scaling-group-and-sns-setup)
- [Conclusion](#conclusion)

---

## Prerequisites

1. AWS account
2. AWS CLI installed and configured
3. A domain name (for DNS setup)
4. Web application code ready for deployment

---

## 1. S3 Bucket Setup

1. Create an S3 bucket in AWS.
2. Upload web application files (e.g., static files, SQL scripts) to the bucket.
3. Optionally configure the bucket for public access if required.

---

## 2. VPC and Networking Setup

1. **Create a 3-Tier VPC**: Navigate to the VPC dashboard and set up public, private, and database subnets.
2. **Enable DNS Hostname**: Ensure DNS resolution and hostname options are enabled.
3. **Internet Gateway**: Attach an Internet Gateway for outbound traffic.
4. **Subnets**: Create public and private subnets for the architecture.
5. **NAT Gateway**: Set up a NAT Gateway for internet access in private subnets.
6. **Routing Tables**: Configure public and private route tables and associate them with the appropriate gateways.

---

## 3. EC2 Instances Setup

1. **Launch EC2 Instances**: Deploy instances in the appropriate subnets for the web and application tiers.
2. **Connect via SSH**: Access instances using AWS Management Console or CLI.
3. **Terminate Instances**: Shut down instances when not needed to save costs.

---

## 4. RDS and Data Migration

1. **Create RDS Instance**: Deploy the database in a private subnet.
2. **Upload SQL Scripts**: Use an S3 bucket to store migration scripts.
3. **IAM Role for S3 Access**: Attach a role with S3 permissions to the EC2 instance used for migration.
4. **Data Migration**: Use Flyway or a similar tool to transfer SQL scripts to the RDS instance.

---

## 5. Application Load Balancer

1. **Create a Target Group**: Define a target group for EC2 instances.
2. **Deploy Application Load Balancer**: Set up the ALB to distribute traffic across EC2 instances.

---

## 6. Website Installation

1. **Prepare Installation Script**: Automate the deployment of the web application.
2. **Run Script**: Install the web application on the web tier EC2 instances.

---

## 7. DNS and SSL Setup

1. **Domain Registration**: Use Route 53 for DNS configuration.
2. **Configure DNS Records**: Point your domain to the ALB.
3. **SSL Certificate**: Use AWS Certificate Manager (ACM) to obtain and attach an SSL certificate for HTTPS.

---

## 8. Auto Scaling Group and SNS Setup

1. **Create AMI**: Save a pre-configured EC2 instance as an AMI.
2. **Set Up Auto Scaling**: Configure Auto Scaling with the AMI to handle traffic spikes.
3. **SNS Notifications**: Set up an SNS topic for Auto Scaling events and subscribe to receive alerts.

---

## Conclusion

This 3-tier architecture on AWS ensures scalability, high availability, and secure data management. By leveraging EC2, RDS, ALB, Auto Scaling, and SNS notifications, this solution optimizes performance and cost while maintaining reliability.

