# Bestehen / App — Stage 23: Exam-Date and Urgency Behavior

> **Status:** Authoritative Stage 23 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Urgency promise:** A deadline changes what is worth doing next, how much realism is useful, and how assertively the coach prioritizes — but it never changes what the learner has actually demonstrated.

## 1. Purpose and Scope

This document defines how Bestehen / App changes the learning plan when the learner has **no date, a target month, an exact planned date, or a booked exam date**, including what happens when the remaining time is insufficient for the current evidence gap.

It also resolves the existing live-checklist Stage 23 scope for **Notifications, Scheduling, and Habit Support**. The current agent prompt names Stage 23 **Exam-Date and Urgency Behavior**, while `Bestehen_App_Product_Shaping_Checklist.md` previously named Stage 23 **Notifications, Scheduling, and Habit Support**. These are tightly related product concerns: urgency creates the planning states that reminders and schedules must support. This document therefore covers both rather than discarding either requirement.

Stage 23 defines:

- no-date, target-month, exact-date, and booked-date modes;
- state transitions when a date is added, changed, cleared, booked, passed, or completed;
- daily workload recommendations and how they interact with the existing 10/25/45-minute session model;
- behavior when the learner is behind the useful preparation path;
- behavior when a deadline is unrealistically close;
- 60-day, 30-day, 21-day, 7-day, final-day, and exam-day modes;
- how urgency changes skill mix, evidence collection, review, mocks, and realism;
- reminder types, study scheduling, quiet hours, frequency caps, ignored-reminder behavior, and non-shaming missed-day recovery;
- the post-exam and outcome-pending state;
- low-cost defaults that do not require recurring AI planning or notification calls.

This is product shaping, not architecture. It does not choose a notification provider, job scheduler, database, calendar API, push platform, time-zone library, model vendor, or device-specific implementation. Later architecture may choose those mechanisms, but it must preserve the product semantics and limits below.

### Core decision

**Exam urgency is a planning modifier, never a readiness modifier.**

A nearer date may:

- move pass-critical weaknesses ahead of lower-value breadth;
- increase the value of target-condition evidence and TELC-specific rehearsal;
- shorten the acceptable delay before clarifying unknown or stale evidence;
- make a mock or component retest worth doing sooner;
- reduce time spent on low-impact enrichment;
- justify a larger recommended time commitment when the learner has capacity;
- make warnings more explicit and scheduling reminders more actionable.

A nearer date may **not**:

- increase the Stage 15 Readiness Index;
- change a Borderline result into Safe pass range;
- count assisted work as unassisted;
- count untimed work as target-condition evidence;
- weaken the independent Written/Oral pass constraints;
- create a fake pass probability;
- convert a booked date into evidence that the learner is ready.

The product must always be willing to say: **“Your date is close, but your current evidence still shows risk.”**

---

## 2. Inputs / Existing Decisions

Stage 23 preserves the shared Product Overview, shared Identity, and App Stages 01–22.

### 2.1 Journey and goal-state constraints

Stage 02 already establishes three broad onboarding paths:

1. **No date:** build readiness first and earn the right to recommend booking.
2. **Considering a date:** plan toward a tentative horizon while separating aspiration from readiness.
3. **Already booked:** activate deadline-aware coaching immediately and show risk honestly.

It also establishes:

- missed days cause replanning, not punishment;
- a changed exam date causes replanning, not history loss;
- a learner may book before Bestehen recommends it;
- after the exam, the journey enters Exam completed / outcome pending and then Passed or Not passed / partial result.

Stage 23 makes these date states precise and adds the target-month case.

### 2.2 Daily coaching constraints

Stage 06 defines the normal session model:

- **Quick:** 10 minutes;
- **Standard:** 25 minutes, the default;
- **Extended:** 45 minutes;
- custom ordinary practice: 5–60 minutes in five-minute increments;
- longer measured mocks remain separate commitments and are never silently compressed into a daily session.

The Daily Coaching Engine optimizes risk-adjusted expected readiness gain per useful learner minute, with pass-risk obligations above generic coverage or preference. It already states that a date changes **urgency and opportunity cost, not capability or readiness**.

Stage 23 therefore does not invent a second planner. It defines the deadline context and workload policy that Stage 06 consumes.

### 2.3 Review constraints

Stage 14 defines review as due coaching obligations with flexible windows rather than exact-day debt. The default learning-return sequence is same-session transfer, 1–3 days, about 7 days, about 21 days, and about 60 days. Missed days never create a punitive backlog, and valid natural practice may satisfy a due obligation.

Stage 23 may compress the *priority* of review near the exam, but it may not mark an overdue item as learned or force the learner to replay all missed review chronologically.

### 2.4 Readiness and booking constraints

Stage 15 is authoritative for Readiness:

- Written and Oral have independent pass constraints;
- the Readiness Index is the weaker target-performance estimate, not a pass probability;
- Safe pass range requires adequate direct, recent, increasingly target-condition evidence;
- readiness is reversible and must preserve uncertainty.

Stage 17 is authoritative for Ready to Book:

- both Written and Oral must be in Safe pass range;
- current decision-grade evidence must be present;
- a clean passing full target-condition mock within 14 days is required;
- each component needs an independent measured confirmation within 30 days;
- overall evidence confidence must be at least Medium;
- a booked date changes urgency, not the booking/readiness gate.

Stage 23 does not weaken those rules even when time is short.

### 2.5 Mock constraints

Stage 16 defines mini, section/component, and full mocks. Mock cadence is **event-driven**, not a fixed weekly quota. Full mocks are expensive in learner time, concentration, fresh-form demand, and productive evaluation; smaller measured scopes should be preferred when they answer the needed question.

Urgency may make a mock decision-relevant sooner, but does not justify repeated full mocks merely to create activity.

### 2.6 Coach and motivation constraints

Stages 18 and 20 establish that:

- the coach becomes more decisive under time pressure, not more emotional;
- warnings use fact → meaning → next action;
- “Only 9 days left — work harder!” style messaging is invalid;
- no classic streak, XP, lost-progress penalty, or shame-based missed-day behavior belongs in the product;
- weekly preparation consistency is descriptive and secondary to Readiness.

Stage 23 applies these rules to countdowns, reminders, missed sessions, and unrealistic deadlines.

### 2.7 User-control constraints

Stage 22 establishes a strong coached default with lightweight overrides. The learner may change today’s duration, choose another useful skill, postpone review, request assistance, or run a mock early. The learner also may set/change/clear an exam date.

The coach owns the recommendation and the semantics of resulting evidence; the learner owns participation and intent.

---

## 3. Decisions and Rationale

## 3.1 Use four planning date modes plus a post-exam mode

**Decision:** Bestehen uses four active preparation date modes:

| Mode | Learner meaning | Coach behavior | Countdown semantics |
|---|---|---|---|
| **No date** | “I want to become ready before I choose the exam.” | Optimize durable readiness and broad evidence; surface Ready-to-Book when earned | No invented countdown |
| **Target month** | “I intend to sit the exam during this month, but I do not know the exact day yet.” | Plan conservatively against a date range; encourage exact-date confirmation as the month approaches | Show a range, never a fake exact day |
| **Exact planned date** | “I am aiming for this specific day, but it is not yet confirmed/booked.” | Use exact horizon for urgency and workload; allow reschedule advice freely | Exact days remaining, labelled planned |
| **Booked exact date** | “This is the real exam date.” | Use the same evidence rules but stronger commitment-aware risk management and final-prep behavior | Exact days remaining, labelled booked |

After the exam, the learner enters **Exam completed / outcome pending**. Preparation urgency stops. Result entry then moves the learner to Passed, Not passed / partial result, or an optional “result not recorded” closed state.

### Why target month is distinct

A target month is useful planning information but is not an exact date. Converting “October” into an arbitrary October 15 deadline would create fake precision. Bestehen should instead preserve a window and become **conservatively urgent** as the earliest plausible date approaches.

For planning-band transitions, the App uses the **first day of the target month** to decide when the learner might need the more urgent behavior. Learner-facing copy still shows a range such as “Target: October · roughly 6–10 weeks away.” This intentionally errs on the side of being ready early without pretending the exam is actually on October 1.

If the learner knows the likely week later, they should be encouraged to set an exact planned date.

---

## 3.2 Date status and readiness status remain orthogonal

**Decision:** Date mode is a separate axis from Readiness.

Examples that must be valid product states:

- No date + Not enough evidence;
- No date + Safe pass range;
- No date + Ready to Book;
- Target month + Not ready;
- Exact planned date + Borderline;
- Booked in 12 days + Not ready;
- Booked in 5 days + Safe pass range but not Ready to Book because consistency evidence is incomplete;
- Booked in 18 days + Ready to Book;
- Exam completed + prior readiness under review.

The product must never visually imply that entering or booking a date causes a readiness jump.

---

## 3.3 Workload recommendations increase only when added time has plausible value

**Decision:** Bestehen does not react to a closer exam by blindly multiplying daily minutes. It first changes **priority and realism**, then recommends more time only when the learner has useful work that can fit the added commitment.

The existing 25-minute Standard session remains the normal unit. Urgency affects the recommended *frequency and use of Extended/measurement blocks*, not the definition of a normal session.

### Initial workload defaults

These are launch recommendations, not scientific requirements or minimum attendance rules:

| Horizon / mode | Normal recommendation | Extended/measurement use | Main intent |
|---|---|---|---|
| **No date / >60 days** | 25 min on ~4 useful preparation days per week | Optional 45-min session when valuable; mocks only when decision-useful | Sustainable capability growth and breadth |
| **31–60 days** | 25 min on ~4–5 useful days per week | 45 min 1–2 times/week when a productive block, section rehearsal, or deeper repair benefits | Close major gaps and increase B1 independence |
| **22–30 days** | 25–45 min on ~5 useful days per week | Add component/mini-mock blocks when they answer a readiness question | Convert learning into target-condition evidence |
| **8–21 days** | 25–45 min on most available preparation days, with deliberate rest/recovery | Use measured component/full-mock commitments selectively; avoid full-mock churn | Protect pass gates, repair recoverable blockers, rehearse execution |
| **2–7 days** | Usually one focused 25–45 min commitment on a study day; shorter is valid when fatigue is high | Only high-value measured work early enough to recover from it; no automatic full mock | Stabilize, refresh, and protect execution |
| **Final day / exam eve** | Optional 10–25 min light review or no study | No full mock; no heavy new repair campaign | Logistics, confidence from known strengths, rest |
| **Exam day** | No normal coaching workload | Optional 5–10 min warm-up only if learner wants it and it reduces friction | Arrive oriented, not exhausted |

### Workload guardrails

1. **Availability is a constraint, not a moral score.** If the learner can study only 15 minutes, the coach chooses the highest-value 15 minutes rather than complaining that 45 was recommended.
2. **No catch-up debt.** Missing three 25-minute days does not create a 75-minute obligation tomorrow.
3. **No ordinary marathon normalization.** The existing 60-minute normal-practice ceiling remains. Full mocks are separate and should not be stacked with another demanding session by default.
4. **More time must have a named purpose.** “Add 20 minutes today” is valid only if the coach can say what useful work the time enables.
5. **Fatigue can reduce evidence quality.** Near the exam, extra volume that makes target-condition performance worse is counterproductive.
6. **Learner override remains valid.** A learner may choose Quick, Standard, Extended, custom time, or rest; the plan adapts without punishment.

---

## 3.4 When behind schedule, triage scope before increasing volume

**Decision:** “Behind schedule” means the remaining learner availability is no longer sufficient to complete all currently useful preparation opportunities before the target horizon. It does **not** mean the learner has failed a planned number of minutes.

The coach responds in this order:

1. **Protect pass-critical current weaknesses** in Written or Oral.
2. **Close decision-relevant unknown/stale evidence** that could be hiding a pass risk.
3. **Protect due retention for recently repaired high-impact weaknesses** where forgetting risk is material.
4. **Prioritize target-condition execution** for skills already strong enough to measure realistically.
5. **Maintain current strengths only as needed to keep them fresh.**
6. **Drop lower-value breadth, rare patterns, and generic enrichment first.**
7. **Increase recommended time only if the learner has capacity and the added block has clear value.**
8. If the remaining path still exceeds available time, state that explicitly rather than creating an impossible plan.

### What “behind” never does

- It never replays all skipped sessions.
- It never clears missed review by marking it complete.
- It never forces equal section coverage for appearance of balance.
- It never suppresses Oral because Reading is cheaper to practice.
- It never turns every day into a mock.
- It never converts a weak readiness state into “on track” merely because the learner followed the schedule.

---

## 3.5 Unrealistic deadlines get an honest feasibility warning, not false optimism

**Decision:** Bestehen must recognize when the target date is too close for the current evidence state to justify a normal “on track” plan.

Because the product has no calibrated learning-velocity model at launch, it must not claim **“you need exactly 42 hours to become ready.”** Instead it uses a conservative rule-based feasibility assessment.

### Initial unrealistic-deadline triggers

A deadline should be labelled **At risk for this date** when one or more of these conditions apply:

