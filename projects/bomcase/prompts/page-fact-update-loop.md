---
project: bomcase
type: prompt
status: active
version: v0.1
role: page_fact_update_loop
updated: 2026-06-30
migration_note: merged legacy source-only and brief-only prompt rules into this unified page fact update loop
---

# Page Fact Update Loop

## 1. Purpose

This prompt is the user-facing active prompt for incremental fact updates to existing BOMCASE pages.

It receives unrouted page material and decides how the current page fact layer should be updated:

```text
unrouted page material
-> read current page fact layer
-> classify input
-> route to source / page brief / candidates / not written
-> output write plan
-> output minimal patch
-> local consistency check
```

This prompt is used only for existing pages that already have a current source and page brief.

It is not used for:

* new page initialization;
* page fact-layer reconstruction from raw material;
* pending ID closure;
* Delivery Output generation;
* cross-page bulk restructuring;
* project-level governance rule deposition.

Use these prompts instead when the task matches their scope:

| Task | Prompt |
|---|---|
| New page initialization / page fact-layer reconstruction | `projects/bomcase/prompts/page-fact-layer-bootstrap.md` |
| Existing pending ID confirmation closure | `projects/bomcase/prompts/pending-update-loop.md` |
| Delivery handoff document generation | `projects/bomcase/prompts/delivery-output-handoff.md` |

---

## Execution Stages

Existing page fact updates must follow four stages by default:

1. Pre-check / read-only validation:
   read the current fact layer and classify the input before any patch.

2. Write Plan:
   output the target source writes, page brief writes, pending candidates, decision candidates, and not-written items before patching.

3. Apply Patch:
   only execute a minimal patch when the write plan is safe.

4. Post-check:
   run Local Consistency Check after patching.

If pre-check or write plan fails, output missing information / Not Written / Conflicts and do not patch.

---

## 2. Input Contract

The input is unrouted page material.

The user does not need to decide the target file before running this prompt.

The user does not need to provide a Fact Patch.

Accepted input may include:

* newly confirmed product wording;
* page state expression;
* page fact supplement;
* confirmed explanation;
* page rule correction;
* local correction to an existing fact;
* a prepared Fact Patch;
* notes that may contain confirmed facts, conflicts, gaps, or suggestions.

The task command should provide as much of the following as available:

```text
Page name:
Page display name:
Input material:
Confirmation status:
Confirmation source:
Business fact updated date:
Boundary notes:
Optional target source:
Optional target page brief:
Optional declared mode:
```

Supported internal execution modes include:

* `source-only`;
* `source-and-brief`;
* `brief-only`;
* `patch-only`;
* `candidate-only`;
* `not-written-only`.

If the user declares `source-only`, `brief-only`, `source-and-brief`, or `patch-only`, follow the declared mode if it does not violate fact-layer governance.

If the user does not declare a mode, this prompt must classify the input and route it based on the current fact layer.

If the user provides a Fact Patch, process it as a compatible input format, not as the only valid format.

If the page cannot be identified, if the confirmation status is unclear, or if the current source / page brief relationship is broken, output a write plan with missing information and do not patch.

---

## 3. Required Reading

Before routing or patching, read:

```text
projects/bomcase/prompts/README.md
projects/bomcase/project-brief.md
projects/bomcase/sources/<target-page>.md
projects/bomcase/pages/<target-page>.md
projects/bomcase/pending.md
projects/bomcase/decisions.md
```

When the target page is not explicit, use `project-brief.md` and the input material to identify exactly one likely page. If more than one page may be affected, stop and output a routing ambiguity report.

Forbidden as current fact sources:

```text
outputs/**
archive/**
old outputs
draft outputs
unrelated page source/page files
historical versions
superseded sources
README / index as business facts
```

Historical versions, old outputs, archived materials, or unrelated files may be read only when the user explicitly marks them as this task's input material. Even then, they remain input material to classify, not automatic current facts.

---

## 4. Routing Rules

Classify each input item into one of these categories:

| Category | Meaning | Default route |
|---|---|---|
| confirmed page fact | Confirmed, page-related fact with enough detail | source |
| source-level detail | Detailed fields, states, interactions, copy, rules, acceptance criteria, or pending boundary | source |
| page brief summary | Summary-level reading layer affected by current source changes | page brief |
| pending candidate | Unconfirmed, conflicting, missing, partial, suggested, or inferred item | report only |
| decision candidate | Stable, cross-page, project-level, reusable judgment | report only |
| out-of-scope item | Not part of the current page fact layer | not written |
| conflict / not written item | Cannot be safely written because it conflicts with current source or lacks support | not written |

Rules:

