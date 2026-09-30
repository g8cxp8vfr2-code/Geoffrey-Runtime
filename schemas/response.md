# Response Schema

The response schema defines the standard result returned by Geoffrey Runtime after a request has been processed.

A response reports whether the runtime completed, failed, blocked, rejected, or could not authorize a request.

## Standard Response

```json
{
  "schema_version": "1.0",
  "request_id": "req-001",
  "response_id": "res-001",
  "timestamp": "2026-07-19T21:35:00-05:00",
  "status": "success",
  "message": "Radio started successfully.",
  "payload": {
    "target": "radio",
    "action": "play",
    "executor": "radio_executor"
  }
}
```

## Required Fields

| Field | Description |
|---|---|
| `schema_version` | Response schema version |
| `request_id` | Original request identifier |
| `response_id` | Unique response identifier |
| `timestamp` | Time the response was generated |
| `status` | Outcome of the request |
| `message` | Human-readable result |
| `payload` | Additional structured response data |

## Example Failed Response

```json
{
  "schema_version": "1.0",
  "request_id": "req-002",
  "response_id": "res-002",
  "timestamp": "2026-07-19T21:36:00-05:00",
  "status": "failed",
  "message": "Vehicle not available.",
  "payload": {
    "target": "tesla",
    "action": "preheat_off"
  }
}
```

## Example Blocked Response

```json
{
  "schema_version": "1.0",
  "request_id": "req-003",
  "response_id": "res-003",
  "timestamp": "2026-07-19T21:37:00-05:00",
  "status": "blocked",
  "message": "Radio is currently locked.",
  "payload": {
    "target": "radio",
    "action": "play",
    "reason": "radio_lock"
  }
}
```

## Status Values

- success
- failed
- blocked
- invalid_request
- unauthorized

## Notes

Every response corresponds to exactly one request.

A Free Radio post-execution receipt/state report is not a response to a governed request and must never cause another Radio execution. Local Radio runs without Jackson-West governance; access defaults false/off. The governed/blocked examples above describe server-request outcomes, not evidence that Jackson-West controls the customer-editable local Shortcut. Server-originated Radio requires prior local initialization. The unchanged contract is documented in [`radio-v1.md`](radio-v1.md) and the [frozen architecture](../docs/radio-v1.md).

The outer response shape remains consistent. Target-specific details are placed inside `payload`.

A successful response may also generate a separate receipt and one or more log entries.
