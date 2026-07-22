# 09 - Microservices Architecture

## Overview
Together-Wifi uses a domain-driven microservices architecture to decouple responsibilities, allow independent scaling, and isolate failures across business functions.

---

## Architecture Diagram

```
                             +-------------------+
                             |   Mobile Client   |
                             +---------+---------+
                                       |
                                       v
                             +-------------------+
                             |    API Gateway    |
                             +---------+---------+
                                       |
       +-------------------+-----------+-----------+-------------------+
       |                   |                       |                   |
       v                   v                       v                   v
+--------------+    +--------------+        +--------------+    +--------------+
| Auth Service |    | WiFi Service |        |Payment Serv. |    | Review Serv. |
+------+-------+    +------+-------+        +------+-------+    +------+-------+
       |                   |                       |                   |
       +-------------------+-----------+-----------+-------------------+
                                       |
                                       v (Asynchronous Events)
                             +-------------------+
                             |     RabbitMQ      |
                             +---------+---------+
                                       |
                                       v
                             +-------------------+
                             | Notification Serv |
                             +-------------------+
```

---

## Microservices Breakdown

### 1. API Gateway
- **Role:** Single point of entry for clients.
- **Functions:** Routing, TLS termination, global rate-limiting, JWT authentication validation before passing traffic downstream.

### 2. Auth Service
- **Role:** Manages user identity, registrations, authentication, and profile settings.
- **Data:** Dedicated PostgreSQL schema/database for credentials, refresh tokens, user metadata.

### 3. WiFi Service
- **Role:** Manages WiFi hotspot registration by providers, geographic search for available hotspots, and active session connection management.
- **Data:** Dedicated PostgreSQL database (PostGIS optional for geo-queries), Redis for active session status.

### 4. Payment Service
- **Role:** Handles payment transactions, Razorpay webhook processing, provider earnings, and payout settlements.
- **Data:** Dedicated PostgreSQL database with strict transactional isolation.

### 5. Review Service
- **Role:** Collects and processes user ratings and reviews for WiFi providers.
- **Data:** Dedicated PostgreSQL database for rating aggregations.

### 6. Notification Service
- **Role:** Consumes async message events from RabbitMQ and dispatches FCM push notifications, email alerts, or SMS.
- **Data:** Event history log database.

---

## Inter-Service Communication

### Synchronous Communication (HTTP / REST)
- Used for immediate client-driven requests (e.g., Auth verification, fetching nearby hotspots, creating payment orders).

### Asynchronous Communication (AMQP / RabbitMQ)
- Used for event broadcasting and background processing (e.g., `payment.completed` event triggers `notification.send` and updates session stats).

---

## Service Autonomy & Database-per-Service
Each microservice owns its data store to enforce strict boundaries. No service directly queries another service's database. Cross-service data fetching is performed via REST APIs or cached event materialization.
