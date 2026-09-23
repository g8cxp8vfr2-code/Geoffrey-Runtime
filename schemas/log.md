# Log Schema

The log schema defines the standard format for all Geoffrey Runtime log entries.

Logs provide a chronological record of runtime activity for troubleshooting, auditing, and diagnostics.

## Standard Log Entry

```json
{
  "schema_version": "1.0",
  "log_id": "log-001",
  "timestamp": "2026-07-19T21:35:01-05:00",
  "request_id": "req-001",
  "logged_by": "wrap_request",
  "event": "request_received",
  "status": "success",
  "message": "Request wrapped successfully."
}
```

## Required Fields

| Field | Description |
|---|---|
| `schema_version` | Log schema version |
| `log_id` | Unique log identifier |
| `timestamp` | Time of the event |
| `request_id` | Related request |
| `logged_by` | Runtime component writing the log |
| `event` | Event that occurred |
| `status` | success, failure, warning, or info |
| `message` | Human-readable description |

## Common Events

- request_received
- request_validated
- validation_failed
- policy_checked
- executor_started
- executor_completed
- notification_sent
- receipt_created
- request_completed

## Status Values

- success
- failure
- warning
- info

## Example Failure

```json
{
  "schema_version": "1.0",
  "log_id": "log-002",
  "timestamp": "2026-07-19T21:36:10-05:00",
  "request_id": "req-002",
  "logged_by": "validation",
  "event": "validation_failed",
  "status": "failure",
  "message": "Missing required parameter: vehicle."
}
```

## Purpose

Logs provide detailed visibility into every stage of Geoffrey Runtime execution.

Unlike receipts, multiple log entries may exist for a single request, allowing the complete processing path to be reconstructed.