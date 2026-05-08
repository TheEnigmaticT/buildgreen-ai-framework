---
name: measure-inference-cost
description: Use when a team needs to instrument AI workflows for cost tracking, establish cost-per-run as a first-class metric, or identify where inference spend is concentrated in a production system.
version: 1.0.0
author: Build Green AI
license: MIT
metadata:
  buildgreen:
    principle: 04-measure-inference-cost
    tags: [green-ai, cost-tracking, instrumentation, inference-cost, observability]
    related_files:
      - references/cost-instrumentation-rubric.md
      - templates/inference-cost-report.md
---

# Measure inference cost

## Overview

You cannot optimize what you do not measure. The reason AI costs spiral in production is that organizations treat inference cost the way they once treated cloud egress — as a line item they will optimize later. Later never comes because the workflows are already built and the cost is invisible until the bill arrives.

This skill establishes cost-per-workflow-run as the primary metric, not cost-per-API-call. A workflow that makes twelve API calls and costs $0.004 per run is more informative than knowing the per-call price of each model used.

## When to use

Use this skill when:
- an AI workflow is moving from prototype to production
- a team is receiving monthly API bills but cannot connect them to specific workflows
- cost-per-run has never been measured for a workflow that runs frequently
- a workflow's inference cost is suspected to be high but has not been quantified
- you want to establish a baseline before making optimization changes

Do not use this skill when:
- the workflow runs only once or has no repeating structure
- cost measurement is already in place and current — use the output to drive skill 01 or 02 instead

## Required inputs

Gather as many of these as the current environment allows:
- list of every AI call made in the workflow, in order
- model name and provider for each call
- approximate input token count per call (or a representative sample)
- approximate output token count per call (or a representative sample)
- current pricing for each model in use
- workflow run frequency (daily, per-event, per-user-request)
- total monthly or weekly volume if known
- any existing cost data from provider billing dashboards

If inputs are missing, state that explicitly and estimate from available evidence with clearly marked confidence levels.

## Workflow

### Step 1: List every inference call in the workflow
Name every point where the workflow calls a model. For each call, record:
- the model and provider
- the purpose of the call
- whether it runs on every workflow execution or only conditionally
- approximate token counts, if known

Do not skip conditional calls. They matter for worst-case cost and for identifying escalation paths that could be restructured.

### Step 2: Calculate per-call cost
For each inference call, calculate:
- input cost = input tokens × input price per token
- output cost = output tokens × output price per token
- total cost per call = input cost + output cost

Use current published pricing. Flag the date of the pricing used, because model prices change.

### Step 3: Calculate cost-per-workflow-run
Sum the per-call costs for a single complete workflow execution. If some calls are conditional, produce:
- minimum cost per run (only required calls)
- maximum cost per run (all calls including conditional)
- expected cost per run (weighted by actual conditional frequency if known)

### Step 4: Calculate cost at volume
Multiply cost-per-run by actual or estimated run frequency:
- daily cost
- monthly cost
- annual cost at current volume
- annual cost at 2× projected growth

Flag which figures are measured and which are estimated.

### Step 5: Rank calls by cost contribution
Sort all inference calls from highest to lowest cost contribution per workflow run. Express each as a percentage of total cost per run.

The top one or two calls almost always account for the majority of cost. These are the optimization targets.

### Step 6: Identify instrumentation gaps
Note any calls where token counts or costs could not be measured directly. Recommend instrumentation to close each gap.

### Step 7: Produce the structured report
Output the findings using `templates/inference-cost-report.md`.

## Classification rules

### High-priority optimization target
Any single call that represents more than 40% of per-run cost and has a determinism score of 0–2. Route to skill 01 or 02.

### Medium-priority optimization target
Any call that represents 15–40% of per-run cost or runs on every execution at a determinism score of 2–3.

### Instrumentation gap
Any call where cost cannot be directly measured because token counts are unavailable. Flag for immediate instrumentation before optimization.

### Justified cost
Any call that represents significant cost but has a determinism score of 3–4 and has been explicitly reviewed and accepted. Must be documented as a deliberate decision, not an oversight.

## Output format

Return a report with these sections:
1. Workflow summary
2. All inference calls (model, purpose, tokens, cost per call)
3. Cost per workflow run (min / expected / max)
4. Cost at volume (daily / monthly / annual / projected)
5. Cost ranking by call
6. High-priority optimization targets
7. Instrumentation gaps
8. Recommended next actions

Every call must include:
- model and provider
- purpose
- input and output token estimates
- per-call cost
- percentage of total per-run cost
- determinism score
- recommendation label from shared taxonomy

## Common pitfalls

1. Measuring cost per API call instead of cost per workflow run
Per-call cost hides the cumulative cost of multi-step workflows. Always measure at the workflow level.

2. Using outdated pricing
Model prices change frequently. Always record the date of the pricing data used.

3. Ignoring conditional calls
A conditional call that runs 30% of the time is still a real cost center. Measure it at its actual frequency.

4. Treating token estimates as precise
When working from samples rather than instrumentation, flag confidence levels explicitly.

5. Optimizing the smallest calls first
Always address the highest cost-contribution calls first, regardless of which optimization is easiest.

6. Stopping at measurement without recommending action
Every high-priority optimization target should route to skill 01 or skill 02.

## Verification checklist

Before finalizing the report, verify:
- every inference call in the workflow is named and costed
- pricing data is dated
- cost-per-run is reported at min / expected / max
- volume projections are clearly labeled as measured or estimated
- calls are ranked by cost contribution percentage
- every high-priority target has a recommendation label and a routing to skill 01 or 02
- instrumentation gaps are explicitly listed

## Recommended next action

After producing the report, end with one of:
- route highest-cost call to skill 01 (should this be deterministic code?)
- route highest-cost call to skill 02 (can this use a smaller model?)
- implement call-level cost instrumentation before optimizing
- establish a quarterly cost-per-run review cadence

The report should end with the single highest-leverage next move.
