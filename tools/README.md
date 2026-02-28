# Tools

Helper scripts for working with FMD files. These are optional utilities — FMD itself has no runtime dependency.

## excel_to_fmd.py

Converts an Excel workbook (`.xlsx`) to FMD. Each sheet becomes a separate `.md` file inside a folder named after the workbook.

**Requirements**

```bash
pip install openpyxl
```

**Usage**

```bash
python excel_to_fmd.py <path_to_workbook.xlsx>
```

**Output**

```
workbook_name/
├── Sheet1.md
├── Sheet2.md
└── ...
```

**Formula translation**

| Excel | FMD |
|-------|-----|
| `=B3*C3` (same-row) | `` `={Column B}*{Column C}` `` |
| `=SUM(B2:B10)` (single column) | `` `=SUM(Column B)` `` |
| Cross-row, cross-sheet, or unsupported | Replaced with last computed value |

Cell comments are collected at the bottom of each file under a `## Comments` section.

---

## Planned

- `fmd_eval.py` — Reference evaluator: reads an FMD file and outputs a version with all formulas replaced by computed values.
- MCP server — Expose FMD evaluation as a [Model Context Protocol](https://modelcontextprotocol.io/) tool so any MCP-compatible agent can evaluate FMD documents natively.
