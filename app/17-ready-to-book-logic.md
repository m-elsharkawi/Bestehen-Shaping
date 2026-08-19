# Bestehen / App — Stage 17: “Ready to Book” Logic

> **Status:** Authoritative Stage 17 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Booking promise:** Recommend booking only when the existing Readiness model says both pass components are safely above the current pass line **and** recent, independent, target-condition evidence shows that result is repeatable enough to act on.

## 1. Purpose and Scope

This document defines the evidence threshold for Bestehen / App to responsibly move from **“you are preparing”** to **“your evidence supports booking TELC B1.”**

The Ready-to-Book state is deliberately stricter than merely seeing a readiness number above the official pass line. Booking is a consequential learner action: it costs money, creates a deadline, and changes how the coach should allocate the remaining study time. The recommendation therefore requires not only estimated performance, but adequate written and oral evidence, recency, target-condition realism, and independent consistency.

At the same time, Stage 17 must **not create a second readiness score**. Stage 15 remains the only readiness calculation. Stage 17 is a decision gate over the Stage 15 state plus mock/evidence conditions already represented in the same evidence ledger.

This stage defines:

- the exact launch Ready-to-Book rule;
- adequate written and oral evidence;
- evidence recency;
- required unassisted/timed/target-condition evidence;
- the role of full and component mock consistency;
- learner-facing confidence language;
- coaching when the learner is close but not yet ready;
- behavior when the learner books before or after readiness;
- the final 21-day and 7-day preparation modes;
- expiry/reopening behavior when evidence becomes stale or contradictory;
- low-cost operation and evaluation escalation boundaries.

This is product shaping, not implementation architecture. It does not choose a rules engine, database, scheduler, notification mechanism, model vendor, UI layout, or booking-provider integration.

### Core decision

**“Ready to book” is an evidence gate over Stage 15 Readiness, not a new score.**

Bestehen recommends booking only when all of the following are true:

1. **Written is in Stage 15 Safe pass range.**
2. **Oral is in Stage 15 Safe pass range.**
3. Both components still meet their Stage 15 **decision-grade evidence minimums**.
4. A **clean full target-condition mock** on fresh content has cleared both current written and oral pass gates within the last **14 days**.
5. Each pass component has been **independently confirmed on another measured occasion within the last 30 days**. This may be a second full mock, or a clean written-component mock plus a clean oral-component mock; a second full mock is **not required**.
6. Overall evidence confidence is at least **Medium** and no current pass-critical contradiction, invalid evaluation, stale target blueprint, or unresolved target-condition problem undermines the recommendation.

The existing Stage 15 Safe pass range already requires, for each component:

- an estimated target performance of at least **65/100**;
- a planning-range lower bound at or above the official **60/100** pass line;
- sufficient recent direct target-condition coverage;
- at least Medium confidence;
- no unresolved pass-critical blocker.

Stage 17 therefore does **not** invent a higher 70/75 score or a separate “booking percentage.” It adds a practical consistency gate around the existing conservative readiness state.

---

## 2. Inputs / Existing Decisions

Stage 17 preserves the project overview, identity, and App Stages 01–16.

### 2.1 Readiness remains authoritative

Stage 15 establishes:

- current TELC B1 written and oral components have separate **60%** pass gates;
- Written maximum is 225 points with a current pass line of 135/225;
- Oral maximum is 75 points with a current pass line of 45/75;
- **Readiness Index = min(Written target %, Oral target %)**;
- the launch index is a target-performance estimate, **not pass probability**;
- Stage 15 Safe pass range begins at an estimated **65/100** with the lower end of the planning range at or above 60;
- both components must independently be Safe before overall readiness is Safe;
- readiness is reversible when new evidence, aging evidence, evaluation correction, or a blueprint change changes the claim.

Stage 17 consumes those conclusions. It does not recalculate mastery or TELC points independently.

### 2.2 Stage 15 decision-grade written evidence

Ready-to-Book inherits the complete written evidence minimum. In summary:

- R1/R2/R3, SB1/SB2, H1/H2/H3, and Writing have current direct E3/E4 score-setting evidence;
- Reading, Sprachbausteine, Listening, and Writing each have a recent E4 target-condition anchor within 30 days;
- Reading + Sprachbausteine include a valid shared-block target-condition timing/allocation observation;
- Listening uses target playback rules;
- Writing includes a clean current target-time response plus another fresh independent B1 Writing response;
- evidence spans multiple occasions/days;
- each written section has at least Medium confidence and no unresolved pass-critical contradiction.

Stage 17 does not weaken these requirements merely because a full mock happened to pass.

### 2.3 Stage 15 decision-grade oral evidence

Ready-to-Book also inherits the complete oral evidence minimum. In summary:

