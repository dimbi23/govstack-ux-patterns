# 7. Data Structures

The canonical JSON Schema is located at: `schema/service-pattern.schema.json`

It conforms to **JSON Schema draft 2020-12** and can be validated using any compliant validator.

---

## 7.1 Top-Level Discriminator

Every pattern document is either a `StepPattern` or a `FunctionalPattern`, identified by the required `kind` field.

```json
{ "kind": "StepPattern" }     // single interaction
{ "kind": "FunctionalPattern" } // end-to-end journey
```

---

## 7.2 Shared Types

### PatternMetadata

Common metadata present in all patterns.

| Field | Type | Required | Description |
|---|---|---|---|
| `id` | string | ✅ | Unique ID. Convention: `<prefix>.<slug>` (e.g. `step.check-answers`) |
| `version` | string (semver) | ✅ | Semantic version |
| `kind` | enum | ✅ | `StepPattern` or `FunctionalPattern` |
| `status` | enum | ✅ | `draft`, `review`, `stable`, `deprecated` |
| `label` | string | ✅ | Short human-readable name |
| `description` | string | — | Longer explanation |
| `tags` | string[] | — | Discoverability tags |
| `authors` | object[] | — | Name, org, url |
| `source_url` | uri | — | Canonical GovStack URL |
| `supersedes` | string | — | ID of replaced pattern |
| `changelog` | object[] | — | Version history entries |
| `extensions` | object | — | Custom metadata (namespaced) |

### DataField

A typed piece of data consumed or produced by a step or pattern.

| Field | Type | Required | Description |
|---|---|---|---|
| `id` | string | ✅ | Field identifier (e.g. `payment.status`) |
| `type` | enum | ✅ | `string`, `number`, `boolean`, `date`, `datetime`, `enum`, `object`, `array`, `file`, `credential`, `signature` |
| `label` | string | — | Human-readable name |
| `description` | string | — | Purpose and usage |
| `values` | string[] | — | Allowed values when `type: enum` |
| `required` | boolean | — | Default: `true` |
| `sensitive` | boolean | — | Default: `false`. Triggers privacy handling. |
| `extensions` | object | — | Custom metadata |

### Condition

An explicit boolean expression attached to a flow edge.

| Field | Type | Required | Description |
|---|---|---|---|
| `expression` | string | ✅ | The condition (e.g. `payment.status == success`) |
| `label` | string | — | Human-readable label |
| `syntax` | enum | — | `natural-language` (default), `jsonlogic`, `jexl`, `cel`, `javascript` |

### FlowEdge

A directed transition between two steps in a functional pattern.

| Field | Type | Required | Description |
|---|---|---|---|
| `from` | string | ✅ | Source step ID or `START` |
| `to` | string | ✅ | Target step ID or `END` |
| `condition` | Condition | — | Guard expression for this transition |
| `label` | string | — | Human-readable edge label |
| `notes` | string | — | Implementation notes |

### BuildingBlockRef

A reference to a GovStack Building Block used by the pattern.

| Field | Type | Required | Description |
|---|---|---|---|
| `id` | string | ✅ | BB identifier (e.g. `bb.payment`) |
| `role` | enum | ✅ | `primary`, `supporting`, `optional`, `conditional` |
| `notes` | string | — | How this BB is used in context |

### UXConsideration

A design or usability requirement attached to a pattern.

| Field | Type | Required | Description |
|---|---|---|---|
| `text` | string | ✅ | The requirement |
| `applies_to` | enum[] | — | Channels: `digital`, `assisted`, `offline`, `mobile`, `kiosk`, `low-bandwidth`, `all` |
| `severity` | enum | — | `must`, `should`, `may` (default: `should`) |

### TechnicalNote

A technical requirement or implementation guidance attached to a pattern.

| Field | Type | Required | Description |
|---|---|---|---|
| `text` | string | ✅ | The requirement |
| `category` | enum | — | `security`, `performance`, `integration`, `data`, `audit`, `accessibility`, `general` |
| `severity` | enum | — | `must`, `should`, `may` (default: `should`) |

---

## 7.3 StepPattern-Specific Fields

| Field | Type | Required | Description |
|---|---|---|---|
| `purpose` | string | ✅ | What this step achieves from the user's perspective |
| `use_when` | string[] | — | When to use this step |
| `do_not_use_when` | string[] | — | When not to use this step |
| `inputs` | DataField[] | — | Data this step consumes |
| `outputs` | DataField[] | — | Data this step produces |
| `variants` | object[] | — | Named variants for different contexts |
| `building_blocks` | BuildingBlockRef[] | — | BBs involved |
| `ux_considerations` | UXConsideration[] | — | Design requirements |
| `technical_notes` | TechnicalNote[] | — | Technical requirements |

---

## 7.4 FunctionalPattern-Specific Fields

| Field | Type | Required | Description |
|---|---|---|---|
| `use_when` | string[] | ✅ | Conditions for selecting this pattern |
| `do_not_use_when` | string[] | — | Exclusion conditions |
| `building_blocks` | BuildingBlockRef[] | — | BBs involved at pattern level |
| `related_patterns` | PatternRef[] | — | Commonly combined patterns |
| `steps` | FunctionalPatternStep[] | ✅ | Ordered step list |
| `flow` | FlowEdge[] | ✅ | Directed transition graph |
| `inputs` | DataField[] | — | Data required before the pattern starts |
| `outputs` | DataField[] | — | Data produced on completion |
| `ux_considerations` | UXConsideration[] | — | Design requirements |
| `technical_notes` | TechnicalNote[] | — | Technical requirements |