- the exam is within **21 days** and either Written or Oral is clearly Not ready with a pass-critical current blocker that has not yet shown successful fresh transfer;
- the exam is within **21 days** and a whole required modality/component remains materially under-evidenced, so the App cannot rule out a major risk;
- the exam is within **7 days** and either component remains below Safe pass range on current direct evidence;
- the exam is within **7 days** and required target-condition evidence is still substantially missing or contradicted;
- the learner is still predominantly at Supported Foundation / Guided A2 conditions in a pass-critical skill and the exam is close enough that a normal progression path cannot be responsibly described as likely to reach target conditions;
- the available study time the learner has provided is insufficient even for the highest-priority remaining repair/evidence commitments before the date.

These are **planning-risk triggers**, not predictions that passing is impossible. A learner can outperform current evidence. Bestehen simply refuses to call that a safe plan.

### Coach behavior by booking status

**Exact planned date, not booked:**

- state the risk plainly;
- recommend moving the target date when the evidence gap is material;
- offer the best plan for the current date if the learner keeps it;
- never shame the learner for changing the date.

**Booked exact date:**

- acknowledge the fixed commitment;
- do not repeatedly tell the learner to cancel;
- if rescheduling is realistically an option, surface it once as a decision, not as nagging;
- otherwise switch to **point protection and execution mode**: highest-value repair, strongest available section gains, target mechanics, timing, speaking interaction, writing task coverage, listening playback discipline, and exam logistics;
- keep Readiness honest throughout.

### Required message pattern

> **Fact:** “Your exam is in 9 days. Oral is still below the safe range in two recent measured attempts.”
>
> **Meaning:** “That makes Oral the current pass risk; the date does not change that evidence.”
>
> **Next action:** “Use today’s 45 minutes for S2/S3 interaction repair and a fresh measured check. Extra Reading is lower value right now.”

Avoid:

- “You can definitely catch up.”
- “There is no chance.”
- “You should have started earlier.”
- “Only 9 days left!” without an actionable reason.
- fake hour totals or pass probabilities.

---

## 3.6 Use milestone modes at 60 / 30 / 21 / 7 days

**Decision:** Exact-date and target-month preparation use named internal coaching horizons at **60, 30, 21, and 7 days**. They are planning modes, not learner levels and not new readiness states.

Crossing a horizon triggers one concise plan re-evaluation. It does not require a notification if there is no useful action.

### 60-day mode — Build and expose risk

**Primary objective:** Make sure there is enough time left to discover the real blockers rather than meet them for the first time near the exam.

Coach priorities:

- close major unknown Written/Oral evidence gaps;
- move pass-relevant skills from supported/guided work toward independent B1 where reachable;
- keep reviewing repaired high-value weaknesses;
- ensure Speaking and Writing are not postponed because they cost more effort to evaluate;
- begin target-condition probes for skills already stable enough;
- use mini/section mocks when they answer a concrete evidence or timing question;
- preserve broad enough task-family coverage that later readiness is not built on one narrow form.

Workload default: Standard 25-minute sessions on roughly four useful days per week, with occasional Extended or measured blocks.

Coach message example:

> “About two months remain. We still have time to build capability, but Oral evidence is too thin to leave until the final month. This week we’ll add two interaction samples while continuing your Listening repair.”

### 30-day mode — Convert capability into exam evidence

**Primary objective:** Stop relying on assisted/untimed success where target-condition evidence is now more informative.

Coach priorities:

- make current Written/Oral pass risk explicit;
- close remaining high-impact B1 gaps;
- increase P3/P4 work and current-format TELC specificity;
- verify shared timing/playback/preparation constraints that matter;
- use component mocks to answer pass-gate questions efficiently;
- schedule a full mock when the result will materially change readiness or final preparation;
- repair mock causes before simply repeating another full form;
- reduce time on low-relevance enrichment.

Workload default: 25–45 minutes on about five useful days per week when learner capacity allows, plus separate measured commitments when valuable.

Coach message example:

> “Your target is about a month away. Reading is already well covered; the higher-value work now is clean Writing timing and a full oral component. We’re shifting from learning evidence to exam-condition evidence.”

### 21-day mode — Final preparation begins

**Primary objective:** Use the Stage 17 booked-exam final-preparation model: protect both pass gates, make risk actionable, and stop broad curriculum expansion.

Coach priorities:

- identify the single biggest Written/Oral risk and a secondary risk at most;
- keep evidence fresh enough to trust decisions;
- repair only recoverable, high-impact weaknesses;
- emphasize current target mechanics and time allocation;
- schedule component retests after repair where they can answer a decision;
- use a full mock only when the learner can benefit from the whole-exam evidence/rehearsal and there is enough recovery time;
- maintain strengths without overspending minutes on them;
- begin explicit exam logistics prompts when a date is booked.

A learner who is already Ready to Book does **not** need to keep proving readiness every day. The plan shifts to stability, execution, and avoiding unnecessary volatility.

Coach message example:

> “Three weeks remain. Written and Oral are both in the safe range, so the goal is no longer to chase a higher score. We’ll keep Oral interaction fresh, do one planned full rehearsal, and protect Writing timing.”

### 7-day mode — Stabilize and protect execution

**Primary objective:** Preserve what the learner can already do, repair only high-yield issues, and avoid creating fatigue or confidence noise with unnecessary heavy testing.

Coach priorities:

- one primary pass-risk focus at a time;
- brief high-value due review and fresh transfer;
- target-condition rehearsal only where the result can still change action;
- no new broad grammar/vocabulary syllabus;
- no repeated full mocks by default;
- if a full mock is still useful, place it early enough in the week to diagnose and recover, not on the eve of the exam;
- refresh known exam routines: timing allocation, Writing content-point check, Listening playback discipline, Speaking interaction behaviors;
- keep logistics visible and low-friction.

Workload default: normally one 25–45 minute focused commitment on available study days; shorter sessions or deliberate rest are valid when they protect performance.

Coach message example:

> “Seven days remain. New breadth is lower value now. Today we’ll check the Writing content-point routine and do one short Oral interaction block; your strong Reading evidence only needs maintenance.”

---

## 3.7 Final-day and exam-day guidance prioritize execution, not learning volume

### Final day / exam eve

**Decision:** Bestehen should not recommend a full mock or a large new learning campaign on the day before the exam.

Default guidance:

- optional **10–25 minutes** of light, familiar review;
- revisit one or two known functional patterns only if they reliably help execution;
- review personal exam routines, not a giant content list;
- confirm time, location, identification/material needs, and practical arrival plan where the learner has entered those details or the product can show a generic checklist;
- avoid readiness score checking as a compulsive loop after every tiny warm-up;
- encourage normal rest and preparation without making medical or lifestyle claims;
- if the learner has a serious unresolved blocker, give one short high-value action and clearly state that the evidence remains risky rather than forcing a cram schedule.

Default coach message:

> “Tomorrow is execution day. Your best use of study time is a short familiar review, then stop. Do not spend tonight trying to relearn the whole exam.”

### Exam day

