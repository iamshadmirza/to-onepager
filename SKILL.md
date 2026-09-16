---
name: to-onepager
description: Distill a Cursor conversation into a one-pager and publish to the user's configured destination (local, Google Docs, or Confluence).
argument-hint: "Transcript path or paste (optional). Otherwise use the current conversation. Say 'setup' to reconfigure publish destination."
disable-model-invocation: true
---

Turn a conversation into a one-pager: one **claim**, grounded evidence, easy to read and follow, configured publish destination.

**Input:** transcript path/paste if given; else current conversation. `setup` / `reconfigure` → run Setup even when `config.md` exists.

**Config:** `config.md` beside this `SKILL.md` (local to the install). Shape: [config.example.md](config.example.md).

**Page types (live):** `research-finding` | `proposal`. Prefer research-finding when unclear. Ask once if both fit. Announce the choice before drafting.

## Steps

### 0. Setup

If `config.md` is missing or the user asked to reconfigure:

1. Ask destination: `local` | `google-docs` | `confluence` (exactly one).
2. Collect fields for that destination (see config.example.md). Confluence requires `confluence_folder_url`.
3. Write `config.md` in this skill directory.
4. Tell the user it applies to every future run; say `setup` to change it.

**Completion:** valid `config.md` with a known `destination`. Setup-only runs stop here unless a one-pager was also requested.

### 1. Mine

Read the full input. Working notes only (do not show the user):

* Session intent: empirical claim vs decision bet
* The question or problem the whole session served
* Assumptions tested (lead with corrections / what changed)
* Grounded facts (sourced) vs unsourced claims (medium confidence)
* Method, limits, open questions, next actions (product/research decisions, not local runbooks)

If intent leans **research-finding**, also capture:

* Explanatory mechanisms with counts (dominant signal, FP pattern, counterfactual)
* User-elevated findings ("put this in Key findings")
* **Experiment?** If the session compares the same measurement across N conditions (caps, modes, scopes, configs, A/B arms), list each condition and the smoking-gun table (scorecard, gap composition, equality check). Flag `fill: experiment`.

If intent leans **proposal**, also capture:

* Problem / who hurts, recommended bet, why now, approach, alternatives (with sources when present), risks
* Near-term next steps discussed in the session

**Completion:** intent signals, corrections, sourced facts, and branch-specific notes captured. No interpretation yet.

### 2. Route

Pick exactly one page type from the catalog below. Announce: `Page type: …`.

| Page type | Use when | Prefer the other when |
| --- | --- | --- |
| `research-finding` | Evidence answered "what is true?" | Session is mainly a bet with little new evidence |
| `proposal` | Session frames a bet (problem, path, why, how) | Session is pure measurement with no recommended change |

Hold verification and architecture for later; if the session is only those shapes, ask which live type is closest or stop.

**Completion:** one page type chosen and announced.

### 3. Distill

Load the template for the routed type (context pointer — read only that file):

* `research-finding` → [templates/research-finding.md](templates/research-finding.md)
* `proposal` → [templates/proposal.md](templates/proposal.md)

Fill that spine for **easy reading**: a cold reader should get the claim in seconds and follow one thread per section.

**research-finding fill path**

* **Default:** Assumptions → Results → Key findings (template default spine).
* **Experiment** (when Mine flagged `fill: experiment`): use the template **experiment spine**. Announce: `Fill path: experiment`.
  * **Finding ladder:** stacked bullets (one verdict per condition) plus an optional bottom line; do not crush N conditions into one mega-sentence.
  * **Context before conditions (optional):** after Answer, a short block that defines arms or metrics (e.g. types vs instances) so tables are not misread. Use only when Question is not enough. Any clear heading is fine; omit when unneeded. Do not invent a mandatory “What we compare” section.
  * **Condition sections:** one top-level section per condition; each is **Verdict** then **Analysis**. Title the section by **fairness or outcome** (e.g. “Fair A/B: cap removed”), not only the raw knob (“MaxMessages = 100”). Put the shareable proof in Analysis (scorecard and/or same-conclusion / gap-composition table).
  * **Replication:** nest under the decisive/fair condition (e.g. Multi-session check); do not add a top-level condition section just for repeats.
  * Do **not** flatten an N-condition experiment into Assumptions → Results → Key findings.

