# 18 - Development Guidelines

## Overview
These guidelines establish coding standards, Git workflow rules, and best practices for all engineers working on Together-Wifi.

---

## 1. Git Workflow & Branching Model

### Branching Naming Convention
- `feature/<feature-name>` (e.g. `feature/jwt-refresh-token`)
- `bugfix/<issue-name>` (e.g. `bugfix/redis-connection-timeout`)
- `hotfix/<critical-fix>` (e.g. `hotfix/payment-webhook-signature`)

### Commit Message Rules (Conventional Commits)
- `feat: add geo-radius search to wifi service`
- `fix: resolve null reference in user profile handler`
- `docs: update docker compose guide`
- `test: add unit test for payment settlement calculation`

---

## 2. Code Standards & Style

### General Rules
- Keep functions small, focused, and single-purpose.
- Prefer explicit variable and parameter types.
- Never commit secrets, passwords, or API keys. Use `.env` files.

### Language Specific Guidelines
- **JavaScript/TypeScript:** Enforce ESLint + Prettier rules.
- **Dart (Flutter):** Enforce `flutter analyze` lint rules; follow Effective Dart guidelines.
- **SQL / Migrations:** Use versioned database migrations (e.g. Knex / Flyway / TypeORM migrations); never alter production tables manually.

---

## 3. Pull Request (PR) Checklist
Before submitting a PR:
- [ ] Code compiles and passes all local linters.
- [ ] New code includes corresponding unit or integration tests.
- [ ] All existing tests pass cleanly.
- [ ] Relevant documentation updated in `docs/`.
- [ ] Requires approval from at least 1 team reviewer before merging to `develop` or `main`.