Default guidance:

- no normal daily plan;
- optional **5–10 minute** familiar warm-up only if the learner wants it;
- show concise exam routine reminders and logistics;
- do not run readiness recomputation from a tiny warm-up;
- no high-stakes warning barrage immediately before the exam;
- after the scheduled exam window, offer **Mark exam completed** rather than another training reminder.

---

## 3.8 Readiness truth is protected under urgency

**Decision:** The system must preserve the same evidence semantics in every horizon mode.

Urgency can change:

- *which* activity is chosen;
- *when* a due check is served;
- *how much* TELC specificity matters;
- *how soon* a component mock is recommended;
- *how much* learner time is requested;
- *how prominently* a risk is communicated.

Urgency cannot change:

- correctness;
- evidence tier;
- evaluator confidence;
- pass line;
- Written/Oral separation;
- Safe pass range criteria;
- Ready-to-Book criteria;
- mock validity;
- the fact that missing evidence is unknown.

A deadline-aware plan can become aggressive. The readiness model cannot become optimistic.

---

## 4. Detailed Product Model / Rules

## 4.1 Date-state model and transitions

### States

| State | Required learner data | Planning behavior |
|---|---|---|
| **NoDate** | None | Durable readiness plan; no countdown |
| **TargetMonth** | Year + month | Range-based urgency; conservative horizon transitions |
| **ExactPlanned** | Exact calendar date, not marked booked | Exact urgency; free reschedule advice |
| **BookedExact** | Exact calendar date + booked status | Exact urgency; commitment-aware final prep and logistics |
| **ExamCompleted** | Completion marker/date | Stop countdown/prep urgency; offer reflection/outcome follow-up |
| **OutcomePending** | Exam completed, result unknown | Optional maintenance only; no exam-date pressure |
| **Passed** | Learner-reported pass/result | Close TELC B1 goal; stop preparation reminders |
| **NotPassedOrPartial** | Learner-reported non-pass/partial result | Rebase next-attempt plan from known official outcome data |

### Transition rules

1. `NoDate → TargetMonth` when a month is entered.
2. `NoDate/TargetMonth → ExactPlanned` when an exact target day is entered but not booked.
3. `Any active date state → BookedExact` when the learner marks a confirmed date booked.
4. `ExactPlanned/BookedExact → same state with new date` on reschedule; evidence history remains unchanged and urgency is recomputed.
5. `TargetMonth/ExactPlanned → NoDate` when the learner clears the target; history remains.
6. `BookedExact → NoDate` is allowed only through an explicit cancellation/clear action so the App does not accidentally discard a real booking context.
7. `BookedExact/ExactPlanned → ExamCompleted` when the learner marks the exam done. A passed calendar date alone does not prove attendance.
8. `ExamCompleted → OutcomePending` immediately unless a result is entered at the same time.
9. `OutcomePending → Passed` or `NotPassedOrPartial` when the learner records the official outcome.
10. If a target month ends without an exact date or completion marker, change the goal status to **Date needs update** rather than assuming the learner sat the exam.
11. If an exact date passes without completion, ask once in-app: **“Did you take the exam?”** with Taken / Rescheduled / Not taken. Do not send repeated pressure notifications.

### Readiness-triggered transitions do not alter date mode

A learner can become Safe or Ready to Book while remaining NoDate or TargetMonth. The coach may recommend setting/booking an exact date, but readiness state and date state remain separate.

---

## 4.2 Target-month behavior

Target month requires special handling because it is a range.

Rules:

1. Show the month explicitly: `Target: October 2026`.
2. Show a human range when useful: `roughly 6–10 weeks`, not `53 days`.
3. Use the **first day of the target month** for internal urgency-band entry so preparation does not assume the learner gets the last possible date.
4. Do not show exact-day logistics or final-day mode without an exact date.
5. At the 60-day and 30-day boundaries, the coach may recommend confirming the exact exam day if known.
6. At approximately 21 days before the target month begins, make exact-date confirmation a visible planning action because the difference between an early- and late-month sitting is now material.
7. If the month begins and no exact date is known, use **high urgency but no fake exam-eve behavior**. Continue coaching, show “Exact date needed for final-day guidance,” and ask for the date at a natural planning moment.
8. Changing the target month recalculates workload/priority only; learner evidence is untouched.

---

## 4.3 Daily plan adaptation by urgency

The Daily Coaching Engine keeps its Stage 06 priority hierarchy. Stage 23 adds a horizon modifier to candidates.

### No date / long horizon

Increase value for:

- durable repair and retention;
- broad task-family evidence;
- prerequisite work;
- assistance removal when stable;
- section freshness without pressure;
- efficient original practice rather than repeated target simulations.

### Medium horizon (60–31 days)

Increase value for:

- unknown productive/oral evidence;
- independent B1 attempts;
- high-impact persistent weaknesses;
- first realistic timing/playback/interaction probes;
- content breadth that prevents a narrow readiness picture.

### 30–22 days

Increase value for:

- current target-condition evidence;
- complete component questions;
- timing and execution weaknesses;
- mock-linked repair;
- stale evidence that could change a readiness/booking decision.

Reduce value for:

- low-impact enrichment;
- generic broad-topic expansion;
- repeated comfortable strong-skill practice.

### 21–8 days

Increase value for:

- pass-gate blockers;
- recoverable productive/interactive weaknesses;
- fresh confirmation after repair;
- target-condition execution;
- component-specific retests where they are cheaper/more informative than a full mock.

### 7–2 days

Increase value for:

- known high-yield routines and stable patterns;
- brief fresh checks on pass risks;
- exam mechanics and execution confidence;
- sleep/fatigue-aware workload reduction as a product scheduling consideration, not a health prescription.

Strongly reduce value for:

- broad new learning;
- long speculative remediation;
- repeated full mocks;
- low-relevance review queues.

### Final day

Planning engine returns **light review / logistics / rest** as the default commitment rather than an ordinary optimization session.

---

## 4.4 Behind-schedule compression rules

When remaining useful work exceeds available time, the plan enters **Compressed priority mode**.

The learner sees:

- the current pass-critical priority;
- what the coach is intentionally deprioritizing;
- the expected commitment for today;
- whether the date itself should be reconsidered if not booked;
- a truthful readiness/risk state.

Example:

> “With 12 days left and about 20 minutes available on weekdays, we cannot cover every weak area equally. Oral interaction is the pass-critical risk, so it gets three of the next four primary sessions. Reading stays on maintenance only.”

The App must not claim that this schedule guarantees readiness. It is a **best-use-of-time plan**.

---

## 4.5 Mock logic under deadline pressure

Urgency changes *when a mock is useful*, not how mocks count.

Rules:

