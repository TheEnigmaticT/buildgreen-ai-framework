# Determinism audit report

## Audit scope
- logs reviewed
- time period covered
- inaccessible sources

## Repeated tasks found
- short list of recurring user asks or workflow patterns

## Opportunities

### Opportunity N: [Task name]
- Evidence from logs:
- Current workflow:
- Target workflow:
- Workload class:
- Determinism score:
- Cron suitability score:
- Automation priority:
- Recommended path:
- What remains non-deterministic:
- Verification step:

## Cron job candidates
- tasks that should become scheduled jobs

## Deterministic code candidates
- tasks that should become scripts, rules, parsers, or fixed workflows

## Hybrid candidates
- cron + deterministic code + narrow residual LLM use

## Keep as LLM tasks
- tasks that still need open-ended judgment, strategy, or persuasion

## Recommended next builds
1. fastest high-leverage automation
2. second-best follow-up
3. anything blocked by missing data, access, or tooling
