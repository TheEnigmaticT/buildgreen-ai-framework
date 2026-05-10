# Principle Routing 

Use this guide when a workflow feels wrong, but you don't know where to start. 

Start with the shape of the problem. Not the tool. Not the model. 

## The fast route 

If you ask only one question, ask this: 

**Should this be code instead?** 

If the answer is maybe, start with: 
- [Principle 01: Default to determinism](principles/01-default-to-determinism.md) 

## Decision tree 

### 1. Is the workflow fuzzy or poorly mapped? 

Signals: 
- nobody can describe the current steps 
- too many handoffs 
- suspected duplicated work 
- process grew by accretion 

Start here: 
- [Principle 03: Audit before automate](principles/03-audit-before-automate.md) 

Why: 
A bad workflow doesn't become good because a model sits in it. 

--- 

### 2. Is the work stable or rules-based? 

Signals: 
- fixed inputs 
- stable output shape 
- routing by written criteria 
- repetitive reports 
- extraction or formatting 

Start here: 
- [Principle 01: Default to determinism](principles/01-default-to-determinism.md) 

Why: 
This is the first place to cut waste. 

--- 

### 3. Does it need inference, but the current model is too big? 

Signals: 
- frontier models used for routine ops 
- cost pressure without quality proof 
- latency complaints 
- bounded tasks using large models 

Start here: 
- [Principle 02: Minimum sufficient model](principles/02-minimum-sufficient-model.md) 

Why: 
Workflows can need inference and still be wildly over-sized. 

--- 

### 4. Is it already running, but nobody knows the cost? 

Signals: 
- monthly bills with no explanation 
- no cost-per-run number 
- no ranking of expensive calls 
- no token visibility 

Start here: 
- [Principle 04: Measure inference cost](principles/04-measure-inference-cost.md) 

Why: 
You can't fix cost blind. 

--- 

### 5. Do privacy or cost make cloud calls look suspect? 

Signals: 
- sensitive data leaves your perimeter 
- API spend is climbing 
- latency matters 
- local hardware exists 

Start here: 
- [Principle 05: Local-first where possible](principles/05-local-first-where-possible.md) 

Why: 
Some workloads belong on your own hardware. Check instead of guessing. 

--- 

### 6. Does the output need to survive audit or review? 

Signals: 
- regulated workflow 
- legal or financial consequence 
- safety consequence 
- external review likely 

Start here: 
- [Principle 06: Auditable by design](principles/06-auditable-by-design.md) 

Why: 
A useful output isn't enough if you can't defend it. 

## If more than one principle fits 

Use this order: 

1. [Audit before automate](principles/03-audit-before-automate.md) if the workflow is unclear 
2. [Default to determinism](principles/01-default-to-determinism.md) if stable work is mixed in 
3. [Minimum sufficient model](principles/02-minimum-sufficient-model.md) if inference remains 
4. [Measure inference cost](principles/04-measure-inference-cost.md) if it runs at volume 
5. [Local-first where possible](principles/05-local-first-where-possible.md) if cloud calls are suspect 
6. [Auditable by design](principles/06-auditable-by-design.md) if the output has consequences 

## Three quick examples 

### Example 1 
A team uses a model to sort support tickets, extract info, and route them. 

Start here: 
- [Principle 01: Default to determinism](principles/01-default-to-determinism.md) 

Why: 
Most of that belongs in code. 

### Example 2 
A workflow works, but the bill keeps climbing and nobody knows why. 

Start here: 
- [Principle 04: Measure inference cost](principles/04-measure-inference-cost.md) 

Why: 
You need the cost map before you fix things. 

### Example 3 
A compliance workflow uses a model, but the team can't explain why it gave a specific answer. 

Start here: 
- [Principle 06: Auditable by design](principles/06-auditable-by-design.md) 

Why: 
If the workflow needs defense, it needs traceability. 

## What to do next 

Open the matching `SKILL.md`, run one assessment, and end with one recommendation. 

