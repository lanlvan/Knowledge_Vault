---
project: bomcase
type: prompt
status: active
version: v0.1
role: pending_update_loop
governance_basis: BOM-D008
updated: 2026-06-29
---

# BOMCASE Pending Update Loop

## 1. Prompt Purpose

This prompt is used to process confirmed results for existing BOMCASE pending IDs.

It handles the governance loop:

```text
pending ID confirmation result
-> close / keep / rewrite / merge / derived candidate
-> update source / page brief / global-navigation / project-brief / decisions when needed
-> update pending.md
-> local consistency check for this update
```

Use this prompt when a user provides confirmation results for one or more existing entries in:

```text
projects/bomcase/pending.md
```

This prompt is not used to generate Delivery Output.

This prompt is active for existing pending ID confirmation closure.

---

## Execution Stages

Pending closure must follow four stages by default:

1. Pre-check:
   verify the pending ID exists, read related fact files, and check whether the confirmation result is sufficient.

2. Write Plan:
   decide close / keep / rewrite / merge, list target files, and state the intended write-back.

3. Apply Patch:
   after the write plan is safe, apply minimal patches to `pending.md` and any affected knowledge files.

4. Post-check:
   run the local consistency check for pending status, source / page brief sync, decisions, project brief, and derived candidates.

Do not modify multiple files directly from a short confirmation sentence without first outputting the write plan.

---

## 2. Relation to Existing Prompts

| Prompt | Relationship |
|---|---|
| `page-fact-update-loop.md` | Processes unrouted incremental fact material for an existing page. It may write source / page brief, but its trigger is page fact update material, not pending ID confirmation. |
| `pending-update-loop.md` | Processes pending ID confirmation results and performs the multi-file closure loop. It may write source when the confirmed result affects detailed page facts. |
| `stage-check.md` | Performs read-only global structure and governance checks. This prompt only performs local consistency checks for the current pending update and does not replace `stage-check.md`. |
| `page-fact-layer-bootstrap.md` | Initializes or reconstructs a page fact layer from raw materials. This prompt does not initialize new pages or create source/brief pairs from raw material. |
| `delivery-output-handoff.md` | Generates delivery handoff output after facts are updated. This prompt must run before Delivery Output when pending confirmation changes the knowledge layer. |

Boundary with `page-fact-update-loop.md` is based on trigger source, not file type:

```text
page-fact-update-loop.md:
User provides unrouted existing page fact update material -> route source / page brief writes and output candidates by default.

pending-update-loop.md:
User provides pending ID confirmation result -> close / keep / rewrite / merge pending and update related knowledge files.
```

Both prompts may write `sources/*.md` and `pages/*.md`, but they serve different workflows.

---

## 3. Core Principle

`pending.md` is the only pending pool.

Rules:

* `pending.md` is the single source of unresolved product questions.
* Page briefs may mention pending awareness, but pending items in page briefs must stay aligned with `pending.md`.
* `global-navigation.md` records confirmed navigation facts only. It must not maintain pending items.
* `decisions.md` records stable project-level judgments only. It must not record pending IDs or single-page implementation details.
* `pending.md` is not a changelog.
* Confirmed pending results must be removed, rewritten, merged, or retained according to the current confirmation result.

---

## 4. Input Format

The user must provide pending confirmation results using this format:

```text
Current task: Use pending-update-loop to process pending confirmation results.

Pending IDs:
- <ID>

Confirmation results:
- <ID>: <confirmed result / still pending / rewrite / merge target / invalid / derived issue>

Confirmation source:
- <source of confirmation>

Impact scope:
- source:
- page brief:
- global-navigation:
- project-brief:
- decisions:

Boundary notes:
-
```

If the confirmation result is incomplete, report the missing information in the write plan and do not proceed to patch.

Do not infer confirmation from old output, draft output, archive, screenshots, examples, or unstated assumptions.

---

## 5. Processing Steps

### Step 1: Read `pending.md`

Read:

```text
projects/bomcase/pending.md
```

Identify the current pending entry, section, severity, source files, current impact, and pending product question.

### Step 2: Verify Pending ID

Check whether each provided pending ID exists.

If an ID does not exist:

* do not create it automatically;
* report it as missing;
* ask the user to confirm whether it is a new pending candidate.

### Step 3: Classify Action

For each existing pending ID, classify the action:

| Action | Meaning |
|---|---|
| close | Confirmation resolves the pending item. Remove it from `pending.md` after writing confirmed facts where needed. |
| keep | Confirmation is insufficient. Keep the pending item unchanged or with a clarified wording. |
| rewrite | Pending remains valid but wording, source, impact, or question needs correction. |
| merge | Multiple pending items describe the same unresolved issue. Keep the earliest ID and merge content. |
| derived candidate | Confirmation exposes a new unresolved issue. Output as candidate only; do not write automatically. |

### Step 4: Read Target Write Files

Read only the files required by the classified action.

Allowed target files:

```text
projects/bomcase/sources/*.md
projects/bomcase/pages/*.md
projects/bomcase/global-navigation.md
projects/bomcase/pending.md
projects/bomcase/project-brief.md
projects/bomcase/decisions.md
```

Do not read old output, draft output, archive, unrelated page source, or superseded source as fact sources.

### Step 5: Output Write Plan First

Before modifying anything, output a write plan.

The write plan must list:

* files to update;
* reason for each update;
* pending action per ID;
* confirmed facts to write;
* pending items to remove, keep, rewrite, or merge;
* derived pending candidates, if any;
* decisions upgrade recommendation, if any;
* local consistency checks to run.

Do not modify files during this step.

### Step 5.5: Governance Context Check Before Patch

In Patch Stage, before outputting the minimal patch, perform a read-only Governance Context Check.

Read and summarize the current project governance constraints from:

```text
projects/bomcase/pending.md
projects/bomcase/decisions.md
projects/bomcase/project-brief.md
projects/bomcase/prompts/README.md
```

Also read the target source / page brief / global files named in the confirmed write plan, including relevant global files such as:

```text
projects/bomcase/global-navigation.md
```

The Governance Context Check must judge:

* current fact source relationship;
* whether pending items are centrally managed in `pending.md`;
* whether page briefs reference global files where project governance requires it, instead of duplicating global facts;
* whether `decisions.md` contains constraints affecting this patch;
* whether `project-brief.md` needs synchronization for pending overview, current priority focus, or project status summary;
* if target source contains `section_layer` / `layer_note`, whether pending confirmation affects annotated sections;
* how F / F+E / A:view / Unknown affects pending confirmation reliability;
* whether `## 9. Pending Boundary` needs a `layer_note` update;
* whether closed, missing, or stale pending IDs are retained only as Maintenance Log history and not as active pending boundary;
* this patch's write boundary.

This check is read-only and must not replace `stage-check.md`.

### Step 6: After User Confirmation, Output Minimal Patch

Only after the user confirms the write plan, output or apply the minimal patch.

The patch must be scoped to the confirmed update.

Do not rewrite full files.

### Step 7: Local Consistency Check

After the patch is applied, check only this update's local consistency:

* resolved pending IDs are no longer active pending entries;
* retained pending IDs still reflect unresolved questions;
* page brief pending awareness matches `pending.md`;
* source does not contain unconfirmed facts;
* `global-navigation.md` contains only confirmed navigation facts;
* `project-brief.md` pending summary is current if it was affected;
* `decisions.md` was updated only if upgrade criteria were met;
* affected source `section_layer` / `layer_note` still matches the updated pending state;
* `## 9. Pending Boundary` does not retain closed or missing pending as active;
* `A:view` was not used alone for pending closure;
* `Unknown` did not drive closure without explicit human confirmation;
* no derived pending candidate was written without user confirmation.

This local check does not replace `stage-check.md`.

---

## 6. Write Target Rules

When the same confirmation affects both source and page brief, update the active source first, then update the page brief as a compressed reading layer.

### `sources/*.md`

Write to source when the confirmation changes detailed page facts, fields, states, interactions, copy, rules, acceptance criteria, or pending boundary.

Do not write unresolved or partial confirmation as fact.

### `pages/*.md`

Write to page brief when the confirmation changes page summary, pending awareness, decision boundary, or current page reading boundary.

Page brief remains a compressed view and does not replace source.

### `global-navigation.md`

Write only confirmed navigation facts.

Do not add pending questions, pending IDs, design todos, route guesses, or unresolved behavior.

### `pending.md`

Update `pending.md` for close, keep, rewrite, merge, severity change, and confirmed new pending entries.

Do not use `pending.md` as changelog.

### `project-brief.md`

Update only when the change affects:

* pending overview;
* current priority focus;
* project status summary.

Do not update `project-brief.md` for every single pending closure if the project-level summary is unchanged.

### `decisions.md`

Update only when the confirmed result meets the Decisions Upgrade Rules.

