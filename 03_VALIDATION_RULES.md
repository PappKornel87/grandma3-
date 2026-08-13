# grandMA VALIDATION RULES v0.1

## Purpose

The validation layer checks a proposed grandMA Macro, Lua plugin, command sequence, or workflow before it is shown to the user.

Its purpose is to catch technical errors that can survive retrieval and reasoning.

It does not redesign the solution unless validation fails.

---

## 1. Validation order

Always validate in this order:

1. platform
2. version compatibility
3. command/API existence
4. syntax/signature
5. object/property validity
6. execution order
7. logic consistency
8. mutation/safety scope
9. completeness
10. output readiness

A failure in an earlier stage blocks later approval.

---

## 2. Platform validation

Confirm that every executable element belongs to the requested platform.

### MA2
- MA2 command-line syntax only
- MA2 `gma.*` API only
- no MA3 handle/API syntax

### MA3
- MA3 command-line syntax only
- MA3 API/functions only
- no MA2 `gma.*` calls

If any mixed-platform element is found:
- reject the solution;
- return it to the reasoning layer for reconstruction.

---

## 3. Version validation

For every version-sensitive element:

- compare against the requested software version;
- check the record's version/version_scope;
- reject elements known to conflict with the target version;
- mark unresolved compatibility as `VERSION_UNVERIFIED`.

Do not silently assume forward/backward compatibility.

---

## 4. Command and API existence validation

Every grandMA-specific command, function, object, property, enum, and API call must have supporting evidence in the canonical knowledge/retrieval output.

Any primitive supported only by a `REJECTED` knowledge record is invalid and must be rejected. A `REJECTED` record must never be used to construct executable output.

Reject:
- plausible but unretrieved API names;
- guessed command keywords;
- guessed properties;
- undocumented object paths used as facts;
- API calls imported from the other platform.

Standard Lua language functions do not require MA API evidence, but must be valid Lua for the platform runtime.

---

## 5. Signature validation

For Lua/API calls:

- verify argument count where known;
- verify optional vs required arguments;
- verify argument type expectations where known;
- verify return assumptions;
- do not use a return value if the API is documented as returning nothing;
- do not assume a handle when a string/integer is returned.

If the signature is incomplete:
- allow only if the use is supported by a validated example or behavior test;
- otherwise mark as unresolved and return to reasoning.

---

## 6. Macro syntax validation

For each macro line:

- verify command keyword;
- verify object keyword;
- verify options/switches;
- verify variable syntax;
- verify quoting;
- verify separators;
- verify Wait value if present;
- verify that command order is executable.

Special attention:
- `SetVar` / `SetUserVar`
- popup input syntax
- object addressing
- `Store`, `Assign`, `Copy`, `Clone`, `Delete`, `Import`, `Export`
- `/merge`, `/overwrite`, `/remove`, `/nc` and related options

Do not accept a macro because it “looks like MA syntax.”

---

## 7. Lua structure validation

A returned plugin must be structurally complete.

Check:
- required entry function exists;
- helper functions are defined before/when used;
- variables referenced are defined;
- MA API calls are platform-correct;
- `return` structure is appropriate for the platform/plugin pattern;
- no stale names remain after a revision;
- no undefined handle/object variable is used;
- nil/invalid-object cases are handled where realistic;
- no accidental infinite loop;
- no uncontrolled recursion;
- no blocking wait/poll loop without justification.

---

## 8. Object and path validation

### MA3
- `path` and `addr` are not guaranteed globally unique;
- do not validate object identity using path/address alone;
- prefer handles/runtime object resolution where required;
- verify object class when the operation depends on it.

### MA2
- numeric Root paths are version-sensitive;
- prefer named object/root paths where supported;
- validate any numeric-root assumption explicitly.

---

## 9. Logic validation

Validate the solution as a whole, not only line by line.

Check:
- each step produces the state expected by the next;
- variables contain the expected type/value;
- loops terminate;
- conditional branches are reachable and sensible;
- Store/Assign/Copy operations target the intended object;
- a read-before-write dependency is respected;
- temporary state is restored if required;
- a correction did not break previously working behavior.

---

## 10. Mutation and safety validation

Classify every solution:

### LOW
Read-only / inspection.

### MEDIUM
Temporary state/programmer/playback/selection changes.

### HIGH
Store, overwrite, delete, import, clone, patch, showfile, bulk changes.

For HIGH:
- identify exact mutation target;
- verify scope is bounded;
- verify there is no silent destructive default;
- require explicit warning in output;
- recommend copy/onPC/offline testing when practical.

If scope cannot be proven:
- validation fails.

