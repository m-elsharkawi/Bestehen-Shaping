# Bestehen / App — Stage 14: Review and Spaced Repetition

> **Status:** Authoritative Stage 14 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Review promise:** Important exam-relevant weaknesses return at useful intervals until they survive fresh, increasingly independent use — without turning Bestehen into a separate flashcard product.

## 1. Purpose and Scope

This document defines how Bestehen / App decides **what returns, when it returns, in what form, and when it can safely stop receiving explicit review**.

Review is the long-term continuation of the core loop **Observe → Attempt → Diagnose → Repair → Retry → Remember**. The same-session Retry proves only that the repair helped now. Review answers the harder question: **Did the capability survive after the answer and explanation were no longer fresh?**

The product therefore does not treat spaced repetition as a deck of cards to clear. It treats review as a set of **due coaching obligations** attached to exam-relevant learner capabilities, mistakes, productive patterns, and strategies. Those obligations are normally satisfied inside the coached daily session or naturally inside later exam-shaped practice.

Stage 14 defines:

- which vocabulary, grammar, phrase, listening, Writing, Speaking, and strategy signals may enter review;
- deterministic return intervals and due windows;
- TELC-relevance weighting and queue priority;
- repeated-failure behavior;
- stronger credit for successful productive use where the claim is productive;
- quick-review formats by capability type;
- how review is blended into 10-, 25-, and 45-minute coached sessions;
- interaction with Mistake Memory, learner-model freshness/decay, and natural task encounters;
- backlog, inactivity, uncertainty, and exam-date behavior;
- a low-cost operating model that does not require recurring AI scheduling calls.

This is product shaping, not an implementation algorithm, storage schema, notification system, or final TELC-readiness formula. Later stages may calibrate numerical intervals, build screens, or choose technical mechanisms, but they must preserve the review behavior and evidence boundaries defined here.

### Core decision

**Bestehen schedules review around exam-relevant capabilities and mistake patterns, not around viewed content. A due item is satisfied only by a valid fresh opportunity in the lane and condition relevant to the claim. Successful spontaneous use can satisfy review automatically; repeated failure triggers re-diagnosis and repair rather than endless repetition.**

---

## 2. Inputs / Existing Decisions

Stage 14 preserves the project overview, identity, and App Stages 01–13.

### 2.1 Product and coaching constraints

- Bestehen is a calm, direct, evidence-based **personal German exam coach**, not a generic course, flashcard product, or AI companion.
- Readiness is primary. Review exists to protect retained exam capability and improve the quality of readiness evidence, not to maximize cards completed.
- The learner may start around A1. Review format and difficulty must remain reachable while the target continues to point toward authentic B1 performance.
- Written and oral pass risk stay separate. Review cannot average a strong receptive skill over missing productive/oral evidence.
- The Daily Coaching Engine normally builds a 25-minute session with one dominant priority and a short due-review block when useful.
- The learner may override or skip review. Skipping changes scheduling/uncertainty; it is not treated as failure or punishment.

### 2.2 Learner-model constraints

Stage 04 already separates:

- capability/mastery;
- confidence;
- freshness/stability;
- readiness contribution;
- assisted versus unassisted evidence;
- open, practice-timed, and exam-timed evidence;
- Reading, Listening, Writing production, Speaking production, and interactive Speaking lanes.

Its ordinary freshness defaults remain authoritative:

| Freshness state | Existing default | Stage 14 interpretation |
|---|---:|---|
| Fresh | 0–30 days | No maintenance review merely because time passed; use natural practice unless a specific due check exists |
| Aging | 31–60 days | High-value capabilities may receive a concise refresh if natural evidence is unlikely |
| Stale | 61–120 days | Cannot alone support “reliable now”; schedule a recheck when decision-relevant |
| Historical-only | >120 days | Preserve history; use a concise natural recheck before current claims rather than rebuilding a giant backlog |

Stage 04 also defines stability as successful fresh evidence across occasions and time. A stable capability decays more slowly for daily coaching, but still becomes stale for readiness.

### 2.3 Mistake Memory constraints

Stage 05 already establishes the mistake lifecycle and minimum return cadence:

- same-session fresh Retry;
- first delayed transfer in **1–3 days**;
- short retention check at about **7 days**;
- broader transfer at about **21 days**;
- later stability/resolution check at about **60 days**.

It also establishes that:

- time does not repair a weakness;
- same-item repetition is not independent recurrence;
- immediate Retry success is responsiveness, not retained mastery;
- productive weaknesses require productive repair evidence;
- a Repaired weakness normally becomes Resolved only after later retention succeeds;
- failed checks raise priority and return the learner to repair/shorter delay;
- successful spontaneous use in normal practice can satisfy a due check;
- missed days must not create a punitive backlog.

**Stage 14 does not replace these rules. It operationalizes them across all reviewable material and defines how competing review obligations are prioritized and embedded in daily coaching.**

### 2.4 Skill-coaching constraints

Stages 09–13 establish additional review boundaries:

- Reading and Language Elements are normally objective and can be scored deterministically from reviewed answer keys.
- Listening review must use audio when the claim is sound recognition; transcript success cannot substitute for direct Listening evidence.
- Writing review must require learner-produced language for productive claims. Model text and corrected model prose are not learner evidence.
- Speaking review must remain oral for oral claims. Typed rehearsal cannot satisfy Speaking review.
- Interaction requires a real partner turn, even if that partner is a fixed/prerecorded low-cost scenario; a monologue cannot satisfy an interactive-speaking review obligation.
- Useful memorized phrases are legitimate evidence only when they are used appropriately in fresh contexts rather than recited because the App supplied the phrase.

