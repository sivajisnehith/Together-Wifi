# ADR 002: Adoption of Docker & Container Orchestration

## Status
**Accepted**

## Context
Developing and running microservices locally across multiple developer machines (Windows, macOS, Linux) often introduces environment inconsistencies ("works on my machine" syndrome), mismatched runtime dependencies, and complicated database/message-broker setup procedures.

## Decision
We decided to standardize containerization using **Docker** and orchestrate the local multi-service environment using **Docker Compose**.

## Consequences

### Positive
- **Consistent Environments:** Guarantees identical execution runtime across development, staging, and production environments.
- **One-Command Setup:** Developers can spin up PostgreSQL, Redis, RabbitMQ, and services using `docker-compose up -d`.
- **Cloud Readiness:** Container images can be seamlessly deployed to cloud orchestrators like AWS ECS or Kubernetes.

### Negative
- Requires developer familiarity with Docker CLI and container networking concepts.
- Resource usage overhead on local developer workstations when running multiple heavy containers simultaneously.
