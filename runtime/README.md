# Geoffrey Runtime

> A governed personal automation runtime built with Apple Shortcuts and AI.

Geoffrey Runtime is a modular automation runtime designed to provide deterministic execution, structured request handling, scheduling, logging, and AI-assisted orchestration. Governed requests entering the runtime follow versioned contracts. Explicitly local capabilities can instead execute on the customer device and publish a post-execution receipt or status event.

---

# Why Geoffrey Runtime?

Most home automation focuses on executing commands.

Geoffrey Runtime focuses on governing them.

For governed capabilities, Geoffrey Runtime introduces a runtime layer that standardizes requests, validates data, records execution history, and coordinates automation services through reusable runtime components. Explicitly local capabilities keep their documented local boundary.

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

## Radio V1 boundary

**Radio V1 architecture is frozen.** Free Radio executes locally without Jackson-West governance; Global Lock / Jackson-West access defaults false/off. When enabled, the local action still happens first and its subsequent receipt/state report must not dispatch Radio again. Jackson-West independently authenticates/authorizes governed requests at the server boundary. Server-originated execution invokes the initialized customer-device Radio executor; structured execution before the first local run is unsupported.

The interactive path bootstraps `radio.json` from the public registry. The customer-owned Shortcut/registry remain intentionally editable and cannot grant server authorization. Distributable Jackson-West Core and Text Jackson-West customer values stay blank until optional onboarding. Mac media-action labels are development artifacts, not the final execution device.

Radio supports Play, Stop, Back, and Next, with no V1 volume, pause, or resume. Play invokes local station and output helpers. Stations and Speakers are required separate installation components with their own packaging/publishing. Global Lock controls local access; Jackson-West is an optional service. Unpublished helper links are deployment work, not Radio-engine defects. See [`../docs/radio-v1.md`](../docs/radio-v1.md) for the official architecture.

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

Every governed Geoffrey Runtime request follows the lifecycle below.

1. Receive the request.
2. Wrap the request.
3. Validate the request.
4. Execute the request.
5. Generate a receipt.
6. Record the event.
7. Return the result.

These principles make runtime behavior predictable, testable, and easier to troubleshoot.

A local Radio receipt is evidence of a device-reported local action. It is not a second request and does not prove that Jackson-West authorized the local action.

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

Radio V1 architecture/readiness review is complete and frozen. Its remaining work is iPhone/device verification, Stations/Speakers packaging and publishing, completing website installation links/content, and final customer-install testing. This does not assert that every runtime service is frozen. See [`../recent.md`](../recent.md).

---

# Vision

Geoffrey Runtime is an exploration of what a governed personal automation runtime can become.

The long-term vision is a platform capable of coordinating local automation, scheduling, AI-assisted workflows, and smart home services through a consistent runtime architecture while remaining transparent, deterministic, and extensible.

---

# License

This repository is shared as a portfolio project for educational and demonstration purposes.