No earlier decision is materially changed by Stage 14.

---

## 3. Decisions and Rationale

### 3.1 Review the capability, not the content object

**Decision:** The review unit is a **review obligation against a learner capability or mistake pattern**, not a permanent flashcard.

A due obligation identifies the smallest useful claim that needs another fresh opportunity, for example:

- recognize `verschieben` from natural audio in an appointment context;
- choose and produce subordinate-clause word order after `weil`;
- notice a restriction before matching a Reading notice;
- cover all four Writing content points without a supplied checklist;
- respond to a partner disagreement with an alternative;
- use a functional suggestion phrase appropriately without a phrase bank.

One obligation may be fulfilled by several possible fresh tasks. The learner should not need to repeat the original question, sentence, recording, or exact wording.

### 3.2 Review is evidence-driven, not exposure-driven

**Decision:** Merely seeing, studying, saving, or liking an item does not place it into high-priority spaced review.

An item enters review because there is a defensible coaching reason: a diagnosed gap, a repaired weakness needing delayed transfer, a high-value capability whose evidence is aging/stale, or an intentionally taught exam pattern that has not yet been independently demonstrated.

This prevents the queue from becoming a vocabulary notebook with thousands of low-value entries.

### 3.3 Use one deterministic scheduling model across modalities

**Decision:** All review types share the same lifecycle — immediate transfer, early delayed transfer, consolidation, broader transfer, and long-term stability — while the **review format changes by capability lane**.

The scheduler does not need an AI model to decide dates. It uses the learner state, mistake lifecycle, last valid opportunity, review result, TELC relevance, current stability, assistance/condition, exam date, and content availability.

### 3.4 TELC relevance changes urgency, not truth

**Decision:** TELC importance affects **how soon and how explicitly** an obligation returns. It does not change whether the learner actually succeeded or failed.

A pass-relevant target pattern can be reviewed explicitly even when natural recurrence is infrequent. A low-impact item can wait for a natural encounter once the learner has repaired it.

### 3.5 Production earns stronger productive credit

**Decision:** When the capability being reviewed is productive, correct **spontaneous Writing or Speaking use on fresh content** is stronger evidence than recognition or selection.

The system may therefore advance a productive review obligation more quickly after clean spontaneous use. It must not convert that productive success into unsupported mastery in another modality.

### 3.6 Repeated failure means “change the intervention”

**Decision:** Bestehen never responds to repeated review failure by serving the same drill indefinitely at ever-shorter intervals.

A failed due check is new diagnostic evidence. Repeated failure can mean the cause was wrong, the repair was too shallow, the task is too difficult, the learner remains support-dependent, or a prerequisite is missing. The coach must re-enter Diagnose/Repair when that is more valuable than another repetition.

### 3.7 Natural practice can clear review debt

**Decision:** A valid fresh opportunity inside Reading, Listening, Language Elements, Writing, Speaking, or a mock can satisfy a due obligation automatically.

The learner should never complete an artificial micro-review immediately after already demonstrating the same capability cleanly in a normal task.

---

## 4. What Enters Review

Not everything that is wrong or taught becomes an explicit queue item. A review obligation requires an identifiable capability/pattern, valid evidence, and enough exam value to justify future learner time.

### 4.1 Entry classes

A capability may enter review through four routes:

| Entry class | Trigger | Typical first action |
|---|---|---|
| **Repair retention** | A candidate/known weakness received repair and immediate fresh Retry | Schedule first delayed transfer in 1–3 days |
| **Known-weakness monitoring** | A known/stabilizing/repaired weakness is due for its next lifecycle check | Serve fresh direct-lane opportunity or allow natural embedding |
| **High-value learned pattern** | The coach intentionally taught a TELC-relevant phrase/strategy/pattern but independent use is not yet established | Schedule one future independent use rather than a card deck |
| **Freshness maintenance** | A previously reliable high-value capability is aging/stale and natural exposure is insufficient | Concise recheck at the strongest useful condition |

An isolated low-confidence mistake normally remains Mistake Memory history/candidate evidence rather than creating a recurring explicit review obligation.

### 4.2 Vocabulary

**Enters review when:**

- a word/phrase/concept is a diagnosed vocabulary gap affecting an exam task;
- a high-TELC-value functional word or synonym/paraphrase relationship was explicitly repaired;
- sound recognition and text recognition diverge and the audio form needs retention;
- a useful word/phrase is required productively and has not yet been independently recalled;
- a previously reliable high-value vocabulary concept is stale and materially blocks current practice/readiness.

**Does not enter merely because:** it appeared in content, was looked up once, belongs to a CEFR list, or was manually marked as interesting.

Review follows the lane: text recognition, sound recognition, meaning-to-form recall, or productive use are different claims.

### 4.3 Grammar patterns

**Enters review when:**

- a specific grammar relationship is a candidate/known weakness with adequate cause confidence;
- a grammar repair succeeded immediately but needs delayed transfer;
- the learner can select a form in Language Elements but productive control in Writing/Speaking is a current exam-relevant goal;
- a high-value grammar pattern has become stale and needs a concise direct-lane check.

Review targets the **decision/function in context**, not a chapter label. “Subordinate-clause verb position after `weil` in a fresh sentence/message” is reviewable; “B1 grammar — subordinate clauses” is too broad.

### 4.4 Useful phrases

