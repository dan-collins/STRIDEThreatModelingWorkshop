# How to Draw a DFD (fast)

A Data Flow Diagram (DFD) is a simple picture of:
- **External entities** (users, browsers, third-party services)
- **Processes** (frontend, backend API)
- **Data stores** (database, object storage)
- **Data flows** (requests/responses)
- **Trust boundaries** (where assumptions change, like “internet → server”)

Tips:
- Keep it high-level and readable
- Draw arrows for flows
- Add trust boundaries around “stuff you control” vs “stuff you don’t”

See `example-system/dfd.mmd` for a Mermaid example.
