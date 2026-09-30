# Receipt Schema

The receipt schema defines durable evidence recorded after a governed request has been processed.

A receipt indicates whether the runtime rejected, blocked, failed, or completed a governed request. Free Radio uses a distinct post-execution receipt/status profile because the customer device has already executed the action; see [`radio-v1.md`](radio-v1.md).

## Standard Receipt

```json
{
  "schema_version": "1.0",
  "request_id": "req-001",
  "receipt_id": "receipt-001",
  "timestamp": "2026-07-19T21:35:00-05:00",
  "status": "success",
  "target": "radio",
  "action": "play",
  "message": "Radio started successfully.",
  "executor": "radio_executor"
}
```

## Required Fields

| Field | Description |
|---|---|
| `schema_version` | Receipt schema version |
| `request_id` | Original request identifier |
| `receipt_id` | Unique receipt identifier |
| `timestamp` | Time the response was generated |
| `status` | success, failed, or blocked |
| `target` | Target executor |
| `action` | Action performed |
| `message` | Human-readable result |

## Example Failed Receipt

```json
{
  "schema_version": "1.0",
  "request_id": "req-002",
  "receipt_id": "receipt-002",
  "timestamp": "2026-07-19T21:36:00-05:00",
  "status": "failed",
  "target": "tesla",
  "action": "preheat_off",
  "message": "Vehicle not available."
}
```

## Status Values

- success
- failed
- blocked
- invalid_request
- unauthorized

## Notes

Every governed receipt corresponds to one request. A locally originated Radio execution receipt instead correlates to the local action by `request_id` and must never be interpreted as a new governed request.

A governed request may also generate a response and one or more log entries. Radio V1 remains local-first with access defaulting false/off. When Jackson-West is enabled, the post-action receipt/state report is validated at the server boundary and must not cause another execution. Server-originated Radio requires prior local initialization; see the [frozen architecture](../docs/radio-v1.md).
