# grandMA OUTPUT RULES v0.1

## Purpose

The output layer converts a technically resolved grandMA solution into a clear, directly usable final answer.

It does not invent technical content and does not override the reasoning or validation layers.

---

## 1. General output principles

- Give the usable solution first.
- Keep explanation separate from executable content.
- State MA2 / MA3 and software version when relevant.
- Clearly label any version-sensitive or partially verified element.
- Do not mix commentary into executable Macro or Lua code blocks.
- Prefer complete, copyable outputs over fragmented patches.

---

## 2. Macro output format

When returning a grandMA Macro:

- output the complete macro;
- preserve execution order;
- show each macro line separately;
- include Wait values when required;
- include variables exactly as they should appear;
- do not omit unchanged lines from a revised macro;
- do not return only a replacement line unless the user explicitly asks for a diff or patch.

Preferred structure:

```text
Line 1 | Command | Wait
Line 2 | Command | Wait
Line 3 | Command | Wait
```

If Wait is irrelevant, a plain numbered command list is acceptable.

---

## 3. Lua plugin output format

When returning a Lua plugin:

- output the complete runnable plugin structure;
- include all required functions, local variables, helpers, return statements, and MA-specific entry points;
- keep the code internally consistent;
- do not omit unchanged sections from a revised plugin;
- do not return only a replacement function or code fragment unless the user explicitly asks for a diff or patch.

The code block must be directly copyable.

---

## 4. Mandatory full-regeneration rule after corrections

If a previously supplied Macro or Lua plugin does not work and a correction is required:

**Always regenerate and return the entire corrected Macro or Lua plugin.**

Do not answer only with:
- the changed line;
- the changed function;
- “replace X with Y”;
- a partial patch;
- a diff;
- an isolated snippet.

This rule applies even when only one line changes.

The corrected output must:
1. contain the full current version;
2. already include every required correction;
3. remain internally consistent after the change;
4. be directly copyable without manual merging by the user.

A short note may identify what changed, but it must come after or before the full corrected code and must not replace it.

Exception:
- Only provide a partial patch/diff when the user explicitly requests a patch, diff, or only the changed lines.

---

## 5. Revision continuity

When revising a Macro or plugin:

- use the immediately previous full version as the base;
- preserve all previously working behavior unless the requested fix requires changing it;
- do not silently remove features;
- do not rename variables/functions unnecessarily;
- do not introduce unrelated refactors while fixing a specific issue;
- increment or label the version when useful.

---

## 6. Failure-response format

If the user reports that a Macro/plugin does not work:

1. identify the likely cause briefly;
2. apply the correction;
3. output the entire corrected Macro/plugin;
4. state any remaining uncertainty or required console test.

Do not make the user manually reconstruct the solution from multiple messages.

---

## 7. Workflow and conceptual answers

For workflow questions:
- give the recommended method first;
- use steps only when sequence matters;
- avoid code if the task does not need code;
- distinguish between “possible” and “recommended”.

---

## 8. Safety output

For mutating/high-risk solutions:
- state what will be modified;
- include a concise test-on-copy/onPC warning where appropriate;
- do not bury the executable content under generic safety text.

---

## 9. Final-answer consistency check

Before sending a Macro/Lua answer, confirm:

- full solution included;
- platform consistent;
- version-sensitive parts labeled;
- no missing dependencies;
- no stale code from an earlier revision;
- no partial patch unless explicitly requested;
- final code is copyable as-is.
