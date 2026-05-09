# Principle 05: Local-first where possible

Check if a repeated workload should move from a hosted API to local inference.

This is about fit, not ideology.

Local inference isn't always viable or cheaper. But for the right task, it removes per-token costs and reduces latency.

## What this principle is trying to prevent

Teams often assume they have only two choices:
- keep paying a hosted API forever
- avoid AI entirely

That misses a third category: workloads that can run locally on available hardware, especially when they are repeated, bounded, privacy-sensitive, or latency-sensitive.

This principle exists to evaluate that option responsibly.

## What good looks like

A good local-first decision:
- starts only after confirming the task still needs inference
- describes the workload constraints precisely
- checks available hardware honestly
- names realistic candidate local models
- calculates break-even against current API spend
- accounts for privacy, compliance, and operational overhead
- proposes a feasibility test before migration

A local move is only good if it fits the task and the organization can support it.

## Signals that a workload may be a local candidate

A workflow is a strong local candidate when:
- it runs often enough for API cost to matter
- the task is bounded enough for smaller local models to fit
- privacy or data residency constraints are real
- latency pressure favors avoiding round-trips to an API
- local hardware already exists or can be provisioned sensibly

## Common failure modes

### 1. Treating privacy as an automatic answer
Local only solves the exposure problem if the full data path stays local.

### 2. Ignoring maintenance cost
Local inference is not free. Hardware, model management, updates, and monitoring still exist.

### 3. Skipping the break-even calculation
A technically possible local move may still be economically weak if the workload volume is low.

### 4. Forcing frontier work onto local hardware
Some workloads still need stronger hosted models. Local-first does not mean local-only.

## Before / after example

### Before
A document-classification workflow sends every file to a hosted model API. The task runs thousands of times per month and contains sensitive internal data.

### After
The team assesses:
- task complexity
- current API spend
- available local hardware
- candidate local models
- break-even timeline
- quality threshold

They find the task fits a local model, the break-even period is acceptable, and the privacy posture improves materially.

That is a good local-first outcome.

## Relationship to the other principles

Local-first is never the first question.

First determine whether the workflow should be deterministic.
If it still needs inference, then determine whether a smaller hosted tier or a local model is the better fit.

Related principles:
- [Principle 01: Default to determinism](01-default-to-determinism.md)
- [Principle 02: Minimum sufficient model](02-minimum-sufficient-model.md)
- [Principle 04: Measure inference cost](04-measure-inference-cost.md)

## Use the executable skill

To apply this principle in a real system, use:
- [`skills/05-local-first-where-possible/SKILL.md`](../skills/05-local-first-where-possible/SKILL.md)

That skill assesses hardware fit, candidate local models, cost break-even, privacy requirements, and the concrete feasibility test needed before migration.
