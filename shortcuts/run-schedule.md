# Run Schedule

Finds due Geoffrey automation reminders and sends each eligible item to Jackson-West.

## Input

No explicit input is required.

## Observed selection rules

The Shortcut searches the `Automation` reminder list for reminders that:

- are due within the next six minutes; and
- are not completed.

## Observed processing flow

1. Reads the current date.
2. Finds reminders matching the selection rules.
3. Repeats over each result.
4. Reads the reminder title and retains the reminder as the payload.
5. If the title has a value, runs `text: Jackson-West`.
6. Marks the reminder completed.
7. Replaces the reminder notes with a `Sent to Geoffrey` timestamp.
8. Stops if a reminder has no usable title.

## Output

No explicit response dictionary is constructed. Completion is represented by the reminder's completed state and updated notes. That local state records dispatch by this Shortcut; it is not a correlated receipt proving downstream execution.

## Failure conditions

- Reminders access is denied.
- The `Automation` list is unavailable.
- A reminder has no title.
- `text: Jackson-West` is unavailable or rejects the payload.

## Related shortcuts

- `Set Schedule`
- `text: Geoffrey Runtime`