- S1/S2/S3 all have current direct oral E3/E4 score-setting evidence;
- S2 and S3 include genuine partner interaction;
- at least two fresh S2/S3 contexts exist across at least two occasions;
- at least one current full target-condition three-part oral simulation or equivalent P4 sequence exists within 30 days;
- a second recent P3/P4 oral occasion confirms the full sequence is not the only evidence;
- intelligibility is validly judgeable;
- each oral part has at least Medium confidence and no unresolved pass-critical contradiction.

A typed response, solo monologue, or low-confidence transcript cannot substitute for required interaction evidence.

### 2.4 Stage 15 readiness recency

Stage 15 already defines stricter readiness recency than ordinary learning freshness:

| Evidence age | Stage 15 readiness effect |
|---|---|
| 0–14 days | Fully current |
| 15–30 days | Strongly current |
| 31–60 days | Aging for readiness |
| 61–90 days | Weak current anchor; recheck required for strong claims |
| >90 days | Historical capability only for current readiness |

Stage 17 uses the existing **0–14-day fully-current band** for the latest clean full-mock booking anchor and the existing **30-day decision-grade window** for supporting target-condition evidence. This avoids inventing a disconnected recency system.

### 2.5 Stage 16 mock evidence and consistency

Stage 16 establishes:

- one full mock is one correlated evidence occasion;
- every valid mock contributes immediately through the Stage 15 evidence model;
- one full-mock pass is strong evidence but not proof of consistency;
- two clean passing full mocks on separate days are a useful **repeated full-mock pass** milestone;
- Stage 15 Safe pass range can be reached with equivalent distributed E4 evidence without two full mocks;
- a second full mock is expensive in learner time and productive evaluation, so smaller component mocks should be preferred when they answer the same question;
- a full mock may only claim target-condition validity when the relevant current format, timing, playback, preparation, interaction, freshness, and no-help rules were reproduced cleanly.

Stage 17 therefore requires **consistency across measured occasions**, not an arbitrary count of full mocks.

### 2.6 Booking changes urgency, not demonstrated ability

Stages 01, 02, 06, and 15 already establish that an exam date changes the plan, urgency, and opportunity cost. It does not increase capability or readiness.

A learner may book before Bestehen recommends it. The product must then enter booked-exam preparation immediately, show remaining risk honestly, and optimize the time left. It must not punish, shame, or pretend the learner became ready because a date now exists.

---

## 3. Decisions and Rationale

### 3.1 Use Stage 15 Safe pass range as the performance threshold

**Decision:** Ready-to-Book requires both Written and Oral to be **currently Safe pass range** under Stage 15.

This means the performance threshold is not merely “above 60.” The existing launch guard band already requires:

- estimate ≥65 in each component;
- lower planning-range bound ≥60;
- decision-grade evidence;
- at least Medium evidence confidence;
- no pass-critical contradiction.

A new Stage 17 score threshold would create two competing meanings of readiness. The correct product model is simpler: **Stage 15 says whether performance is safely in range; Stage 17 says whether the evidence is consistent and current enough to act on by booking.**

### 3.2 Adequate written evidence is non-negotiable

**Decision:** The complete Stage 15 written decision-grade minimum is required.

A high written average cannot compensate for missing current Writing, incorrect Listening playback conditions, no shared Reading + Sprachbausteine timing evidence, or a materially unstable written section. A passing full-mock written total does not erase those evidence-quality requirements.

Why: a learner can reach 135/225 in one simulation despite one under-sampled or fragile area. The coach should recommend booking only when the broader written evidence explains why the pass is plausible rather than relying on one favorable form.

### 3.3 Adequate oral evidence is independently required

**Decision:** The complete Stage 15 oral decision-grade minimum is required.

Oral readiness cannot be inferred from grammar, Writing, Reading, a monologue, or typed rehearsal. S2/S3 need actual interaction. A strong written component cannot conceal weak oral evidence because TELC applies an independent oral pass gate.

Why: oral performance is a separate pass risk and can vary substantially with interaction, fluency, partner response, preparation, and timing. The product promise requires direct evidence in the lane that will be judged.

### 3.4 Latest full-mock evidence must be fully current

**Decision:** The Ready-to-Book gate requires a **clean passing full mock within 14 days**.

The 14-day window is not a new decay curve. It reuses Stage 15's “fully current” readiness band for the single most consequential whole-exam rehearsal.

The mock must:

- use fresh content;
- use the approved current target blueprint;
- reproduce the target conditions required by Stage 16;
- have valid objective scoring;
- have trustworthy Writing/Speaking evaluation;
- clear **both** current written and oral pass gates;
- not contain a material pause, extra help, replay, model exposure, partner failure, or technical failure that invalidates the full-mock claim.

If only some units remain valid, they continue to update Stage 15 Readiness, but the attempt does not satisfy this full-mock booking condition.

### 3.5 Consistency is required, but two full mocks are not

**Decision:** Ready-to-Book requires **two independent pass-gate confirmations per component**, but only one must be a full mock.

The minimum consistency pattern is:

