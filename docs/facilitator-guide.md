# Facilitator Guide

## Ground rules
- Design-focused and defensive
- No attacking anything during the workshop

## Workflow
1) **Diagram**: Build a DFD and mark trust boundaries
2) **Identify**: Apply STRIDE to elements/flows
3) **Mitigate**: Pick realistic controls
4) **Validate**: Did we cover all STRIDE categories and key assets?

## Helpful prompts
- What happens if someone pretends to be a user?
- What if someone modifies requests? Are we validating server-side?
- Can someone deny doing an action? Do we have logs?
- What sensitive data exists? How is it protected?
- What endpoints can be spammed? Any rate limiting?
- Where do we enforce RBAC? Are admin actions protected?
