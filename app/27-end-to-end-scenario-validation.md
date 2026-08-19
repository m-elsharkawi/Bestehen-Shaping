# Bestehen / App — Stage 27: End-to-End Scenario Validation

> **Status:** Authoritative Stage 27 system-validation decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Validation promise:** A learner should experience one coherent exam coach from first A1 evidence through repair, deadline pressure, mocks, readiness, and booking advice; no transition may silently weaken evidence truth, independent Written/Oral pass constraints, learner agency, or the low-cost operating model.

## 1. Purpose and Scope

This stage stress-tests the complete App product shaped in Stages 01–26 as **one system** rather than as a set of individually sensible features.

The validation question is not whether each earlier document is internally plausible. It is whether representative learners can move through the product and receive a coherent answer to all of the following at the same time:

- **What does Bestehen currently know about me?**
- **What does it not know yet?**
- **What is the highest-value thing to do now?**
- **Why is that more useful than the alternatives?**
- **What evidence will the activity create?**
- **What changes if I use help, choose something else, run out of time, return after a break, or encounter a technical failure?**
- **How does the result affect capability, Mistake Memory, review, Readiness, and Ready-to-Book status?**
- **Does the coach remain calm, specific, and honest when the result is poor or the deadline is close?**
- **Can the complete behavior operate at personal-project cost?**

This stage validates the required scenarios:

1. A1 Day-1;
2. A2 midpoint;
3. strong Reading / weak Speaking;
4. 30-day deadline;
5. return after a break;
6. failed mock;
7. Speaking coaching;
8. Writing repair; and
9. transition to Ready to Book.

For every scenario, this document shows learner state, coach decision, selected activities, evidence updates, readiness changes, and learner-facing messaging.

### Validation result

**The shaped product is coherent across all nine required journeys.** No earlier product decision must be reversed. The scenario pass did reveal one integration need: earlier stages define their own local rules correctly, but later design/architecture needs an explicit **cross-stage precedence model** for moments when validity, deadline pressure, review, user override, and readiness all apply simultaneously. Section 4 defines that integration contract.

This is a **system-level clarification**, not a change to the underlying rules. It belongs in this Stage 27 validation artifact rather than being duplicated into every single-stage document.

---

## 2. Inputs / Existing Decisions

Stage 27 preserves the shared Product Overview, shared Identity, and all App Stages 01–26.

### 2.1 Product thesis and journey

Stages 01–02 establish that Bestehen is a personal **exam coach**, not a course catalog. It teaches German through TELC-shaped work from roughly A1 toward B1, adapts from evidence, preserves history across absence or failure, and centers the journey on readiness rather than lesson completion.

### 2.2 Evidence and mistake semantics

Stages 03–05 establish that:

- the first diagnostic builds a starting picture rather than assigning a permanent level;
- missing evidence is **unknown**, not zero;
- direct modality evidence is required for the modality being claimed;
- one failure is normally a candidate/provisional signal rather than an instant permanent weakness;
- known weaknesses require independent recurrence;
- same-session repair success shows responsiveness, while delayed fresh transfer is required for stronger repair/retention claims;
- technical/content/evaluator invalidity creates no negative learner evidence.

### 2.3 Daily coaching and progression

Stages 06–08 establish that:

- the standard daily session is 25 minutes, with bounded shorter/longer alternatives;
- one dominant priority is normal;
- pass risk and decision-relevant evidence gaps outrank generic breadth;
- support and difficulty progress per task family rather than through one global CEFR level;
- a difficulty wall causes a local adjustment to the causal axis rather than global demotion;
- a deadline changes opportunity cost and realism, not ability.

### 2.4 Skill contracts

Stages 09–13 define direct Reading, Language Elements, Listening, Writing, and Speaking behavior. The system-level constraints most relevant here are:

- strong performance in one task family or modality cannot substitute for missing direct evidence elsewhere;
- Reading + Sprachbausteine target timing uses the shared current 90-minute block rather than invented per-section official limits;
- target Listening preserves its playback rules;
- Writing is judged for TELC B1 communicative sufficiency, normally emphasizing one or two high-value corrections;
- same-prompt Writing revision does not retroactively improve the original score and does not replace a later fresh complete task;
- typed rehearsal cannot become oral evidence;
- S2/S3 readiness requires genuine interaction, not only monologue production;
- productive evaluation may remain pending when confidence or technical quality is insufficient.

### 2.5 Review, readiness, mocks, and booking

Stages 14–17 establish that:

- review is a due capability obligation, normally satisfied through fresh natural practice rather than a separate card-deck economy;
- Readiness is a target-performance estimate, not pass probability;
- Written and Oral remain separate pass risks and the overall launch index is bottlenecked by the weaker component;
- Safe pass range requires sufficient current direct evidence, Medium-or-better confidence, and a conservative planning-range floor at/above the pass line;
- mocks contribute according to their actual valid scope and do not receive a secret multiplier;
- one mock is one correlated evidence occasion;
- after a failed mock, repair and smaller retest normally precede another full mock;
- Ready to Book is stricter than Safe pass range and requires the complete Stage 17 gate: both components Safe, decision-grade breadth, a clean passing full mock within 14 days, independent written and oral pass confirmation within 30 days, Medium-or-better confidence, and no current pass-critical contradiction.

### 2.6 Coach, IA, motivation, content, control, deadline, analytics, cost, and platform

Stages 18–26 establish that:

- important coach messages use **fact → meaning → next action**;
- Coach/Home normally exposes one primary action, while Readiness explains the evidence picture and Train permits deliberate learner choice;
- no XP, classic streak, or activity economy may compete with readiness;
- learner-facing content is rights-safe, natural, fresh at the content-family level, and quality-approved for the evidence role claimed;
- learner choice changes immediate intent, not the semantics of evidence;
- exam-date urgency changes planning, priority, realism, and sometimes recommended workload, but never increases readiness by itself;
- product success is outcome/evidence-led rather than engagement-led;
- private personal-project operation is the initial default, with deterministic/cached behavior wherever it preserves quality;
- responsive web is the launch posture; high-stakes media/productive work requires preflight and evidence-preserving recovery;
- a slow or unavailable evaluator produces **Pending evaluation**, not a guessed score.

### 2.7 Checklist continuity note

