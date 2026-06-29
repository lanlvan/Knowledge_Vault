---
project: bomcase
type: prompt
status: active
version: v0.1
role: page_fact_layer_bootstrap
schema_basis: source-brief-object-spec.md v0.2
updated: 2026-06-28
---

# Page Fact Layer Bootstrap Prompt

## 1. Prompt Purpose

This prompt is used to initialize a BOMCASE page fact layer from raw page materials.

It converts raw page material into the standard BOMCASE knowledge structure:

```text
raw page material
→ active source
→ page brief
→ pending candidates
→ decision candidates
→ bootstrap report
```

This prompt does not generate Delivery Output.

Delivery Output is handled only by:

```text
projects/bomcase/prompts/delivery-output-handoff.md
```

This prompt is intended for new page intake or page fact-layer reconstruction, such as introducing a new page like Card Gallery into BOMCASE.

---

## 2. Relationship with Existing Prompts

This prompt has a distinct responsibility from existing prompts:

| Prompt                         | Responsibility                                                                              |
| ------------------------------ | ------------------------------------------------------------------------------------------- |
| `page-fact-layer-bootstrap.md` | Initializes a complete page fact layer from raw materials: source + page brief + candidates |
| `page-fact-update-loop.md`     | Incrementally updates an existing page fact layer from unrouted page material               |
| `pending-update-loop.md`       | Processes existing pending ID confirmation results and the pending closure loop             |
| `delivery-output-handoff.md`   | Generates delivery handoff output based on page brief + active source + pending + decisions |
| `stage-check.md`               | Performs read-only project structure and governance checks                                  |

This prompt must not replace `page-fact-update-loop.md`, `pending-update-loop.md`, or `delivery-output-handoff.md`.

Use `page-fact-update-loop.md` for daily incremental updates to an already existing page fact layer.

Keep this prompt focused on new page initialization or page fact-layer reconstruction from raw material.

---

## 3. Core Governance Model

BOMCASE page delivery is based on the following chain:

```text
page brief + active source + pending + decisions
        ↓
Delivery Output
```

Layer responsibilities:

| Layer                        | Role                                   | Delivery Output Dependency        |
| ---------------------------- | -------------------------------------- | --------------------------------- |
| `sources/<page>.md`          | Current detailed fact source           | Required                          |
| `pages/<page>.md`            | Page fact brief / compressed page view | Required                          |
| `pending.md`                 | Current unresolved issue pool          | Required for delivery             |
| `decisions.md`               | Confirmed project-level decisions      | Required for delivery             |
| `outputs/**`                 | Delivery results / drafts              | Never used as fact source         |
| README / index               | Navigation only                        | Never used as fact source         |
| archived / superseded source | Historical trace only                  | Never used as current fact source |

---

## Execution Stages

Bootstrap / reconstruction must not start by directly creating or updating files.

Use four stages by default:

1. Pre-check / read-only validation:
   - read raw material paths;
   - verify target source and page brief paths;
   - verify schema authority;
   - check forbidden fact sources;
   - check whether raw material is sufficient;
   - check whether existing page facts may be overwritten or reconstructed.

2. Write Plan:
   - output whether the task is initial creation or reconstruction;
   - list target files;
   - list proposed source sections;
   - list proposed page brief sections;
   - list pending candidates;
   - list decision candidates;
   - list Fact Gaps;
   - state whether it is safe to write.

3. Apply Patch:
   - create or update only allowed files;
   - use minimal patch when updating existing files;
   - do not overwrite existing fact layers unless reconstruction is explicitly in scope;
   - do not invent missing facts.

4. Post-check:
   - run Delivery Readiness Criteria;
   - verify active source frontmatter;
   - verify page brief `active_source`;
   - verify pending / decision candidates are separated from confirmed facts;
   - verify no Delivery Output was generated.

If pre-check or write plan fails, output a Fact Gap Report or Bootstrap Write Plan and do not create / update source or page brief.

---

## 4. Schema Authority

The structure of generated source and page brief files must follow:

```text
projects/bomcase/specs/source-brief-object-spec.md
```

Current schema authority:

```text
Source / Brief Object Spec v0.2
```

Spec v0.2 has locked the current required structures:

* active source: 11 top-level sections;
* page brief: 8 top-level sections.

This prompt must follow spec v0.2.

If `source-brief-object-spec.md` is upgraded in the future, this prompt must be reviewed and updated accordingly.

---

## 5. Allowed Inputs

The task command must explicitly provide:

```text
Page name:
Page display name:
Raw material path(s):
Target source path:
Target page brief path:
Target bootstrap report path:
Business fact updated date:
Source type:
Bootstrap scope:
Confirmation status:
Boundary notes:
```

Allowed raw materials may include:

```text
historical handoff document
PRD draft
UI review notes
confirmed page notes
business brief
existing source fragments
```

