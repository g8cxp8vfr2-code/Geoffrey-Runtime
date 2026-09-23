# text: Geoffrey Runtime

Text transport adapter that forwards incoming Shortcut text to the configured Jackson-West Messages recipient.

## Input

Any Shortcut Input that can be converted to text, commonly a serialized request dictionary.

## Observed processing flow

1. Receives Shortcut Input.
2. Converts the input to text.
3. Sends the text through Apple Messages to the configured Jackson-West recipient.

The recipient's underlying address or account identifier is intentionally not documented.

## Output

The result supplied by the Messages send action, if any.

## Failure conditions

- Shortcut Input cannot be converted to text.
- Messages access is unavailable.
- The configured recipient cannot be resolved.
- Message delivery fails.

## Security

Do not include authorization values, private recipient addresses, or device-derived credentials in documentation examples.

## Related shortcuts

- `Talk to Geoffrey Runtime`
- `From Geoffrey Runtime`
