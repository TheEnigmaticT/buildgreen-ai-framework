# Principle 06: Auditable by design

Build workflows so high-stakes outputs can be explained, traced, and defended.

This matters for legal, financial, or safety decisions. A raw model call isn't just expensive. It's a liability.

## What this principle is trying to prevent

A system can be useful and still be impossible to defend.

That happens when:
- the output varies on identical inputs
- the model version is not pinned
- inputs and outputs are not logged
- nobody can reconstruct the process later
- a regulator, auditor, client, or court would get only a vague explanation

In low-stakes creative work, that may be acceptable.
In high-stakes workflows, it is not.

## What good looks like

A good auditable design:
- identifies which outputs are consequential
- defines what must be provable and to whom
- logs inputs, outputs, and process metadata
- pins model versions when inference remains in the loop
- separates deterministic and stochastic components clearly
- replaces high-risk stochastic steps when auditability is non-negotiable

The more of a workflow becomes deterministic, the easier it becomes to audit.

## The four auditability dimensions

This repo evaluates auditability across four dimensions:
- **Reproducibility:** can the same inputs produce the same output again?
- **Traceability:** can the output be linked to its exact inputs, process, and model version?
- **Explainability:** can the reason for the output be stated plainly?
- **Logging:** are the output, inputs, and process retained appropriately?

An output that fails one of these dimensions has an auditability gap.

## Signals that a workflow needs this principle

Use this principle when:
- outputs feed regulated or consequential decisions
- a bad output has legal, financial, or safety consequences
- external review is possible or expected
- the team needs to demonstrate process compliance later
- an existing AI workflow is being evaluated for readiness in a regulated environment

## Common failure modes

### 1. Confusing explainability with accuracy
A wrong answer can still be auditable. Auditability is about traceable process, not correctness.

### 2. Assuming logging alone is enough
Logging a stochastic output is not the same as making it reproducible.

### 3. Treating the whole workflow as safe because some steps are logged
Every consequential output needs its own assessment.

### 4. Recommending documentation where determinism is required
For high-stakes outputs, documenting a stochastic step is often weaker than replacing it.

## Before / after example

### Before
A compliance-sensitive review workflow uses an LLM to produce a recommendation, but does not pin the model version or retain enough information to reproduce the result later.

### After
The team maps the consequential outputs, identifies the auditability gaps, and either:
- converts the risky step to deterministic code
- or adds the controls needed to make the remaining model use defensible

That turns an opaque workflow into one that can be reviewed and justified.

## Relationship to the other principles

This principle overlaps strongly with Principle 01.

Deterministic systems are easier to audit. That means the environmental case and the compliance case often point to the same architectural answer.

Related principles:
- [Principle 01: Default to determinism](01-default-to-determinism.md)
- [Principle 03: Audit before automate](03-audit-before-automate.md)
- [Principle 04: Measure inference cost](04-measure-inference-cost.md)

## Use the executable skill

To apply this principle in a real system, use:
- [`skills/06-auditable-by-design/SKILL.md`](../skills/06-auditable-by-design/SKILL.md)

That skill identifies consequential outputs, scores auditability across the four dimensions, names the gaps, and recommends the right remediation path for each one.
