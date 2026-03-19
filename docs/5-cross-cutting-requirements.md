# 5. Cross-Cutting Requirements

These requirements apply to all patterns defined under this specification, regardless of type (step or functional).

---

## 5.1 Determinism

Every conditional branch in a flow graph **must** carry an explicit `condition` expression. Unconditional edges are permitted only where no branching occurs.

Condition expressions **should** use a declared `syntax` value (`natural-language`, `jsonlogic`, `jexl`, `cel`, or `javascript`). Implementations consuming patterns for automated evaluation **must** declare and respect the syntax used.

Pattern authors **must not** use vague or open-ended conditions (e.g., "if appropriate", "as needed"). All conditions must be resolvable to a boolean outcome given a defined data context.

**Rationale:** The GovStack AI Readiness Guide identifies ambiguous interfaces as the root cause of agent hallucinations in public sector contexts. Deterministic conditions prevent agents from guessing outcomes and protect citizens from automated errors.

---

## 5.2 Versioning

Every pattern **must** carry a `version` field following semantic versioning (semver.org):
- **Patch** (x.x.N): clarifications, typo fixes, no structural change
- **Minor** (x.N.0): new optional fields, new variants, backwards-compatible additions
- **Major** (N.0.0): breaking changes to required fields, flow structure, or data contracts

Every pattern **should** carry a `changelog` array documenting what changed in each version.

When a pattern is replaced by a newer one, the superseded pattern **must** set `status: deprecated` and the new pattern **must** reference it via the `supersedes` field.

---

## 5.3 Extensibility

Every top-level object in the schema carries an `extensions` field that accepts arbitrary key-value pairs. This allows:
- Country-specific metadata without forking the schema
- Tooling-specific annotations (e.g., Figma component links, GitHub issue references)
- Experimental fields under review for future schema versions

Extension keys **should** use reverse-domain namespacing to avoid collisions (e.g., `"x-ke.nairobi-county.field": "value"`).

Extensions **must not** be used to override or contradict core schema fields. If a country or implementation requires a structural change, a formal schema contribution should be made instead.

---

## 5.4 Multi-Channel Support

Patterns **must** be designed to support at minimum three service delivery channels:
- **Digital** — web or mobile application
- **Assisted** — a human agent (civil servant, help desk operator) acting on the citizen's behalf
- **Offline** — paper-based or in-person processes with no digital component

Steps that only apply to specific channels **must** declare this via the `channel_constraints` field. Steps without `channel_constraints` are assumed to apply to all channels.

UX considerations **should** specify their target channels via the `applies_to` field.

---

## 5.5 Privacy and Data Sensitivity

Any `DataField` containing personal or sensitive data **must** set `sensitive: true`.

Sensitive fields carry the following implied constraints for consuming systems:
- **Display:** mask or partially hide values where full display is not required
- **Logging:** exclude from plain-text logs; apply appropriate encryption
- **Transfer:** require explicit consent or legal basis before sharing across systems
- **Retention:** subject to applicable data protection regulations

Pattern authors **must not** include sensitive data in `label` or `description` fields as examples. Use placeholders (e.g., `"user.id": "[citizen identifier]"`).
