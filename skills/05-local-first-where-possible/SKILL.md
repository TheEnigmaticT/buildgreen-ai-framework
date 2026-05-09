---
name: local-first-where-possible
description: Use when evaluating whether a workload that currently uses a hosted model API could be moved to local inference, or when assessing whether local execution is technically and economically viable for a given task.
version: 1.0.0
author: Build Green AI
license: CC-BY-4.0
metadata:
  buildgreen:
    principle: 05-local-first-where-possible
    tags: [green-ai, local-inference, on-prem, apple-silicon, privacy, cost]
    related_files:
      - references/local-feasibility-rubric.md
      - templates/local-inference-assessment.md
---

# Local-first where possible

## Overview

Local inference eliminates per-token API costs entirely for qualifying workloads. It also keeps sensitive data inside the organizational perimeter, resolving a class of compliance and data governance problems that cloud inference creates by design.

Local-first is not always possible, and it is not always the right answer even when it is possible. This skill exists to evaluate whether it is the right answer for a specific workload — not to advocate for local inference as a general principle.

The two conditions for local-first to be viable: the workload must fit a model that can run on available hardware, and the volume must be high enough that the infrastructure investment recovers its cost against the API spend it replaces.

## When to use

Use this skill when:
- a workload has real privacy or data residency constraints that cloud inference violates
- API spend on a repeated workload is high enough to justify infrastructure cost
- latency requirements favor local inference over round-trip API calls
- a team is evaluating Apple Silicon or other local hardware for AI workloads
- you want to know whether a hosted model call can be replaced with a local model

Do not use this skill when:
- the workload has not yet been through skill 01 (it may not need inference at all)
- the task requires frontier-level reasoning that no current local model can provide
- the organization has no path to provision or maintain local inference hardware
- the workload volume is too low to justify the operational overhead of local infrastructure

## Required inputs

Gather as many of these as the current environment allows:
- the workload description and current model in use
- current API cost per run and monthly API spend for this workload
- run frequency and volume
- privacy, compliance, or data residency requirements
- available local hardware (model, memory, whether Apple Silicon)
- latency requirements or service level targets
- team capacity to provision and maintain local inference
- any existing local model experiments or benchmark results

If information is missing, state that explicitly and flag what must be gathered before a local-first decision can be made responsibly.

## Workflow

### Step 1: Confirm the workload is a model-sizing candidate, not a determinism candidate
Before evaluating local inference, confirm this workload still legitimately needs a model. If it scores 0–1 on the determinism scale, route it to skill 01 instead.

### Step 2: Describe the workload constraints precisely
Local feasibility depends on the specifics:
- What is the actual task?
- What are the input and output formats?
- What is the acceptable quality floor?
- What is the maximum acceptable latency?
- Are there hard data residency or privacy requirements?
- What is the run volume?

Do not proceed with a local-first assessment on a vague task description.

### Step 3: Assess available hardware
Record what local inference hardware is available or could be provisioned:
- machine type and model
- RAM and unified memory (for Apple Silicon)
- whether the Neural Engine or GPU acceleration is available
- whether the hardware is already in use for other workloads

For Apple Silicon specifically: unified memory architecture allows larger models to run in-context without paging. The M-series Neural Engine is optimized for matrix operations. Idle power draw is near zero. These are engineering properties relevant to cost and feasibility, not brand considerations.

### Step 4: Identify candidate local models
Based on the workload type and hardware constraints, list candidate local models in order of preference. For each, record:
- model name and size
- memory requirement
- whether it fits on available hardware
- known strengths and limitations relevant to this workload

### Step 5: Calculate the break-even point
Estimate how long it takes for local inference to recover its infrastructure cost against the API spend it replaces.

Break-even = infrastructure cost ÷ monthly API spend replaced

If the break-even is longer than 18 months at current volume, flag it as economically marginal. If volume is growing, recalculate at projected volume.

### Step 6: Assess privacy and compliance fit
If there are data residency or compliance requirements, assess whether local inference satisfies them. Record:
- what data leaves the perimeter under the current cloud approach
- whether local inference eliminates that exposure entirely
- any residual compliance questions (e.g., model licensing, audit logging)

### Step 7: Design a local feasibility test
Produce a concrete test plan before recommending migration. The test must include:
- the local model to test
- the hardware to run it on
- the sample task set
- the pass-fail quality standard
- the latency measurement method
- the cost comparison method
- the rollback condition if quality or latency fails to meet the bar

### Step 8: Produce the structured report
Output the findings using `templates/local-inference-assessment.md`.

## Classification rules

### Strong local-first candidate
- real privacy or compliance requirement
- workload volume sufficient for break-even within 12 months
- task fits a model that runs on available hardware
- latency requirements are compatible with local inference

### Marginal local-first candidate
- no hard privacy requirement, but cost pressure is real
- break-even is 12–24 months
- hardware provisioning is possible but not yet in place
- quality uncertainty requires a feasibility test before committing

### Not viable for local
- task requires frontier-level reasoning no local model can provide
- hardware cannot be provisioned or maintained
- volume too low for break-even within a reasonable timeframe
- latency requirements exceed what local hardware can deliver

## Output format

Return a report with these sections:
1. Workload summary
2. Current API cost baseline
3. Hardware assessment
4. Candidate local models
5. Break-even analysis
6. Privacy and compliance assessment
7. Local feasibility test plan
8. Recommendation and classification

Every recommendation must include:
- workload classification (strong / marginal / not viable)
- recommendation label from shared taxonomy (Move local / Downshift model tier / Keep current approach, but justify it)
- break-even estimate
- named candidate local model
- one feasibility test plan
- one measurable verification step

## Common pitfalls

1. Treating privacy as an automatic answer for local
Local inference only resolves the data exposure problem if the model and its outputs are also kept on-prem. Assess the full data flow.

2. Ignoring operational overhead
Local inference requires someone to provision, update, and maintain the hardware and model. If that capacity does not exist, local is not free.

3. Recommending local without a break-even calculation
Cost reduction from eliminating API spend only materializes if the infrastructure cost is recovered. Always calculate.

4. Assuming Apple Silicon is always the right local hardware
Apple Silicon has real architectural advantages for AI inference, but it is not always available or appropriate. Assess what is actually available.

5. Skipping the quality floor assessment
A local model that runs cheaply but fails the quality bar is not a cost reduction — it is a quality reduction with a cost reduction on top.

6. Recommending migration without a test plan
Local inference recommendations must include a concrete test before full migration.

## Verification checklist

Before finalizing the report, verify:
- the workload was confirmed as a genuine inference requirement (not a determinism candidate)
- hardware was assessed against specific model memory requirements
- break-even was calculated with clearly labeled assumptions
- privacy assessment covers the full data flow, not just the API call
- the feasibility test plan names a specific model, hardware, sample set, and pass-fail standard
- the recommendation uses a label from the shared taxonomy

## Recommended next action

After producing the report, end with one of:
- run a local feasibility test on the named candidate model and hardware
- provision local hardware and re-evaluate once available
- keep the current API approach and re-evaluate at higher volume
- route to skill 02 for a hosted small-model assessment instead

The report should end with the single clearest next move.
