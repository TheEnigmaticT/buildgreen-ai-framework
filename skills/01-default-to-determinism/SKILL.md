---
name: default-to-determinism
description: Use when an agent should review its own interaction logs with a user and identify repeated tasks that should become cron jobs, deterministic code, or hybrid workflows instead of repeated LLM chats.
version: 1.0.0
author: Build Green AI
license: MIT
metadata:
  buildgreen:
    principle: 01-default-to-determinism
    tags: [green-ai, determinism, automation, cron, workflow-audit, logs]
    related_files:
      - references/log-audit-rubric.md
      - templates/determinism-audit-report.md
---

# Default to determinism

## Overview

Use this skill to review an agent's own interaction history with a user and identify repeated work that should stop being handled as ad hoc LLM chat.

The point is not to remove judgment from everything. The point is to find work that keeps being paid for with tokens even though it could be handled by deterministic code, a recurring cron job, or a hybrid workflow that leaves only the narrow judgment step to the model.

This is the light version of a larger system. For now, the skill acts as an audit and recommendation workflow.

## When to use

Use this skill when:
- the same user keeps asking for similar tasks over and over
- you want to identify work that should become software instead of chat
- you want to find recurring tasks that should become cron jobs
- you want to reduce token spend on repetitive operational work
- you want to separate stable workflow steps from real reasoning

Do not use this skill when:
- you only have a single isolated interaction with no history
- the task is mostly persuasion, negotiation, strategy, or creative judgment
- you do not have access to any conversation logs or transcript history

## Required inputs

Gather as many of these as the current environment allows:
- current conversation history
- past session transcripts or summaries
- local chat exports
- tool logs that reveal repeated patterns
- examples of tasks the user has asked for multiple times

If a source is unavailable, record that explicitly in the final report.

## Workflow

### Step 1: Find every available log source
Review every interaction source you can legally access in the current environment.

Minimum sources to check:
1. current session
2. searchable session history or transcript summaries
3. local log files or exported chats, if present
4. tool outputs that reveal recurring requests

Do not pretend the audit is complete if some sources were inaccessible.

### Step 2: Extract repeated tasks
As you read the logs, list recurring asks such as:
- repeated status checks
- repeated report generation
- repeated message drafting from fixed inputs
- repeated file or data transformations
- repeated monitoring or reminder requests
- repeated content collection or summarization tasks on a schedule

Normalize similar requests into one task family when they share the same real workflow.

### Step 3: Score each repeated task
For each task family, assign:
- workload class
- determinism score
- cron suitability score
- automation priority

Use the exact scoring language from `references/log-audit-rubric.md`.

### Step 4: Choose the target workflow
For each task family, decide whether the best next form is:
- cron job candidate
- deterministic code candidate
- hybrid candidate
- keep as LLM task

Make the recommendation based on the real workflow, not on whether an LLM can technically do it.

### Step 5: Recommend the smallest useful automation
Do not jump straight to a large platform build unless the logs justify it.

Prefer the smallest useful recommendation first:
- one cron job
- one script
- one rules-based report generator
- one cron + script pipeline

The audit should surface the smallest high-leverage next step.

### Step 6: Produce a structured report
Output the findings using the structure in `templates/determinism-audit-report.md`.

## Classification rules

### Cron job candidate
Use this when the task is driven by time, repetition, monitoring, or threshold checks.

A strong cron candidate usually has:
- a recurring cadence
- stable source data
- a predictable output shape
- low value in asking the user to remember it manually

### Deterministic code candidate
Use this when the task is mainly transformation, extraction, validation, filtering, normalization, comparison, routing, or assembly of known fields.

A strong deterministic-code candidate usually has:
- stable inputs
- stable outputs
- explicit rules
- low tolerance for output variation

### Hybrid candidate
Use this when the right design is:
- cron or trigger gathers inputs
- deterministic code handles the stable workflow
- LLM handles only a narrow residual judgment step, if any

### Keep as LLM task
Use this only when the task still depends on open-ended reasoning that cannot yet be narrowed or stabilized enough to justify automation.

## Output format

Return a report with these sections:
1. Audit scope
2. Repeated tasks found
3. Opportunities
4. Cron job candidates
5. Deterministic code candidates
6. Hybrid candidates
7. Keep as LLM tasks
8. Recommended next builds

Every opportunity must include:
- evidence from logs
- current workflow
- target workflow
- workload class
- determinism score
- cron suitability score
- automation priority
- recommended path
- what remains non-deterministic
- one verification step

## Common pitfalls

1. Treating every repeated task as a cron job
A repeated task is not automatically time-based. Some tasks should become scripts, not schedules.

2. Treating every structured task as a full software project
Recommend the smallest useful automation first.

3. Confusing summarization with judgment
Many summaries are really extraction plus formatting. Do not keep them as LLM tasks by default.

4. Recommending deterministic replacement without naming the stable inputs and outputs
If you cannot describe the stable shape, the recommendation is too vague.

5. Ignoring inaccessible logs
A partial audit is fine. An unacknowledged partial audit is not.

6. Recommending automation without verification
Every recommendation must say how to confirm it worked.

## Verification checklist

Before finalizing the report, verify:
- every accessible log source was reviewed or explicitly marked inaccessible
- repeated tasks were grouped into clear task families
- each opportunity uses the shared scoring labels exactly
- each recommendation names cron job, deterministic code, hybrid, or keep as LLM
- each recommendation explains why ad hoc chat is the wrong long-term form
- each recommendation includes one measurable verification step

## Recommended next action

After producing the audit, recommend one of these next steps:
- implement the highest-priority cron job
- implement the highest-priority deterministic script
- design a hybrid cron + deterministic workflow
- collect more logs before automating

The report should end with the single highest-leverage next build.
