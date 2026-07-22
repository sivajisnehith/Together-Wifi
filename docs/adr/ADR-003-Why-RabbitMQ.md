# ADR 003: Selection of RabbitMQ as Message Broker

## Status
**Accepted**

## Context
Together-Wifi microservices require asynchronous communication for non-blocking workflows such as dispatches of push notifications, post-payment event processing, and audit log tracking. We evaluated message queuing options including Apache Kafka, RabbitMQ, and AWS SQS.

## Decision
We selected **RabbitMQ** as the primary message broker due to its mature support for complex AMQP routing patterns (Topic Exchanges), low-latency message delivery, lightweight resource footprint, and ease of local container deployment.

## Consequences

### Positive
- **Flexible Routing:** Flexible Topic Exchanges allow publishing events once and routing to multiple queues based on pattern matching.
- **Reliable Delivery:** Native support for consumer acknowledgments, publisher confirms, and Dead Letter Exchanges.
- **Low Overhead:** Operates with lower memory and setup overhead compared to Apache Kafka clusters for transactional messaging.

### Negative
- Not designed as a permanent event log (unlike Kafka log retention).
- Requires monitoring queue depths to prevent memory overflow during consumer outages.