**Enters review when:**

- the phrase represents an exam-useful communicative function such as proposing, asking, disagreeing, requesting, apologizing, giving a reason, offering an alternative, or closing an email;
- the learner needed explicit phrase support during Writing/Speaking and later independent availability matters;
- the phrase is part of a small reviewed functional pattern bank whose usefulness is supported by target/Copus evidence.

The review goal is **adaptable use**, not exact memorization of a whole answer. A phrase leaves active review after it appears appropriately and spontaneously across fresh contexts without App support.

### 4.5 Listening distinctions

**Enters review when:**

- the learner repeatedly confuses concrete values such as numbers, dates, times, prices, names, or similar forms;
- a known word is not recognized in natural speech;
- negation, restriction, correction, speaker change, or connected-speech cues are repeatedly missed;
- a repaired audio distinction needs delayed transfer under progressively more realistic playback/speed conditions.

Direct Listening review must use **fresh audio**. Reading the transcript can be repair support but cannot satisfy the Listening obligation.

### 4.6 Writing mistakes

**Enters review when:**

- a Writing-specific weakness or rubric-relevant pattern is known/stabilizing, such as missing content points, unstable register, weak organization, a recurrent grammar pattern, unusable functional phrase, or timed incompletion;
- a Writing repair needs fresh delayed productive transfer;
- a useful pattern taught through a model/revision has not yet appeared in independent Writing.

The obligation targets the pattern, not the old email. A due Writing review normally asks the learner to produce a **new sentence, message segment, content point, or full fresh prompt** depending on the breadth of the claim.

### 4.7 Speaking corrections

**Enters review when:**

- a spoken-production or interaction shortfall is sufficiently supported;
- a phrase, repair strategy, fluency behavior, intelligibility issue, proposal/alternative pattern, or turn-taking behavior was explicitly coached;
- the learner succeeded only with phrase support and needs independent oral use;
- a repaired oral weakness needs delayed transfer with a fresh prompt/partner turn.

Speaking obligations stay oral. Interactive obligations require a partner response. Accent differences that do not reduce intelligibility do not become review items.

### 4.8 Exam strategies

**Enters review when:**

- the learner has an observable strategy weakness such as overlooking restrictions, failing to extract constraints, not checking Writing content points, misallocating time, ignoring a correction, or not responding to a Speaking partner;
- a strategy behavior was repaired and needs to be demonstrated later without a coach cue;
- a high-value strategy has not been demonstrated under the relevant target condition.

Strategies are reviewed **inside a task that requires the behavior**. “Remember to scan first” is a reminder, not mastery evidence. A flashcard asking “What should you do before matching notices?” cannot satisfy the strategy obligation.

---

## 5. Scheduling Model

### 5.1 The default return sequence

Stage 14 adopts the existing Stage 05 sequence as the cross-product default:

| Review stage | Default due window | What it asks |
|---|---|---|
| **R0 — Immediate transfer** | Same session after repair | Did the repair help on fresh equivalent content? |
| **R1 — Early delayed transfer** | 1–3 days | Did the capability survive after the explanation was no longer fresh? |
| **R2 — Consolidation** | About 7 days; normal window 6–9 days | Can the learner repeat success on another fresh context? |
| **R3 — Broader transfer** | About 21 days; normal window 18–28 days | Does the capability generalize across topic/task variation and preferably less support? |
| **R4 — Stability / resolution** | About 60 days; normal window 45–75 days | Is the capability still available after a meaningful interval, ideally under a stronger realistic condition? |

These are **initial product defaults, not scientific constants**. Stage 26 may recalibrate them using delayed-transfer and real outcome data.

### 5.2 Due windows, not exact-day punishment

Review is due within a **window** rather than at one magical timestamp.

- Completing a check anywhere in the window is normal.
- If the learner is inactive, the obligation becomes overdue/stale but does not accumulate daily penalties.
- Returning after a long gap triggers re-prioritization, not a chronological queue replay.
- Natural valid use inside the window satisfies the obligation.

### 5.3 Schedule advances only from valid evidence

A due review advances when the learner produces a valid success in the relevant lane and condition.

Examples:

- a text-choice quiz cannot advance a Speaking-production obligation;
- a transcript-assisted answer cannot advance an independent Listening obligation;
- a phrase-bank-supported sentence cannot advance clean productive independence;
- a technically invalid recording does not count as failure or success;
- a same-item repeat after answer exposure cannot advance delayed-transfer status.

### 5.4 Stronger evidence may skip redundant micro-review

A clean, fresh, spontaneous success under a **stronger condition than the scheduled check required** can move the obligation directly to the next meaningful stage.

Examples:

- a connector due for a 7-day controlled production check appears correctly and spontaneously in an unassisted fresh Writing task: count the review as satisfied and move to the broader-transfer/stability stage rather than forcing a cloze;
- a Listening distinction due for practice review succeeds under exact target playback: do not add an easier extra audio drill;
- a Speaking alternative phrase appears naturally in a fresh S3 negotiation without a phrase bank: satisfy the productive obligation and move it to a later monitoring check.

This is the main mechanism by which successful productive use improves mastery more strongly **where appropriate**.

### 5.5 Assistance changes what the success proves

Assisted review success can show that the learner remains reachable and may justify continued learning, but it does not advance an independence claim as quickly.

Default behavior:

- clean unassisted success: advance normally;
- light non-answer-bearing support: advance if it does not change the tested capability;
- answer-bearing support/phrase bank/transcript/extra replay beyond the claim: keep or only partially advance the review stage and schedule a clean future check;
- model exposure followed by repetition: treat as repair exposure, not delayed-transfer success.

