# ADR 005: Selection of Amazon Web Services (AWS) as Cloud Provider

## Status
**Accepted**

## Context
Together-Wifi requires a robust, secure, and globally available cloud provider offering managed relational databases, serverless container execution, caching, content delivery networks, and automated backup infrastructure.

## Decision
We selected **Amazon Web Services (AWS)** as our target cloud provider for production deployment.

## Consequences

### Positive
- **Managed Services:** Reduces operational burden via AWS RDS (PostgreSQL), ElastiCache (Redis), and ECS Fargate (Containers).
- **Security & Compliance:** Comprehensive security integrations via IAM, VPC isolation, AWS WAF, and KMS key management.
- **Global Footprint:** Route 53 and CloudFront ensure low-latency global API resolution.

### Negative
- Potential cloud vendor lock-in for provider-specific services (e.g. IAM, CloudWatch).
- Cloud resource usage costs must be strictly tracked via AWS Budgets and cost tags.
