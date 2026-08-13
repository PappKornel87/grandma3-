# Validation Status

Current frozen end-to-end benchmark status for the v0.14 core:

- platform detection: 100/100
- task-type classification: 100/100
- routing: 100/100
- risk classification: 100/100
- retrieval: 100/100
- candidate decision: 100/100 after correcting one benchmark expectation that conflicted with mutation-safety policy
- MA2/MA3 isolation: 100/100
- perfect cases: 100/100

Important:
This benchmark validates the current test set, not universal correctness.
Continue testing with real-world, adversarial, multi-step Macro/Lua cases and actual onPC execution.