* Confirmed, page-related, sufficiently detailed facts go into the active source.
* Source changes that affect page reading summary must be reflected in the page brief.
* Unconfirmed, conflicting, missing, partial, or suggested material must not be written as confirmed fact.
* Unconfirmed, conflicting, missing, partial, or suggested material may be output as pending candidate or Not Written / Conflicts.
* Stable, cross-page, project-level, reusable judgments may be output as decision candidates.
* Single-page concrete rules do not upgrade to `decisions.md` by default.
* Pending ID confirmation closure must route to `pending-update-loop.md`.
* New page raw material initialization or page fact-layer reconstruction must route to `page-fact-layer-bootstrap.md`.
* Delivery handoff generation must route to `delivery-output-handoff.md`.

---

## 5. Write Order

When patching is safe, use this order:

1. Update source first.
2. Update page brief second.
3. Output pending candidates in the report only by default.
4. Output decision candidates in the report only by default.

If source and page brief are both affected, the page brief must be derived from the updated source state, not from the user's raw wording alone.

---

## 6. Source Update Rules

The active source is the detailed fact carrier.

Write to source when the input changes:

* detailed page facts;
* page goal or structure;
* modules;
* fields;
* display rules;
* state rules;
* interaction rules;
* user-facing copy;
* info / hover copy;
* button copy;
* empty or abnormal states;
* acceptance criteria;
* pending boundary;
* non-goals.

Rules:

* Write only confirmed, explicit, target-page-related facts.
* Do not expand facts beyond the input and current confirmed fact layer.
* Do not infer missing product rules.
* If input conflicts with current source, do not overwrite it automatically; list it in Not Written / Conflicts.
* Empty, unconfirmed, partial, or suggested content must not be written as confirmed fact.
* Visual implementation details must be rewritten into product expression constraints unless explicitly marked as design hard constraints.
* Source is a detailed fact carrier, not a Delivery Output document.
* Do not write source sections in handoff document language.

Visual expression rewrite examples:

| Input type | Source-safe wording |
|---|---|
| fixed color | State must be visually distinguishable; final color follows the design draft. |
| fixed icon style | State or action must have a clear identifier; final icon style follows the design draft. |
| fixed animation | State must be distinguishable from normal state; final motion follows the design draft. |

Maintenance Log rules:

* If the target source already has `Maintenance Log` or a similar maintenance section, append to that section.
* If the target source has no maintenance section, decide whether to add `## Maintenance Log` based on the current source structure and the active source schema.
* Maintenance Log records only fact-layer maintenance summary.
* Maintenance Log must not contain Delivery Output wording.
* Maintenance Log must not expand into a detailed change table.
* Log format:

```text
YYYY-MM-DD | type | summary
```

Recommended maintenance types:

```text
confirmed_fact_add
confirmed_fact_fix
confirmed_fact_remove
expression_cleanup
supplement_add
pending_candidate
brief_sync
```

---

## 7. Page Brief Update Rules

The page brief is a compressed reading layer. It does not replace the active source.

Write to page brief when the input or source update changes:

* page objective summary;
* page structure summary;
* key product logic summary;
* pending awareness;
* decision boundary;
* non-goals / not covered scope;
* maintenance notes;
* current page reading boundary.

Rules:

* Page brief must clearly declare `active_source`.
* Page brief must not add facts that are not confirmed in source.
* Page brief must not copy a full detailed source.
* Page brief must not copy historical rule file structure.
* Page brief must not automatically backfill old material.
* Page brief must not treat `pending.md` as a fact source.
* Page brief must not treat `decisions.md` as a page fact source.
* Page brief may mark pending awareness, aligned with `pending.md`.
* Page brief may mark decision boundary, aligned with `decisions.md`.
* Page brief may mark non-goals / not covered scope.
* Keep the update scoped to one page.
* Do not generate Delivery Output inside the page brief.

If a user asks only to create or refresh a brief from an existing active source, this prompt may run in `brief-only` mode after verifying the active source relationship.

---

## 8. Pending Candidate Rules

By default, this prompt does not modify:

```text
projects/bomcase/pending.md
```

Rules:

* Do not automatically create pending IDs.
* Do not write unconfirmed material into `pending.md`.
* Do not treat `pending.md` as a fact database.
* Unconfirmed, missing, conflicting, partial, suggested, or inferred items are output as pending candidates only.
* Pending awareness in page brief must align with current `pending.md`.
* If the user asks to write, close, rewrite, merge, or confirm an existing pending ID, route the task to `pending-update-loop.md`.
* If the user explicitly wants to enter pending writing stage, instruct the user to run or explicitly invoke `pending-update-loop.md`.

Pending candidate format:

```markdown
| Candidate | Source Input | Why Pending | Suggested Scope | Suggested Severity |
|---|---|---|---|---|
|  |  |  |  |  |
```

---

## 9. Decision Candidate Rules

By default, this prompt does not modify:

```text
projects/bomcase/decisions.md
```

Rules:

