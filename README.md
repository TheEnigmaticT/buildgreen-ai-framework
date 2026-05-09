# Build Green AI

Build Green AI is an open resource for designing AI systems that cost less, waste less compute, and stay easier to justify.

This repo has two jobs:

1. explain the principles behind greener AI use
2. provide repeatable skills and templates for applying those principles to real workflows

The goal is not to ban model use. The goal is to stop paying for model calls when code, rules, smaller models, local models, or better workflow design would do the job better.

## Who this is for

- operators running AI-heavy workflows
- teams trying to reduce AI spend without losing useful capability
- builders deciding when to use code, local models, small hosted models, or frontier models
- consultants and educators who need a practical framework for greener AI decisions

## Start here

If you are new to the repo, use this order:

1. Read the six principles below.
2. Open `skills/README.md` to see how the executable layer is organized.
3. Pick one workflow you already run often.
4. Use the most relevant skill to assess that workflow.
5. Record the result with one of the provided templates.

If you want the theory first, start in `principles/`.
If you want the operational layer first, start in `skills/`.
If you want model-selection guidance, start in `models/`.

## The six principles

### 1. Default to determinism
If a workflow is mostly rules, transformations, extraction, routing, or validation, it should usually become code or a rules-based workflow before it becomes another model call.

### 2. Minimum sufficient model
Use the smallest model tier that reliably does the job. Frontier models should be justified, not assumed.

### 3. Audit before automate
Do not automate a bad workflow just because an LLM can sit in the middle of it. Audit the workflow first.

### 4. Measure inference cost
If you do not measure cost, latency, volume, and failure modes, you cannot manage them.

### 5. Local-first where possible
When privacy, latency, cost control, or predictable throughput matter, check whether the workload should move local.

### 6. Auditable by design
A workflow should be explainable, reviewable, and traceable. If nobody can say why it produced an output, the system is fragile.

## How this repo is organized

### `principles/`
Public principle documents. This is the human-readable layer.

### `skills/`
Executable coaching skills. This is the operational layer.

Each skill is designed to tell an agent or operator:
- when to use it
- what inputs to gather
- how to classify the workload
- what output to produce
- how to verify the recommendation

### `models/`
Current model recommendations, selection guidance, and update rules.

### `contributing/`
Contribution rules for expanding the principles, skills, templates, and guidance.

### `docs/plans/`
Implementation notes and internal build planning for the repo itself.

## A simple way to use this repo

Take one AI workflow you already run and ask four direct questions:

1. Is this actually deterministic work in disguise?
2. If not, is the current model larger than the task needs?
3. If model use remains justified, do we know what it costs?
4. Can we make the workflow more local, more constrained, and more auditable?

That sequence alone will find a surprising amount of waste.

## What this repo produces

Build Green AI is meant to produce decisions, not slogans.

A good output from this repo should end in one of a few clear recommendations:
- replace with code
- replace with workflow rule
- downshift model tier
- move local
- add instrumentation first
- keep the current approach, but justify it

## Current state

The executable skill layer is already present.

The public principle layer and public model-guidance layer are still being expanded. See `BACKLOG.md` for the current roadmap.

## Contributing

Start with:
- `contributing/README.md`
- `contributing/writing-build-green-ai-skills.md`

Contributions should make the repo more practical, more explicit, and easier to verify.

## License

This public repo is licensed under **CC BY 4.0**.

You can use and adapt the contents with attribution. See `LICENSE` for the full legal text.
