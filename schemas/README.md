# Schemas

Schemas define the data contracts used by Geoffrey Runtime.

Each published request, response, receipt, and log profile follows a documented structure so components can communicate predictably.

## Published schemas

- [Request](request.md)
- [Response](response.md)
- [Receipt](receipt.md)
- [Log entry](log.md)
- [Radio V1 — frozen field/action contract](radio-v1.md)

Radio architecture is [frozen](../docs/radio-v1.md). Documentation alignment does not change message fields, parameter rules, or JSON examples. Local Radio receipts/state reports are distinct from governed requests and must not dispatch another execution.

## Planned schemas

- Notification
- Runtime State
- Registry Entry
- Executor Result

As Geoffrey Runtime evolves, each schema will be documented in this folder.
