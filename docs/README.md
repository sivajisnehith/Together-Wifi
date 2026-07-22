# Together-Wifi Documentation Index

Welcome to the comprehensive system documentation for **Together-Wifi**, a distributed microservice platform enabling shared WiFi monetization, location discovery, and seamless connections.

---

## 📂 Documentation Directory Structure

```
docs/
│
├── README.md                     ⭐ Documentation Index
│
├── adr/
│   ├── ADR-001-Why-Microservices.md
│   ├── ADR-002-Why-Docker.md
│   ├── ADR-003-Why-RabbitMQ.md
│   ├── ADR-004-Why-Redis.md
│   ├── ADR-005-Why-AWS.md
│   ├── ADR-006-Why-JWT.md
│   └── ADR-007-Why-Flutter.md
│
├── diagrams/
│   ├── architecture/
│   ├── database/
│   ├── deployment/
│   ├── flowcharts/
│   ├── networking/
│   ├── sequence/
│   ├── usecase/
│   └── class/
│
├── 01-project-overview.md
├── 02-functional-requirements.md
├── 03-non-functional-requirements.md
├── 04-system-architecture.md
├── 05-database-design.md
├── 06-api-design.md
├── 07-deployment.md
├── 08-technology-stack.md
├── 09-microservices-architecture.md
├── 10-security-architecture.md
├── 11-authentication-flow.md
├── 12-docker-architecture.md
├── 13-aws-architecture.md
├── 14-ci-cd-pipeline.md
├── 15-rabbitmq-design.md
├── 16-redis-design.md
├── 17-mobile-architecture.md
├── 18-development-guidelines.md
├── 19-testing-strategy.md
└── 20-future-enhancements.md
```

---

## 📚 Core Architecture Documents

| Chapter | Document Title | Description |
| :--- | :--- | :--- |
| **01** | [01-project-overview.md](01-project-overview.md) | High-level project goals, features, and target audience |
| **02** | [02-functional-requirements.md](02-functional-requirements.md) | Functional capabilities, user stories, and feature specs |
| **03** | [03-non-functional-requirements.md](03-non-functional-requirements.md) | Scalability, latency, security, and uptime SLAs |
| **04** | [04-system-architecture.md](04-system-architecture.md) | High-level service layout and system components |
| **05** | [05-database-design.md](05-database-design.md) | Database per service schemas and data modeling |
| **06** | [06-api-design.md](06-api-design.md) | REST API specifications and Gateway endpoints |
| **07** | [07-deployment.md](07-deployment.md) | Deployment strategies, environment management |
| **08** | [08-technology-stack.md](08-technology-stack.md) | Tech stack breakdown (Node, Flutter, Postgres, Redis, RabbitMQ) |
| **09** | [09-microservices-architecture.md](09-microservices-architecture.md) | In-depth microservices design and inter-service comms |
| **10** | [10-security-architecture.md](10-security-architecture.md) | End-to-end security, encryption, rate limiting, CORS |
| **11** | [11-authentication-flow.md](11-authentication-flow.md) | JWT dual-token scheme, token rotation, and invalidation |
| **12** | [12-docker-architecture.md](12-docker-architecture.md) | Docker Compose orchestration, networking, and multi-stage builds |
| **13** | [13-aws-architecture.md](13-aws-architecture.md) | AWS Cloud infrastructure (ECS, RDS, ElastiCache, S3, ALB) |
| **14** | [14-ci-cd-pipeline.md](14-ci-cd-pipeline.md) | GitHub Actions CI/CD workflows, testing, and automated deploy |
| **15** | [15-rabbitmq-design.md](15-rabbitmq-design.md) | AMQP exchanges, event queues, routing keys, and DLX |
| **16** | [16-redis-design.md](16-redis-design.md) | In-memory caching strategies, rate limiting, and GEO search |
| **17** | [17-mobile-architecture.md](17-mobile-architecture.md) | Flutter application architecture, state management, and plugins |
| **18** | [18-development-guidelines.md](18-development-guidelines.md) | Branching strategy, commit conventions, and code standards |
| **19** | [19-testing-strategy.md](19-testing-strategy.md) | Unit, integration, E2E, and performance testing frameworks |
| **20** | [20-future-enhancements.md](20-future-enhancements.md) | Roadmap for Passpoint, Web3 payments, and Kubernetes migration |

---

## 🏛️ Architectural Decision Records (ADRs)

| ADR ID | Decision Document | Key Decision Summary |
| :--- | :--- | :--- |
| **ADR-001** | [ADR-001-Why-Microservices.md](adr/ADR-001-Why-Microservices.md) | Why microservices were chosen over a monolithic architecture |
| **ADR-002** | [ADR-002-Why-Docker.md](adr/ADR-002-Why-Docker.md) | Standardizing containerization for environment parity |
| **ADR-003** | [ADR-003-Why-RabbitMQ.md](adr/ADR-003-Why-RabbitMQ.md) | Choosing RabbitMQ Topic Exchanges for async event processing |
| **ADR-004** | [ADR-004-Why-Redis.md](adr/ADR-004-Why-Redis.md) | In-memory caching, token blacklisting, and geospatial search |
| **ADR-005** | [ADR-005-Why-AWS.md](adr/ADR-005-Why-AWS.md) | Selecting AWS cloud managed services for production hosting |
| **ADR-006** | [ADR-006-Why-JWT.md](adr/ADR-006-Why-JWT.md) | Stateless JWT authentication with dual token rotation |
| **ADR-007** | [ADR-007-Why-Flutter.md](adr/ADR-007-Why-Flutter.md) | Cross-platform mobile development using Flutter & Dart |

---

## 🎨 Diagrams Directory

All visual architecture blueprints, database ERDs, flowcharts, and sequence diagrams are organized under [docs/diagrams](diagrams/):

- 📐 [diagrams/architecture/](diagrams/architecture/) - High-level and component architecture diagrams
- 🗄️ [diagrams/database/](diagrams/database/) - Entity-Relationship Diagrams (ERDs) and schemas
- 🚀 [diagrams/deployment/](diagrams/deployment/) - AWS infrastructure and Docker container topologies
- 🔄 [diagrams/flowcharts/](diagrams/flowcharts/) - Business logic and connection flowcharts
- 🌐 [diagrams/networking/](diagrams/networking/) - VPC subnets, API Gateway, and security boundaries
- ⏱️ [diagrams/sequence/](diagrams/sequence/) - Request/response sequence diagrams (Auth, Payment)
- 👤 [diagrams/usecase/](diagrams/usecase/) - User & Provider use case interactions
- 🧩 [diagrams/class/](diagrams/class/) - Domain model and service class diagrams
