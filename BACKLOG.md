---
kanban-plugin: board
---

## Next

- [ ] **Principles: publish the six public principle docs** — Create `principles/01-default-to-determinism.md` through `principles/06-auditable-by-design.md` with plain-language explanations, why each principle matters, common failure modes, and links to the corresponding skills. [added::2026-05-09] [done-when::All six principle files exist and each one can stand alone for a human reader] [priority::high]

## In Progress

## In Review

## Backlog

Roadmap framing:
- **Public teaching layer:** make the repo understandable to first-time visitors, not just contributors.
- **Operational layer:** connect the public principles to executable skills, templates, and model guidance.
- **Proof layer:** add examples, audits, and case studies that show how greener AI decisions work in practice.

### Public teaching layer

- [ ] **Guide: start here workflow** — Add a `START-HERE.md` or equivalent guide that walks a reader through auditing one existing AI workflow in 15–30 minutes. [added::2026-05-09] [done-when::A first-time reader can complete one lightweight workflow assessment using only repo materials] [priority::high]
- [ ] **Guide: principle routing / decision tree** — Add a guide that helps readers decide which principle to apply first based on the shape of the workflow. [added::2026-05-09] [done-when::A reader can route a workflow to the right principle without reading every skill first] [priority::medium]
- [ ] **Docs: glossary of Build Green AI terms** — Add `GLOSSARY.md` defining determinism, bounded judgment, local model candidate, hosted small model candidate, frontier model justified, inference cost, and auditability. [added::2026-05-09] [done-when::Core repo terms are defined in one place and linked from the README] [priority::medium]
- [ ] **Docs: FAQ and objections** — Add `FAQ.md` covering common objections like quality tradeoffs, when frontier models are justified, when local is worth it, and how to measure cost without perfect telemetry. [added::2026-05-09] [done-when::The repo answers the most common reuse and adoption objections without requiring a separate conversation] [priority::medium]

### Operational layer

- [ ] **Models: publish current recommendations** — Create `models/current-recommendations.md` with opinionated guidance on when to use deterministic code, local models, hosted small models, and frontier models. [added::2026-05-09] [done-when::The repo includes a dated, practical model-selection document that supports the six principles] [priority::high]
- [ ] **Templates: shared workflow assessment worksheet** — Add a reusable public worksheet for evaluating one AI workflow across the six principles. [added::2026-05-09] [done-when::A contributor or workshop participant can fill out one standardized assessment from the repo alone] [priority::medium]
- [ ] **Contributing: evidence standards** — Expand the contribution docs to define what counts as a justified recommendation, how to cite evidence, and how to separate opinion from grounded claims. [added::2026-05-09] [done-when::Contribution guidance includes explicit evidence and citation expectations for new principles, skills, and examples] [priority::medium]
- [ ] **License: align skill frontmatter with repo license** — Update all six `SKILL.md` files so their `license:` metadata matches the repo’s CC-BY-4.0 license, or document an intentional split-license strategy. [added::2026-05-09] [done-when::No public file metadata contradicts the repo’s declared license] [priority::high]

### Proof layer

- [ ] **Examples: add practical case studies** — Add 3–5 case studies showing how common AI workflows become greener through determinism, smaller models, local execution, or better instrumentation. [added::2026-05-09] [done-when::The repo includes multiple concrete before/after examples across different workflow types] [priority::high]
- [ ] **Examples: publish sample audits and reports** — Add completed examples using the shared templates so readers can see what a finished assessment looks like. [added::2026-05-09] [done-when::At least one completed example exists for a principle skill and one cross-principle workflow assessment] [priority::medium]

## Done

- [x] **README: establish the public entry point** — Created a root `README.md` that explains the purpose of Build Green AI, who it is for, the six principles, how to use the repo, and where to start. [added::2026-05-09] [done::2026-05-09]

## Cancelled

%% kanban:settings
```
{"kanban-plugin":"board","list-collapse":[null]}
```
%%