1. Do not recommend a full mock just because a milestone day was crossed.
2. Prefer mini/component mocks when they answer the needed risk question at lower learner and AI cost.
3. A full mock is most useful when the learner can understand the result, has enough time to repair anything discovered, and whole-exam sequencing/endurance is itself a question.
4. Inside the final 7 days, avoid a full mock by default unless it is early enough to produce actionable repair and the learner has not yet obtained necessary whole-exam evidence.
5. Never recommend a full mock on the final day.
6. A weak mock near the exam changes priorities but does not trigger an automatic second full mock.
7. A strong mock does not cause the coach to drop all maintenance or pretend weak independent component evidence disappeared.

---

## 4.6 Review behavior under deadline pressure

Review remains capability-based.

Rules:

- high-TELC-relevance due obligations may move earlier within their safe due window as the exam approaches;
- overdue queues are reprioritized by pass impact, not chronological age;
- low-impact or already well-covered obligations may be deferred beyond the exam rather than consuming scarce final-week time;
- a valid fresh mock/practice success may satisfy a due obligation normally;
- final-week review favors fast transfer checks and known functional patterns over broad card-like recall;
- missing a due review because of the exam schedule does not create a penalty or lower readiness by itself; only the absence/aging of evidence affects confidence according to existing models.

---

## 5. Notifications, Scheduling, and Habit Support

## 5.1 Principle: reminders exist to protect preparation value

**Decision:** Bestehen sends reminders only when there is a concrete preparation action or planning decision worth protecting.

A valid notification should answer at least one of:

- **What useful commitment is planned now?**
- **What due evidence/repair will become less useful if postponed?**
- **What mock commitment did the learner intentionally schedule?**
- **What exam-date milestone materially changes the plan?**
- **What logistics action matters because the booked exam is close?**

Invalid notification purposes include:

- increasing app opens for their own sake;
- protecting a streak;
- saying “we miss you”;
- vague “keep learning German” nudges;
- creating anxiety from a countdown that has no next action.

---

## 5.2 Reminder types

Bestehen supports the following product-level reminder types:

| Reminder | Default role | Default notification behavior |
|---|---|---|
| **Planned study reminder** | Protect a learner-configured preparation window | Primary routine reminder; opt-in/configurable |
| **Due-review reminder** | Protect a high-value repair/retention opportunity | Normally bundled into the planned study reminder or Coach plan; separate push only when unusually time-sensitive and no study reminder exists |
| **Mock reminder** | Protect a coach-recommended or learner-scheduled measured commitment | One reminder at the chosen time; optional earlier preflight for a long/full mock |
| **Exam-horizon reminder** | Mark a 60/30/21/7-day planning transition when it changes action | Milestone-based, not daily countdown spam |
| **Exam logistics reminder** | Protect practical preparation for a booked exact date | Final-day / exam-day only; concise |
| **Weekly coaching summary reminder** | Surface a meaningful evidence review when one exists | Optional; no reminder if the summary would be empty/noisy |
| **Post-exam outcome follow-up** | Ask for outcome when useful for closing/rebasing the goal | One gentle follow-up after the learner has marked the exam completed; no repeated nagging |

There is **no separate reminder per vocabulary item, mistake, or due review obligation**.

---

## 5.3 Configurable study schedule

**Decision:** The learner can set a simple weekly preparation schedule without configuring the coaching engine.

Schedule controls:

- preferred preparation days;
- one preferred start time or broad time window per selected day;
- usual session duration, reusing Quick 10 / Standard 25 / Extended 45 / custom bounded duration;
- whether reminders are enabled;
- temporary **Not today / Snooze / Change this week** controls;
- optional separate long-block window for a scheduled mock when the learner chooses one.

### Default behavior

- Bestehen should **not** assume a seven-days-per-week schedule.
- During onboarding, weekly availability may seed a suggested schedule, but reminders remain easy to edit or disable.
- If no schedule is configured, the App still creates a plan on open but does not manufacture routine push reminders.
- A schedule is a planning preference, not evidence and not a success metric.
- The coach can suggest changing the schedule when repeated overload or ignored reminders show that the current plan is unrealistic.

### Schedule and urgency

Near the exam, Bestehen may recommend adding a useful preparation window, but it must ask rather than silently changing the learner’s schedule.

Example:

> “Your exam is in 18 days and Oral needs two measured opportunities. Add one 45-minute block this weekend?”

The learner may decline. The coach then compresses priorities honestly.

---

## 5.4 Due-review reminders

**Decision:** Review notifications are **obligation-bundled**, not item-bundled.

Rules:

1. If due review already fits today’s coached session, the normal study reminder may say “Today: 25 min · Speaking priority + one due Listening check.” No second push is needed.
2. A standalone due-review notification is justified only when a high-value obligation is inside a narrow useful window and no normal study reminder will surface it.
3. Use one grouped action such as **“10-minute retention check due”**, never “17 items overdue.”
4. If the learner ignores or postpones it, reschedule according to Stage 14 priority and evidence freshness; do not repeat the same notification every day.
5. After a long absence, collapse old review debt into a new re-entry plan rather than firing historical reminders.

---

## 5.5 Mock reminders

**Decision:** Mock reminders are commitment reminders, not cadence pressure.

Rules:

- notify only for a mock the coach recommended as decision-useful or the learner explicitly scheduled;
- show expected commitment and setup: e.g. `Full mock · allow ~3 hours + oral setup` rather than a generic “Time for a mock!”;
- for a long/full mock, one optional preflight reminder up to a day earlier may be useful to protect time/equipment; it counts toward the frequency cap;
- if the learner ignores the mock reminder, return the mock to the coaching queue and reconsider whether it is still the highest-value action;
- do not reschedule a missed mock automatically every day;
- a learner-selected unscheduled mock remains available from Train without push pressure.

---

## 5.6 Exam-date urgency reminders

**Decision:** The countdown is primarily **in-app context**. Push reminders are tied to milestone changes or planned actions.

Default horizon reminders for an exact booked date:

- **60 days:** preparation-plan review if there is a meaningful gap to close;
- **30 days:** move toward stronger target-condition evidence;
- **21 days:** enter final-preparation mode;
- **7 days:** stabilize and protect execution;
- **1 day:** logistics + light-review guidance;
- **exam day:** concise practical reminder only if notifications are enabled.

Target-month mode can use 60/30/21/7 transitions relative to the first day of the month, but messaging must say **“Your target month is approaching”**, not “your exam is in 21 days.”

Do not send a separate push at every horizon if the learner already opens the App frequently and sees the state change. The notification exists to protect action, not to announce arithmetic.

---

## 5.7 Quiet hours

**Decision:** Default quiet hours are **21:00–08:00 in the learner/device local time**, editable by the learner.

Product rules:

- no routine study, review, mock, weekly-summary, or urgency notifications during quiet hours;
- if a chosen study time falls inside quiet hours, the learner’s explicit schedule wins for that reminder;
- exam-day logistics may appear before 08:00 only when the learner explicitly scheduled an early exam reminder or configured an earlier allowed window;
- changing time zone must not produce duplicate reminders or surprise overnight pushes; technical handling belongs to architecture, but the product contract is local-time respectful.

The initial 21:00–08:00 default is a product heuristic and may later be adjusted from user research. It is not a claim about optimal study hours.

---

## 5.8 Notification frequency caps

**Decision:** Notification volume is capped even when many obligations exist.

Launch caps:

1. **Normal preparation:** maximum **1 proactive preparation notification per calendar day** and normally no more than **4 proactive preparation notifications per rolling 7 days**.
2. **Booked exam within 21 days:** maximum **1 preparation/urgency notification per day**; the weekly cap may rise to **6** only when notifications are enabled and each message is tied to a scheduled/high-value action.
3. **Exam eve/day:** one additional **logistics** notification may coexist with a scheduled study reminder when materially useful, for a maximum of **2 notifications that day**.
4. System/account/security notifications are outside this coaching cap, but later stages must not use that exception for engagement nudges.
5. Several due reviews, a milestone transition, and a planned session should be **merged into one message** rather than consuming separate sends.

These caps are initial product defaults, not engagement-optimization targets. Stage 26 may measure whether they are too noisy or too weak.

---

## 5.9 Behavior when the learner ignores reminders

**Decision:** Bestehen decreases pressure when reminders are not useful.

Rules:

1. One ignored reminder simply leaves the plan available in-app.
2. Repeated ignored reminders do not escalate in emotional language or frequency.
3. After **three consecutive ignored routine study reminders**, suppress the next routine push and ask in-app at the next visit: **“Do you want to change your study days/time or turn reminders off?”**
4. If the learner does not open the App, routine pushes remain reduced rather than becoming a re-engagement campaign.
5. Major booked-exam milestone/logistics reminders may still occur if enabled because their value is different from a routine habit nudge, but they remain capped and factual.
6. When the learner returns, rebuild the plan from current evidence and time remaining. Do not show a missed-notification backlog.

---

## 5.10 Missed-day messaging

**Decision:** No missed day is framed as failure, lost progress, broken momentum, or coach disappointment.

Allowed:

- “Yesterday’s plan wasn’t completed. I rebuilt today around the highest-value remaining work.”
- “You have 20 minutes today, so we’ll keep the Oral check and defer lower-priority review.”
- “Your last current Writing evidence is aging. One fresh response will make the estimate more useful again.”

Avoid:

- “You missed your goal.”
- “Your streak is broken.”
- “Don’t fall behind again.”
- “You ignored three reminders.”
- “We missed you.”
- guilt-oriented countdown language.

A missed day changes **planning and possibly evidence freshness**, never mastery by itself.

---

## 5.11 Reminder-copy contract

Every proactive coaching reminder should contain:

1. **Action:** what useful thing is planned.
2. **Reason/value:** why it matters now, when space allows.
3. **Commitment:** time/scope when material.

Examples:

- `25 min today: Oral interaction first. It is still the booking blocker; Reading only needs maintenance.`
- `10-minute Listening check due. It will tell us whether Monday’s numbers-and-times repair held.`
- `Full mock tomorrow, 10:00. Keep about 3 hours free and test audio/mic before starting.`
- `7 days to your booked exam. Today’s plan is Writing timing + a short Oral check; no extra full mock is needed.`
- `Tomorrow is exam day. Keep review light and check your time, route, and required documents.`

Generic `Keep your streak alive`, `Come back and learn`, or `Only X days left!` messages are invalid.

---

## 6. Post-Exam State

## 6.1 Marking the exam complete stops urgency immediately

**Decision:** When the learner marks the exam completed:

- stop exam countdowns and final-preparation reminders;
- stop treating pre-exam due review as urgent debt;
- preserve all historical learner evidence and readiness history;
- keep the most recent pre-exam Readiness snapshot as a historical estimate, not a post-hoc official prediction;
- offer a short optional reflection while memory is fresh;
- do not infer an official result from the learner’s feelings after the exam.

### Optional reflection

The App may ask for a lightweight, non-scored reflection such as:

- Which component felt harder/easier than expected?
- Any format/timing surprise?
- Any task that could not be completed?
- Do you want to record anything before the result arrives?

This reflection is qualitative context. It does not retroactively rewrite the Stage 15 readiness score.

---

## 6.2 Outcome pending is a low-pressure state

While the official result is unknown:

- no daily TELC B1 urgency reminders;
- no requirement to maintain a readiness streak/state;
- optional light German maintenance can be offered if the learner wants it;
- the Coach/Home primary action becomes **Record result when available** only when appropriate, not every visit;
- one optional result follow-up reminder may be scheduled if the learner wants it or supplies an expected result date;
- without an expected result date, do not poll or nag repeatedly.

---

## 6.3 Passed

When the learner reports a pass:

- close the active TELC B1 preparation goal;
- stop exam-preparation reminders;
- preserve milestones and evidence history;
- show a concise summary of meaningful progress and the final preparation state;
- offer optional maintenance or a future goal without immediately inventing a new exam target.

The product should celebrate the real outcome more clearly than an internal milestone, while still avoiding theatrical gamification.

---

## 6.4 Not passed / partial result

When the learner reports a non-pass or failed component:

- treat the official component outcome as high-value outcome evidence for recalibration and replanning;
- do not infer detailed skill causes that the official result does not support;
- compare the official result with the pre-exam readiness estimate where appropriate;
- preserve strengths and repaired weaknesses rather than resetting the learner to zero;
- ask whether the learner wants to prepare for another TELC B1 attempt and, if so, capture a new date mode;
- prioritize the failed/weak component while still preserving the independent other pass gate for the next attempt;
- avoid language implying that prior work was wasted.

Stage 26 will later define analytics/calibration use of real outcomes. Stage 23 only establishes the learner-facing state transition.

---

## 7. Edge Cases / Failure or Uncertainty Handling

### 7.1 Date entered in the past

If a learner enters a past exact date, do not silently accept it as a future target. Ask whether it is:

- an exam already taken;
- a rescheduled/cancelled date;
- a mistaken entry.

No readiness interpretation changes until the state is clarified.

### 7.2 Target month is current month

Use the remaining date range and high-urgency planning, but do not invent an exact exam day. Ask for an exact date when known. Do not enter final-day mode without one.

### 7.3 Learner books before diagnostic completion

Enter BookedExact immediately, but prioritize enough broad evidence to identify major pass risk before overfitting the plan to small early signals. Show **Not enough evidence** where appropriate rather than fake optimism from the countdown.