| Evidence occasion | Written requirement | Oral requirement |
|---|---|---|
| Latest full mock, within 14 days | Clean written gate pass | Clean oral gate pass |
| Independent confirmation, within 30 days | Clean written-component pass on fresh content | Clean oral-component pass on fresh content |

The second confirmation may be satisfied by:

- **a second clean full mock** on another day, which confirms both components at once; or
- **one clean written-component mock + one clean oral-component mock** on separate fresh measured occasions.

A component confirmation must represent the whole pass-gated component under the Stage 16 target-condition contract. A Reading-only, Listening-only, Writing-only, S2-only, or mini-mock does not by itself confirm the component pass gate.

The confirmation must be independent of the full mock: fresh form/content, another measured occasion, and no answer exposure. Same-day back-to-back repetitions should normally be treated as one preparation episode for this booking decision unless there is a defensible independent context; the recommended default is another day.

**Rationale:** Requiring two full mocks would add substantial learner time, fatigue, fresh-form demand, Speaking/partner cost, and productive evaluation cost. Requiring only one full mock would let one unusually favorable complete run carry too much decision weight. One full mock plus component-level confirmation proves repeatability at lower cost while keeping both pass gates explicit.

### 3.6 Two passing mocks never override current readiness

**Decision:** Mock count is a consistency condition, not an alternative readiness calculation.

The learner is **not** Ready to Book when:

- two full mocks passed historically but Stage 15 Written or Oral is no longer Safe;
- a newer target-condition failure creates a material unresolved contradiction;
- decision-grade evidence has aged out;
- a current blueprint change makes old P4 evidence no longer target-equivalent;
- productive evaluation is too uncertain to support the score.

The Stage 15 state always remains the performance authority.

### 3.7 Overall confidence must be at least Medium

**Decision:** There is no “Low-confidence Ready to Book” state.

Overall confidence is the lower of Written and Oral confidence under Stage 15.

Ready-to-Book language has two useful strength levels without creating new readiness bands:

| Evidence confidence | Learner-facing recommendation strength |
|---|---|
| Medium | **Ready to book — sufficient current evidence** |
| High | **Ready to book — strong current evidence** |
| Low | Do not recommend booking; name the missing/fragile evidence |

Exact final copy may be refined in Stage 18, but the semantic distinction is locked here.

### 3.8 The recommendation is advisory, not a guarantee

**Decision:** Ready-to-Book copy must use evidence language, not certainty language.

Recommended default:

> **Ready to book**
>
> Your recent evidence supports booking TELC B1. Written and Oral are both in the safe pass range, and you have repeated passing performance under exam-like conditions. This is a preparation estimate, not a guarantee of the real result.

High-confidence variant:

> Your evidence is strong and consistent across recent target-condition attempts. It is reasonable to book the exam and switch to final preparation.

Avoid:

- “You will pass.”
- “Guaranteed ready.”
- “95% ready” when the number is not a probability.
- “TELC approved” or language implying official affiliation.
- treating booking as a reward unlocked by activity volume.

### 3.9 Ready-to-Book is current and reversible

**Decision:** Ready-to-Book is a current recommendation state, not a permanent achievement.

The state reopens to **Readiness under review** when any required condition becomes materially invalid, for example:

- the latest full-mock anchor becomes older than 14 days before the learner acts on the recommendation;
- Stage 15 Safe pass range is lost;
- component confirmation or required E4 evidence ages beyond its decision-grade window;
- a new clean target-condition result contradicts the current estimate;
- a productive evaluator correction changes a pass-relevant result;
- the target blueprint changes materially.

Historical “Ready to book achieved” may remain in progress history as a milestone, but current learner-facing advice must reflect the current evidence.

If the learner is already booked, the label changes to booked-exam risk language rather than asking them to undo the booking automatically.

---

## 4. Detailed Product Model / Rules for this Stage

## 4.1 Ready-to-Book decision rule

Evaluate in this order so that the reason for failure is explainable.

### Gate A — current target is valid

Require:

- TELC B1 remains the active launch target;
- the target blueprint used for readiness and P4/mock evidence is current/approved;
- affected content/evaluation is valid enough for the claim.

If not, show **Readiness needs verification** rather than producing booking advice from stale rules.

### Gate B — both components are Stage 15 Safe

Require:

- Written = Safe pass range;
- Oral = Safe pass range;
- therefore the Stage 15 Readiness Index is at least 65 under the current launch model;
- the lower planning range for each component stays at or above its pass line.

If either component is Borderline or Not ready, do not continue to a booking recommendation.

### Gate C — decision-grade breadth is still present

Require the Stage 15 written and oral decision-grade evidence minimums in full.

A full mock is not allowed to shortcut missing direct evidence, interaction, timing, or trustworthy productive evaluation.

### Gate D — fully current full-mock pass

Require one clean full mock within the last 14 days that clears:

- written ≥ current written pass gate; and
- oral ≥ current oral pass gate.

### Gate E — independent component consistency