The live App checklist has historical numbering drift: its existing Stage 27 section is the business/cost section that Stage 25 intentionally resolved early. This validation stage does **not** invalidate those completed business/cost decisions. The live checklist should retain that legacy Stage 27 continuity note and add the prompt-defined **Stage 27 End-to-End Scenario Validation** completion items beside it.

---

## 3. Decisions and Rationale

## 3.1 Treat scenario validation as an invariant test, not a new scoring system

**Decision:** Stage 27 introduces no new readiness score, mastery formula, CEFR level, mock multiplier, engagement metric, or AI classifier.

The scenarios test whether previously shaped state transitions produce a sensible next action. When a scenario requires a number, this document uses only the launch thresholds already defined by Stage 15/17. Otherwise it preserves uncertainty rather than inventing numerical precision.

## 3.2 One system decision must survive every scenario: evidence truth outranks convenience

A learner can ask for help, choose another skill, start a mock early, study on a phone, return after six weeks, or experience a network/evaluator failure. The App should remain helpful in all of those cases. What it may **not** do is preserve a stronger evidence label than the conditions support.

This invariant prevents several system failures:

- assisted work becoming independent evidence;
- typed Speaking becoming oral evidence;
- interrupted mocks remaining silently “clean”;
- a repaired same-prompt Writing answer overwriting a failed original attempt;
- strong Reading averaging away weak Oral;
- a near exam date manufacturing readiness;
- technical failure becoming a low learner score.

## 3.3 The daily plan resolves competing concerns by decision value, not by equal coverage

When several obligations exist at once, the coach chooses the smallest valid activity that can most improve or clarify the current **pass decision**, subject to learner time, environment, freshness, and reachability.

This means:

- a weak Speaking component can dominate the plan even while Reading is excellent;
- a due low-impact review may be deferred when a booked exam exposes a more urgent pass risk;
- a 30-minute component retest can be preferred to a three-hour full mock;
- a returning learner can receive one short recheck rather than a broad restart diagnostic;
- an A1 learner can receive a reachable version of the exam mechanism instead of generic chapter-based teaching.

## 3.4 Readiness movement and learning progress remain different

A scenario can be successful even when the Readiness Index does not move. Examples include:

- an A1 learner understanding a target mechanism with less support;
- a same-session Speaking repair showing responsiveness;
- a Writing revision fixing the teaching target but not yet proving fresh transfer;
- a returning learner refreshing one stale lane while the overall evidence base remains incomplete;
- a learner in Safe pass range completing the missing consistency evidence and becoming Ready to Book while the numeric readiness estimate barely changes.

This distinction is essential to both honest measurement and motivation.

## 3.5 High-cost capability is invoked only when the scenario needs it

The scenario model confirms the cost strategy from earlier stages:

- objective work is deterministically scored;
- routine planning/readiness/review/Mistake Memory is deterministic;
- content/audio is normally pre-generated, reviewed, cached, and reused;
- Writing and Speaking evaluation receive one bounded normal evaluation;
- adaptive Speaking is used when actual learner-specific interaction is the skill being tested;
- a stronger/second evaluation is reserved for high-impact uncertainty;
- a full mock is not used when a smaller measured block answers the decision more cheaply.

---

## 4. Detailed Product Model / Cross-Stage Precedence Rules

Earlier stages correctly define local behavior. This section defines what wins when several rules apply at once.

### Rule 1 — Validity and fairness come first

Before interpreting performance, decide whether content, media, equipment, timing, evaluator, and interaction conditions were valid enough for the claimed evidence.

If not:

- preserve completed unaffected work;
- downgrade, exclude, or keep pending only the affected evidence scope;
- do not create a learner weakness from the failure;
- choose the nearest valid retry or alternative.

### Rule 2 — Direct evidence beats cross-skill inference

A relationship between skills may suggest what to check next. It may not replace direct evidence.

Therefore:

- Reading cannot prove Listening;
- Writing cannot prove Speaking;
- typed oral rehearsal cannot prove oral production;
- a solo Speaking task cannot prove S2/S3 interaction.

### Rule 3 — The independent Written/Oral pass risk beats overall comfort

When one pass component is weak or under-evidenced, a strong other component does not lower its priority simply because the overall learner experience would feel more positive.

### Rule 4 — Clarify uncertainty before committing to a large repair

When evidence conflicts or the cause is uncertain, use the smallest fresh diagnostic/clarifying probe that can distinguish the important hypotheses. Do not build a multi-session remediation plan around a speculative fine-grained diagnosis.

### Rule 5 — Repair responsiveness is not retention

Immediate fresh retry can end the current repair loop. It does **not** by itself mark a weakness repaired/resolved or justify a broad readiness claim. Delayed fresh transfer remains required under the existing lifecycle rules.

### Rule 6 — Deadline urgency wraps the plan; it does not rewrite evidence

A nearer date can:

- raise pass-critical blockers and stale evidence in priority;
- compress lower-value breadth;
- increase target-condition practice;
- justify a larger useful commitment when the learner has capacity.

It cannot:

- lower the evidence standard;
- count same-day correlated attempts as independent;
- transform assistance into target-condition evidence;
- allow strong Written evidence to cover Oral;
- mark the learner Ready merely because the exam is booked.

### Rule 7 — Return-after-break re-entry uses the smallest decision-relevant recheck

History survives absence. When evidence has aged:

1. retain prior capability and milestones as historical evidence;
2. lower current confidence/readiness contribution according to freshness rules;
3. identify the smallest set of stale/uncertain lanes that can change the current coaching decision;
4. recheck those first;
5. do not replay every missed review or restart the complete diagnostic unless the prior baseline was never usable.

If a deadline is also close, apply this rule **inside the deadline priority model**: recheck pass-critical stale evidence first, not the whole learner profile.

### Rule 8 — User override changes the plan, not the truth

A learner-selected valid task counts normally. Skipping, postponing, or choosing a strength creates no ability penalty. The original blocker remains unresolved until direct evidence changes it.

### Rule 9 — Pending productive evaluation blocks only dependent conclusions

When Writing/Speaking evaluation is pending:

- preserve the submitted response as the original immutable attempt;
- continue unaffected objective/review work when useful;
- withhold only the component/full-mock/readiness conclusion that depends on the pending evaluation;
- apply the result once when it becomes available;
- do not manufacture a temporary score to keep the UI complete.

