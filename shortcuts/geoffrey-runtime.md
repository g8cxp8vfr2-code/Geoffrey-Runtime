# Geoffrey Runtime

Device-aware home menu and top-level launcher for the installed Geoffrey Runtime shortcuts.

## Input

No explicit input is required.

## Observed processing flow

1. Reads the current device name.
2. Normalizes the device name through lowercase and configured text-replacement actions for use in routing.
3. Presents a home menu containing Geoffrey, TV, Fleet, lights, Radio, scenes, vacuum, services, Dee's kitchen, announcement, add-song, and Amazon options.
4. Dispatches the selected option to its configured downstream Shortcut.
5. Stops after the selected branch completes.

The installed Shortcut remains authoritative for the exact downstream target behind each menu branch.

## Output

The selected branch's result, if that downstream Shortcut returns one.

## Failure conditions

- No menu selection is made.
- A configured downstream Shortcut is unavailable.
- A downstream Shortcut rejects or fails the request.

## Related shortcuts

- `Geoffrey Runtime Menu`
- `Talk to Geoffrey Runtime`
