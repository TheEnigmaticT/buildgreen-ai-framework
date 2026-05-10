Pick one workflow you already run. 

Don't pick five. Pick one. 

This guide is the fastest way to get value from Build Green AI. 

Finish this in 15 to 30 minutes. 

## Step 1: Choose the workflow 

Pick something that happens more than once. 

Good candidates: 
- recurring summaries 
- intake classification 
- report generation 
- content repurposing 
- document extraction 
- support or ops routing 

Bad candidates: 
- one-off research 
- purely creative work 
- a workflow you can't describe yet 

## Step 2: Write the workflow in one sentence 

Use this format: 

`This workflow takes [input] and produces [output] for [person/team].` 

Example: 

`This workflow takes inbound support emails and produces a routed ticket for the support queue.` 

If you can't write that sentence clearly, stop. 

You don't understand the workflow yet. 

Read [Principle 03: Audit before automate](principles/03-audit-before-automate.md). 

## Step 3: Ask the first hard question 

Is this actually code in disguise? 

Look for work like: 
- parsing 
- validation 
- formatting 
- field extraction 
- routing by rules 
- repetitive report assembly 

If most of the workflow looks like that, start here: 
- [Principle 01: Default to determinism](principles/01-default-to-determinism.md) 
- [`skills/01-default-to-determinism/SKILL.md`](skills/01-default-to-determinism/SKILL.md) 

## Step 4: If it still needs inference, size the model 

If the workflow still needs judgment, ask: 
- Is the current model larger than the task needs? 
- Would a smaller hosted model work? 
- Would a local model work? 

Read: 
- [Principle 02: Minimum sufficient model](principles/02-minimum-sufficient-model.md) 
- [Principle 05: Local-first where possible](principles/05-local-first-where-possible.md) 

Use: 
- [`skills/02-minimum-sufficient-model/SKILL.md`](skills/02-minimum-sufficient-model/SKILL.md) 
- [`skills/05-local-first-where-possible/SKILL.md`](skills/05-local-first-where-possible/SKILL.md) 

## Step 5: Measure the current cost 

If the workflow runs in production or at volume, measure it before you change it. 

You need to know: 
- which model calls happen 
- which call costs the most 
- what one run costs 
- what the workflow costs at scale 

Read: 
- [Principle 04: Measure inference cost](principles/04-measure-inference-cost.md) 

Use: 
- [`skills/04-measure-inference-cost/SKILL.md`](skills/04-measure-inference-cost/SKILL.md) 

## Step 6: Check the output audit path 

If the output affects compliance, legal, money, or safety, ask: 

Can you explain why this exact output happened? 

If the answer is no, read: 
- [Principle 06: Auditable by design](principles/06-auditable-by-design.md) 

Use: 
- [`skills/06-auditable-by-design/SKILL.md`](skills/06-auditable-by-design/SKILL.md) 

## Step 7: End with one recommendation 

Don't end with a vague reflection. 

End with one move: 
- replace with code 
- replace with workflow rule 
- downshift model tier 
- move local 
- add instrumentation first 
- keep the current approach, with justification 

One workflow. One recommendation. 

That's enough to start. 

## What to do next 

If this first pass worked: 
- run the process on your next repeated workflow 
- add a written assessment using the templates 
- build a library of before/after cases 

This is how the repo becomes a system instead of a pile of principles.
