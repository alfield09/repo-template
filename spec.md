# Technical Specification

> EDITING DIRECTIVE: USER AND AGENT EDIT THIS FILE COLLABORATIVELY. THE USER MUST REVIEW AND APPROVE ITS CONTENT.

Purpose of this file: Define what the completed project must do so it can be planned, built, and verified.

## Instructions for the user

Translate the approved research into a specification without distorting its evidence, limitations, or uncertainty. Direct the work toward the intended result, judge gaps and trade-offs rather than accepting invented requirements, and approve only a complete, testable specification grounded in the research.

## Instructions for the agent

Read AGENTS.md, brief.md, research.md, and this file. Begin with a concise orientation and one focused question.

Guide the specification one feature at a time. Help turn approved decisions into precise requirements and surface gaps or trade-offs without inventing requirements or making product decisions. Draft concise updates for review, focus on the intended result rather than implementation steps, and never approve the specification on the user's behalf.

## Goal

State what the completed project should accomplish for its intended audience.

The completed calculator should let creative-media employees — regardless of role, technical background, or how they personally feel about AI — see how their own professional AI use (text, image generation, and coding-agent sessions) compares in energy, carbon, and water cost to their broader digital habits and everyday activities, using transparent, cited methodology that visibly communicates confidence and uncertainty rather than presenting estimates as settled facts.

## Features

For each feature, define:

- the need it addresses and intended audience outcome
- its behavior, inputs, and outputs
- its calculations, supporting evidence, and uncertainty
- its interface expectations and acceptance checks

### Feature 1: Image-generation bucket

**Need / audience outcome:** the calculator currently only models text prompts, so anyone doing image-generation work (Alex) has no way to see that use represented at all. This adds it.

**Behavior, inputs, outputs:** "An AI image" is a new selectable prompt-type row, entered as a quantity (e.g. "10 AI images today"), contributing its own energy/carbon/water line to the running total — same interaction pattern as existing prompt-size rows. It is **model-agnostic**: available and calculated the same way regardless of which text model is selected in the existing model picker, since the underlying evidence is not per-model.

