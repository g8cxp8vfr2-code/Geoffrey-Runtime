# Request Schema

The request schema defines the standard structure for every command entering Geoffrey Runtime.

Requests may come from buttons, voice input, schedules, messages, calendar events, or AI interpretation.

## Standard Request

```json
{
  "schema_version": "1.0",
  "request_id": "unique-request-id",
  "timestamp": "2026-07-19T21:30:00-05:00",
  "source": "governed_button",
  "user_id": "mr_jackson",
  "device_id": "geoffrey_phone",
  "intent": "media_control",
  "target": "radio",
  "action": "play",
  "parameters": {
    "station": "Jazz Radio",
    "rooms": [
      "upstairs"
    ]
  },
  "raw_text": null
}
```

## Required Fields

| Field | Description |
|---|---|
| `schema_version` | Version of the request contract |
| `request_id` | Unique identifier for the request |
| `timestamp` | Time the request was created |
| `source` | Where the request originated |
| `user_id` | User making the request |
| `device_id` | Device that created the request |
| `intent` | High-level request category |
| `target` | Executor or system receiving the action |
| `action` | Requested operation |
| `parameters` | Values needed to complete the action |

## Optional Fields

| Field | Description |
|---|---|
| `raw_text` | Original natural-language request used for AI fallback |
| `metadata` | Additional context that does not affect the core contract |

## Approved Source Values

- `governed_button`
- `voice`
- `schedule`
- `calendar`
- `message`
- `ai_interpreted`
- `system`

## Example: Radio Request

```json
{
  "schema_version": "1.0",
  "request_id": "req-001",
  "timestamp": "2026-07-19T21:30:00-05:00",
  "source": "voice",
  "user_id": "mr_jackson",
  "device_id": "geoffrey_phone",
  "intent": "media_control",
  "target": "radio",
  "action": "play",
  "parameters": {
    "station": "Clark Howard",
    "rooms": [
      "upstairs"
    ]
  },
  "raw_text": "Play Clark Howard upstairs"
}
```

## Example: Tesla Request

```json
{
  "schema_version": "1.0",
  "request_id": "req-002",
  "timestamp": "2026-07-19T21:31:00-05:00",
  "source": "governed_button",
  "user_id": "mr_jackson",
  "device_id": "geoffrey_phone",
  "intent": "vehicle_control",
  "target": "tesla",
  "action": "preheat_off",
  "parameters": {
    "vehicle": "model_y"
  },
  "raw_text": null
}
```

## Validation Rules

A request must fail validation when:

- A required field is missing
- `target.action` is not approved
- A required parameter is missing
- A parameter value is not found in the approved registry
- The request violates a runtime lock or policy
- The schema version is unsupported

AI may interpret a request, but AI-generated output must still pass the same validation process before execution.