# research-finding template

Copy one spine below. Prefer **experiment** when Mine flagged a multi-condition comparison. Quality rules live in SKILL.md **Ground** — do not weaken them here.

## Default spine

Use when the session answers one claim without comparing N controlled conditions.

```markdown
# [Claim: what is true, with a number when measured]

| | |
| --- | --- |
| **Owner** | [name or mention] |
| **Go deeper** | dashboard, doc, PR, transcript (links only) |

## Question

## Answer

* **Finding:** (TLDR)
* **Confidence:** high / medium / low — one reason
* **So what:**

## Findings

### Assumptions we tested

| # | Assumption | Verdict | Evidence |
| --- | --- | --- | --- |
| 1 | | True / False / Not always / Incomplete / Rejected | |

### Results

### Key findings

* 

## Method and limits

* 

## Open questions

* 

## Recommendation

None / research complete — **or**, only if the transcript discussed follow-ups:

* Decision / owner
* Near-term next steps (from the session only): …

## Review

* [ ] Owner named
* [ ] Ready for human review
```

## Experiment spine

Use when the session compares the **same measurement** across **N conditions** (caps, modes, scopes, configs). One section per condition. Do **not** flatten into Assumptions → Results → Key findings.

```markdown
# [Claim: what is true across conditions, with the decisive number]

| | |
| --- | --- |
| **Owner** | [name or mention] |
| **Go deeper** | dashboard, doc, PR, transcript (links only) |

## Question

## Answer

* **Finding:** (TLDR: condition → verdict, include decisive number)
* **Confidence:** high / medium / low — one reason
* **So what:**

---

## 1. [Condition A]

### Verdict

[One sentence: prefer X / types tie / invalid comparison / …]

### Analysis

| | Arm 1 | Arm 2 |
| --- | ---: | ---: |
| [metric] | | |
| [metric] | | |

[Optional smoking-gun check table when the claim is a gap or equality:]

| Check | Result |
| --- | --- |
| [e.g. Types equal?] | |
| [e.g. Counts equal?] | |
| [e.g. Gap composition] | |

* **Types / Counts / Why:** short bullets; facts only. Interpretation stays in Verdict / Answer.

---

## 2. [Condition B]

### Verdict

### Analysis

(same pattern)

---

## 3. [Condition C]

### Verdict

### Analysis

(same pattern)

---

## Method and limits

* 

## Recommendation

None / research complete — **or**, only if the transcript discussed follow-ups:

* Decision / owner
* Near-term next steps (from the session only): …

## Review

* [ ] Owner named
* [ ] Ready for human review
```

## Fill notes

* Lead with the concrete claim in the title and Finding; put setup in Question only.
* **Default spine:** Assumptions one row per prior belief; drop when none. Results / Key findings: measured outcome first. Include mined mechanisms with counts in Key findings.
* **Experiment spine:** one section per condition; each has Verdict then Analysis. Put the shareable proof table in Analysis (scorecard and/or same-conclusion / gap-composition). Drop Assumptions / Results / Key findings unless the session also needs a short cross-condition rollup (prefer a table inside the decisive section).
* Recommendation: do not invent next steps. Closed research → None. Only list actions the session actually discussed.
* Body budget about 600 words for default. For experiment spines, keep prose short; **do not cut the smoking-gun table** to hit the budget.