### Rule 10 — Content inventory limits the evidence claim, not learner access to useful practice

If no fresh readiness-approved family is available:

- do not reuse exposed or near-duplicate content as independent confirmation;
- offer a lower-stakes valid practice alternative if useful;
- keep the evidence/booking gate explicitly unconfirmed;
- do not penalize the learner for the product inventory gap.

### Rule 11 — The smallest decision-useful measurement beats a larger ritual

Choose mini/component/full mock by **information value**. A full mock is not automatically better because it is longer or more “real.”

### Rule 12 — Structured state wins over generated wording

All learner-facing messages in these scenarios are expressions of structured evidence state. If generated prose conflicts with validity, recurrence, readiness, or booking gates, the structured state and deterministic fallback copy win.

---

## 5. Scenario Validation

The learner states below are deliberately representative test fixtures. Numeric examples use only already-shaped thresholds; they are not new calibration claims.

## 5.1 Scenario A — A1 Day-1

### Learner state

- Learner reports roughly A1 German and wants TELC B1 eventually.
- No exam date is set.
- The initial diagnostic produced a usable but sparse starting picture: reachable Reading/Language Elements evidence, a short Listening sample, a basic functional Writing response, and a valid short spoken sample.
- Most work is P0 Supported Foundation; no P4/target-condition evidence exists.
- Confidence is intentionally Low/Moderate and the product does **not** have enough evidence for a defensible Readiness Index.

### Coach decision

Do **not** assign a generic A1 course or force a full B1 simulation. Start with one exam-shaped mechanism that is reachable and informative, then repair the narrow blocker exposed by the attempt.

### Selected activities

A representative first 20–25 minute coached session:

1. **Supported R3-style situation → notice matching** with short texts and limited vocabulary support, preserving the selective-reading/restriction mechanism.
2. One attempt without pre-correction.
3. If the learner matches by topic but misses a restriction such as time/day eligibility, give a 2–4 minute restriction-scanning repair.
4. One **fresh equivalent** match with different scenario/details.
5. Optional 3–5 minute short functional language review only if it directly supports the same communication need.

### Evidence updates

- The first attempt records the served P0 condition, assistance, direct Reading lane, outcome, and candidate cause.
- One restriction miss is a **candidate**, not a known weakness.
- Successful fresh retry shows repair responsiveness at the supported condition.
- It does not create B1 Reading mastery or target-condition readiness evidence.

### Readiness change

**No numeric readiness is shown.** The correct change is from a vague starting state toward better evidence coverage and a clearer reachable working rung. Progress may say that one exam mechanism is now understood with support.

### Learner-facing messaging

> **We have enough evidence to start coaching, not enough to judge TELC readiness yet.** You matched the topic correctly but missed the time restriction. We’ll train that exact reading behavior with shorter text first, then remove the support as it becomes reliable.

### Validation result

**Pass.** The system teaches through the target mechanism from Day 1 without pretending the learner is already working at B1 or replacing the exam-coach identity with a traditional A1 syllabus.

---

## 5.2 Scenario B — A2 Midpoint

### Learner state

- The learner has several weeks of evidence across all five areas.
- Reading and Language Elements are moving through P1/P2; many tasks are unassisted at A2/Bridge difficulty.
- Listening works with controlled speed/replay support but is not yet stable under target playback.
- Writing can complete short communicative tasks with a checklist; fresh full B1 emails are not yet reliable.
- Speaking production is functional in short tasks, while interaction still needs bounded partner support.
- Several earlier weaknesses have survived delayed checks; one or two active weaknesses remain.
- No decision-grade P4 evidence base exists, so full TELC readiness remains incomplete.

### Coach decision

Avoid equal “A2 curriculum coverage.” Choose the capability that most blocks the move toward independent B1 while blending one due review obligation.

Representative decision: **Speaking interaction first**, because the learner can already produce basic language but still relies on predictable partner support.

### Selected activities

1. 12–15 minute S3 Bridge interaction with bounded partner branches.
2. Diagnose the first interaction breakdown, not every grammar error.
3. 3–5 minute repair on proposing an alternative after rejection.
4. Fresh short S3 interaction with a different planning scenario.
5. 3–4 minute due Listening retention check using a fresh audio family.

### Evidence updates

- Speaking creates direct oral interaction evidence at P2, with actual assistance/partner mode attached.
- Same-session fresh success may move the capability toward Functional/less support-dependent but does not prove retained repair.
- The Listening check may satisfy its Stage 14 due obligation if it directly tests the required recognition behavior.
- No cross-modal evidence is invented from vocabulary/grammar success.

### Readiness change

The headline may remain **Not enough decision-grade evidence**. Secondary progress can still show:

- stronger interaction capability;
- one support reduction;
- one retained Listening pattern;
- increased evidence coverage.

### Learner-facing messaging

> **Speaking is the best use of today’s 25 minutes.** You can produce the basic language, but interaction still depends on a predictable partner. We’ll practice one negotiation pattern, then check it in a fresh plan. Your Listening review fits at the end and can close one due retention question.

### Validation result

**Pass.** The system can show meaningful midpoint progress without inventing course completion, XP, or an unsupported B1 readiness number.

---

## 5.3 Scenario C — Strong Reading, Weak Speaking

### Learner state

Representative current evidence:

- Written component is currently **Safe**, with strong Reading and adequate direct evidence elsewhere; illustrative Written target estimate: **68/100** with decision-grade evidence.
- Oral has direct recent samples but repeatedly weak S2/S3 interaction; illustrative Oral target estimate: **57/100**, Medium confidence.
- Overall Readiness Index is therefore **57/100 / Borderline**, because the weaker component controls the launch index.
- Reading is fresh and does not need more than maintenance.
- The learner often prefers Reading because it feels comfortable.

### Coach decision

Make **Speaking interaction** the dominant priority. Keep Reading on minimal maintenance only when freshness requires it.

The learner may still choose Reading from Train. That Reading evidence remains valid, but it cannot resolve the oral blocker.

### Selected activities

Recommended 25-minute session:

1. 15–18 minutes of S2/S3 interaction targeting the repeated oral blocker.
2. One narrow repair and fresh interaction retry.
3. Optional 4–5 minute Reading maintenance only if due.

