# grandMA Semantic Guardrails

## MA2 runtime target
Exact runtime evidence in this project is centered on grandMA2 onPC 3.9.63.6.

## Command-call vs semantic proof
A successful `gma.cmd("...")` call proves only that the command was accepted without Lua error.
It does not prove the intended show-state mutation unless the state was independently read back.

Use these evidence levels conceptually:
- official syntax;
- runtime call/dispatch;
- runtime semantic/postcondition;
- runtime negative finding.

## Object addressing
Do not equate CLI object syntax with Lua object paths.

Known tested examples:
- `Executor 97.1` can be accepted in CLI usage while `gma.show.getobj.handle("Executor 97.1")` returns nil.
- Macro line direct handles such as `Macro 9990.1` and tested `getobj.child()` traversal did not resolve macro lines.
- Preset CLI syntax and Lua resolver behavior must be treated separately.

## Preset
Official MA2 CLI supports:
`Preset [Preset-type].[ID]`

Therefore:
- `Preset 1.1` = preset type 1, preset ID 1;
- `Preset 2.1` = preset type 2, preset ID 1;
etc.

Do not infer that the same string is a valid `gma.show.getobj.handle()` path.

## Verified semantic postconditions
The runtime suite explicitly verified Store/Label/Delete semantics with readback for selected Group and View scratch objects.

## Nil findings
A nil handle in one show proves that the object/path did not resolve in that tested show/context.
It does NOT prove the keyword/object class is globally invalid.

## Safety
Delete and overwrite must be treated as destructive unless read-only or scratch-scoped.
Never weaken safety merely to satisfy a benchmark or produce an executable artifact.

## Real-world operator evidence

### PresetType "Dimmer" At Delay

Confirmed in real MA2 use:

`PresetType "Dimmer" At Delay <value>`

Treat this as validated operator/runtime workflow evidence for MA2.

### Update / ClearAll ordering

Confirmed operational behavior:
an immediate `ClearAll` after `Update` can clear the programmer before the update is fully committed.

Guardrail:
place a short Wait between `Update` and `ClearAll`.

Default recommendation:
`Wait 0.1`
