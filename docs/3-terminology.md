# 3. Terminology

### Agent / Agentic System

A software system capable of autonomously performing tasks on behalf of a user, including discovering services, navigating flows, submitting data, and receiving outcomes — without requiring human interaction at each step. In the context of this specification, an agent is the primary consumer of machine-readable service patterns.

### Service Pattern

A reusable, tested model of how a government service or interaction typically works. GovStack defines service patterns at two levels: step patterns and functional patterns.

### Step Pattern

A single, reusable user task or screen-level interaction (e.g., "Check answers", "Send a notification"). Step patterns are the atomic building blocks of service journeys. They define a specific purpose, expected inputs, produced outputs, and interaction guidance.

### Functional Pattern

A complete end-to-end service journey composed of multiple step patterns (e.g., "Make a payment", "Authenticate"). Functional patterns define the overall flow, the sequence of steps, branching conditions, and the building blocks involved.

### Flow Graph

A directed graph representation of the transitions between steps in a functional pattern. Each edge connects two steps and may carry a condition that must be satisfied for the transition to occur. The graph has a designated entry node (`START`) and one or more terminal nodes (`END`).

### Machine-readable

A format that can be parsed, traversed, and processed by software without ambiguity. In this specification, machine-readable means valid JSON conforming to the defined JSON Schema, with typed fields, explicit conditions, and formal data contracts.

### AI-readable

A subset of machine-readable that additionally supports reasoning by large language models and AI agents. AI-readable patterns carry enough semantic context — through `use_when`, `purpose`, `label`, and `description` fields — for an agent to understand intent, not just structure.

### Determinism

The property of a system that produces the same output given the same input, every time. In the context of agentic government services, determinism means that every flow branch has an explicit, unambiguous condition — leaving no room for an agent to guess or hallucinate an outcome.

### Conformance

The state in which a service implementation satisfies all constraints defined as `"severity": "must"` in the relevant pattern(s). A conformant implementation covers all required steps, handles all defined output states, and respects all mandatory UX and technical notes.

### Building Block Reference

A pointer from a pattern to a GovStack Building Block (e.g., `bb.payment`, `bb.identity`) that the pattern depends on. Each reference carries a `role` indicating whether the BB is primary, supporting, optional, or conditional for that pattern.

### Data Field

A typed, named piece of data that a step or pattern either consumes (input) or produces (output). Data fields carry a type, an optional set of allowed values (for enums), a required flag, and a sensitive flag indicating whether the data contains personal or sensitive information.

### Severity

A conformance level indicator applied to UX considerations and technical notes, following RFC 2119 conventions:
- `must` — required for conformance; non-compliance is a defect
- `should` — strongly recommended; deviation requires justification
- `may` — optional; included for guidance only