If the learner chooses `Train → Reading` instead:

- serve valid fresh Reading practice;
- state once that Speaking remains the pass blocker;
- return the next recommendation to Speaking afterward.

### Evidence updates

- Reading success strengthens Reading evidence only.
- S2/S3 work creates direct oral evidence and can confirm, repair, or narrow the oral weakness.
- If the interaction issue recurs independently, Mistake Memory can promote/confirm the known oral weakness under Stage 05 rules.
- A successful immediate retry is not enough to declare Oral repaired.

### Readiness change

- Reading improvement alone may leave the overall index unchanged at the Oral bottleneck.
- Fresh successful oral transfer can move Oral upward and narrow uncertainty.
- Overall readiness changes only when the weaker Oral component genuinely changes.

### Learner-facing messaging

> **Written is currently in the safe range; Oral is not.** Reading practice is still useful, but it will not change the current pass risk. Today’s best move is S3 interaction because that is what is holding the overall recommendation at Borderline.

### Validation result

**Pass.** The independent component gates survive a strong-skill preference; the product cannot average Reading comfort into oral readiness.

---

## 5.4 Scenario D — 30-Day Deadline

### Learner state

- Exact **planned** TELC date is 30 days away; it is not yet booked.
- Written evidence is near the pass line but not safely separated from it; one recent Writing sample is useful but target-condition confirmation is incomplete.
- Oral is under-evidenced in S3 and currently the larger uncertainty.
- The learner can normally study 25 minutes on weekdays and has one 45-minute weekend block.
- No clean recent full mock exists that would justify a Ready-to-Book recommendation.

### Coach decision

Enter the Stage 23 **22–30-day** policy: increase value for target-condition evidence and pass-critical repair, normally recommend 25–45 minutes on about five useful days when the learner has that capacity, but **do not** simply increase volume or force a full mock.

The first job is to reduce the largest pass uncertainty while there is still time to act on the result.

### Selected activities

Representative next sequence:

- **Today (25 min):** S3 interaction sample → narrow repair → fresh interaction check.
- **Next suitable 45-min block:** one clean 30-minute Writing target-condition response plus review of the result.
- **Following sessions:** delayed transfer on the confirmed blocker and brief maintenance for strong areas.
- **Measured follow-up:** component/section mock selected when it answers a specific readiness question.
- **Full mock:** recommended only once complete rehearsal will produce decision-useful information, not because the calendar crossed “30 days.”

### Evidence updates

- The planned date itself produces **no capability evidence**.
- Fresh S3 and Writing samples can close missing direct/target-condition evidence.
- Any assisted or modified attempt retains its actual lower evidence condition.
- If a component is still materially below Safe as the date moves toward 21/7 days, the plan becomes increasingly compressed and the App may state the date is at risk.

### Readiness change

Readiness changes only from new evidence. It can remain Borderline even as the plan becomes more urgent. If both components become Safe later but the Stage 17 consistency gate remains incomplete, the learner may be **Safe but not Ready to Book**.

### Learner-facing messaging

> **Your planned exam is 30 days away.** Oral is still the larger evidence gap, and Writing needs one clean timed confirmation. This week we’ll close those two questions before spending time on broad new material. The date makes them more urgent; it does not change the readiness estimate by itself.

If the evidence remains clearly risky and the date is still only planned:

> **This date is currently at risk.** We can keep preparing toward it, but moving the planned exam would give the weak component more time to become reliable.

### Validation result

**Pass.** Deadline pressure changes priority, evidence cadence, and later realism without manufacturing readiness or turning preparation into a minute quota.

---

## 5.5 Scenario E — Return After a Break

### Learner state

- The learner returns after **42 days** away.
- Before the break, Written evidence was reasonably strong and Oral had one repairing weakness.
- The historical attempts and milestones remain valid history, but important current evidence is now **aging for readiness** under the stricter Stage 15 recency model.
- Several review obligations would be chronologically “overdue” if treated like cards.
- No near-term booked date exists in this base scenario.

### Coach decision

Do **not** reset the learner, replay the initial diagnostic, or present an overdue backlog. Use the previous learner model to choose the **smallest representative recheck** that can tell the coach what still holds.

Start with the old pass-critical/repairing lane, then refresh one representative strong lane only if it changes current planning confidence.

### Selected activities

Representative 20–25 minute return session:

1. 8–10 minute fresh oral interaction check for the previously repairing S3 behavior.
2. If it still holds, one brief unassisted fresh check in the highest-value aging written area.
3. Rebuild the next plan from those results rather than from chronological missed review.
4. Reintroduce remaining due review only according to current pass value/freshness.

### Evidence updates

- Old evidence remains in history; its **freshness/readiness contribution** is reduced rather than deleted.
- Fresh direct success renews only the tested capability/condition.
- Fresh failure can reopen a prior weakness if recurrence criteria support it; one failure does not erase all historical progress.
- Missed days themselves create no negative mastery evidence.

### Readiness change

The current Readiness state may have become less certain because evidence aged. The learner should see **needs fresh confirmation / lower confidence**, not “you got worse.” A small successful recheck can restore current confidence in the lanes actually tested; the rest remains as old or aging evidence until refreshed.

### Learner-facing messaging

> **Your history is intact.** The last strong oral evidence is 42 days old, so the current estimate is less certain—not because we know your German got worse. One short S3 recheck will tell us what still holds; there is no backlog to clear.

### Validation result

**Pass.** Freshness and history remain separate, and return is an evidence-refresh problem rather than a punishment/restart event.

### Combined deadline branch

If the same learner returns with a booked exam in 10 days, Stage 23 urgency wraps this return rule: recheck the **pass-critical stale lanes first**, then enter final preparation. The product still does not run a broad restart diagnostic or clear old review chronologically.

---

## 5.6 Scenario F — Failed Full Mock

### Learner state

- The learner had previously reached a reasonably strong recent pattern.
- A clean full mock is completed on fresh readiness-approved content.
- Written clears its gate comfortably; Oral scores below the current **45/75** pass gate because S3 interaction collapses after the partner rejects the first proposal.
- The result conflicts with earlier stronger oral evidence.
- The mock itself is technically valid; this is not a media/evaluator failure.

