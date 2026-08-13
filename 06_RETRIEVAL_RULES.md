# Retrieval Rules v0.1

1. Detect/fix platform first: MA2 and MA3 must never be mixed silently.
2. Apply version filtering before semantic ranking when a version is known.
3. Exclude `REJECTED` by default.
4. Exclude `UNVERIFIED_IMPLEMENTATION` by default unless the user explicitly wants experimental/community implementations.
5. Rank relevance first, then use authority and verification status as reliability tie-breakers.
6. Prefer exact API/object/enum names over general semantic matches.
7. Surface `PARTIALLY_VERIFIED` and `VERSION_SENSITIVE` explicitly.
8. `tested=false` means "not behavior-tested", even when a signature is runtime/package verified.
9. Mutation/high-risk records should trigger a safety/test-on-copy instruction in the future reasoning layer.
10. Retrieval returns evidence records; it does not itself decide the final answer.
