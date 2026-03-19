# 6. Functional Requirements

## 6.1 Step Patterns

Step patterns are the atomic building blocks of service journeys. Each step pattern defines a single user task or screen-level interaction.

All step patterns **must** conform to the `StepPattern` type defined in the JSON Schema (see Section 7).

### Catalogue

| ID | Label | Status |
|---|---|---|
| `step.service-catalogue` | Service catalogue | Pending |
| `step.service-sheet` | Service sheet | Pending |
| `step.task-list` | Task list | Pending |
| `step.before-you-start` | Before you start | Pending |
| `step.ask-a-question` | Ask a question | Pending |
| `step.upload-information` | Upload information | Pending |
| `step.check-answers` | Check answers | **Stable** |
| `step.outcome` | Outcome | Pending |
| `step.ask-for-feedback` | Ask for feedback | Pending |
| `step.send-a-notification` | Send a notification | Pending |
| `step.matching` | Matching | Pending |

Source: [GovStack Step Patterns](https://specs.govstack.global/service-patterns/3.-step-patterns)

---

## 6.2 Functional Patterns

Functional patterns describe complete end-to-end service journeys composed of multiple step patterns.

All functional patterns **must** conform to the `FunctionalPattern` type defined in the JSON Schema (see Section 7).

### Catalogue

| ID | Label | Status |
|---|---|---|
| `pattern.find-a-service` | Find a service | Pending |
| `pattern.guide-users` | Guide users through a service | Pending |
| `pattern.other-ways-to-access` | Other ways to access a service | Pending |
| `pattern.ask-for-consent` | Ask for consent | Pending |
| `pattern.authenticate` | Authenticate | Pending |
| `pattern.check-eligibility` | Check eligibility | Pending |
| `pattern.get-a-credential` | Get a credential | Pending |
| `pattern.manage-a-credential` | Manage a credential | Pending |
| `pattern.present-a-credential` | Present a credential | Pending |
| `pattern.make-a-payment` | Make a payment | **Stable** |
| `pattern.schedule-an-appointment` | Schedule an appointment | Pending |
| `pattern.provide-a-signature` | Provide a signature | Pending |

Source: [GovStack Functional Patterns](https://specs.govstack.global/service-patterns/2.-functional-patterns)
