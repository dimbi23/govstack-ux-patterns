# 2. Description

## 2.1 Context: From Portal to Agentic State

For two decades, digital government operated under what the GovStack AI Readiness Guide calls the **"Web Portal Paradigm"** — taking paper processes and migrating them to screens. Forms became HTML pages. Offices became websites. But the underlying bureaucratic logic remained unchanged, and the citizen remained the manual connector between disconnected systems.

That model has hit its limits.

We are now entering what GovStack identifies as the **third phase of digital government**: the Agentic State. The driving force is the rise of AI-driven conversational interfaces and autonomous software agents. In this phase, the primary user of a government service is no longer a human staring at a screen — it is a software agent acting on that human's behalf.

This shift has a direct architectural consequence: **the primary product of a modern government is no longer its GUI, it is its API**. Systems must stop being built for human eyes and start being built for machine understanding.

## 2.2 The Problem: UX Patterns Are Human-Readable Only

GovStack service patterns are currently documented as narrative text in GitBook. They describe — clearly and usefully — how services should be designed, what steps they involve, and how users move through them.

But a software agent cannot consume narrative text reliably. It cannot:

- Traverse a flow and determine which branches are possible
- Verify that an implementation covers all required steps
- Connect the outputs of one pattern to the inputs of another
- Compose multiple patterns into a coherent service blueprint
- Do any of this **deterministically** — without risk of misinterpretation or hallucination

The GovStack AI Readiness Guide is explicit on this point: *"If an AI agent encounters a vague error or an ambiguous rule, it may attempt to guess the solution. In the public sector, this is a liability."*

The current pattern documentation, however excellent for humans, is ambiguous by nature. It was not designed for machines.

## 2.3 The Contribution: A Machine-Consumable Pattern Layer

This specification introduces a **formal, machine-readable representation** of GovStack UX/UI service patterns.

It does not replace the existing narrative documentation. It adds a complementary layer: a **JSON Schema** that formalizes the structure of every service pattern — step patterns and functional patterns alike — in a way that is:

- **Traversable** — the flow graph can be walked algorithmically
- **Composable** — patterns can be chained via typed inputs and outputs
- **Validatable** — implementations can be checked for conformance automatically
- **Deterministic** — conditions are explicit; no guessing required
- **Versionable** — each pattern carries a semantic version and changelog
- **Extensible** — open to context-specific metadata without breaking the core contract

This is the **AI-readiness layer for GovStack UX/UI service patterns**.

## 2.4 Scope and Boundaries

**In scope:**
- A JSON Schema for representing Step Patterns and Functional Patterns
- Machine-readable encodings of all 11 step patterns and 12 functional patterns defined in the GovStack service pattern specification
- Documentation of agentic use cases enabled by this representation

**Out of scope:**
- Replacing or modifying the existing GovStack narrative documentation
- Defining new service patterns not already present in the GovStack specification
- Runtime execution environments or agent orchestration platforms
- UI component libraries or design system specifications