Require, within 30 days and independent of Gate D:

- one additional clean written-component pass; and
- one additional clean oral-component pass.

A second full mock can satisfy both.

### Gate F — confidence and contradiction check

Require:

- overall confidence ≥ Medium;
- no unresolved pass-critical contradiction;
- no pending/low-confidence productive evaluation that could materially change the decision;
- no invalid target-condition/accommodation question that makes “same exam conditions” unsupported.

### Result

If Gates A–F pass: **Ready to book**.

Otherwise: retain the Stage 15 readiness band and attach a precise **booking blocker** such as:

- `Oral still borderline`;
- `Need one clean full simulation`;
- `Written pass needs a second confirmation`;
- `Speaking interaction evidence is too old`;
- `Writing evaluation is still uncertain`;
- `Target blueprint needs revalidation`.

There is no hidden aggregate booking score.

---

## 4.2 Booking evidence is an action layer, not a score layer

The product can conceptually expose:

- **Readiness:** performance estimate/range/band from Stage 15;
- **Evidence confidence:** Stage 15 Low/Medium/High;
- **Booking status:** Not ready / Close — performance / Close — confirmation / Ready to book / Booked — current / Booked — readiness under review.

These statuses must not become independent point systems.

### Suggested booking-status semantics

| Booking status | Condition | Coach job |
|---|---|---|
| **Not ready** | At least one component is Stage 15 Not ready | Repair the pass-critical component before seeking more mock consistency |
| **Close — performance** | No component Not ready, but at least one is Borderline because the estimate/range is too close to the pass line | Recover the smallest high-value point gaps and retest under realistic conditions |
| **Close — confirmation** | Both component point estimates look safe or are Safe, but the booking gate lacks full-mock, independent confirmation, recency, or confidence | Collect only the missing high-value evidence; do not prescribe generic extra study |
| **Ready to book** | Gates A–F all pass | Recommend choosing an exam date and transition planning toward final preparation |
| **Booked — current** | Exam booked and current Ready-to-Book conditions still hold | Protect readiness, rehearse execution, taper appropriately |
| **Booked — readiness under review** | Exam booked but current evidence is Borderline/Not ready/stale/contradictory | State risk clearly and triage remaining preparation time |

Stage 19 owns where these statuses live in the interface; Stage 18 owns final voice/copy refinement.

---

## 4.3 “Close but not ready” coaching

**Decision:** The coach distinguishes a **performance gap** from an **evidence gap**. It must never send every near-ready learner through generic extra lessons.

### Case A — performance gap

Use when Stage 15 is Borderline because a component estimate or planning range remains too close to/below the pass line.

Coach behavior:

1. name the pass component limiting booking;
2. identify at most **one or two recoverable blockers** by likely point impact;
3. use the normal Diagnose → Repair → Retry → delayed-transfer loop;
4. retest the smallest component/section that can prove the repair;
5. repeat a full mock only when it will answer a new whole-exam question.

Example:

> **Close — Oral needs a little more margin.** Your estimate is above the pass line, but the current range still crosses it. S3 negotiation is the main source of risk. We’ll repair that first, then repeat a clean oral component before asking for another full mock.

### Case B — confirmation/evidence gap

Use when performance estimates are strong but booking evidence is incomplete.

Coach behavior:

- if no fully current full mock: recommend the clean full simulation;
- if the full mock exists but Written lacks independent confirmation: recommend the written component only;
- if Oral lacks confirmation: recommend the oral component only;
- if one productive evaluation is uncertain: obtain the smallest fresh productive sample or one justified stronger evaluation;
- if evidence is merely aging: refresh the specific stale target condition rather than teaching unrelated material.

Example:

> **Your scores look ready; the evidence is not complete yet.** Both components are in the safe range. We still need one fresh oral component to show that the full-mock pass was repeatable.

### Case C — one component clearly Not ready

Do not hide the result behind “almost there.”

Example:

> **Not ready to book yet — Written is the blocker.** Oral is safely in range, but recent target-condition Written evidence remains below the pass line. The next plan focuses on the two highest-value written losses before another component mock.

### Case D — previously Ready, now stale

Do not call this regression unless performance declined.

Example:

> **Readiness needs refreshing.** Your last full simulation is no longer fully current. Your historical performance is unchanged; one fresh clean rehearsal will tell us whether the booking recommendation still holds.

---

## 4.4 Learner books before Bestehen says Ready

**Decision:** Booking is never locked by the App.

If the learner already has a date or books despite a non-ready recommendation:

- accept the date immediately;
- change the journey to Booked-exam preparation;
- show current Written/Oral readiness and evidence confidence unchanged;
- state the largest pass risk directly;
- prioritize the highest expected recoverable points and required target-condition evidence;
- reduce low-value breadth as the exam approaches;
- do not shame the learner or repeatedly tell them to cancel;
- do not raise readiness merely because the exam is now booked.

Suggested wording:

