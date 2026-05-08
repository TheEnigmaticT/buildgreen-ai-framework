# Build Green AI skill system implementation plan

> **For Hermes:** Use `subagent-driven-development` to implement this plan task-by-task. Steps use checkbox syntax for tracking.

**Goal:** Build the first usable Build Green AI skill library, including shared taxonomy, contribution rules, and one coaching skill for each of the six principles.

**Architecture:** Treat the repo as two layers: a public framework layer (`principles/`, `models/`, `contributing/`) and an executable skills layer (`skills/`). Put shared rubrics and templates in one place, then build each principle skill on top of those shared materials so scoring language, output formats, and decision rules stay consistent.

**Tech Stack:** Markdown, static repo docs, SKILL.md-style authoring conventions, git.

---

## Planned repo structure

```text
buildgreen-ai/
├── index.html
├── patterns.md
├── docs/
│   └── plans/
│       └── 2026-05-07-build-green-ai-skill-system.md
├── principles/
│   ├── README.md
│   ├── 01-default-to-determinism.md
│   ├── 02-minimum-sufficient-model.md
│   ├── 03-audit-before-automate.md
│   ├── 04-measure-inference-cost.md
│   ├── 05-local-first-where-possible.md
│   └── 06-auditable-by-design.md
├── skills/
│   ├── README.md
│   ├── _shared/
│   │   ├── taxonomy.md
│   │   ├── output-formats.md
│   │   └── verification-checklists.md
│   ├── 01-default-to-determinism/
│   │   ├── SKILL.md
│   │   ├── references/log-audit-rubric.md
│   │   └── templates/determinism-audit-report.md
│   ├── 02-minimum-sufficient-model/
│   │   ├── SKILL.md
│   │   ├── references/model-selection-rubric.md
│   │   └── templates/model-right-sizing-report.md
│   ├── 03-audit-before-automate/
│   │   ├── SKILL.md
│   │   ├── references/workflow-audit-checklist.md
│   │   └── templates/workflow-audit-report.md
│   ├── 04-measure-inference-cost/
│   │   ├── SKILL.md
│   │   ├── references/cost-instrumentation-checklist.md
│   │   └── templates/cost-baseline-report.md
│   ├── 05-local-first-where-possible/
│   │   ├── SKILL.md
│   │   ├── references/local-first-decision-tree.md
│   │   └── templates/local-first-feasibility-report.md
│   └── 06-auditable-by-design/
│       ├── SKILL.md
│       ├── references/auditability-rubric.md
│       └── templates/auditability-review-report.md
├── models/
│   ├── README.md
│   └── current-recommendations.md
└── contributing/
    ├── README.md
    └── writing-build-green-ai-skills.md
```

## Shared design rules for every Build Green AI skill

1. Each skill must be runnable by an agent or readable by a human without hidden context.
2. Each skill must define: trigger, inputs, workflow, scoring language, output format, and verification.
3. Each skill must produce a structured report, not just advice.
4. Each skill must distinguish deterministic software, local model work, and frontier-model work.
5. Each skill must end with a recommended next action, not a vague summary.
6. No placeholders, no “analyze this” hand-waving, no undefined scoring labels.

## Shared taxonomies to define once and reuse everywhere

### Workload classification
- Deterministic
- Local model candidate
- Hosted small model candidate
- Frontier model justified
- Do not automate yet

### Determinism score
- 0 = already deterministic, should be code
- 1 = mostly rules with a small amount of classification
- 2 = bounded judgment with stable inputs and outputs
- 3 = open-ended judgment, but still constrainable
- 4 = frontier-level reasoning genuinely required

### Recommendation types
- Replace with code
- Replace with workflow rule
- Downshift model tier
- Move local
- Add instrumentation first
- Keep current approach, but justify it

### Standard output sections
- Context reviewed
- Findings
- Scores
- Recommended changes
- Risks and caveats
- Verification steps

## Delivery order

1. Shared taxonomy and contribution rules
2. Principle 1 skill: default to determinism
3. Principle 2 skill: minimum sufficient model
4. Principle 3 skill: audit before automate
5. Principle 4 skill: measure inference cost
6. Principle 5 skill: local-first where possible
7. Principle 6 skill: auditable by design
8. Public model guidance doc
9. Public principles docs cleanup

---

### Task 1: Create repo scaffolding for principles, skills, models, and contribution docs

**Objective:** Establish the directory structure so the repo can hold executable skills and public framework docs without mixing concerns.