### Coach decision

Treat the clean mock as strong **new E4 evidence**, but still one correlated occasion. Recompute readiness and confidence, identify at most two immediate priorities, and **do not** schedule an automatic second full mock.

The first priority is the pass-critical S3 interaction problem. If the fine-grained cause is not yet recurrent enough to become a permanent known weakness, keep it as a high-priority provisional blocker and clarify it with fresh work.

### Selected activities

1. Post-mock validity/result explanation.
2. 1–2 focused repair sessions on S3 response-to-rejection / alternative proposal behavior.
3. First delayed fresh transfer after the normal short interval.
4. Fresh oral component/part retest under increasingly target-like conditions.
5. Another full mock only when the repair has evidence or the exam date makes whole-exam rehearsal decision-useful.

### Evidence updates

- The mock result remains immutable.
- Valid written success strengthens/refreshes written evidence.
- Oral failure becomes a strong current contradiction and pass-risk signal.
- Same-root errors inside the mock do not count as several independent recurrence occasions.
- Repair and later retest create separate linked evidence episodes.

### Readiness change

- Written may remain Safe.
- Oral may move from Safe to Borderline or **under review**, depending on the recalculated range/confidence and conflict with earlier evidence.
- Overall readiness follows the weaker current oral state.
- Any previous historical milestone remains in Progress; current Ready-to-Book status can reopen if its conditions are no longer true.

### Learner-facing messaging

> **Written cleared the pass threshold in this simulation; Oral did not.** The main loss was S3 interaction after your first idea was rejected. One full mock is strong evidence, but it is one occasion and it conflicts with your earlier oral pattern. We’ll repair that interaction first and retest Oral before another full mock.

Avoid: “You failed again,” “your B1 level dropped,” or an immediate `Retake full mock` CTA.

### Validation result

**Pass.** A bad mock is consequential without becoming catastrophic, and the recovery path uses the smallest next measurement rather than score-chasing.

---

## 5.7 Scenario G — Speaking Coaching

### Learner state

- S1 production is functional.
- S2 is improving.
- S3 is P2/P3: the learner can make a first proposal but often stops after disagreement.
- Microphone and audio preflight pass; intelligibility can be judged.
- The learner has one prior similar failure, so recurrence is plausible but still needs careful cause handling.

### Coach decision

Run a real **interactive** S3 task, not a generic chatbot conversation and not a typed substitution. Judge communicative effect before surface grammar. Target the narrow interaction behavior that changes the outcome.

### Selected activities

1. Fresh S3 planning scenario with a bounded/adaptive partner that can react to the learner’s actual proposal.
2. Learner proposes; partner rejects/changes one constraint.
3. Diagnose whether the learner fails to respond, cannot formulate an alternative, or has an unrelated language/intelligibility issue.
4. 2–5 minute repair: one compact negotiation pattern plus a minimal example close to learner language.
5. Fresh S3 scenario with a different planning configuration.
6. Schedule delayed fresh interaction in another context if the retry succeeds.

### Evidence updates

- The original attempt is direct oral interaction evidence.
- If the same interaction failure recurs independently, the Mistake Memory can confirm the known pattern.
- Same-session fresh success is **responsive repair**, not retention/resolution.
- A later fresh successful S3 interaction can strengthen the repair lifecycle and oral evidence.
- Grammar imperfections that do not materially hurt B1 communication remain secondary.

### Readiness change

Immediate retry may improve capability evidence or reduce diagnosis uncertainty, but Oral should not jump to Safe from one repaired interaction. Strong oral readiness still requires all S1/S2/S3 coverage, genuine S2/S3 interaction, multiple fresh contexts, direct oral evidence, valid intelligibility, and target-like conditions.

### Learner-facing messaging

> **You started the plan clearly, but the exchange stopped when the partner rejected the first option.** The important issue is interaction, not the small word-order errors. Practice one alternative turn now, then use it in a fresh planning scenario.

After same-session success:

> **That repair worked in the fresh scenario.** Good evidence that the response pattern is usable now; we still need it to hold in another context later before calling it reliable.

### Validation result

**Pass.** Speaking remains modality-correct, interaction-specific, B1-sufficient rather than perfectionist, and selectively AI-backed only where live adaptation adds evidence value.

---

## 5.8 Scenario H — Writing Repair

### Learner state

- The learner completes a clean current-format **30-minute** Writing email on a fresh prompt.
- The response is understandable but covers only **3 of 4** content points.
- A repeated word-order pattern also weakens Formale Richtigkeit.
- Other style issues exist but do not materially threaten B1 communicative success.

### Coach decision

Keep the original measured result immutable. Emphasize **two** repair targets:

1. the missing communicative request/content point; and
2. the repeated word-order pattern that most affects correctness/readability.

Do not replace the learner’s email with a polished advanced model and call that learning.

### Selected activities

1. Show TELC-aligned result and content-point coverage.
2. Highlight the missing request and one representative word-order example.
3. Learner revises the relevant part of the same email.
4. Mark that revision as guided repair/responsiveness, not a new target-condition score.
5. Later, serve a **fresh complete email prompt** with different scenario/content wording.
6. If timing is relevant to readiness, the later full sample must also reproduce the required clean time condition.

### Evidence updates

- Original P4 Writing evidence and score remain unchanged.
- Same-prompt revision creates linked guided learning evidence.
- The immediate correction can show that the learner understands the missing request/pattern.
- A later fresh complete email is required before broad Writing/task-fulfillment improvement is claimed.
- If the same omission recurs across independent prompts, Mistake Memory can promote the pattern; one occurrence alone is not enough for an over-specific permanent weakness.

### Readiness change

The same-prompt revision does **not** retroactively raise Written readiness. A later fresh complete unassisted response can strengthen Writing evidence, confidence, and potentially the Written target estimate when Stage 15 evidence requirements are otherwise met.

### Learner-facing messaging

> **The email is understandable and covers 3 of 4 points.** The missing request is the main task loss; the second priority is the repeated verb-position pattern. Fix those two here, then we’ll test them on a fresh complete email before treating Writing as stronger.

### Validation result

**Pass.** Writing repair improves learning without contaminating the measured evidence or overcorrecting beyond B1 sufficiency.

---

## 5.9 Scenario I — Ready-to-Book Transition

