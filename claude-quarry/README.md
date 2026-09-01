# Claude Quarry

Curated extracts from the skill-repo vetting session (2026-09-01), for the
"Making Claude better" project. This folder is self-contained — nothing else
in the repo references it. Everything here is MIT-licensed source material
(license copies included per source) meant to be **quarried into custom
skills**, not installed as-is.

## Verdict summary from the vetting

| Source | Verdict |
|---|---|
| `nextlevelbuilder/ui-ux-pro-max-skill` | **Install** (not copied here — it's 3.8MB of data+code; install as plugin, see below) |
| `leonxlnx/taste-skill` | Install only for frontend work (not copied — 87KB skill, overlaps with ui-ux-pro-max) |
| `anthropics/financial-services` | Study as skill-craft reference; two transferable skills copied here |
| `coreyhaines31/marketingskills` | Quarry only — the ~3 dense pieces are copied here, rest is generic |
| `charlie947/social-media-skills` | Quarry only — voice-builder method copied here, rest is LinkedIn-creator-specific |

## What's in here and why

### `marketingskills/` (from coreyhaines31/marketingskills)
- **`copy-editing/`** — the "Seven Sweeps" revision procedure (Clarity → Voice →
  So What → Prove It → Specificity → Emotion → Zero Risk, with loop-back rules).
  Best density in that repo. Use as the revision loop in a future Mattsee
  caption skill.
- **`social-references/`** — `platform-limits.md` (verified char/hashtag limits,
  e.g. Instagram shows ~125 caption chars before "more"), `carousel-frameworks.md`
  (5 slide-by-slide architectures with failure modes), `short-form-video.md`
  (timing structures).

### `social-media-skills/` (from charlie947/social-media-skills)
- **`voice-builder/`** — the "absence signals" voice-extraction method: define a
  brand voice by what it provably never does, evidenced across writing samples
  ("no em dashes: 0 of 5 samples"). The interview questions are hardcoded for
  solo LinkedIn creators — rewrite them for a place brand before use. Also worth
  copying: its architecture of one shared `voice.md` that every other skill reads.

### `financial-services/` (from anthropics/financial-services, official Anthropic)
- **`gl-recon/`** — normalize → full-outer-join → bucket → classify-cause
  reconciliation pattern with a break taxonomy. Near-template for reconciling
  Kessan (finance tracker) against bank CSV exports.
- **`comps-analysis/`** — "value X by comparable peers, adjust, present a range
  not a point estimate." Structurally the same problem as the Resale Price
  Estimator; steal the workflow shape.
- The repo itself is also the best public reference for skill *craft*:
  anti-rationalization sections ("common shortcuts to REJECT"), mistake
  catalogs, output contracts, utility-skill layering, validation scripts as gates.

## Install list for the main PC (Claude Code)

```
/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
/plugin install ui-ux-pro-max@ui-ux-pro-max-skill
```

taste-skill (optional, frontend sessions only): https://github.com/leonxlnx/taste-skill

## Next step (Kanryo task 413)

Build a bespoke Tourism-Mattsee caption skill with prompt-architect, seeded with:
1. an absence-signals `voice.md` extracted from real captions (voice-builder method),
2. Seven Sweeps as the revision loop,
3. `platform-limits.md` as hard constraints.