**Files:**
- Create: `principles/README.md`
- Create: `skills/README.md`
- Create: `skills/_shared/taxonomy.md`
- Create: `skills/_shared/output-formats.md`
- Create: `skills/_shared/verification-checklists.md`
- Create: `models/README.md`
- Create: `contributing/README.md`
- Create: `contributing/writing-build-green-ai-skills.md`

- [ ] **Step 1: Create the directory tree**

Run:
```bash
mkdir -p principles skills/_shared models contributing \
  skills/01-default-to-determinism/references skills/01-default-to-determinism/templates \
  skills/02-minimum-sufficient-model/references skills/02-minimum-sufficient-model/templates \
  skills/03-audit-before-automate/references skills/03-audit-before-automate/templates \
  skills/04-measure-inference-cost/references skills/04-measure-inference-cost/templates \
  skills/05-local-first-where-possible/references skills/05-local-first-where-possible/templates \
  skills/06-auditable-by-design/references skills/06-auditable-by-design/templates
```
Expected: directories created with no errors.

- [ ] **Step 2: Create `skills/README.md`**

Write this content:
```md
# Build Green AI skills

This directory contains executable coaching skills for applying the six Green AI principles.

Each skill must:
- declare when to use it
- require explicit inputs
- use shared scoring language from `skills/_shared/taxonomy.md`
- produce a structured report
- include a verification checklist

Shared references live in `skills/_shared/`.
Principle-specific references and templates live under each numbered skill directory.
```

- [ ] **Step 3: Create `principles/README.md`**

Write this content:
```md
# Build Green AI principles

This directory contains the public principle documents.

The principle documents explain the ideas.
The `skills/` directory shows how to apply those ideas in repeatable workflows.
```

- [ ] **Step 4: Create `models/README.md` and `contributing/README.md`**

Write this content to `models/README.md`:
```md
# Model guidance

This directory holds current model recommendations, selection notes, and update rules.

These recommendations should stay practical, cost-aware, and easy to revise as the market changes.
```

Write this content to `contributing/README.md`:
```md
# Contributing to Build Green AI

Contributors can improve the principles, skills, templates, rubrics, and model guidance.

Start by reading `contributing/writing-build-green-ai-skills.md` before editing any skill.
```

- [ ] **Step 5: Commit scaffolding**

Run:
```bash
git add principles skills models contributing
git commit -m "chore: scaffold build green ai skills library"
```
Expected: one commit containing only directory scaffolding and README files.

### Task 2: Define the shared taxonomy, report format, and verification standards

**Objective:** Create the common language every principle skill will reuse.

**Files:**
- Modify: `skills/_shared/taxonomy.md`
- Modify: `skills/_shared/output-formats.md`
- Modify: `skills/_shared/verification-checklists.md`

- [ ] **Step 1: Write `skills/_shared/taxonomy.md`**

Include these sections and exact labels:
```md
# Shared Green AI taxonomy

## Workload classes
- Deterministic
- Local model candidate
- Hosted small model candidate
- Frontier model justified
- Do not automate yet

## Determinism score
- 0 — already deterministic, should be code
- 1 — mostly rules with a small amount of classification
- 2 — bounded judgment with stable inputs and outputs
- 3 — open-ended judgment, but still constrainable
- 4 — frontier-level reasoning genuinely required

## Recommendation labels
- Replace with code
- Replace with workflow rule
- Downshift model tier
- Move local
- Add instrumentation first
- Keep current approach, but justify it
```

- [ ] **Step 2: Write `skills/_shared/output-formats.md`**

Include this report template:
```md
# Standard skill output format

## Context reviewed
- materials reviewed
- system or workflow boundaries

## Findings
- issue or opportunity
- current class
- target class

## Scores
- determinism score
- confidence
- expected cost impact
- expected reliability impact

## Recommended changes
- action
- why
- prerequisites

## Risks and caveats
- where the recommendation may fail

## Verification steps
- exact checks to confirm the recommendation worked
```

- [ ] **Step 3: Write `skills/_shared/verification-checklists.md`**

Include this checklist:
```md
# Shared verification checklist

Every Build Green AI skill should verify:
- the reviewed workload was described concretely
- every recommendation maps to a named workload class
- any proposed model change has a reason
- deterministic replacement advice specifies what becomes code or rules
- the output includes at least one measurable follow-up check
```

- [ ] **Step 4: Commit shared standards**

Run:
```bash
git add skills/_shared
git commit -m "docs: define shared green ai skill taxonomy"
```
Expected: one commit containing the reusable shared standards.

