---
name: minimum-sufficient-model
description: Use when a workflow still requires probabilistic inference and you need to identify the lightest viable model tier, or justify why a frontier model is still necessary.
version: 1.0.0
author: Build Green AI
license: MIT
metadata:
  buildgreen:
    principle: 02-minimum-sufficient-model
    tags: [green-ai, model-selection, right-sizing, local-models, small-models, inference]
    related_files:
      - references/model-selection-rubric.md
      - templates/model-right-sizing-report.md
---

# Minimum sufficient model

## Overview

Use this skill to right-size model choice for workloads that still legitimately need probabilistic inference.

The purpose is not to prove that every workflow should use a smaller model. The purpose is to separate workloads that truly justify frontier-model cost from workloads that can be handled by a smaller hosted model, a local model, or a hybrid design that leaves only a narrow escalation step on a larger model.

This skill is downstream of `01-default-to-determinism`. If the workload should be code, rules, parsing, routing, or scheduling instead of inference, do not keep sizing models around a bad workflow. Route it back to skill 1.

## When to use

Use this skill when:
- a workflow still appears to need a model, but the current model may be over-sized
- a team is using frontier models for repeated operational workloads
- latency, cost, or privacy pressure suggests a lower model tier may be enough
- you need to justify why a frontier model call should remain in the system
- you want to test whether local or hosted small models can replace part of a workflow

Do not use this skill when:
- the workload should really be deterministic code or workflow rules
- you have no examples of the task, outputs, or failure modes
- the real problem is that the workflow itself is unclear or broken
- you are looking for a list of fashionable models without workload evidence

## Required inputs

Gather as many of these as the current environment allows:
- current prompt or workflow sample
- current model or provider in use
- representative inputs and outputs
- examples of acceptable and unacceptable results
- current task volume or frequency
- latency expectations or service level targets
- privacy, security, or data residency constraints
- any required output schema or formatting constraints
- the operational cost of a bad answer
- any existing evaluation set, benchmark, or human review criteria

If a source is missing, state that explicitly in the final report.

## Workflow

### Step 1: Confirm the workload still needs a model
Start by checking whether this is actually a model-sizing problem.

Ask:
1. Is the task mainly extraction, validation, routing, filtering, formatting, or field assembly?
2. Are the inputs and outputs stable enough for deterministic handling?
3. Is the current model mostly serving as glue between deterministic steps?

If the answer points toward deterministic handling, classify the workload as `Deterministic` and recommend one of these shared labels:
- `Replace with code`
- `Replace with workflow rule`

Then stop and route the workload back to `01-default-to-determinism`.

### Step 2: Describe the workload concretely
Before recommending a model tier, capture:
- what the task actually does
- what enters the system
- what leaves the system
- how often it runs
- how quickly it must respond
- what happens when it fails
- whether privacy or deployment constraints limit provider choices

Do not write a recommendation for a vague task description.

### Step 3: Score the workload using the rubric
Use `references/model-selection-rubric.md` and score:
- reasoning intensity
- output structure strictness
- hallucination tolerance
- latency sensitivity
- privacy and data control constraints
- volume and repetition
- variation tolerance
- failure cost

Use the rubric qualitatively. Do not collapse the decision into one blind average.

### Step 4: Map the workload to a shared class
Use the exact shared taxonomy labels:
- `Deterministic`
- `Local model candidate`
- `Hosted small model candidate`
- `Frontier model justified`
- `Do not automate yet`

For model-sizing work, the common target classes will usually be:
- `Hosted small model candidate`
- `Local model candidate`
- `Frontier model justified`

Use `Do not automate yet` only if the workflow is too poorly understood to size responsibly.

### Step 5: Recommend the lightest viable tier
Choose the smallest tier that can plausibly satisfy the real workload constraints.

Use one of these final recommendation paths:
- keep frontier model
- downshift to hosted small model
- move to local model
- use a hybrid pipeline
- return to skill 1 because this should be code instead

