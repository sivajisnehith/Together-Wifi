# ADR 001: Adoption of Microservices Architecture

## Status
**Accepted**

## Context
Together-Wifi consists of several distinct functional domains with varying scaling requirements, database models, and failure sensitivities:
- Authentication & User Profiles
- WiFi Hotspot Registration & Radius Search
- Transactional Payments & Payout Ledgers
- Ratings & Reviews
- Asynchronous Notifications (FCM / Email)

A monolithic application architecture would couple these distinct domains, making independent deployments risky and preventing selective scaling of high-traffic endpoints (such as nearby WiFi searches).

## Decision
We decided to adopt a **Domain-Driven Microservices Architecture**. Each business domain operates as an autonomous microservice with its own dedicated database and API interface, coordinated via an API Gateway and asynchronous message broker.

## Consequences

### Positive
- **Independent Scalability:** High-traffic services (e.g. WiFi location search) can scale up independently of low-traffic services.
- **Fault Isolation:** A failure in the Review Service or Notification Service will not impact user login or payment processing.
- **Technology Flexibility:** Different services can leverage the runtime best suited for their specific workload.
- **Autonomous Deployment:** Independent team deployment cycles without full platform redeployments.

### Negative
- Higher initial operational complexity (distributed tracing, API gateway setup).
- Requires eventual consistency management across service boundaries via asynchronous messaging.
