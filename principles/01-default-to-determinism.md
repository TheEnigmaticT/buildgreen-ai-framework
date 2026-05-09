# Principle 01: Default to determinism

Default to determinism means this: if rules, code, or structured logic can handle a workflow, it shouldn't stay a model call.

Start here for greener AI.

Most waste comes from paying model costs for stable work.

## What this principle is trying to prevent

Teams put a model in the middle because it's fast. That's fine for a prototype. It's a problem when that call handles:
- formatting known fields
- classifying into stable buckets
- extracting structured data
- routing items by explicit criteria
- generating routine reports from fixed inputs
- checking thresholds or monitoring recurring conditions

Those are usually signs that the workflow should move toward code, rules, or a hybrid design where the model only handles the narrow part that still needs judgment.

## What good looks like

A good design:
- uses code for transformations
- uses workflow rules for decisions
- uses triggers for recurring jobs
- leaves models for real ambiguity
- names the exact part that is still non-deterministic

Don't force determinism onto everything.
Do stop treating model use as the default shape of operational work.

## Signals that a workflow should become deterministic

Turn a workflow into code if:
- the inputs are stable
- the outputs are stable
- the rules can be written down
- the task happens repeatedly
- output variation is not useful
- a human would describe the job as "mostly the same every time"

This is especially true for internal operations work where reliability matters more than stylistic flexibility.

## Common failure modes

### 1. Treating repetition as intelligence
A task that happens often is not automatically a model problem. Repetition usually means it is worth stabilizing.

### 2. Automating the whole workflow with a model
A workflow may contain one narrow judgment step and five deterministic steps. The right answer is usually to isolate the judgment step, not keep the whole chain stochastic.

### 3. Jumping from chat to platform build
The first deterministic improvement is often small:
- one script
- one cron job
- one report generator
- one parser with one escalation path

You do not need a giant system to stop wasting tokens.

### 4. Confusing summarization with reasoning
Many things labeled as "summaries" are actually extraction plus formatting. Those often belong in deterministic code.

## Before / after example

### Before
A team asks a model every morning to:
- check a few dashboards
- summarize the same metrics
- flag any threshold breaches
- post the result in Slack

### After
- scheduled job collects the metrics
- deterministic script checks thresholds
- deterministic formatter builds the report
- model is used only if an anomaly needs interpretation

That is greener, cheaper, and more reliable.

## Relationship to the other principles

This principle comes first for a reason.

Before you choose a model, measure cost, or assess local feasibility, you should ask whether the workflow should be a model workflow at all.

Related principles:
- [Principle 02: Minimum sufficient model](02-minimum-sufficient-model.md)
- [Principle 03: Audit before automate](03-audit-before-automate.md)
- [Principle 06: Auditable by design](06-auditable-by-design.md)

## Use the executable skill

To apply this principle in a real system, use:
- [`skills/01-default-to-determinism/SKILL.md`](../skills/01-default-to-determinism/SKILL.md)

That skill is designed to review logs or workflow history, identify repeated task families, classify them, and recommend the smallest useful automation path.
