# 12 - Docker Architecture

## Overview
Together-Wifi uses Docker for containerization and local service orchestration to guarantee environment consistency across development, testing, and production.

---

## 1. Container Setup

The microservice stack is orchestrated locally using Docker Compose ([docker-compose.yml](file:///C:/Users/ALPHA_JUNIOR/Desktop/Together-Wifi/backend/docker/docker-compose.yml)).

### Service Inventory

| Container Name | Base Image | Internal Port | Host Port | Function |
| :--- | :--- | :--- | :--- | :--- |
| `together-postgres` | `postgres:16` | 5432 | 5432 | Primary Relational Database |
| `together-rabbitmq` | `rabbitmq:3-management` | 5672, 15672 | 5672, 15672 | AMQP Message Broker & Management UI |
| `together-redis` | `redis:7-alpine` | 6379 | 6379 | In-memory Cache & Key-value store |
| `together-pgadmin` | `dpage/pgadmin4` | 80 | 5050 | Database Administration UI |

---

## 2. Docker Network Architecture

All containers communicate over an isolated bridge network named `together-network`.

```
                    +------------------------------------+
                    |        together-network            |
                    |                                    |
  +-----------------+-----------------+------------------+-----------------+
  |                 |                 |                  |                 |
  v                 v                 v                  v                 v
[postgres]     [rabbitmq]          [redis]           [pgadmin]      [gateway/services]
(Port 5432)   (Ports 5672/15672)  (Port 6379)       (Port 5050)
```

---

## 3. Environment & Secrets Management
- Environment configurations are supplied via `.env` in `backend/docker/`.
- Default fallback parameters are configured inside `docker-compose.yml` to ensure graceful initialization without missing variables.

---

## 4. Multi-Stage Builds
Microservice Dockerfiles employ multi-stage builds:
1. **Build Stage:** Installs full dependencies, runs TypeScript compilation / build scripts.
2. **Production Stage:** Copies only compiled artifacts and production dependencies into lightweight Alpine Linux runtime images to minimize security attack surfaces and image size.
