# grandMA ARTIFACT VALIDATION RULES v0.1

## Purpose

This layer validates the actual generated Macro/Lua artifact itself.

It must not trust only the model's declared `used_primitives`.
It extracts grandMA-specific primitives directly from the emitted artifact and compares them against the retrieved Evidence Bundle.

The goal is to catch:
- undeclared API calls;
- invented commands;
- MA2/MA3 mixing;
- incomplete corrected artifacts;
- unsupported switches/options;
- stale code left behind after a fix.

---

## 1. Lua extraction

### MA2
Extract:
- every `gma.*` call;
- nested namespaces such as `gma.show.getobj.handle`;
- command strings sent through `gma.cmd(...)`.

### MA3
Extract:
- top-level MA API calls such as `Cmd(...)`;
- handle/object method calls where the method/property is grandMA-specific and evidence-backed;
- command strings sent through `Cmd(...)`.

Do not treat standard Lua functions as grandMA primitives.

---

## 2. Macro extraction

For every macro line extract:
- command keyword;
- primary object keyword when identifiable;
- switches/options beginning with `/`;
- variables beginning with `$`.

Example:

`Store Sequence 5 /Overwrite`

should produce roughly:
- command: `Store`
- object: `Sequence`
- option: `/Overwrite`

Exact semantic validation depends on available evidence.

---

## 3. Evidence comparison

Every extracted MA-specific primitive must be supported by the Evidence Bundle.

Allowed:
- exact name match;
- explicit syntax/signature support in evidence;
- canonical command/object token supported by a retrieved record.

Reject:
- primitive absent from evidence;
- primitive supported only by `REJECTED`;
- MA2 primitive in MA3 artifact;
- MA3 primitive in MA2 artifact.

---

## 4. Command-string validation

A Lua API call can be valid while the command string inside it is invalid.

Therefore:

`gma.cmd("...")`
and
`Cmd("...")`

must be checked at two levels:
1. API call valid?
2. command content valid?

The validator must not stop after validating only `gma.cmd` or `Cmd`.

---

## 5. Revision validation

If `revision_of_failed_artifact = true`:
- validate the full regenerated artifact;
- reject patch-only responses;
- reject placeholders such as `...`, `rest unchanged`, `same as above`;
- reject missing helper functions referenced by the artifact.

---

## 6. Status

Return one of:
- `VALIDATED`
- `VALIDATED_WITH_WARNING`
- `PARTIALLY_VALIDATED`
- `FAILED_VALIDATION`

Unknown syntax is not automatically accepted.

---

## 7. v0.1 boundary

v0.1 is a deterministic structural validator.

It can reliably:
- extract common Lua API calls;
- extract macro command/object/options;
- catch platform mixing;
- catch unsupported extracted primitives;
- catch partial-patch patterns.

It does not yet fully parse the complete grandMA command grammar.
