📸 Photo Album Website on AWS

COS20019 – Cloud Computing Architecture | Assignment 1B

📌 Project Overview

This project demonstrates the design, deployment, and testing of a secure, multi-tier AWS infrastructure to host a Photo Album web application.
The application stores photos in Amazon S3, metadata in Amazon RDS (MySQL), and runs on an Apache + PHP web server hosted on EC2, all within a custom VPC.

The system follows cloud best practices including:

Network isolation using public/private subnets

Least-privilege security groups and Network ACLs

Bastion host access pattern

Persistent public access using Elastic IP

🧑‍🎓 Student Information

Name: Thu Tran

Student ID: [Your Student ID]

Unit: COS20019 – Cloud Computing Architecture

Institution: Swinburne University of Technology

🏗️ Architecture Overview

The deployed infrastructure includes:

Custom VPC (us-east-1)

2 Public Subnets

2 Private Subnets

Internet Gateway for public access

Security Groups for Web, DB, and Test tiers

Network ACL applied to Public Subnet 2

EC2 Instances

Bastion/Web Server (Public Subnet)

Test Instance (Private Subnet)

Amazon RDS

MySQL 8.0.34 (Private Subnet)

Amazon S3

Public photo storage via bucket policy

🖥️ EC2 Configuration
Bastion / Web Server

AMI: Amazon Linux 2

Instance Type: t2.micro

Services Installed:

Apache

PHP

MySQL client

phpMyAdmin

Elastic IP: Enabled for persistent URL

Test Instance

Located in a private subnet

Used to:

SSH via bastion host

Ping the web server (ICMP test)

🗄️ Database Design (Amazon RDS)

Engine: MySQL 8.0.34

Access: Private only (WebServerSG)

Table: photos

Column Name	Type
title	VARCHAR(255)
description	VARCHAR(255)
creation_date	DATE
keywords	VARCHAR(255)
s3_url	VARCHAR(255)
☁️ S3 Photo Storage

Photos stored in a dedicated S3 bucket

Public access enabled via bucket policy

Individual object ACLs not used (as per requirements)

Example object URL:

https://<bucket-name>.s3.amazonaws.com/example.jpg

🌐 Web Application Functionality

The Photo Album website allows users to:

View all uploaded photos

Display photo metadata from RDS

Load images dynamically from S3

Application URL
http://<Elastic-IP>/cos20019/photoalbum/album.php

🔐 Security Implementation

Security Groups

WebServerSG: HTTP (80), SSH (22)

DBServerSG: MySQL (3306) from WebServerSG only

TestInstanceSG: ICMP enabled

Network ACL

SSH allowed from anywhere

ICMP allowed only from Test subnet

HTTP allowed for public users

🧪 Testing & Validation

Verified:

SSH access to private EC2 via bastion

ICMP ping from Test instance to Web server

Photos correctly rendered from S3

Metadata correctly retrieved from RDS

Website accessible via Elastic IP

Screenshots are included in the submission PDF as required.

📄 Submission Notes

Environment: AWS Learner Lab

Submission format: Single PDF (IEEE style, ≤15 pages)

Resources checked for availability before submission

Assignment complies with all functional and infrastructure requirements

✅ Assignment Checklist

✔ Custom VPC
✔ Correct subnet & routing configuration
✔ Secure EC2 deployment
✔ RDS in private subnet
✔ S3 public access via bucket policy
✔ Network ACL implemented
✔ Functional Photo Album website
