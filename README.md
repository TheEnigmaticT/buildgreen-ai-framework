# Build Green AI

Build Green AI is an open resource for designing AI systems that cost less, waste less compute, and stay easier to justify.

This repo has two jobs:

1. explain the principles behind greener AI use
2. provide repeatable skills and templates for applying those principles to real workflows

We aren't here to ban models. We're here to stop paying for them when code, rules, smaller models, or better workflow design do the job better.

## Who this is for

- operators running AI-heavy workflows
- teams trying to reduce AI spend without losing useful capability
- builders deciding when to use code, local models, small hosted models, or frontier models
- consultants and educators who need a practical framework for greener AI decisions

## Start here

If you are new to the repo, use this order:

1. Read the six principle docs in `principles/`.
2. Open `skills/README.md` to see how the executable layer is organized.
3. Pick one workflow you already run often.
4. Use the most relevant skill to assess that workflow.
5. Record what you found using the templates.

If you want the theory first, start here:
- [`principles/01-default-to-determinism.md`](principles/01-default-to-determinism.md)
- [`principles/02-minimum-sufficient-model.md`](principles/02-minimum-sufficient-model.md)
- [`principles/03-audit-before-automate.md`](principles/03-audit-before-automate.md)
- [`principles/04-measure-inference-cost.md`](principles/04-measure-inference-cost.md)
- [`principles/05-local-first-where-possible.md`](principles/05-local-first-where-possible.md)
- [`principles/06-auditable-by-design.md`](principles/06-auditable-by-design.md)

If you want the operational layer first, start in `skills/`.
If you want model-selection guidance, start in `models/`.

## The six principles

### 1. Default to determinism
If a workflow is mostly rules, transformations, or validation, it should become code before you add a model.

### 2. Minimum sufficient model
Use the smallest model that reliably does the job. Justify frontier models; don't assume them.

### 3. Audit before automate
Don't automate a bad workflow just because an LLM can sit in it. Audit first.

### 4. Measure inference cost
If you don't measure cost and latency, you can't manage them.

### 5. Local-first where possible
When privacy or cost matter, check if the workload should move local.

### 6. Auditable by design
A workflow should be reviewable and traceable. If nobody knows why it produced an output, the system is fragile.

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

Take one workflow you already run and ask four questions:

1. Is this actually code in disguise?
2. Is the current model larger than the task needs?
3. Do we know what it costs?
4. Can we make the workflow local and auditable?

That sequence alone will find a surprising amount of waste.

## What this repo produces

Build Green AI produces decisions, not slogans.

A good recommendation looks like this:
- replace with code
- replace with workflow rule
- downshift model tier
- move local
- add instrumentation first
- keep the current approach (with justification)

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
