# 08 - Technology Stack

## Overview
Together-Wifi is built on a modern, scalable, distributed architecture designed for high availability, low latency, and ease of deployment.

---

## 1. Core Stack Summary

| Domain | Technology | Purpose |
| :--- | :--- | :--- |
| **Mobile App** | Flutter / Dart | Cross-platform mobile app for iOS & Android |
| **API Gateway** | Node.js / Express | Unified entry point, routing, rate limiting |
| **Microservices** | Node.js / Java Spring Boot | Core domain services (Auth, WiFi, Payment, Review, Notification) |
| **Relational Database** | PostgreSQL 16 | Primary persistent data store |
| **In-Memory Cache** | Redis 7 | Caching, session store, rate limiting counters |
| **Message Broker** | RabbitMQ 3.x | Asynchronous event-driven communication |
| **Containerization** | Docker & Docker Compose | Local development and container deployment |
| **Cloud Hosting** | AWS (EC2, RDS, ElastiCache, S3) | Production infrastructure |
| **CI/CD** | GitHub Actions | Automated build, test, and deployment pipeline |

---

## 2. Service-by-Service Stack Breakdown

### Mobile Application
- **Framework:** Flutter (Dart)
- **State Management:** Provider / BLoC
- **HTTP Client:** Dio / http
- **Local Storage:** Flutter Secure Storage, Shared Preferences
- **Maps & Location:** Google Maps SDK, Geolocator

### API Gateway
- **Runtime:** Node.js (v20+)
- **Framework:** Express / Fastify
- **Security:** Helmet, CORS, Rate Limiters
- **Authentication:** jsonwebtoken, passport-jwt

### Backend Services
- **Auth Service:** User management, JWT token generation & verification
- **WiFi Service:** Hotspot location indexing, geofencing, session control
- **Payment Service:** Payment gateway integration (Razorpay), settlement ledgers
- **Review Service:** Star rating system, reviews, sentiment scoring
- **Notification Service:** Firebase Cloud Messaging (FCM), Nodemailer for emails

### Data & Messaging Infrastructure
- **PostgreSQL 16:** Relational database per microservice pattern
- **Redis 7 Alpine:** Key-value store, pub/sub, token blacklisting
- **RabbitMQ 3 Management:** AMQP queue protocol for async background events

---

## 3. DevOps & Environment
- **Containerization:** `docker-compose` orchestration for local and staging environments
- **Version Control:** Git, hosted on GitHub
- **CI/CD:** GitHub Actions workflows for automated linting, testing, image building, and deployment
