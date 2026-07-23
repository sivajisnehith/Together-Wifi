# ADR-001: API Gateway Routing Strategy

## Status
Accepted

## Context

The API Gateway needs to route requests to backend microservices.

Spring Cloud Gateway supports two primary approaches:
- YAML configuration
- Java RouteLocator configuration

## Decision

Use YAML-based route configuration for Together WiFi.

## Rationale

- Routes are static.
- Easy to read.
- Easy to maintain.
- Environment-specific values can be externalized.
- Widely used in Spring Boot microservice projects.

## Consequences

- Route behavior remains configuration-driven.
- Dynamic routing can be introduced later if needed using Java configuration.