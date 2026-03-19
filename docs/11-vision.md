# 11. Vision — The Life Event Horizon

> *"A child is born. A parent shouldn't have to visit five ministries."*

---

## The promise of agentic government

Every government that has invested in digital infrastructure has made, implicitly or explicitly, a promise to its citizens: that the state will work for them — not the other way around.

For decades, that promise has been only partially kept. Digital services replaced paper forms. Portals replaced physical offices. But the citizen remained the connector. They still had to know which agency to contact, which document to bring, which deadline to meet — and do it five times over for a single life event.

The GovStack AI Readiness Guide names this clearly: *"the citizen acts as the manual connector between disconnected databases."*

Machine-readable service patterns are a step toward ending that.

---

## The life event scenario

A child is born.

In a GovStack-aligned agentic infrastructure, this single event triggers a coordinated, automatic cascade:

1. **Civil registry** — birth registered, certificate issued (`pattern.get-a-credential`)
2. **National identity** — child enrolled in the identity system (`pattern.authenticate` → identity BB)
3. **Health system** — vaccination schedule created, first appointment booked (`pattern.schedule-an-appointment`)
4. **Social protection** — eligibility checked, family benefit enrollment triggered (`pattern.check-eligibility`)
5. **Tax authority** — dependent status updated, family tax record amended
6. **Education** — pre-registration for school cohort initiated

The parent does not navigate between departments.  
The parent does not re-enter their name six times.  
The parent does not miss a deadline they didn't know existed.

The agent does it for them — deterministically, traceably, and with the citizen's consent at every step.

---

## Why this requires machine-readable patterns

This scenario is not science fiction. The building blocks exist. The data flows are possible. What has been missing is a **shared, formal language** for describing how services behave — one that both humans and machines can read without ambiguity.

Narrative documentation cannot power this. A software agent cannot read a GitBook page and reliably determine:
- Which steps are required vs optional
- What data a service needs before it can start
- What states a service can end in
- Which building blocks must be in place
- When and how to hand off to the next service

Machine-readable patterns answer all of these questions — explicitly, deterministically, without interpretation.

Each pattern's `flow` graph defines the journey. Each `DataField` defines the contract. Each `severity: "must"` defines the non-negotiable. Each `outputs` → `inputs` chain defines the handoff.

The life event cascade becomes a **composition problem** — one that any sufficiently capable agent can solve.

---

## What this means for adopter country?

Several countries are deploying foundational identity and digital payment infrastructure right now — before legacy systems have calcified, before path dependencies have locked in the portal model.

The window to build for the agentic era — rather than retrofit for it — is open.

Machine-readable service patterns are one piece of that foundation. They ensure that the services being built today can be composed, orchestrated, and extended tomorrow — by agents, by other services, and by governments that have not yet started their journey.

Building for machines is not a technical luxury. It is a design decision that determines whether the infrastructure we build today will serve citizens for ten years or for fifty.

---

## The horizon

The life event cascade is the horizon this specification is pointed at.

Not as a distant aspiration — but as a concrete, achievable next state for governments that are willing to:
- Formalise their service patterns
- Type their data contracts
- Make their flows explicit
- And share that knowledge as open infrastructure

---

*"The primary product of a modern government is no longer its Graphical User Interface. It is its Application Programming Interface."*  
— GovStack AI Readiness Guide, §1.2
