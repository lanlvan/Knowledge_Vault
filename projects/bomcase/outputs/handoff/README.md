# Handoff Outputs

This directory stores generated delivery handoff documents.

Outputs are delivered artifacts, not fact sources.

## Directory Rules

- Official handoff documents may be stored under this directory.
- `_drafts/` stores test drafts and validation outputs.
- `_drafts/` must not be used as a fact source.
- Old handoff outputs must not be used to reconstruct current page facts.
- Archive, old output, draft output, and `_drafts/` must not be read as fact sources for new delivery generation.

## Generation Rule

To generate a new handoff document, use:

1. current page brief
2. page active source
3. `pending.md`
4. `decisions.md`
5. `prompts/delivery-output-handoff.md`

Do not generate new handoff documents by editing old output as the source of truth.

## Draft Rule

Test drafts may be used for validation discussion, but they do not update:

- page brief
- active source
- `pending.md`
- `decisions.md`
- prompt rules

If a test draft exposes missing or incorrect facts, return to fact-layer maintenance before generating a formal handoff.