**Readability (every page)**

* **Lead with the concrete thing:** title and Finding open with the number, verdict, or bet. Context follows; it does not open the page. For experiments, Finding may carry the stake as a bullet ladder; the title may name the comparison if Finding holds the numbers.
* **Explain after the example:** in Results, Key findings, Analysis, and How, state the measured outcome or chosen path first, then one short line of context if needed.
* **One job per section:** each heading does one job. If a section argues two things, split or cut.
* **Answer** a cold reader can use without caring about page type: Finding (TLDR) / Confidence / So what
* Title is the **claim** (include a measured number when the transcript has one; experiments may put the number in Finding instead)
* Recommendation: only actions discussed in the session. If the session only answered a question (closed research, no product bet), write **None** (or "research complete; no follow-up") — do **not** invent next steps, doc TODOs, reviewer homework, or a "~1 week" plan.
* Header: Owner, Go deeper
* Review section present

Owner: resolve a real person. For Confluence destinations use Atlassian mentions when publishing ([publish.md](publish.md)). Otherwise display name. Ask if unknown; `TBD` only if deferred.

**Completion:** routed spine filled (default or experiment); chrome complete; Owner resolved or explicit `TBD`; title and Finding lead with the concrete claim.

### 4. Ground

Fail and edit until every check passes. This step is the single source of truth for quality (templates do not restate these rules).

**Every page**

* Every factual cell/bullet traces to the transcript
* No unmeasured magnitudes
* Cold-reader Answer works without reading page type; Finding is the TLDR and leads with the concrete claim (experiment Finding may be a bullet ladder)
* Title leads with the claim (not a topic or soft header); experiments may name the comparison in the title if Finding holds the stake/numbers
* Body matches the routed page type (no hybrid spine)
* One job per section; no section that both explains and recommends
* Chrome complete (Owner, Go deeper)
* Go deeper / recommendations stay free of local runbook clutter
* Confidence matches evidence; title matches measured numbers when present (or Finding does, for experiment ladders)
* **One-page budget:** about 600 words of prose; if over, cut the least important ideas (do not shrink type or stuff an appendix). **Exception:** experiment smoking-gun tables (scorecard, gap composition, equality check) are not cut to hit the budget; shorten bullets around them instead.
* **Plain pass** on Answer + Recommendation: active voice, short words, cut needless words and jargon
* **No templated bridges:** cut phrases like "in today's landscape," "game-changer," "here's why this matters," or a closing question added only for engagement
* **No soft recap:** Recommendation does not rephrase Finding
* **No invented follow-ups:** next steps only if the transcript discussed them; otherwise Recommendation is None / research complete
* Every section adds something new; delete filler that only restates an earlier section

**research-finding**

* Default spine: Findings hold facts only (interpretation stays in Answer); Results and Key findings lead with the measured outcome; mechanisms with counts and user elevations appear in Key findings; Assumptions have verdicts when prior beliefs existed
* Experiment spine: Finding ladder; optional short context after Answer only when needed; one section per condition titled by fairness/outcome; each has Verdict then Analysis with the shareable proof table; replication nested under the decisive condition; no Assumptions/Results/Key findings dump
* Closed understanding sessions often have Recommendation: None

**proposal**

* Problem, What, Why, How present and non-empty
* Finding states the recommended bet up front
* How leads with the chosen path, then options
* Alternatives table present (at least "do nothing"); each option has a why-not and a source or link when the transcript had one
* How names the chosen path; if the session compared options, list them under How or Alternatives with sources
* Near-term next steps only when the session named them; otherwise say none rather than inventing a week plan

**Completion:** all applicable checks pass.

### 5. Publish

Read `config.md`. If missing or invalid, run Setup, then continue.

Follow [publish.md](publish.md) for the configured `destination`.

**Completion:** published to the configured destination, or local copy saved with the destination's connect prompt. Page type announced; Owner named or `TBD`.
