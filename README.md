# Agent-Ready Service Pattern Specification

**A machine and AI-readable representation of GovStack UX/UI service patterns.**

---

> *"The primary user of a government service will not be a human staring at a screen, but a software agent acting on that human's behalf."*
> — GovStack AI Readiness Guide, §1.2

---

## What this is

GovStack service patterns are currently documented as human-readable text. This specification adds a formal, machine-consumable layer: a JSON Schema that allows AI agents, validators, and developer tools to **discover, compose, validate, and execute** service patterns without human interpretation.

This is the **AI-readiness layer for GovStack UX/UI service patterns**.

## Repository structure

```
├── README.md                        ← this file
├── schema/
│   └── service-pattern.schema.json  ← canonical JSON Schema
├── patterns/
│   ├── step/                        ← 11 step patterns
│   └── functional/                  ← 12 functional patterns
└── docs/
    ├── 1-version-history.md
    ├── 2-description.md
    ├── 3-terminology.md
    ├── 4-key-digital-functionalities.md
    ├── 5-cross-cutting-requirements.md
    ├── 6-functional-requirements.md
    ├── 7-data-structures.md
    ├── 8-agentic-use-cases.md
    ├── 9-workflows.md
    └── 10-other-resources.md
```

## Vision

The life event scenario — a single event triggering coordinated, automatic government action across civil registry, health, social protection, tax, and education — is the horizon this specification is pointed at.

→ [Read: The Life Event Horizon](docs/11-vision.md)

---

## Quick start

**For AI agents:** Load `schema/service-pattern.schema.json` and the relevant pattern files from `patterns/`. Use `use_when` arrays for pattern selection, `flow` for traversal, and `inputs`/`outputs` for data contracts.

**For developers:** Validate your service implementation against the schema using any JSON Schema validator (draft 2020-12).

**For designers:** Browse `patterns/functional/` to find the closest pattern to your service, and `patterns/step/` for individual interaction components.

## Status

| Patterns | Count | Status |
|---|---|---|
| Step patterns | 11 | In progress |
| Functional patterns | 12 | In progress |
| JSON Schema | 1 | Stable |

## Contributing

See `docs/` for the full specification. Contributions follow the GovStack Building Block contribution guidelines.

## Related resources

- [GovStack AI Readiness Guide](https://specs.govstack.global/ai-readiness)
- [GovStack Service Patterns](https://specs.govstack.global/service-patterns)
- [GovStack Implementation Playbook](https://app.gitbook.com/s/DLeKag4x9xUV26hiPlNo/)
- [DPI Safeguard Framework — UN 2024](https://www.undp.org/digital/dpi-safeguards)