### Learner state before final confirmation

Representative state using existing Stage 15/17 semantics:

- Written = **Safe pass range**, illustrative estimate **70/100**, planning-range floor ≥60, decision-grade evidence, Medium+ confidence.
- Oral = **Safe pass range**, illustrative estimate **67/100**, planning-range floor ≥60, decision-grade evidence, Medium+ confidence.
- A clean full mock on fresh content passed **both** current component gates **9 days ago**.
- A separate clean written-component pass exists **18 days ago**.
- The additional independent oral-component pass required by Stage 17 is **still missing**.
- No pass-critical contradiction exists.

The learner is therefore **Safe but not Ready to Book**.

### Coach decision

Do **not** recommend another full mock merely because booking is consequential. The missing decision is specifically oral consistency, so recommend the smallest valid evidence action: a clean oral component confirmation on fresh content.

### Selected activities

1. Oral preflight: microphone, audio, partner mode, content, target blueprint, and checkpoint reliability.
2. Full target-condition oral component: 20-minute preparation + S1 → S2 → S3 under the current valid interaction contract.
3. One bounded structured evaluation after completion.
4. If evaluation confidence is sufficient and the component clears its pass gate, recompute the Stage 17 gate deterministically.

### Evidence updates

On a clean passing oral result:

- the oral component receives another independent current measured confirmation;
- Stage 15 capability/readiness evidence is refreshed normally;
- Stage 17 Gate E (independent component consistency) becomes satisfied;
- no mock-count bonus is added;
- the Readiness Index may move little or not at all because the learner was already Safe.

### Readiness / booking change

Before the oral confirmation:

> **Safe pass range — not yet Ready to Book:** one independent oral pass confirmation is missing.

After the clean passing confirmation:

- Written remains Safe;
- Oral remains Safe;
- decision-grade breadth remains current;
- the passing full mock remains within 14 days;
- written and oral independent confirmations are within 30 days;
- confidence remains ≥Medium;
- no contradiction blocks the claim.

Result: **Ready to book — sufficient current evidence** (or the stronger wording if Stage 17 confidence is High).

### Learner-facing messaging

Before:

> **Your performance is in the safe pass range.** Booking is not recommended yet because we still need one independent oral pass confirmation. A full mock would add unnecessary time; the oral component is the missing evidence.

After:

> **Ready to book — sufficient current evidence.** Written and Oral are both in the safe pass range, the recent full mock cleared both gates, and each component has now repeated a pass under fresh exam-like conditions. This is a preparation estimate, not a guarantee of the real result.

If the learner then marks an exam date as booked, the date changes the plan to booked/final preparation according to Stage 23. It does not change the already-earned readiness evidence.

### Validation result

**Pass.** Ready-to-Book is a separate consequential gate over readiness, and the product chooses the cheapest evidence-equivalent confirmation rather than defaulting to another full mock.

---

## 6. Cross-Scenario Validation Matrix

| System invariant | A1 Day-1 | A2 midpoint | Strong R / weak S | 30-day | Return | Failed mock | Speaking | Writing | Ready-to-Book |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| Exam-shaped learning starts before B1 | ✓ | ✓ | — | — | — | — | — | — | — |
| Direct evidence lane preserved | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Missing evidence stays unknown | ✓ | ✓ | ✓ | ✓ | ✓ | — | ✓ | — | — |
| Written/Oral gates stay independent | — | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Same-session repair ≠ retention | ✓ | ✓ | ✓ | ✓ | — | ✓ | ✓ | ✓ | — |
| Deadline changes plan, not ability | — | — | — | ✓ | branch | — | — | — | ✓ |
| No punitive absence/backlog | — | — | — | — | ✓ | — | — | — | — |
| One mock is one correlated occasion | — | — | — | ✓ | — | ✓ | — | — | ✓ |
| Learner override cannot corrupt evidence | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Technical/content failure is non-learner | applies | applies | applies | applies | applies | applies | applies | applies | applies |
| Readiness and Ready-to-Book stay distinct | — | — | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Low-cost deterministic default holds | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | bounded AI | bounded AI | bounded AI |

**Result:** no required scenario requires a rule that contradicts the shaped product baseline.

---

## 7. Contradictions, Missing Rules, and Cross-Stage Corrections

## 7.1 Product contradictions found

**None requiring an earlier decision reversal.**

The important apparent tensions resolve cleanly under the existing model:

- **Strong Reading vs weak Speaking:** Stage 15's independent components/min bottleneck prevents averaging.
- **Deadline vs evidence quality:** Stage 23 changes priority but explicitly cannot change evidence semantics.
- **Autonomy vs coach authority:** Stage 22 lets the learner choose while keeping evidence interpretation non-overridable.
- **Failed mock vs prior strong evidence:** Stages 04/15/16 lower confidence/recompute rather than either ignoring the new result or globally resetting the learner.
- **Return after absence vs Mistake Memory:** Stages 04/14 preserve history and change freshness; missed review is not a failure event.
- **Repair vs measurement:** Stages 07/12/13 separate original attempt, repair, fresh retry, and delayed transfer.
- **Ready-to-Book vs cost:** Stage 17 permits component confirmation rather than mandating a second full mock; Stage 25 keeps the gate deterministic.
- **Accessibility/technical recovery vs target realism:** Stage 26 preserves access while recording the actual measured condition.

## 7.2 Integration rule clarified by Stage 27

**Clarification added:** when several stage rules apply simultaneously, use the precedence rules in Section 4. This closes the main system-level ambiguity without altering the local semantics of any earlier stage.

Most importantly:

- `validity → direct evidence → pass risk/uncertainty → due repair/retention → progression/coverage → preference` is the conceptual order for deciding what can be claimed and what should happen next;
- date urgency modifies the priority/value of valid actions but never moves ahead of evidence validity;
- return-after-break re-entry is scoped to the smallest decision-relevant stale evidence set rather than a broad restart;
- pending productive evaluation blocks only dependent conclusions, not the rest of the product;
- insufficient fresh P4 content is a product evidence gap, not a learner failure.

## 7.3 Earlier shaping documents amended

**None.** Scenario validation did not uncover a contradictory or missing *single-stage* product rule that would make an earlier artifact internally wrong. The integration behavior above is genuinely cross-stage and is therefore documented here, where future design/architecture agents can consume it once rather than through duplicated amendments.

