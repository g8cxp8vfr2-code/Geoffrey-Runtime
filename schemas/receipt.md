# Response Schema

The response schema defines the standard result returned by Geoffrey Runtime after a request has been processed.

A response indicates whether the runtime accepted, rejected, or completed a request.

## Standard Response

```json
{
  "schema_version": "1.0",
  "request_id": "req-001",
  "response_id": "res-001",
  "timestamp": "2026-07-19T21:35:00-05:00",
  "status": "success",
  "target": "radio",
  "action": "play",
  "message": "Radio started successfully.",
  "executor": "radio_executor",
  "receipt_id": "receipt-001"
}
```

## Required Fields

| Field | Description |
|---|---|
| `schema_version` | Response schema version |
| `request_id` | Original request identifier |
| `response_id` | Unique response identifier |
| `timestamp` | Time the response was generated |
| `status` | success, failed, or blocked |
| `target` | Target executor |
| `action` | Action performed |
| `message` | Human-readable result |

## Example Failed Response

```json
{
  "schema_version": "1.0",
  "request_id": "req-002",
  "response_id": "res-002",
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

Every response corresponds to exactly one request.

A successful response may also generate a receipt and one or more log entries.