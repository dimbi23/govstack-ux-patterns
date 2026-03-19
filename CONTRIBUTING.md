# Contributing

Thank you for your interest in contributing to the GovStack Agent-Ready Service Pattern Specification.

This project is a community contribution to the [GovStack UX/UI Building Block](https://govstack.global). Contributions of all kinds are welcome — new patterns, corrections, translations of technical notes, tooling, and documentation improvements.

---

## Ways to contribute

- **Encode a missing pattern** — check `docs/6-functional-requirements.md` for any patterns still marked `Pending`
- **Improve an existing pattern** — fix inaccuracies, add missing UX considerations or technical notes, improve flow conditions
- **Add a variant** — document a known contextual variant of a step pattern
- **Build tooling** — validators, visualisers, code generators using the JSON Schema
- **Raise an issue** — flag inconsistencies with the official GovStack spec, or suggest schema improvements

---

## Before you start

1. Read the [GovStack Service Patterns specification](https://specs.govstack.global/service-patterns)
2. Read `docs/7-data-structures.md` to understand the schema
3. Read the existing patterns in `patterns/` to understand the conventions
4. Open an issue before starting significant work — to avoid duplication and align on scope

---

## Adding or editing a pattern

### Step patterns

Files go in `patterns/step/step.<slug>.json`.

Required fields: `id`, `version`, `kind`, `status`, `label`, `purpose`  
Convention: `id` must follow `step.<kebab-case-slug>`

### Functional patterns

Files go in `patterns/functional/pattern.<slug>.json`.

Required fields: `id`, `version`, `kind`, `status`, `label`, `use_when`, `steps`, `flow`  
Convention: `id` must follow `pattern.<kebab-case-slug>`

### Validation

Your pattern must be valid JSON and conform to `schema/service-pattern.schema.json`.

You can validate locally with any JSON Schema draft 2020-12 validator:

```bash
# Example with ajv-cli
npx ajv validate -s schema/service-pattern.schema.json -d patterns/step/your-pattern.json
```

---

## Schema changes

Schema changes require more care than pattern additions.

- **Backwards-compatible additions** (new optional fields): open a PR with a clear description
- **Breaking changes**: open an issue first for discussion before any PR
- All schema changes must increment the version in `$id` following semver

---

## Pull request checklist

- [ ] Pattern file is valid JSON
- [ ] Pattern conforms to the JSON Schema
- [ ] `source_url` points to the canonical GovStack spec page
- [ ] All required fields are present
- [ ] `flow` has explicit `condition` on all branching edges
- [ ] Sensitive data fields have `"sensitive": true`
- [ ] `ux_considerations` and `technical_notes` use correct severity (`must` / `should` / `may`)
- [ ] `status` is appropriate (`draft` for new, `stable` only after review)
- [ ] `version` is incremented if editing an existing pattern
- [ ] `changelog` entry added if editing an existing pattern

---

## Code of conduct

This project follows the [Contributor Covenant Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/).

Be respectful, constructive, and collaborative. This is expert-driven, community-based work — the same spirit as GovStack itself.

---

## Questions

Open an issue or start a discussion on GitHub. For GovStack-specific questions, refer to the [GovStack community](https://govstack.global/community).