If Stage 28 incorporates these precedence rules into the final specification, this Stage 27 artifact remains the audit trail explaining why they exist.

## 7.4 Cross-stage change log

| Change | Type | Affected stages | Repository action |
|---|---|---|---|
| Added explicit cross-stage precedence for validity, direct evidence, pass risk, uncertainty, review, progression, preference | Integration clarification | 04–08, 14–18, 22–26 | Captured in Stage 27; no earlier rule changed |
| Defined return-after-break + near-deadline composition | Integration clarification | 02, 04, 14, 23 | Captured in Stage 27; existing rules preserved |
| Defined pending productive evaluation as blocking only dependent conclusions | Integration clarification | 12–13, 15–17, 19, 26 | Captured in Stage 27; existing pending-state rules preserved |
| Defined fresh-content exhaustion as product evidence gap, not learner failure | Integration clarification | 16–17, 21, 25–26 | Captured in Stage 27; no evidence threshold weakened |
| Preserved legacy live-checklist Stage 27 business/cost completion while adding prompt-defined Stage 27 scenario validation | Checklist continuity correction | Checklist, 25, 27 | Live checklist updated; Stage 25 remains business/cost authority |

---

## 8. Edge Cases / Failure or Uncertainty Handling

### 8.1 Learner has less time than the recommended scenario block

Rebuild around the smallest complete valid commitment. Do not truncate a clean component/mock into an invalid fragment and silently retain the same claim. Deferred work remains a priority, not a failure.

### 8.2 Learner chooses a comfortable strength during an urgent weak-skill scenario

Allow it. Record valid evidence normally. Explain the opportunity cost once. Keep the unresolved pass blocker in the next recommendation.

### 8.3 Fresh retry content is unavailable

Do not reuse the exposed family as independent transfer. Either use a genuinely fresh lower-stakes alternative or leave the transfer/booking gate unconfirmed until suitable content exists.

### 8.4 Productive evaluation is slow

Show **Evaluation pending** after submission. The learner can continue with independent work. Readiness/booking conclusions that depend on the score remain withheld until the evaluation is trustworthy.

### 8.5 Productive evaluator remains uncertain after one justified escalation

Preserve uncertainty. Prefer another fresh sample later over an unbounded model-voting chain.

### 8.6 Technical failure inside a scenario

Apply Stage 26 recovery: preserve work, classify only the affected scope as modified/partial/invalid/pending, and never create negative learner evidence from infrastructure failure.

### 8.7 A close deadline and very low proficiency collide

The coach may enter compressed priority mode and still teach reachable exam mechanisms, but it must state that the date is **at risk** rather than invent a learning-velocity guarantee. For a planned/unbooked date, recommend moving it when the evidence gap is material. For a booked date, optimize recoverable points and execution while preserving the truth of current risk.

### 8.8 Learner becomes Safe but fresh P4 inventory cannot support Stage 17 confirmation

Keep the learner **Safe but not Ready to Book** and name the missing confirmation honestly. Do not reuse an exposed form or lower the gate because the product lacks inventory.

### 8.9 Accessibility changes the measured condition

Non-answer-bearing accessibility support keeps the same evidence where shaped. Extra time, transcripts, typed oral substitutes, or other evidence-sensitive accommodations use the actual condition. If target-equivalence for a formal accommodation is not verified, keep that specific claim under review rather than treating the learner as failed.

### 8.10 New evidence contradicts a recently earned milestone

Historical milestone remains in Progress; current state changes. A previously earned Ready-to-Book milestone can remain historical while current booking advice reopens.

---

## 9. Relationship to Other Bestehen Stages

### Stages 01–02 — Thesis and Journey

Stage 27 confirms that the full journey remains exam-coach-first from beginner evidence through booking. The product does not drift into a course, content catalog, or mock-test-only product at any scenario boundary.

### Stages 03–08 — Diagnostic, Learner Model, Mistake Memory, Daily Coach, Loop, Progression

These stages supply the state-transition machinery used by every scenario. Stage 27's precedence rules clarify how their evidence and prioritization semantics compose.

### Stages 09–13 — Skill Coaching

Scenario validation confirms that modality-specific rules remain necessary. No cross-skill shortcut is introduced by system integration.

### Stage 14 — Review

Review remains a capability obligation that competes by current value, not chronological debt. Return and deadline scenarios confirm that this model scales better than a backlog/deck model.

### Stage 15 — TELC Readiness

Stage 15 remains the sole readiness calculation. Stage 27 adds no scores or weights and confirms that the weaker Written/Oral component remains the correct system bottleneck.

### Stage 16 — Mock Exams

Failed-mock and Ready-to-Book scenarios confirm that mock scope/validity and one-correlated-occasion semantics remain coherent. Full mocks are not automatic recovery or confirmation rituals.

### Stage 17 — Ready to Book

Stage 27 validates the gate as a separate action decision over Safe readiness. The final confirmation scenario demonstrates why a component mock may be the correct evidence-efficient action.

### Stage 18 — Coach Personality

Every scenario can be communicated through fact → meaning → next action without motivational fluff, shame, or false certainty.

### Stage 19 — Information Architecture

Each scenario resolves naturally to the existing surfaces:

- **Coach** for the dominant next action;
- **Readiness** for current evidence/pass state;
- **Train** for deliberate override;
- **Progress** for history/milestones;
- **Goal** for deadline state;
- **Mock** for measured rehearsal.

No new primary destination is required.

### Stage 20 — Progress and Motivation

Scenario validation confirms that capability/evidence movement is sufficient to make progress visible when the headline readiness number is flat. No XP/streak substitute is needed.

### Stage 21 — Content Strategy

All repair, transfer, mock, and confirmation scenarios depend on genuinely fresh content families and approval levels. Content quality is part of the measurement instrument.

### Stage 22 — User Controls / Corpus Contract

The learner may override any recommended scenario path where already shaped. The current learner state and evidence semantics remain authoritative regardless of who chose the activity.

### Stage 23 — Exam Date / Scheduling

The 30-day and return-with-deadline branches validate urgency as a planning wrapper, not an ability modifier.

### Stage 24 — Analytics / Data

