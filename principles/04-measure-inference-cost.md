# Principle 04: Measure inference cost

Treat model spend as a workflow property, not an abstract API line item.

If you don't know what one run costs, you don't know if the workflow is efficient.

This principle exists because AI costs often stay invisible until the bill becomes painful. By then, the workflow is already embedded in production.

## What this principle is trying to prevent

Most teams can tell you which model they use.
Far fewer can tell you:
- what one workflow run costs
- which call contributes most of that cost
- what the workflow costs at daily, monthly, or annual volume
- whether the expensive call is actually justified

That is the gap this principle closes.

The unit that matters is usually not cost per API call.
It is cost per workflow run.

A workflow with eight small calls may cost less than a workflow with two large calls. Until you measure at the workflow level, you are mostly guessing.

## What good looks like

A good cost measurement practice:
- names every inference call in the workflow
- records model, provider, and purpose
- estimates or measures token use per call
- calculates cost per call
- sums to cost per workflow run
- projects cost at actual operating volume
- ranks calls by cost contribution
- identifies where instrumentation is missing

That gives you something to fix.

## Signals that a workflow needs cost measurement now

You should measure inference cost when:
- a prototype is moving toward production
- API bills exist but cannot be tied to workflows
- a repeated workflow has never had cost-per-run measured
- a team suspects one or two calls are dominating spend
- you want a baseline before optimization work

## Common failure modes

### 1. Measuring per call but not per workflow
Per-call pricing is useful background. It is not operational visibility.

### 2. Ignoring conditional calls
Escalations, retries, fallback calls, and long-tail cases still affect cost.

### 3. Using stale pricing
Model prices move. A cost report without a pricing date decays quickly.

### 4. Stopping at measurement
Measurement should route you into action: determinism work, model right-sizing, or better instrumentation.

## Before / after example

### Before
A team knows they use several models in one customer-support workflow. They know the monthly bill feels high, but they cannot explain which part of the workflow creates it.

### After
They instrument the workflow and learn:
- one summarization call accounts for 48% of per-run cost
- the expensive call runs on every execution
- the task scores low on determinism and moderate on reasoning intensity
- the obvious next step is to test a smaller model tier

That turns vague concern into a ranked optimization target.

## Relationship to the other principles

Cost measurement does not replace design judgment. It supports it.

Once you know where spend is concentrated, you can route the expensive parts to the right next principle:
- Principle 01 if the work should become code
- Principle 02 if the model is over-sized
- Principle 05 if repeated API spend may justify local execution

Related principles:
- [Principle 01: Default to determinism](01-default-to-determinism.md)
- [Principle 02: Minimum sufficient model](02-minimum-sufficient-model.md)
- [Principle 05: Local-first where possible](05-local-first-where-possible.md)

## Use the executable skill

To apply this principle in a real system, use:
- [`skills/04-measure-inference-cost/SKILL.md`](../skills/04-measure-inference-cost/SKILL.md)

That skill names every inference call, calculates cost-per-run, projects cost at volume, ranks the biggest contributors, and identifies what to fix first.