* Do not automatically create decisions.
* Do not treat `decisions.md` as a page fact database.
* Single-page concrete facts, wording, state rules, or implementation details do not upgrade to decisions by default.
* Output a decision candidate only when the judgment is stable, cross-page, project-level, reusable, and supported by the input.
* Do not convert unresolved issues into decisions.
* Do not write pending IDs or single-page details into `decisions.md`.

Decision candidate format:

```markdown
| Candidate | Why Project-Level | Supported By | Reuse Scope | Write Now |
|---|---|---|---|---|
|  |  |  |  | No |
```

---

## 10. Forbidden Actions

Do not:

* generate Delivery Output;
* modify `outputs/**`;
* modify `archive/**`;
* modify prompts unless the current task explicitly maintains prompts;
* spread across pages;
* read old outputs to infer current facts;
* treat page brief as source;
* treat `pending.md` as a fact database;
* treat `decisions.md` as a page fact database;
* write unconfirmed content as fact;
* write UI suggestions as development tasks;
* expand interface rules;
* expand analytics / tracking rules;
* expand test cases;
* expand schedule or delivery planning;
* replace `page-fact-layer-bootstrap.md`;
* replace `pending-update-loop.md`;
* replace `delivery-output-handoff.md`;
* write delivery-document wording into source or page brief;
* use archive, old output, draft output, or unrelated page files as current fact sources.

---

## 11. Patch Rules

Patch rules:

* Output a minimal patch.
* Do not rewrite full files.
* Preserve existing file structure.
* Preserve existing section order unless the current structure is broken and the fix is explicitly in scope.
* Modify only content directly supported by the input material and current confirmed fact layer.
* Put conflicts in Not Written / Conflicts.
* When source and brief both change, patch source first and brief second.
* Do not patch if the target page is ambiguous.
* Do not patch if confirmation is insufficient.
* Do not patch if current source / brief dependency is broken.
* If safe writing is not possible, output a patch plan and stop.

Patch output must identify:

```text
File:
Operation:
Location:
Original:
New Markdown:
Reason:
```

---

## 12. Local Consistency Check

After producing or applying a patch, check:

| Check | Required result |
|---|---|
| one target page only | Only one page was processed. |
| source active status | Source remains `type: source` and `status: active` where frontmatter exists. |
| source role | Source remains the detailed fact carrier. |
| page brief active source | Page brief points to one active source. |
| page brief fact boundary | Page brief did not add facts outside source. |
| pending awareness | Pending awareness matches current `pending.md`. |
| decisions boundary | Decisions were not given single-page details. |
| Maintenance Log | Source log was appended when source changed. |
| forbidden sources | No forbidden fact sources were read. |
| output boundary | No `outputs/**` or `archive/**` files were modified. |
| prompt boundary | This prompt did not replace bootstrap, pending update, or delivery output workflows. |

This is a local consistency check for the current update. It does not replace `stage-check.md`.

---

## 13. Output Format

Use this report format:

```markdown
# Page Fact Update Report

## 1. Read Summary

| File | Purpose | Read? |
|---|---|---|
|  |  |  |

## 2. Input Classification

| Input Item | Classification | Confirmation Status | Reason |
|---|---|---|---|
|  |  |  |  |

## 3. Routing Result

| Input Item | Route | Target | Reason |
|---|---|---|---|
|  |  |  |  |

## 4. Write Plan

| File | Update Type | Reason | Safe To Patch? |
|---|---|---|---|
|  |  |  |  |

## 5. Patch Diff

### File: <path>

Operation:

Location:

Original:

New Markdown:

Reason:

## 6. Source Writes

| Fact | Target Section | Write Type |
|---|---|---|
|  |  |  |

## 7. Page Brief Writes

| Summary | Target Section | Source Support |
|---|---|---|
|  |  |  |

## 8. Not Written / Conflicts

| Item | Reason | Next Step |
|---|---|---|
|  |  |  |

## 9. Pending Candidates

| Candidate | Source Input | Why Pending | Suggested Scope | Suggested Severity |
|---|---|---|---|---|
|  |  |  |  |  |

## 10. Decision Candidates

| Candidate | Why Project-Level | Supported By | Reuse Scope | Write Now |
|---|---|---|---|---|
|  |  |  |  | No |

## 11. Maintenance Log

State whether a log entry is required and provide the exact log line.

## 12. Boundary Check

| Check | Result |
|---|---|
| one target page only |  |
| source remains active source |  |
| page brief points to unique active_source |  |
| page brief did not add source-external facts |  |
| pending awareness aligned with pending.md |  |
| decisions not used for single-page details |  |
| forbidden fact sources not read |  |
| outputs / archive not modified |  |
| bootstrap / pending-update / delivery-output not replaced |  |

## 13. Final Status

State one of:

* Patch ready for user confirmation.
* Patch applied and locally checked.
* Candidate-only; no patch produced.
* Not safe to patch; missing information listed.
* Routed to another prompt.
```
