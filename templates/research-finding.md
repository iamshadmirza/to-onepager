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
# [Comparison or claim; numbers may live in Finding]

| | |
| --- | --- |
| **Owner** | [name or mention] |
| **Go deeper** | dashboard, doc, PR, transcript (links only) |

## Question

## Answer

* **Finding:**
  * [Condition 1 → verdict]
  * [Condition 2 → verdict]
  * [Condition 3 → verdict]
  * **Bottom line:** …
* **Confidence:** high / medium / low — one reason
* **So what:**

---

## [Optional short context]

Only when Answer/Question are not enough for a cold reader (define arms, metrics like types vs instances, how to read tables). Pick any clear heading, or fold into Question. Skip if unneeded.

---

## 1. [Fairness or outcome title, e.g. Under the current cap]

### Verdict

[One sentence: prefer X / types tie / not a fair contest / …]

### Analysis

| | Arm 1 | Arm 2 |
| --- | ---: | ---: |
| [metric] | | |
| [metric] | | |

* **Types / Counts / Why:** short bullets; facts only. Interpretation stays in Verdict / Answer.

---

## 2. [Next condition, outcome-framed]

### Verdict

### Analysis

(same pattern)

---

## 3. [Decisive / fair condition]

### Verdict

### Analysis

| | Arm 1 | Arm 2 |
| --- | ---: | ---: |
| [metric] | | |

[Smoking-gun check when the claim is a gap or equality:]

| Check | Result |
| --- | --- |
| [e.g. Types equal?] | |
| [e.g. Counts equal?] | |
| [e.g. Gap composition] | |

### [Replication nest, e.g. Multi-session check]

Only if the transcript repeated the fair test. Keep under this section; do not promote to a top-level condition.

| Check | Result |
| --- | --- |
| | |

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
* **Experiment spine:** Finding as a bullet ladder. Optional short context after Answer only when tables need a legend. Title condition sections by fairness/outcome, not only raw knobs. Put the shareable proof table in Analysis. Nest replication under the decisive condition. Drop Assumptions / Results / Key findings.
* Recommendation: do not invent next steps. Closed research → None. Only list actions the session actually discussed.
* Body budget about 600 words for default. For experiment spines, keep prose short; **do not cut the smoking-gun table** to hit the budget.
