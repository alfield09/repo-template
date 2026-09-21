# Research

> EDITING DIRECTIVE: USER AND AGENT EDIT THIS FILE COLLABORATIVELY. THE USER MUST REVIEW AND APPROVE ITS CONTENT.

Purpose of this file: Develop and record the evidence and decisions that will guide the technical specification.

## Instructions for the user

You are responsible for the ethics, accuracy, and fairness of the research. Direct the inquiry toward useful questions, judge sources and suggestions rather than accepting them at face value, and approve only results supported by verified evidence and audience needs. Seek evidence that challenges your assumptions, represent uncertainty honestly, and reject claims you cannot verify. See [UNESCO's Guidance for generative AI in education and research](https://www.unesco.org/en/articles/guidance-generative-ai-education-and-research).

## Instructions for the agent

Read AGENTS.md, brief.md, and this file. Begin with a concise orientation and one focused question.

Guide the research one stage at a time. Help the user explore options, assess sources, and identify contrary evidence or uncertainty without making decisions for them. Draft concise updates for review, and never mark research or feature choices approved on the user's behalf.

## Reference employee profiles

- Alex — Los Angeles, 24, junior video editor: Uses text, image, and video-generation tools for production work. Streams reference media and uses social platforms across a phone, laptop, and television. Wants to understand impacts beyond text prompts and is particularly attentive to water use.
- Jordan — Austin, 38, creative technologist: Uses coding agents and generative tools in long, irregular sessions. Games on a desktop PC and participates in frequent video calls. Finds "prompts per day" too simplistic and wants assumptions, ranges, and project-level totals.
- Robin — Chicago, 56, operations manager: Uses text AI occasionally but spends substantial time in video meetings, streaming media, and social platforms. Is skeptical of the company's motives and needs plain-language explanations, visible sources, and honest indications of uncertainty.

These are fictional starting profiles, not evidence about demographic groups. Research the activities, circumstances, and needs they represent rather than making assumptions based on age or location.

## Audience needs

Record information about the activities, circumstances, and needs represented by all three reference profiles. Separate evidence from assumptions that still need checking.

### Alex — image/video generation, water use, cross-device

**Evidence:**
- The current calculator only models text prompts (EcoLogits). Per-inference energy for image generation is measured at ~62x text generation (2.9 Wh vs. 0.047 Wh) in a peer-reviewed study ([Luccioni, Jernite & Strubell, "Power Hungry Processing," FAccT 2024](https://arxiv.org/html/2311.16863v3)).
- Video generation is far higher again: MIT Technology Review reported ~3.4 million joules (~944 Wh) for a 5-second CogVideoX clip, ~700x a single image ([MIT Technology Review, May 2025](https://www.technologyreview.com/2025/05/20/1116327/ai-energy-usage-climate-footprint-big-tech/)). The article itself notes this is one open-source model — proprietary systems (Sora, Veo) aren't measured, and longer clips scale non-linearly, not necessarily proportionally.
- **No peer-reviewed study has directly measured water use for image or video generation.** The Luccioni paper explicitly names this as an open gap in its own field. Every water figure circulating publicly (e.g. "~23 mL per image") is back-calculated from energy estimates using a generic water-per-kWh conversion, not a direct measurement.

**Implication:** there's solid evidence that image and video generation cost far more energy per output than text — but Alex's specific concern (water) has no direct measurement to cite. The honest answer is "we don't know," which is itself worth stating rather than presenting a back-calculated number as fact.

**Assumption needing checking:** whether Alex's water-use concern is about data-center cooling specifically, or a broader "AI is resource-intensive" worry that water just stands in for.

### Jordan — coding agents, project-level totals

**Evidence:**
- Two independent measurements of real Claude Code sessions both show wide variance around a "typical" figure, supporting Jordan's complaint that "prompts per day" hides how differently agent sessions actually run:
  - A median session ≈ 41 Wh (24 API calls, ~592,000 tokens), back-solved from published per-token energy estimates ([Couch, "Electricity use of AI coding agents," Jan 2026](https://simonpcouch.com/blog/2026-01-20-cc-impact/)). The author calls this "napkin math" and flags the weak link himself: it borrows GPT-4o's energy-per-token from one source and Anthropic's *pricing* ratios from another — pricing isn't energy.
  - A more rigorous, longer-running measurement of one person's actual 8-week Claude Code usage (1,138 prompts, 14,000+ model calls, 3.2 billion tokens) found ~150 Wh per prompt (60–290 Wh range), ~3.0 kWh per day (1.2–5.9 kWh range), and a ~170 kWh total (70–330 kWh range) over the 8 weeks ([Hausfather, "The real energy use of agentic AI," 2026](https://www.theclimatebrink.com/p/the-real-energy-use-of-agentic-ai)). The author states ~2x uncertainty and that his usage is heavy — "likely far above typical user distributions."
- A peer-reviewed-adjacent measurement of agentic coding tasks found token cost varies meaningfully by task complexity, and that even the *same* task's most expensive run can use roughly 2x the tokens of its cheapest run ([Bai et al., "Tokenomics," arXiv 2601.14470](https://arxiv.org/abs/2601.14470)).
- **Assumption needing checking:** whether Jordan would actually want a running project-level total (sum of sessions) versus just a wider single-session range. Not yet evidenced — a design question, not a research one.

**Implication:** Jordan's complaint is well supported — session size varies by an order of magnitude or more, and that variance is inherent to agent workloads. The Hausfather source is also the best evidence found so far for giving Jordan an actual multi-day/project-level total rather than a single-prompt figure.

### Robin — broader digital life, skepticism, honest uncertainty

**Evidence:**
- **Video streaming:** the IEA's corrected analysis puts one hour of 2019-baseline streaming at ~36 g CO2, and identifies specific, named errors behind the much larger viral estimate (a megabit/megabyte unit mixup, a ~35x overestimate of data-center energy intensity, and a ~50x overestimate of network energy intensity) ([IEA, "The carbon footprint of streaming video: fact-checking the headlines"](https://www.iea.org/commentaries/the-carbon-footprint-of-streaming-video-fact-checking-the-headlines)). The IEA also names its own limitations: country-average emission factors may overstate data-center impact given renewable procurement, and the estimate excludes set-top boxes/consoles. This is a strong, concrete example of "here's exactly how an estimate went wrong and by how much" for a skeptical reader.
- **Video calls:** Purdue/Yale/MIT researchers found one hour of videoconferencing emits 150–1,000 g CO2 and uses 2–12 L of water, with camera-off cutting this ~96% ([Obringer et al., *Resources, Conservation and Recycling*, 2021](https://www.purdue.edu/newsroom/archive/releases/2021/Q1/turn-off-that-camera-during-virtual-meetings,-environmental-study-says.html)). The researchers themselves call the estimates "rough," dependent on the completeness of third-party provider data.
- **Gaming PC:** LBNL's Green Gaming project (the most credible research group in this space) reports qualitative findings — gaming systems can draw "as much as four efficient refrigerators," with wide variance across systems and idle/navigation power sometimes close to active-gameplay power — but I could not extract a specific, direct wattage figure from the underlying report (PDF was not machine-readable). The commercial "how many watts does a gaming PC use" articles found in search are marketing/buying-guide content, not measurement, and are not reliable sources. **Open gap** if a gaming-related feature is selected.
- **Assumption needing checking:** whether Robin's skepticism is about the company's motives specifically, or about AI/tech-industry claims generally. Not yet evidenced — worth watching for, since it affects tone more than figures.

**Implication:** the IEA and Purdue sources both model exactly what Robin needs — visible methodology, honest ranges, named limitations — and the IEA piece doubles as a case study in how estimates can be manipulated by unit errors, which speaks directly to Robin's skepticism.

## Possible features

Generate several possibilities before choosing. Keep the initial notes brief. For each idea, record:

- what it would help someone learn or do
- the profiles or needs it would serve
- any evidence or implementation challenge that might affect it

### Candidates considered

**1. Image-generation bucket.** Add "an AI image" as a prompt-type option. Helps someone see that image generation costs far more per output than a text prompt. Serves Alex directly. Evidence solid (peer-reviewed, Luccioni et al.); needs its own UI row alongside existing text buckets.

**2. Video-generation bucket.** Add "a short AI video clip." Helps someone see video generation's much larger footprint. Serves Alex. Evidence real but rests on one contested model (MIT Technology Review / CogVideoX) — risks implying more certainty than warranted if presented like the other buckets.

**3. Coding-agent range instead of a single point estimate.** Replace the current single 75,000-token "agent session" bucket with a min/typical/heavy range. Helps someone see that agent sessions vary far more than other prompt types. Serves Jordan directly. Low implementation risk — a data/UI change to an existing bucket, backed by Hausfather and Couch.

**4. Project-level running total.** Let someone log multiple sessions or set a sessions-per-week multiplier to see an accumulated total. Helps Jordan see project-scale impact, not just one prompt. Design risk: unclear whether Jordan wants a log or a multiplier — unresolved in research, would need a design decision, not just a source.

**5. Video-streaming comparison.** "An hour of streaming ≈ X AI images/prompts," using the IEA figure. Helps someone place AI use alongside a familiar daily activity. Serves Alex (streams reference media) and Robin. Strong source; also works as a teaching moment on how estimates get corrected.

**6. Video-call comparison, with camera on/off.** Mirrors the bucket-comparison pattern using Obringer's range. Helps someone see how a familiar work habit (camera on vs. off) changes footprint. Serves Robin (frequent meetings) and Jordan (video calls). Evidence solid but wide range — the "rough, self-acknowledged" caveat needs to be visible, not buried.

**7. Gaming-PC comparison.** "An hour of PC gaming ≈ X." Helps Jordan place a personal habit in context. Blocked: no confirmed wattage figure, only qualitative LBNL findings — not buildable yet without more source work.

**8. Visible per-line confidence/uncertainty labels.** Tag each result inline (e.g. "high confidence," "one model, not representative," "no data — omitted") instead of leaving caveats in the collapsed methodology accordion. Helps anyone judge how much weight to put on a given number. Serves Robin most directly (visible sources, honest uncertainty) but strengthens the whole calculator. Doubles as the natural place to disclose the water-use evidence gap (idea 9) rather than needing a separate feature.

**9. Explicit "no data" water disclosure for image/video.** A narrower version of idea 8, specifically flagging that no direct water measurement exists for image/video generation rather than silently omitting it. Serves Alex specifically. Folded into idea 8 rather than built separately.

**10. "Why estimates disagree" explainer.** A short module using the IEA/Shift Project correction as a worked example of how to read a footprint figure. Serves Robin's skepticism directly. Considered as a possible component of idea 8 rather than a standalone feature.

## Source assessments

For each source, record:

- the full citation and working link
- the claim or figure the project may use
- evidence checked directly
- important limitations or uncertainty
- confidence and decision: use, use with qualifications, or reject

### Checked so far

**Luccioni, Jernite & Strubell, "Power Hungry Processing: Watts Driving the Cost of AI Deployment?", ACM FAccT 2024.** [arXiv](https://arxiv.org/html/2311.16863v3)
- Claim: per-inference energy ~0.047 Wh (text) vs. ~2.9 Wh (image), ~62x.
- Checked directly: yes, fetched the paper text.
- Limitations: benchmarked on A100 GPUs in a single AWS region; doesn't cover video; explicitly does not measure water and says so.
- Confidence: high — peer-reviewed, transparent methodology.
- Decision: **use** for the image-energy figure.

**MIT Technology Review, "We did the math on AI's energy footprint" (May 2025).** [Link](https://www.technologyreview.com/2025/05/20/1116327/ai-energy-usage-climate-footprint-big-tech/)
- Claim: 5-second AI video (CogVideoX) ≈ 3.4 million joules (~944 Wh), ~700x a single image.
- Checked directly: yes, fetched the article text.
- Limitations: one open-source model, not representative of proprietary systems (Sora, Veo); article itself says longer clips scale non-linearly, not proportionally; no water figure given.
- Confidence: medium — credible measurement, generalization uncertain.
- Decision: **use with qualifications** — state clearly this is one model's result, not a general constant.

**Water use for AI image/video generation — no direct source found.**
- Claim under consideration: some per-image/video water figure.
- Checked directly: multiple searches; every public figure traces back to an energy-to-water conversion, not measurement. Luccioni et al. name this as an open research gap themselves.
- Limitations: this is an absence-of-evidence finding, not a citable number.
- Confidence: high confidence that no credible direct figure currently exists.
- Decision: **reject** any specific water-per-image/video number; **use** the absence itself as a stated limitation if a water-related feature touches image/video generation.

**Couch, "Electricity use of AI coding agents" (Jan 2026).** [Link](https://simonpcouch.com/blog/2026-01-20-cc-impact/)
- Claim: median Claude Code session ≈ 41 Wh (24 API calls, ~592,000 tokens).
- Checked directly: yes, fetched the post.
- Limitations: self-described "napkin math"; combines GPT-4o per-token energy (one source) with Anthropic pricing ratios (a different, non-energy source) — a weak methodological link the author names himself.
- Confidence: low-medium — directionally useful, not precise.
- Decision: **use with qualifications** — cite for order-of-magnitude variance, not a precise Wh figure.

**Hausfather, "The real energy use of agentic AI" (The Climate Brink, 2026).** [Link](https://www.theclimatebrink.com/p/the-real-energy-use-of-agentic-ai)
- Claim: ~150 Wh/prompt (60–290 range), ~3.0 kWh/day (1.2–5.9 range), ~170 kWh over 8 weeks (70–330 range), from the author's own real Claude Code logs (1,138 prompts, 14,000+ model calls, 3.2B tokens).
- Checked directly: yes, fetched the post.
- Limitations: author states ~2x uncertainty from unknown cache-read energy assumptions; his own usage is heavy and explicitly "likely far above typical user distributions"; single individual, not a population sample.
- Confidence: medium-high — most rigorous personal measurement found, cross-checked against three independent per-token energy frameworks, but still one user.
- Decision: **use** — best available source for session variance and for a real multi-day/project-level total.

**Bai et al., "Tokenomics: Quantifying Where Tokens Are Used in Agentic Software Engineering" (arXiv 2601.14470).** [Link](https://arxiv.org/abs/2601.14470)
- Claim: token cost varies with task complexity; same-task runs can vary up to ~2x in token cost between cheapest and most expensive run.
- Checked directly: yes, via search-confirmed abstract/summary (not the full paper text).
- Limitations: preprint, not yet peer-reviewed; based on 30 tasks in one framework (ChatDev), not necessarily representative of other coding agents (e.g. Claude Code).
- Confidence: medium — clear on the qualitative point (variance exists even on identical tasks), less certain the ~2x figure generalizes beyond ChatDev.
- Decision: **use with qualifications** — cite for "variance exists even on the same task," with the ~2x figure attributed specifically to this study's framework.

**IEA, "The carbon footprint of streaming video: fact-checking the headlines."** [Link](https://www.iea.org/commentaries/the-carbon-footprint-of-streaming-video-fact-checking-the-headlines)
- Claim: ~36 g CO2/hour central estimate (2019 baseline); identifies a megabit/megabyte unit error plus ~35x and ~50x overestimates of data-center and network energy intensity behind the higher viral figure.
- Checked directly: yes, fetched the article.
- Limitations: 2019 baseline; uses country-average emission factors (may overstate given renewable procurement by some providers); excludes set-top boxes/consoles.
- Confidence: high — IEA is a primary international authority with a transparent, itemized error analysis.
- Decision: **use**.

**Obringer et al., "The overlooked environmental footprint of increasing Internet use," *Resources, Conservation and Recycling* (2021).** [Purdue summary](https://www.purdue.edu/newsroom/archive/releases/2021/Q1/turn-off-that-camera-during-virtual-meetings,-environmental-study-says.html)
- Claim: 1 hour of videoconferencing ≈ 150–1,000 g CO2 and 2–12 L water; camera-off cuts this ~96%.
- Checked directly: yes, fetched the Purdue summary (not the full journal article).
- Limitations: authors themselves call the estimates "rough," dependent on third-party provider data quality.
- Confidence: medium — peer-reviewed and the most-cited source in this space, self-acknowledged as rough.
- Decision: **use with qualifications** — present the range, attribute the "rough" caveat to the authors.

**LBNL Green Gaming project (Mills et al., "Toward Greener Gaming" and related reports).** [Project page](https://greengaming.lbl.gov/faqs)
- Claim under consideration: gaming-PC power draw during active play, by system tier.
- Checked directly: partial — fetched the FAQ page (qualitative findings only: "as much as four efficient refrigerators," wide variance across systems, idle power sometimes close to active-gameplay power); the underlying report PDFs did not render as extractable text.
- Limitations: no specific wattage figure confirmed yet; would need another attempt at the source PDFs or the paywalled Springer article to get hard numbers.
- Confidence: low until a specific figure is confirmed directly.
- Decision: **pending** — only use if a gaming-related feature is selected, and only after getting a direct number; reject the commercial "PC wattage guide" sites found alongside it as unreliable (marketing content, not measurement).

## Selected features

List the five selected features. Briefly explain why each was selected and how the set serves all three reference profiles. Name a few serious alternatives and explain why they were rejected.

### The five

1. **Image-generation bucket** — add "an AI image" as a prompt-type option, using the Luccioni et al. figure (~2.9 Wh/inference, ~62x text). *Professional AI use.* Serves Alex directly; solid peer-reviewed evidence.
2. **Coding-agent range** — replace the single 75,000-token "agent session" point estimate with a min/typical/heavy range, drawing on Hausfather's and Couch's measurements. *Professional AI use.* Serves Jordan directly; addresses the "prompts per day is too simplistic" complaint with real variance data.
3. **Video-streaming comparison** — "an hour of streaming ≈ X," using the IEA's 36 g CO2/hour figure. *Broader digital life.* Serves Alex (streams reference media) and Robin; also demonstrates how a viral overestimate gets corrected, which speaks to Robin's skepticism.
4. **Video-call comparison, with camera on/off** — using Obringer et al.'s range (150–1,000 g CO2, 2–12 L water/hour, ~96% cut from camera-off). *Broader digital life.* Serves Robin (frequent meetings) and Jordan (video calls in long sessions).
5. **Visible per-line confidence/uncertainty labels** — tag each calculator result inline with its confidence level and key limitation (e.g. "one model, not representative," "no data — omitted for water use here") instead of leaving this only in the collapsed methodology section. *Strongest remaining need.* Serves Robin most directly (visible sources, honest uncertainty over polish) but touches every number in the calculator, and is where Alex's water-use question gets an honest answer (no reliable figure exists for image/video water use) rather than a guessed one.

Together, the five give Alex two of his three specific concerns (image energy, honest water disclosure) plus a streaming comparison relevant to his media consumption; give Jordan both requested changes (agent-session range, video calls); and give Robin the transparency and skepticism-directed features (confidence labels, streaming correction story, videoconferencing range) that his profile calls for most.

**Serious alternatives rejected:**
- **Video-generation bucket** — real evidence, but rests on one contested model (CogVideoX) and risks looking as certain as the image figure when it isn't. Left out in favor of keeping the image figure clean; could be revisited later with a stronger caveat design.
- **Project-level running total** — would serve Jordan further, but the design question (log of sessions vs. a multiplier) is unresolved and unevidenced; a bigger implementation lift for a feature that's more UX decision than research finding.
- **Gaming-PC comparison** — would serve Jordan, but no reliable wattage figure was found; the only credible source (LBNL Green Gaming) didn't yield a usable number, and the alternative sources found were unreliable marketing content.

User approval: Review the completed research directly. Confirm that sources exist and support the claims the project will use, correct the document as needed, and explicitly approve the selected features before developing the specification. The agent cannot complete this approval on the user's behalf.

## Commands

### Start research

User: Open the project repository as your workspace, start a fresh chat, and type `start research`.

### Save transcript

Agent: After the user approves the selected features, remind them that the transcript is a deliverable and ask them to say `save transcript`. Wait for that direction.

When the user directs the agent to save the transcript, the agent saves the entire conversation in the `transcripts/` directory as `research-YYYY-MM-DD_HHMMSS.md`, marks user and agent responses clearly, and confirms the saved relative path.
