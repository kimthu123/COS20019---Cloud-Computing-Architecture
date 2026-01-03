# Highly Available Photo Album Website on AWS  
COS20019 – Cloud Computing Architecture | Assignment 2

## Project Overview
This project extends Assignment 1B by designing and deploying a **highly available and scalable Photo Album web application** on Amazon Web Services (AWS). The system uses **Auto Scaling**, **Application Load Balancer**, **Lambda**, and **IAM roles** to ensure fault tolerance, scalability, and secure service-to-service communication.

Photos are uploaded through the web application, stored securely in Amazon S3, processed by an AWS Lambda function to generate thumbnails, and their metadata is stored in an Amazon RDS MySQL database.

---

## Student Information
Name: Thu Tran  
Student ID: [Your Student ID]  
Unit: COS20019 – Cloud Computing Architecture  
Institution: Swinburne University of Technology  

---

## Architecture Overview
The infrastructure is built on top of Assignment 1B and includes:

- Custom VPC (us-east-1)
- Two Availability Zones
- Public and private subnets in each AZ
- Internet Gateway and NAT (Instance or Gateway)
- Application Load Balancer (ALB)
- Auto Scaling Group (ASG)
- EC2 Web Servers (private subnets)
- Dev Server (public subnet)
- Amazon RDS (MySQL)
- Amazon S3 (private access via bucket policy)
- AWS Lambda (CreateThumbnail)
- IAM Roles and Policies
- Network ACLs for traffic control

---

## Web Application Features

### album.php
- Retrieves photo metadata from RDS
- Displays photos stored in S3
- Accessible only via Application Load Balancer

### photouploader.php
- Uploads photos from client to EC2
- Stores photos in S3
- Inserts metadata into RDS
- Invokes Lambda function to generate thumbnails

Website access:
http://<ELB-DNS>/photoalbum/album.php

---

## Auto Scaling & Load Balancing
- Auto Scaling Group:
  - Minimum instances: 2
  - Maximum instances: 3
  - Deployed across private subnets
- Target tracking policy:
  - Request count per target = 30
- Application Load Balancer:
  - Distributes traffic across EC2 instances
  - Health check path: /photoalbum/album.php

---

## EC2 & AMI Configuration
- Base AMI: Amazon Linux 2
- Custom AMI created from Dev Server
- Includes:
  - Apache Web Server
  - PHP
  - AWS SDK for PHP
  - Photo Album source code
- Instances launched automatically by ASG
- No manual configuration after launch

---

## Lambda Function: CreateThumbnail
- Runtime: Python 3.11
- Architecture: arm64
- Triggered by EC2 invocation
- Downloads image from S3
- Resizes image
- Uploads resized image back to S3
- Output filename format:
  resized-<original_filename>.png

---

## Database Configuration (Amazon RDS)
- Engine: MySQL
- Hosted in private subnets
- Same database as Assignment 1B
- Managed via Dev Server using phpMyAdmin

---

## S3 Bucket Security
- S3 bucket access restricted using bucket policy
- Direct public access to objects disabled
- Access allowed only from:
  - EC2 instances
  - Lambda function
- Thumbnail images stored in the same bucket

---

## Security Implementation
- IAM Roles:
  - EC2 role: S3 access + Lambda invoke
  - Lambda role: S3 read/write permissions
- Security Groups:
  - ELBSG
  - WebServerSG
  - DBServerSG
  - NATServerSG (if applicable)
  - DevServerSG
- Network ACL:
  - PrivateSubnetsNACL blocks bidirectional ICMP to/from Dev Server

---

## Testing & Validation
The following tests were performed successfully:
- Website accessible only via ELB
- Photos uploaded and stored in S3
- Metadata recorded in RDS
- Thumbnails created by Lambda function
- Auto Scaling launches replacement instances on termination
- All ELB targets remain healthy
- Direct public access to S3 objects blocked
- Network ACL ICMP rules enforced correctly

---

## Submission Notes
- Environment: AWS Learner Lab
- Submission format: Single PDF document
- Documentation follows IEEE Conference Style
- Maximum length: 15 pages
- All AWS resources active at submission time

---

## Assignment Checklist
- VPC configured with multi-AZ subnets
- NAT configured correctly
- IAM roles implemented with least privilege
- Auto Scaling Group operational
- Application Load Balancer configured correctly
- Lambda function working as expected
- Secure S3 bucket policy applied
- Website fully functional and highly available

---

## References
- AWS Documentation
- COS20019 Assignment 2 Specification
