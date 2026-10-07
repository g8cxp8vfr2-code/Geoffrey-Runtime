# Public execution trace — synthetic example

This document demonstrates Geoffrey Runtime's **request → validation → policy → execution → receipt** contract using a deliberately synthetic example.

> **Security note:** This is not a production log. All identifiers, timestamps, device references, and values below are fictitious. Private endpoints, credentials, authentication material, internal policy rules, household identifiers, service topology, and Jackson-West implementation details are intentionally omitted.

The purpose of this example is to show the **shape of the system boundary and evidence trail**, not how to access or reproduce the private service.

---

## Scenario

A user requests a bounded home action:

> "Turn on the living room scene."

The public example assumes the request has already reached the governed request boundary. It does **not** expose transport details, authentication headers, private URLs, customer identifiers, or internal infrastructure.

---

## 1. Request intake

A request is normalized into a bounded structure.

```json
{
  "request_id": "req_demo_01",
  "requested_at": "2026-10-07T17:00:00Z",
  "actor": {
    "type": "user",
    "id": "user_demo"
  },
  "source": {
    "type": "button",
    "client": "public-demo"
  },
  "action": {
    "capability": "home_scene",
    "command": "activate",
    "target": "living_room"
  }
}
```

### What is intentionally absent

- production user IDs
- real device IDs
- API keys or tokens
- network addresses
- private endpoint paths
- internal service names
- exact authorization claims

---

## 2. Validation result

The runtime validates the request shape and checks that the requested capability, command, and target are recognized.

```json
{
  "request_id": "req_demo_01",
  "stage": "validation",
  "status": "accepted",
  "checks": {
    "schema_valid": true,
    "capability_known": true,
    "command_allowed": true,
    "target_known": true
  }
}
```

A malformed or unknown request would stop here instead of reaching an executor.

Example rejection:

```json
{
  "request_id": "req_demo_02",
  "stage": "validation",
  "status": "rejected",
  "reason_code": "UNKNOWN_TARGET"
}
```

The public trace intentionally uses coarse reason codes rather than exposing internal validation logic.

---

## 3. Policy decision

After structural validation, a separate policy decision determines whether this request is eligible for execution.

```json
{
  "request_id": "req_demo_01",
  "stage": "policy",
  "status": "approved",
  "decision": {
    "capability": "home_scene",
    "command": "activate",
    "target": "living_room"
  }
}
```

This public example does **not** publish the private rule set, authorization graph, account state, or policy evaluation internals.

The important boundary is:

```text
valid request != authorized request
```

Both conditions must be satisfied before governed execution.

---

## 4. Execution result

Only after validation and policy approval is the bounded action passed to an executor.

```json
{
  "request_id": "req_demo_01",
  "stage": "execution",
  "status": "completed",
  "executor_result": {
    "capability": "home_scene",
    "command": "activate",
    "target": "living_room",
    "result": "success"
  }
}
```

The example does not reveal:

- executor addresses
- local automation names
- device vendor credentials
- customer network details
- private dispatch mechanisms

---

## 5. Receipt

The resulting receipt preserves enough information to correlate the action without exposing the private implementation.

```json
{
  "receipt_id": "rcpt_demo_01",
  "request_id": "req_demo_01",
  "recorded_at": "2026-10-07T17:00:01Z",
  "status": "success",
  "action": {
    "capability": "home_scene",
    "command": "activate",
    "target": "living_room"
  },
  "evidence": {
    "execution_result_recorded": true
  }
}
```

The receipt is an evidence record for the governed workflow. It should not be interpreted as publishing private telemetry or internal infrastructure details.

---

## End-to-end relationship

```text
Request
  |
  v
Validation
  |
  v
Policy
  |
  v
Execution
  |
  v
Receipt
```

The key engineering properties demonstrated by the trace are:

1. **Correlation** — one request ID follows the operation across stages.
2. **Bounded inputs** — execution receives a recognized capability, command, and target rather than unrestricted natural language.
3. **Fail closed** — invalid requests stop before execution.
4. **Separate authorization** — structural validity does not itself grant permission.
5. **Evidence after execution** — the workflow produces a result/receipt that can be associated with the originating request.
6. **Private implementation stays private** — the public contract can be demonstrated without exposing credentials, endpoints, household identity, or proprietary policy logic.

---

## Where AI fits

If natural-language interpretation is needed, AI may propose structured fields before the validation stage.

For example:

```json
{
  "capability": "home_scene",
  "command": "activate",
  "target": "living_room"
}
```

That output is still treated as **untrusted input**. It must pass the same deterministic validation and policy checks before any governed action can execute.

**AI does not receive direct authority to control the device.**

---

## Scope

This example documents a public architectural contract only. It is intentionally insufficient to operate, authenticate to, enumerate, or reconstruct private Jackson-West services.

For a real deployed cross-system acceptance example, see the [Estelle's Kitchen engineering case study](../docs/estelles-kitchen/engineering-case-study.md).