Forbidden inputs as fact sources:

```text
outputs/handoff/**
outputs/handoff/_drafts/**
README / index
archived output
old generated delivery documents
unconfirmed AI-generated drafts unless explicitly marked as raw material
```

---

## 6. Output Files

This prompt may create or update only:

```text
projects/bomcase/sources/<page>.md
projects/bomcase/pages/<page>.md
projects/bomcase/outputs/bootstrap/_drafts/<page-name>-fact-layer-bootstrap-report-v0.1.md
```

This prompt must not directly modify:

```text
projects/bomcase/pending.md
projects/bomcase/decisions.md
projects/bomcase/outputs/handoff/**
projects/bomcase/outputs/handoff/_drafts/**
projects/bomcase/prompts/**
```

Pending and decision findings must be output as candidates in the bootstrap report.

They must not be written directly into `pending.md` or `decisions.md`.

The bootstrap report is an output artifact and must not be treated as a fact source.

---

## 7. Active Source Requirements

The generated source must be the current detailed fact carrier.

Required frontmatter:

```yaml
---
project: bomcase
page: <page-name>
type: source
status: active
role: detailed_fact_source
source_type: <handoff_document | consolidated_source>
version: current
updated: <business-fact-updated-date>
source_history:
  - absorbed: <raw-material-name>
    note: Absorbed as current detailed fact source.
---
```

Rules:

* `status: active` means this source is currently effective.
* Do not use `status: confirmed` as the active source status.
* `updated` represents the last substantive business fact update date.
* Metadata migration, path rename, or expression cleanup must be recorded in `Maintenance Log`, not by changing `updated`.
* `source_type` defaults to `handoff_document` when initialized from a single raw material.
* Use `source_type: consolidated_source` only when the source is created by absorbing multiple versions, multiple historical sources, or multiple current fact fragments.
* If confirmation state is needed later, use a separate descriptive field; do not overload `status`.

---

## 8. Active Source Structure

The source must follow `source-brief-object-spec.md` v0.2.

Required top-level structure:

```markdown
# <Page Display Name> Active Source

## 1. Source Scope

## 2. Page Goal

## 3. Structure

## 4. Data / Fields

## 5. States

## 6. Interactions

## 7. Rules

## 8. Acceptance Criteria

## 9. Pending Boundary

## 10. Non-goals

## 11. Maintenance Log
```

The source must preserve enough detail to support future Delivery Output.

The source should include, where applicable:

* page goal;
* page structure;
* modules;
* fields;
* display rules;
* state rules;
* interaction rules;
* copy / info text;
* empty states;
* abnormal states;
* acceptance criteria;
* pending boundary;
* non-goals;
* source history;
* maintenance log.

Do not write the source as a delivery handoff document.

---

## 9. Page Brief Requirements

The generated page brief is a compressed view, not a detailed source.

Required frontmatter:

```yaml
---
project: bomcase
type: page_brief
status: current
knowledge_role: handoff-brief
active_source: ../sources/<page>.md
updated: <business-fact-updated-date>
---
```

Rules:

* `knowledge_role` defaults to `handoff-brief` for new page intake.
* Use `fact-brief` only after the page brief has matured into a stable fact brief with clear fact boundaries and a stable active source.
* Always use `active_source`.
* Do not use legacy `source` or `additional_source`.
* Do not duplicate the full source.
* Do not generate Delivery Output inside the page brief.

---

## 10. Page Brief Structure

The page brief must follow `source-brief-object-spec.md` v0.2.

Required top-level structure:

```markdown
# <Page Display Name> Page Brief

## 1. Source Policy

## 2. Page Objective

## 3. Page Structure Summary

## 4. Key Product Logic

## 5. Pending Awareness

## 6. Decision Boundary

## 7. Non-goals

## 8. Maintenance Notes
```

The page brief must remain a compressed view.

It should summarize:

* where the active source is;
* what the page objective is;
* the high-level page structure;
* key product logic;
* pending awareness;
* decision boundary;
* non-goals;
* maintenance notes.

---

## 11. Pending Candidate Rules

This prompt must not modify `pending.md`.

When raw material contains uncertainty, conflict, missing detail, or unresolved implementation boundary, classify it as a pending candidate in the bootstrap report.

Types:

| Type                         | Meaning                                 | Action                   |
| ---------------------------- | --------------------------------------- | ------------------------ |
| Existing Pending             | Already exists in `pending.md`          | Reference only           |
| Source Confirmed Uncertainty | Raw material explicitly says unresolved | Output pending candidate |
| Inferred Pending Candidate   | AI detects likely unresolved issue      | Output as candidate only |
| Delivery-Only Boundary       | Only affects delivery expression        | Do not enter pending     |
| Invalid / Overstated         | Unsupported or excessive                | Remove or downgrade      |

