# Inference cost report

Use this template for all reports produced by skill 04 (measure inference cost).

---

## 1. Workflow summary

- **Workflow name:**
- **Run frequency:**
- **Total monthly volume (measured or estimated):**
- **Pricing data date:**

---

## 2. All inference calls

| # | Model | Provider | Purpose | Runs per execution | Input tokens | Output tokens | Cost per call | % of run cost | Det. score |
|---|-------|----------|---------|-------------------|-------------|--------------|--------------|--------------|-----------|
| 1 | | | | | | | | | |
| 2 | | | | | | | | | |
| 3 | | | | | | | | | |

_Measurement quality for each call: Measured / Sampled / Estimated / Unknown_

---

## 3. Cost per workflow run

| Scenario | Cost |
|----------|------|
| Minimum (required calls only) | |
| Expected (weighted by conditional frequency) | |
| Maximum (all calls including conditional) | |

---

## 4. Cost at volume

| Period | Cost | Basis |
|--------|------|-------|
| Daily | | Measured / Estimated |
| Monthly | | Measured / Estimated |
| Annual (current volume) | | Measured / Estimated |
| Annual (2× projected growth) | | Estimated |

---

## 5. Cost ranking by call

_Sorted highest to lowest by percentage of per-run cost._

| Rank | Call # | Model | Cost per call | % of run cost | Priority label |
|------|--------|-------|--------------|--------------|----------------|
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |

---

## 6. High-priority optimization targets

_Calls contributing >40% of per-run cost, or medium-priority calls with a determinism score of 0–2._

- **Call N:**
  - Model:
  - Cost per call:
  - % of run cost:
  - Determinism score:
  - Recommendation label:
  - Routing: Skill 01 / Skill 02 / Skill 03

---

## 7. Instrumentation gaps

_Calls where cost could not be directly measured._

- **Call N:** 
  - Why unavailable:
  - Recommended instrumentation:

---

## 8. Recommended next actions

_Ordered by priority._

1. 
2. 
3. 

---

## Recommended next action

_One sentence. The single highest-leverage next move._