Do not add pending IDs or single-page details to `decisions.md`.

## 6.5 v0.3 Information Layer Check for Pending Closure

These rules protect the v0.3 information-layer governance result while preserving this prompt's role as the pending closure loop.

* Pending closure should be supported first by F content or by the F portion of an F+E section.
* E-only content may confirm user-visible wording, but it generally cannot close structure or rule pending items by itself.
* `A:view` cannot be the main fact source for closing, rewriting, or merging pending items.
* `Unknown` can affect pending closure only after explicit human confirmation.
* After a pending ID is closed, merged, rewritten, or judged missing, source Pending Boundary must not keep it as active pending.
* Closed or stale IDs may remain only as Maintenance Log history, not as active pending boundary.
* Page brief Pending Awareness must stay synchronized with `pending.md`.

---

## 7. Decisions Upgrade Rules

Recommend adding a new `BOM-Dxxx` decision only when all conditions are met:

1. The confirmed result applies across pages or modules.
2. The confirmed result is expected to remain valid long term.
3. The confirmed result concerns governance method, boundary judgment, or global product boundary.
4. The confirmed result affects future handling of multiple pages, multiple prompts, or multiple pending items.

Do not add to `decisions.md` when the result is only:

* a single-page concrete rule;
* a specific number;
* a specific user-facing copy;
* a specific UI expression;
* a one-time implementation detail;
* a pending ID closure note;
* a design, testing, schedule, or engineering task.

When in doubt, keep the confirmed fact in source / page brief and do not upgrade to decisions.

---

## 8. Derived Pending Candidate Rules

If a confirmation result exposes a new unresolved issue:

* output it as a pending candidate only;
* do not write it into `pending.md`;
* do not assign a final pending ID unless the user confirms creation;
* do not write it as a confirmed fact in source, page brief, global-navigation, project-brief, or decisions.

Candidate format:

```markdown
## Derived Pending Candidates

| Candidate | Suggested Prefix | Source | Why It Is Pending | Suggested Severity |
|---|---|---|---|---|
|  |  |  |  |  |
```

---

## 9. Pending Numbering Rules

General rules:

* Closed IDs are not reused.
* New entries use the next unused number for that prefix and severity.
* Split entries receive new IDs. Do not use `<original>-1` or `<original>-2`.
* When merging multiple entries, keep the earliest ID and state where the other IDs were merged in the write plan.
* If severity changes, keep the original numeric ID and update the severity field / heading as needed.
* Do not renumber existing pending entries for cosmetic ordering.

Prefix rules:

| Prefix | Scope |
|---|---|
| `NAV` | Global navigation |
| `HOME` | Home |
| `SHOP` | Shop |
| `OB` | Open Box |
| `OBR` | Open Box Result |
| `TC` | Toy Collection |

Severity format:

```text
<PREFIX>-A001
<PREFIX>-B001
```

Use A for blockers and B for non-blocking product expression, acceptance, or knowledge consistency issues.

---

## 10. Output Format

### Write Plan Format

```markdown
# Pending Update Write Plan

## 1. Pending IDs

| ID | Exists | Current Section | Action | Reason |
|---|---|---|---|---|
|  |  |  |  |  |

## 2. Files To Read

-

## 3. Files To Update

| File | Update Type | Reason |
|---|---|---|
|  |  |  |

## 4. Confirmed Facts To Write

| Fact | Target File | Target Section |
|---|---|---|
|  |  |  |

## 5. Pending Changes

| ID | Change |
|---|---|
|  |  |

## 6. Decision Upgrade Check

Result:

Reason:

## 7. Derived Pending Candidates

| Candidate | Write Now? | Reason |
|---|---|---|
|  | No | Requires user confirmation. |

## 8. Local Consistency Check Plan

-
```

### Patch Format

```markdown
# Pending Update Patch

## 0. Governance Context Check

| Check | Result |
|---|---|
| current fact source relationship |  |
| pending is centrally managed in `pending.md` |  |
| page briefs reference global files where required |  |
| decisions constraints checked |  |
| project-brief synchronization need checked |  |
| patch write boundary confirmed |  |

## File: <path>

Operation:
Location:
Original:
New Markdown:
```

### Final Check Format