Rules:

* Do not write candidates into `pending.md`.
* Do not create pending IDs automatically.
* Do not write delivery-only boundaries into pending.
* Do not write unsupported inference as confirmed pending.
* Output all candidates in the bootstrap report for human review.

---

## 12. Decision Candidate Rules

This prompt must not modify `decisions.md`.

Decision candidates may be proposed only if they are:

* project-level or cross-page;
* stable;
* reusable;
* supported by raw material;
* not merely page implementation detail;
* not unresolved pending.

Rules:

* Do not write candidates into `decisions.md`.
* Do not create decision IDs automatically.
* Do not duplicate existing decisions.
* Do not convert unresolved issues into decisions.
* Output all candidates in the bootstrap report for human review.

---

## 13. Visual Expression Boundary

Classify visual content into three levels:

| Type                  | Enter Source? | Rule                                |
| --------------------- | ------------- | ----------------------------------- |
| Product Rule          | Yes           | Business/product requirement        |
| Expression Constraint | Yes           | Required product expression outcome |
| Design Implementation | No            | Belongs to UI design/design system  |

Allowed in source:

```text
The selected state must be distinguishable.
The recommended action must have higher visual priority.
The protection marker must not conflict with selected state.
The warning expression must not overpower the primary action.
```

Not allowed as fixed product fact:

```text
specific color
specific icon shape
specific animation
specific shadow
specific border radius
specific spacing
specific glow effect
```

When raw material includes visual implementation details, rewrite them into product expression constraints.

---

## 14. Fact Gap Handling

If raw material is insufficient to create a valid active source, do not invent missing facts.

Output a Fact Gap Report instead of fabricating content.

Fact gaps include:

* missing page goal;
* missing page structure;
* missing field definitions;
* missing state rules;
* missing interaction rules;
* missing acceptance criteria;
* contradictory raw material;
* unclear pending ownership;
* unclear active source target;
* unclear business fact updated date.

If major fact gaps exist, the page is not ready for Delivery Output.

---

## 15. Maintenance Log

Every generated source must include a final section, formatted as:

```markdown
## 11. Maintenance Log
```

This section appears as the 11th and final section of the source file, per spec v0.2.

Initial creation log format:

```text
YYYY-MM-DD | initial_creation | Initialized active source and page brief from raw material. Pending and decision candidates listed separately. No Delivery Output generated.
```

`initial_creation` is introduced only for the `page-fact-layer-bootstrap` workflow.

It is not part of the normal `page-fact-update-loop.md` incremental update workflow.

For later maintenance, use the existing fact patch change types such as:

```text
confirmed_fact_add
confirmed_fact_fix
confirmed_fact_remove
expression_cleanup
supplement_add
pending_candidate
```

---

## 16. Bootstrap Report

After execution, output:

```markdown
# <Page Display Name> Fact Layer Bootstrap Report
```

Required report sections:

```markdown
## 1. Files Read

## 2. Files Created / Updated

## 3. Active Source Result

## 4. Page Brief Result

## 5. Pending Candidates

## 6. Decision Candidates

## 7. Visual Boundary Handling

## 8. Fact Gaps

## 9. Delivery Readiness

## 10. Boundary Check
```

---

## 17. Delivery Readiness Criteria

A page is delivery-ready only if:

```text
pages/<page>.md exists
sources/<page>.md exists
page brief has active_source
active_source file exists
source has type: source
source has status: active
source has role: detailed_fact_source
source has page matching page brief
source follows source-brief-object-spec.md v0.2
page brief follows source-brief-object-spec.md v0.2
pending candidates are separated from confirmed facts
decision candidates are separated from confirmed facts
outputs are not used as fact sources
```

If all pass, report:

```text
Ready for Delivery Output.
```

If not, report:

```text
Not ready for Delivery Output.
```

---

## 18. Boundary Rules

Must not:

* generate Delivery Output;
* modify outputs;
* treat outputs as fact source;
* treat README/index as fact source;
* write unresolved issues as confirmed facts;
* write pending candidates into `pending.md`;
* write decision candidates into `decisions.md`;
* write delivery-only boundaries into pending;
* write page-specific details into project-level decisions;
* hard-code visual implementation as product fact;
* use legacy `source` / `additional_source` in page brief;
* create source without `status: active`;
* create source without `role: detailed_fact_source`;
* bypass `source-brief-object-spec.md` v0.2.

---

# Standard Task Input Template

Use the following input format when running this prompt:

```text
当前任务：使用 `projects/bomcase/prompts/page-fact-layer-bootstrap.md` 从原始页面材料初始化 / 重建页面事实层。

页面名称：
页面展示名称：
原始材料：
目标 source：
目标 page brief：
目标 bootstrap report：
业务事实更新时间：
source_type：
本次范围：
确认状态：
边界说明：
```
