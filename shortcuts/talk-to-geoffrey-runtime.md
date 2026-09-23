# Talk to Geoffrey Runtime

Voice-or-text entry point for submitting a governed request to Jackson-West.

## Input

No explicit input is required. The user chooses to dictate or type a request.

## Observed processing flow

1. Runs `Geoffrey Request Information` and reads `user_id` for the greeting.
2. Converts underscores in the user identifier to spaces for display.
3. Prompts the user to choose `Talk to Geoffrey` or `Type to Geoffrey`.
4. Captures dictated text or asks for typed text.
5. Treats an empty value, `nevermind`, or `stop` as an invalid or cancelled request.
6. On cancellation, shows a retry alert, calls `Talk to Geoffrey Runtime` again, and stops the current invocation.
7. Builds a request dictionary with `source: voice`, `status: running`, the Shortcut identifier, and request parameters.
8. Runs `Geoffrey Request Information` to add governed request metadata.
9. Sends the wrapped request through `text: Jackson-West`.
10. Builds a success-status message and runs `Notification`.

## Sanitized wrapped-request example

The metadata-enriched request passed to transport can contain the following fields. Values must remain sanitized:

```json
{
  "source": "voice",
  "status": "success",
  "request_id": "<REQUEST_ID>",
  "user_id": "<USER_ID>",
  "device_id": "<DEVICE_ID>",
  "auth": "<SECRET>"
}
```

## Output

After transport, the Shortcut constructs a success-status dictionary and passes a completion message to `Notification`. This status records the local handoff flow; it is not an authoritative receipt proving downstream or physical execution.

## Failure conditions

- The user supplies no request or selects a stop phrase.
- Request metadata cannot be constructed.
- `text: Jackson-West` is unavailable or rejects the request.
- Notification delivery fails.

## Related shortcuts

- `Geoffrey Request Information`
- `Notification`
- `Geoffrey Runtime Menu`