---

## 11. Full-regeneration validation

When a Macro/plugin is revised after a reported failure:

Validation must be performed on the **entire regenerated artifact**, not only on the changed line/function.

Check:
- old broken code is gone;
- all references match the new implementation;
- no partial patch remains;
- all previously required functionality is still present;
- the final artifact is internally self-consistent.

The validator must reject a final answer that contains only a patch unless the user explicitly requested a patch/diff.

---

## 12. Completeness validation

Before approval:

For Macro:
- all required lines included;
- all variables initialized;
- all Wait values included where needed;
- no hidden dependency on a previous chat snippet.

For Lua:
- complete code block;
- no “rest unchanged” placeholders;
- no omitted helper functions;
- no unresolved pseudo-code;
- no references to code not present in the answer.

The final answer must be independently usable.

---

## 13. Validation statuses

Use one of:

- `VALIDATED`
- `VALIDATED_WITH_WARNING`
- `VERSION_UNVERIFIED`
- `PARTIALLY_VALIDATED`
- `FAILED_VALIDATION`

Definitions:

### VALIDATED
All required checks passed using available evidence.

### VALIDATED_WITH_WARNING
Technically supported, but contains a known risk/version caveat that does not block use.

### VERSION_UNVERIFIED
Core solution is plausible, but target-version behavior is not confirmed.

### PARTIALLY_VALIDATED
Some elements are supported but at least one implementation detail lacks enough evidence.

### FAILED_VALIDATION
Do not show executable solution as final.

---

## 14. Failure behavior

If validation fails:

1. identify the failed check;
2. return the solution to reasoning;
3. reconstruct the full solution;
4. re-run validation;
5. only then pass to output.

Do not expose a known-invalid executable solution as the final answer.

---

## 15. Minimal validation report

The validation layer should internally produce:

```text
Platform: MA2 / MA3
Version: ...
Artifact: Macro / Lua / CLI / Workflow
Validation status: ...
Evidence gaps: ...
Risk: LOW / MEDIUM / HIGH
Blocking issues: ...
Warnings: ...
```

This report is internal by default.

Only surface warnings/errors that materially help the user.

---

## 16. Definition of validation success

A solution is ready for output only when:

- platform is correct;
- version assumptions are controlled;
- all MA-specific primitives are supported;
- syntax/signatures are consistent with available evidence;
- logic is internally coherent;
- mutation scope is understood;
- the artifact is complete;
- a revised artifact is fully regenerated;
- no known invalid fragment remains.


## MA2 exact-runtime mutation evidence
For grandMA2 3.9.63.6, the following exact scratch-object operations have VERIFIED_RUNTIME evidence from a disposable showfile:
- `Store Macro 9999 "AI_BV_TEMP" /o`
- `Label Macro 9999 "AI_BV_TEMP"`
- `Delete Macro 9999 /nc`

Do not generalize this evidence to other object classes, object numbers, options, or command compositions without separate runtime evidence.


## MA2 runtime coverage v0.2
Exact grandMA2 3.9.63.6 runtime evidence now exists for:
- selected-executor object/property inspection;
- Sequence 9999 object inspection;
- Cue 1 object inspection within Sequence 9999;
- exact Store/Label/Delete sequence/cue scratch commands.

Promote only direct successful non-nil API calls to VERIFIED_RUNTIME. Keep command evidence narrow to exact tested forms.

## MA2 Preset validation rule

When validating generated MA2 artifacts:
1. Validate CLI Preset expressions against official command grammar (`Preset [Preset-type].[ID]`).
2. If Lua uses `gma.show.getobj.handle()` for a Preset, do not validate the path merely because the same text is valid CLI syntax.
3. Require runtime evidence or defensive nil checking for the handle.
4. If the returned Preset identity matters, verify at least `getobj.class()` and `getobj.number()` or equivalent readback.

## 17. MA2 real-world validation additions

### PresetType Dimmer Delay

For MA2, accept this workflow as validated operator/runtime evidence:

`PresetType "Dimmer" At Delay <value>`

Still validate:
- platform is MA2;
- the value or variable is syntactically valid;
- the command is used in the intended current-selection context.

### Update followed by ClearAll

When a generated MA2 Macro contains `Update` followed by `ClearAll`, validate that a Wait exists between them.

Preferred default:
`Wait 0.1`

Reason:
real-world operator evidence shows that immediate `ClearAll` can race ahead of completion of `Update` and clear the programmer too early.

If no Wait is present:
- return the Macro to reasoning;
- regenerate the full Macro with the Wait inserted;
- validate the complete artifact again.
