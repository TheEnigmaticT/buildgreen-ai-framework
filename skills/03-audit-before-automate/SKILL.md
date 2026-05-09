---
name: audit-before-automate
description: Use when a team wants to introduce AI into a workflow, or suspects their existing AI-assisted workflow is poorly designed. Maps the actual workflow before recommending any automation.
version: 1.0.0
author: Build Green AI
license: CC-BY-4.0
metadata:
  buildgreen:
    principle: 03-audit-before-automate
    tags: [green-ai, workflow-audit, process-mapping, automation, pre-build]
    related_files:
      - references/workflow-map-rubric.md
      - templates/workflow-audit-report.md
---

# Audit before automate

## Overview

Use this skill before building anything. The most common failure mode in AI workflow design is building a solution for the workflow as imagined rather than the workflow as it actually exists.

The actual workflow, when mapped honestly, almost always reveals unnecessary steps, redundant processes, and tasks that were already handled deterministically by humans — which means they can be expressed as code more easily than anyone expected.

This skill is upstream of all other Green AI skills. If you have not mapped the workflow, you do not yet know whether it needs AI at all.

## When to use

Use this skill when:
- a team wants to introduce AI into an existing workflow for the first time
- an existing AI workflow feels expensive, slow, or unreliable
- you suspect the workflow was designed around what the AI can do rather than what the business needs
- someone is about to start building without a clear picture of current state
- a workflow involves multiple steps and it is unclear which ones actually require inference

Do not use this skill when:
- the workflow is already fully mapped and the audit is current
- the task is a one-off with no repeating structure
- you are only sizing a model for an already-well-understood task (use skill 02 instead)

## Required inputs

Gather as many of these as the current environment allows:
- a description of the workflow goal and what a successful output looks like
- a description of every step currently performed, in order
- who or what performs each step (human, rule, script, LLM)
- the inputs and outputs at each step
- the frequency and volume of the workflow
- examples of edge cases or failure modes
- time and cost estimates for each step if available
- any existing documentation, SOPs, or process maps

If information is missing, state that explicitly and flag it as an audit gap.

## Workflow

### Step 1: State the workflow goal
Write one sentence that describes what the workflow is supposed to produce and for whom. If this cannot be written clearly, stop and gather that clarity before proceeding.

### Step 2: Map every current step
List every step in the current workflow in sequence. For each step, record:
- what triggers it
- who or what performs it
- what enters the step
- what leaves the step
- whether it is currently performed by a human, a rule, a script, or a model

Do not skip steps that seem obvious. The audit value is often in the steps everyone assumes are trivial.

### Step 3: Score each step on the determinism scale
For each step, assign a determinism score using the shared taxonomy:
- 0 — already deterministic, should be or already is code
- 1 — mostly rules with a small amount of classification
- 2 — bounded judgment with stable inputs and outputs
- 3 — open-ended judgment, but still constrainable
- 4 — frontier-level reasoning genuinely required

Record the score and a one-sentence justification for each step.

### Step 4: Identify waste and redundancy
Flag any steps that are:
- duplicated elsewhere in the workflow
- performed by a model but scorable at 0 or 1
- present only because the original workflow was not designed for automation
- producing outputs that are immediately discarded or reformatted by the next step

### Step 5: Identify the genuinely hard steps
Separate the steps that actually require inference from those that do not. A step requires inference only if it involves reasoning that cannot yet be expressed as rules, parsing, or structured logic.

### Step 6: Recommend the redesigned workflow
Describe the target workflow. For each step, recommend one of:
- keep as-is (already optimal)
- replace with deterministic code
- replace with a workflow rule
- right-size to a smaller model (route to skill 02)
- keep on current model with explicit justification
- remove entirely (unnecessary step)

### Step 7: Produce the structured report
Output the findings using `templates/workflow-audit-report.md`.

## Classification rules

### Steps to replace with code
Steps that are mainly parsing, formatting, extraction, validation, filtering, routing, field assembly, or transformation of known inputs with known outputs.

### Steps to replace with a workflow rule
Steps that are currently handled by human judgment but follow a pattern that can be expressed as conditional logic once the pattern is written down.

### Steps to right-size
Steps that genuinely need inference but are currently using a more powerful model than the task requires. Route these to skill 02.

### Steps to keep
Steps that require open-ended reasoning, nuanced synthesis, or judgment that cannot yet be narrowed into rules. These should be explicitly justified, not just assumed.

### Steps to remove
Steps that exist because the workflow was built incrementally without a clear design, and whose outputs are not actually used downstream.

## Output format

Return a report with these sections:
1. Workflow goal
2. Current workflow map (step by step)
3. Determinism scores
4. Waste and redundancy found
5. Steps that require genuine inference
6. Recommended redesigned workflow
7. Estimated cost and complexity impact
8. Open audit gaps

Every step recommendation must include:
- current form (human / rule / script / model)
- determinism score
- recommended form
- one-sentence justification
- any dependency on another step

## Common pitfalls

1. Auditing the imagined workflow instead of the real one
Talk to the people who actually do the work. The documented process and the real process are often different.

2. Treating "we use AI for this" as a reason to keep using AI for it
Current AI usage is not evidence the task needs AI. Audit from first principles.

3. Skipping steps that seem too simple to matter
Trivial-seeming steps are often where the most waste accumulates.

4. Mapping steps without recording inputs and outputs
A step map without data flows is too vague to act on.

5. Recommending redesign without naming what changes
Every recommendation must specify the target form, not just flag the current form as wrong.

6. Conflating step frequency with step importance
A step that runs ten thousand times per day at determinism score 0 is a high-priority fix even if it seems simple.

## Verification checklist

Before finalizing the report, verify:
- the workflow goal is stated in one clear sentence
- every step in the current workflow is named and described
- every step has a determinism score with a one-sentence justification
- waste and redundancy findings cite specific steps
- every recommended change names the target form
- audit gaps are explicitly listed rather than silently omitted

## Recommended next action

After producing the audit, recommend one of:
- implement the highest-priority deterministic replacement (route to skill 01)
- right-size the model for the highest-cost inference step (route to skill 02)
- redesign the workflow end-to-end before building anything
- collect missing inputs before proceeding

The report should end with the single clearest next move.
