# CODEX DISPATCH — PLANNING INFLUENCE MVE V1

Status: READY_FOR_EXECUTION
Project: AI_MEMORY_VAULT
Source agent: LUNA
Target agent: CODEX
Round: R001

## Objective

Implement and execute the minimum viable experiment required to test whether persistent memory can causally influence an agent's planning computation, rather than merely improve context.

## Authoritative inputs

- `07_EVALUATION/luna/COGNITIVE_MEMORY_TARGET_MODEL_V2.md`
- `07_EVALUATION/luna/PLANNING_INFLUENCE_EXPERIMENT_V1.md`
- Perplexity adversarial validation supplied on 2026-09-04; verdict: GO WITH MANDATORY MVE CHANGES.
- Perplexity validation report: `PERPLEXITY ADVERSARIAL VALIDATION REPORT`, HEAD observed by Perplexity: `da05ab7ae1c0174ea7f01f6165a8a41e734ba315`.

## Mandatory experiment corrections from Perplexity

1. Do NOT use hand-coded treatment priors such as `P=0.0/0.8` as proof of memory influence.
2. Include an antecedent acquisition trial so the memory prior is derived from prior experience.
3. Derive empirical action values from the acquisition episode and transform them into soft priors; do not clamp fatal branches deterministically for the cognitive-memory treatment.
4. Use four arms:
   - Arm 1: Uninformed baseline, uniform priors, no memory.
   - Arm 2: Passive Advisory RAG, identical semantic memory text, uniform priors.
   - Arm 3: Cognitive Planning Influence, memory-derived priors from antecedent experience + compact IR card.
   - Arm 4: Stale/Adversarial memory, intentionally outdated or environment-mismatched experience.
5. Recommended MVE size: 30 paired synthetic debugging scenarios.
6. Recommended planner: Python MCTS, depth=3, rollouts=16, exploration constant=1.414.
7. Keep semantic information controlled between passive-RAG and cognitive-planning arms so the difference is the programmatic planning prior, not extra textual knowledge.
8. Control branch-order bias by random permutation of branch identifiers across runs/tasks.
9. Use deterministic action proposal generation where practical (`temperature=0`) or multiple seeds; record the exact choice.
10. Enforce comparable compute/token budgets across arms; record node evaluations, model calls, tokens, and wall-clock time.
11. Record the provenance chain:
    acquisition episode -> evidence -> extracted pattern/value -> applicability -> memory prior -> planner trajectory -> outcome.
12. Do not update canonical long-lived memory from a single outcome without the required safeguards. Keep experiment-derived memory isolated.

## Required outputs

Create experiment artifacts under:

`07_EVALUATION/luna/experiments/planning_mve/`

At minimum:

- deterministic/synthetic task generator or fixtures;
- Python MCTS runner;
- acquisition/consolidation path for experiment memory;
- four-arm runner;
- structured trace schema;
- result aggregation script;
- README/protocol;
- final evidence report with exact commands and stdout/stderr excerpts.

## Acceptance metrics

Primary:

- planning efficiency / nodes to verified solution;
- frequency of revisiting known fatal branches;
- outcome success rate.

Secondary:

- model calls;
- token expenditure;
- wall-clock runtime;
- branch ordering/search trajectory;
- robustness under stale/adversarial memory.

The experiment is successful only if treatment improvements can be attributed to memory-derived planning influence rather than privileged information, prompt leakage, or planner configuration differences.

## Required negative result handling

A null result is valid evidence.

Do not tune the task generator, prior temperature, rollout count, or stopping rule until the control/treatment protocol itself is fixed and documented. Any later parameter sweep must be a separate experiment.

## Existing repository caution

Do not modify core Vault storage schema as part of this MVE.

Before graph-conditioned tests, verify the current state of `cognitive_core/spreading_activation.py` and specifically verify whether the previously reported weighted-edge overwrite bug is still present on the actual branch being used. If already fixed, record the code/test evidence; do not re-implement blindly.

## Evidence discipline

Never report a test as passed without real execution output.
Never report runtime/CI evidence from another branch as local evidence.
Every substantive change must be committed.
Before handoff, persist CODEX agent/project/task/session state according to `09_COORDINATION/AGENT_MEMORY/UNIVERSAL_AGENT_MEMORY_PROTOCOL_V1.md`.

## Exact handoff

SOURCE_AGENT -> TARGET_AGENT -> TASK_ID -> PROJECT_ID -> CURRENT_SHA -> EVIDENCE_REFS -> REQUIRED_NEXT_ACTION

SOURCE_AGENT: LUNA
TARGET_AGENT: CODEX
TASK_ID: R001-PLANNING-MVE-V1
PROJECT_ID: AI_MEMORY_VAULT
CURRENT_SHA: use the latest verified commit containing V2 + this dispatch
EVIDENCE_REFS:
- `07_EVALUATION/luna/COGNITIVE_MEMORY_TARGET_MODEL_V2.md`
- `07_EVALUATION/luna/PLANNING_INFLUENCE_EXPERIMENT_V1.md`
- Perplexity adversarial validation report supplied 2026-09-04
REQUIRED_NEXT_ACTION: implement, run, and report the four-arm Planning Influence MVE without touching core Vault schema.
