# STRIDE Cheat Sheet

STRIDE categories (plain-English):

- **Spoofing**: attacker pretends to be someone/something else (identity/authentication)
- **Tampering**: attacker modifies data or code (integrity)
- **Repudiation**: attacker denies actions; system can’t prove otherwise (non-repudiation)
- **Information Disclosure**: data exposed to unauthorized parties (confidentiality)
- **Denial of Service (DoS)**: system becomes unavailable/unusable (availability)
- **Elevation of Privilege**: gain permissions beyond what should be allowed (authorization)

Quick prompts:
- Where does identity come from? Can it be faked?
- Where do we trust user input? Can it be modified?
- What actions need audit logs?
- What data must not leak?
- What endpoints can be overwhelmed?
- Where are roles/permissions checked?
