# Geoffrey Runtime

> Local-first Apple Shortcuts, personal automation, and optional AI orchestration.

This is the official public documentation repository for Geoffrey Runtime. It describes the customer-facing software, documented architecture, and request/receipt contracts. Geoffrey Runtime brings a digital identity, personality, policies, and useful capabilities together.

## Shipped project: Estelle’s Kitchen

[Estelle’s Kitchen](docs/estelles-kitchen/README.md) is a deployed household meal-planning and grocery workflow: a mobile-first recipe experience, scheduled meal updates, and a user-reviewed Apple Shortcuts handoff to a personal Reminders list. Explore the [live Kitchen](https://geoffreyruntime.com/estelles-kitchen/), [architecture](docs/estelles-kitchen/architecture.md), and [engineering case study](docs/estelles-kitchen/engineering-case-study.md).

## Start here

- [Explore Estelle’s Kitchen: deployed project and engineering case study](docs/estelles-kitchen/README.md)
- [Explore Geoffrey Runtime](https://geoffreyruntime.com/)
- [Browse the Shortcut library](https://geoffreyruntime.com/shortcuts)
- [Check Radio V2 availability](https://geoffreyruntime.com/radio/install)
- [Preview Black Line Express](https://geoffreyruntime.com/black-line-express/demo/): a browser concept with simulated vehicle controls and an external WVLG player link. No vehicle connection is active.
- [Read the architecture documentation](docs/README.md)

## Current Radio status

Radio V2 is being prepared and verified. The main Radio installer is temporarily unavailable; the official Radio page does not offer an earlier installer. Radio remains free and local-first, with no Jackson-West account required. Its published setup path uses Global Lock and does not require Global Key. See the [Radio status page](https://geoffreyruntime.com/radio/install) for availability and setup.

The V1 architecture documents below are retained as a frozen reference. They do not establish current installer availability or a V2 release.

## Software and service boundary

Geoffrey Runtime is the customer-facing software. Some capabilities run entirely on the customer device. Optional Jackson-West services have their own independently enforced authorization boundary; downloading or editing a Shortcut does not grant access.

This repository's covered materials use the Geoffrey Runtime Source-Available License V1. See [Licensing](#licensing) for the existing terms. Private Jackson-West technology, systems, services, and credentials remain outside this repository.

## Overview

Geoffrey Runtime combines deterministic execution with optional AI assistance. Governed requests can be validated, logged, approved, executed, and audited. Explicitly local capabilities retain their local execution boundary and may report a receipt or status event afterward.

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

# Documented architecture and capabilities

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

### Radio V1 — frozen architecture reference

Radio V1 completed its architecture/readiness review. Its official architecture is **local-first**, with Global Lock / Jackson-West access defaulting to **false/off**. Free Radio executes locally without Jackson-West governance. Actions are **Play, Stop, Back, and Next**; volume, pause, and resume are outside V1.

Play selects a station and one or more outputs and invokes the appropriate local helper Shortcuts. The complete product relationship is **Geoffrey Runtime Radio → Radio controller → Radio Stations → Speakers/outputs → Global Lock → optional Jackson-West service**. Stations and Speakers are required installation components with separate packaging/publishing; unpublished helper downloads are not frozen-engine defects.

The customer-owned Shortcut and `radio.json` registry are intentionally editable, not security boundaries. Jackson-West independently authenticates/authorizes governed requests and is the authoritative security boundary. Local edits or access flags cannot grant server authorization. With Jackson-West enabled, Radio still acts locally first; the later receipt/state report never requests a second execution. Distributable Jackson-West Core and Text Jackson-West customer values are intentionally blank until optional customer onboarding.

Run Radio locally at least once to create its required registry/setup. The public registry bootstraps the interactive path. Server-originated/structured execution before initialization is unsupported in V1. Native media actions labeled Mac during development execute on the customer device and remain subject to device verification.

Current installation availability and setup requirements are published on the permanent [Radio](https://geoffreyruntime.com/radio/install), [Stations](https://geoffreyruntime.com/radio/install/stations), [Speakers](https://geoffreyruntime.com/radio/install/speakers), and [Global Lock](https://geoffreyruntime.com/global-lock/install) pages. Available downloads follow the website's agreement/acceptance flow. The main Radio installer is temporarily unavailable while V2 is prepared and verified.

The frozen V1 architecture and public contract are documented in [`docs/radio-v1.md`](docs/radio-v1.md) and [`schemas/radio-v1.md`](schemas/radio-v1.md). Their release-readiness history does not establish current distribution status.

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

# Licensing

Copyright © 2026 Geoffrey Runtime LLC. Geoffrey Runtime LLC owns the customer-distributed Geoffrey Runtime software in this repository.

Materials expressly covered by [LICENSE](LICENSE) are available under the **Geoffrey Runtime Source-Available License V1**, version `gr-source-available-2026-09-30-v1`. The complete LICENSE text matches the [published website license](https://geoffreyruntime.com/legal/source-available-license). It permits inspection, study, installation, running, copying, and modification for personal, household, educational, research, evaluation, nonprofit, and Internal Business Use, plus qualifying noncommercial distribution, subject to the license conditions. It does not permit commercial redistribution, charging for access, paid bundling, commercial sublicensing, competing commercial offerings, or misleading use of Geoffrey Runtime or Jackson-West branding without written authorization. This is a source-available license, not an open-source license.

The [Customer Usage Agreement](https://geoffreyruntime.com/legal/usage) separately governs the Geoffrey Runtime website, official installation experience, and connected features. The software license controls copyright permissions for covered software; the Usage Agreement does not replace those permissions. Official website installation requires affirmative, recorded acceptance before continuing to Apple Shortcuts. Merely browsing this repository does not constitute acceptance of the Customer Usage Agreement.

Private Jackson-West technology, systems, services, and credentials are outside this repository and are not licensed by the Source-Available License. Third-party and file-specific notices continue to control their respective materials.

For commercial authorization, contact [jack@jackson-west.io](mailto:jack@jackson-west.io).

---

# Documented baseline

**Runtime V1 architecture**

This documentation baseline is separate from the Radio product's current release status. Radio V2 is in preparation, and the main installer is temporarily unavailable.

Documented capabilities include:

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


