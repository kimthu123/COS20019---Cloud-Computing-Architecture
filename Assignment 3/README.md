# Serverless / Event-Driven Photo Album Architecture  
COS20019 – Cloud Computing Architecture | Assignment 3

## Project Overview
This project presents a **serverless and event-driven architectural design** for a globally scalable and highly available Photo Album application. The design responds to increasing user demand, global performance requirements, and operational cost concerns by adopting **managed AWS services** and **event-driven processing**.

The proposed architecture replaces traditional server-based components where possible and focuses on **scalability, decoupling, reliability, security, and cost efficiency**, following AWS Well-Architected Framework principles.

---


## Business Context
The Photo Album application has experienced rapid growth, with demand doubling every six months. The existing EC2-based architecture is reaching performance limits and is costly to scale. The business requires a future-proof solution that:
- Minimises system administration overhead
- Scales automatically with unpredictable demand
- Improves global response times
- Supports media processing (images and future video)
- Uses cost-effective, managed cloud services
- Adopts a serverless and event-driven model

---

## Proposed Architecture Overview
The proposed solution adopts a **fully managed, serverless-first architecture** using the following AWS services:

- Amazon Route 53
- Amazon CloudFront
- Amazon S3
- Amazon API Gateway
- AWS Lambda
- Amazon DynamoDB
- Amazon SQS
- Amazon SNS
- AWS Step Functions
- AWS Media Services (Elastic Transcoder / MediaConvert)
- Amazon Rekognition (extensible future service)
- AWS IAM
- Amazon CloudWatch

The architecture is designed to be globally distributed, loosely coupled, and highly resilient.

---

## Core Architectural Components

### Content Delivery & Access
- **Route 53** for DNS and global traffic routing
- **CloudFront** for global content delivery and low-latency access
- **S3** as the primary storage for original and processed media

### Application Layer
- **API Gateway** to expose RESTful endpoints
- **Lambda functions** to handle application logic without managing servers
- **IAM roles** for fine-grained access control

### Data Storage
- **DynamoDB** replaces relational databases for faster performance and lower cost
- Fully managed, auto-scaling NoSQL database

### Media Processing (Event-Driven)
- Media upload to S3 triggers **S3 Event Notifications**
- Events published to **SQS** queues
- Worker Lambda functions or container-based services consume messages
- Media transformations performed asynchronously:
  - Thumbnail generation
  - Image resizing
  - Video transcoding (future)
- Processed media stored back in S3

### Orchestration & Extensibility
- **Step Functions** coordinate complex processing workflows
- **SNS** enables fan-out notifications
- Architecture supports easy integration of AI services such as Rekognition

---

## UML Interaction Overview
The design includes UML collaboration / sequence diagrams covering:
- Media upload flow
- Event-driven media processing pipeline
- Asynchronous worker execution
- Error handling and retry mechanisms

These diagrams demonstrate clear message ordering and service interactions.

---

## Design Rationale

### Performance & Scalability
- Serverless services scale automatically based on demand
- CloudFront improves global response times
- Asynchronous processing prevents application overload

### Reliability
- Fully managed AWS services reduce single points of failure
- Decoupled components isolate failures
- Built-in retries and dead-letter queues improve resilience

### Security
- IAM roles follow least-privilege principles
- Private S3 buckets with controlled access
- API Gateway authentication and throttling
- Encrypted data at rest and in transit

### Cost Efficiency
- Pay-per-use pricing model
- No idle EC2 instances
- Reduced operational overhead
- Cost-effective NoSQL storage

---

## Alternative Solutions Considered
- EC2 vs Containers vs Serverless
- SQL (RDS) vs NoSQL (DynamoDB)
- Push-based vs Pull-based messaging
- Monolithic vs Multi-tier vs Event-driven architecture

Quantitative and qualitative comparisons were used to justify the final design.

---

## Extensibility & Future Enhancements
- Video transcoding using AWS MediaConvert
- AI-based tagging using Amazon Rekognition
- User authentication using Amazon Cognito
- Advanced monitoring with CloudWatch dashboards

---

## Submission Notes
- Document format: IEEE Conference Style
- Maximum length: 15 pages
- Submission type: PDF
- Interview presentation prepared with architecture diagrams
- Design decisions documented with clear assumptions

---

## References
- AWS Well-Architected Framework
- AWS Architecture Center
- Cloud Design Patterns
- COS20019 Assignment 3 Specification

