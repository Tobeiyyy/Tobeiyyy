# prompt-vault

Canonical home of every AI instrument in use: Claude Project instructions,
trigger prompts, pipelines, and standalone system prompts. One folder per
instrument; the file IS the current version; git history IS the version
history. Edited via Claude Code (file edit + diff-verify + push), then
pasted into the deploying surface — the paste is the only manual step.

Convention per instrument folder:
- `instructions.md` (or `trigger.md` / `pipeline.md`) — the deployable text, verbatim
- first line of this README's index row — what it's for + audit verdict

## Index

| Instrument | Type | Deployed in | Audit verdict |
|---|---|---|---|
| _(backfill pending — see Kanryo task 425)_ | | | |

## Backfill checklist (paste each into a Claude Code session with this repo attached)
- [ ] Social Media / Tourism Mattsee (Project) — rebuild already planned (Kanryo 413/416)
- [ ] Resale Price Estimator (Project)
- [ ] Learning Architect (Project)
- [ ] captions.py system prompt (API deployment)
- [ ] Ultimate Prompt Architect → NOT here; lives in FLIP-prompt-architect (its own canonical repo)
- [ ] any Gems / custom GPTs still in use
- [ ] any pipelines (multi-station prompt sets)