### Task 3: Write the contribution guide for Build Green AI skills

**Objective:** Document how future contributors should author skills so the repo stays consistent.

**Files:**
- Modify: `contributing/writing-build-green-ai-skills.md`

- [ ] **Step 1: Write the authoring guide header and scope**

Start the file with:
```md
# Writing Build Green AI skills

Build Green AI skills are executable coaching documents.
They are not essays, slogans, or principle summaries.

Every skill must tell an agent or operator:
- when to use the skill
- what inputs to gather
- how to evaluate the workload
- how to classify the result
- what output to produce
- how to verify the recommendation
```

- [ ] **Step 2: Add the required skill shape**

Include this required structure:
```md
## Required skill structure
1. Overview
2. When to use
3. Required inputs
4. Workflow
5. Classification rules
6. Output format
7. Common pitfalls
8. Verification checklist
```

- [ ] **Step 3: Add the prohibited patterns list**

Include this list:
```md
## Do not write skills like this
- vague prompts such as "analyze the workflow"
- unsupported claims about cost savings
- undefined labels like "probably use a smaller model"
- principle-only writing with no workflow
- output formats that depend on hidden judgment
```

- [ ] **Step 4: Add the review checklist**

Include this checklist:
```md
## Review checklist
- Does the skill use shared taxonomy labels exactly?
- Could a fresh agent run it without outside context?
- Does it produce a structured report?
- Does it end with measurable verification?
- Does it avoid vague language?
```

- [ ] **Step 5: Commit the contribution guide**

Run:
```bash
git add contributing/writing-build-green-ai-skills.md
git commit -m "docs: add build green ai skill authoring guide"
```
Expected: one commit with the contribution rules only.

### Task 4: Build principle skill 01, default to determinism

**Objective:** Create the foundational skill for finding work that should not be an LLM call.

**Files:**
- Create: `skills/01-default-to-determinism/SKILL.md`
- Create: `skills/01-default-to-determinism/references/log-audit-rubric.md`
- Create: `skills/01-default-to-determinism/templates/determinism-audit-report.md`

- [ ] **Step 1: Write `references/log-audit-rubric.md`**

Include these audit questions:
```md
# Determinism audit rubric

Ask for each repeated step:
1. Is the input structure stable?
2. Is the desired output structure stable?
3. Can rules or parsing handle this reliably?
4. Is the current model call mostly formatting, routing, extraction, or lookup?
5. What breaks if the output varies?
6. What would a deterministic replacement look like?
```

- [ ] **Step 2: Write `templates/determinism-audit-report.md`**

Use this format:
```md
# Determinism audit report

## Workflow reviewed
## Repeated tasks found
## Determinism scores
## Replace with code now
## Keep model, but constrain it
## Verify after changes
```

- [ ] **Step 3: Write `SKILL.md`**

The skill must include:
- trigger: use when reviewing logs, workflows, or repetitive LLM calls
- required inputs: workflow samples, logs, prompt-output pairs, failure examples
- workflow: inventory repeated tasks, score determinism, classify workload, recommend replacement path
- output: structured determinism audit report
- verification: compare cost, latency, and variation before vs after

- [ ] **Step 4: Commit skill 01**

Run:
```bash
git add skills/01-default-to-determinism
git commit -m "feat: add default to determinism skill"
```
Expected: one complete foundational skill with rubric and template.

### Task 5: Build principle skills 02 and 03

**Objective:** Add the next two high-leverage skills, model right-sizing and workflow audit.

**Files:**
- Create: `skills/02-minimum-sufficient-model/SKILL.md`
- Create: `skills/02-minimum-sufficient-model/references/model-selection-rubric.md`
- Create: `skills/02-minimum-sufficient-model/templates/model-right-sizing-report.md`
- Create: `skills/03-audit-before-automate/SKILL.md`
- Create: `skills/03-audit-before-automate/references/workflow-audit-checklist.md`
- Create: `skills/03-audit-before-automate/templates/workflow-audit-report.md`

- [ ] **Step 1: Build the model right-sizing reference and template**

The reference must score workloads by:
- latency tolerance
- accuracy tolerance
- output variability tolerance
- privacy constraints
- volume and frequency

The template must include:
- current model usage
- smaller-model candidates
- justification for keeping frontier calls
- test plan for substitution

- [ ] **Step 2: Build `skills/02-minimum-sufficient-model/SKILL.md`**

