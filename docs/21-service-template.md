# Together WiFi - Microservice Template

## Purpose

This document defines the standard structure and conventions for every backend microservice in the Together WiFi project.

All developers must follow this template to ensure consistency across the project.

---

# Technology Stack

| Technology | Version |
|------------|---------|
| Java | 21 |
| Spring Boot | 3.4.3 |
| Maven | Latest Stable |
| Database | PostgreSQL |
| Configuration | YAML |
| Packaging | Jar |

---

# Project Metadata

Example:

Group

com.togetherwifi

Artifact

wifi-service

Package

com.togetherwifi.wifi

---

# Required Dependencies

Every business microservice must include:

- Spring Web
- Spring Data JPA
- PostgreSQL Driver
- Validation
- Lombok
- Spring Boot Actuator
- Spring Boot Test

Do NOT include unless required:

- Spring Security
- JWT
- Redis
- RabbitMQ
- OpenFeign
- Docker-specific libraries

---

# Standard Package Structure

com.togetherwifi.<service>

├── controller
├── service
├── repository
├── entity
├── dto
│   ├── request
│   └── response
├── mapper
├── exception
├── config
├── validation
└── <ServiceName>Application.java

Packages should only be created when needed.

---

# application.yml

Example:

spring:
  application:
    name: wifi-service

server:
  port: 8082

---

# Standard Ports

| Service | Port |
|----------|------|
| API Gateway | 8080 |
| Auth Service | 8081 |
| WiFi Service | 8082 |
| Location Service | 8083 |
| Payment Service | 8084 |
| Review Service | 8085 |
| Session Service | 8086 |
| Notification Service | 8087 |

---

# Coding Standards

- Follow SOLID Principles.
- Use constructor injection.
- Use DTOs.
- Validate request bodies.
- Do not expose entities directly.
- Use meaningful package names.
- Follow REST naming conventions.
- Use Global Exception Handling.
- Add logging where appropriate.

---

# Development Workflow

For every feature:

1. Design
2. Database Schema
3. Entity
4. Repository
5. Service
6. Controller
7. Validation
8. Unit Tests
9. Documentation
10. Git Commit

No feature is considered complete until all steps are finished.

---

# Definition of Done

A service is considered production-ready when:

- Builds successfully
- Starts without errors
- Uses standard package structure
- Uses standard port
- Uses application.yml
- Includes validation
- Includes logging
- Includes exception handling
- Includes unit tests
- API documented


## Infrastructure Service Package Structure

API Gateway

com.togetherwifi.gateway
├── config
├── constant
├── exception
├── filter
├── security
└── util

Business Services

com.togetherwifi.auth
├── controller
├── service
├── repository
├── entity
├── dto
├── mapper
├── config
├── exception
└── util