```markdown
# Pending Update Local Check

## 1. Files Updated

-

## 2. Pending Result

- Closed:
- Kept:
- Rewritten:
- Merged:
- Candidates only:

## 3. Knowledge Layer Check

| Check | Result |
|---|---|
| pending.md remains the only pending pool |  |
| page brief aligns with pending.md |  |
| source contains only confirmed facts |  |
| global-navigation contains no pending |  |
| project-brief updated only if needed |  |
| decisions updated only if threshold met |  |

## 4. Stage Check Boundary

This was a local consistency check only. It does not replace `stage-check.md`.
```

---

## 11. Prohibited Actions

Do not:

* directly modify files before a write plan is confirmed;
* rewrite full files when a small patch is enough;
* write pending or partial confirmation as confirmed fact;
* use `pending.md` as changelog;
* treat page brief as source;
* treat sample data, screenshots, or example states as fixed rules;
* write UI styling, animation details, testing tasks, development tasks, schedules, or pure design todos into pending;
* automatically create derived pending entries;
* add pending IDs or single-page details to `decisions.md`;
* maintain pending items in `global-navigation.md`;
* use old output, draft output, archive, or superseded source as current fact source;
* replace `stage-check.md` global read-only validation with this prompt's local check.

---

## 12. Standard Invocation Templates

Use these templates to run `pending-update-loop.md` in controlled stages.

Each execution must declare its mode.

Do not process pending IDs outside the declared scope.

Do not automatically create derived pending entries.

Do not commit git changes unless the user explicitly asks.

### 12.1 Plan Stage Template

Use this stage to read current files, classify pending actions, and output a write plan.

This stage must not modify files.

This stage must not output a patch.

```text
Current task:
Use `projects/bomcase/prompts/pending-update-loop.md` in Plan Stage.

Execution mode:
Plan only. Read, classify, and output write plan. Do not modify files. Do not output patch. Do not commit git.

Pending IDs to process:
-

Product confirmation result:
-

Confirmation source:
-

Scope limits:
- Only process the pending IDs listed above.
- Do not process other pending items.
- Do not automatically add derived pending items.
- If derived pending is found, output candidate only.

Required reading:
- `projects/bomcase/pending.md`
- Related page brief, active source, global-navigation, project-brief, or decisions only if needed for the listed pending IDs.

Required output:
- Pending Update Write Plan
- Missing information, if any
- Derived pending candidates, if any
- Decision upgrade check
- Local consistency check plan
```

### 12.2 Patch Stage Template

Use this stage after the user has confirmed a write plan.

This stage must re-check the current files before producing the patch.

This stage must output the smallest patch needed.

This stage must not modify files.

```text
Current task:
Use `projects/bomcase/prompts/pending-update-loop.md` in Patch Stage.

Execution mode:
Patch only. Re-check current files and output minimal patch. Do not modify files. Do not commit git.

Confirmed write plan:
-

Pending IDs to process:
-

Product confirmation result:
-

Scope limits:
- Only patch files required by the confirmed write plan.
- Do not process other pending items.
- Do not automatically add derived pending items.
- If derived pending is confirmed for creation, user must explicitly say so.

Required reading:
- `projects/bomcase/pending.md`
- Target source / page brief / global files named in the confirmed write plan
- `projects/bomcase/decisions.md`
- `projects/bomcase/project-brief.md`
- `projects/bomcase/prompts/README.md`
- Relevant global files for the pending scope, for example `projects/bomcase/global-navigation.md`

Required output:
- `## 0. Governance Context Check`
- Minimal patch
- Files included in patch
- Files intentionally not changed
- Local consistency checks to run after apply
```

### 12.3 Apply and Validate Stage Template

Use this stage only after the user has approved a specific patch.

This stage may apply the approved patch.

After applying, run the local consistency check for this pending update only.

This stage does not replace `stage-check.md`.

```text
Current task:
Use `projects/bomcase/prompts/pending-update-loop.md` in Apply and Validate Stage.

Execution mode:
Apply approved patch and validate locally. Do not commit git.

Approved patch:
-

Pending IDs to process:
-

Product confirmation result:
-

Scope limits:
- Apply only the approved patch.
- Do not process other pending items.
- Do not automatically add derived pending items.
- Do not run global stage-check unless separately requested.
- Do not commit git.

Required validation:
- List modified files.
- Confirm pending changes: closed / kept / rewritten / merged / candidates only.
- Confirm source updates, if any.
- Confirm page brief updates, if any.
- Confirm global-navigation updates, if any.
- Confirm project-brief updates, if any.
- Confirm decisions updates, if any.
- Confirm derived pending was not written without explicit user confirmation.
- Confirm whether the updated files are ready to commit.
```
