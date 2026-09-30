# Geoffrey Runtime Radio V1 — Frozen Architecture

**Status: architecture/readiness review complete; architecture frozen as of September 30, 2026.** This document records the approved V1 behavior. Remaining publication and device checks are deployment work, not permission to redesign the Radio engine or change its frozen schema.

## Local-first execution

Radio is the customer-owned local controller. Free Radio executes on the customer's device without Jackson-West governance. Global Lock / Jackson-West access defaults to `false` / off. Jackson-West is an optional service layer; local Radio does not require a Jackson-West subscription or authorization.

Radio supports exactly **Play, Stop, Back, and Next** (`play`, `stop`, `back`, `next`). Volume, pause, resume, and other playback actions are outside V1.

Play selects a station and one or more speaker/output destinations, then invokes the appropriate local station and speaker/output helper Shortcuts. Output selectors can describe this device, Tesla, a portable speaker, or a configured room. Stop, Back, and Next use the applicable local playback context; their parameters remain empty in the frozen contract.

| Origin / service state | Radio execution | Jackson-West interaction |
| --- | --- | --- |
| Customer uses Free Radio; access off | Local action on the customer's device | No Jackson-West governance of the local action |
| Customer uses Radio; Jackson-West enabled and configured | Local action first | A subsequent receipt/state report records the action; it is not a request to execute Radio again |
| Server-originated / structured execution | Supported only after local initialization; Radio executes on the customer's device | Jackson-West independently authenticates and authorizes governed requests before server dispatch; the subsequent report must not dispatch a second execution |

Enabling Jackson-West does not move Radio execution to the server or make a customer-originated local action a governed request. A report rejected by Jackson-West does not undo the local action. An unconfigured reporting path is not evidence of server receipt or authorization.

## Initialization and bootstrap

The customer must run Radio locally at least once before server-originated/structured execution. This local initialization creates the required `radio.json` registry/setup. The public registry is the fresh-install/bootstrap source for the interactive Radio path.

**Server-originated Radio execution before initialization is unsupported in V1.** Do not document a server cold-start path, auto-bootstrap structured execution, or another V2 behavior as part of this release. A first local run establishes setup; it does not grant Jackson-West authorization.

## Product and installation relationship

The complete product relationship is:

**Geoffrey Runtime Radio → Radio controller → Radio Stations → Speakers/outputs → Global Lock → optional Jackson-West service**

This expresses component roles, not a rigid wizard or a governance-before-local-play requirement. Stations and Speakers are required components of the complete Radio installation experience. Customers install the listening choices and applicable output helpers for their own setup and can return later to add more.

| Component | Role | Permanent customer address |
| --- | --- | --- |
| Radio controller | Selects actions, stations, and destinations; invokes local helpers | https://geoffreyruntime.com/radio/install |
| Radio Stations | Individual installable station Shortcuts supply listening choices | https://geoffreyruntime.com/radio/install/stations |
| Speakers/outputs | Separate installable output Shortcuts route playback to available destinations | https://geoffreyruntime.com/radio/install/speakers |
| Global Lock | Local access control; Jackson-West access defaults off | https://geoffreyruntime.com/global-lock/install |
| Jackson-West | Optional authenticated and governed service | Separate customer onboarding; no private configuration is published here |

Apple iCloud Shortcut links are replaceable implementation details behind the permanent installation pages. Stations and Speakers have their own packaging, readiness verification, and publishing process. Missing unpublished helper links are distribution work, not defects in the frozen Radio engine. Examples of station/output selectors are not an exhaustive published component inventory.

## Security boundary and editable local components

The customer-owned Radio Shortcut and local registry are intentionally editable. They are **not security boundaries**. No local tamper-resistance allowlist is required by this architecture. Local edits can change local execution but cannot grant Jackson-West authorization.

**Jackson-West is the authoritative governance/security boundary.** It independently authenticates and authorizes governed requests and validates inbound receipt/state reports before accepting authoritative server state. Editing registry entries, access flags, execution values, or a Shortcut does not bypass server policy. Missing or invalid server identity, authorization, or customer configuration must be rejected at that boundary.

The distributable Radio Shortcut intentionally leaves **Jackson-West Core** and **Text Jackson-West** customer values blank. They are populated during customer onboarding for the optional service. These blanks are expected distribution placeholders, not Radio-engine defects. Never publish customer credentials, authorization values, private recipients, endpoints, or private infrastructure in this repository.

## Receipts and development-device labels

When Jackson-West is enabled, Radio still performs the local action first. Communication afterward is a receipt/state report, not a second Radio execution. Jackson-West must not feed it back through the request dispatch path. A device report records reported local execution; transport or handoff alone does not prove physical playback or server acceptance.

Mac labels on native media actions are development-device artifacts. Final execution occurs on the customer's device. Assess those actions through iPhone/device verification rather than changing the engine to match development Mac labels.

## Deployment work remaining

- Verify Radio and native media actions on the customer iPhone/device.
- Package, verify, and publish the separate Stations and Speakers components.
- Supply the Radio/controller and component installation links and complete the website installation content.
- Run final customer-install tests, including the first local initialization and subsequent structured/server execution.

The website already provides the three permanent installation areas; publication of pages does not mean their Apple downloads or complete customer installation have been verified. Architecture work is closed for V1. Documentation alignment does not execute, modify, or re-audit the installed Shortcut.

See the unchanged field/action contract in [`../schemas/radio-v1.md`](../schemas/radio-v1.md), sanitized examples in [`../examples/radio-v1.md`](../examples/radio-v1.md), and deployment status in [`../recent.md`](../recent.md).
