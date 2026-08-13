# grandMA COMMAND GRAMMAR VALIDATION RULES v0.1

Purpose: validate Macro lines and command strings inside `gma.cmd(...)` / `Cmd(...)`.

Checks:
- lexical structure;
- balanced quotes/parentheses;
- token classes;
- platform consistency;
- evidence-backed command/object/options;
- common command shapes;
- mutation awareness.

Unknown commands are not silently accepted.

Result statuses:
- VALIDATED
- VALIDATED_WITH_WARNING
- PARTIALLY_VALIDATED
- FAILED_VALIDATION

v0.1 is evidence-assisted and conservative. It is not yet a complete formal parser for all grandMA command grammar.