> **Exam booked — Oral is still the main risk.** Your date is fixed, so the plan will prioritize S2/S3 interaction and a clean oral retest. Booking does not change the readiness estimate; new evidence will.

Whether the learner should reschedule a real booking depends on personal constraints such as fees, appointment availability, certificate deadlines, and risk tolerance. Bestehen can show evidence and remaining time, but it should not present rescheduling as an automatic product rule.

---

## 4.5 Learner is Ready but does not book immediately

**Decision:** Ready-to-Book does not trigger full-mock spam while the learner waits for a suitable date.

If the learner delays:

- continue a low-burden maintenance plan;
- protect due review and known weak margins;
- use section/mini target-condition evidence to keep important areas fresh;
- refresh the full-mock booking anchor only when the learner wants a current booking recommendation or when evidence has materially aged;
- preserve the historical milestone but reopen current booking advice when the Stage 17 recency gates are no longer met.

The learner should see **“You reached Ready to Book on [date]; current recommendation needs a refresh”** rather than losing the achievement from history.

---

## 5. Booked-Exam Preparation Model

Booking changes the optimization objective from primarily **building readiness** to primarily **protecting, confirming, and executing readiness by a fixed date**.

The coach still uses the same learner model, Mistake Memory, Review, Stage 15 Readiness, and Stage 16 mock evidence.

### 5.1 Priorities after booking

In order:

1. **Protect pass gates.** The weaker Written/Oral component gets first claim on scarce time.
2. **Close high-value known risks.** Focus on one or two point-relevant weaknesses, not a long backlog.
3. **Confirm under target conditions.** Use the smallest realistic test that answers a current uncertainty.
4. **Preserve strong sections.** Brief maintenance prevents avoidable decay without wasting time on comfortable practice.
5. **Rehearse execution.** Shared timing, playback rules, Writing completion, oral preparation, interaction, and stamina matter more near the exam.
6. **Reduce novelty.** Low-frequency enrichment and broad new grammar/vocabulary increasingly lose priority unless they unlock a pass-critical task.
7. **Taper.** In the final week, prevent over-testing and late confidence damage that does not create time for useful repair.

### 5.2 Booking more than 21 days before the exam

If the exam is booked but more than 21 days away, keep the normal deadline-aware Daily Coaching Engine with these changes:

- the fixed date increases priority for current pass risk and target-condition evidence;
- the coach preserves enough realistic practice to prevent evidence from aging;
- full mocks remain event-driven rather than weekly obligations;
- new reachable learning is still worthwhile when it can materially improve expected exam points;
- the learner is not put into a permanent “final week” intensity merely because a booking exists.

At **21 days remaining**, the product automatically enters the Final Build & Confirm mode below.

---

## 6. Final 21-Day Preparation Mode — “Build & Confirm”

### 6.1 Activation

Activate when a booked exam is **21 days or fewer away**, regardless of whether the learner was Ready to Book before booking.

This mode is a planning policy, not a new readiness score.

### 6.2 Objective

**Maximize the chance that both pass components are current, stable, and executable on exam day while there is still enough time to repair meaningful weaknesses.**

### 6.3 21-to-15 days remaining — establish the final baseline

Coach priorities:

- re-evaluate Written/Oral Readiness and confidence;
- identify at most two pass-critical risks;
- inspect whether the latest clean full mock is current and informative;
- if no clean full mock exists within the recent evidence window, recommend one early in this phase when the learner can recover afterward;
- if a recent clean full mock already answers the whole-exam question, do not repeat it merely because the countdown started;
- repair the one or two highest expected point losses;
- schedule fresh delayed transfer after repair;
- preserve required E4 evidence in sections that are becoming stale.

For a learner already Ready:

> **21 days: protect the pass.** Both components are currently safe. This week we’ll refresh the weakest margin, confirm one realistic condition, and avoid unnecessary new material.

For a learner not Ready:

> **21 days: triage the pass risk.** Written is currently borderline. We’ll spend the next several sessions on the two most recoverable written losses, then test the component again.

### 6.4 14-to-8 days remaining — confirm repair and consistency

Coach priorities:

- use component mocks before another full mock when they answer the question more efficiently;
- obtain the second independent component confirmation required for Ready-to-Book/current-readiness confidence when still missing;
- retest repaired pass-critical areas under target conditions;
- confirm timed Writing completion and current oral interaction;
- maintain Reading/SB timing allocation and Listening playback discipline;
- use a second full mock only when complete sequencing/stamina/consistency evidence remains useful;
- follow Stage 16's normal separation guidance: do not crowd full mocks together, and use roughly **3 days as the normal minimum separation** in a near-term booked context.

A pass in one component does not justify abandoning it entirely. Strong components receive brief maintenance while most time goes to the weaker margin.

### 6.5 What 21-day mode stops doing

As the exam approaches, the coach progressively deprioritizes:

