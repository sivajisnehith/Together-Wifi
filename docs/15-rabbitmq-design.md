# 15 - RabbitMQ Design

## Overview
Together-Wifi relies on RabbitMQ for asynchronous, event-driven messaging between microservices. This prevents blocking operations, ensures eventual consistency, and decouples core services.

---

## 1. Message Exchange Topology

RabbitMQ uses a **Topic Exchange** (`together.events`) to route message events to specific microservice queues based on routing keys.

```
                  +--------------------------------+
                  |  Topic Exchange: together.events
                  +---------------+----------------+
                                  |
         +------------------------+------------------------+
         | routing key:           | routing key:           | routing key:
         | payment.*              | wifi.*                 | user.*
         v                        v                        v
+------------------+    +------------------+    +------------------+
| Queue:           |    | Queue:           |    | Queue:           |
| payment-events   |    | wifi-events      |    | notification-    |
|                  |    |                  |    | events           |
+--------+---------+    +--------+---------+    +--------+---------+
         |                         |                         |
         v                         v                         v
  (Payment Service)         (WiFi Service)         (Notification Serv)
```

---

## 2. Event Routing Table

| Producer Service | Routing Key | Event Description | Consumer Service(s) |
| :--- | :--- | :--- | :--- |
| **Auth Service** | `user.registered` | New user created | Notification Service |
| **WiFi Service** | `wifi.session.started` | User connected to hotspot | Payment Service |
| **WiFi Service** | `wifi.session.ended` | Connection closed, duration calculated | Payment Service, Review Service |
| **Payment Service** | `payment.success` | Payment completed | Notification Service, WiFi Service |
| **Payment Service** | `payment.failed` | Payment failed | Notification Service |
| **Review Service** | `review.created` | New review posted | WiFi Service (updates rating avg) |

---

## 3. Reliability & Resilience

- **Message Persistence:** Queues and messages are declared `durable` so messages survive broker restarts.
- **Consumer Acknowledgments (`ack`):** Messages are acknowledged only after processing succeeds. On uncaught error, messages are re-queued or sent to a **Dead Letter Exchange (DLX)**.
- **Dead Letter Exchange (`together.dlx`):** Captures failed messages after maximum retry attempts (e.g. 3 attempts) for manual inspection and troubleshooting.
- **Connection Management:** Retries connection automatically with exponential backoff on startup or network partition.
