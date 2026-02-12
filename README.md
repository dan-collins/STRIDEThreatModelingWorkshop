# STRIDE Threat Modeling Workshop (Hackathon Edition)

Threat modeling is a methodical review of a system design to discover design-level security problems early. Microsoft uses **STRIDE** to categorize common threat types: **Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege**.

**This workshop is defensive and design-focused.** We will not exploit systems; we will identify design risks and plan mitigations.

## Outcomes (what you'll produce)
By the end, your team will have:
1) A simple Data Flow Diagram (DFD) + trust boundaries
2) A STRIDE threat register with at least 1 threat per category (S/T/R/I/D/E)
3) A short mitigation plan: “Top 5 fixes we can realistically do during the hackathon”

## Agenda (60–90 minutes)
- 10 min: What is STRIDE + why DFDs/trust boundaries matter
- 15 min: Diagram your system (DFD)
- 25 min: Apply STRIDE to your diagram and record threats
- 15 min: Prioritize and pick mitigations
- 5–15 min: Share-outs + “how to explain this to judges”

## Start here
- `templates/threat-model-template.md`
- `templates/threat-register.csv`
- `docs/stride-cheatsheet.md`
- `docs/how-to-dfd.md`

## Optional tooling
You can do this with pen & paper, Mermaid diagrams, or OWASP Threat Dragon.
