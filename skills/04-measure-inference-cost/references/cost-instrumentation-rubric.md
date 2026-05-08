# Cost instrumentation rubric

Use this rubric when assessing measurement quality and identifying optimization targets in skill 04.

## Measurement quality levels

| Level | Description | Action |
|-------|-------------|--------|
| Measured | Token counts pulled directly from API responses or logs | Use as-is |
| Sampled | Token counts estimated from a representative batch of real runs | Flag confidence, use for planning |
| Estimated | Token counts approximated from prompt length and expected output | Flag explicitly, prioritize closing the gap |
| Unknown | No token data available | Treat as instrumentation gap, do not optimize without closing it |

---

## Call classification by cost contribution

| Contribution | Label | Priority |
|-------------|-------|----------|
| >40% of per-run cost | High-priority optimization target | Immediate |
| 15–40% of per-run cost | Medium-priority optimization target | Near-term |
| <15% of per-run cost | Low-priority | Address after high and medium |
| Unknown | Instrumentation gap | Instrument before optimizing |

---

## Optimization routing

After ranking calls by cost contribution, route each high-priority call using this decision tree:

1. Determinism score 0–1 → Route to skill 01 (replace with code or rule)
2. Determinism score 2 → Route to skill 02 (can a smaller model handle this?)
3. Determinism score 3–4, cost unjustified → Route to skill 03 (re-audit the workflow step)
4. Determinism score 3–4, cost accepted → Document as justified cost, set review cadence

---

## Volume projection method

When calculating cost at volume, use this method:

- **Measured runs:** Use actual run count from logs
- **Estimated runs:** State the basis (user count × estimated frequency, event rate, etc.)
- **Growth projection:** Default to 2× current volume unless there is a specific forecast

Always label which figures are measured and which are estimated.

---

## Pricing data hygiene

- Record the date pricing was checked
- Note the source (provider pricing page URL where possible)
- Flag any models where pricing is usage-tiered and the tier boundary is relevant
- Re-check pricing before using a report for budget decisions if it is more than 60 days old
