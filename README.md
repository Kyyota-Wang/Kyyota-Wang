# Yunlong (Mark) Wang

**Director, AI Scientist at IQVIA** · Ph.D. ECE, Stony Brook · M.B.A., Boston University · IEEE Senior Member

I lead an AI/ML portfolio and a team that builds it — and I still write the code.
Most of what I ship is behind an enterprise firewall, so the repositories here are the
ones I built on my own time to keep the hands-on half honest: real deployments, real
users, real evaluation numbers including the ones that are not flattering.

[LinkedIn](https://linkedin.com/in/yunlongwangsbu) ·
[Google Scholar](https://scholar.google.com/citations?user=xHv-7cQAAAAJ) ·
markyunlongwang@gmail.com · Malvern, PA

---

## What I build

Applied AI in regulated, evidence-heavy domains — pharmaceutical commercial analytics,
clinical development, and regulatory workflow. The recurring problem in this space is not
model quality. It is **whether you can defend the output**: where each value came from,
what the system refused to decide, and how you know it is right.

That constraint shows up in both projects below.

---

## Projects

### 🐝 [INDHive](https://github.com/Kyyota-Wang/indhive) — automated FDA IND Module 1 preparation

**[indhive.com](https://indhive.com)** · Python · TypeScript · Cloudflare Workers

Sponsor, product, protocol and plan records go in; a deterministic pipeline normalises them
into one canonical record and maps that into FDA Module 1 artifacts — Form 1571, the 1.20
General Investigational Plan, a Module 1 gap analysis, a drafted cover letter.

Two design decisions carry the project:

- **Every value keeps the source record it came from.** Provenance is not a logging
  afterthought; it is part of the data structure.
- **Where two source records disagree, the field is left empty and flagged.** The system
  does not choose. In a regulatory filing, a plausible guess is worse than a blank.

The cover letter is drafted from an approved-fact whitelist and then checked against those
facts for unsupported claims. The assistant on the site never states a case fact that did
not come from a tool call, never resolves a conflict, and never claims filing readiness.

**How I know it works:** a clinical partner built a real-shaped input package for a
programme of his own and sent his own answers with it — a hand-filled Form 1571, a ten-entry
gaps log, and a traceability matrix declaring 23 numbers that must agree across his dossiers.
The pipeline ran on his input and never saw his answers. Four comparison views put the two
side by side; four of his ten gaps came back independently.

*Every case is fictional and nothing here is submittable to FDA. It is a proof of concept,
not regulatory software — and the README says so before you ask.*

---

### 🍀 [CloverAI Lab](https://github.com/Kyyota-Wang/cloverailab) — GRE Analytical Writing reviewer

**[cloverailab.com](https://cloverailab.com)** · TypeScript · Cloudflare Workers · Claude

An essay reviewer built on LLM-as-judge with an explicit ETS rubric and official scored
anchors, plus a writer agent. No fine-tuning — 30 ground-truth essays cannot train a scoring
model, and pretending otherwise is the usual failure mode in this category.

**Measured, not asserted** — leave-one-out over the gold set:

| Gold set | n | QWK | Within 1 band | Bias |
|---|---:|---:|---:|---:|
| ETS official anchors | 18 | **0.825** | 83.3% | −0.33 |
| All (ETS + teacher-scored) | 26 | **0.774** | 80.8% | −0.48 |

The negative bias is real: the reviewer scores slightly harsher than human raters. It is in
the repository along with the worst misses, because a benchmark you can only pass is not a
benchmark.

**The part I am most pleased with is a data bug.** Seven of the eighteen official Issue
essays in the public corpus had rater commentary spliced into the essay text — one
"1,039-word" score-6 response is 775 words of essay and 264 words of a grader saying the
response demonstrates facility with the conventions of standard written English. Left alone,
the highest-scoring anchors would have taught the model that *sounding like a grader* is what
a 6 looks like. The extractor re-derives them from the source PDFs and separates the two, and
there is an assertion in the validator that fails if it ever regresses.

---

### 📐 [Expert-calibrated domain scoring](https://github.com/Kyyota-Wang/expert-calibrated-scoring) — scoring that was calibrated, then checked

Python · Pydantic · structured output

Scores a job description against a fixed ontology of 44 life-science domains,
1–10 with a written reason per score. The scoring is the easy part; the reason
this one is here is what surrounds it.

**The calibration is an offset, and it is written down.** A clinical panel
hand-scored a seed set to establish the baseline. Aligning the model to it
revealed that the panel judged relevance about **one band more inclusively** than
the model does by default — where a domain sits in the macro background of a
senior role, the panel called it moderately relevant and the model called it
weak. That offset is stated in plain language in the rubric, along with the
specific disagreements found during calibration, rather than being absorbed
invisibly from a few-shot set. It is a thumb on the scale, deliberately, and a
reader can disagree with it.

**Then it was checked.** Two independent scoring runs were compared across
~1,000 jobs × 44 domains. The first version of that analysis reported band
agreement alone, which flatters when scores cluster; it now reports quadratic
weighted kappa alongside a signed mean difference, so *"these two disagree"* is
separable from *"one sits a point above the other"* — the second being a
calibration offset, and fixable.

---

## Research

42 peer-reviewed publications · 858 citations · h-index 15 · 4 granted U.S. patents, 2 pending

Recent work in **IEEE TPAMI**, **NeurIPS**, and **CVPR** (2024–2026), on adversarial
robustness and distributed learning. Ph.D. dissertation: *Distributed Bayesian Learning in
Multi-Agent Systems* (advisor: Petar M. Djurić).

Primary inventor on patented HCP-level promotion response and multichannel media attribution
methods now used in commercial pharmaceutical measurement.

→ [Google Scholar](https://scholar.google.com/citations?user=xHv-7cQAAAAJ)

**Papers with public code** — released by the first authors:

| Paper | Venue | Code |
|---|---|---|
| Boosting the Transferability of Adversarial Attack on Vision Transformer with Adaptive Token Tuning | NeurIPS 2024 | [MisterRpeng/ATT](https://github.com/MisterRpeng/ATT) |
| TRM-UAP: Enhancing the Transferability of Data-Free Universal Adversarial Perturbation via Truncated Ratio Maximization | ICCV 2023 | [RandolphCarter0/TRMUAP](https://github.com/RandolphCarter0/TRMUAP) |
| SUOD: Accelerating Large-Scale Unsupervised Heterogeneous Outlier Detection | MLSys 2021 | [yzhao062/SUOD](https://github.com/yzhao062/SUOD) |

---

## Day job

At IQVIA I hold technical and delivery leadership for an AI/ML portfolio in pharmaceutical
commercial analytics, with a team spanning data science, ML engineering, data engineering
and software engineering. The work I am proudest of there is the unglamorous kind:

- **Violet** — the enterprise AI platform the organization's data science teams build on;
  17 applications, 50+ active builders, consolidated from several overlapping stacks.
- **MCP Factory** — a governed registry for MCP servers and AI skills serving a ~500-person
  business unit: submission templates, an automated review step, a human approval gate, and
  active curation to retire duplicate capabilities.
- **A responsible-AI operating model** — risk tiering, approval gates, evaluation thresholds,
  human-in-the-loop rules and auditability — with a remit covering every AI platform the unit
  uses, including ones other teams built. Run in standing partnership with information
  security, data privacy, and legal.
- **An evaluation stack** that decides whether things ship: benchmark sets drawn from
  historically scored data, release thresholds, expert review fed back into the agent, and
  LLM-as-judge with multi-agent cross-scoring.

None of that is on GitHub. The two projects above are how I keep the skill.

---

## Stack

**Languages** Python · TypeScript · SQL
**AI** Claude / Anthropic API · Gemini · LangGraph · MCP · DSPy · Bedrock · evaluation harnesses
**Data & platform** Databricks · Snowflake · Spark · Azure · AWS · Cloudflare Workers
**Serving** FastAPI · Streamlit · React
