# Implementation Plan

> EDITING DIRECTIVE: USER AND AGENT EDIT THIS FILE COLLABORATIVELY. THE USER MUST REVIEW AND APPROVE ITS CONTENT.

Purpose of this file: Turn the approved specification into ordered, updatable implementation and verification work.

## Instructions for the user

Preserve the approved requirements and verify the completed work. Direct priorities, scope, and meaningful checkpoints; judge technical choices, risks, and proposed changes; and approve results only after checking them against the specification rather than relying solely on the agent's report.

If the intended result changes, update the specification. If only the route changes, update this plan and record the revision.

## Instructions for the agent

Read AGENTS.md, brief.md, research.md, spec.md, and this file, then inspect the relevant project files. Begin with a concise orientation and one focused question.

Guide planning one stage at a time. Surface dependencies, risks, and verification needs without expanding scope or making decisions for the user. Draft concise, project-specific tasks and keep them current. Never mark approval gates or user-verification items complete on the user's behalf.

## Approach

Describe the technical approach, important dependencies, and the order in which the features will be built. Explain any non-obvious choices and identify likely risks.

**Build order:** confidence-label infrastructure (tier taxonomy + a small reusable inline-label mechanism) first, applied immediately to the existing EcoLogits text rows and the existing gaming row — every later feature declares its own tier as it's built, rather than retrofitting labels afterward. Then Features 1–4 in spec order. Then a final Feature 5 pass to confirm every row (old and new) is labeled and the citation footnote list is complete.

**Non-obvious choice — Feature 1 is a standalone toggle, not a row.** The spec describes the image bucket as using "the same interaction pattern as existing prompt-size rows," but those rows are keyed by `{model, size}`, and the image figure is model-agnostic. Building it as a row would require a model dropdown that doesn't actually change the number, which is misleading. Decided instead to build it as a standalone checkbox + quantity toggle, matching the existing gaming add-on's pattern. This changes the *route*, not the intended result (a model-agnostic contribution to the total, still labeled per Feature 5) — recorded here per plan.md's revision rule rather than reopening spec.md.

**Risks to watch:**
- **Footnote numbering.** The report-generation code references citations by hardcoded numeric index (`fn(1)`, `fn(2)`, etc.) into the `REPORT_REFS` array. New sources (Luccioni, Hausfather, IEA, Obringer) must be *appended*, not inserted, or existing `fn()` call sites will silently point at the wrong citation.
- **Total-calculation wiring.** Features 1, 3, and 4 are new standalone toggles (like gaming), each needing its own contribution wired into both the per-metric total functions and the top-line daily-energy function — gaming's existing dual-function pattern (`gamingDailyTriple` / `gamingDailyEnergy`) is the template to follow so nothing is double-counted or dropped from one of the two paths.
- **Feature 2's replacement, not addition.** Widening the agent min/max must *replace* each model's existing EcoLogits-only range, not stack on top of it — otherwise sessions would show an implausibly huge combined spread.
- **Methodology/label drift.** The inline tier labels (Feature 5) and the detailed methodology accordion text must stay consistent; a single source of truth for each tier's wording (rather than duplicating it in two places) reduces the risk of them diverging as features are added later.

## Checklist

Replace or expand the implementation placeholders below with tasks specific to the approved specification.

### Approval gates

- [x] User has reviewed, verified, and approved the research claims and selected features (2026-09-21)
- [x] User has reviewed and approved the specification (2026-09-27)
- [x] User has reviewed and approved the implementation approach and task sequence (2026-09-27)

### Implementation

- [ ] Add the confidence-label taxonomy (4 tiers) as shared data/markup, and apply it to the existing EcoLogits text rows and the existing (unsourced) gaming row
- [ ] Feature 1 — image-generation toggle: standalone checkbox + quantity add-on (Luccioni ~2.9 Wh/image), wired into both total-calculation paths, carbon-only (no embodied-hardware term, no water), tagged "single-point estimate"
- [ ] Feature 2 — coding-agent range: replace each model's existing agent min/max with mean × 0.4 / mean × 1.9 (Hausfather ratio), update methodology text with the prompt-vs-session distinction and the extrapolation caveat, append Hausfather to `REPORT_REFS`
- [ ] Feature 3 — streaming toggle: standalone checkbox + hours/day add-on, flat 36 g CO2/hour regardless of region (matching the home/diet/driving/flying pattern), no water value, append IEA to `REPORT_REFS`
- [ ] Feature 4 — video-call toggle: standalone checkbox + hours/day add-on plus camera on/off (default on), Obringer range (150–1,000 g CO2 / 2–12 L water/hour) with ~96% camera-off reduction, append Obringer to `REPORT_REFS`
- [ ] Final Feature 5 pass: confirm every row (old and new) shows a tier label, and that the methodology accordion text matches the inline labels
- [ ] Implement the tasks in meaningful checkpoints, keeping the plan and specification aligned with approved changes

### Verification

- [ ] User has checked feature behavior and calculations against the specification and sources independently of the agent
- [ ] User has confirmed factual and numerical claims have working citations and communicate important limitations or uncertainty
- [ ] User has confirmed the project runs locally, serves all three reference profiles, and matches the specification
- [ ] User has confirmed footnote numbering in the generated report is correct after new sources were added (no `fn()` call site points at the wrong citation)

### Delivery

- [ ] Commit meaningful checkpoints and export the working chat transcripts
- [ ] Add the provided Project 2 debrief, complete it after verification, and export its transcript

## Revisions

Record material changes to the approach, sequence, or checklist and explain why they were made.

## Commands

### Start planning

User: Open the project repository as your workspace, start a fresh chat, and type `start planning`.

### Start implementation

User: After approving the plan, open the project repository in a fresh chat and type `start implementation`.

Agent: Read AGENTS.md, brief.md, spec.md, and this file, then inspect only the project files relevant to the approved work. Follow AGENTS.md and the approved plan. Do not begin implementation if the plan has not been approved. Keep the plan current, but never mark approval gates or user-verification items complete on the user's behalf.

### Save transcript

Agent: At the end of planning, remind the user that the transcript is a deliverable and ask them to say `save transcript`. Wait for that direction. When directed, save the entire conversation in the `transcripts/` directory as `plan-YYYY-MM-DD_HHMMSS.md`, mark user and agent responses clearly, and confirm the saved relative path.

Agent: At the end of every implementation chat, remind the user to say `save transcript`. When directed, save the entire conversation as `build-YYYY-MM-DD_HHMMSS.md` using the same location and formatting.
