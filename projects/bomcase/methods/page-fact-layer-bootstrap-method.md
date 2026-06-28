# Page Fact Layer Bootstrap Method

---
project: bomcase
type: method
status: draft
version: v0.1
updated: 2026-06-28
---

## 1. Method Purpose

This method records why BOMCASE needs a `page-fact-layer-bootstrap` workflow and how it should be used.

The purpose is to preserve the reasoning behind the prompt, not to replace the prompt itself.

The prompt is the executable tool.  
This method explains the design logic behind the tool.

---

## 2. Background

During BOMCASE Delivery Output governance, the project moved from historical handoff materials toward a controlled fact-chain model:

```text
page brief + active source + pending + decisions
        ↓
Delivery Output
```

Open Box became the first fully closed-loop page.

The governance process established:

* active source as the current detailed fact carrier;
* page brief as the compressed page view;
* pending as unresolved issue pool;
* decisions as confirmed judgment pool;
* outputs as delivery artifacts, not fact sources;
* source schema and brief schema as governed by `source-brief-object-spec.md` v0.2.

After the active source rename, all 5 current pages entered the same model:

```text
pages/home.md            → sources/home.md
pages/shop.md            → sources/shop.md
pages/open-box.md        → sources/open-box.md
pages/open-box-result.md → sources/open-box-result.md
pages/toy-collection.md  → sources/toy-collection.md
```

The missing reusable capability is the ability to onboard a new page into this structure from raw material.

---

## 3. Problem to Solve

Before this method, BOMCASE had:

| Existing Capability          | Limitation                                                  |
| ---------------------------- | ----------------------------------------------------------- |
| `create-page-brief.md`       | Can create or update page brief only                        |
| `source-maintenance.md`      | Can patch existing source only                              |
| `delivery-output-handoff.md` | Can generate delivery document only after fact layer exists |
| `stage-check.md`             | Can audit structure only                                    |

What was missing:

```text
raw material
→ active source
→ page brief
→ pending candidates
→ decision candidates
→ delivery readiness
```

This is the new page intake capability.

Example future use case:

```text
Card Gallery raw material
→ sources/card-gallery.md
→ pages/card-gallery.md
→ pending candidates
→ decision candidates
→ Ready for Delivery Output
```

---

## 4. Design Principles

### 4.1 Active Source First

The source is the current detailed fact carrier.

A new page cannot be delivery-ready without:

```text
sources/<page>.md
type: source
status: active
role: detailed_fact_source
```

### 4.2 Page Brief Is a Compressed View

The page brief is not the full fact source.

It should point to:

```text
active_source: ../sources/<page>.md
```

It should summarize, not duplicate.

### 4.3 Spec Is the Schema Authority

`source-brief-object-spec.md` v0.2 is the schema authority.

Prompt logic must follow the spec.

If the spec changes, the prompt must be updated.

### 4.4 Pending and Decisions Are Candidates Only

The bootstrap prompt must not directly modify:

```text
pending.md
decisions.md
```

It only outputs:

```text
pending candidates
decision candidates
```

Human review decides whether those candidates enter the governance files.

### 4.5 Outputs Are Never Fact Sources

Delivery outputs and drafts must never feed back into the fact layer.

They can be used for audit only when explicitly treated as validation materials, not facts.

### 4.6 Visual Implementation Must Be Rewritten as Product Constraint

Raw material may contain design-specific implementation details.

The bootstrap workflow should preserve product intent but avoid hard-coding UI implementation.

Example:

```text
red button with glowing effect
```

should become:

```text
primary action must have higher visual priority and be distinguishable from secondary actions
```

### 4.7 `updated` Means Business Fact Update

`updated` records the last substantive business fact update.

Metadata migration, rename, or formatting cleanup belongs in Maintenance Log.

---

## 5. Prompt Relationship Map

| Prompt                         | Role                               |
| ------------------------------ | ---------------------------------- |
| `page-fact-layer-bootstrap.md` | New page fact-layer initialization |
| `create-page-brief.md`         | Existing source → page brief       |
| `source-maintenance.md`        | Existing source patch maintenance  |
| `delivery-output-handoff.md`   | Delivery handoff generation        |
| `stage-check.md`               | Read-only structure audit          |

The bootstrap prompt should remain draft until it is validated with a real new page.

---

## 6. Why `initial_creation` Exists

Existing fact patch change types are designed for later maintenance:

```text
confirmed_fact_add
confirmed_fact_fix
confirmed_fact_remove
expression_cleanup
supplement_add
pending_candidate
```

They do not describe the initial creation of a page fact layer.

Therefore, bootstrap introduces:

```text
initial_creation
```

Scope:

```text
Only for page-fact-layer-bootstrap workflow.
Not a normal source-maintenance change type.
Not used by regular fact patch tasks.
```

---

## 7. When to Use This Method

Use this method when:

* a new page enters BOMCASE;
* raw material exists but no active source exists;
* a page needs source + brief initialized together;
* pending and decision candidates need to be separated from confirmed facts;
* the page needs to become ready for Delivery Output.

Do not use this method when:

* only a source patch is needed;
* only a page brief refresh is needed;
* a delivery handoff document is needed;
* pending or decisions need direct manual editing.

---

## 8. Validation Path

Before marking `page-fact-layer-bootstrap.md` as active:

1. Keep prompt status as `draft`.
2. Test it on a real new page.
3. Verify generated source follows spec v0.2.
4. Verify generated page brief follows spec v0.2.
5. Verify pending / decision candidates are not written directly.
6. Run stage-check.
7. Run Delivery Output only after readiness passes.
8. Then consider upgrading prompt status to `active`.

---

## 9. Final Judgment

The page fact layer bootstrap capability turns the BOMCASE governance process into a reusable workflow:

```text
raw page material
→ governed fact layer
→ delivery-ready page
```

It captures the lessons from the Open Box and 5-page active source migration process and makes the same process repeatable for future pages.
