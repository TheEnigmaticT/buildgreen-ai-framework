# Model right-sizing report

## Context reviewed
- materials reviewed
- workflow boundaries
- current model or provider
- current use frequency and volume

## Workload reviewed
- task name
- task description
- why a model is being used today
- whether deterministic replacement was considered first

## Current model usage
- current workload class
- current model tier
- current prompt or workflow pattern
- current latency, cost, or privacy concerns

## Findings
- issue or opportunity
- current class
- target class
- why the current model appears over-sized, under-sized, or justified

## Dimension scores
- reasoning intensity
- output structure strictness
- hallucination tolerance
- latency sensitivity
- privacy and data control constraints
- volume and repetition
- variation tolerance
- failure cost
- confidence

## Candidate target architectures
- hosted small model option
- local model option
- hybrid option
- justification for keeping frontier calls if applicable

## Recommended changes
- final recommendation label
- recommended target architecture
- why
- prerequisites

## Test plan for substitution
- baseline model
- candidate replacement
- evaluation set
- pass-fail criteria
- cost comparison method
- latency comparison method
- rollback condition

## Risks and caveats
- where the recommendation may fail
- what would invalidate the downshift
- what still needs human review

## Verification steps
- exact checks to confirm the recommendation worked
- explicit before and after metrics to compare
