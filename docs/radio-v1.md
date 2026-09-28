# Radio V1

Radio V1 has two intentional execution lanes. They must not be collapsed into one architecture.

| Lane | Execution | Jackson-West interaction |
| --- | --- | --- |
| Free Radio | Executes locally on the customer device | May send a post-execution receipt/status event where configured |
| Governed Radio | Executes only after the existing Jackson-West validation, authentication, authorization, and governance path | Produces the governed result and receipt expected by that path |

A Free Radio receipt records an action that already happened locally. It is not a new governed request, and Jackson-West must not dispatch the action a second time.

## V1 actions

Radio V1 supports exactly:

- `play`
- `stop`
- `back`
- `next`

`pause`, `resume`, volume changes, and other playback actions are outside Radio V1.

## Play and routing

`play` requires a station plus at least one configured output selector. The public Jackson-West envelope carries output selectors in `parameters.speakers`. Registry-defined selectors can represent a room or source/output such as `this_device`, `tesla`, or `portable_speaker`. Room selectors use the configured room output identifier, such as `living_room_speakers`.

Allowed stations, rooms, and outputs are configuration-backed. A name appearing in documentation does not make it available on every customer device.

`stop`, `back`, and `next` do not accept station, room, output, or volume parameters in V1. They act on the applicable current local or governed Radio context.

## Security and authorization boundary

Customer-side access configuration can decide whether a local capability attempts to report to Jackson-West. That configuration is not server authorization. Jackson-West independently authenticates and authorizes every inbound receipt/status event and governed request and must fail closed when required identity, customer configuration, or authorization material is missing or invalid.

Public examples use placeholders only. Live access values, API keys, bearer tokens, private Shortcut internals, credential-bearing URLs, and customer-specific secrets must not be committed.

## Receipt meaning

A local receipt/status event means the customer device reported that it completed the local action. It records the action, routing parameters, device identity, timestamp, and correlation identifier required by the configured Jackson-West interface. It does not retroactively turn that action into a governed request.

A governed receipt has the meaning assigned by the existing governed path. Transport or handoff alone is not proof of physical playback; authoritative execution claims still require the receipt expected by that path.

See the exact public field profile in [`../schemas/radio-v1.md`](../schemas/radio-v1.md) and sanitized examples in [`../examples/radio-v1.md`](../examples/radio-v1.md).