### 5.6 Exam-date compression

A fixed exam date changes review opportunity cost, not learning history.

- **More than 60 days away:** use the normal cadence.
- **22–60 days away:** retain normal early intervals; prefer R3/R4 checks that also increase realism rather than adding separate maintenance drills.
- **8–21 days away:** pass-critical unresolved/repaired weaknesses get at least one recent direct check under the strongest reachable condition; low-impact long-term items are deferred.
- **0–7 days away:** review becomes protection and rehearsal. Prioritize stable high-value phrases, target-condition distinctions, known pass-risk patterns, and execution strategies. Avoid building a large new review program whose benefit would occur after the exam.

Stage 17 owns the final 21-day and 7-day preparation modes; this stage supplies the review behavior they should consume.

---

## 6. TELC-Relevance Weighting and Queue Priority

### 6.1 Relevance bands

Until Stage 15 finalizes exact readiness weights, review uses the same ordered TELC-relevance approach established in Stage 06:

| Relevance | Meaning | Review consequence |
|---|---|---|
| **Core / pass-critical** | Directly affects a required target task, official rubric behavior, written/oral pass risk, or repeated target-condition point loss | Protect the due window; explicit review is justified even if natural exposure is unlikely |
| **Meaningful** | Regularly useful for target tasks or cross-skill exam performance | Normal cadence; natural embedding preferred when available |
| **Supporting** | Useful German or lower-frequency exam support but not currently a major pass-risk lever | Review mostly through natural encounters once repaired; explicit queue time is limited |

When Stage 15 provides target section/task weights, those become an additional target-value input. They must not erase personal learner need or written/oral bottlenecks.

### 6.2 Queue priority hierarchy

Review obligations compete in this order:

1. **Pass-critical due obligation** — target-condition or written/oral bottleneck with a due/overdue retention check.
2. **Failed/reopened obligation** — a due check failed recently or a repaired weakness recurred.
3. **Known/stabilizing high-TELC weakness** — active repair has not yet proven retention.
4. **Decision-relevant stale capability** — current freshness is insufficient for a coaching/readiness decision.
5. **Meaningful normal due review** — useful scheduled consolidation/transfer.
6. **Supporting maintenance** — can normally wait for natural practice.

Within the same tier, use the Stage 06 value dimensions: exam impact, learner need, review urgency, evidence value, deadline/mock relevance, reachability, time efficiency, fatigue/environment fit, repetition penalty, diagnosis confidence, and operating cost.

### 6.3 TELC relevance is bounded

High global frequency does not automatically dominate a learner's session.

- Corpus/TELC evidence may raise the priority of a capability that is genuinely due or under-evidenced.
- It cannot create a personal weakness without learner evidence.
- A low-frequency but persistent personal failure under target conditions may outrank a globally common pattern the learner already handles reliably.
- Oral pass risk can outrank cheaper written micro-review even when the written item is easy to schedule.

---

## 7. Behavior After Repeated Failure

### 7.1 One failed due check

A failed valid review is a new independent episode when the content/context is fresh enough.

Default response:

1. re-diagnose the cause at the narrowest defensible level;
2. raise Mistake Memory priority/recurrence as supported;
3. give or schedule the smallest useful repair;
4. use a fresh same-session Retry when time and content allow;
5. return the obligation to **R1 (1–3 days)** after repair rather than continuing to the longer interval.

### 7.2 Two consecutive delayed failures

**Decision:** Two consecutive valid delayed-review failures on the same pattern trigger a **repair-quality check**, not another identical drill.

The coach asks which of these is more likely:

- the original diagnosis is wrong or too broad;
- a prerequisite vocabulary/grammar/recognition skill is missing;
- the difficulty or target condition is currently unreachable;
- assistance was removed too quickly;
- the learner succeeds in recognition but not production;
- the content is not isolating the intended distinction;
- timing/attention rather than language is the blocker.

The next activity may restore one support dimension, run one clarifying contrast, or choose a prerequisite. It should not simply serve more items of the same form.

### 7.3 Persistent or target-condition recurrence

A pattern that meets Stage 05 recurring/persistent criteria becomes a higher-priority coaching target.

For persistent target-condition failure:

- dedicate a coherent coaching block rather than scattering many tiny reviews;
- include at least one fresh target-condition verification before calling it repaired;
- consider cross-modal verification only when the underlying node plausibly transfers; never infer the other modality's weakness without direct evidence;
- explain the pattern neutrally: “This still returns under one-play Listening,” not “You keep failing this.”

### 7.4 Do not grind within one session

A review item normally receives **one meaningful check and, if needed, one repair + fresh Retry** in a session. If it still fails, save the evidence and schedule the next useful intervention. Repeating near-identical items until the learner happens to answer correctly creates poor evidence and fatigue.

---

## 8. Successful Productive Use and Mastery Effects

### 8.1 Productive success is direct evidence for productive claims

Successful spontaneous use in Writing or Speaking receives stronger productive evidence than recognition, selection, copying, or repeating a supplied phrase.

Examples:

- choosing `weil` correctly in a cloze strengthens contextual-selection evidence;
- producing correct `weil` word order in a fresh email strengthens Writing-production evidence more strongly;
- producing it naturally in a fresh spoken answer strengthens Speaking-production evidence;
- none of those automatically prove Listening recognition.

### 8.2 Productive success can satisfy due review automatically

