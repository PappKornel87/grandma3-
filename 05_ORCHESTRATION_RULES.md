# grandMA ORCHESTRATION RULES v0.1

## Purpose

The orchestration layer controls the order in which the grandMA system components are used.

It is not itself the knowledge base, retrieval engine, reasoning model, validator, or formatter.

Its job is to route one user request through the correct stages and keep the stages separated.

## Runtime pipeline

```text
USER REQUEST
    |
    v
1. REQUEST ANALYSIS
    |
    v
2. RETRIEVAL
    |
    v
3. EVIDENCE BUNDLE
    |
    v
4. REASONING
    |
    v
5. VALIDATION
    |
    |-- FAIL -> return to REASONING
    |
    v
6. OUTPUT
    |
    v
FINAL ANSWER
```

The Eval layer sits outside this runtime path and audits the system.

## 1. Request analysis

Extract:
- platform: MA2 / MA3 / unknown
- requested version, if supplied
- task type
- whether executable output is requested
- whether the request mutates show data
- whether the user is reporting failure of a previous Macro/plugin
- whether the user explicitly requests experimental/unverified methods

Do not solve the technical task in this stage.

## 2. Retrieval call

Pass the normalized request to the retrieval engine.

Requirements:
- enforce platform filtering when platform is known;
- apply version filtering when possible;
- exclude `REJECTED` by default;
- exclude `UNVERIFIED_IMPLEMENTATION` by default;
- retrieve enough records to support every grandMA-specific primitive required by the solution.

Retrieval returns evidence, not a final answer.

## 3. Evidence bundle

Convert retrieval results into a compact structured package for reasoning.

Required fields:

```json
{
  "request": "...",
  "platform": "MA2",
  "version": "3.9.x",
  "task_type": "macro",
  "executable_requested": true,
  "revision_of_failed_artifact": false,
  "risk_hint": "LOW",
  "evidence": [],
  "allowed_primitives": [],
  "warnings": [],
  "unsupported": []
}
```

Reasoning should use the evidence bundle rather than unrestricted memory for exact grandMA-specific syntax/API claims.

## 4. Reasoning call

Apply `REASONING_RULES.md`.

Reasoning decides:
- Macro / Lua / CLI / workflow;
- implementation structure;
- required primitives;
- risk level;
- whether evidence is sufficient;
- whether clarification is required.

Reasoning must not silently introduce MA-specific primitives absent from the evidence bundle.

## 5. Validation call

Apply `VALIDATION_RULES.md` to the proposed solution.

If validation fails:
- do not continue to final output;
- return failure details to reasoning;
- regenerate the full solution;
- validate again.

Limit correction loops. If repeated validation fails, return an explicit unsupported/unverified answer.

## 6. Output call

Apply `OUTPUT_RULES.md` only after validation.

Important:
- preserve validation status and warnings;
- if correcting a failed Macro/plugin, output the complete corrected artifact;
- never reduce a complete corrected artifact to a patch unless explicitly requested.

## 7. State between turns

When a user says a previously returned Macro/plugin does not work:
- treat the previous full artifact as revision context;
- preserve working behavior;
- apply the correction;
- regenerate the entire artifact;
- validate the entire artifact;
- output the entire corrected artifact.

## 8. Stop conditions

Clarify when:
- platform is required but unknown;
- target version materially changes the solution;
- mutation target is ambiguous and potentially destructive.

Stop as unsupported when:
- required API/command/property cannot be verified;
- only rejected evidence supports the requested primitive;
- validation repeatedly fails.

## 9. Separation of responsibilities

- Knowledge = what is known.
- Retrieval = what evidence is relevant.
- Reasoning = what solution should be built.
- Validation = whether the solution is acceptable.
- Output = how it is presented.
- Eval = whether the system behaves correctly.
- Orchestration = which layer runs when, and what data passes between them.

## 10. v0.1 limitation

The local Python orchestrator can:
- analyze the request heuristically;
- run the real retrieval engine;
- build the evidence bundle;
- enforce deterministic routing/safety gates.

It does not replace the LLM reasoning/generation step.

Production flow should pass the evidence bundle plus the reasoning/validation/output rules into the model, then validate the generated candidate before final output.