Justify the recommendation from the workload evidence, not from general model reputation.

### Step 6: Design a substitution test plan
Do not stop at a recommendation.
Create a concrete comparison plan that names:
- the current baseline model or workflow
- the candidate replacement tier
- the sample task set to evaluate
- the pass-fail standard
- the cost comparison method
- the latency comparison method
- the rollback condition if quality drops below the bar

A model downshift without a test plan is incomplete.

### Step 7: Produce the structured report
Output the findings using `templates/model-right-sizing-report.md`.

## Classification rules

### `Hosted small model candidate`
Use this when the workload still needs inference, but the task is bounded enough that a smaller hosted model should be able to perform it.

Strong signs:
- reasoning is light or moderate
- outputs are structured or semi-structured
- cost and latency matter because the task repeats
- the workflow does not require deep synthesis or nuanced judgment

Common recommendation label:
- `Downshift model tier`

### `Local model candidate`
Use this when the workload is bounded enough for smaller inference and the operating constraints strongly favor local execution.

Strong signs:
- privacy constraints are real
- throughput or repeated use makes API cost unattractive
- the task is narrow enough to fit a smaller local model
- the deployment environment can actually support local inference

Common recommendation label:
- `Move local`

### `Frontier model justified`
Use this only when the workload still demonstrates real need for frontier capability.

Strong signs:
- reasoning depth is genuinely high
- nuanced synthesis or complex tradeoffs matter
- lower tiers fail the task standard in testing
- the cost of a bad answer is high enough that the extra capability is justified

Common recommendation label:
- `Keep current approach, but justify it`

### Hybrid pipeline
Use this when the workflow should be split by difficulty.

Typical pattern:
- deterministic code handles stable setup and post-processing
- a local or hosted small model handles common cases
- only escalation cases go to a frontier model

Common recommendation labels:
- `Downshift model tier`
- `Move local`
- `Add instrumentation first`

### `Do not automate yet`
Use this only when the task boundaries, success criteria, or operating constraints are still too unclear to size responsibly.

If you use this class, say what evidence is missing and what must be collected first.

## Output format

Return a report with these sections:
1. Context reviewed
2. Workload reviewed
3. Current model usage
4. Findings
5. Dimension scores
6. Candidate target architectures
7. Recommended changes
8. Test plan for substitution
9. Risks and caveats
10. Verification steps

Every recommendation must include:
- workload description
- current class
- target class
- dimension scores
- current model tier
- proposed target tier
- one sentence explaining why the current tier is over-sized, under-sized, or justified
- exact recommendation label from the shared taxonomy
- one substitution test plan
- one measurable verification step

## Common pitfalls

1. Recommending a smaller model because the current bill looks large
High cost alone is not evidence that the workload can be downshifted safely.

2. Confusing strict output format with easy reasoning
A structured output can still depend on hard judgment.

3. Treating privacy as an automatic local-model answer
Local is only a good answer when the task and hardware fit.

4. Ignoring the possibility that the task should be deterministic instead
Some over-sized model calls should disappear, not shrink.

5. Naming a target tier without a comparison plan
The recommendation is not operational until it can be tested.

6. Justifying frontier usage with brand prestige
Use workload evidence, not vendor status signals.

## Verification checklist

Before finalizing the report, verify:
- the workload was described concretely
- deterministic replacement was considered first
- every recommendation maps to a named workload class
- every proposed model change has an explicit reason
- the report uses the shared taxonomy labels exactly
- the report includes a substitution test plan
- the report includes at least one measurable follow-up check
- any recommendation to keep frontier usage is explicitly justified

## Recommended next action

After producing the report, end with one of these next steps:
- run a hosted small-model substitution test
- run a local-model feasibility test
- redesign the workflow as a hybrid pipeline
- keep the frontier model and instrument its performance more tightly
- route the workload back to skill 1 for deterministic replacement

The report should end with the single highest-leverage next move.
