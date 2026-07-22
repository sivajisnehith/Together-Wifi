# ADR 004: Adoption of Redis for Caching and Session Management

## Status
**Accepted**

## Context
High-frequency read requests (such as rate limit checking, active user session validation, JWT revocation lists, and nearby hotspot geographical lookup) would severely strain the primary PostgreSQL relational database if queried directly on every HTTP request.

## Decision
We chose **Redis** as our in-memory data store for response caching, token blacklisting, rate limiting counters, and geospatial indexing.

## Consequences

### Positive
- **Sub-millisecond Latency:** In-memory key-value lookups provide ultra-fast response times.
- **Built-in Geo-spatial Indexing:** Native `GEOSEARCH` commands streamline radius-based hotspot queries.
- **Sliding Window Rate-Limiting:** Enables efficient sliding-window rate limiters at the API Gateway layer.

### Negative
- Volatile memory storage requires eviction policies and optional RDB/AOF persistence configuration to avoid data loss on restarts.
- Memory consumption must be monitored to keep dataset sizes within allocated RAM limits.