A productive success counts as the scheduled check when all are true:

- the content/context is fresh;
- the learner did not receive the answer/form from the App immediately beforehand;
- the use is relevant and not accidental/formulaic;
- the evaluation is trustworthy enough for the claim;
- the lane matches the obligation.

### 8.3 Strong productive use accelerates exit from active review

When a learner uses a pattern spontaneously and correctly under a stronger condition than required:

- mark the due check satisfied;
- advance to the next meaningful interval;
- remove lower-level redundant micro-drills;
- after repeated fresh spontaneous use across occasions, move the item from active review to monitoring/resolved according to Stage 05 criteria.

The product does **not** award a hidden arbitrary “double point.” It strengthens the evidence because production is a harder, more direct claim. Stage 26 may later calibrate the numerical learner-model update while preserving this ordering.

### 8.4 Memorized phrases are credited with guardrails

A useful phrase is not penalized because it was learned. It becomes strong evidence when it is:

- chosen appropriately for the communicative function;
- adapted to the fresh context/recipient;
- produced without the App supplying it in that attempt;
- used across more than one fresh context when broad availability is claimed.

A large memorized block reproduced regardless of the prompt does not receive the same transfer credit.

---

## 9. Quick-Review Formats

Quick review is **micro exam practice**, not a generic flashcard UI. Most items should take about **20 seconds to 3 minutes**; broader productive checks may take longer and then become a normal coaching block rather than “quick review.”

| Review type | Preferred quick formats | What does **not** count |
|---|---|---|
| Vocabulary — text recognition | Choose meaning/paraphrase in a fresh sentence or notice; identify synonym that preserves meaning | Re-reading the saved definition |
| Vocabulary — sound recognition | Hear a fresh short clip and select/type the heard meaning/value | Reading the transcript first |
| Vocabulary — productive recall | Function/meaning cue → type or say the word/phrase in a fresh sentence | Copying from a visible bank |
| Grammar — contextual selection | 1–3 fresh cloze/contrast decisions with reviewed distractors | Repeating the original item with reordered choices |
| Grammar — productive control | Complete or produce a fresh sentence/message segment using the pattern | Multiple-choice recognition used to claim Writing/Speaking mastery |
| Useful phrase | Communicative function cue → say/write one suitable phrase; adapt it to recipient/situation | Recite a full memorized template unrelated to context |
| Listening distinction | 5–20 sec fresh audio contrast for number/date/negation/correction/connected speech, then one decision | Transcript-only quiz for a Listening claim |
| Writing | 1–3 minute micro-write: one missing content point, request, connector sequence, register choice, greeting/closing, or fresh sentence pattern | Merely editing the old answer after seeing corrections |
| Speaking production | 20–60 sec fresh oral response using the repaired function/pattern | Typed answer |
| Speaking interaction | Fresh partner turn requiring response, disagreement, alternative, clarification, or negotiation | Solo monologue used to claim interaction |
| Exam strategy | Tiny exam-shaped decision that requires the behavior: extract constraints, pick evidence, check content points, move-on choice | “What is the strategy?” knowledge card |

### 9.1 Format variation

The scheduler should vary surface form when several formats can test the same capability. Variation helps transfer and prevents the learner from memorizing the review mechanic.

However, variation must not change the evidence lane accidentally. A productive review cannot be replaced by an easier recognition format just for convenience.

### 9.2 Review can expand into a full task

If the claim is broad — for example full Writing task coverage, sustained H2 Listening detail, or S3 negotiation — a micro-review may be insufficient. The due obligation should then be embedded into the next appropriate full/partial exam-shaped task rather than squeezed into an invalid card.

---

## 10. Integration with Daily Coaching

### 10.1 Review is a component of Today’s Plan

Review remains subordinate to the coach-led daily mission. The primary experience is still “What should I do today?”, not “You have 37 cards due.”

A due obligation may appear as:

- a short opening **Fresh check**;
- a natural requirement inside the dominant coaching block;
- a secondary evidence/coverage task;
- a full task chosen partly because it satisfies one or more high-value reviews.

### 10.2 Session budgets

These are starting product defaults consistent with Stage 06:

| Session | Normal review behavior |
|---|---|
| **5–9 min micro-session** | One highest-value due check or one compact repair/retry loop; it may be entirely review if that is the best use of the time |
| **10 min Quick** | Normally 1–2 review obligations plus one compact priority move, or a review-focused session when a pass-critical check is due |
| **25 min Standard** | Normally **0–4 minutes and 1–3 explicit due checks**, then the dominant coaching block; expand review only when the due item itself becomes the dominant repair |
| **45 min Extended** | Normally 3–8 minutes of explicit due work plus one or two deeper blocks; prefer natural embedding over a long review list |
| **Mock / P4 measured block** | No teaching/review interruptions during measurement; due obligations may be satisfied by valid mock evidence and are reconciled afterward |

These are not quotas. A 25-minute session may spend 18 minutes on a reopened Writing weakness because it is no longer “small review”; it has become today’s dominant coaching target.

### 10.3 Queue capping and backlog behavior

**Decision:** The App never asks the learner to “clear” all overdue review.

For a normal session:

- select only the highest-value obligations that fit the available time;
- lower-value overdue items remain available for natural embedding or later scheduling;
- avoid multiple reviews of near-identical nodes in one session unless a deliberate contrast is the repair;
- protect modality diversity when one cheap review type would otherwise crowd out oral/written pass risk;
- after inactivity, rebuild from current priorities rather than replaying every missed due date.

