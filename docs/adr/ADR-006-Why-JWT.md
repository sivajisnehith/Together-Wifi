# ADR 006: Selection of JSON Web Tokens (JWT) for Authentication

## Status
**Accepted**

## Context
In a microservices architecture, authenticating every incoming request by querying a central database for session state creates bottleneck latency and introduces a single point of failure across services.

## Decision
We adopted **JSON Web Tokens (JWT)** paired with a dual-token strategy (Short-lived Access Tokens + Long-lived Refresh Tokens).

## Consequences

### Positive
- **Stateless Verification:** Microservices can verify incoming Access Token signatures independently using a public key / shared secret without calling the database.
- **Cross-Platform Compatibility:** JWTs are standard standards RFC 7519 easily consumed by mobile (Flutter) and backend APIs.
- **Enhanced Security:** Short 15-minute token lifespan minimizes risk if an access token is compromised.

### Negative
- Revoking active JWTs before expiration requires a Redis-backed token blacklist.
- Token payload size increases HTTP header size slightly compared to raw opaque session keys.
