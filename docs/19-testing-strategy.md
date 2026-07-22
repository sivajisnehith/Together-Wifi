# 19 - Testing Strategy

## Overview
Together-Wifi adopts a comprehensive test pyramid strategy combining Unit Testing, Integration Testing, End-to-End (E2E) Testing, and Security/Load Testing.

---

## 1. Test Pyramid Breakdown

```
        / \
       /   \        End-to-End (E2E) Tests  (Mobile UI, Flutter Integration)
      / ---- \
     /        \     Integration Tests        (API Endpoints, DB, RabbitMQ)
    / ---------- \
   /              \  Unit Tests              (Business Logic, Token Helpers)
  /----------------\
```

---

## 2. Testing Layers

### A. Unit Testing
- **Backend:** Testing business logic, utility classes, and service methods in isolation using mocks for DB and external APIs (Jest / JUnit / Mocha).
- **Mobile App:** Unit testing view models, BLoC states, and repository mapping functions using `flutter_test` and `mockito`.

### B. Integration Testing
- Test interaction between microservices, PostgreSQL databases, Redis cache, and RabbitMQ queues.
- Dockerized test suite spins up isolated database and queue instances using `testcontainers` or Docker Compose test profiles.

### C. End-to-End (E2E) Testing
- Automated API testing using Postman / Supertest.
- Mobile UI automation using Flutter Integration Test (`integration_test` package).

### D. Performance & Load Testing
- Simulated traffic testing using **k6** or **Apache JMeter**.
- Benchmarking API Gateway throughput (target: 1,000+ requests/sec with latency < 50ms).

---

## 3. Continuous Integration Enforcement
- PRs cannot be merged unless test coverage meets minimum thresholds:
  - **Unit Tests:** >= 80% coverage
  - **Integration Tests:** Critical paths (Auth, Payments, Connection Flow) covered 100%
