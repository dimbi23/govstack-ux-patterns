# 9. Workflows

## 9.1 How an Agent Selects a Pattern

```
INPUT: service description (natural language or structured)

1. Load pattern catalogue (all functional patterns)
2. For each functional pattern:
   a. Evaluate use_when[] against service description
   b. Evaluate do_not_use_when[] — exclude if any condition matches
   c. Score relevance
3. Return ranked list of matching patterns
4. For each selected functional pattern:
   a. Identify referenced step patterns (via steps[].ref)
   b. Load step patterns
5. OUTPUT: recommended pattern set with justification
```

**Decision rule:** A pattern is selected if at least one `use_when` condition matches and no `do_not_use_when` condition matches.

---

## 9.2 How an Agent Composes a Multi-Pattern Service

```
INPUT: list of selected functional patterns

1. For each pattern, extract:
   - inputs[] (what it needs)
   - outputs[] (what it produces)
2. Build a dependency graph:
   - Edge: pattern A → pattern B if A.outputs[] satisfies B.inputs[]
3. Detect conflicts:
   - Missing inputs (no pattern produces a required input)
   - Type mismatches (output type ≠ input type)
4. Resolve ordering:
   - Topological sort of the dependency graph
5. Use related_patterns[] as additional composition hints
6. Generate composite service blueprint (JSON)
7. Validate composite against schema
8. OUTPUT: ordered service blueprint with data flow annotations
```

**Composition rule:** Outputs are matched to inputs by `id` convention and `type` compatibility. When `id` conventions differ, the agent must declare an explicit mapping.

---

## 9.3 How an Agent Validates an Implementation

```
INPUT: service implementation spec + referenced pattern IDs

1. Load all referenced patterns
2. For each functional pattern:
   a. Check all steps with optional: false are present → MUST
   b. Traverse flow graph:
      - Verify all steps are reachable from START
      - Verify all paths reach END
      - Verify all conditional edges have explicit conditions
3. For each step pattern:
   a. Check all outputs are consumed or returned
   b. Check sensitive fields are handled (masked, encrypted)
4. For all ux_considerations with severity: "must":
   a. Check each is addressed in the implementation
5. For all technical_notes with severity: "must":
   a. Check each is satisfied
6. Generate conformance report:
   - PASS: check satisfied
   - FAIL: required check not satisfied (blocks deployment)
   - WARN: should-level check not satisfied (requires justification)
   - SKIP: check not verifiable automatically (requires human review)
7. OUTPUT: conformance report with per-check status and remediation guidance
```
