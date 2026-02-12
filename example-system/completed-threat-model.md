# Completed Example Threat Model: Hackathon Submissions Web App

> **Purpose:** Demonstrate a lightweight, hackathon-friendly STRIDE threat model for a typical web app.

## 1) What are we working on?

### High-level description
A web application where users can register/login, submit a project, and view submissions. Admins can moderate submissions.

### System components
- **User browser** (frontend)
- **Web frontend** (serves UI)
- **Backend API** (business logic)
- **Database** (users + submissions)
- **OAuth provider** (optional external identity)

### Data Flow Diagram (Mermaid)
```mermaid
flowchart LR
  user[User (Browser)] -->|HTTPS| web[Web Frontend]
  web -->|API calls (HTTPS)| api[Backend API]
  api -->|SQL| db[(Database)]
  api -->|OAuth redirect| idp[OAuth Provider]

  subgraph TB1[Trust Boundary: Public Internet]
    user
    idp
  end

  subgraph TB2[Trust Boundary: App Infrastructure]
    web
    api
    db
  end
```

### Assets (what we protect)
- **User accounts** (identity, sessions)
- **User emails** (personal data)
- **Submission content** (may include sensitive info)
- **Admin privileges** (ability to remove/hide submissions)
- **Availability** (app stays up during judging)

### Entry points
- Login/signup endpoints
- Submission create/update endpoint
- Submission view/list endpoint
- Admin moderation endpoints

### Trust boundaries
- Public internet ↔ app infrastructure
- Third-party identity provider ↔ app infrastructure (if used)

### Assumptions
- Traffic uses HTTPS
- Secrets are not committed to the repo
- The demo app is not intended for production use

---

## 2) What can go wrong? (STRIDE)

Below is **one representative threat per STRIDE category** plus mitigations.

### S — Spoofing (identity/authentication)
**Threat ID:** S1

**Scenario:** An attacker gains access as another user (e.g., by stealing a session token/cookie from an insecure client, or by using weak login controls).

**Impact:** Unauthorized access to accounts and submissions.

**Mitigations (hackathon-sized):**
- Use a reputable auth mechanism (OAuth/OIDC) or enforce strong passwords.
- Secure session cookies: `HttpOnly`, `Secure`, `SameSite`.
- Short session lifetime; rotate session identifiers on login.

**Mitigations (post-hackathon):**
- Add MFA for admins.
- Add device/session management and anomaly detection.

---

### T — Tampering (integrity)
**Threat ID:** T1

**Scenario:** A user tampers with client-side requests (e.g., changes `userId` or `isAdmin` fields in a submission POST) to alter data they shouldn’t.

**Impact:** Unauthorized modification of submissions or privilege flags.

**Mitigations (hackathon-sized):**
- Never trust client input for ownership/roles; derive `userId` from the authenticated session on the server.
- Server-side validation (schema) for request bodies.
- Use parameterized queries / ORM to prevent dangerous query construction.

**Mitigations (post-hackathon):**
- Add integrity checks for critical records (e.g., immutable audit trail for moderation actions).

---

### R — Repudiation (non-repudiation/accountability)
**Threat ID:** R1

**Scenario:** A user or admin denies performing a sensitive action (e.g., deleting/hiding a submission), and the system can’t prove what happened.

**Impact:** Disputes, loss of trust, inability to investigate incidents.

**Mitigations (hackathon-sized):**
- Add audit logs for: login, create/update/delete submissions, admin moderation.
- Log: actor (user id), action, timestamp, target record id, request id.

**Mitigations (post-hackathon):**
- Centralized log storage + retention.
- Tamper-evident logging for high-risk actions.

---

### I — Information Disclosure (confidentiality)
**Threat ID:** I1

**Scenario:** Insecure Direct Object Reference (IDOR): a user accesses another user’s submission by guessing an ID, or the API returns too much data (e.g., emails) in responses.

**Impact:** Exposure of private submissions or personal data.

**Mitigations (hackathon-sized):**
- Enforce authorization on every read: user can only read their own private submissions unless marked public.
- Minimize API responses (don’t return email unless needed).
- Avoid verbose error messages in production mode.

**Mitigations (post-hackathon):**
- Data classification + automated checks in code review.
- Add security tests for authorization rules.

---

### D — Denial of Service (availability)
**Threat ID:** D1

**Scenario:** An attacker (or an accidental script) floods the list/search endpoints or uploads huge payloads, degrading the app during judging.

**Impact:** App becomes slow/unavailable; demo fails.

**Mitigations (hackathon-sized):**
- Add rate limiting per IP/user for key endpoints.
- Add request body size limits.
- Paginate list endpoints and set timeouts.

**Mitigations (post-hackathon):**
- Caching for read-heavy endpoints.
- Autoscaling and WAF/CDN protections.

---

### E — Elevation of Privilege (authorization)
**Threat ID:** E1

**Scenario:** Missing or inconsistent RBAC checks allow a normal user to call admin endpoints (e.g., `/admin/hideSubmission`).

**Impact:** Unauthorized moderation or takeover of the system’s control functions.

**Mitigations (hackathon-sized):**
- Centralize authorization in middleware (deny-by-default).
- Separate admin routes and require an `admin` role claim.
- Add a simple integration test verifying non-admin cannot access admin endpoints.

**Mitigations (post-hackathon):**
- Fine-grained authorization (scopes/permissions).
- Privileged access monitoring.

---

## 3) What are we going to do about it? (prioritized plan)

### Top 5 mitigations (feasible during hackathon)
1) Add server-side authorization checks for reads/writes (prevents IDOR + EoP)
2) Ensure server derives ownership from session (prevents tampering)
3) Secure sessions/cookies and basic auth hardening (reduces spoofing)
4) Add basic audit logging for sensitive actions (repudiation)
5) Add rate limiting + pagination (availability)

## 4) Did we do a good enough job?
- [x] DFD exists with trust boundaries
- [x] At least 1 threat per STRIDE category
- [x] Mitigations mapped to threats and hackathon-feasible
- [ ] Owners assigned (depends on team)
