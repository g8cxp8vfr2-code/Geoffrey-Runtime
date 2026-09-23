# Geoffrey Runtime

> A governed personal automation runtime for Apple Shortcuts and AI orchestration.

## Overview

Geoffrey Runtime is a deterministic automation platform built on Apple Shortcuts. It combines rule-based execution with optional AI assistance to create a reliable, auditable, and extensible personal automation system.

Unlike traditional smart home automations that connect devices directly together, Geoffrey Runtime routes every request through a governed runtime where requests can be validated, logged, approved, executed, and audited.

The goal is simple:

**Every request has a beginning, a decision, an execution, and a receipt.**

---

# Core Principles

- Deterministic first
- AI only when needed
- Every request is logged
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

## AI Orchestration

When deterministic routing cannot resolve a request, Geoffrey Runtime can optionally send the request to an AI model for interpretation.

The AI returns structured data which is validated before execution.

AI never directly controls devices.

---

# Architecture

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

Every automation becomes part of a governed runtime where requests are validated, logged, executed, and documented.

The objective is to make personal automation predictable, maintainable, and extensible over time.
