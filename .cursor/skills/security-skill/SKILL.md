---
name: security-skill
description: Enforce secure coding practices for frontend and backend work, including secret management with .env files, input validation, auth/session safety, and dependency hardening. Use when implementing features, reviewing code, or handling configuration that could impact security.
---

# Security Skill

## When to Apply

Apply this skill when the user asks for:
- security improvements or hardening
- authentication, authorization, or session work
- API, form, or database input handling
- environment variable and secret management
- dependency updates and vulnerability fixes
- code reviews focused on security risks

## Non-Negotiable Rules

1. Never hardcode secrets, API keys, tokens, passwords, or private credentials.
2. Never commit secrets into the codebase, including test fixtures and sample files.
3. Store secrets only in environment variables via `.env` files (for local) and secure platform secret managers (for deployed environments).
4. Ensure `.env*` files that contain secrets are gitignored.
5. Commit and maintain `.env.example` with placeholder values only.
6. If a secret is exposed, rotate it immediately and remove it from history if required by policy.

## Secret Management Workflow

1. Add required variables to `.env.example` using non-sensitive placeholders.
2. Read values from `process.env` (or framework equivalent) and fail fast when required variables are missing.
3. Keep separate values per environment (`development`, `staging`, `production`).
4. Do not print secrets in logs, error messages, analytics, or browser console.
5. Use short-lived tokens when possible; avoid long-lived static credentials.

## Input and Data Validation

- Treat all input as untrusted (query params, form fields, headers, cookies, uploaded files).
- Validate and sanitize input at API boundaries with strict schemas.
- Enforce type, length, range, and format constraints.
- Reject unexpected fields to prevent mass-assignment style bugs.
- Escape or encode untrusted data before rendering to avoid XSS.

## Auth, Session, and Access Control

- Enforce authorization checks on every protected action (server-side, not UI-only).
- Apply least privilege for roles and permissions.
- Use secure cookie settings for sessions (`HttpOnly`, `Secure`, `SameSite`).
- Implement session timeout and token expiration/refresh policy.
- Protect auth endpoints against brute force with throttling/rate limits.

## Frontend Security Baseline

- Avoid `dangerouslySetInnerHTML` unless absolutely required and sanitized.
- Keep user tokens out of localStorage when safer cookie-based approaches are available.
- Do not expose server-only secrets to client bundles.
- Add and maintain restrictive Content Security Policy (CSP) where supported.
- Use safe defaults for links (`rel="noopener noreferrer"` for external targets).

## API and Backend Security Baseline

- Use parameterized queries/ORM safeguards; never interpolate raw user input into SQL.
- Return generic auth errors to avoid account/user enumeration.
- Protect sensitive routes with authentication + authorization middleware.
- Limit payload size and upload type/size to reduce abuse risk.
- Add CSRF protection where cookie-authenticated state-changing requests are used.

## Transport and Infrastructure

- Enforce HTTPS in all non-local environments.
- Set security headers (`X-Content-Type-Options`, `X-Frame-Options` or `frame-ancestors`, `Referrer-Policy`).
- Disable debug features and verbose error leaks in production.
- Restrict CORS origins to explicit allowlists; avoid wildcard origins with credentials.

## Dependency and Supply-Chain Hygiene

- Prefer maintained packages from trusted sources.
- Run dependency audits regularly and patch critical/high issues quickly.
- Remove unused dependencies and lock versions appropriately.
- Review install scripts and high-risk package changes before merging.

## Logging, Monitoring, and Incident Readiness

- Log security-relevant events (auth failures, permission denials, suspicious spikes).
- Redact personal/sensitive fields in logs.
- Configure alerts for unusual auth and traffic behavior.
- Maintain a basic incident response path: detect, contain, rotate, recover, review.

## Security Review Checklist

Before finalizing changes, verify:
- [ ] No secrets or credentials were added to tracked files
- [ ] `.env.example` is updated with placeholders for new config
- [ ] Input validation exists at trust boundaries
- [ ] Auth + authorization are both enforced for protected operations
- [ ] No obvious XSS, CSRF, injection, or IDOR exposure
- [ ] Error responses avoid leaking sensitive internals
- [ ] Security headers/CORS/session settings match policy
- [ ] Dependency changes do not introduce known critical risks
