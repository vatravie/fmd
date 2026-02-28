---
fmd: 0.1
---

# Risk Log — Q1 2025

---

## Assumptions

<!-- fmd:vars -->
| var                  | value |
|----------------------|-------|
| review_period_days   | 90    |
| high_risk_threshold  | 4     |

---

## Risk Register

<!-- fmd:table -->
| Risk                | Frequency (per year) | Impact (1–10) | Score                                    | Priority         | Owner   |
|---------------------|----------------------|---------------|------------------------------------------|------------------|---------|
| Data breach         | 0.5                  | 9             | `={Frequency (per year)}*{Impact (1–10)}`| `=RANK(Score)`   | Alice   |
| Key person leaves   | 2                    | 6             | `={Frequency (per year)}*{Impact (1–10)}`| `=RANK(Score)`   | Bob     |
| Supplier failure    | 0.3                  | 8             | `={Frequency (per year)}*{Impact (1–10)}`| `=RANK(Score)`   | Alice   |
| Regulatory change   | 1                    | 5             | `={Frequency (per year)}*{Impact (1–10)}`| `=RANK(Score)`   | Carol   |

---

## Summary

<!-- fmd:summary -->
| Metric                        | Value                                        |
|-------------------------------|----------------------------------------------|
| Total risks                   | `=COUNT(Risk)`                               |
| High risks (Score > threshold)| `=COUNTIF(Score, ">{high_risk_threshold}")`  |
| Highest risk item             | `=MAX_ROW(Score, Risk)`                      |
| Average score                 | `=AVG(Score)`                                |

---

## Comments

- **Supplier failure / Frequency (per year)** *(Alice)*: Frequency updated from 0.3 based on Q4 incident report.
- **Key person leaves / Impact (1–10)** *(Bob)*: Succession plan in progress — reassess next quarter.
