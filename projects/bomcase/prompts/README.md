# BOMCASE Prompts

## Active Prompts

| Prompt | Role | Status |
|---|---|---|
| `delivery-output-handoff.md` | Generate delivery handoff documents from current page facts | active |
| `source-maintenance.md` | Apply confirmed Fact Patch into target active source | active |

## Draft / Supporting Prompts

This section documents non-active or supporting prompt capabilities to avoid role confusion.

| Prompt | Status | Role | Boundary |
|---|---|---|---|
| `page-fact-layer-bootstrap.md` | draft | Initialize new page fact layer from raw material: `raw material -> active source -> page brief -> pending candidates -> decision candidates -> bootstrap report` | Does not generate Delivery Output; does not modify `pending.md` / `decisions.md`; bootstrap report is not a fact source; keep as draft until real new-page validation |
| `create-page-brief.md` | supporting | Existing active source -> generate or update one page brief | Does not replace active source; does not auto-confirm new facts |
| `stage-check.md` | supporting | Read-only structure and governance checks | Does not auto-fix or modify project files |
| `source-maintenance.md` | active (see Active Prompts) | Controlled fact patch maintenance for existing active source | Listed in Active Prompts table; not duplicated as a draft capability |

## Delivery Output Prompt v1.1

`delivery-output-handoff.md` is the active neutral prompt for generating delivery handoff documents.

It must not contain page-specific business facts.

Delivery output generation must read:

1. page brief
2. active source
3. `pending.md`
4. `decisions.md`
5. necessary global facts

It must not use archive, old output, draft output, README, index, or unrelated page source as fact sources.

Full mode must preserve the delivery granularity of active source, including:

- fields
- states
- interactions
- acceptance criteria
- user-facing copy
- info / hover copy
- button copy
- status copy
- bottom summary copy

If Copy Coverage fails, the generator must output Copy Coverage Failure Report instead of claiming a complete handoff document.

## Clean Execution Command Rule

Execution commands should only provide:

- input parameters
- allowed reading scope
- forbidden fact sources
- output path
- modification boundary

Execution commands must not supplement, replace, or extend prompt rules.

Page-specific coverage requirements should come from page brief and active source, not from ad hoc execution commands.

## Source Maintenance Prompt

`source-maintenance.md` is used only to apply confirmed fact patches into the target active source.

It must not generate delivery handoff documents.

It must not update `pending.md` or `decisions.md` unless explicitly instructed by the relevant workflow.
