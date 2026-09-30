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

The recorded downstream name `Jackson West Free Radio` does not make local Radio a Jackson-West-governed service. Under the [frozen Radio V1 architecture](../docs/radio-v1.md), access defaults false/off; Free Radio executes locally without Jackson-West governance. When enabled, communication afterward is a receipt/state report, not a second execution. Governed server requests are independently authenticated/authorized by Jackson-West and require prior local Radio initialization before dispatch to the customer device.

The authenticated menu inventory above does not define the public Radio installer. The permanent Radio installation pages provide the controller, required Stations, and required Speakers independently of optional Jackson-West onboarding. The customer-owned Radio Shortcut/registry remain editable. Blank Jackson-West Core and Text Jackson-West customer values in distributable Radio are intentional.

## Output

The selected downstream Shortcut's result, if one is returned.

## Failure conditions

- Request metadata cannot be constructed.
- No menu item is selected.
- The selected downstream Shortcut is unavailable.

## Related shortcuts

- `Geoffrey Request Information`
- `Talk to Geoffrey Runtime`
