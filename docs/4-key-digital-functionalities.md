# 4. Key Digital Functionalities

This specification enables five core functionalities for AI agents and developer tooling operating on GovStack service patterns.

---

## 4.1 Pattern Discovery

An agent can identify the correct pattern for a given service context by reasoning over the `use_when` and `do_not_use_when` arrays of each pattern.

**How it works:**
- The agent receives a service description or a set of requirements
- It evaluates each pattern's `use_when` conditions against the context
- It selects the matching functional pattern(s) and their component step patterns

**Why it matters:**
Without this, an agent building or auditing a government service must read narrative documentation and interpret it. With structured `use_when` arrays, the selection becomes deterministic and auditable.

**Example:**
> "I need to build a service where citizens pay a fee before receiving a permit."
> → Agent matches `pattern.make-a-payment` (`use_when`: "A service requires payment before completion or progression.")

---

## 4.2 Service Composition

An agent can assemble a complete, multi-pattern service by chaining functional patterns together, connecting the `outputs` of one to the `inputs` of the next.

**How it works:**
- The agent identifies the functional patterns required for the target service
- It checks that the output types of one pattern are compatible with the input types of the next
- It uses `related_patterns` references as composition hints
- It produces a composite service blueprint as a structured document

**Why it matters:**
A life event service (e.g., birth registration) typically requires authentication, eligibility check, credential issuance, and payment. Today, assembling this requires expert knowledge. With typed inputs/outputs, composition becomes a data-matching problem that any agent can solve.

---

## 4.3 Conformance Validation

An agent or automated tool can verify that a service implementation satisfies the requirements defined in its referenced patterns.

**How it works:**
- For each pattern referenced by the service, the agent checks that:
  - All steps with `optional: false` are present in the implementation
  - All `outputs` defined by the pattern are handled by the next step or returned
  - All UX considerations and technical notes with `severity: "must"` are addressed
  - All flow branches defined in the `flow` graph are covered

**Why it matters:**
This converts the GovStack pattern specification from a design reference into an executable compliance standard. Countries can run automated audits against their implementations before deployment.

---

## 4.4 Flow Traversal

An agent can algorithmically walk the `flow` graph of a functional pattern to simulate a citizen journey, detect structural issues, or generate test cases.

**How it works:**
- The graph is a directed structure with `from`/`to` edges and optional `condition` expressions
- Starting from `START`, the agent follows edges based on condition evaluation
- It detects: dead-ends (steps with no outgoing edge), orphaned steps (steps not reachable from `START`), and missing terminal nodes (paths that never reach `END`)

**Why it matters:**
The GovStack AI Readiness Guide identifies vague or ambiguous interfaces as the primary source of agent hallucinations. Explicit, traversable flow graphs eliminate structural ambiguity at design time, before any implementation begins.

---

## 4.5 Deterministic Handoff

An agent passing control between steps, patterns, or external systems can rely on typed, named data contracts to transfer state without ambiguity.

**How it works:**
- Each step defines its `inputs` (what it needs) and `outputs` (what it produces) as typed `DataField` objects
- Sensitive fields are flagged, allowing agents to apply appropriate handling (masking, encryption, access control)
- Output enum values (e.g., `payment.status: success | pending | failed`) leave no room for interpretation

**Why it matters:**
In a multi-agent government service pipeline, ambiguous state transfer is the equivalent of a corrupt handshake. Typed data contracts ensure that every agent in the chain receives exactly what it expects, in exactly the format it can process — making the entire pipeline deterministic and safe.
