# Geoffrey Runtime Shortcuts

This directory records the previously observed Apple Shortcuts in the `Geoffrey Runtime` folder without changing or executing them. These inventory notes do not establish the public Radio installation requirements or override the [official frozen Radio V1 architecture](../docs/radio-v1.md).

## Recorded inventory

- [`Geoffrey Runtime`](geoffrey-runtime.md)
- [`Set Schedule`](set-schedule.md)
- [`Run Schedule`](run-schedule.md)
- [`Welcome to Geoffrey Runtime`](welcome-to-geoffrey-runtime.md)
- [`Talk to Geoffrey Runtime`](talk-to-geoffrey-runtime.md)
- [`Geoffrey Runtime Menu`](geoffrey-runtime-menu.md)
- [`Geoffrey Request Information`](geoffrey-request-information.md)
- [`text: Geoffrey Runtime`](text-geoffrey-runtime.md)
- [`From Geoffrey Runtime`](from-geoffrey-runtime.md)
- [`Notification`](notification.md)
- [`subcribe to jackson west`](subcribe-to-jackson-west.md)

Names above intentionally preserve the installed spelling and capitalization.

## Security

Documentation must never contain live authorization codes, API keys, bearer or OAuth tokens, passwords, secrets, private credential-bearing URLs, or device identifiers used as credentials. Examples use placeholders such as `<SECRET>`, `<USER_ID>`, `<DEVICE_ID>`, `<REQUEST_ID>`, and `<REDACTED_SHORTCUT_URL>`.

## Radio distribution boundary

Radio is local-first with Jackson-West access defaulting false/off. Its complete installation consists of the Radio controller, required separate Stations and Speakers components, Global Lock, and optional Jackson-West service onboarding. The earlier authenticated menu/installer inventory above is not a prerequisite for Free Radio. In distributable Radio, Jackson-West Core and Text Jackson-West customer values are intentionally blank until onboarding. Local registry/Shortcut edits do not grant server authorization.

The customer must run Radio locally at least once to create `radio.json` before server-originated/structured execution. Stations/Speakers packaging, iPhone verification, and final installation tests are deployment work; unpublished helpers do not reopen Radio-engine architecture.

## Documentation scope

Each file records the purpose, observed inputs, processing flow, outputs, failure behavior, and related installed Shortcuts. Runtime code and architecture are outside this directory's scope.
