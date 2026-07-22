# 13 - AWS Architecture

## Overview
Together-Wifi targets deployment on Amazon Web Services (AWS) using cloud-native managed infrastructure to deliver high scalability, fault tolerance, and automated operations.

---

## Architecture Topology

```
                                +-------------------+
                                |    Route 53       |
                                +---------+---------+
                                          |
                                          v
                                +-------------------+
                                |  CloudFront CDN   |
                                +---------+---------+
                                          |
                                          v
                                +-------------------+
                                | Application Load  |
                                |   Balancer (ALB)  |
                                +---------+---------+
                                          |
                        +-----------------+-----------------+
                        |   VPC Public / Private Subnets   |
                        +-----------------+-----------------+
                                          |
        +---------------------------------+---------------------------------+
        |                                 |                                 |
        v                                 v                                 v
+---------------+                 +---------------+                 +---------------+
|   AWS ECS     |                 |   AWS RDS     |                 |ElastiCache    |
| (Fargate /    |                 |(PostgreSQL 16)|                 |  (Redis)      |
| Microservices)|                 +---------------+                 +---------------+
+---------------+
```

---

## AWS Services Breakdown

### 1. Networking & Edge Security
- **Amazon Route 53:** DNS management and latency-based routing.
- **AWS WAF & Shield:** Firewall protection against web exploits and DDoS attacks.
- **Amazon CloudFront:** Global Content Delivery Network (CDN) for static assets and API caching.
- **AWS VPC:** Isolated virtual network split across Availability Zones (AZs) into Public Subnets (ALB, Gateway) and Private Subnets (Microservices, Databases).

### 2. Compute & Microservices
- **Amazon ECS (Elastic Container Service) with AWS Fargate:** Serverless container execution for microservices (API Gateway, Auth, WiFi, Payment, Review, Notification).
- **Auto Scaling Groups:** Scales container instances based on CPU, memory, and HTTP request metrics.

### 3. Data Stores & Messaging
- **Amazon RDS for PostgreSQL:** Multi-AZ deployment for high availability, automated backups, and read replicas.
- **Amazon ElastiCache for Redis:** Managed cache cluster for low-latency session and token storage.
- **Amazon MQ / Self-Hosted RabbitMQ on EC2:** Managed message broker for inter-service async events.
- **Amazon S3:** Object storage for user uploads (profile photos, hotspot verification documents).

### 4. Security & Monitoring
- **AWS IAM:** Fine-grained role-based access control.
- **AWS Secrets Manager / Parameter Store:** Centralized secrets management.
- **Amazon CloudWatch:** System metrics, alarm triggers, log aggregation, and tracing via AWS X-Ray.
