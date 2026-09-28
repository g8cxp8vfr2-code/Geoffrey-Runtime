# Radio V1 Schema

This document defines the public Radio V1 message profile. It describes messages sent toward Jackson-West without publishing private credentials or Shortcut internals.

## Actions

| Action | Required parameters | Allowed parameters |
| --- | --- | --- |
| `play` | `station`, `speakers` | `station`, `speakers` |
| `stop` | none | none |
| `back` | none | none |
| `next` | none | none |

No other action is part of Radio V1. In particular, `pause`, `resume`, and volume control are unsupported.

## Envelope

Messages sent to Jackson-West use these fields:

| Field | Rule |
| --- | --- |
| `schema_version` | Radio V1 uses `1.0` |
| `shortcut` | Configured public Shortcut identifier; the canonical Radio identifier is `radio` |
| `source` | Origin of the message, such as `button`, `governed_button`, `voice`, or a configured automation source |
| `target` | Must be `radio` |
| `action` | Must be `play`, `stop`, `back`, or `next` |
| `device_id` | Configured device identity; public examples use `<DEVICE_ID>` |
| `request_id` | Unique correlation identifier |
| `status` | `success` for a completed local execution receipt; `received` for a new governed request |
| `logged_by` | Configured producer identifier |
| `user_id` | Configured user identity; public examples use `<USER_ID>` |
| `timestamp` | Timestamp for the action or governed request |
| `auth` | Private Jackson-West credential supplied at runtime; documentation uses `<SECRET>` only |
| `parameters` | Action-specific object defined below |

The presence of `auth` does not guarantee authorization. The server validates the credential, identity, device, source, action, and customer policy independently.

## Parameters

For `play`:

```json
{
  "station": "jacks_jazz_radio",
  "speakers": [
    "this_device"
  ]
}
```

`station` is a non-empty configured station identifier. `speakers` is a non-empty list of configured output selectors. Selectors may represent a room or output/source, including customer-supported values such as `this_device`, `tesla`, `portable_speaker`, or a room identifier such as `living_room_speakers`.

For `stop`, `back`, and `next`, `parameters` must be an empty object:

```json
{}
```

## Local execution receipt/status profile

A Free Radio message sent after local execution has `status: success`. Jackson-West treats it as an observation of completed local execution, does not send it through governance as a new request, and does not dispatch Radio again.

```json
{
  "schema_version": "1.0",
  "shortcut": "radio",
  "source": "button",
  "target": "radio",
  "action": "play",
  "device_id": "<DEVICE_ID>",
  "request_id": "<REQUEST_ID>",
  "status": "success",
  "logged_by": "jackson_west_core",
  "user_id": "<USER_ID>",
  "timestamp": "<TIMESTAMP>",
  "auth": "<SECRET>",
  "parameters": {
    "station": "jacks_jazz_radio",
    "speakers": [
      "this_device"
    ]
  }
}
```

If reporting is not configured, local execution does not imply that Jackson-West received a receipt. If reporting is configured but authentication or authorization fails, Jackson-West rejects the event and must not update authoritative server state from it.

## Governed request profile

A Jackson-West-originated or otherwise governed Radio request has `status: received` and enters the existing authentication, authorization, governance, routing, execution, and receipt path.

```json
{
  "schema_version": "1.0",
  "shortcut": "radio",
  "source": "governed_button",
  "target": "radio",
  "action": "play",
  "device_id": "<DEVICE_ID>",
  "request_id": "<REQUEST_ID>",
  "status": "received",
  "logged_by": "jackson_west_core",
  "user_id": "<USER_ID>",
  "timestamp": "<TIMESTAMP>",
  "auth": "<SECRET>",
  "parameters": {
    "station": "jacks_jazz_radio",
    "speakers": [
      "living_room_speakers"
    ]
  }
}
```

Local customer configuration can expose this route, but only Jackson-West policy grants server authorization. Missing or invalid server-side configuration must fail closed.
