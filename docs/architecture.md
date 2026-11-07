# Architecture v0.1 — NusanCode

## Deployment View
```mermaid
flowchart TB
    I[Internet] --> F[UFW Firewall]
    F --> C[Caddy :80]
    C --> G[Gunicorn 127.0.0.1:8000]
    G --> A[Flask Application]
    A --> D[(SQLite Database)]
