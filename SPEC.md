# FMD Specification

**Version:** 0.1  
**Status:** Draft

---

## Overview

FMD (Formula Markdown) is a convention layered on top of standard [CommonMark](https://commonmark.org/) Markdown. It adds two things:

1. **Directives** — HTML comments that mark evaluation zones.
2. **Formula cells** — backtick-wrapped expressions inside table cells.

An FMD document is valid Markdown. Formulas render as inline code when not evaluated. When an agent or evaluator processes the document, it resolves formulas and replaces them with computed values.

---

## Directives

Directives are standard HTML comments and are invisible in rendered Markdown.

### `<!-- fmd:vars -->`

Marks the next table as a variable definition block.

- The table must have exactly two columns.
- The first column is the variable name; the second is its value.
- Variable names must be valid identifiers (`[A-Za-z_][A-Za-z0-9_]*`).
- Variables are available in all `fmd:table` blocks that follow within the same file.

```markdown
<!-- fmd:vars -->
| var        | value |
|------------|-------|
| tax_rate   | 0.08  |
| discount   | 0.10  |
```

### `<!-- fmd:table -->`

Marks the next table as an evaluatable data table.

- The first row is the header row. Column names are used as formula references.
- Subsequent rows are data rows. Each cell may contain a formula or a literal value.

```markdown
<!-- fmd:table -->
| Item     | Qty | Unit Price | Subtotal              |
|----------|-----|------------|-----------------------|
| Widget A | 3   | 25.00      | `={Qty}*{Unit Price}` |
```

### `<!-- fmd:summary -->`

Marks the next table as a summary block. Identical to `fmd:table` in evaluation rules. Semantic distinction only — a summary aggregates across a preceding table.

---

## Formula syntax

A formula cell contains a backtick-wrapped expression starting with `=`:

```
`={expression}`
```

The expression is a standard arithmetic expression with the extensions below.

### Column references

Reference a value from the **same row** using the column header name wrapped in `{}`:

```
`={Qty}*{Unit Price}`
```

Column names are matched exactly (case-sensitive). Spaces are allowed inside `{}`.

### Variable references

Reference a variable defined in an `fmd:vars` block:

```
`={Subtotal}*{tax_rate}`
```

Variable names and column names share the same namespace. **Column names take precedence** when there is a collision.

### Aggregate functions

Aggregate functions operate on an entire column of the nearest preceding `fmd:table`:

| Function | Meaning |
|----------|---------|
| `SUM(Column)` | Sum of all values in the column |
| `AVG(Column)` | Arithmetic mean |
| `MIN(Column)` | Minimum value |
| `MAX(Column)` | Maximum value |
| `COUNT(Column)` | Count of non-empty cells |
| `COUNTIF(Column, ">N")` | Count of cells matching condition |
| `MAX_ROW(ScoreCol, LabelCol)` | Value of `LabelCol` in the row where `ScoreCol` is maximum |
| `RANK(Column)` | Rank of this row's value within the column (1 = highest) |

```markdown
<!-- fmd:summary -->
| Metric      | Value               |
|-------------|---------------------|
| Grand Total | `=SUM(Subtotal)`    |
| Top item    | `=MAX_ROW(Subtotal, Item)` |
```

### Supported operators

`+` `-` `*` `/` `(` `)` and numeric literals. No string operations in v0.1.

---

## Evaluation rules

1. Build the variable namespace from all `fmd:vars` blocks in document order.
2. For each `fmd:table` or `fmd:summary` block, process rows top to bottom.
3. Within a row, resolve column references left to right. Cells that are not formulas are treated as their literal value (string or number).
4. For `RANK` and aggregate functions, all non-formula cells in the column are evaluated first; formula cells are evaluated in row order.
5. Circular references must be detected and reported as an error.
6. Division by zero produces the value `#DIV/0`.

---

## Handling non-evaluatable references

When an FMD document is produced from another source (e.g. converted from Excel), references that cannot be expressed in FMD syntax — cross-row references, cross-file references, unsupported functions — **must be replaced with their last known computed value** rather than kept as opaque formula strings. This ensures the document always contains meaningful data when read without evaluation.

---

## File conventions

- FMD files use the `.md` extension. No special extension is required.
- A file may contain multiple `fmd:vars`, `fmd:table`, and `fmd:summary` blocks.
- Non-directive Markdown (headings, paragraphs, lists) is ignored by evaluators and renders normally.

---

## Versioning

The spec version is declared in the document front matter (optional):

```markdown
---
fmd: 0.1
---
```

If omitted, evaluators should assume the latest stable version.

---

## Example

See [`examples/risk_log.md`](examples/risk_log.md) for a complete annotated example.