### 7.4 Learner books while far below B1

Do not block the booking state. Show the booked date, current evidence limitations, and the best reachable plan. If the date is not realistically supported by current evidence, use **At risk for this date** language and a reschedule option if relevant.

### 7.5 Learner clears/reschedules date repeatedly

Recompute urgency each time and preserve history. Do not penalize indecision or create a “failed target” milestone. The coach may say that frequent date changes make workload planning less stable, but should still recommend the best current plan.

### 7.6 Readiness falls near the exam

A newer weak target-condition result may lower/qualify readiness. Do not freeze the old score for confidence. Explain the evidence change and choose the highest-value clarifier/repair that fits the remaining time.

### 7.7 Technical failure near exam

Technical invalidity is not learner failure. If a mock/listening/speaking attempt is invalid, preserve valid unaffected units, lower evidence confidence where necessary, and use a cheaper/smaller replacement measure if that can answer the decision before the exam.

### 7.8 Learner cannot use audio/microphone on a scheduled day

Use Stage 22 environment fallback: select the highest-value useful quiet-mode work while keeping the oral/listening obligation visible. Do not count text substitution as equivalent oral/listening evidence.

### 7.9 Learner requests much more than 60 minutes daily

Bestehen may support explicit long mock/rehearsal commitments, but it should not redefine normal coaching around daily marathons. Recommend splitting ordinary practice into separate focused blocks with a break. This is a product usability/fatigue guardrail, not a medical limit.

### 7.10 Learner studies less than recommended

Adapt to actual available time. Do not hide the trade-off. Example: “With 10 minutes today, we can protect the Oral repair but not complete the Writing retest. Writing remains tomorrow’s top evidence gap.”

### 7.11 Notifications unavailable or disabled

All urgency and scheduling behavior must remain fully usable in-app. Push notifications are convenience, not a dependency of the coaching model.

### 7.12 Time-zone/travel changes

Product semantics are local-calendar based. Avoid duplicate or overnight reminders and preserve the exam’s local date/time context where known. Exact technical conversion belongs to architecture.

---

## 8. Coach Messaging Examples

### No date

> **Today: 25 minutes of Listening.** Your appointment-detail repair is due, and Oral evidence is already fresh. There is no deadline pressure, so we can fix this properly before increasing realism.

### Target month

> **Target: October.** We still have a range rather than an exact exam day. Oral evidence is the area to close first so you are not discovering that risk inside the target month.

### Exact planned date, on track

> **42 days to your planned exam.** Written and Oral are both improving, but Writing still relies on untimed evidence. Today we’ll do one clean 30-minute response so the plan is based on stronger conditions.

### Exact planned date, unrealistic

> **Your planned exam is in 12 days.** Oral is still below the safe range and interaction has not yet held in a fresh measured check. I recommend moving the date if you can. If you keep it, Oral becomes the dominant priority from today.

### Booked date, behind plan

> **18 days to your booked exam.** We do not have enough time to treat every weak area equally. Speaking interaction is the current pass risk, so Reading moves to maintenance while we use three of the next four primary sessions on Oral.

### 7-day mode, ready

> **7 days remain.** Both components are currently in the safe range. This week is about stability and execution: one Oral refresh, one Writing timing check, and no unnecessary full-mock churn.

### 7-day mode, not ready

> **7 days remain.** Written is borderline and Writing timing is the main reason. The evidence does not support calling this safe yet. Today’s 45-minute block is a targeted Writing repair followed by one fresh timed response.

### Missed day

> **Yesterday’s plan wasn’t completed.** I rebuilt today around the highest-value remaining work. The due Listening check still matters; the lower-priority vocabulary review can wait.

### Ignored reminders

> **Want to change your reminder schedule?** The last few study reminders did not lead to a session. Choose different days/time, keep reminders off, or leave the plan in-app only.

### Final day

> **Tomorrow is execution day.** Keep review light: one familiar Writing checklist and your main Speaking interaction phrases, then stop. No full mock is needed today.

### Exam completed

> **The exam is done.** Your preparation countdown is closed. Record anything you want to remember now, or come back when the official result arrives.

### Not passed

> **The official result gives us better evidence for the next attempt.** We will keep the strengths you already built and rebase the plan around the component that missed the pass line. Nothing resets to zero.

---

## 9. Relationship to Other Bestehen Stages

### Stage 02 — Complete Learner Journey

Stage 23 makes the date states, booked-exam preparation, and post-exam transition concrete. It preserves Stage 02’s no-punishment return path.

### Stage 06 — Daily Coaching Engine

Stage 06 remains authoritative for activity prioritization and session assembly. Stage 23 supplies date horizon, urgency mode, feasibility risk, and workload recommendation context.

### Stage 08 — A1 → B1 Progression

Urgency may increase the value of advancing toward P3/P4, but it cannot skip the evidence needed to treat a learner as independently B1-capable. An unrealistic date does not collapse Supported Foundation into target conditions.

### Stage 14 — Review and Spaced Repetition

Stage 23 may reprioritize due review near the exam but preserves Stage 14’s capability-based due windows and non-punitive backlog behavior.

### Stage 15 — TELC Readiness

Stage 15 remains the sole readiness calculation. Exam date never changes the score directly.

### Stage 16 — Mock Exams

Stage 23 changes when mock evidence becomes urgent/useful, while Stage 16 remains authoritative for scope, validity, timing, scoring, and evidence semantics.

### Stage 17 — Ready to Book

Stage 17 remains the gate for recommending booking. Stage 23 defines planning after a date is selected/booked, including when the learner books before meeting that gate.

### Stage 18 — Coach Personality

Stage 18’s calm, direct, evidence-based voice remains authoritative. Urgency increases decisiveness, not emotional pressure.

### Stage 19 — Information Architecture

Goal / Exam Date remains the utility surface for setting target mode/date. Coach/Home shows days remaining and urgency only when it changes action. Readiness shows date context without letting countdown dominate evidence.

### Stage 20 — Progress and Motivation

No streak or missed-day penalty is introduced. Reminder behavior is subordinate to preparation value.

### Stage 22 — User Controls vs Coach Autonomy

The learner may change/clear/reschedule dates, schedule, reminders, and today’s available time. The coach recommends; the learner chooses; evidence semantics remain non-overridable.

### Stage 24 — Account, Data, and Portability

Later work must decide retention/sync/privacy for schedule, date, and notification preferences. Stage 23 defines the user contract only.

### Stage 25 — Accessibility and Device Experience

Later work must ensure reminders, countdowns, timed modes, and exam-day guidance remain accessible. It may refine platform-specific notification behavior without changing Stage 23’s semantic caps/guardrails.

### Stage 26 — Product Analytics and Evaluation

