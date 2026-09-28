# Radio V1 Examples

These examples are sanitized public contract examples. They contain no working credentials, private Shortcut internals, or customer-specific identifiers.

## Local play, then report

1. The customer device executes `play` locally using the configured station and output.
2. If Jackson-West reporting is configured, the device sends the `status: success` profile shown in [`../schemas/radio-v1.md`](../schemas/radio-v1.md).
3. Jackson-West authenticates and authorizes the receipt/status event. It records the observation without governing or dispatching the Radio action again.

## Local next without reporting

1. The customer device executes `next` locally.
2. If the capability is not configured to report to Jackson-West, no server message is created. Local completion alone is not evidence that Jackson-West received or authorized anything.

## Governed room playback

1. A governed request uses `action: play`, a configured station identifier, and a room output such as `living_room_speakers`.
2. Jackson-West independently validates authentication, customer policy, the station, and the output.
3. Only an approved request proceeds through the existing governed execution path.
4. Completion is established by the authoritative receipt required by that path, not by transport or handoff alone.

## Unsupported actions

Requests for pause, resume, or volume control are outside Radio V1 and must fail validation rather than being translated into another action.
