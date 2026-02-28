---
fmd: 0.1
---

# Risk Log — Q1 2025

This is a complete FMD example. It shows every feature of the format.
Non-directive Markdown (like this paragraph) is ignored by evaluators.

---

## Assumptions

<!-- fmd:vars -->
| var                  | value |
|----------------------|-------|
| review_period_days   | 90    |
| high_risk_threshold  | 4     |

Variables defined here are available in all tables below.
`{review_period_days}` = 90, `{high_risk_threshold}` = 4.

---

## Risk Register

<!-- fmd:table -->
| Risk                | Frequency (per year) | Impact (1–10) | Score                                    | Priority         | Owner   |
|---------------------|----------------------|---------------|------------------------------------------|------------------|---------|
| Data breach         | 0.5                  | 9             | `={Frequency (per year)}*{Impact (1–10)}`| `=RANK(Score)`   | Alice   |
| Key person leaves   | 2                    | 6             | `={Frequency (per year)}*{Impact (1–10)}`| `=RANK(Score)`   | Bob     |
| Supplier failure    | 0.3                  | 8             | `={Frequency (per year)}*{Impact (1–10)}`| `=RANK(Score)`   | Alice   |
| Regulatory change   | 1                    | 5             | `={Frequency (per year)}*{Impact (1–10)}`| `=RANK(Score)`   | Carol   |

**How to read this table:**
- `Score` is computed per row: `{Frequency (per year)} * {Impact (1–10)}`
- `Priority` ranks rows by Score (1 = highest risk)
- Column names with spaces are referenced using `{}` — e.g. `{Frequency (per year)}`

---

## Summary

<!-- fmd:summary -->
| Metric                        | Value                                        |
|-------------------------------|----------------------------------------------|
| Total risks                   | `=COUNT(Risk)`                               |
| High risks (Score > threshold)| `=COUNTIF(Score, ">{high_risk_threshold}")`  |
| Highest risk item             | `=MAX_ROW(Score, Risk)`                      |
| Average score                 | `=AVG(Score)`                                |

**Notes:**
- `{high_risk_threshold}` is resolved from the vars block above (value: 4)
- `MAX_ROW(Score, Risk)` returns the value of the `Risk` column in the row with the highest `Score`
- Aggregate functions operate on the nearest preceding `fmd:table`

---

## Comments

> This section is optional. It is plain Markdown, not an FMD block.
> Tools that convert from Excel will auto-populate this section with cell comments.

- **C3** *(Alice)*: Frequency updated from 0.3 based on Q4 incident report.
- **B4** *(Bob)*: Succession plan in progress — reassess next quarter.
