# Notification

Displays a user-facing notification from a structured request dictionary.

## Input

A dictionary containing:

- `parameters`
- `parameters.sound`
- `parameters.notification`
- notification `title` data within the notification payload

## Observed processing flow

1. Converts Shortcut Input to a dictionary.
2. Extracts `parameters`, then `sound` and `notification`.
3. Extracts the notification title.
4. Stops immediately if the input dictionary has no value.
5. If `sound` is `off`, shows the notification without the configured sound.
6. Otherwise, shows the notification with sound behavior enabled by the action configuration.

## Output

No explicit response dictionary is constructed. The visible notification is the action's effect.

## Failure conditions

- Input is empty or not a dictionary.
- Required notification data is missing.
- Notification permission is unavailable.

## Related shortcuts

- `Talk to Geoffrey Runtime`
- `From Geoffrey Runtime`