### 10.4 Example 25-minute daily integration

A learner has weak S3 interaction, a due Listening negation check, and several lower-priority grammar/vocabulary items.

**Today’s Plan:**

1. **2 min — Listening fresh check:** one short H1-style audio under the current playback rule tests the due negation distinction.
2. **17 min — Speaking S3 dominant block:** fresh planning scenario; diagnose and repair response-to-disagreement behavior; fresh partner Retry.
3. **4 min — Embedded grammar/phrase evidence:** the S3 exchange itself can satisfy a due suggestion/alternative phrase if used spontaneously; otherwise one short oral follow-up is added.
4. **2 min — Remember/summary:** record what transferred, what remains due, and why a lower-priority vocabulary item was deferred.

The learner experiences one coherent session, not three disconnected decks.

### 10.5 “Why this today?” explanation

Review-related recommendation copy should explain the consequence, for example:

- “You repaired this Listening distinction two days ago. This short fresh clip checks whether it stayed.”
- “You used this phrase independently in today’s Speaking task, so I removed the separate review.”
- “This Writing pattern failed again under a fresh prompt. It moves back into focused repair rather than another quick quiz.”
- “You were away for three weeks. I picked the two highest-value stale checks; the rest can wait.”

---

## 11. Example Review Queue

The queue below is illustrative. It shows how the coach reasons; it is not a required learner-facing table.

| Obligation | Current state | Due | TELC value | Best next evidence | Queue decision |
|---|---|---|---|---|---|
| Listening: hear `nicht/noch nicht` correctly in H1-style speech | Known weakness; immediate Retry passed | Today (R1) | Core/high | Fresh short audio at current target playback | **Do now** — early delayed transfer |
| Speaking S3: respond to disagreement with an alternative | Stabilizing; one delayed success | In 2 days | Core/oral pass risk | Fresh partner disagreement turn | **Protect window**; can be embedded in dominant S3 block |
| Writing: check all four content points before submit | Repaired after repeated omission | Today (R2) | Core/high | Fresh micro-prompt requiring a plan/check, or next full email | **Do/Embed** — strategy must be demonstrated, not recalled as advice |
| Grammar: `weil` verb-final in Writing | R2 due | Today | Meaningful/high transfer | Fresh sentence/message production | **Embed** in Writing if possible; do not add cloze if production already succeeds |
| Vocabulary/audio: `verschieben` sound recognition | Candidate repaired once | Tomorrow | Meaningful | Fresh appointment audio | **Can defer within window** |
| Useful phrase: `Ich würde vorschlagen, …` | Used spontaneously in fresh S3 yesterday | Was due today | Meaningful | Later fresh planning context | **Auto-satisfied**; move to broader-transfer interval |
| Reading restrictions (`nur`, date range, location) | Repaired; last clean check 54 days ago | R4 window | Core/high | Fresh R3/selective task | **Maintenance**; embed soon, not necessarily today |
| Low-frequency vocabulary from one old passage | Historical isolated gap | Overdue by old date | Supporting | Natural future encounter | **Do not surface as backlog** |

---

## 12. Interaction with Mistake Memory

Mistake Memory and Review have different responsibilities.

| Mistake Memory owns | Review owns |
|---|---|
| What happened and likely cause | When the next useful fresh opportunity should occur |
| Candidate/known/repairing/stabilizing/repaired/resolved/reopened lifecycle | Due stage/window, queue urgency, and preferred review lane/format |
| Independent recurrence and opportunity-adjusted failure | Selection among competing obligations in limited study time |
| Whether a weakness is currently active | Whether a valid natural task can satisfy the due obligation |
| Historical truth | Operational return timing |

### 12.1 State transitions

- **Candidate:** may receive one clarifying or natural recheck; do not automatically create long-term review.
- **Known / Repairing:** explicit review is normally active and protected.
- **Stabilizing:** schedule R2/R3 checks and prefer broader/fresher conditions.
- **Repaired:** dedicated daily repair stops; R4 monitoring remains.
- **Resolved:** no active explicit queue by default; history remains and natural opportunities can confirm continued stability.
- **Reopened:** return to Known and R1 after repair, with priority based on current TELC impact and target realism.

### 12.2 Failed review creates evidence, not a scheduler-only event

A failed valid review must flow back into Mistake Memory as an independent episode when independence rules are met. The scheduler cannot hide repeated failure by merely moving a date.

### 12.3 Successful review can resolve memory obligations

A successful review updates learner evidence and may move a pattern from Stabilizing → Repaired or Repaired → Resolved only when the Stage 05 criteria are actually met. The scheduler does not declare repair from elapsed time alone.

---

## 13. Interaction with Learner-Model Decay and Freshness

### 13.1 Review and decay are related but not identical

Learner-model freshness answers **how current the evidence is**. Review scheduling answers **when another opportunity is worth the learner’s time**.

Therefore:

- a capability can be Fresh without having a specific review obligation;
- a repaired weakness can have an R1 check due even though its evidence is technically Fresh;
- an Aging strong capability may need no explicit review if natural practice will refresh it soon;
- a Stale high-value capability can enter maintenance review even without a recent mistake.

### 13.2 A review refreshes only what it actually tests

A successful check updates freshness for the exact capability/lane/condition supported by the evidence.

Examples:

- an untimed cloze refreshes contextual grammar selection, not exam-timed Writing production;
- one extra-replay Listening check cannot refresh target-playback evidence;
- a 30-second Speaking monologue can refresh production but not sustained interaction;
- a full target-condition mock can refresh many obligations at once when attribution is valid.

