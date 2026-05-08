# Local feasibility rubric

Use this rubric when scoring a workload's suitability for local inference under skill 05.

## Primary feasibility dimensions

Score each dimension as: strong fit / marginal fit / not viable

| Dimension | Strong fit | Marginal fit | Not viable |
|-----------|-----------|--------------|------------|
| **Privacy / compliance** | Hard requirement that cloud violates | Preference but not mandatory | No requirement; cloud is acceptable |
| **Volume** | Break-even <12 months | Break-even 12–24 months | Break-even >24 months or volume too low |
| **Task complexity** | Bounded, structured, fits small model | Moderate reasoning, may need mid-size local model | Requires frontier-level capability |
| **Hardware availability** | Appropriate hardware in place | Hardware can be provisioned | No viable path to provision hardware |
| **Latency** | Local latency meets or beats API | Local latency is acceptable | Local latency fails the requirement |
| **Operational capacity** | Team can maintain local inference | Team can learn with effort | No capacity to maintain local infrastructure |

A strong local-first recommendation requires at least four strong fits and no not-viable scores.
A marginal recommendation requires no not-viable scores and at least two strong fits.
Any not-viable score requires explicit justification to proceed.

---

## Apple Silicon reference (current as of 2025)

| Hardware | Unified memory | Notes |
|----------|---------------|-------|
| M3 / M4 base | 16–32 GB | Suitable for 7B–13B parameter models |
| M3 / M4 Pro | 36–48 GB | Suitable for 13B–34B parameter models |
| M3 / M4 Max | 64–128 GB | Suitable for 34B–70B parameter models |
| M2 / M3 Ultra | 192 GB+ | Suitable for very large models |

_Model memory requirements vary by quantization. 4-bit quantized models run in approximately 50–60% of the full-precision memory footprint._

_Update this table when new hardware releases._

---

## Break-even calculation method

```
Monthly API spend replaced = (cost per run × monthly run volume)
Infrastructure cost = hardware purchase price + annual maintenance estimate
Break-even (months) = infrastructure cost ÷ monthly API spend replaced
```

Always calculate break-even at current volume and at 2× projected volume.
Flag the assumptions behind the run volume estimate.

---

## Candidate local model categories

Use these categories when listing candidates. Do not recommend specific models without checking current benchmark availability — the local model landscape changes quickly.

| Category | Parameter range | Typical use |
|----------|----------------|-------------|
| Very small | 1B–3B | Classification, simple extraction, routing |
| Small | 7B | Structured generation, constrained summarization |
| Medium | 13B–20B | Moderate reasoning, longer context tasks |
| Large | 34B–70B | Complex reasoning, nuanced generation |

_Always verify current model availability and benchmark data before recommending a specific model._
