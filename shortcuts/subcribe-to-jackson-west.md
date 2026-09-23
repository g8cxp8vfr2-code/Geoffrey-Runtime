# subcribe to jackson west

Subscription-control menu for sending a subscribe or cancel request to Jackson-West.

The heading intentionally preserves the installed Shortcut's spelling.

## Input

No explicit input is required.

## Observed processing flow

1. Presents `Subscribe to Jackson-West` and `Cancel Jackson-West` menu options.
2. Converts the selection into the corresponding action text.
3. Builds a request dictionary whose `shortcut` and `target` fields use the installed Shortcut name.
4. Adds request metadata by running `Geoffrey Request Information`.
5. Sends the wrapped request through `text: Geoffrey Runtime`.

## Sanitized request example

```json
{
  "shortcut": "subcribe to jackson west",
  "target": "subcribe to jackson west",
  "action": "<SUBSCRIBE_OR_CANCEL>",
  "source": "button",
  "request_id": "<REQUEST_ID>",
  "user_id": "<USER_ID>",
  "device_id": "<DEVICE_ID>",
  "auth": "<SECRET>"
}
```

## Failure conditions

- No menu selection is made.
- Request metadata cannot be constructed.
- Message transport fails.

## Related shortcuts

- `Geoffrey Request Information`
- `text: Geoffrey Runtime`
