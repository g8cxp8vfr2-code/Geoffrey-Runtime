# Geoffrey Request Information

Adds request identity, device, lifecycle, timestamp, and authorization metadata to an incoming dictionary.

## Input

An optional request dictionary. If Shortcut Input is present, it is converted to a dictionary and used as the working request.

## Metadata added

| Field | Observed source |
| --- | --- |
| `request_id` | Current date combined with a generated random number |
| `user_id` | Normalized device hostname |
| `device_id` | Normalized device model |
| `status` | Literal `received` |
| `logged_by` | Literal `jackson_west_core` |
| `timestamp` | Current date |
| `auth` | Private Jackson-West access key |

## Observed processing flow

1. Converts Shortcut Input to a dictionary.
2. Generates a random number between `100000` and `99999999` and combines it with the current date for `request_id`.
3. Normalizes the device hostname to lowercase and replaces separators before storing it as `user_id`.
4. Normalizes the device model before storing it as `device_id`.
5. Adds `status`, `logged_by`, and `timestamp`.
6. Adds the private authorization value to `auth`.
7. Returns the enriched dictionary as the Shortcut result.

## Sanitized output example

```json
{
  "request_id": "<REQUEST_ID>",
  "user_id": "<USER_ID>",
  "device_id": "<DEVICE_ID>",
  "status": "received",
  "logged_by": "jackson_west_core",
  "timestamp": "<TIMESTAMP>",
  "auth": "<SECRET>"
}
```

## Security

The installed Shortcut contains live authorization material. Never copy the observed value into source control, issues, logs, examples, screenshots, or messages. Use `<SECRET>` only. Treat the device-derived identity fields as sensitive and use `<USER_ID>` and `<DEVICE_ID>` in documentation.

## Failure conditions

- Shortcut Input cannot be converted to a dictionary.
- Device information is unavailable.
- Required metadata cannot be added to the dictionary.

## Related shortcuts

- `Talk to Geoffrey Runtime`
- `From Geoffrey Runtime`
- `subcribe to jackson west`
