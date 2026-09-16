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

### Jordan — coding agents, project-level totals

**Evidence:**
- The current calculator's "agent session" bucket uses a single ~75,000-word (~100,000-token) benchmark. Real coding-agent sessions vary far more than that: an informal analysis of a developer's own Claude Code logs found a *median* session used ~41 Wh across 24 model calls and ~592,000 tokens, while large sessions (heavy subagent use, big data-analysis tasks) reached ~600 Wh and ~10 million tokens ([Couch, "Electricity use of AI coding agents," 2026](https://simonpcouch.com/blog/2026-01-20-cc-impact/)). That's roughly a 15x spread between "typical" and "heavy" sessions — a single point estimate hides this.
- A peer-reviewed-adjacent measurement study (arXiv preprint) found agentic coding tasks consume on the order of 1,000x the tokens of an ordinary chatbot turn, and that token use for the *same task* can vary up to 30x run-to-run because agent trajectories are stochastic ([Bai et al., "Tokenomics," 2026](https://arxiv.org/html/2601.14470v1)).
- **Assumption needing checking:** whether Jordan would actually want a running project-level total (sum of sessions) versus just a wider single-session range. Not yet evidenced — this is a design question, not a research one.

**Implication:** Jordan's complaint that "prompts per day" is too simplistic is well supported — session size genuinely varies by an order of magnitude or more, and that variance is inherent to agent workloads, not just a modeling gap.

### Alex — image and video generation, water use

**Evidence:**
- The calculator's existing model data (EcoLogits) only covers text models. Peer-reviewed measurement (FAccT 2024) found per-inference energy of ~0.047 Wh for text generation but ~2.9 Wh for image generation — roughly 60x more per output ([Luccioni, Jernite & Strubell, "Power Hungry Processing," 2024](https://dl.acm.org/doi/10.1145/3630106.3658542)).
- Video generation is far higher again: measured energy for a 5-second clip from a specific open model (CogVideoX) was reported at ~3.4 million joules (~944 Wh) — over 700x a single image — with an older, lower-quality version of the same model at ~109,000 joules (~30 Wh) ([MIT Technology Review, May 2025](https://www.technologyreview.com/2025/05/20/1116327/ai-energy-usage-climate-footprint-big-tech/), reporting Luccioni's CodeCarbon measurements).
- **Important uncertainty:** this video figure is for one model family, not a general video-generation constant, and even specialists are unsure how far it generalizes. Andy Masley — whose work the current calculator already relies on — wrote that he received pushback from readers skeptical the number is that large, and separately criticized the MIT report's *presentation* (a scenario where video is 98% of a daily total) as likely to mislead readers about routine chatbot use, even though he doesn't dispute the raw figure ([Masley, "Reactions to MIT Technology Review's report," 2025](https://andymasley.com/writing/reactions-to-mit-technology-reviews/)). This is a direct, on-topic example of the kind of "represent uncertainty honestly" the brief and Alex's water-use concern both call for.
- No water-use figures for image/video generation were found yet with a comparable level of verification — still open.

**Implication:** there's real, citable evidence that image and especially video generation cost far more per output than text — but the video number rests on one model and is contested even among people sympathetic to it. Any feature using it needs a visible caveat, not a bare number.

### Robin — broader digital life, skepticism, honest uncertainty

**Evidence, and a genuine conflict worth keeping:**
- **Video streaming:** The IEA's corrected analysis puts one hour of Netflix-style streaming at ~36 g CO2 (2019 baseline), and traces earlier viral estimates (The Shift Project's ~3.2 kg/hour) to a specific, identified error — the authors mixed up megabits and megabytes, overestimated data-center energy intensity ~35x, and overestimated network energy ~50x ([IEA, "The carbon footprint of streaming video: fact-checking the headlines"](https://www.iea.org/commentaries/the-carbon-footprint-of-streaming-video-fact-checking-the-headlines)). This is a strong, citable example of how wildly digital-footprint estimates can be manipulated by unit errors — useful for Robin's skepticism, in either direction.
- **Video calls:** here the sources actively disagree, not just in magnitude but in what they're measuring. Purdue's peer-reviewed study (the most-cited academic source in this space) found one hour of videoconferencing emits 150–1,000 g CO2 and 2–12 L of water, with turning off the camera cutting the footprint ~96% ([Obringer et al., "The overlooked environmental footprint of increasing Internet use," *Resources, Conservation and Recycling*, 2021](https://www.purdue.edu/newsroom/archive/releases/2021/Q1/turn-off-that-camera-during-virtual-meetings,-environmental-study-says.html); the paper itself calls its own estimates "rough"). A 2026 arXiv preprint, by contrast, measured the camera-on/off *marginal* difference alone at just ~0.036 g CO2e/hour — four orders of magnitude smaller ([Mortas, "Assessing the Carbon Footprint of Virtual Meetings," 2026](https://arxiv.org/pdf/2601.06045)). The likely reason is scope: Purdue's number is a full-system estimate (device + network + data center + amortized manufacturing) while the preprint isolates only the camera's incremental contribution — but I have not confirmed this reconciliation, and the preprint is unreviewed and single-author.
- **Implication:** rather than picking one video-call number, this is a case where showing the range and explaining *why* estimates disagree (system boundary, not just measurement error) may serve Robin's stated need — plain language, visible sources, honest uncertainty — better than a single figure would.
- **Assumption needing checking:** whether Robin's skepticism is really about the company's motives for building the calculator, or about AI/tech-industry claims in general. Not yet evidenced from any of the above — worth watching for as we go, since it affects tone more than figures.

## Possible features

Generate several possibilities before choosing. Keep the initial notes brief. For each idea, record:

- what it would help someone learn or do
- the profiles or needs it would serve
- any evidence or implementation challenge that might affect it

## Source assessments

For each source, record:

- the full citation and working link
- the claim or figure the project may use
- evidence checked directly
- important limitations or uncertainty
- confidence and decision: use, use with qualifications, or reject

### Checked so far

**Luccioni, Jernite & Strubell, "Power Hungry Processing: Watts Driving the Cost of AI Deployment?", ACM FAccT 2024.** [DOI](https://dl.acm.org/doi/10.1145/3630106.3658542)
- Claim: per-inference energy of ~0.047 Wh (text generation) vs. ~2.9 Wh (image generation).
- Checked directly: yes, abstract/summary confirmed via ACM listing and corroborating MIT Technology Review coverage.
- Limitations: benchmark-task energy, not a specific commercial model; doesn't cover video.
- Confidence: high — peer-reviewed, widely cited, methodology transparent (CodeCarbon).
- Decision: **use** for an image-generation feature.

**MIT Technology Review, "We did the math on AI's energy footprint" (May 2025).** [Link](https://www.technologyreview.com/2025/05/20/1116327/ai-energy-usage-climate-footprint-big-tech/)
- Claim: 5-second AI video ≈ 3.4 million joules (~944 Wh) for a newer CogVideoX version; ~109,000 J for an older, lower-quality version.
- Checked directly: yes, plus the primary researcher's (Luccioni) own follow-up commentary via Andy Masley's reaction piece.
- Limitations: single model family (CogVideoX), not representative of all video generators (e.g., commercial closed models like Sora or Veo); not independently peer-reviewed at time of writing; Masley notes real skepticism about the magnitude even from people who trust Luccioni's other numbers.
- Confidence: medium — credible measurement, but generalization is uncertain.
- Decision: **use with qualifications** — must state it's one model's measured result, not a general video-generation constant, and flag the contested magnitude.

**Andy Masley, "Reactions to MIT Technology Review's report on AI and the environment" (2025).** [Link](https://andymasley.com/writing/reactions-to-mit-technology-reviews/)
- Claim: used here as a limitations/uncertainty source, not a figure source — documents expert disagreement over the video number and criticizes misleading presentation of relative scale.
- Checked directly: yes.
- Limitations: opinion/commentary piece, not a study; Masley is also the source of most of the existing calculator's methodology, so not an independent check on his own work — but here he's critiquing someone else's report, not his own.
- Confidence: medium-high for the specific claim it's used to support (that experts themselves flag this uncertainty).
- Decision: **use** as an uncertainty citation, not a data source.

**IEA, "The carbon footprint of streaming video: fact-checking the headlines."** [Link](https://www.iea.org/commentaries/the-carbon-footprint-of-streaming-video-fact-checking-the-headlines)
- Claim: ~36 g CO2/hour central estimate for 2019 streaming; identifies specific unit/methodology errors behind higher viral estimates.
- Checked directly: yes.
- Limitations: 2019 baseline (grids and device efficiency have shifted since); doesn't cover 4K/large-screen high end explicitly in the estimate.
- Confidence: high — IEA is a primary international authority with transparent error analysis.
- Decision: **use**.

**Obringer et al., "The overlooked environmental footprint of increasing Internet use," *Resources, Conservation and Recycling* (2021).** [Purdue summary](https://www.purdue.edu/newsroom/archive/releases/2021/Q1/turn-off-that-camera-during-virtual-meetings,-environmental-study-says.html)
- Claim: 1 hour of videoconferencing ≈ 150–1,000 g CO2 and 2–12 L water; camera-off cuts this ~96%.
- Checked directly: partial — read via Purdue's official summary of the peer-reviewed paper, not the journal article itself yet.
- Limitations: authors themselves call the estimates "rough," dependent on third-party provider data; wide range reflects real uncertainty, not sloppiness.
- Confidence: medium — peer-reviewed and the most-cited source in this space, but self-acknowledged as rough, and I have not yet read the full paper directly.
- Decision: **use with qualifications** — present the range, attribute the "rough" caveat to the authors themselves.

**Mortas, "Assessing the Carbon Footprint of Virtual Meetings: A Quantitative Analysis of Camera Usage" (arXiv preprint, 2026).** [Link](https://arxiv.org/pdf/2601.06045)
- Claim: camera-on marginal cost ≈ 0.036 g CO2e/hour — far smaller than Purdue's full-call estimate.
- Checked directly: yes.
- Limitations: unreviewed preprint, single author; appears to measure only the camera's incremental contribution rather than the full call, which likely (not confirmed) explains the gap with Obringer et al. rather than one source being simply wrong.
- Confidence: low-medium — useful as an illustration of scope-dependent disagreement, not as a standalone figure.
- Decision: **use with qualifications** — pair with Obringer et al. to illustrate that estimates diverge by system boundary, don't present alone as "the" camera-off saving.

**Couch, "Electricity use of AI coding agents" (2026).** [Link](https://simonpcouch.com/blog/2026-01-20-cc-impact/)
- Claim: median Claude Code session ≈ 41 Wh (24 calls, ~592k tokens); large sessions up to ≈ 600 Wh (~10M tokens).
- Checked directly: yes, including the author's own stated methodology and caveats.
- Limitations: self-described as "napkin math"; back-solves per-token energy from a different lab's (Epoch AI's) ChatGPT-4o estimate combined with Anthropic's *pricing* ratios — pricing is not energy, so this step is a real weak link the author himself flags as "pretty silly."
- Confidence: low-medium — directionally useful (shows order-of-magnitude session variance) but not solid enough to hang a specific number on without qualification.
- Decision: **use with qualifications** — cite for the *range/variance* claim, not for a precise Wh figure.

**Bai et al., "Tokenomics: Quantifying Where Tokens Are Used in Agentic Software Engineering" (arXiv preprint, 2026).** [Link](https://arxiv.org/html/2601.14470v1)
- Claim: agentic coding tasks use ~1,000x the tokens of a chatbot turn; same-task token use varies up to 30x run-to-run.
- Checked directly: partial — read via search summary, not the full paper yet.
- Limitations: preprint, not yet peer-reviewed; "1,000x" and "30x" figures need to be confirmed against the paper's actual text before citing.
- Confidence: low until read directly.
- Decision: **pending** — needs a direct read before use.

## Selected features

List the five selected features. Briefly explain why each was selected and how the set serves all three reference profiles. Name a few serious alternatives and explain why they were rejected.

User approval: Review the completed research directly. Confirm that sources exist and support the claims the project will use, correct the document as needed, and explicitly approve the selected features before developing the specification. The agent cannot complete this approval on the user's behalf.

## Commands

### Start research

User: Open the project repository as your workspace, start a fresh chat, and type `start research`.

### Save transcript

Agent: After the user approves the selected features, remind them that the transcript is a deliverable and ask them to say `save transcript`. Wait for that direction.

When the user directs the agent to save the transcript, the agent saves the entire conversation in the `transcripts/` directory as `research-YYYY-MM-DD_HHMMSS.md`, marks user and agent responses clearly, and confirms the saved relative path.