### 13.3 Stable history is not erased by one failure

Consistent with Stage 04, one new weak result first creates contradiction/recheck need. It does not instantly reset a stable historical capability to “not demonstrated.”

Repeated valid failure, especially under target conditions, can lower current mastery/confidence and reopen Mistake Memory as the evidence accumulates.

### 13.4 Stale evidence does not create a huge review list

When multiple skills become stale after inactivity:

1. prioritize written/oral decision gaps and core TELC task families;
2. sample a small number of representative high-value checks;
3. use results to decide whether broader refresh is necessary;
4. allow strong results to reactivate related broad rollups cautiously without inventing untested fine-node freshness;
5. leave low-value historical items in history until naturally relevant.

---

## 14. Edge Cases / Failure or Uncertainty Handling

### Learner misses the due date

Move the obligation to overdue/stale priority according to value. Do not count a failure, reset a streak, or show shame-based backlog language.

### Learner returns after weeks or months

Do not serve every missed R2/R3/R4 check. Rebuild a compact queue from current exam relevance, written/oral gaps, known weaknesses, and representative stale capabilities.

### Review content is too similar to the original

It cannot count as independent delayed transfer. Replace it with a sufficiently fresh variant or wait for a natural task.

### No fresh content is available

Do not reuse exposed content to manufacture completion. Keep the obligation due and use a broader reviewed task or later natural opportunity. Stage 21 owns content-pool depth and anti-duplication.

### Cause confidence is low

Use a clarifying review/probe, not a fine-grained drill. If the result remains ambiguous, preserve the broad evidence and avoid promoting a precise weakness.

### The learner succeeds only with support

Credit assisted learning. Keep the independent obligation open or move it only to the next appropriate assisted step; do not claim clean retention.

### The learner produces a correct form accidentally once

One spontaneous use can satisfy a due check when context makes the use meaningful, but broader mastery still requires repeated evidence. Do not over-generalize from one token.

### Writing/Speaking evaluator unavailable

Store the attempt and deterministic metadata. A learner may self-check for learning value, but do not close a high-impact productive obligation or move readiness on untrusted evaluation. Evaluate later only if still useful and permitted.

### Technical failure in audio/voice review

Invalidate the evidence effect. Reschedule without counting a failure.

### Learner is far below the scheduled B1 condition

Step down one causal axis — language load, speed, support, output size, partner complexity, or timing — and repair the prerequisite. Preserve the target obligation as not yet proven rather than forcing repeated B1 failure.

### Learner is already strong

If a fresh stronger-condition task demonstrates the capability cleanly, satisfy the due review and move to longer monitoring. Do not invent micro-corrections to keep the queue busy.

### Current TELC blueprint changes

Re-rank target relevance and target-condition status. Historical transferable capability remains valid, but obsolete task-specific review should not continue merely because it was previously scheduled.

---

## 15. Relationship to Other Bestehen Stages

- **Stage 04 — Learner Model:** supplies mastery, confidence, freshness, stability, modality lanes, and condition-specific evidence that review consumes.
- **Stage 05 — Mistake Memory:** owns the weakness lifecycle, recurrence, repair criteria, and baseline return sequence that Stage 14 schedules operationally.
- **Stage 06 — Daily Coaching Engine:** decides how review competes with pass risk, evidence gaps, coverage, fatigue, and available time; Stage 14 supplies due obligations and urgency.
- **Stage 07 — Core Learning Loop:** Review is delayed **Remember → fresh Attempt**. Failed review re-enters Diagnose/Repair; successful review updates Remember.
- **Stage 08 — A1→B1 Progression:** determines reachable difficulty/support for each review while ensuring target-condition claims use the appropriate rung.
- **Stages 09–13 — Skill Coaching:** define the valid direct-evidence formats and task-specific diagnosis/repair rules used by each review type.
- **Stage 15 — TELC Readiness:** will define exact target weights, recency requirements, and pass-model contribution. Stage 14 must feed it condition-qualified evidence rather than a generic SRS score.
- **Stage 16 — Mock Exams:** mock evidence can satisfy many due obligations naturally; diagnosis/review occurs only after the measured block.
- **Stage 17 — Ready to Book:** uses the exam-date compression behavior and stricter recent target-condition review needs.
- **Stage 19 — Information Architecture:** decides whether/how the learner can inspect a Review area or due list. The coach-led Today view remains primary.
- **Stage 21 — Content Strategy:** must provide sufficiently fresh equivalent content and anti-duplication rules for delayed transfer.
- **Stage 23 — Notifications:** decides whether due-review reminders are sent and how they are capped.
- **Stage 26 — Analytics:** recalibrates intervals, success/retention rates, repeated-failure thresholds, natural-embedding effectiveness, and productive-evidence effects.
- **Stage 27 — Cost Boundaries:** applies portfolio-wide operating limits to productive evaluation and generated review content.

### Cross-stage guardrail

Later stages may calibrate the numerical windows, but they must preserve these behaviors:

1. review is capability/mistake-based rather than a card-collection product;
2. due checks require fresh evidence in the correct lane;
3. Stage 05’s immediate → 1–3d → ~7d → ~21d → ~60d progression remains the starting lifecycle;
4. TELC relevance and pass risk affect urgency;
5. natural valid practice can satisfy review automatically;
6. productive independent use is stronger evidence for productive claims;
7. repeated failure triggers diagnosis/repair rather than infinite repetition;
8. missed days never create a punitive backlog;
9. no AI model is required to calculate the routine schedule.

