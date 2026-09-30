# Radio V1 Examples — Frozen Architecture

These sanitized scenarios explain the frozen V1 architecture without changing the field/action contract in [`../schemas/radio-v1.md`](../schemas/radio-v1.md). They contain no working credentials or private customer configuration.

## First local run

1. The customer installs Radio, its selected station helpers, applicable speaker/output helpers, and Global Lock as part of the complete installation experience.
2. The customer runs Radio locally at least once. The interactive path uses the public registry as its fresh-install/bootstrap source and creates the required `radio.json` registry/setup.
3. Global Lock / Jackson-West access defaults false/off. Local initialization does not grant server authorization.
4. Only after initialization is server-originated/structured execution supported. A server cold start before that first local run is unsupported in V1.

## Local play with access off

1. The customer selects Play, a station, and one or more speaker/output destinations.
2. Radio invokes the appropriate local station and output helper Shortcuts on the customer device.
3. Free Radio executes without Jackson-West governance. Optional Jackson-West service setup is not required for this local action.

## Local play, then report when enabled

1. The device performs the local Play action first.
2. When Jackson-West is enabled and configured, Radio sends the post-action receipt/state report (`status: success` in the frozen profile).
3. Jackson-West independently authenticates/authorizes the report before accepting authoritative server state. It records the observation without dispatching Radio a second time.
4. Rejecting a report does not undo the already-performed local action. Transport alone does not prove physical playback or server acceptance.

## Local next without reporting

The customer device executes Next locally using the applicable playback context. With access off/unconfigured, local completion is not evidence of Jackson-West receipt or authorization.

## Server-originated room playback after initialization

1. The customer has already run Radio locally and created the required registry/setup.
2. A governed server request uses Play, a configured station, and one or more outputs, such as a configured room.
3. Jackson-West independently authenticates/authorizes the request and applies its server policy before dispatch.
4. The initialized Radio Shortcut performs the action on the customer's device using local helpers.
5. The subsequent receipt/state report records that action. It is not another execution request and must not produce a second dispatch.

The governed `status: received` profile is distinct from the post-action report. Enabling service access does not turn a customer-originated local action into a governed request.

## Editable local registry and distribution placeholders

A customer may edit the local Shortcut or registry. Those edits affect local execution and cannot grant Jackson-West authorization. No local tamper-resistance allowlist is part of V1. Jackson-West Core and Text Jackson-West customer values are intentionally blank in distribution and populated during optional customer onboarding.

## Component publication and device verification

Stations and Speakers are required separately installable components; unpublished helper installation links are distribution work, not Radio-engine defects. Mac labels on development media actions are device-context artifacts; verify final execution on the customer's iPhone/device.

## Unsupported actions

Pause, resume, and volume control are outside V1. They must not be translated into another action or presented as V1 features.
