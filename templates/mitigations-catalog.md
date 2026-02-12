# Mitigations Catalog (menu of options)

## Authentication & Session
- Use an established auth provider (OAuth/OIDC) or strong password auth
- Use secure cookies (HttpOnly, Secure, SameSite)
- Short session lifetimes + refresh tokens (if applicable)

## Authorization
- Centralize RBAC checks (middleware)
- Deny by default; allow explicitly

## Input Validation
- Validate server-side (schema validation)
- Use parameterized queries/ORM to avoid injection classes

## Logging & Audit
- Log security-relevant events: login, create/update/delete, admin actions
- Include who/what/when + request IDs

## Data Protection
- Minimize data returned (least data)
- Encrypt sensitive data at rest (managed services)
- Avoid verbose errors in production

## Availability
- Rate limiting, request size limits
- Timeouts + pagination
- Cache read-heavy endpoints
