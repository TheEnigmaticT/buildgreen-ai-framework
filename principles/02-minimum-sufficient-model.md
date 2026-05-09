# Principle 02: Minimum sufficient model

Use the lightest model that reliably does the job.

Not every workflow needs a frontier model.

Don't jump from "this isn't code" to "use the biggest model." That's expensive and hard to justify in production.

## What this principle is trying to prevent

This principle exists to prevent over-sizing.

Over-sized model use shows up as:
- frontier models used for repeated operational tasks
- expensive calls doing work that a smaller hosted model could handle
- privacy-sensitive tasks sent to cloud APIs without checking local alternatives
- workflows designed around model prestige instead of workload evidence

Don't ask if a big model can do it. Ask if the task needs that much brainpower.

## What good looks like

A good model-sizing decision:
- starts only after deterministic options have been ruled out
- describes the workload concretely
- names the real failure cost
- accounts for latency, privacy, and output structure needs
- chooses the smallest tier that plausibly clears the quality bar
- includes a substitution test plan before migration

A right-sized system does not guess. It compares.

## Typical model tiers

In this repo, the usual model classes are:
- `Deterministic`
- `Local model candidate`
- `Hosted small model candidate`
- `Frontier model justified`
- `Do not automate yet`

Most real sizing work is about deciding between:
- local model
- hosted small model
- frontier model

## Signals that a workflow may be over-sized

A workflow is a strong candidate for downshifting when:
- the task repeats at volume
- outputs must follow a stable format
- the acceptable answer space is bounded
- the task mostly classifies, ranks, extracts, or rewrites within constraints
- latency or cost is already a concern
- nobody has run a real comparison against a smaller tier

## Common failure modes

### 1. Sizing models around a bad workflow
If the task should really be code or rules, model-sizing is the wrong conversation. Start with Principle 01.

### 2. Choosing by reputation
Model popularity is not evidence. Workload shape is evidence.

### 3. Ignoring failure cost
A low-cost workflow with minor consequences can tolerate smaller models more easily than a high-consequence workflow.

### 4. Downshifting without a test plan
A model recommendation without a comparison plan is only a hunch.

## Before / after example

### Before
A support operations workflow uses a frontier model to:
- classify incoming messages
- extract account details
- route each item to the right queue
- draft a standard acknowledgment

### After
- deterministic parser extracts known fields
- small hosted model handles the bounded classification step
- rules route the ticket
- standard acknowledgment is templated
- frontier model is removed entirely

The workflow still uses inference where it helps, but the expensive default is gone.

## Relationship to the other principles

This principle is downstream of determinism.

If a workflow should be code, it should not be model-sized at all.
If it still needs inference, then the next question is how small and constrained the model layer can become.

Related principles:
- [Principle 01: Default to determinism](01-default-to-determinism.md)
- [Principle 04: Measure inference cost](04-measure-inference-cost.md)
- [Principle 05: Local-first where possible](05-local-first-where-possible.md)

## Use the executable skill

To apply this principle in a real system, use:
- [`skills/02-minimum-sufficient-model/SKILL.md`](../skills/02-minimum-sufficient-model/SKILL.md)

That skill scores the workload, maps it to the shared taxonomy, and produces a concrete right-sizing recommendation with a substitution test plan.