The skill must:
- identify where a smaller model is sufficient
- separate reasoning-heavy work from structured tasks
- recommend downshifts with justification
- require a comparison test plan

- [ ] **Step 3: Build the workflow audit reference and template for principle 03**

The checklist must inspect:
- repeated human steps
- hidden deterministic steps
- unnecessary prompt chaining
- approval points
- data dependencies

The template must include:
- current workflow map
- wasted steps
- automation candidates
- blocked areas that need more context first

- [ ] **Step 4: Build `skills/03-audit-before-automate/SKILL.md`**

The skill must:
- map a workflow before recommending automation
- classify each step by workload type
- identify where not to automate yet
- produce a workflow audit report

- [ ] **Step 5: Commit skills 02 and 03**

Run:
```bash
git add skills/02-minimum-sufficient-model skills/03-audit-before-automate
git commit -m "feat: add model right-sizing and workflow audit skills"
```
Expected: two complete skills with matching references and templates.

### Task 6: Build principle skills 04, 05, and 06

**Objective:** Finish the six-skill core library.

**Files:**
- Create: `skills/04-measure-inference-cost/SKILL.md`
- Create: `skills/04-measure-inference-cost/references/cost-instrumentation-checklist.md`
- Create: `skills/04-measure-inference-cost/templates/cost-baseline-report.md`
- Create: `skills/05-local-first-where-possible/SKILL.md`
- Create: `skills/05-local-first-where-possible/references/local-first-decision-tree.md`
- Create: `skills/05-local-first-where-possible/templates/local-first-feasibility-report.md`
- Create: `skills/06-auditable-by-design/SKILL.md`
- Create: `skills/06-auditable-by-design/references/auditability-rubric.md`
- Create: `skills/06-auditable-by-design/templates/auditability-review-report.md`

- [ ] **Step 1: Build the cost measurement skill set**

The reference must cover:
- per-call cost
- per-workflow cost
- baseline capture
- before/after comparison
- alert thresholds

The skill must require measurable baselines and explicit verification.

- [ ] **Step 2: Build the local-first skill set**

The decision tree must check:
- data sensitivity
- workload repetition
- latency needs
- hardware constraints
- model size fit

The skill must recommend local-first only when the workload and hardware actually fit.

- [ ] **Step 3: Build the auditable-by-design skill set**

The rubric must score:
- output traceability
- deterministic checkpoints
- record retention
- reproducibility
- human review boundaries

The skill must identify where stochastic behavior breaks auditability.

- [ ] **Step 4: Commit skills 04 through 06**

Run:
```bash
git add skills/04-measure-inference-cost skills/05-local-first-where-possible skills/06-auditable-by-design
git commit -m "feat: complete build green ai core skill set"
```
Expected: the full six-principle skills library exists in the repo.

### Task 7: Add public principle docs and current model guidance

**Objective:** Connect the public framework to the executable skills so the repo is useful to both readers and operators.

**Files:**
- Create: `principles/01-default-to-determinism.md`
- Create: `principles/02-minimum-sufficient-model.md`
- Create: `principles/03-audit-before-automate.md`
- Create: `principles/04-measure-inference-cost.md`
- Create: `principles/05-local-first-where-possible.md`
- Create: `principles/06-auditable-by-design.md`
- Create: `models/current-recommendations.md`

- [ ] **Step 1: Write the six public principle docs**

Each principle doc must include:
- short principle statement
- why it matters
- what it changes operationally
- link to the matching skill directory

- [ ] **Step 2: Write `models/current-recommendations.md`**

Use this structure:
```md
# Current model recommendations

## How to read this document
## Good default choices by workload type
## When frontier models are justified
## When local models make sense
## Update rules for revising this file
```

- [ ] **Step 3: Commit the public docs and model guidance**

Run:
```bash
git add principles models/current-recommendations.md
git commit -m "docs: connect public principles to executable skills"
```
Expected: the repo can now serve both as a public framework and a practical operating library.

## Self-review

- [ ] Every file path above is exact and consistent.
- [ ] Shared taxonomy is defined before any skill depends on it.
- [ ] Principle 1 is implemented before later skills reuse its logic.
- [ ] No task depends on placeholder content.
- [ ] Each skill produces a structured report and verification step.
- [ ] Public docs and executable skills remain separate but linked.

## Execution handoff

Plan complete and saved to `docs/plans/2026-05-07-build-green-ai-skill-system.md`.

Recommended execution approach: use `subagent-driven-development` and implement one task at a time, starting with shared scaffolding and taxonomy, then skill 01.