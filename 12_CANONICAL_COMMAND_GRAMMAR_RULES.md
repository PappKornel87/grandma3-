# grandMA CANONICAL COMMAND GRAMMAR RULES v0.1

The canonical command grammar is a machine-readable layer between raw knowledge and command validation.

Principles:
- MA2 and MA3 remain separate namespaces.
- Only evidence-backed tokens are promoted into the grammar.
- Lua API names are not automatically command keywords.
- REJECTED / UNVERIFIED_IMPLEMENTATION records are excluded.
- Grammar-safe connectors are explicitly marked as system grammar tokens.
- A token being valid does not prove every sequence containing it is valid.
- Command patterns carry their own confidence level.
- Unknown patterns remain partial/unverified rather than being accepted by analogy.
- High-risk mutation patterns preserve risk classification.

Current grammar is intentionally conservative and incomplete.
