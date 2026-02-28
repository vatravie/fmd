# Contributing to FMD

Thank you for your interest. FMD is a small, focused project and contributions of all sizes are welcome.

---

## What we're looking for

### High value
- **Spec feedback** — ambiguities, edge cases, or missing rules in `SPEC.md`
- **New examples** — real-world FMD documents (project estimates, budgets, logs)
- **Tool implementations** — converters or evaluators in other languages
- **Bug reports** — issues with the Excel converter or spec inconsistencies

### Out of scope (for now)
- GUI tooling
- A new file extension (`.fmd`) — the project intentionally uses `.md`
- Features that require a custom runtime (FMD is designed to be evaluatable by any LLM)

---

## How to contribute

1. **Open an issue first** for non-trivial changes so we can discuss the direction.
2. Fork the repo and create a branch: `git checkout -b my-change`
3. Make your changes. Keep commits focused and descriptive.
4. Open a pull request against `main`. Fill in the PR template.

---

## Spec changes

Changes to `SPEC.md` carry the most weight. Please:

- Explain the motivation — what real problem does this solve?
- Show a before/after example in FMD syntax.
- Consider backward compatibility with existing FMD documents.

---

## Style

- **Markdown**: Use ATX headings (`##`), fenced code blocks with language tags.
- **Python**: Follow PEP 8. No dependencies outside the standard library except `openpyxl` for the Excel tool.
- **Keep it simple**: FMD's main advantage is that it needs no special runtime. Contributions that add complexity without clear benefit will be declined with explanation.

---

## Code of conduct

Be respectful and constructive. This project follows the [Contributor Covenant](https://www.contributor-covenant.org/version/2/1/code_of_conduct/).