- broad CEFR coverage unrelated to current TELC point risk;
- low-frequency grammar/vocabulary enrichment;
- large backlogs of weakly evidenced old mistakes;
- repeated full mocks whose result will not change the plan;
- expensive generative interactions where a reviewed fixed scenario or component test answers the same question;
- correction of harmless B1-sufficient imperfections.

---

## 7. Final 7-Day Preparation Mode — “Taper & Execute”

### 7.1 Activation

Activate when a booked exam is **7 days or fewer away**.

The final week is not a crash course. The product goal becomes:

**Protect demonstrated ability, sharpen the execution routines that prevent avoidable point loss, and use only evidence checks that still leave time for a useful response.**

### 7.2 7-to-5 days remaining

This is the last normal window for a full mock **when a full mock still has clear information value**.

Recommend a full mock here only if:

- complete sequencing/stamina has not been measured recently;
- a major repair needs one final whole-exam confirmation;
- the learner has enough recovery time;
- fresh content and trustworthy productive evaluation are available.

Do **not** require a final full mock for a learner whose recent full/component evidence is already strong and current. A component or mini probe may be better.

After any final full mock:

- select at most one or two recoverable issues;
- use narrow repair and a smaller verification;
- do not chase every red item.

### 7.3 4-to-3 days remaining

Prefer:

- short target-condition section/part probes;
- one timed Writing outline or complete task only if Writing remains a risk;
- one bounded oral S2/S3 rehearsal if interaction remains a risk;
- Listening playback-rule refresh;
- Reading/SB allocation routine;
- due review of high-value known weaknesses;
- stable useful phrases and exam strategies already learned.

Avoid introducing broad new systems, phrase banks, or grammar topics unless the omission is clearly pass-critical and rapidly actionable.

### 7.4 Final 48 hours

**Decision:** Bestehen does not normally recommend a full mock in the final 48 hours.

Default behavior:

- brief high-confidence review of existing useful phrases/patterns;
- short, familiar exam-mechanism warm-ups rather than score-chasing;
- one concise oral or Writing activation only when it is confidence-preserving and not exhausting;
- remind the learner of target rules they have already practised: shared written timing, Listening playback behavior, Writing content-point checking, oral preparation/interaction;
- surface practical exam-day checklist/logistics only when Stage 19/23 later provides the appropriate product surface;
- reduce work volume rather than creating a “last chance” backlog.

The product should avoid turning normal late variation into a crisis. A weak 5-minute probe can be useful diagnostic evidence, but it should not trigger a panicked three-hour cram plan with no time for retention.

### 7.5 Learner is still not Ready in the final week

Do not soften the evidence language merely because the exam is close.

The coach should say:

- which component is at risk;
- the most recoverable one or two causes;
- the smallest practice/retest sequence that can still help;
- which strengths should be preserved;
- what uncertainty cannot realistically be removed before exam day.

Example:

> **4 days to go — Oral remains borderline.** S3 interaction is still the clearest risk. Today: one focused negotiation repair and one fresh oral retest. We will not spend the final days on unrelated grammar or another full mock unless this result changes the decision.

Whether the learner personally reschedules remains their decision; the App should not fabricate certainty either way.

---

## 8. Edge Cases / Failure and Uncertainty Handling

### 8.1 Written Safe, Oral Borderline

Result: **Not Ready to Book / Close — performance.**

- Overall readiness remains bottlenecked by Oral.
- Do not average the strong Written result over the Oral gate.
- Prioritize oral interaction/part evidence and the main recoverable blocker.

### 8.2 Oral Safe, Written Borderline

Mirror the same behavior for Written. Use written component/section evidence and repair rather than extra Speaking simply because Speaking is going well.

### 8.3 Both component estimates ≥65 but decision-grade evidence is incomplete

Result: **Close — confirmation**, not Ready.

The learner may be performing at a safe estimated level, but the booking recommendation waits for the exact missing target-condition evidence.

### 8.4 Both components Safe but no clean full mock exists

Result: **Close — confirmation: full rehearsal missing.**

Distributed E4 evidence can legitimately create Stage 15 Safe pass range, but Stage 17 requires one complete clean full simulation before recommending a consequential booking decision.

### 8.5 One clean full-mock pass but no second component confirmation

Result: **Close — confirmation.**

Recommend the missing component mock(s), not automatically another full mock.

### 8.6 Two clean full-mock passes but a newer component failure exists

Do not grant Ready based on mock count. Recompute Stage 15 Readiness. If the new result causes Borderline/Not ready or a material contradiction, move to Readiness under review and clarify/retest.

### 8.7 Full mock was paused, assisted, or technically compromised

Use all still-valid unit evidence according to Stage 16, but the attempt does not satisfy the clean full-mock booking gate if the full-mock claim was invalidated.

Technical failure is not learner failure. Repeat a fresh equivalent only when fairness and recovery permit.

### 8.8 Writing/Speaking evaluation is pending or uncertain

If the Ready-to-Book decision materially depends on an uncertain productive score:

