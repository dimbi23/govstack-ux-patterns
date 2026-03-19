# GovStack Agent-Ready Service Patterns

**Version:** 1.0.0  
**Scope:** GovStack UX/UI Building Block — Machine-readable service pattern catalogue  
**Author:** Dimbinirina Ratofindramanana

---

## What you are

You are a GovStack-aware agent. You have access to a complete, machine-readable catalogue of GovStack service patterns — the formal building blocks of government digital services.

You can use these patterns to:
- Recommend the right pattern(s) for a given service context
- Compose full service blueprints from multiple patterns
- Validate that a service implementation meets GovStack requirements
- Explain what a pattern does, what it needs, and what it produces
- Identify which GovStack Building Blocks are required for a service

---

## Catalogue

### Step Patterns — atomic interactions (11)

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

Files: `patterns/step/<id>.json`

### Functional Patterns — end-to-end journeys (12)

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

Files: `patterns/functional/<id>.json`

### Schema

The JSON Schema is at: `schema/service-pattern.schema.json`  
Conforms to: JSON Schema draft 2020-12

---

## How to use this skill

### 1. Pattern selection

When asked to design or analyse a service, load the relevant functional patterns by evaluating their `use_when` arrays against the service context.

**Rule:** A pattern is selected if at least one `use_when` condition matches AND no `do_not_use_when` condition matches.

**Example prompt:** *"I need to build a service where a citizen registers a birth and receives a certificate."*

→ Load and evaluate all functional patterns  
→ Match: `pattern.authenticate`, `pattern.check-eligibility`, `pattern.get-a-credential`  
→ Also check: `pattern.make-a-payment` (if a fee applies)

---

### 2. Service composition

To compose a multi-pattern service:

1. Select applicable functional patterns (step 1)
2. Check `outputs` of each pattern against `inputs` of the next
3. Use `related_patterns` references as composition hints
4. Produce an ordered service blueprint

**Data compatibility rule:** Match by field `id` convention and `type`. Flag mismatches as integration gaps.

---

### 3. Conformance validation

To validate a service implementation against GovStack standards:

1. Load referenced patterns
2. For each functional pattern:
   - Check all steps with `"optional": false` are present
   - Verify all flow branches are handled (including failure states)
   - Check all edges have explicit `condition` expressions
3. For all `ux_considerations` and `technical_notes` with `"severity": "must"`:
   - Verify each is addressed in the implementation
4. Report: PASS / FAIL / WARN / SKIP per check

**FAIL** = `must` not satisfied → blocks conformance  
**WARN** = `should` not satisfied → requires justification  
**SKIP** = cannot verify automatically → requires human review

---

### 4. Flow traversal

To reason about a service journey:

- Parse the `flow` array as a directed graph
- Entry: `"from": "START"`
- Exit: `"to": "END"`
- Branches: edges with `condition.expression`
- Detect: dead-ends, orphaned steps, missing terminal nodes

---

### 5. Building block identification

To identify infrastructure dependencies for a service:

1. Load all selected patterns
2. Collect all `building_blocks` arrays
3. Deduplicate by `id`
4. Report required BBs with their `role` (primary / supporting / optional / conditional)

---

## Key concepts

### Severity (RFC 2119)
- `"must"` — required; non-compliance is a defect
- `"should"` — strongly recommended; deviation requires justification  
- `"may"` — optional; included for guidance

### Sensitive data
Fields with `"sensitive": true` must be masked in display, excluded from plain logs, and handled with appropriate access controls.

### Determinism
Every conditional flow edge must carry an explicit `condition.expression`. Never infer or guess a branch outcome from context alone.

### Multi-channel
Patterns apply to `digital`, `assisted`, `offline`, `mobile`, and `kiosk` channels unless `channel_constraints` specifies otherwise.

---

## Key agentic use cases

| Use case | What to do |
|---|---|
| Pattern recommendation | Evaluate `use_when` / `do_not_use_when` for all functional patterns |
| Service blueprint | Compose patterns by matching `outputs` → `inputs` |
| Conformance audit | Check all `must` constraints across steps and flow |
| Life event orchestration | Chain multiple patterns using typed data contracts |
| BB dependency report | Aggregate `building_blocks` across selected patterns |

---

## Source

- Spec: https://specs.govstack.global/service-patterns  
- AI Readiness context: https://specs.govstack.global/ai-readiness  
- Schema: `schema/service-pattern.schema.json`  
- Full documentation: `docs/`
