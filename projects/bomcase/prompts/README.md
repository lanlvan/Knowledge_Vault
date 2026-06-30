# BOMCASE Prompts

## Active Prompts

| Prompt | Role | Status |
|---|---|---|
| `page-fact-layer-bootstrap.md` | Initialize or reconstruct a page fact layer from raw material | active |
| `page-fact-update-loop.md` | Incrementally update an existing page fact layer from unrouted page material | active |
| `pending-update-loop.md` | Process existing pending ID confirmation results and local consistency checks | active |
| `delivery-output-handoff.md` | Generate delivery handoff documents from current page facts | active |
| `delivery-output-module-change-note.md` | Generate module-level Delivery Output change notes from current active fact layer | active |

## Draft / Supporting Prompts

This section documents non-active or supporting prompt capabilities to avoid role confusion.

| Prompt | Status | Role | Boundary |
|---|---|---|---|
| `stage-check.md` | supporting | Read-only structure and governance checks | Does not auto-fix or modify project files |

## Execution Discipline

BOMCASE fact-layer maintenance prompts must be executed in four stages by default:

1. Pre-check / read-only validation;
2. Write Plan / proposed changes and target files;
3. Apply Patch / minimal patch execution;
4. Post-check / local consistency validation.

This applies to:

- `page-fact-layer-bootstrap.md`
- `page-fact-update-loop.md`
- `pending-update-loop.md`

Do not skip directly to patching unless the command explicitly says the pre-check and write plan have already passed.

`delivery-output-handoff.md` follows a related delivery flow:

1. readiness check;
2. generation plan;
3. output generation;
4. Copy Coverage / boundary check.

Delivery output generation must not maintain or repair the fact layer. If facts are incomplete or inconsistent, route the issue back to the relevant fact-layer maintenance prompt.

### Delivery Output Execution Note

`delivery-output-handoff.md` may be executed through a single clean execution command when the command only provides input parameters, required reading scope, output path, and execution boundaries.

Delivery output is not a fact-layer maintenance flow and is not required to be split into multiple independent commands by default. The single execution command must still rely on `delivery-output-handoff.md` internal gates, including readiness, source dependency, knowledge update, Copy Coverage, and boundary checks.

If any gate fails, generation must stop and the issue must return to the appropriate fact-layer maintenance prompt.

## User-Facing Prompt Classification

BOMCASE user-facing prompts are classified by input material state, not by target file.

Do not ask the user to choose a prompt based on whether a change should write `sources/*.md`, `pages/*.md`, `pending.md`, or `decisions.md`.

Use the following routing:

| Input material state | Prompt | Result |
|---|---|---|
| New page material, or existing page fact-layer reconstruction from raw material | `page-fact-layer-bootstrap.md` | Creates / updates source + page brief and outputs pending / decision candidates in bootstrap report |
| Existing page incremental fact update from unrouted page material | `page-fact-update-loop.md` | Reads current fact layer, routes source / brief writes, outputs pending / decision candidates by default |
| Existing pending ID receives a confirmation result | `pending-update-loop.md` | Closes / keeps / rewrites / merges pending and updates related knowledge files as needed |
| Current facts are ready and a delivery document is needed | `delivery-output-handoff.md` | Generates Delivery Output only |

The former source-only and brief-only single-file prompt entries have been merged into `page-fact-update-loop.md` and deleted.

They are no longer callable prompt entries.

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

## Delivery Output Module Change Note Prompt

`delivery-output-module-change-note.md` is the active prompt for module-level Delivery Output change notes.

Relationship:

- Belongs to the Delivery Output family.
- Module-scoped variant of `delivery-output-handoff.md`.
- Inherits Delivery Output skeleton semantics.
- Does not create a separate document system.
- Does not replace Full Handoff or Incremental Handoff.

Use when:

- A single module or local rule changed.
- Full Handoff is too broad for the immediate reader.
- Incremental Full-context Handoff still carries too much page context.
- The target reader needs focused current-rule, development-impact, and acceptance information.

Does not:

- Maintain source.
- Maintain page brief.
- Update pending.
- Update decisions.
- Use old output / draft output / archive as fact source.
- Generate page-specific skeleton rules.

## Clean Execution Command Rule

Execution commands should only provide:

- input parameters
- allowed reading scope
- forbidden fact sources
- output path
- modification boundary

Execution commands must not supplement, replace, or extend prompt rules.

Page-specific coverage requirements should come from page brief and active source, not from ad hoc execution commands.

## Pending Update Loop Prompt

`pending-update-loop.md` is the prompt for maintaining the BOMCASE pending closure workflow.

Use it when an existing ID in `pending.md` receives a human confirmation result and the project needs to execute close / keep / rewrite / merge / write-back / local consistency check.

It may update `sources/*.md`, `pages/*.md`, `global-navigation.md`, `project-brief.md`, `decisions.md`, and `pending.md` according to the confirmed result and write-target rules.

It does not replace `stage-check.md`; it only performs local consistency checks for the current pending update.

It differs from `page-fact-update-loop.md` by trigger source:

- `page-fact-update-loop.md`: user provides unrouted material for an existing page fact update.
- `pending-update-loop.md`: user provides pending ID confirmation results and needs a multi-file closure loop.

Derived pending items must be output as candidates only and must not be written into `pending.md` unless the user confirms creation.

## Page Fact Update Loop Prompt

`page-fact-update-loop.md` is used for existing page fact-layer updates from unrouted page material.

It must not generate delivery handoff documents.

It may update `sources/*.md` first and `pages/*.md` second when current page facts and the page reading layer are both affected.

It does not directly update `pending.md` or `decisions.md` by default. Pending and decision findings are output as candidates unless the task is explicitly routed to the relevant workflow.
