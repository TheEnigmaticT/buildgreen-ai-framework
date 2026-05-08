---
name: auditable-by-design
description: Use when a workflow must produce outputs that are auditable, traceable, or defensible — particularly in regulated industries, compliance-sensitive contexts, or any system where a bad output has meaningful legal, financial, or safety consequences.
version: 1.0.0
author: Build Green AI
license: MIT
metadata:
  buildgreen:
    principle: 06-auditable-by-design
    tags: [green-ai, auditability, compliance, determinism, traceability, regulated-industries]
    related_files:
      - references/auditability-rubric.md
      - templates/auditability-assessment.md
---

# Auditable by design

## Overview

Stochastic systems produce different outputs on identical inputs. That is a feature when you need creativity or synthesis. It is a serious liability when outputs must be auditable — when a regulator, auditor, or court needs to understand exactly why a system produced a specific output on a specific date.

The design constraint is simple: if a workflow requires auditability, it must be deterministic. If it must be deterministic, it cannot be a raw LLM call.

This principle converges with Principle 01 (Default to Determinism): the more of your workflow you convert to deterministic code, the more of your workflow is automatically auditable. Environmental benefit and compliance benefit are the same architectural decision.

This skill exists for teams who are building in regulated contexts and need to assess where their auditability gaps are, and what to do about each one.

## When to use

Use this skill when:
- the workflow operates in a regulated industry (financial services, healthcare, legal, government)
- outputs may be reviewed by auditors, regulators, or courts
- a bad output has meaningful legal, financial, or safety consequences
- the team needs to demonstrate that a specific output was produced by a specific process
- an existing AI workflow is being evaluated for compliance readiness

Do not use this skill when:
- the workflow produces outputs where variation is acceptable and there is no compliance requirement
- auditability has already been assessed and is current
- the task is purely creative or exploratory with no downstream accountability

## Required inputs

Gather as many of these as the current environment allows:
- a description of every step in the workflow and who or what performs each step
- the compliance or regulatory framework that applies
- the specific auditability requirements (what must be provable, to whom, and over what retention period)
- examples of outputs and the decisions they inform
- any existing audit logging or traceability infrastructure
- the consequence of an output that cannot be explained or reproduced

If requirements are unclear, state that explicitly. Auditability assessments cannot be completed against undefined standards.

## Workflow

### Step 1: Establish the auditability requirement
Before assessing the workflow, establish what auditability actually means for this context:
- Who needs to be able to audit the outputs? (Internal compliance team, external regulator, court)
- What must be demonstrable? (That a specific output was produced, that the process was followed, that no prohibited inputs were used)
- Over what time period must the audit trail be retained?
- What is the consequence of an output that cannot be explained?

Do not assume the auditability requirement is obvious. Different frameworks impose different obligations.

### Step 2: Map every output that enters a consequential decision
Identify which outputs of the workflow feed into decisions that have compliance, legal, financial, or safety consequences. Not every output needs to be fully auditable — only the ones that matter downstream.

### Step 3: Score each consequential output on the auditability scale
For each consequential output, assess:
- **Reproducibility:** Can the exact same output be reproduced given the same inputs?
- **Traceability:** Can you trace the output back to the specific inputs, model version, and process that produced it?
- **Explainability:** Can you explain, in plain language, why the output was what it was?
- **Logging:** Is the output, its inputs, and the process that produced it logged and retained?

Score each dimension as: full / partial / none.

### Step 4: Identify auditability gaps
For each output where any dimension scores partial or none, identify the gap specifically:
- Is the gap a stochastic model call where the output varies?
- Is the gap a missing log?
- Is the gap a model version that is not pinned?
- Is the gap a process step that is undocumented?

### Step 5: Recommend remediation for each gap
For each gap, recommend the appropriate fix:
- Replace the stochastic step with deterministic code (route to skill 01)
- Pin the model version and log inputs and outputs at each call
- Add structured logging to an existing step
- Document an undocumented process step
- Redesign the step to separate the deterministic and stochastic parts

### Step 6: Assess residual risk
For any gap that cannot be fully closed, assess the residual risk:
- what cannot be made auditable and why
- what compensating controls exist
- whether the residual risk is acceptable given the regulatory context

### Step 7: Produce the structured report
Output the findings using `templates/auditability-assessment.md`.

## Classification rules

### Fully auditable
Output is deterministic, logged, traceable, and explainable. No gaps.

### Auditable with controls
Output involves stochastic inference, but model version is pinned, inputs and outputs are logged, and the process is documented. Sufficient for many compliance contexts.

### Partially auditable
Some elements are logged or deterministic, but there are meaningful gaps in reproducibility, traceability, or explainability.

### Not auditable
Raw LLM call with no pinned version, no input/output logging, and no documented process. Not acceptable for regulated workflows.

## Output format

Return a report with these sections:
1. Auditability requirements
2. Consequential outputs identified
3. Auditability scores by output and dimension
4. Gaps found
5. Remediation recommendations
6. Residual risk assessment
7. Recommended next actions

Every gap must include:
- which output it affects
- which auditability dimension it fails
- root cause (stochastic call / missing log / unpinned version / undocumented step)
- recommended remediation
- recommendation label from shared taxonomy
- estimated effort to remediate (low / medium / high)

## Common pitfalls

1. Conflating explainability with accuracy
An output can be fully auditable and still wrong. Auditability is about process traceability, not output quality.

2. Assuming logging is sufficient
Logging an LLM output does not make it reproducible if the model version is not pinned or the temperature is not fixed.

3. Treating the whole workflow as auditable because some steps are
Every consequential output must be assessed independently. One deterministic step does not make an end-to-end stochastic workflow auditable.

4. Ignoring model version drift
An LLM provider can update a model without notice. A logged output from six months ago may not be reproducible if the model has changed. Pin versions explicitly.

5. Underestimating the retention requirement
Many regulated industries require audit trails for five to seven years. Assess whether current logging infrastructure can meet that requirement before recommending a compliant approach.

6. Recommending documentation instead of determinism
Documentation of a stochastic process is better than nothing, but it is not the same as determinism. For high-stakes outputs, the right answer is usually to replace the stochastic step.

## Verification checklist

Before finalizing the report, verify:
- the auditability requirement is stated specifically, not generically
- every consequential output is identified and assessed
- every gap names the specific dimension that fails and the root cause
- every remediation recommendation uses a label from the shared taxonomy
- residual risks are assessed against the specific regulatory context
- the report does not conflate auditability with accuracy

## Recommended next action

After producing the report, end with one of:
- replace the highest-risk stochastic step with deterministic code (route to skill 01)
- implement input/output logging and model version pinning for the highest-risk call
- redesign the workflow to isolate stochastic steps from consequential outputs
- engage legal or compliance counsel to assess residual risk before proceeding

The report should end with the single clearest next move.
