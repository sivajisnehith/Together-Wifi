# 14 - CI/CD Pipeline

## Overview
Together-Wifi uses GitHub Actions to automate Continuous Integration (CI) and Continuous Deployment (CD). Every code push and pull request undergoes automated linting, unit testing, container build validation, and deployment.

---

## 1. Pipeline Stages

```
   [ Code Commit / PR ]
            |
            v
+-----------------------+
|  Stage 1: Lint & Test | ---> Static Analysis, Unit & Integration Tests
+-----------+-----------+
            |
            v
+-----------------------+
| Stage 2: Build Images | ---> Multi-stage Docker Builds
+-----------+-----------+
            |
            v
+-----------------------+
| Stage 3: Registry Push| ---> Push to Amazon ECR / GitHub Container Registry
+-----------+-----------+
            |
            v
+-----------------------+
|  Stage 4: Deployment  | ---> Rolling Update on AWS ECS / Server Deployment
+-----------------------+
```

---

## 2. Workflow Triggers

- **Pull Requests (main / develop):** Triggers Stage 1 (Linting & Unit Tests).
- **Push to `develop`:** Triggers Stage 1 & 2, deploys to Staging Environment.
- **Push to `main` (or Release Tag):** Triggers full pipeline and deploys to Production Environment.

---

## 3. GitHub Actions Jobs

### `lint-and-test.yml`
- Setup Node.js / Java / Dart environments.
- Run code linters (`eslint`, `flutter analyze`).
- Run unit test suites with coverage reports (`jest`, `flutter test`).

### `build-and-push.yml`
- Log in to Amazon Elastic Container Registry (ECR).
- Build tagged Docker images for each microservice using Docker layer caching.
- Vulnerability scan Docker images using Trivy.
- Push images to ECR.

### `deploy-aws.yml`
- Update AWS ECS task definitions with new container image tags.
- Execute rolling deployment with zero downtime (`aws ecs update-service`).
- Run database migrations before completing deployment.
