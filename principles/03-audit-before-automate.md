# Principle 03: Audit before automate

Map the workflow as it actually exists before you decide where a model belongs.

This stops you from automating the imagined workflow instead of the real one. Skip the audit, and you just preserve waste.

## What this principle is trying to prevent

A lot of AI projects start from the wrong question.

They ask:
- where can we add AI?
- what can the model do here?
- how do we speed this up with an LLM?

Those questions are too late.

The first question should be:
- what is this workflow actually trying to produce, step by step, and which parts are genuinely hard?

A real workflow audit usually reveals:
- unnecessary steps
- duplicated steps
- model calls doing deterministic work
- human judgment that is really just unwritten policy
- outputs that are immediately reformatted or discarded downstream

## What good looks like

A good workflow audit:
- states the workflow goal clearly
- maps every current step in sequence
- records who or what performs each step
- identifies inputs and outputs at each step
- scores each step for determinism
- separates genuine inference from everything else
- recommends a redesigned workflow before anyone builds

This is upstream work.
It reduces bad automation before it starts.

## Signals that a workflow needs an audit

You should audit first when:
- a team wants to introduce AI into a workflow for the first time
- an existing AI workflow is slow, expensive, or unreliable
- nobody can explain which step truly needs inference
- the workflow has multiple handoffs or multiple tools
- the process documentation and the real process are probably different

## Common failure modes

### 1. Auditing the documented process instead of the real process
The official workflow and the actual workflow are often not the same.

### 2. Skipping the boring steps
The boring steps are often the ones that should become code.

### 3. Treating every human step as judgment
Many human steps are really policy, validation, formatting, or routing.

### 4. Preserving steps that exist only because the workflow grew badly
Some steps should not be automated. They should be removed.

## Before / after example

### Before
A content team says they need an AI workflow to turn transcripts into social posts.

After mapping the real workflow, the process turns out to be:
- transcript cleanup
- quote extraction
- approval routing
- formatting for channels
- asset tagging
- final copy review

Only one or two of those steps need open-ended language judgment.
Most of the rest are deterministic or rules-based.

### After
- transcript cleanup becomes code
- asset tagging becomes rules
- approval routing becomes workflow logic
- model use is isolated to selecting and refining promising excerpts

The result is a smaller, clearer system with less waste.

## Relationship to the other principles

This principle is upstream of the rest.

Before you default to determinism, size models, measure cost, or assess local viability, you should understand the workflow shape.

Related principles:
- [Principle 01: Default to determinism](01-default-to-determinism.md)
- [Principle 02: Minimum sufficient model](02-minimum-sufficient-model.md)
- [Principle 04: Measure inference cost](04-measure-inference-cost.md)

## Use the executable skill

To apply this principle in a real system, use:
- [`skills/03-audit-before-automate/SKILL.md`](../skills/03-audit-before-automate/SKILL.md)

That skill maps the workflow step by step, scores determinism, identifies waste and redundancy, and recommends a redesigned target workflow before automation proceeds.