**Calculations, evidence, uncertainty:** ~2.9 Wh per image ([Luccioni, Jernite & Strubell, FAccT 2024](https://arxiv.org/html/2311.16863v3)), converted to carbon using the same regional-grid method already applied to text prompts (Wh × grid intensity). Unlike EcoLogits' per-model text figures, this source gives no confidence interval — must be presented as a single-point benchmark average, not a range, and labeled accordingly. No water figure exists for this row (see Feature 5).

**Stated limitation:** every text row's carbon figure also includes EcoLogits' embodied-hardware-emissions term (amortized manufacturing impact per inference) on top of the grid-electricity carbon. Luccioni's image figure is energy-only and has no equivalent embodied-carbon term, so the image row's carbon is electricity-only. This must be disclosed — otherwise image generation would silently look proportionally cleaner on that dimension than text, for no evidenced reason, not because it actually is.

**Interface expectations / acceptance checks:**
- "An AI image" appears in the prompt-type selector independent of the model dropdown; switching models does not change its figure or make it disappear.
- Selecting a quantity N adds N × 2.9 Wh to total energy, converted to carbon via the selected region's grid intensity, consistent with how text rows are costed.
- The water column/value for this row is explicitly marked as unavailable, not silently zero (dependency: Feature 5).
- The methodology section cites Luccioni et al. and states this is a single-point estimate with no stated confidence range, unlike the text-model figures.

### Feature 2: Coding-agent range

**Need / audience outcome:** Jordan's complaint that "prompts per day" is too simplistic is sharpest for agent sessions, which the current calculator represents as near-fixed values (EcoLogits' 100,000-token benchmark plus its architecture-uncertainty range). This feature makes the "agent session" option reflect how much real sessions actually vary in scope, not just uncertainty about the model's build.

**Behavior, inputs, outputs:** The existing "a coding / agent session" row is unchanged in how it's selected (still one row per model, still a quantity), but its min/max range is widened to reflect real-world session-to-session variance rather than only EcoLogits' architecture uncertainty.

**Calculations, evidence, uncertainty:** Hausfather's measured Claude Code data ([The Climate Brink, 2026](https://www.theclimatebrink.com/p/the-real-energy-use-of-agentic-ai)) reports two different units: a per-*prompt* figure (~60–290 Wh around a ~150 Wh mean, a single typed instruction that can trigger many model calls) and a separate, much larger per-*session* figure (~600 Wh median, 100+ model calls, ~10 million tokens). The per-prompt figure is the one used here, since its scale is closer to the calculator's existing "agent session" concept — but it is not the same unit Hausfather himself calls a "session," and that distinction must be stated, not implied away. The ratio taken from it (~60/150 = 0.4x, ~290/150 = 1.9x) is applied to *every* model's existing mean session figure, replacing each model's current EcoLogits-only min/max with mean × 0.4 and mean × 1.9.

**Why the ratio, not the absolute figures:** Hausfather's per-day data (mean 3.0 kWh, range 1.2–5.9 kWh) produces almost the same ratio (~0.4x–1.97x) at a completely different scale. That the proportional spread holds across two different units in his own data is the actual justification for generalizing the *ratio* — not a claim that his "prompt" and the calculator's "session" are the same thing.

**Stated limitation (required, per the brief's uncertainty rule):** this ratio was measured only on Claude Code. It is being applied to GPT-5.5, Gemini, and other agent figures as an assumption, not a measurement — there is no direct evidence that other coding agents vary by the same proportion. The methodology text must say this plainly, not bury it, and must not imply Hausfather's units map cleanly onto "one agent session" as modeled here.

**Interface expectations / acceptance checks:**
- Every model's "agent session" row shows the widened min/max (mean × 0.4 to mean × 1.9), replacing the previous EcoLogits-only range.
- The on-page methodology text names Hausfather's study, states the 0.4x–1.9x ratio, and explicitly flags that this ratio is extrapolated to non-Claude models without direct evidence.
- The report/citation output (footnote list) includes the Hausfather source alongside the existing EcoLogits citation for this row.

### Feature 3: Video-streaming comparison

**Need / audience outcome:** lets someone place their AI use next to a familiar daily activity (streaming), and serves as a concrete example of how a viral overestimate got corrected — directly useful for Robin's skepticism, and relevant to Alex's habit of streaming reference media.

**Behavior, inputs, outputs:** a new "Also count streaming" toggle, following the same interaction pattern as the existing gaming add-on (checkbox reveals an hours/day input), contributing its own carbon line to the daily total.

**Calculations, evidence, uncertainty:** flat 36 g CO2/hour ([IEA, "The carbon footprint of streaming video: fact-checking the headlines"](https://www.iea.org/commentaries/the-carbon-footprint-of-streaming-video-fact-checking-the-headlines)), applied regardless of the user's selected region, because it's IEA's own already-composed carbon estimate (device + network + data center under IEA's assumptions), not a raw wattage to multiply by grid intensity. This is **not** a special exception: the calculator's existing home, diet, driving, and flying comparisons already use flat, pre-computed carbon figures the same way — only the AI-prompt and gaming rows use the energy × grid approach. Streaming follows the same pattern as those existing life-comparison rows, and the methodology text should say so rather than presenting it as an inconsistency needing an apology. No water figure exists for this row (dependency: Feature 5, "no data" disclosure).

**Interface expectations / acceptance checks:**
- Toggling "Also count streaming" on reveals an hours/day input; the resulting carbon contribution is hours × 36 g CO2, unaffected by the region selector.
- A visible note (not just in the methodology accordion) explains that this figure is a fixed global estimate, not adjusted for the user's chosen region, and why.
- The water value for this row is explicitly marked unavailable.
- The methodology section cites the IEA source and, briefly, the Shift Project correction story as the basis for the figure's credibility.

### Feature 4: Video-call comparison, camera on/off

**Need / audience outcome:** lets someone place AI use next to another familiar work habit (video meetings), and shows how a personal choice (camera on/off) changes the footprint — relevant to Robin (frequent meetings) and Jordan (video calls during long sessions).

**Behavior, inputs, outputs:** a new "Also count video calls" toggle, same interaction pattern as gaming/streaming (checkbox reveals an hours/day input), plus a camera on/off control defaulting to **on** (reflects typical behavior rather than nudging toward either choice). Contributes its own carbon and water lines to the daily total.

**Calculations, evidence, uncertainty:** 150–1,000 g CO2 and 2–12 L water per hour with camera on ([Obringer et al., *Resources, Conservation and Recycling*, 2021](https://www.purdue.edu/newsroom/archive/releases/2021/Q1/turn-off-that-camera-during-virtual-meetings,-environmental-study-says.html)); camera off applies a ~96% reduction to both figures, per the same study. Unlike the existing gaming add-on (which shows a single flat number), this row displays the actual min–max range rather than collapsing it to one figure, since the source itself gives a range, not a point estimate, and inventing a "typical" value would overstate precision the evidence doesn't have.

**Interface expectations / acceptance checks:**
- Toggling "Also count video calls" reveals hours/day and a camera on/off control, defaulted to on.
- With camera on, the row shows the full 150–1,000 g CO2 and 2–12 L range scaled by hours; with camera off, both bounds are reduced ~96%.
- The methodology section cites Obringer et al., states the range explicitly, and repeats the authors' own "rough" characterization of the estimate.

### Feature 5: Visible per-line confidence/uncertainty labels

**Need / audience outcome:** currently, confidence and limitations live only in the collapsed methodology accordion — someone has to go looking for them. This surfaces that information next to each number instead, serving Robin's stated need (visible sources, honest uncertainty over polish) and giving every other feature's caveats somewhere to actually be seen.

**Behavior, inputs, outputs:** every value-producing row in the calculator (existing text-model rows, and all four new features above, plus the pre-existing gaming row) gets a short inline label next to its number, drawn from a four-tier taxonomy:

1. **Peer-reviewed with stated range** — existing EcoLogits text-model rows; Feature 2's coding-agent range (paired with its extrapolation caveat).
2. **Single-point estimate, no confidence range given** — Feature 1's image-generation figure.
3. **Rough / well-sourced but limited** — Feature 3's streaming figure (sourced, but not region-adjusted); Feature 4's range (sourced and peer-reviewed, but the authors themselves call their own estimates rough — this self-acknowledged limitation is why it sits in this tier rather than tier 1).
4. **No data / unsourced** — water values for image, video-gen (if ever added), and streaming rows; the pre-existing gaming wattage figure, which has no citation in the original calculator.

Exact visual treatment (badge, icon, inline text) is left to the build phase, not fixed here.

**Calculations, evidence, uncertainty:** this feature doesn't add a number of its own — it labels the confidence/limitation status of every other row's number, using the tiering above.

**Interface expectations / acceptance checks:**
- Every row with a value (all existing text-model rows, all four new features, and the existing gaming row) displays one of the four tier labels next to its number, visible without expanding the methodology section.
- Rows with no data for a given metric (e.g. water for image/streaming) show "no data" rather than a blank or a zero.
- The gaming row is labeled as unsourced, reflecting that its wattage figure carries no citation in the original calculator.
- The methodology section still contains the full explanation for each tier, so the inline label and the detailed accordion text stay consistent with each other.

## User approval

Review the completed specification directly and explicitly approve it before planning begins. The agent cannot complete this approval on the user's behalf.

**Approved by the user on 2026-09-27.** The goal and all five features above (image-generation bucket, coding-agent range, video-streaming comparison, video-call comparison, visible confidence/uncertainty labels), including the three corrections from the verification pass, are confirmed as final for planning.

## Out of scope

Record ideas that will not be part of this project.

- **Video-generation bucket.** Real evidence exists (MIT Technology Review / CogVideoX), but it rests on one contested model; adding it alongside the more solid image figure risked implying equal certainty. May be revisited later with a stronger caveat design.
- **Project-level running total / session log for coding agents.** Would further serve Jordan, but the design question (a log of sessions vs. a simple multiplier) is unresolved and unevidenced — more a UX decision than a research-backed feature.
- **New/improved gaming-PC comparison.** No reliable wattage source was found during research (LBNL's Green Gaming project gave only qualitative findings); the existing gaming feature is left as-is except for the new confidence label from Feature 5.
- **Correcting or re-sourcing the existing gaming wattage figure.** Feature 5 labels it as unsourced but does not attempt to find or substitute a better-cited number — that would be new research, not a labeling change.
- **Regionalizing the streaming figure.** Considered and rejected in favor of a flat, non-region-adjusted number (Feature 3) to avoid adding an unevidenced approximation layer.

## Revisions

If implementation changes the intended result, update the specification and record what changed and why.

## Commands

### Start specification

User: Open the project repository as your workspace, start a fresh chat, and type `start specification`.

### Save transcript

Agent: After the user approves the specification, remind them that the transcript is a deliverable and ask them to say `save transcript`. Wait for that direction.

When the user directs the agent to save the transcript, the agent saves the entire conversation in the `transcripts/` directory as `spec-YYYY-MM-DD_HHMMSS.md`, marks user and agent responses clearly, and confirms the saved relative path.
