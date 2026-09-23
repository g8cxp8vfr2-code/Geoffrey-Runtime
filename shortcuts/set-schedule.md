# Set Schedule

Creates a reminder-backed Geoffrey automation from an incoming request dictionary.

## Input

A dictionary containing:

- `action`: the requested due date or time action
- `payload`: the request payload to retain
- `parameters`: request parameters
- `parameters.display`: the reminder title shown to the user

## Observed processing flow

1. Converts Shortcut Input to a dictionary.
2. Extracts `action`, `payload`, `parameters`, and `parameters.display`.
3. Adds a reminder to the `Geoffrey Automation` list without an alert.
4. Sets the reminder due date from `action`.
5. Stores the payload in the reminder notes.

## Output

The created or edited reminder object supplied by the Reminders actions.

## Failure conditions

- Shortcut Input is not a dictionary.
- A required field is missing or has an incompatible type.
- The `Geoffrey Automation` reminder list is unavailable.
- Reminders access is denied.

## Related shortcuts

- `Run Schedule`
