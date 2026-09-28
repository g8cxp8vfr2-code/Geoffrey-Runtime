# Geoffrey Runtime

> A governed personal automation runtime for Apple Shortcuts and AI orchestration.

## Overview

Geoffrey Runtime is a deterministic automation platform built on Apple Shortcuts. It combines rule-based execution with optional AI assistance to create a reliable, auditable, and extensible personal automation system.

Unlike traditional smart home automations that connect devices directly together, Geoffrey Runtime provides a governed path where requests can be validated, logged, approved, executed, and audited. Some explicitly local capabilities, including Free Radio, execute on the customer device first and may then report a receipt or status event to Jackson-West.

The goal is simple:

**Every governed request has a beginning, a decision, an execution, and a receipt. Local execution is reported as local execution, not recast as governance.**

---

# Core Principles

- Deterministic first
- AI only when needed
- Every governed request is logged
- Reported local actions retain receipt/status evidence
- Every action is validated
- Every execution returns a result
- Architecture over shortcuts
- Modular components
- Portable design

---

# Current Features

## Request Intake

- Voice requests
- Button requests
- Wrapped requests
- Request IDs
- Timestamping
- User identification
- Device identification

## Validation

- Input validation
- Required parameter checking
- Approved action verification
- Registry lookups
- Failure handling

## Logging

- Request logging
- Execution logging
- Success logging
- Failure logging
- Notification logging
- Runtime receipts

## Runtime

- Radio control
- Tesla control
- Home scenes
- Announcements
- Vacuum control
- State management
- Runtime locks

The Radio V1 execution boundary and public contract are documented in [`docs/radio-v1.md`](docs/radio-v1.md) and [`schemas/radio-v1.md`](schemas/radio-v1.md).

## AI Orchestration

When deterministic routing cannot resolve a request, Geoffrey Runtime can optionally send the request to an AI model for interpretation.

The AI returns structured data which is validated before execution.

AI never directly controls devices.

---

# Architecture

The flow below is the governed path. Free Radio is a separate local-first lane: the customer device executes the action, then sends a receipt or status update where configured. A local receipt is not a new governed request.

```
Voice
Buttons
Schedules
Calendar
Messages
        │
        ▼
Wrap Request
        │
        ▼
Request Intake
        │
        ▼
Validation
        │
        ▼
Policy Checks
        │
        ▼
Executor
        │
        ▼
Device
        │
        ▼
Receipt
        │
        ▼
Logging
```

---

# Design Goals

Geoffrey Runtime is designed to be:

- Reliable
- Deterministic
- Modular
- Expandable
- Auditable
- Safe
- Human understandable

---

# Repository Structure

```
docs/
examples/
runtime/
schemas/
shortcuts/
```

---

# Version

Current Version:

**Runtime V1**

Current capabilities include:

- Request wrapping
- Structured logging
- Runtime validation
- Local execution
- Local execution receipts/status
- AI fallback
- Notification system
- Runtime locking
- State management

---

# Roadmap

Future versions will include:

- Plugin architecture
- Customer configuration
- Runtime updates
- Cloud synchronization
- Multi-home support
- Additional executors
- Expanded AI orchestration

---

# Philosophy

Geoffrey Runtime treats automation as software engineering instead of isolated automations.

Governed automations are validated, logged, executed, and documented by the runtime. Explicitly local capabilities retain their local execution boundary and may publish post-execution status without claiming that Jackson-West governed the action.

The objective is to make personal automation predictable, maintainable, and extensible over time.
