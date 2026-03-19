# 8. Agentic Use Cases

This section describes how AI agents can consume machine-readable service patterns to perform tasks that currently require expert human knowledge. Each use case maps directly to a functionality described in Section 4.

---

## 8.1 Pattern Recommendation

**Scenario:** A government team is designing a new digital service and needs to know which GovStack patterns apply.

**Agent behaviour:**
1. Receives a service description in natural language (e.g., "Citizens apply for a birth certificate and pay a fee")
2. Loads the pattern catalogue
3. Evaluates each functional pattern's `use_when` array against the description
4. Returns a ranked list of applicable patterns with justification

**What makes this possible:** Structured `use_when` arrays in plain English, paired with `do_not_use_when` exclusions, give the agent unambiguous selection criteria without requiring it to interpret narrative prose.

**Output example:**
```
Recommended patterns:
- pattern.authenticate        (identity verification required before service access)
- pattern.check-eligibility   (not all citizens can obtain a birth certificate)
- pattern.make-a-payment      (fee required before issuance)
- pattern.get-a-credential    (birth certificate is a reusable credential)
```

---

## 8.2 Service Blueprint Generation

**Scenario:** An agent is asked to produce a complete service blueprint for a passport application.

**Agent behaviour:**
1. Selects the relevant functional patterns via use case 8.1
2. Checks input/output compatibility between patterns (output of step N → input of step N+1)
3. Uses `related_patterns` references as composition hints
4. Generates a composite JSON document representing the full service flow
5. Validates the composite against the JSON Schema

**What makes this possible:** Typed `DataField` inputs and outputs allow the agent to verify that data flows correctly between patterns — the same way a type system catches mismatches at compile time.

**Value:** A task that currently takes an expert consultant days to produce becomes a validated, machine-generated starting point in seconds.

---

## 8.3 Conformance Audit

**Scenario:** A country has built a digital service and wants to verify that it conforms to GovStack standards before deployment.

**Agent behaviour:**
1. Receives the service implementation description (or a structured service spec)
2. Loads the referenced patterns
3. Checks that:
   - All `optional: false` steps are present
   - All flow branches are handled (including failure states)
   - All `severity: "must"` UX considerations are addressed
   - All `severity: "must"` technical notes are satisfied
4. Returns a conformance report: passed checks, failed checks, and unverifiable checks

**What makes this possible:** The `severity` field on `UXConsideration` and `TechnicalNote` transforms design guidance into machine-checkable conformance criteria. The explicit `flow` graph makes it possible to enumerate all branches and verify coverage.

**Value:** Countries can run automated pre-deployment audits. Development teams catch gaps earlier in the process, reducing remediation cost.

---

## 8.4 Life Event Orchestration

**Scenario:** A citizen registers the birth of a child. This single event should automatically trigger multiple government services.

**Agent behaviour:**
1. Receives trigger: `life_event: birth_registration`
2. Loads all patterns tagged with relevant contexts
3. Identifies required services: civil registry update, social benefit enrollment, health record creation, tax authority notification
4. For each service, selects the appropriate functional patterns
5. Orchestrates the execution sequence, passing outputs from one service as inputs to the next
6. Tracks status across all services and notifies the citizen on completion or failure

**What makes this possible:** Typed `outputs` from each pattern (e.g., `credential.id`, `registration.reference`) become inputs to the next service in the chain. The agent does not need to interpret what a "birth certificate number" is — it is a `string` output of `pattern.get-a-credential` that feeds into subsequent services.

**Value:** This is the core promise of the GovStack AI Readiness Guide: a single life event triggers coordinated, automatic government action. The citizen does not navigate between departments. The agent does it for them.

---

## 8.5 AI Skill Packaging

**Scenario:** Any AI agent (regardless of platform) should be able to become GovStack-aware by loading a single skill package.

**Structure of the skill:**
```
govstack-patterns-skill/
├── SKILL.md                    ← agent instructions
├── schema/
│   └── service-pattern.schema.json
└── patterns/
    ├── step/        ← all 11 step patterns
    └── functional/  ← all 12 functional patterns
```

**SKILL.md instructs the agent to:**
- Use `use_when` arrays to select patterns
- Use `flow` graphs to reason about service journeys
- Use `inputs`/`outputs` to verify data compatibility
- Use `severity: "must"` fields to identify non-negotiable requirements
- Use `building_blocks` references to identify infrastructure dependencies

**What makes this possible:** The combination of a formal schema and a complete, consistent catalogue means the entire GovStack pattern knowledge base fits in a single loadable context. Any agent with this skill can answer questions about service design, generate blueprints, and validate implementations — without internet access, without hallucination risk, and without requiring a GovStack expert in the loop.

**Value:** This democratises GovStack expertise. A small country with limited digital government capacity can deploy an agent that applies GovStack best practices automatically, from day one.
