# Geoffrey Runtime

> A governed personal automation runtime built with Apple Shortcuts and AI.

Geoffrey Runtime is a modular automation runtime designed to provide deterministic execution, structured request handling, scheduling, logging, and AI-assisted orchestration. Every request entering the runtime follows a versioned schema, making execution predictable, auditable, and easier to maintain as the system evolves.

---

# Why Geoffrey Runtime?

Most home automation focuses on executing commands.

Geoffrey Runtime focuses on governing them.

Rather than allowing every automation to execute independently, Geoffrey Runtime introduces a runtime layer that standardizes requests, validates data, records execution history, and coordinates automation services through reusable runtime components.

The goal is to bring software engineering principles such as versioning, middleware, logging, scheduling, and deterministic execution to Apple Shortcuts.

---

# Features

- Structured request wrapping
- Deterministic runtime execution
- Runtime logging
- Local scheduler
- Notification services
- Receipt generation
- Versioned schemas
- AI-assisted intent resolution
- Apple Home integration
- Apple Reminders scheduling
- Apple Messages communication
- Modular runtime components

---

# Runtime Architecture

```text
                 User
                   │
                   ▼
          Wrap Request V1
                   │
                   ▼
          Geoffrey Runtime
                   │
     ┌─────────────┼─────────────┐
     │             │             │
     ▼             ▼             ▼
 Scheduler     Notifications   Logging
     │             │             │
     └─────────────┼─────────────┘
                   │
                   ▼
           Runtime Services
                   │
                   ▼
 Apple Home • Tesla • Radio • Scenes
```

---

# Repository Structure

```text
GeoffreyRuntime/

├── README.md
├── docs/
├── schemas/
├── shortcuts/
├── examples/
└── images/
```

---

# Runtime Components

| Component | Purpose |
|-----------|---------|
| Wrap Request V1 | Standardizes incoming requests |
| Contact Geoffrey V1 | Sends requests into Geoffrey Runtime |
| Geoffrey Scheduler Local V1 | Executes scheduled tasks |
| Notify This V1 | Displays runtime notifications |
| Log This V1 | Records runtime events |

---

# Runtime Principles

Every Geoffrey Runtime request follows the same lifecycle.

1. Receive the request.
2. Wrap the request.
3. Validate the request.
4. Execute the request.
5. Generate a receipt.
6. Record the event.
7. Return the result.

These principles make runtime behavior predictable, testable, and easier to troubleshoot.

---

# Technologies

- Apple Shortcuts
- Apple Home
- Apple Reminders
- Apple Messages
- iCloud Drive
- JSON
- Markdown

---

# Current Status

**Version:** 1.0

Current focus:

- Runtime stabilization
- Documentation
- Schema versioning
- Additional runtime services

---

# Vision

Geoffrey Runtime is an exploration of what a governed personal automation runtime can become.

The long-term vision is a platform capable of coordinating local automation, scheduling, AI-assisted workflows, and smart home services through a consistent runtime architecture while remaining transparent, deterministic, and extensible.

---

# License

This repository is shared as a portfolio project for educational and demonstration purposes.