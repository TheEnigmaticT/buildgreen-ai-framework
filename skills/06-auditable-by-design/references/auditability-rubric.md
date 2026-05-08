# Auditability rubric

Use this rubric when scoring consequential outputs in skill 06.

## Auditability dimensions

Score each dimension for each consequential output as: full / partial / none.

| Dimension | Full | Partial | None |
|-----------|------|---------|------|
| **Reproducibility** | Identical inputs always produce identical outputs | Outputs are stable under most conditions but not guaranteed | Outputs vary; cannot be reproduced |
| **Traceability** | Every output is linked to its exact inputs, model version, and process version | Inputs are logged but model version or process is not pinned | No input or process logging |
| **Explainability** | The reason for the output can be stated in plain language from the process rules | A post-hoc explanation can be constructed but is not inherent to the process | Output cannot be explained from first principles |
| **Logging** | All inputs, outputs, and process metadata are logged and retained per the retention requirement | Partial logging; some fields or steps are missing | No logging |

---

## Root cause labels

Use these labels when identifying gap root causes:

- `Stochastic call` — a raw LLM call where output varies by design
- `Unpinned model version` — model version is not fixed; provider may update silently
- `Missing input log` — inputs to a step are not recorded
- `Missing output log` — outputs from a step are not recorded
- `Undocumented step` — a process step exists but is not described anywhere
- `Unretained log` — logs exist but are not retained for the required period
- `Temperature not fixed` — LLM call has non-zero temperature; outputs vary

---

## Remediation routing

| Root cause | Primary remediation | Route to |
|-----------|--------------------|---------:|
| Stochastic call | Replace with deterministic code | Skill 01 |
| Stochastic call (inference still needed) | Pin model version, fix temperature, log I/O | This skill |
| Unpinned model version | Pin model version in API call | This skill |
| Missing input/output log | Add structured logging to the step | This skill |
| Undocumented step | Document the step and add it to the process record | This skill |
| Unretained log | Extend log retention to meet the requirement | This skill |

---

## Auditability classification

| Classification | Description | Acceptable for regulated context? |
|---------------|-------------|----------------------------------|
| Fully auditable | Deterministic, logged, traceable, explainable | Yes |
| Auditable with controls | Inference used, but version pinned, I/O logged, process documented | Depends on jurisdiction and risk level |
| Partially auditable | Some gaps in logging, traceability, or reproducibility | Generally no |
| Not auditable | Raw LLM call, no pinning, no logging | No |

---

## Common retention requirements by industry

_Note: Always verify with legal counsel. These are general reference points, not legal advice._

| Industry | Common retention period |
|----------|------------------------|
| Financial services | 5–7 years (varies by record type) |
| Healthcare | 6–10 years (varies by record type and jurisdiction) |
| Legal | Matter-specific; often 7+ years |
| Government | Varies widely; often defined by specific regulation |

---

## Model version pinning reference

Most major providers support version-pinned model calls. Always use a versioned model identifier (e.g., `claude-3-5-sonnet-20241022` rather than `claude-3-5-sonnet-latest`) in any workflow where reproducibility is required. Log the model identifier alongside the input and output for every call.
