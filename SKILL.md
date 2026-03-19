---
name: govstack-ux-patterns
description: GovStack agent-ready service pattern catalogue. Use when designing, validating, or composing government digital services following GovStack standards. Enables pattern recommendation, service blueprint generation, conformance validation, and building block identification for any government service journey (authentication, payment, eligibility, credentials, scheduling, consent, signature, and more).
license: CC-BY-4.0
metadata:
  author: Dimbinirina Razafindramanana
  version: "1.0.0"
  source: https://github.com/dimbi23/govstack-ux-patterns
  spec: https://specs.govstack.global/service-patterns
---

# GovStack Agent-Ready Service Patterns

You have access to a complete, machine-readable catalogue of GovStack service patterns — the formal building blocks of government digital services.

Use this skill when:
- Designing or reviewing a government digital service
- Selecting the right GovStack pattern(s) for a given service context
- Composing a multi-pattern service blueprint
- Validating that an implementation meets GovStack requirements
- Identifying which GovStack Building Blocks are needed
- Explaining what a pattern does, what it needs, and what it produces

---

## Catalogue

### Step Patterns — atomic interactions (11)

Files: `patterns/step/<id>.json`

| ID | Label |
|---|---|
| `step.service-catalogue` | Service catalogue |
| `step.service-sheet` | Service sheet |
| `step.task-list` | Task list |
| `step.before-you-start` | Before you start |
| `step.ask-a-question` | Ask a question |
| `step.upload-information` | Upload information |
| `step.check-answers` | Check answers |
| `step.outcome` | Outcome |
| `step.ask-for-feedback` | Ask for feedback |
| `step.send-a-notification` | Send a notification |
| `step.matching` | Matching |

### Functional Patterns — end-to-end journeys (12)

Files: `patterns/functional/<id>.json`

| ID | Label |
|---|---|
| `pattern.find-a-service` | Find a service |
| `pattern.guide-users` | Guide users through a service |
| `pattern.other-ways-to-access` | Other ways to access a service |
| `pattern.ask-for-consent` | Ask for consent |
| `pattern.authenticate` | Authenticate |
| `pattern.check-eligibility` | Check eligibility |
| `pattern.get-a-credential` | Get a credential |
| `pattern.manage-a-credential` | Manage a credential |
| `pattern.present-a-credential` | Present a credential |
| `pattern.make-a-payment` | Make a payment |
| `pattern.schedule-an-appointment` | Schedule an appointment |
| `pattern.provide-a-signature` | Provide a signature |

### Schema

`schema/service-pattern.schema.json` — JSON Schema draft 2020-12

Full documentation: see [references/REFERENCE.md](references/REFERENCE.md)

---

## How to use this skill

### 1. Pattern selection

Evaluate each functional pattern's `use_when` array against the service context.

**Rule:** Select a pattern if at least one `use_when` matches AND no `do_not_use_when` matches.

**Example:** *"A citizen registers a birth and receives a certificate"*
→ `pattern.authenticate` + `pattern.check-eligibility` + `pattern.get-a-credential`

### 2. Service composition

1. Select applicable functional patterns
2. Match `outputs` of one pattern to `inputs` of the next (by field `id` and `type`)
3. Use `related_patterns` as composition hints
4. Produce an ordered service blueprint

### 3. Conformance validation

For each referenced pattern, check:
- All steps with `"optional": false` are present
- All flow branches are handled including failure states
- All `"severity": "must"` UX and technical requirements are addressed

Severity levels (RFC 2119):
- `must` → required; non-compliance is a defect
- `should` → strongly recommended
- `may` → optional guidance

### 4. Flow traversal

Parse the `flow` array as a directed graph. Entry: `START`. Exit: `END`. Detect dead-ends, orphaned steps, and unguarded branches.

### 5. Building block identification

Aggregate `building_blocks` across all selected patterns. Deduplicate by `id`. Report required BBs with role: `primary`, `supporting`, `optional`, or `conditional`.

---

## Key agentic use cases

| Use case | Approach |
|---|---|
| Pattern recommendation | Evaluate `use_when` / `do_not_use_when` |
| Service blueprint | Compose by matching `outputs` → `inputs` |
| Conformance audit | Check all `must` constraints |
| Life event orchestration | Chain patterns via typed data contracts |
| BB dependency report | Aggregate `building_blocks` across patterns |

---

## Important rules

- **Determinism:** every conditional flow edge has an explicit `condition.expression` — never infer a branch
- **Sensitive data:** fields with `"sensitive": true` must be masked in display and excluded from plain logs
- **Multi-channel:** patterns apply to digital, assisted, offline, mobile, and kiosk unless `channel_constraints` specifies otherwise
