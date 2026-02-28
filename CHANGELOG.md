# Changelog

All notable changes to the FMD spec and tools are documented here.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).  
The spec uses [Semantic Versioning](https://semver.org/).

---

## [Unreleased]

## [0.1.0] — 2025

### Added
- Initial FMD specification (`SPEC.md`)
- Annotated example: `examples/risk_log.md`
- Excel → FMD converter: `tools/excel_to_fmd.py`
- Directives: `fmd:vars`, `fmd:table`, `fmd:summary`
- Formula syntax: column references `{Name}`, variable references, arithmetic operators
- Aggregate functions: `SUM`, `AVG`, `MIN`, `MAX`, `COUNT`, `COUNTIF`, `MAX_ROW`, `RANK`
