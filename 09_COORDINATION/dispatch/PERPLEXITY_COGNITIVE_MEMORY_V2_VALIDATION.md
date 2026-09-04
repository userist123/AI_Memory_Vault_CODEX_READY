# Perplexity Dispatch — Cognitive Memory Target V2 Validation

SOURCE_AGENT: LUNA
TARGET_AGENT: PERPLEXITY
TASK_ID: R001-CM-V2-VALIDATION
PROJECT_ID: AI_MEMORY_VAULT
CURRENT_BRANCH: luna/cognitive-memory-v1
CURRENT_SHA: 96bdfef7aa858dfdf764f4806c209f5ee64f8274
EVIDENCE_REFS:
- 07_EVALUATION/luna/COGNITIVE_MEMORY_TARGET_MODEL_V2.md
- 07_EVALUATION/luna/PLANNING_INFLUENCE_EXPERIMENT_V1.md
- 07_EVALUATION/luna/AI_MEMORY_VAULT_EVIDENCE_ADVERSARIAL_REVIEW_REPORT.md (uploaded validation basis)

## Objective
Validate, falsify or materially refine V2 against external evidence. Focus on whether the four influence channels and the outcome-to-reorganization loop are technically defensible when the Vault is separated from explicit runtime interfaces.

## Required questions
1. Does V2 correctly separate passive epistemic substrate from active runtime influence mechanisms?
2. Is Planning Influence valid only when a real search harness consumes memory-derived priors/penalties?
3. Are Representation, Epistemic and Execution channels independently testable without claiming hidden-state access?
4. Which parts of the applicability contract have external empirical/theoretical support, and which remain hypotheses?
5. What evidence supports or contradicts outcome-driven reorganization without weight updates?
6. Identify failure modes where memory influence makes behavior worse.
7. Challenge the Planning Influence Experiment V1 design, especially causal attribution, matched information, planner confounds, prior calibration, and held-out falsification.
8. Identify any claim in V2 that is overstated, underspecified or should be removed.

## Output requirements
Return a compact evidence-first report with:
- VERDICT: ACCEPT / ACCEPT WITH CHANGES / REJECT
- claims mapped to evidence strength
- exact proposed changes to V2/experiment
- explicit unknowns
- sources/provenance and research date
- no repository capability claims unless backed by repository evidence

Do not treat this dispatch or V2 design as evidence that implementation exists.