The scenarios produce exactly the structured evidence, readiness snapshots, repair lifecycle, session summary, mock summary, quality incidents, and cost summaries already required. No full clickstream or new analytics score is necessary.

### Stage 25 — Business / Cost

All nine journeys can preserve the complete coach at personal-project cost. High-cost actions are bounded to productive evaluation/real interaction/high-stakes uncertainty.

### Stage 26 — Platform / Accessibility / Reliability

Scenario validation relies on preflight, checkpointing, pending evaluation, capability-specific fallback, and evidence-preserving recovery. No technical failure path requires inventing a learner score.

### Stage 28 — Final Specification

Stage 28 should carry forward:

1. the nine validated reference journeys;
2. the Section 4 precedence rules;
3. the cross-stage change log;
4. the conclusion that no new score/navigation/persona/autonomy model is needed to make the system coherent.

---

## 10. Cost Notes

Stage 27 introduces **no meaningful new recurring-cost requirement**.

### Preferred low-cost default validated by scenarios

- A1/A2/Reading/Language Elements/ordinary Listening: reviewed cached content + deterministic scoring.
- Daily plan, review scheduling, learner-state update, readiness, Ready-to-Book, return logic, deadline logic, and scenario messaging: deterministic structured rules/templates.
- Writing: one bounded normal structured evaluation; one stronger pass only when a high-impact uncertainty justifies it.
- Speaking: fixed/bounded interaction where sufficient; adaptive partner only when learner-specific turn-taking is the behavior under test; one bounded evaluation.
- Failed mock recovery: component/part retest instead of another full mock when it answers the question.
- Ready-to-Book confirmation: component measurement instead of a second full mock when the component is the only missing gate.
- Content: pre-generate, review, cache, and rotate by learner freshness rather than runtime-generate every attempt.
- Audio: cached reviewed assets broadly; stronger audited assets for readiness-grade use.

### Cost failure rule

If the preferred evaluator/interaction path is unavailable or too costly, the fallback is **less richness, lower confidence, pending evidence, or a smaller valid activity**—never fabricated certainty.

### What would justify additional spend later

Only evidence that a higher-cost evaluator, interaction mode, audio path, or human review materially improves:

- B1 rubric consistency;
- oral interaction validity;
- false-ready/false-not-ready calibration;
- content defect rate;
- real-exam outcome prediction; or
- maintenance effort enough to offset its cost.

---

## 11. Decisions Made

1. **All nine required end-to-end scenarios pass without reversing an earlier product decision.**
2. Stage 27 adds an explicit cross-stage precedence model so later design/architecture can combine validity, direct evidence, pass risk, uncertainty, review, deadline, progression, and preference consistently.
3. Validity/fairness is evaluated before learner performance; technical/content/evaluator failure never becomes learner failure.
4. Direct modality evidence cannot be replaced by cross-skill inference.
5. Independent Written/Oral pass risk remains the system-level readiness bottleneck in every scenario.
6. Immediate repair success remains weaker than delayed fresh transfer, including Writing and Speaking.
7. A nearer exam date changes priority, realism, and useful workload, not demonstrated ability or evidence thresholds.
8. Return after absence preserves history and uses the smallest decision-relevant recheck; no diagnostic restart or review-debt replay is required.
9. Learner override affects planning but not evidence semantics or readiness truth.
10. Pending productive evaluation blocks only conclusions that depend on it; unrelated coaching can continue.
11. Fresh content-family independence remains mandatory for transfer, mocks, and Ready-to-Book confirmation.
12. A failed mock triggers focused repair + delayed transfer + smaller retest before another full mock by default.
13. Strong Reading cannot hide weak Speaking; comfortable self-selected work cannot erase a pass blocker.
14. Ready-to-Book can be earned with one clean full mock plus independent component confirmations; a second full mock is not required when a component test closes the actual evidence gap.
15. All scenario paths preserve the private/personal low-cost strategy and require no new always-on AI capability.
16. No earlier App shaping document requires amendment because no single-stage rule was found to be internally wrong; the only new requirement is the cross-stage integration contract documented here.

---

## 12. Open Questions / Deferred Decisions

### Owner questions

**None.** No product decision in this validation pass requires owner preference, legal-risk tolerance, or an unspecified business constraint.

### Deferred calibration, not product behavior

The following remain empirical questions rather than blockers:

- how quickly real learners move across P0–P4 per skill;
- how much readiness typically changes after the representative scenario actions;
- exact alert sensitivity for conflicting evidence and plateaus;
- whether current 65-point Safe guard band, recency windows, and Stage 17 consistency requirements predict real TELC outcomes well;
- evaluator calibration and model-provider choices;
- exact content inventory volume needed to keep fresh P4 forms available at expected usage;
- exact UI layout/copy polish for the validated flows;
- operational SLOs after real usage exists.

Stage 28 should preserve the shaped defaults and mark these as calibration/implementation concerns rather than reopen the product model.

---

## 13. Definition of Done Check

- [x] A1 Day-1 scenario is written and evaluated.
- [x] A2 midpoint scenario is written and evaluated.
- [x] Strong-Reading / weak-Speaking scenario is written and evaluated.
- [x] 30-day deadline scenario is written and evaluated.
- [x] Return-after-break scenario is written and evaluated.
- [x] Failed-mock scenario is written and evaluated.
- [x] Speaking scenario is written and evaluated.
- [x] Writing-repair scenario is written and evaluated.
- [x] Ready-to-Book scenario is written and evaluated.
- [x] Every scenario documents learner state, coach decision, selected activities, evidence updates, readiness changes, and messaging.
- [x] Cross-scenario invariants are validated.
- [x] Contradictions and missing/integration rules are explicitly reviewed.
- [x] Cross-stage precedence rules are documented.
- [x] Earlier-document amendment need is explicitly assessed.
- [x] Cross-stage correction/change log is included.
- [x] Technical/content/evaluator failure and uncertainty behavior is validated.
- [x] Learner-autonomy behavior is validated.
- [x] Deadline and return-state composition is validated.
- [x] Cost behavior is validated and introduces no new routine premium-AI dependency.
- [x] No owner-blocking question remains.

**Stage 27 is product-complete when the live App checklist reflects this validation and Stage 28 can use these scenarios as acceptance journeys for the final specification.**