---

## 16. Cost Notes

Stage 14 has **very low intrinsic recurring-cost requirements**. The scheduler itself should be deterministic.

### Preferred low-cost default

- Calculate due windows, priority tiers, lifecycle transitions, and backlog selection from existing learner-state fields.
- Use reviewed reusable objective content and pre-generated fresh variants for vocabulary, grammar, Reading, strategy, and most Listening micro-checks.
- Batch-generate and cache audio variants; do not call live TTS for every review attempt.
- Use fixed/prerecorded Speaking partner turns for many quick interaction checks where adaptability is not necessary.
- Reuse the structured Writing/Speaking evaluation already produced for the learner response; do not make a second model call merely to decide the next review date.
- Cache unchanged productive evaluations and common feedback/repair templates.
- Let valid normal practice satisfy due obligations so the product does not create extra evaluation work solely because an SRS queue exists.

### When paid AI is justified

A runtime model call is justified only when the productive task itself requires evaluation or an adaptive interaction whose quality materially affects coaching. A stronger/second evaluator is reserved for **high-impact uncertain Writing/Speaking evidence**, especially P4/mock/readiness-relevant decisions, consistent with Stages 12–13.

### Cheap fallback

If rich productive evaluation is unavailable:

- keep the review obligation open;
- provide deterministic/self-check learning value where safe;
- do not claim mastery/readiness movement from unsupported evaluation;
- continue with other valid due work.

There is no product justification for a premium AI call to compute intervals, reorder the queue, or generate motivational review copy.

---

## 17. Decisions Made

1. Defined review as **due coaching obligations against capabilities/mistake patterns**, not permanent flashcards.
2. Defined entry rules for vocabulary, grammar patterns, useful phrases, listening distinctions, Writing mistakes, Speaking corrections, and exam strategies.
3. Adopted the Stage 05 lifecycle as the cross-skill default: same-session Retry → 1–3 days → ~7 days → ~21 days → ~60 days.
4. Added due windows, natural-opportunity satisfaction, stronger-condition skipping, inactivity/backlog rules, and exam-date compression.
5. Defined TELC-relevance bands and a queue hierarchy that protects pass-critical review without letting global frequency invent learner weakness.
6. Defined repeated-failure behavior: one failure returns to repair/R1; two consecutive delayed failures trigger re-diagnosis/repair-quality review; persistent target-condition failure becomes a coherent coaching priority rather than a grind loop.
7. Defined successful spontaneous productive use as stronger evidence for productive claims and allowed it to satisfy/advance review automatically.
8. Defined quick-review formats for every required review category while preserving direct-evidence lanes.
9. Integrated review into 5–9, 10, 25, and 45-minute coached sessions and mocks without creating a separate deck-clearing journey.
10. Defined the boundary between Mistake Memory lifecycle ownership, review scheduling, and learner-model freshness/decay.
11. Chose deterministic scheduling and cached/reusable content as the default, with no recurring premium AI requirement for scheduling.

---

## 18. Open Questions / Deferred Decisions

### No owner question blocks Stage 14

The product behavior can be responsibly defined from the existing shaping decisions. No personal preference or business constraint requires an owner decision here.

### Deferred to later shaping / validation

- Exact calibrated interval lengths, modality-specific decay curves, and any adaptive interval coefficients — **Stage 26**, using retention/transfer data.
- Exact TELC section/task/readiness weights and stricter pass-critical recency windows — **Stage 15**.
- Final 21-day and 7-day booked-exam programs — **Stage 17**.
- Learner-facing Review area, queue visibility, filters, and screen hierarchy — **Stage 19**.
- Fresh-content pool size, generation QA, and anti-near-duplicate thresholds — **Stage 21**.
- Due-review notification rules — **Stage 23**.
- Final privacy/retention of review-related raw Writing/audio — **Stage 24**.
- Storage, scheduling algorithms/data structures, model providers, queues, and technical architecture — post-shaping architecture work.

The intervals and limits in this document are **initial product defaults** chosen to make the first complete product testable and affordable. They are deliberately tunable rather than presented as scientifically exact.

---

## 19. Definition of Done Check

### Stage 14 checklist coverage

- [x] Decide what enters review:
  - [x] vocabulary;
  - [x] grammar patterns;
  - [x] useful phrases;
  - [x] listening distinctions;
  - [x] writing mistakes;
  - [x] speaking corrections;
  - [x] exam strategies.
- [x] Define scheduling principles.
- [x] Weight review priority by TELC relevance.
- [x] Define behavior after repeated failure.
- [x] Let successful productive use improve mastery more strongly where appropriate.
- [x] Define quick-review formats.
- [x] Blend review into daily coaching rather than building a separate flashcard product.

### Required deliverable checks

- [x] Priority and scheduling rules are explicit.
- [x] An example review queue is included.
- [x] Daily coaching integration is concrete.
- [x] Mistake Memory and learner-model decay interactions are defined.
- [x] Repeated failure and successful productive use have explicit effects.
- [x] Routine scheduling is deterministic and does not require recurring AI spend.
- [x] Edge cases, cost boundaries, later-stage relationships, and deferred calibration decisions are documented.

**Stage 14 is product-shaped when important exam-relevant mistakes and fragile capabilities reliably return until they survive fresh, appropriately independent evidence, while the learner still experiences one coherent exam coach rather than a second flashcard product.**
