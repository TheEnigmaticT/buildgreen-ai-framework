# Workflow audit report

Use this template for all reports produced by skill 03 (audit before automate).

---

## 1. Workflow goal

_One sentence. What does this workflow produce, and for whom?_

---

## 2. Current workflow map

| Step | Trigger | Performed by | Input | Output | Notes |
|------|---------|--------------|-------|--------|-------|
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |

_Add rows as needed. "Performed by" should be one of: human / rule / script / model._

---

## 3. Determinism scores

| Step | Score | Justification |
|------|-------|---------------|
| 1 | | |
| 2 | | |
| 3 | | |

---

## 4. Waste and redundancy found

_List each finding. Name the step(s) involved and describe why the step is wasteful or redundant._

- **Finding:** 
  - Steps involved:
  - Description:

---

## 5. Steps that require genuine inference

_List only the steps that still require model inference after the waste review. Justify each._

- **Step N:**
  - Why inference is still needed:
  - Determinism score:
  - Recommended model tier (or route to skill 02):

---

## 6. Recommended redesigned workflow

| Step | Current form | Target form | Recommendation label | Justification |
|------|-------------|-------------|---------------------|---------------|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |

_Recommendation labels: Replace with code / Replace with workflow rule / Downshift model tier / Move local / Keep current approach, but justify it / Remove entirely_

---

## 7. Estimated impact

_Fill in what you can. Mark unknowns explicitly._

- Steps removed or replaced with code: 
- Estimated token reduction:
- Estimated latency improvement:
- Estimated cost reduction:
- Confidence in estimates: low / medium / high

---

## 8. Open audit gaps

_List anything that was unavailable or unclear during the audit. Use standard gap labels from the rubric where applicable._

- Gap:
- Gap:

---

## Recommended next action

_One sentence. The single clearest next move._
