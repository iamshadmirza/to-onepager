# Uncapped A vs B: same types; only Drift+Dragging counts differ (gap 80)

| | |
| --- | --- |
| **Owner** | [@Mohammad Shad Mirza](https://do-internal.atlassian.net/wiki/people/712020:bd38e8db-49a4-4661-8101-5f45c16ed6a9) |
| **Go deeper** | [Gold A/B one-pager](https://do-internal.atlassian.net/wiki/spaces/FI/pages/3469246465/Session+vs+chunk+grading+more+signals+more+accurate) · [Metabase dashboard 4](https://signals-metabase.feedback-intelligence.svc.flux.nyc3.internal.digitalocean.com:3443/dashboard/4-chat-quality-chunks-vs-whole-conversation?session_id=01a05bf8-e955-7182-b5af-9dcdc6abcc7b&team_id=39449946) · local test `signal-engine/maxmessages_session_local_test.go` |

## Question

On long session `01a05bf8-…` (team `39449946`, 1540 dialogues → 4202 ShareGPT msgs, 239 segments), how do V1 segment-compose (**A**) and V2 session (**B**) compare at MaxMessages **100**, **500**, and with the **limit removed**?

## Answer

* **Finding:** **100 → A wins** (B is a last-100 tail). **500 → types tie, counts still favor A for coverage** (B is a wider tail). **Uncapped → same type conclusion**; counts differ only on Drift (51→5) + Dragging (35→1); gap **80**. Uncapped B (**1236** / 1540 user turns) = stored prod B.
* **Confidence:** High (same fixture; `TestMaxMessages100Vs500_Session01a05bf8` + `TestUncappedSegmentVsSession_Session01a05bf8`).
* **So what:** Default 100 is unsafe for session SoT on long chats. 500 fixes types, not full counts. Removing the limit is what makes A and B agree on “what’s wrong.”

---

## 1. Segment vs session at MaxMessages = 100

### Verdict

**Prefer A (segment compose).** B at 100 is not a whole-session grade; it is a last-100 ShareGPT tail (~2% of the stream). Do not use B100 as session SoT on this class of chat.

### Analysis

| | A (segments) | B (session) |
| --- | ---: | ---: |
| Instances | 1312 | 30 |
| Types | 22 | 17 |
| User turns (in-window) | all segments | 34 |
| Drift / Dragging | 51 / 35 | 1 / 1 |

* **Types:** A has the full bag; B misses five types (Clarification, Rephrase, ExhaustionNetwork, ExhaustionRateLimit, FailureStateError).
* **Counts:** B’s low totals are mostly **unseen chat**, not “less inflation.” Comparing A1312 vs B30 as accuracy is invalid.
* **Why:** `AnalyzeShareGPT` keeps last N only. Segments usually fit under 100 msgs, so A still covers the whole timeline; B does not.

---

## 2. Segment vs session at MaxMessages = 500

### Verdict

**Types tie (22=22). Prefer A for full-chat coverage; treat B500 as a wider tail grade, not a finished session.** Raising 100→500 is not enough to call B count-complete (140 vs uncapped B 1236, ~11%).

### Analysis

| | A (segments) | B (session) |
| --- | ---: | ---: |
| Instances | 1316 | 140 |
| Types | 22 | 22 |
| User turns (in-window) | all segments | 165 |
| Drift / Dragging | 51 / 35 | 1 / 1 |

* **Types:** Same catalog surface as A. The five types missing at 100 are back.
* **Counts:** B gained +110 vs B100, but still ~9× below A and far below uncapped B. Drift/Dragging stay at 1.
* **Why:** N=500 is ~12% of 4202 msgs. Type bag saturates early; instance volume does not. A barely moves vs A100 (+4).
* **Product read:** Use A for localization / complete coverage. Use B500 only if product wants “recent-window session severity.” Do **not** ship 500 as “session fixed” (1000 is still only 277 instances / ~22% of full B).

---

## 3. Segment vs session when the limit is removed

### Verdict

**Same conclusion on types (yes). Same conclusion on counts (no).** With MaxMessages uncapped for both, A and B agree on which issues exist; the only count gaps are chunk-re-fire signals (Drift + Dragging). Prefer this setup for fair A/B comparison and for session SoT.

### Analysis

| | A (segments) | B (session) |
| --- | ---: | ---: |
| Instances | 1316 | **1236** (= prod B) |
| Types | **22** | **22** |
| User turns | (per seg) | **1540** (= prod) |
| Drift / Dragging | 51 / 35 | **5** / **1** |

Same-conclusion check (`TestUncappedSegmentVsSession_Session01a05bf8`):

| Check | Result |
| --- | --- |
| Types equal? | **Yes** (only_A / only_B empty) |
| Counts equal? | **No** (gap **80**) |
| Gap composition | Drift −46 + Dragging −34 = **−80** |
| Other 20 types | **Exact count match** |

* **Types:** A and B tell the same “what’s wrong” story.
* **Counts:** Remaining A≫B is **scope** (compose re-fires per chunk), not truncation.
* **Why:** Removing last-N lets B see the full stream. Prod B for this session matches uncapped local B exactly.
* **Product read:** **Uncap session grading** (or N ≥ longest ShareGPT you accept). Keep segment at 100 if you want a cheap guard. If session stays capped, label it a **tail grade**.

---

## Method and limits

* One loadgen session; local `DialoguesToShareGPT` + `AnalyzeShareGPT` (not a live AE deploy).
* A = sum of per-segment instance counts; B = one session analyze.
* Window sweep also measured B at 1000/2000 (277/554 instances); still partial vs uncapped 1236.

## Recommendation

* Session path: **remove MaxMessages** (or unlimited sentinel). That is when A/B type conclusions align.
* Segment path: **100 is fine**.
* Do not treat **500** or **1000** as session-complete.

## Review

* [x] Owner named
* [ ] Ready for human review
