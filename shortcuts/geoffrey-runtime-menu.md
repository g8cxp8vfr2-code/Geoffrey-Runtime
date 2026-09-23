# Geoffrey Runtime Menu

Compact authenticated menu for opening the conversational or radio entry point.

## Input

No explicit input is required.

## Observed processing flow

1. Runs `Geoffrey Request Information`.
2. Extracts `user_id` and replaces underscores with spaces for display.
3. Presents a personalized welcome menu.
4. Runs `Talk to Geoffrey Runtime` when `Talk to Geoffrey` is selected.
5. Runs `Jackson West Free Radio` when `Radio` is selected.

## Output

The selected downstream Shortcut's result, if one is returned.

## Failure conditions

- Request metadata cannot be constructed.
- No menu item is selected.
- The selected downstream Shortcut is unavailable.

## Related shortcuts

- `Geoffrey Request Information`
- `Talk to Geoffrey Runtime`
