# Vault routing — direct-route resolution, measured

Produced by `python 30_SCRIPTS/routing/measure_route_resolution.py --out 07_EVALUATION/vault_routing/route_resolution.json`
on the working tree of `claude/ranking-formula-experiment` at `268f702d6` (commit in the JSON), as the owner so policy hides nothing.
Re-measured 2026-10-10; the previous measurement (4220 routes, 2026-10-06) is superseded by the rows below.

| Measure | Value |
|---|---:|
| Routes (files reachable by `vault://`) | 4434 |
| Domains (`04_CONFIG/vault_domains.yaml`, `expand: subdirs` included) | 117 (`expand: subdirs` adds one domain per sub-directory). `VAULT_STATE.md` states the same count and a test checks it |
| `vault_resolve(uri)` returns that route | 4434 / 4434 |
| `vault_resolve(<last slug segment>)` returns that route | 4197 / 4434 (94.7%) |
| … returns AMBIGUOUS (name shared by several files) | 237 (102 with the requested file among the candidates) |
| … RESOLVED to a different file | **0** |

What this does and does not show:

- Every routed file has a direct route, and a name never silently resolves to the wrong file: shared names
  (README, CURRENT, AGENT) come back AMBIGUOUS with candidates, and the full URI always resolves.
- It does not measure topical questions. `vault_resolve` matches names, titles, aliases, headings and domain
  keywords; it does not read note bodies. Put through `vault_resolve`, the 20 work questions in
  `07_EVALUATION/memory_usage/work_queries.json` returned their `source_file` 0/20 times, at top-1 and in the top 5.
  Those questions are about topics, and the file a task is listed in is not where its answer lives.
  Content questions remain `memory_search` / `vault_search`, whose measured quality is in `VAULT_STATE.md` §5.
- Ambiguous names with the requested file outside the top 5 candidates: 135 (237 ambiguous, 102 with the file among the candidates; mostly `readme`).
  `vault_list(<domain>)` or the full URI reaches them.
