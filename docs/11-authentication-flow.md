# 11 - Authentication Flow

## Overview
Together-Wifi uses a dual-token authentication scheme leveraging short-lived Access Tokens (JWT) and long-lived Refresh Tokens to balance security with seamless user experience.

---

## 1. User Registration & Login Flow

```
Mobile App                  API Gateway               Auth Service               PostgreSQL
    |                            |                         |                         |
    |--- POST /auth/login ------>|                         |                         |
    |                            |--- Forward Request ---->|                         |
    |                            |                         |--- Query User Record -->|
    |                            |                         |<-- User & Password Hash-|
    |                            |                         |                         |
    |                            |                         | [Verify Password Hash]  |
    |                            |                         | [Generate Access JWT]   |
    |                            |                         | [Generate Refresh Token]|
    |                            |                         |                         |
    |                            |                         |--- Store Refresh Token->|
    |                            |<-- Return Tokens -------|                         |
    |<-- 200 OK (Tokens) --------|                         |                         |
```

---

## 2. Token Specifications

### Access Token
- **Lifetime:** 15 minutes
- **Storage:** Memory (Mobile client state)
- **Payload:** `userId`, `email`, `role`, `exp`, `iat`
- **Signing:** HMAC-SHA256 (HS256) or RSA-256 (RS256) with private key

### Refresh Token
- **Lifetime:** 7 to 30 days
- **Storage:** Encrypted Secure Storage on Mobile / HttpOnly Cookie on Web
- **Payload:** Cryptographically random UUID string associated with `userId` and device metadata.

---

## 3. Token Refresh Mechanism

When the short-lived Access Token expires (HTTP 401 response from API Gateway):
1. The Mobile App intercepts the 401 error transparently.
2. Sends a POST request to `/auth/refresh` with the stored Refresh Token.
3. Auth Service validates the Refresh Token against the stored hash in the database / Redis.
4. If valid, a new Access Token (and rotated Refresh Token) is returned.
5. The original failed request is automatically retried with the new Access Token.

---

## 4. Logout & Token Revocation
1. Client calls `POST /auth/logout`.
2. Auth Service deletes the Refresh Token from the database.
3. The current Access Token ID (`jti`) is added to a Redis revocation blacklist with a TTL equal to the token's remaining lifespan.
4. Future API calls with the blacklisted Access Token are rejected by the API Gateway.
