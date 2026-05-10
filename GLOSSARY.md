# Glossary 

This repo uses a small vocabulary on purpose. 

Don't let two people use the same term for different things. Use these definitions for principles, skills, and new docs. 

## Determinism 

The same input produces the same output through rules, code, parsing, or fixed logic. 

Determinism is the first thing to check. If a workflow can be done this way, it should be. 

Related reading: 
- [Principle 01: Default to determinism](principles/01-default-to-determinism.md) 

## Determinism score 

A quick way to describe how much a workflow step depends on inference. 

Lower scores point toward code. Higher scores point toward model judgment. 

Score reference: 
- **0**: Fully deterministic. Rules, parsing, formatting. 
- **1**: Mostly rules. Small threshold decisions. 
- **2**: Bounded judgment. Stable inputs and outputs. 
- **3**: Open-ended judgment. Still constrainable. 
- **4**: Frontier-level reasoning genuinely required. 

## Bounded judgment 

The task needs inference, but the job is narrow. 

Inputs are stable. Output shape is known. The acceptable range is limited. 

Examples: 
- classify a support request into a fixed list 
- extract fields from a predictable document 
- rewrite text into a strict format 
- flag whether a transcript section matches a label 

Bounded judgment is where teams often overpay. A frontier model might work, but that doesn't make it the right choice. 

Related reading: 
- [Principle 02: Minimum sufficient model](principles/02-minimum-sufficient-model.md) 

## Deterministic workload 

A workflow or step handled by code, rules, or scripts instead of a model. 

Common signs: 
- stable input fields 
- stable output fields 
- routing by written rules 
- formatting or parsing 

When a workflow fits this class, the recommendation is: 
- `Replace with code` 
- `Replace with workflow rule` 

## Local model candidate 

A task that needs inference, but is narrow and frequent enough for your own hardware. 

Common signs: 
- low to moderate reasoning 
- privacy matters 
- API spend is piling up 
- latency matters 

Local only makes sense if the workload fits and the hardware is real. 

Related reading: 
- [Principle 05: Local-first where possible](principles/05-local-first-where-possible.md) 

## Hosted small model candidate 

A task that needs inference, but doesn't need frontier-level capability. 

Common signs: 
- low to moderate reasoning 
- structured output 
- frequent repetition 
- cost and latency matter more than range 

Related labels: 
- `Downshift model tier` 

## Frontier model justified 

A larger model is still warranted after checking cheaper paths. 

That case has to be earned. 

Common signs: 
- needs synthesis or hard reasoning 
- high failure cost 
- smaller tiers missed the bar 
- code can't remove the hard part 

Back this label with evidence. Don't use it just because you started with the biggest model and never looked back. 

## Inference cost 

The full cost of running model calls inside a workflow. 

This is more than one API hit. You need to know: 
- cost per run 
- the most expensive call 
- cost at scale (daily, monthly, annual) 

Related reading: 
- [Principle 04: Measure inference cost](principles/04-measure-inference-cost.md) 

## Auditability 

A workflow output you can trace, review, and defend later. 

Auditability has four parts: 
- reproducibility 
- traceability 
- explainability 
- logging 

If you can't defend why an exact result happened, the output is not auditable. 

Related reading: 
- [Principle 06: Auditable by design](principles/06-auditable-by-design.md) 

## Instrumentation gap 

A place where the workflow cannot be measured. 

Examples: 
- missing token counts 
- unknown cost per call 
- unrecorded model versions 

If you hit a gap, add measurement before you change the model stack. 

## Recommendation labels 

Standard labels used across skills: 
- `Replace with code` 
- `Replace with workflow rule` 
- `Downshift model tier` 
- `Move local` 
- `Add instrumentation first` 
- `Keep current approach (with justification)` 

## How to use this glossary 

If a term feels fuzzy, come back here. Then force the term to mean something concrete in your workflow. 

