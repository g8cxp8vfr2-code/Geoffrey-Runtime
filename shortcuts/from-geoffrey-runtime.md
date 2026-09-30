# From Geoffrey Runtime

Inbound dispatcher for structured responses received from Geoffrey Runtime.

## Input

Text containing a JSON-compatible response dictionary.

Expected fields include:

- `request_id`
- `target`
- target-specific payload data

## Observed processing flow

1. Runs `Geoffrey Request Information` and reads `user_id`.
2. Converts Shortcut Input to text, then converts that text to a dictionary named `payload`.
3. Extracts `request_id`.
4. If the payload contains data, extracts `target`.
5. Runs `Notification` with the payload.
6. Runs the Shortcut named by `target`.
7. Builds a success dictionary containing `status`, `request_id`, and the executor result.
8. Sends that result through `text: Geoffrey Runtime`.

## Sanitized response example

```json
{
  "status": "success",
  "request_id": "<REQUEST_ID>",
  "executor": "<EXECUTOR_RESULT>"
}
```

## Failure conditions

- Input text is not a dictionary.
- The payload is empty.
- `target` is missing or does not name an installed Shortcut.
- Notification, target execution, or response transport fails.

## Radio V1 execution prerequisite

When the dispatched target is Radio, the customer must already have run Radio locally at least once to create its required `radio.json` registry/setup. Server-originated/structured Radio execution before initialization is unsupported in V1. Jackson-West independently authenticates/authorizes server requests; this local dispatcher and editable registry do not grant server authorization. Radio executes locally and any subsequent receipt/state report must not dispatch another Radio action. See the [frozen architecture](../docs/radio-v1.md). This note documents the prerequisite; it adds no runtime behavior.

## Related shortcuts

- `Geoffrey Request Information`
- `Notification`
- `text: Geoffrey Runtime`