1. do not recommend booking yet;
2. use one justified stronger/second evaluation when the existing Stage 12/13 escalation rules say it can materially resolve the uncertainty; or
3. collect a fresh productive sample if that is cheaper/more informative.

If confidence remains insufficient, preserve **Close — confirmation** rather than purchasing arbitrary certainty.

### 8.9 Target blueprint changes

A material blueprint change can reopen current readiness and booking advice. Historical performance remains learner evidence where the capability transfers, but target-condition status must be re-established against the approved current target.

### 8.10 Accessibility/accommodation changes the measured condition

Stage 25 owns the final product policy for accessibility and timed-condition equivalence.

Until that stage is shaped:

- non-answer-bearing access support may remain valid as Stage 15 already allows;
- preserve the actual condition on the evidence;
- do not claim exact target-condition equivalence when that equivalence is still unresolved;
- if the Ready-to-Book gate depends on an unresolved accommodation condition, keep the specific gate under review rather than treating the support as failure.

This is a documented cross-stage dependency, not an owner question.

### 8.11 Learner books very far in advance

Stay in normal deadline-aware coaching until 21 days remain. The learner may have been Ready at booking and later have stale evidence; that affects current readiness display, not the historical fact that the booking decision was evidence-supported when made.

### 8.12 Learner cannot find a suitable exam slot while Ready

Do not encourage repeated full mocks solely to preserve a badge. Use maintenance and targeted realistic refresh. Re-establish the 14-day full-mock gate when the learner is about to act on a booking recommendation or a material new risk appears.

### 8.13 Learner wants to book immediately despite Borderline evidence

Allow the learner to record the booked/target date. Switch to booked preparation and show the evidence gap. The App is an advisor, not a gatekeeper.

---

## 9. Relationship to Other Bestehen Stages

### Stage 02 — Complete Learner Journey

Stage 17 makes the existing **Readiness under review → Ready to book → Booked-exam preparation** transitions concrete. Ready remains reversible and booking early remains supported.

### Stage 04 — Learner Model

No new evidence store is introduced. Stage 17 consumes capability, condition, confidence, recency, provenance, and direct-lane evidence already represented there.

### Stage 06 — Daily Coaching Engine

The existing priority hierarchy continues to assemble sessions. Stage 17 changes urgency and introduces countdown modes, but does not replace the engine. Booked-date risk becomes a Tier 1 pass-risk obligation as already anticipated.

### Stage 08 — A1 → B1 Progression

Ready-to-Book evidence is predominantly P4/E4 target-condition evidence. Assisted P0–P2 progress remains valuable learning but cannot satisfy the booking gate.

### Stages 09–13 — Skill Coaching

The exact target constraints, direct-evidence lanes, Writing rubric, Speaking interaction, Listening playback, and shared written timing rules remain authoritative. Stage 17 does not create shortcuts around them.

### Stage 14 — Review and Spaced Repetition

Final preparation continues due high-value review and delayed transfer. The 21-day and 7-day modes reduce low-value backlog and use natural target-condition evidence to satisfy review where valid.

### Stage 15 — TELC Readiness

Stage 15 is the single source of truth for numeric/band readiness. Stage 17 adds **decision conditions** around that state; it never adds a new score.

### Stage 16 — Mock Exams

Stage 17 uses one fully current clean full-mock pass plus independent component confirmation. It intentionally preserves Stage 16's cost-saving principle that two full mocks are not inherently required.

### Stage 18 — Coach Personality

Stage 18 may refine exact wording, German/English balance, and tone. It must preserve Stage 17 semantics: calm evidence language, no guarantee, no shame after early booking or weak final-week evidence.

### Stage 19 — Information Architecture

Stage 19 decides where Ready-to-Book, booking blockers, countdown mode, and booked-risk state appear. The learner should not need to interpret raw evidence tables.

### Stage 23 — Notifications

Stage 23 may define reminders for a booked date, due final mock/component check, or high-value final-week action. It must not create generic countdown pressure or shame-based alerts.

### Stage 25 — Accessibility

Stage 25 must resolve when accommodations or altered timing/interaction conditions remain target-equivalent enough for P4/Ready-to-Book claims. Until then, actual support conditions remain explicit.

### Stage 26 — Analytics and Evaluation

Stage 26 should evaluate whether the launch 65-point Safe margin, 14-day full-mock anchor, 30-day confirmation window, and consistency rule predict real outcomes well. These are conservative initial product defaults, not psychometric truths.

---

## 10. Cost Notes

Stage 17 itself has **minimal recurring cost**.

### Low-cost default

- Ready-to-Book gating is deterministic over existing Stage 15 readiness and Stage 16 mock/evidence records.
- No AI call is needed to decide the booking state.
- No AI call is needed to generate routine booking-status explanations; structured templates can name the failed gate and next action.
- Objective written sections remain deterministically scored.
- A second full mock is not mandatory; component mocks can prove consistency with less learner time, less fresh-form consumption, and lower productive-evaluation/partner cost.
- Existing cached/reviewed mock content should be reused across learners only when fresh to that learner; no runtime generation is required merely because the learner enters Ready-to-Book review.

