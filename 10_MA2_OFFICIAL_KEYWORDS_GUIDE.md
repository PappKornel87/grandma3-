# grandMA2 Official Keywords v0.1

Goal: bring MA2 command grammar closer to the MA3 official-corpus quality level.

Target:
- grandMA2 manual version 3.9
- reference release line: 3.9.x
- behavior target: 3.9.63.6 where relevant

Run on the same Mac virtual environment used for the MA3 crawler:

```bash
DYLD_LIBRARY_PATH="/opt/homebrew/opt/expat/lib" python crawl_ma2_official_keywords.py
DYLD_LIBRARY_PATH="/opt/homebrew/opt/expat/lib" python merge_ma2_official_keywords.py
```

The crawler discovers official keyword pages from the grandMA2 v3.9 manual index instead of relying on a hand-written keyword list.

Outputs:
- `ma2_official_keyword_registry_v3_9.json`
- `ma2_official_keyword_details_v3_9.json`
- `ma2_keyword_crawl_report.json`
- after merge: `ma2_official_keyword_details_v3_9_audited.json`
- updated `canonical_index.jsonl`
- updated `canonical_command_grammar.json`

Important distinction:
Official v3.9 help validates command syntax/documentation. It does not by itself behavior-test every command on the exact 3.9.63.6 runtime. That remains a separate behavior-validation step.
