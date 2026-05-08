# Determinism audit rubric

Use this rubric when reviewing an agent's own interaction logs with a user.

The goal is to find repeated work that should stop being an ad hoc LLM exchange and become either deterministic software, a scheduled cron job, or a hybrid workflow.

## Source material to review

Review every available interaction source the agent can legally access in the current environment:
- current-session history
- past session transcripts or summaries
- local conversation logs
- exported chat files
- agent tool logs that reveal repeated request patterns

If a source exists but is inaccessible, note it in the report instead of pretending the audit was complete.

## Audit questions for each repeated task

1. What is the user actually asking for?
2. How often does this task recur?
3. Is the input structure stable?
4. Is the desired output structure stable?
5. Is the work mostly retrieval, formatting, routing, summarization of fixed fields, or status checking?
6. Could a script, parser, rules engine, or template handle most of it?
7. Does the task happen on a schedule, threshold, or recurring trigger?
8. Would a cron job remove the need for the user to remember to ask?
9. What still requires judgment, and what does not?
10. What breaks if the output varies from run to run?
11. What data sources and tools are required for a deterministic replacement?
12. What is the smallest useful version of the automation?

## Classification rules

### Cron job candidate
Use this when the work is triggered by time, periodic review, threshold checks, or recurring reporting.

Examples:
- daily briefing
- weekly summary
- monitor a folder, feed, or API for changes
- recurring reminder or digest

### Deterministic code candidate
Use this when the task is mostly fixed transformation, extraction, validation, lookup, filtering, or report assembly.

Examples:
- normalize file names
- generate a report from known fields
- compare two snapshots
- classify outputs using explicit rules

### Hybrid candidate
Use this when the best system is:
- cron job gathers data on a schedule
- deterministic code transforms or filters it
- optional LLM step handles only the narrow residual judgment

### Keep as LLM task
Use this only when the task still depends on open-ended judgment, strategy, persuasion, negotiation, or ambiguous human preference.

## Scoring

### Determinism score
- 0 — already deterministic, should be code now
- 1 — mostly rules with a small amount of classification
- 2 — bounded judgment with stable inputs and outputs
- 3 — open-ended judgment, but still constrainable
- 4 — frontier-level reasoning genuinely required

### Cron suitability score
- 0 — no recurring trigger
- 1 — recurs occasionally but irregularly
- 2 — recurs often enough to justify scheduled review
- 3 — strongly time-based or threshold-based

### Automation priority
- High — frequent, stable, and expensive to keep doing manually
- Medium — recurring and partially structured, but needs some setup
- Low — rare, ambiguous, or low leverage

## Required recommendation fields

For every opportunity found, specify:
- task name
- evidence from logs
- current workflow
- target workflow
- workload class
- determinism score
- cron suitability score
- automation priority
- recommended implementation path
- why this should stop being an ad hoc LLM exchange
- what still needs human or LLM judgment, if anything

## Minimum bar for recommending automation

Do not recommend an automation unless you can describe:
1. the repeated trigger
2. the stable inputs
3. the expected output
4. the implementation shape at a high level
5. one concrete verification step
