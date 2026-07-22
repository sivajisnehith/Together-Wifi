# 10 - Security Architecture

## Overview
Together-Wifi incorporates end-to-end security measures across data transmission, authentication, container runtime, and infrastructure isolation.

---

## 1. Network & Infrastructure Security
- **TLS/SSL Encryption:** All client-to-gateway communication is encrypted using HTTPS/WSS (TLS 1.3).
- **VPC Isolation:** AWS resources reside inside private subnets; only the API Gateway and ALB are publicly exposed.
- **Firewall & Security Groups:** Database (PostgreSQL), cache (Redis), and message broker (RabbitMQ) ports are strictly blocked from external public access.

---

## 2. Authentication & Authorization
- **JWT (JSON Web Tokens):** Short-lived Access Tokens (15 min) paired with cryptographically secure Refresh Tokens stored in HTTP-Only secure cookies or mobile secure storage.
- **Role-Based Access Control (RBAC):** Permissions are partitioned into roles (`USER`, `PROVIDER`, `ADMIN`).
- **Token Invalidation:** Redis-based token blacklist for instant logout and session revocation.

---

## 3. Data Protection & Cryptography
- **Password Hashing:** Passwords hashed using `bcrypt` with salt rounds >= 12 or `Argon2id`.
- **Sensitive Data at Rest:** Encryption at rest for PostgreSQL (AWS RDS Storage Encryption using KMS).
- **Secrets Management:** Environment variables, API keys, and database passwords are injected via AWS Secrets Manager or secure `.env` runtime configurations (never hardcoded in repositories).

---

## 4. API & Application Hardening
- **Rate Limiting:** Protects endpoints against brute-force and Denial-of-Service (DoS) attacks via Redis-backed sliding window rate limiters.
- **CORS Policies:** Restrict cross-origin resource sharing strictly to trusted domains.
- **Input Validation & Sanitization:** Strict request validation (e.g., Joi / Zod / class-validator) to prevent SQL Injection (SQLi), Cross-Site Scripting (XSS), and Command Injection.
- **Security Headers:** Express Helmet integration enforcing CSP, HSTS, X-Frame-Options, and X-Content-Type-Options.

---

## 5. Security Auditing & Logging
- **Centralized Audit Logging:** Sensitive actions (logins, password changes, payout requests) emit structured audit logs.
- **Dependency Scanning:** Automated vulnerability scanning of npm/Dart dependencies via GitHub Dependabot.
