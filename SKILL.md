---
name: to-onepager
description: Distill a Cursor conversation into a one-pager and publish to the user's configured destination (local, Google Docs, or Confluence).
argument-hint: "Transcript path or paste (optional). Otherwise use the current conversation. Say 'setup' to reconfigure publish destination."
disable-model-invocation: true
---

Turn a conversation into a one-pager: one **claim**, grounded evidence, configured publish destination.

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

Fill that spine. Every page uses the same **chrome**:

* Header: Status, Owner, Reviewer, Updated, Page type, Go deeper
* **Answer** a **cold reader** can use without caring about page type: Finding (TLDR) / Confidence / So what
* Title is the **claim** (include a measured number when the transcript has one)
* Recommendation names owners, the decision, and **near-term next steps** (what happens in about a week)
* Review section present; Status stays short of Reviewed until a named Reviewer exists

Owner / Reviewer: resolve real people. For Confluence destinations use Atlassian mentions when publishing ([publish.md](publish.md)). Otherwise display names. Ask if unknown; `TBD` only if deferred.

**Completion:** routed spine filled; chrome complete; Owner/Reviewer resolved or explicit `TBD`.

### 4. Ground

Fail and edit until every check passes. This step is the single source of truth for quality (templates do not restate these rules).

**Every page**

* Every factual cell/bullet traces to the transcript
* No unmeasured magnitudes
* Cold-reader Answer works without reading page type; Finding is the TLDR
* Body matches the routed page type (no hybrid spine)
* Chrome complete; Reviewed requires a named Reviewer
* Go deeper / recommendations stay free of local runbook clutter
* Confidence matches evidence; title matches measured numbers when present
* **One-page budget:** about 600 words; if over, cut the least important ideas (do not shrink type or stuff an appendix)
* **Plain pass** on Answer + Recommendation: active voice, short words, cut needless words and jargon

**research-finding**

* Findings hold facts only (interpretation stays in Answer)
* Mechanisms with counts and user elevations appear in Key findings
* Assumptions have verdicts when prior beliefs existed

**proposal**

* Problem, What, Why, How present and non-empty
* Finding states the recommended bet
* Alternatives table present (at least "do nothing"); each option has a why-not and a source or link when the transcript had one
* How names the chosen path; if the session compared options, list them under How or Alternatives with sources

**Completion:** all applicable checks pass.

### 5. Publish

Read `config.md`. If missing or invalid, run Setup, then continue.

Follow [publish.md](publish.md) for the configured `destination`.

**Completion:** published to the configured destination, or local copy saved with the destination's connect prompt. Page type announced; Reviewer named or `TBD`.
