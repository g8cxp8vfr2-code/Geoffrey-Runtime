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
- Every governed action is validated at the Jackson-West boundary; local Radio remains customer-editable
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

### Radio V1 — architecture frozen

Radio V1 completed its architecture/readiness review. Its official architecture is **local-first**, with Global Lock / Jackson-West access defaulting to **false/off**. Free Radio executes locally without Jackson-West governance. Actions are **Play, Stop, Back, and Next**; volume, pause, and resume are outside V1.

Play selects a station and one or more outputs and invokes the appropriate local helper Shortcuts. The complete product relationship is **Geoffrey Runtime Radio → Radio controller → Radio Stations → Speakers/outputs → Global Lock → optional Jackson-West service**. Stations and Speakers are required installation components with separate packaging/publishing; unpublished helper downloads are not frozen-engine defects.

The customer-owned Shortcut and `radio.json` registry are intentionally editable, not security boundaries. Jackson-West independently authenticates/authorizes governed requests and is the authoritative security boundary. Local edits or access flags cannot grant server authorization. With Jackson-West enabled, Radio still acts locally first; the later receipt/state report never requests a second execution. Distributable Jackson-West Core and Text Jackson-West customer values are intentionally blank until optional customer onboarding.

Run Radio locally at least once to create its required registry/setup. The public registry bootstraps the interactive path. Server-originated/structured execution before initialization is unsupported in V1. Native media actions labeled Mac during development execute on the customer device and remain subject to device verification.

Install through the permanent [Radio](https://geoffreyruntime.com/radio/install), [Stations](https://geoffreyruntime.com/radio/install/stations), [Speakers](https://geoffreyruntime.com/radio/install/speakers), and [Global Lock](https://geoffreyruntime.com/global-lock/install) pages. Apple download links are replaceable implementation details. The Radio/controller, station, and speaker links still await publication; Global Lock has its existing separate release.

Remaining work is deployment: iPhone/device verification, Stations/Speakers packaging and publishing, website download/content completion, and final customer-install tests. This is not V2 architecture work.

The authoritative frozen architecture and unchanged public contract are documented in [`docs/radio-v1.md`](docs/radio-v1.md) and [`schemas/radio-v1.md`](schemas/radio-v1.md). See [`recent.md`](recent.md) and [`log.md`](log.md) for documentation/deployment status.

## AI Orchestration

When deterministic routing cannot resolve a request, Geoffrey Runtime can optionally send the request to an AI model for interpretation.

The AI returns structured data which is validated before execution.

AI never directly controls devices.

---

# Architecture

The flow below describes the server-governed request path. Free Radio is local-first and does not pass through Jackson-West governance before local execution. Access defaults off. When enabled and configured, the customer device executes the action, then sends a receipt/state report. Jackson-West validates that report without dispatching Radio again. Server-originated Radio uses the initialized local executor after independent server authentication/authorization; pre-initialization structured execution is unsupported in V1.

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
