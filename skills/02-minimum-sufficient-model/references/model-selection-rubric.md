# Model selection rubric

Use this rubric only after confirming the workload still requires probabilistic inference.

If the workload is better handled by deterministic code, workflow rules, or a cron-driven script, stop and route it back to skill `01-default-to-determinism`.

## Purpose
This rubric scores whether a workload should stay on a frontier model, move to a smaller hosted model, move to a local model, or be split into a hybrid pipeline.

The goal is not to find the fanciest model that can do the task.
The goal is to identify the lightest viable model tier that satisfies the real operational constraints.

## Required evidence
Collect these before scoring:
- current prompt or workflow sample
- current model or provider in use
- sample inputs and outputs
- examples of acceptable and unacceptable results
- frequency or volume of use
- latency expectations
- privacy or data residency constraints
- any structured output requirements
- failure impact if the output is wrong

If one of these is unavailable, record that gap in the final report.

## Gate 1: Confirm this is still a model task
Ask these questions first:
1. Is the task mainly transformation, extraction, routing, validation, filtering, or formatting?
2. Are the input and output structures stable?
3. Would rules, code, parsing, or a workflow engine handle this more reliably?
4. Is the current model call mostly acting as glue between deterministic steps?

If the answer strongly points to deterministic handling, classify the workload as `Deterministic` and recommend `Replace with code` or `Replace with workflow rule`.
Do not continue with model sizing if the workload should not be a model task at all.

## Scoring dimensions
Score each dimension from 0 to 4.
Lower scores point toward lighter model tiers.
Higher scores point toward larger or more capable model tiers.

### 1. Reasoning intensity
- 0 — Extraction, labeling, routing, or formatting only.
- 1 — Light bounded classification or rewrite with clear constraints.
- 2 — Moderate judgment with limited ambiguity.
- 3 — Multi-step reasoning, synthesis, or nuanced tradeoffs.
- 4 — Frontier-level reasoning genuinely required.

### 2. Output structure strictness
- 0 — Fixed schema or tightly constrained output.
- 1 — Mostly structured output with minor free text.
- 2 — Mixed structured and freeform output.
- 3 — Mostly open-ended output.
- 4 — Fully open-ended output where structure is loose.

### 3. Hallucination tolerance
- 0 — Very low tolerance. Output must be exact or verifiable.
- 1 — Low tolerance. Small mistakes are costly.
- 2 — Moderate tolerance with review.
- 3 — Some errors acceptable if corrected downstream.
- 4 — High tolerance for variation or imperfection.

### 4. Latency sensitivity
- 0 — Near-real-time response is important.
- 1 — Fast response materially improves usefulness.
- 2 — Moderate latency is acceptable.
- 3 — Slow responses are acceptable in batch workflows.
- 4 — Latency barely matters.

### 5. Privacy and data control constraints
- 0 — No meaningful privacy constraints.
- 1 — Basic confidentiality requirements only.
- 2 — Sensitive data, but hosted vendors may be acceptable.
- 3 — Strong preference for minimizing third-party exposure.
- 4 — Local execution or tightly controlled infrastructure strongly preferred.

### 6. Volume and repetition
- 0 — Rare or one-off workload.
- 1 — Low frequency.
- 2 — Regular repeated use.
- 3 — High-volume operational workload.
- 4 — Very high-volume or always-on workload where cost compounds quickly.

### 7. Variation tolerance
- 0 — Output should be highly consistent.
- 1 — Minor variation is acceptable.
- 2 — Moderate variation is acceptable.
- 3 — Broad variation is acceptable.
- 4 — Variation is part of the value.

### 8. Failure cost
- 0 — Mistakes are trivial.
- 1 — Mistakes are easy to spot and correct.
- 2 — Mistakes create moderate operational friction.
- 3 — Mistakes are expensive, risky, or slow to catch.
- 4 — Mistakes create severe business or safety consequences.

## Interpretation rules
Use the dimension scores qualitatively, not as a blind average.
The recommendation must be justified by the pattern of scores.

### Strong signs for `Hosted small model candidate`
Common pattern:
- reasoning intensity 0 to 2
- output structure strict or semi-structured
- repeated operational use
- cost and latency matter more than open-ended creativity

Likely shared taxonomy path:
- current class: `Frontier model justified` or `Hosted small model candidate`
- target class: `Hosted small model candidate`
- recommendation label: `Downshift model tier`

### Strong signs for `Local model candidate`
Common pattern:
- reasoning intensity 0 to 2
- privacy constraints 3 to 4, or volume 3 to 4
- latency and cost make remote APIs unattractive
- task is bounded enough that a smaller local model is realistic

Likely shared taxonomy path:
- target class: `Local model candidate`
- recommendation label: `Move local`

### Strong signs for `Frontier model justified`
Common pattern:
- reasoning intensity 3 to 4
- open-ended output or nuanced synthesis matters
- failure cost is high and smaller models materially underperform
- comparison evidence shows lower tiers miss the bar

Likely shared taxonomy path:
- target class: `Frontier model justified`
- recommendation label: `Keep current approach, but justify it`

### Strong signs for hybrid design
Use a hybrid recommendation when:
- one narrow step needs model judgment
- surrounding steps are deterministic
- a small or local model can handle triage, extraction, or draft generation
- only escalation cases need frontier reasoning

Likely recommendation labels:
- `Downshift model tier`
- `Move local`
- `Add instrumentation first`
- plus an explicit note that only the escalation step remains frontier

## Required comparison test plan
Do not recommend a downshift without a test plan.
The plan must specify:
1. current model baseline
2. candidate lower-cost tier
3. evaluation set or task samples
4. pass-fail criteria
5. cost comparison method
6. latency comparison method
7. how failures will be reviewed

## Output requirements
Every scored workload must include:
- workload description
- current class
- target class
- reasoning summary
- dimension scores
- recommendation label
- one sentence on why the current tier is over- or under-sized
- one substitution test plan

## Pitfalls
1. Treating all structured output as a small-model win.
A task can be structured and still require hard reasoning.

2. Treating privacy as an automatic local-model mandate.
Local only makes sense if the workload and hardware fit.

3. Recommending a smaller model without a test harness.
That is opinion, not an operational recommendation.

4. Confusing low hallucination tolerance with frontier necessity.
Low tolerance often means more deterministic scaffolding, not a bigger model.

5. Averaging scores mechanically.
A single hard constraint can outweigh a low average.

## Decision summary language
Use one of these exact final recommendation forms:
- Keep frontier model
- Downshift to hosted small model
- Move to local model
- Use a hybrid pipeline
- Return to skill 1 because this should be code instead
