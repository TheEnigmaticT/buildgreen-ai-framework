# Workflow map rubric

Use this rubric when scoring each step in a workflow audit under skill 03.

## Step classification

For each step, answer these questions in order:

**1. Can the output be produced by a function given stable inputs?**
If yes → determinism score 0 or 1. Recommend `Replace with code` or `Replace with workflow rule`.

**2. Is the output format constrained and the reasoning bounded?**
If yes → determinism score 2. Candidate for hosted small model or local model.

**3. Does the step require genuine synthesis, nuanced judgment, or reasoning across unstable inputs?**
If yes → determinism score 3 or 4. Evaluate with skill 02.

**4. Does the step exist only because the workflow was built incrementally?**
If yes → flag for removal regardless of score.

---

## Determinism score reference

| Score | Description | Default recommendation |
|-------|-------------|----------------------|
| 0 | Fully deterministic. Rules, parsing, routing, formatting, field assembly. | Replace with code |
| 1 | Mostly rules. Small classification or threshold decision. | Replace with code or workflow rule |
| 2 | Bounded judgment. Stable inputs and outputs. Some inference still useful. | Downshift model tier or move local |
| 3 | Open-ended judgment. Constrainable with effort. | Keep as model task, but test downshift |
| 4 | Frontier-level reasoning required. Complex synthesis, novel cases. | Keep current approach, but justify it |

---

## Step waste indicators

Flag a step for waste review if any of these are true:
- its output is reformatted or discarded by the next step
- the same information is produced by a different step earlier in the workflow
- it exists only to bridge a gap between two tools that could be integrated
- it was added as a workaround that was never removed
- no one downstream has noticed when it fails

---

## Audit gap categories

Use these standard labels when logging what was unavailable:

- `No volume data` — frequency and scale of the workflow unknown
- `No failure examples` — no documented cases of the workflow producing bad outputs
- `No cost data` — no token counts, time estimates, or dollar figures available
- `No step owner` — unclear who is responsible for a given step
- `Undocumented step` — step exists in practice but is not described in any SOP or documentation