Later analytics should evaluate whether workload bands, unrealistic-deadline heuristics, horizon transitions, notification caps, and reminder suppression improve preparation outcomes without creating noise. Those heuristics may be recalibrated; readiness truth boundaries may not be weakened merely to improve engagement.

---

## 10. Cost Notes

Stage 23 has **no need for meaningful new per-session AI spend**.

### Preferred low-cost default

Use deterministic/product-state logic for:

- date mode and days/range remaining;
- 60/30/21/7 horizon transitions;
- workload-band recommendations;
- compressed-priority mode;
- unrealistic-deadline risk triggers;
- reminder eligibility;
- quiet hours and frequency caps;
- ignored-reminder suppression;
- post-exam state transitions.

Notification copy should default to reviewed templates populated with existing structured facts such as date, session duration, priority, blocker, and mock scope. There is no product justification for a premium model call merely to phrase “25 minutes of Speaking today.”

### Existing AI costs remain bounded

Urgency may cause a Writing/Speaking evaluation or interactive oral mock to happen sooner, but Stage 23 does not create extra evaluation semantics. Existing Stage 12/13/16 cost controls remain authoritative.

### When a stronger model could be justified

No new stronger-model use is required by this stage. If later experiments show that a model-generated weekly or deadline summary materially improves comprehension over deterministic composition, it may be generated **only after the underlying plan/risk state is already decided**, and it must have a deterministic fallback.

### No always-on expensive monitoring

The product should not require continuous AI re-planning. Urgency can be recomputed from current date, goal state, and stored learner evidence when the learner opens the App, completes meaningful evidence, changes a date/schedule, or when a scheduled reminder needs eligibility evaluation.

---

## 11. Decisions Made

1. Exam date is a planning modifier and never a readiness modifier.
2. Active preparation supports **No date, Target month, Exact planned date, and Booked exact date** as separate modes.
3. Target month preserves a date range; it never invents a synthetic exact day.
4. Target-month urgency transitions conservatively against the first day of the target month while learner-facing copy remains range-based.
5. Standard daily coaching remains 25 minutes; urgency changes frequency, prioritization, realism, and selective Extended/measurement use before it increases raw volume.
6. Initial workload guidance ranges from roughly four useful 25-minute days/week at long horizons to 25–45-minute focused work on most available days in final preparation, with light/no study on the final day.
7. Missed sessions never create catch-up debt.
8. Behind-schedule behavior triages pass risk and decision-relevant evidence before increasing volume.
9. Bestehen uses conservative rule-based **At risk for this date** heuristics instead of fake learning-hour or pass-probability forecasts.
10. If an unrealistic date is unbooked, the coach may recommend moving it; if booked, the product switches to best-use-of-time/point-protection behavior and avoids repeated cancellation nagging.
11. 60-, 30-, 21-, and 7-day modes have distinct coaching objectives but are not readiness states.
12. Final-day guidance avoids full mocks and broad new learning; exam day has no normal daily plan.
13. Urgency never weakens evidence validity, Written/Oral pass constraints, or Ready-to-Book gates.
14. Review is reprioritized near the exam but never turned into punitive backlog.
15. Mock cadence remains decision-driven; urgency does not create fixed weekly/full-mock quotas.
16. Notifications exist only to protect useful preparation actions/decisions.
17. Reminder types are planned study, due review, mock, exam horizon, exam logistics, weekly summary, and post-exam outcome follow-up.
18. The learner controls a simple weekly study schedule and may disable/snooze reminders without penalty.
19. Due-review reminders are bundled at obligation/session level, never per item.
20. Exam urgency pushes are milestone/action based, not a daily countdown by default.
21. Default quiet hours are 21:00–08:00 local time and are editable.
22. Normal proactive preparation notifications are capped at one/day and normally four/rolling seven days; booked final preparation may rise to six/week when each message is useful.
23. After three consecutive ignored routine reminders, routine push pressure is reduced and the App asks whether the schedule should change.
24. Missed-day copy is factual and replans; no streak-loss, guilt, or “we miss you” messaging.
25. Marking the exam complete immediately stops preparation urgency and enters outcome-pending behavior.
26. Post-exam reflection is optional qualitative context and does not retroactively rewrite readiness.
27. Passed closes the TELC B1 goal; non-pass/partial result rebases a future attempt without resetting prior learning.
28. All urgency, scheduling, and reminder logic has a deterministic low-cost default with no required premium AI call.

---

## 12. Open Questions / Deferred Decisions

### No owner questions block Stage 23

The product behavior can be shaped responsibly from the existing project principles. No owner preference is required to complete this stage.

### Deferred to later product/architecture work

- **Exact notification transport/provider and OS behavior** — architecture/platform decision.
- **Storage/sync/privacy for schedules and date history** — Stage 24 plus architecture.
- **Accessibility of notification and timed-mode presentation** — Stage 25.
- **Empirical recalibration of 60/30/21/7 workload guidance, unrealistic-deadline heuristics, quiet-hour default, and notification caps** — Stage 26 analytics/user evidence.
- **Precise real-exam outcome calibration of readiness/pass probability** — Stage 15/26; no deadline behavior may pre-empt it.
- **External exam-provider booking/calendar integration** — not required for the current personal-project product and intentionally not assumed.

These deferrals do not leave major Stage 23 product behavior undefined.

---

## 13. Definition of Done Check

### Agent-prompt scope

- [x] Define no-date mode.
- [x] Define target-month mode.
- [x] Define exact-date mode, including planned versus booked semantics.
- [x] Define daily workload recommendations.
- [x] Define how priorities adapt when behind schedule.
- [x] Define behavior for unrealistic deadlines.
- [x] Define 60-day mode.
- [x] Define 30-day mode.
- [x] Define 21-day mode.
- [x] Define 7-day mode.
- [x] Define final-day and exam-day guidance.
- [x] Define post-exam state.
- [x] Ensure urgency changes coaching but never fakes readiness.
- [x] Include state transitions.
- [x] Include workload logic.
- [x] Include coach messaging examples.

### Live Stage 23 checklist scope

- [x] Define reminder types.
- [x] Define configurable study schedule.
- [x] Define due-review reminders.
- [x] Define mock-exam reminders.
- [x] Define exam-date urgency reminders.
- [x] Avoid shame-based missed-day messaging.
- [x] Define quiet hours.
- [x] Define notification frequency caps.
- [x] Define behavior when the learner ignores reminders.
- [x] Keep reminders tied to preparation value, not generic engagement.

### Completion statement

**Stage 23 is product-complete when later design/architecture agents can take any learner date state — including no date, an approximate target month, a planned or booked exact date, an unrealistic deadline, missed study, ignored reminders, final-week preparation, or a completed exam — and know how the coach should adapt priorities, workload, reminders, messaging, and state transitions without changing the truth of Readiness.**
