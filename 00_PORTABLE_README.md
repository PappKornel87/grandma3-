# grandMA Portable Assistant Bundle v0.2

Self-contained bundle for using the grandMA Engineering Assistant outside the current ChatGPT Project.

Use cases:
- another ChatGPT Project
- Claude Project / knowledge workspace
- Gemini Gem / uploaded context
- local RAG / agent system
- any LLM environment that can ingest Markdown, JSON and JSONL

Important files:
- 01_PROJECT_INSTRUCTIONS.md
- 02_REASONING_RULES.md
- 03_VALIDATION_RULES.md
- 04_OUTPUT_RULES.md
- 05_ORCHESTRATION_RULES.md
- 06_RETRIEVAL_RULES.md
- 07_MODEL_REASONER_PROMPT_REFERENCE.md
- 08_MA2_RUNTIME_EVIDENCE_SUMMARY.json
- 09_SEMANTIC_GUARDRAILS.md
- 10_MA2_OFFICIAL_KEYWORDS_GUIDE.md
- 11_MA3_OFFICIAL_KEYWORDS_GUIDE.md
- 12_CANONICAL_COMMAND_GRAMMAR_RULES.md
- 13_COMMAND_GRAMMAR_VALIDATION_RULES.md
- 14_ARTIFACT_VALIDATION_RULES.md
- 15_CANONICAL_KNOWLEDGE.jsonl
- 16_CANONICAL_COMMAND_GRAMMAR.json
- 17_KNOWLEDGE_MANIFEST.json
- 18_VALIDATION_STATUS.md
- 19_QUICK_START_PROMPTS.md
- 20_DEPLOYMENT_GUIDE.md
- 21_PORTABLE_SYSTEM_PROMPT.md

v0.2 additions:
- MA2 real-world operator evidence for `PresetType "Dimmer" At Delay <value>`
- MA2 `Update` -> `ClearAll` race guardrail
- default operational Wait: 0.1 s

Notes:
- MA2 and MA3 must remain strictly separated.
- Exact MA2 runtime reference is centered on 3.9.63.6.
- The corpus is evidence-oriented, not a universal correctness guarantee.
- Mutating code should be tested on onPC/offline/copy first.