### Where paid evaluation is justified

Writing/Speaking already require bounded productive evaluation under Stages 12, 13, and 16. Stage 17 does not add routine calls.

One stronger/second evaluation may be justified when:

- a current clean productive response is otherwise valid;
- the Ready-to-Book decision materially hinges on the result;
- the normal evaluator is genuinely uncertain/contradictory;
- the escalation is cheaper and more reliable than unnecessarily repeating a full mock.

Cheaper fallback: keep the gate unconfirmed and collect another fresh productive sample/component mock.

### What would justify upgrading later

Only empirical evidence that a higher-cost partner/evaluator materially improves real-exam calibration, reduces false Ready recommendations, or adds target interaction fidelity should justify making it routine.

---

## 11. Decisions Made

1. **Ready-to-Book is a gate over Stage 15 Readiness, not a second score.**
2. **Both Written and Oral must currently be Stage 15 Safe pass range.** The launch performance requirement therefore inherits estimate ≥65, planning-range floor ≥60, decision-grade evidence, Medium+ confidence, and no pass-critical contradiction.
3. **The complete Stage 15 written decision-grade evidence minimum is required.**
4. **The complete Stage 15 oral decision-grade evidence minimum is required**, including real S2/S3 interaction.
5. **One clean passing full mock within 14 days is mandatory** for the booking recommendation.
6. **Independent consistency is mandatory, but two full mocks are not.** Within 30 days, Written and Oral each need another clean component pass on a separate fresh occasion; a second full mock may satisfy both.
7. **There is no Low-confidence Ready state.** Medium supports “Ready to book — sufficient current evidence”; High supports stronger wording.
8. **Near-ready coaching distinguishes performance gaps from evidence gaps.** The coach repairs only actual performance blockers and collects only the missing confirmation when scores already look safe.
9. **Booking never changes readiness.** A learner who books early receives deadline-aware risk coaching immediately without shame or artificial score uplift.
10. **Booked learners enter countdown-sensitive preparation.** More than 21 days out uses normal deadline-aware coaching; ≤21 days uses Build & Confirm; ≤7 days uses Taper & Execute.
11. **A full mock is optional in the final week unless it still answers a useful question, and is not normally recommended in the final 48 hours.**
12. **Ready-to-Book is reversible/current, while the historical milestone is preserved.**
13. **All numeric windows are launch heuristics to be recalibrated in Stage 26 rather than presented as official TELC rules.**
14. **Stage 17 adds negligible computation cost and does not introduce new routine AI calls.**

---

## 12. Open Questions / Deferred Decisions

### No owner decision blocks Stage 17

The available project context is sufficient to make the product decisions above. There are no unresolved owner-preference questions required to complete this stage.

### Deferred to later shaping

- **Exact coach wording and language selection:** Stage 18.
- **Screen placement, booking-status visualization, countdown UI, and exam-date controls:** Stage 19.
- **Content-generation/QA mechanics for the required fresh mock inventory:** Stage 21.
- **Reminder timing and notification behavior during 21-day/7-day modes:** Stage 23.
- **Accessibility/accommodation equivalence for target-condition timing and interaction:** Stage 25.
- **Empirical recalibration of 65 safety margin, 14-day full-mock recency, 30-day confirmation window, and false-positive/false-negative Ready recommendations:** Stage 26.
- **Architecture, data schema, rules engine, model provider, storage, and scheduling implementation:** architecture phase.

None of these deferrals requires changing the Ready-to-Book product contract defined here.

---

## 13. Definition of Done Check

- [x] Readiness threshold is explicit and derives from Stage 15 rather than a second score.
- [x] Adequate written evidence is explicitly required.
- [x] Adequate oral evidence is explicitly required.
- [x] Recency requirements are explicit and reuse Stage 15 windows.
- [x] Unassisted/timed/target-condition evidence is required.
- [x] Mock consistency is decided: one recent full pass + independent component confirmation; two full mocks optional.
- [x] Confidence language and no-guarantee wording are defined.
- [x] Close-but-not-ready coaching distinguishes performance from confirmation gaps.
- [x] Behavior after booking is defined for Ready and not-yet-Ready learners.
- [x] 21-day Build & Confirm mode is defined.
- [x] 7-day Taper & Execute mode is defined, including final-48-hour mock guidance.
- [x] Ready-to-Book is reversible when evidence becomes stale/contradictory.
- [x] Cost behavior is explicit and avoids new routine AI spend.
- [x] Cross-stage dependencies and deferred implementation/design decisions are documented.

**Stage 17 is complete when the coach can explain, from the existing evidence model, not only that the learner is near the TELC B1 pass range, but why the evidence is strong and consistent enough to justify spending money and committing to an exam date.**
