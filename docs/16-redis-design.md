# 16 - Redis Design

## Overview
Together-Wifi utilizes Redis 7 as an in-memory key-value cache, session store, rate limiting counter, and real-time state manager.

---

## 1. Key Use Cases & Data Models

### A. Rate Limiting
- **Key Pattern:** `ratelimit:{ip}:{endpoint}` or `ratelimit:{userId}:{endpoint}`
- **Type:** String / Sliding Window Sorted Set
- **TTL:** 60 seconds
- **Purpose:** Protects API Gateway against brute force logins and resource exhaustion.

### B. Session & Token Management
- **Key Pattern:** `session:{userId}:{sessionId}`
- **Type:** Hash
- **TTL:** 15 minutes to 7 days
- **Fields:** `ip`, `userAgent`, `lastActive`, `deviceToken`

- **Key Pattern:** `blacklist:jwt:{jti}`
- **Type:** String (`1`)
- **TTL:** Remaining lifetime of revoked access token
- **Purpose:** Instant token invalidation upon user logout.

### C. Active Hotspot Caching
- **Key Pattern:** `hotspot:active:{hotspotId}`
- **Type:** Hash
- **TTL:** 5 minutes
- **Purpose:** Fast lookup of online WiFi hotspots without hitting PostgreSQL database.

### D. Geospatial Indexing
- **Key Pattern:** `geo:hotspots`
- **Type:** GEO (Geospatial Index using Sorted Sets)
- **Commands:** `GEOADD`, `GEOSEARCH` (Radius-based lookup for nearby hotspots)
- **Purpose:** Sub-millisecond geographic proximity search for mobile clients.

---

## 2. Eviction Policy & Memory Strategy
- **Eviction Policy:** `allkeys-lru` (Least Recently Used) to prevent Out-Of-Memory (OOM) crashes under heavy load.
- **Persistence:** RDB (Redis Database snapshots) for fast startup recovery + AOF (Append Only File) configured for durability.
- **High Availability:** Redis Sentinel / AWS ElastiCache Multi-AZ replication with automatic failover.
