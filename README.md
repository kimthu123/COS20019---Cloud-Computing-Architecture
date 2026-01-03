# Photo Album Website on AWS  
COS20019 – Cloud Computing Architecture | Assignment 1B

## Project Overview
This project involves designing, deploying, and testing a secure cloud-based Photo Album web application using Amazon Web Services (AWS). The application stores photos in an Amazon S3 bucket, photo metadata in an Amazon RDS MySQL database, and runs on an Apache web server hosted on an EC2 instance within a custom Virtual Private Cloud (VPC).

The infrastructure follows cloud best practices, including network segmentation, least-privilege security, and high availability across multiple subnets.

---

## Architecture Overview
The AWS infrastructure consists of the following components:

- Custom VPC (us-east-1)
- Two public subnets and two private subnets across two availability zones
- Internet Gateway for public access
- Route tables for public and private subnets
- Security Groups for web server, database server, and test instance
- Network ACL applied to Public Subnet 2
- EC2 instances for Web/Bastion server and Test instance
- Amazon RDS MySQL database in private subnets
- Amazon S3 bucket for photo storage

---

## EC2 Configuration

### Bastion / Web Server Instance
- AMI: Amazon Linux 2
- Instance Type: t2.micro
- Subnet: Public Subnet 2
- Services Installed:
  - Apache Web Server
  - PHP
  - MySQL Client
  - phpMyAdmin
- Elastic IP associated for persistent public access
- Hosts the Photo Album web application
- Acts as a bastion host for SSH access to the private Test instance

### Test Instance
- Located in a private subnet
- Used for demonstration and testing only
- Accessed via SSH through the bastion host
- Used to ping the Web Server instance using ICMP

---

## Database Configuration (Amazon RDS)
- Engine: MySQL 8.0.34
- Template: Free Tier
- Public Access: Disabled
- Subnets: Private subnets only
- Access restricted to WebServer Security Group

### Database Table: photos
Columns:
- title (VARCHAR 255)
- description (VARCHAR 255)
- creation_date (DATE)
- keywords (VARCHAR 255)
- s3_url (VARCHAR 255)

---

## S3 Photo Storage
- A dedicated S3 bucket is used to store photos
- Photos are uploaded manually
- Public access is enabled using a bucket policy
- Individual object ACLs are not used
- Each photo is referenced in the database using its S3 object URL

---

## Web Application Functionality
The Photo Album website provides the following features:
- Lists all photos stored in the S3 bucket
- Displays photo metadata retrieved from the RDS database
- Loads and displays images directly from S3
- Allows searching and viewing photos based on metadata

Application URL format:
http://<Elastic-IP>/cos20019/photoalbum/album.php

---

## Security Implementation
- Security Groups:
  - WebServerSG: Allows HTTP (80) and SSH (22)
  - DBServerSG: Allows MySQL (3306) access from WebServerSG only
  - TestInstanceSG: Allows ICMP traffic
- Network ACL:
  - SSH (22) allowed from anywhere
  - ICMP allowed only from the Test instance subnet
  - HTTP traffic allowed for public users

---

## Testing and Validation
The following tests were successfully completed:
- SSH access to private Test instance via Bastion host
- ICMP ping from Test instance to Web Server instance
- Verification of photo display from S3
- Verification of metadata retrieval from RDS
- Website accessibility via Elastic IP

All required screenshots are included in the submission PDF.

---

## Submission Notes
- Environment: AWS Learner Lab
- Submission format: Single PDF document (IEEE style, maximum 15 pages)
- Elastic IP used to ensure persistent website URL
- All AWS resources were active and accessible at submission time

---

## Assignment Checklist
- Custom VPC created
- Public and private subnets correctly configured
- Routing tables properly associated
- Security groups correctly implemented
- Network ACL applied to Public Subnet 2
- EC2 instances deployed in correct subnets
- RDS database created in private subnet
- S3 objects publicly accessible via bucket policy
- Photo Album website fully functional

---

## References
- AWS Documentation
- COS20019 Assignment 1B Specification
