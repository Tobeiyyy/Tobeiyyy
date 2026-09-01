# Method notes from the vetting session (2026-09-01)

Two method-level takeaways that came out of the skill reviews but don't exist
as copyable files anywhere. Written up here so no future session depends on
that session's transcript. Both are inputs for prompt-architect builds.

## 1. The AI-tell catalog method (from taste-skill, re-targeted at captions/copy)

taste-skill's actual value is not its rules — it's *how the rules were made*:
generate lots of output, audit it, and turn every recurring "AI smell" into a
**binary, mechanically checkable banned rule** instead of aspirational advice.
Its rules name specific hex codes, specific fonts, and countable thresholds
("max 1 uppercase-tracking eyebrow per 3 sections — count instances, fail if
over"). Vibes-rules ("be tasteful", "avoid clichés") don't constrain a model;
countable rules do.

Recipe to apply this to any domain (captions, landing copy, YouTube
descriptions, ...):

1. Generate 20-30 outputs for the real use case with a plain prompt.
2. Audit them side by side and list every recurring tell — specific phrases,
   punctuation habits, structural patterns, register slips. For German tourism
   captions expect things like: "malerisch", "idyllisch", "Erlebnis für die
   ganze Familie", emoji-triple closers, rhetorical-question openers,
   hashtag walls, English loan-phrases.
3. Convert each tell into a binary rule with a mechanical check:
   "count question marks in the first sentence; >0 fails",
   "banned word list: [...] — grep, any hit fails",
   "max 4 hashtags; count them".
4. Add explicit override conditions for each rule (when it IS allowed),
   so the rule is a gate, not a superstition.
5. End the skill with a pre-flight checklist that runs the counts before
   output is shown.

The catalog is only buildable from real generated output — a prompt optimizer
can improve the *wording* of rules but cannot invent the tells. Do step 1-2
once per domain, then let prompt-architect shape steps 3-5 into a skill.

## 2. Skill-craft patterns (from anthropics/financial-services)

The best public example of production skill writing. Patterns to copy into
any future skill build:

- **Anti-rationalization sections.** Don't just state rules — pre-empt the
  model's excuses by name. Their DCF skill literally lists "common
  rationalizations to REJECT", e.g. *"'Writing 75+ formulas feels complex,
  so I'll leave a note for the user to complete it manually'"* and
  *"if you catch yourself computing something in Python and writing the
  result — STOP."* Naming the shortcut kills it far more reliably than
  stating the positive rule alone.
- **Mistake catalogs over instructions.** Sections like `<common_mistakes>`
  / "Top 5 errors" with wrong-vs-correct code pairs (they document a specific
  Office-JS merged-cell trap with both versions). Accumulated failure
  knowledge is the moat; instructions are regenerable.
- **Validation as a hard gate, not advice.** A script (`recalc.py`) must pass
  with zero errors before the deliverable counts as done. Equivalent for a
  caption skill: the pre-flight counts from method 1 above.
- **Utility-skill layering.** Domain skills (dcf-model) delegate mechanics to
  utility skills (xlsx-author) so conventions live in exactly one place.
  Equivalent: one shared `voice.md` (see voice-builder here in the quarry)
  read by every content skill, instead of restating the voice per skill.
- **Output contracts.** Every skill defines exactly what the deliverable
  looks like (format, sections, color-coding conventions) so "done" is
  checkable.
- **One source of truth, synced deploys.** Canonical prompt in one file,
  wrapped per deploy surface, with a lint script failing CI when copies
  drift. Relevant the moment a skill exists in both claude.ai and Claude
  Code variants.

## Where things stand / pointers

- Verdicts + install commands: `README.md` in this folder.
- Raw material for the Mattsee caption skill: `marketingskills/copy-editing`
  (Seven Sweeps), `social-media-skills/voice-builder` (absence signals),
  `marketingskills/social-references/platform-limits.md`.
- Raw material for other projects: `financial-services/comps-analysis`
  (→ Resale Price Estimator), `financial-services/gl-recon` (→ Kessan
  bank-CSV reconciliation).
- Tracking: Kanryo project "Making Claude better" (#21); domain rebuild
  tasks live on their own project boards (#26 Resale, #10 Kessan).
