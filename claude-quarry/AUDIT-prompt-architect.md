# Audit: prompt-architect vs. the context-engineering shift (2026-09-01)

Audited: the synced `prompt-architect` skill (IE-v3, framework state
2026-08-02, 2,524 lines), read in full. Question: is it still current now
that instruction scaffolding loses value on smarter models while context
richness gains?

## Verdict

**Not obsolete — it is already half a context-engineering tool.** The
routing engine and interview engine are its future-proof core. One
structural gap and one aging area found. Recommendation: **extend, don't
fork** — no separate context-architect skill.

## What holds up (keep, don't touch)

- **Phase 0 + Environment Capability Table** already does *surface-level*
  placement: routes by capability dimensions (persistence, files, web,
  agentic, budget) across chat/Project/Code/Cowork/Design/Research/API,
  including "build nothing" reroutes to existing tools. This is context
  engineering between surfaces, and it's the part most prompt tools lack.
- **Interview Engine** = context *elicitation*. Smarter models make elicited
  context more valuable, not less. Coverage ledger with non-N/A-able
  objective line is mechanical-check discipline (same philosophy as
  taste-skill's countable rules).
- **Deliverable Economy Rule + check #14 craft pass** already mandate the
  delete-test ("could a line be deleted without changing any output?") —
  the anti-verbosity principle is present.
- **Golden Input Regression Set** (29 locked routing cases) — real
  engineering; extend it with any change below.

## Findings (ranked)

### 1. Intra-container placement is missing (the real gap)
Phase 0 routes BETWEEN surfaces, but once the verdict is "Mode 2/3
container," ALL content lands in the custom-instructions field. No step
asks: which parts belong in **knowledge files** (bulk reference, examples,
voice corpus), which in **instructions** (persona + rules), which in a
**skill** alongside (procedures that should fire cross-project), which in
**per-session trigger**, which retrieved at runtime. The capability table
HAS a Files/knowledge column — the mode templates never use it to split
payloads. Proof case: the Social Media project — a year of voice-in-
instructions failed; the fix (voice.md as separate read-on-demand
artifact) is a placement decision the framework can't currently produce.

**Fix:** add a "Payload Placement" step to Phase 0 (or Phase 3) for
container verdicts: classify each content type (rules / reference /
examples / voice / procedures) into instructions vs knowledge files vs
companion skill vs trigger, with the litmus "instructions carry behavior;
knowledge files carry material; skills carry cross-container procedures."
Mode 2/3 output formats gain an optional Component 3: knowledge-file
manifest (filename + purpose + what goes in).

### 2. Mode 2 template ships scripted ceremony (aging area)
The Mode 2 system-prompt template hardcodes acknowledgment scripts ("I
understand you want to [Goal]… Let me ask a few questions", plus the German
twin) and a rigid Phase 1/2/3 protocol into every generated assistant.
On current models the scripted phrases are dead weight and make output
feel botlike; the GATES (readiness indicator, ledger, execution trigger)
are the load-bearing part and should stay. **Fix:** slim the template —
keep gates/ledger/trigger, drop scripted acknowledgment lines and phase
theater; let the assistant phrase its own acknowledgments.

### 3. No deployment test block
Covered by Kanryo task #419: every deliverable ships with 3 sample inputs
+ expected behavior. Wire into the Delivery Block, gate via a new
Pre-Ship check.

### 4. Minor / hygiene
- Skill fires at ~26k tokens (monolithic). Optional modernization:
  progressive disclosure (slim SKILL.md + references/), per Anthropic
  skill-craft. Complicated by the Project↔skill verbatim-sync rule —
  decide deliberately, not casually.
- Hardcoded Windows paths (C:\Users\Tobey\...) break in remote/cloud
  sessions; make those references conditional ("where available").

## Why extend instead of a companion skill

A separate context-architect would need Phase 0's capability table and
routing logic — duplicating the one piece that must have exactly one owner
(the framework's own redundancy-mapping rule). It would also double the
Project↔skill sync burden that already exists. One skill, one table, one
new placement step is the architecture the framework itself would
recommend.

## Implementation note

The Claude Project is canonical; the skill is a verbatim port. Apply edits
in the Project first, mirror to the skill in the same delivery (its own
sync rule), and add regression cases for: a voice-heavy container build
must produce a knowledge-file manifest, and a Mode 2 build must not emit
scripted acknowledgment lines.
