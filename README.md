# FMD — Formula Markdown

**A plain-text format for documents that contain live calculations.**

FMD extends standard Markdown tables with a lightweight formula syntax. It renders as readable Markdown everywhere, and any LLM or agent can evaluate it without special tooling.

```markdown
<!-- fmd:vars -->
| var        | value |
|------------|-------|
| tax_rate   | 0.08  |

<!-- fmd:table -->
| Item     | Qty | Unit Price | Subtotal              | Tax                       |
|----------|-----|------------|-----------------------|---------------------------|
| Widget A | 3   | 25.00      | `={Qty}*{Unit Price}` | `={Subtotal}*{tax_rate}`  |
| Widget B | 5   | 40.00      | `={Qty}*{Unit Price}` | `={Subtotal}*{tax_rate}`  |
```

---

## Why FMD?

| | Excel / CSV | FMD |
|---|---|---|
| Fits in LLM context | ✗ (binary / large) | ✓ |
| Human-readable | ✗ | ✓ |
| Git-diffable | ✗ | ✓ |
| Lives inside docs | ✗ | ✓ |
| Agent can reason about it | ✗ | ✓ |
| Recalculates on change | ✓ | ✓ (via agent) |

FMD is not a spreadsheet replacement. It is for documents *that contain* calculations — reports, risk logs, estimates, proposals — where you want the numbers to be live and auditable, not hardcoded.

---

## Format at a glance

See [`SPEC.md`](SPEC.md) for the full specification and [`examples/`](examples/) for ready-to-use templates.

---

## Tools

| Tool | Description |
|------|-------------|
| [`tools/excel_to_fmd.py`](tools/excel_to_fmd.py) | Convert an Excel workbook to FMD (one `.md` file per sheet) |
| MCP server | *(planned)* Expose excel_to_fmd as a Model Context Protocol tool |

### Excel → FMD

```bash
pip install openpyxl
python tools/excel_to_fmd.py my_workbook.xlsx
# → my_workbook/Sheet1.md, my_workbook/Sheet2.md …
```

---

## Project structure

```
fmd/
├── SPEC.md                  # The format specification
├── examples/
│   └── risk_log.md          # Annotated example for LLMs and humans
├── tools/
│   └── excel_to_fmd.py      # Excel → FMD converter
├── CONTRIBUTING.md
└── LICENSE                  # MIT
```

---

## Status

FMD is in early design. The format spec and example are stable. Tools are in active development.

- [x] Format specification
- [x] Annotated example
- [x] Excel → FMD converter
- [ ] MCP server

---

## Contributing

Contributions are welcome — especially to the spec, new examples, and tool implementations in other languages. See [`CONTRIBUTING.md`](CONTRIBUTING.md).

---

## License

MIT — see [`LICENSE`](LICENSE).
