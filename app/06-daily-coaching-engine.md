# Bestehen / App — Stage 06: Daily Coaching Engine

> **Status:** Authoritative Stage 06 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** TELC B1
>
> **Coaching promise:** Given the learner’s current evidence and available time, Bestehen chooses the highest-value reachable work, protects pass-critical coverage, and explains why each activity belongs today.

## 1. Purpose and Scope

This document defines how Bestehen / App turns the learner model, mistake memory, TELC B1 priorities, available time, review needs, evidence gaps, fatigue, and exam-date context into a daily coaching session.

The Daily Coaching Engine is the product behavior behind **“What should I do today?”** It is not a content browser, a fixed lesson sequence, or a black-box AI study plan. It owns:

- default and configurable session lengths;
- the objective and decision hierarchy used to assemble a session;
- the balance between exam weighting, weaknesses, spaced review, skill freshness, fatigue, deadline urgency, and section coverage;
- focused versus mixed-session behavior;
- changes caused by mock exams and a fixed exam date;
- learner overrides and the **“Why this today?”** explanation;
- partial completion, interruption, and resumption;
- a low-cost recommendation contract that does not require a premium model call.

This is a product model, not an implementation architecture or a final calibrated scoring formula. Later work may choose algorithms, storage, interfaces, and numerical coefficients. It must preserve the priorities, guardrails, explanations, and fallback behavior defined here.

### Core decision

**Bestehen assembles the session that offers the greatest expected, evidence-defensible improvement in TELC B1 pass readiness per useful learner minute, subject to written/oral pass constraints, due repair obligations, coverage, reachability, fatigue, and learner choice.**

This does not mean chasing the weakest percentage mechanically. A very weak but currently unreachable B1 task may be lower value today than a short prerequisite repair that unlocks it. Likewise, repeated comfortable Reading practice must not crowd out missing Speaking evidence merely because Reading is cheaper or easier to score.

### Out of scope

- the detailed Attempt → Diagnose → Repair → Retry interaction — Stage 07;
- the full assistance ladder and A1→B1 transition criteria — Stage 08;
- final TELC task mappings and skill rubrics — Stages 09–13;
- the complete review scheduler and calibrated intervals — Stage 14;
- readiness calculation, pass thresholds, and official blueprint weights — Stage 15;
- mock format, exact cadence, and pause rules — Stage 16;
- ready-to-book and final 21-day/7-day programs — Stage 17;
- screen structure and notification delivery — Stages 19 and 23;
- technical recommendation services, model providers, and storage.

## 2. Inputs / Existing Decisions

Stage 06 preserves the product overview, identity, and App Stages 01–05:

- Bestehen is a calm, direct, evidence-based personal German exam coach.
- The learner may begin around A1, but activities remain exam-shaped and point toward authentic TELC B1 performance.
- The coach should answer: **Where am I? What is holding me back? What should I do next?**
- Readiness is primary; engagement and easy completion do not outrank pass preparation.
- Written and oral pass risk remain separate. Strength in one cannot hide an unknown or weak other component.
- The learner model separates mastery, confidence, freshness, assistance, timing, and readiness contribution.
- Missing evidence is unknown, not zero. Direct evidence is required in each modality.
- Evidence flows upward from attempts to task patterns, sections, and written/oral views; rollups do not invent fine-grained mastery.
- Stage 04’s ordinary freshness bands are Fresh (0–30 days), Aging (31–60), Stale (61–120), and Historical-only (over 120), subject to stricter later readiness rules.
- Mistake Memory distinguishes candidates from known weaknesses and provides priority, due checks, reachability, lifecycle state, and repair evidence.
- Immediate retry success is not retained mastery. Delayed fresh transfer is required.
- The Stage 05 initial review sequence is same session, 1–3 days, about 7 days, about 21 days, and about 60 days, subject to Stage 14 calibration.
- A mock result is high-strength evidence, but one result does not automatically create every fine-grained known weakness.
- The learner may shorten, replace, or choose work; overrides do not erase personalization or count as failure.
- A fixed exam date changes urgency and opportunity cost, never capability or readiness.
- Corpus provides TELC relevance, task patterns, difficulty, frequency, skill relationships, and content intelligence. The App owns personal prioritization.
- Routine learner-state and scheduling decisions should be deterministic, explainable, cached, and inexpensive.

No earlier decision is changed. This stage resolves the session-duration and prioritization behavior deliberately deferred by Stages 01–05.

## 3. Decisions and Rationale

### 3.1 Default and configurable session lengths

**Decision:** The default daily session is **25 minutes**. The normal presets are:

| Session | Duration | Product promise | Normal shape |
|---|---:|---|---|
| Quick | 10 minutes | Complete one useful coaching commitment | One due check, evidence probe, or compact repair/retry loop |
| Standard | 25 minutes | Make one meaningful priority move while protecting continuity | One dominant block plus a short due/secondary block and summary |
| Extended | 45 minutes | Deepen one priority and add a second meaningful evidence block | One deep block, one secondary block, due work, and summary |

The learner may choose a custom duration from **5 to 60 minutes in five-minute increments**. Below 10 minutes, Bestehen offers a micro-session rather than pretending it can complete a full learning loop. Above 60 minutes, the product recommends separate sessions or an explicitly selected mock/long rehearsal with a break; it should not normalize unfocused daily marathons.

The learner can set a usual duration during onboarding and change **today’s available time** without altering the permanent default. The plan always shows its estimated duration before starting.

Full and section mocks are distinct commitments with authentic durations. They are never silently compressed into a 25-minute daily plan. When the learner has only 25 minutes, the coach may offer mock preparation, a mini-mock, or a section fragment only if it is honestly labeled and still yields valid evidence.

### 3.2 A session is a coaching commitment, not a pile of activities

**Decision:** A Standard session normally contains **one dominant priority** and no more than **two major skill contexts**. Small review items may cross skills, but the learner should not experience a random five-section sampler every day.

Indicative 25-minute budget:

| Component | Typical time | Purpose |
|---|---:|---|
| Due check / orientation | 0–4 min | Protect a scheduled repair or briefly activate the main skill |
| Dominant coaching block | 14–19 min | Attempt, diagnose/repair when needed, and obtain fresh evidence |
| Secondary evidence / coverage block | 0–7 min | Close a high-value evidence gap, preserve another section, or broaden transfer |
| Summary | 1–2 min | State what changed, what remains, and the next likely action |

These are elastic budgets, not quotas. A 25-minute interactive Speaking block may use almost the entire session. A day with several due micro-checks may use more review time. The engine optimizes for a coherent outcome, not compliance with a template.

### 3.3 Optimization objective

**Decision:** The engine optimizes for **risk-adjusted expected readiness gain per learner minute**, not activity completion, weakest-score reduction, or predicted enjoyment alone.

“Risk-adjusted” means the engine values both capability improvement and better evidence while discounting speculative diagnosis, repeated content, invalid conditions, or plans that are too difficult to produce a meaningful attempt. “Readiness gain” includes:

- repairing a confirmed pass-relevant weakness;
- proving that a repair transferred and remained stable;
- collecting missing or stale evidence needed for an honest decision;
- advancing a skill from assisted to less-assisted or from untimed to realistic conditions;
- protecting a previously reliable capability from decay;
- improving task execution, timing, or stamina when language knowledge is not the main blocker.

The engine may choose a task whose immediate score is unlikely to improve the readiness display if that task is necessary to resolve uncertainty or build a prerequisite. It must be able to explain that distinction.

### 3.4 Use a decision hierarchy before a weighted comparison

**Decision:** Session assembly uses a **lexicographic hierarchy plus a simple within-tier value comparison**. This prevents a large number of low-value bonuses from outvoting a pass-critical oral gap.

#### Priority tiers

| Tier | Candidate type | Examples |
|---|---|---|
| 0 — Required validity and safety | Work needed to make a planned activity valid and accessible | Working audio, microphone alternative, suitable difficulty, reviewed content, pending evaluation handling |
| 1 — Pass-risk obligation | A current written/oral blocker, booked-date risk, or evidence gap that prevents a responsible readiness decision | Unknown oral evidence; persistent timed Writing incompletion; booked exam with weak interaction |
| 2 — Due learning obligation | Time-sensitive repair, delayed transfer, or post-mock clarification | 1–3-day transfer check; unresolved high-impact mock cause; reopened weakness |
| 3 — High-value improvement | Active/recurrent weakness, readiness bottleneck, realism progression, or strong evidence opportunity | Listening restriction pattern; first unassisted task after stable guided success |
| 4 — Coverage and freshness | Aging section, under-sampled task pattern, topic/form breadth, or normal rotation | Listening not practiced recently; Writing prompt-category gap |
| 5 — Preference and exploration | Learner-requested useful practice, variety, or lower-priority improvement | Extra Reading chosen for confidence or interest |

Higher tiers are considered first, but they are not absolute commands. A Tier 1 B1 task that is unreachable may be converted into a reachable prerequisite or clarifying task. A due check can be moved within its safe window when fatigue, environment, or a booked-date obligation makes another activity more valuable.

#### Within-tier value dimensions

Candidates in the same tier are compared using small ordinal ratings rather than a pseudo-scientific pass-probability formula:

| Dimension | Question |
|---|---|
| Exam impact | How much can this capability or task pattern affect TELC B1 points or a written/oral pass gate? |
| Learner need | Is this unknown, weak, recurring, repair-resistant, or contradicted for this learner? |
| Review urgency | Is a transfer/retention check due, and what is the risk of waiting? |
| Evidence value | Will the task close a decision-relevant gap or replace stale/assisted evidence with stronger evidence? |
| Deadline/mock relevance | Does a booked date or recent/upcoming mock materially increase the value today? |
| Reachability | Can the learner make a meaningful attempt and likely benefit at the available support level? |
| Coverage value | Does the task prevent a section, task pattern, modality, or topic from being neglected? |
| Time efficiency | Can it produce a complete useful outcome in the time available? |
| Fatigue/environment fit | Is the cognitive load and required setup appropriate today? |
| Repetition penalty | Was the same content, form, modality, or repair used too recently to add independent evidence? |
| Diagnosis/quality risk | Is the cause, content, mapping, or evaluation too uncertain for targeted repair? |
| Operating cost | Can equal-quality value be delivered with reviewed/cached/deterministic material? |

Later analytics may calibrate the relative influence of these dimensions. The initial product requirement is that no opaque model may bypass the tier order, written/oral guardrails, or explanation contract.

### 3.5 Exam weighting and bottleneck protection

**Decision:** The coaching engine consumes the best available TELC B1 blueprint relevance for sections, task patterns, and rubric dimensions. Until Stages 09–15 finalize exact mappings and weights, it uses **ordered relevance bands**—core/high, meaningful, and supporting—rather than inventing precise official coefficients.

Rules:

1. Required and higher-impact task patterns receive more coaching value than rare supporting details, all else equal.
2. The engine does not allocate time in exact proportion to exam points. Weakness, evidence quality, reachability, and pass constraints still matter.
3. Written and oral bottlenecks override a flattering overall average.
4. Corpus frequency can raise relevance but cannot create a learner weakness.
5. Low-confidence Corpus mappings reduce the fine-grained priority; the engine may choose a broader reviewed task instead.
6. As the exam approaches, TELC-specific patterns and target-condition evidence increasingly outrank generic B1 enrichment.

### 3.6 Weakness, review, freshness, and coverage balance

**Decision:** Every plan balances four different forms of need without pretending they are the same:

- **Weakness need:** confirmed or probable point loss that may be repaired;
- **Review need:** a due transfer/retention check whose timing carries evidence value;
- **Freshness need:** previously useful evidence has aged and needs a concise recheck;
- **Coverage need:** a section, task pattern, modality, or relevant context has too little evidence or recent practice.

Balancing rules:

1. A known pass-relevant weakness normally outranks generic new practice.
2. A due repair check is protected because skipping it can waste the earlier repair and leave retention unknown.
3. Unknown or stale oral/written evidence can outrank a moderate known weakness if it blocks a responsible readiness view.
4. No section may remain unknown or stale indefinitely while the engine repeatedly serves a comfortable strength.
5. Coverage is assessed across a rolling history, not forced into every day.
6. A strong skill receives occasional maintenance and realistic checks, not equal daily time merely for symmetry.
7. Review demand is capped to the highest-value items that fit; missed days never create a punitive backlog.
8. Successful spontaneous use in normal practice can satisfy a due review when it is a valid opportunity; redundant micro-drills are removed.
9. “Skill freshness” means freshness of learner evidence. “Content freshness” means the task is sufficiently new to test transfer. Both matter and remain distinct.

### 3.7 Fatigue and cognitive load

**Decision:** Fatigue changes session composition and evidence interpretation; it does not become a language weakness by default.

The engine considers:

- learner-reported energy or preference for a lighter session;
- time of day and session length only if the learner has chosen to share/use that context;
- recent task load within the current session;
- consecutive high-load productive or listening blocks;
- observed deterioration that may reflect timing, stamina, technical quality, or confusion rather than knowledge.

Rules:

1. Avoid placing two high-load productive tasks back-to-back in a normal 25-minute session unless a mock/stamina objective justifies it.
2. Put the pass-critical or cognitively demanding task early when the learner is likely to have more attention.
3. On a low-energy day, shorten scope, increase coherence, and preserve one high-value completion; do not replace everything with easy points.
4. If fatigue may invalidate a result, lower evidence confidence or collect a later clarifier rather than diagnosing broad regression.
5. Near the exam, deliberate stamina work may temporarily override fatigue avoidance, but it is explicitly labeled as rehearsal.
6. Repeated learner-reported overload should suggest a more realistic default duration; it must not silently reduce the target standard.

## 4. Detailed Product Model / Rules for This Stage

### 4.1 Required planning inputs

The engine can use only evidence and context that the product has responsibly collected. The minimum conceptual inputs are:

| Input | Use in planning | Guardrail |
|---|---|---|
| Available time today | Sets the maximum meaningful session commitment | Do not squeeze an invalid fragment into the slot |
| Exam status/date | Changes urgency, realism, and opportunity cost | Never raises mastery/readiness |
| Section/task rollups | Identifies pass risk, coverage, and evidence gaps | Preserve written/oral separation |
| Fine capability states | Finds reachable skills and prerequisites | Missing is unknown; avoid exhaustive graph testing |
| Mistake-memory state | Supplies candidate/known status, priority, cause confidence, repair state, and due check | Unresolved causes get clarification, not speculative drills |
| Evidence freshness/confidence | Chooses rechecks and stronger evidence | High historical mastery may still need current evidence |
| Assistance/timing dependence | Selects appropriate support and next realism step | Do not compare assisted and target-condition evidence as equivalent |
| Recent session/content history | Prevents repetition and protects varied coverage | Same task/answer cannot become fresh evidence |
| Learner choice/environment | Accounts for energy, microphone, audio, and preference | Preference is not ability evidence |
| Content availability/quality/cost | Ensures a valid activity exists | Use reviewed fallback content when fine-grained content is unavailable |
| Mock context | Creates preparation, clarification, repair, and retest needs | One mock does not shotgun-label fine weaknesses |

### 4.2 Candidate activity types

Before assembling a plan, Bestehen generates only useful candidate commitments:

1. **Due transfer or retention check** — a fresh opportunity for a repaired/repairing pattern.
2. **Clarifying probe** — resolves a high-impact uncertain cause or contradictory evidence.
3. **Targeted repair loop** — works on a known reachable weakness.
4. **Evidence-gap task** — directly samples an unknown/under-evidenced section, modality, task pattern, or rubric dimension.
5. **Realism progression** — reduces help, adds timing, or increases authentic task conditions after working-level stability.
6. **Coverage/maintenance task** — refreshes an aging strength or neglected section.
7. **Mock preparation or recovery** — rehearses execution or repairs a mock-revealed blocker.
8. **Learner-requested useful task** — respects preference while remaining connected to the exam goal.

Every candidate must declare at product level:

- estimated time and whether it can end at a meaningful boundary;
- primary section/skill/task pattern and intended evidence;
- current difficulty, assistance, timing, and realism condition;
- exam relevance and expected coaching value;
- prerequisite state and reachability;
- cognitive load and setup needs such as audio/microphone;
- content freshness and quality;
- due window if applicable;
- known generation/evaluation cost class;
- the evidence-based reason that could be shown to the learner.

These are product requirements, not a prescribed database record.

### 4.3 Session-assembly pseudologic

~~~text
INPUT learner state, mistake memory, goal/date, recent history,
      available minutes, environment/energy, reviewed activity pool

1. Exclude activities that are invalid, inaccessible, too long to reach a
   meaningful boundary, based on exposed answers, or below the required
   content/evaluation quality.

2. Create candidates for:
   - written/oral pass-risk and evidence gaps,
   - due repair/retention checks,
   - active or high known weaknesses,
   - unresolved high-impact clarifiers,
   - needed realism progression,
   - aging/stale section evidence and coverage,
   - mock/date obligations,
   - useful learner preferences.

3. Convert unreachable high-priority targets into the smallest reachable
   prerequisite, scaffolded repair, or diagnostic contrast. Do not fill the
   session with repeated failure.

4. Assign each candidate to the highest applicable priority tier.
   Compare candidates inside that tier using exam impact, learner need,
   review/evidence value, urgency, reachability, time efficiency, fatigue fit,
   repetition/uncertainty penalties, and cost.

5. Choose one dominant commitment that fits today's time and produces a
   coherent outcome. Protect separate written/oral risk before optimizing
   smaller gains.

6. Reserve time for any due check that would lose material evidence value if
   postponed. A valid natural opportunity may replace a separate drill.

7. Add at most one secondary major block when it closes a meaningful evidence
   or coverage gap without fragmenting the session. Prefer related context or
   a different cognitive load.

8. Add a short summary. Remove the lowest-value optional block if estimates
   exceed available time; never rely on the learner rushing.

9. Generate “Why this today?” from structured reasons. Show the expected time,
   main goal, evidence basis, and any deadline/review reason.

10. If the learner overrides, preserve valid completed evidence, reassemble the
    remaining minutes, and retain unresolved priorities without punishment.

OUTPUT an ordered, time-bounded session plus explanation and alternatives
~~~

### 4.4 Tie-breaking rules

When two candidate plans remain similarly valuable, choose in this order:

1. the candidate protecting the weaker or less-evidenced **written/oral pass gate**;
2. the larger **recoverable TELC B1 point/rubric impact**;
3. the **due transfer/retention check** whose evidence value is most time-sensitive;
4. the task that resolves a **decision-blocking uncertainty**;
5. the higher-quality, more direct **target-condition evidence** opportunity;
6. the more **reachable transfer** with a complete outcome in the available time;
7. the more neglected section/task pattern or less recently practiced modality;
8. the better fatigue, accessibility, device, and environment fit;
9. the lower-repetition and lower-operating-cost option when learning value is equivalent;
10. the learner’s stated preference and then deterministic rotation toward the least recently served equal-priority option.

Cost appears late in the tie-break order on purpose: it decides between equivalent-quality choices; it does not displace a materially better pass-critical activity.

### 4.5 Focused versus mixed sessions

**Decision:** The normal Standard session is **focused with limited mixing**: one dominant priority uses roughly two-thirds or more of meaningful work, while due review or one secondary evidence need may use the rest.

#### Choose a focused session when:

- a high/pass-critical weakness requires a complete repair loop;
- a due delayed-transfer check should be followed by repair or broader transfer;
- a recent mock reveals one dominant recoverable blocker;
- the session is 10–15 minutes and switching would destroy coherence;
- a productive task needs setup, preparation, response, and evaluation time;
- the learner is low-energy and one useful completion is better than fragmentation;
- a booked exam makes one section or execution skill decisively urgent;
- the learner explicitly chooses a useful focus.

#### Choose a mixed session when:

- no single blocker dominates;
- several sections need freshness or evidence coverage;
- a short due review can be satisfied before the main task;
- the learner is in early Foundation/Bridge coaching and varied direct evidence is still needed;
- alternating receptive and productive load improves attention;
- a repaired capability needs natural embedding in a different task;
- the session is Extended and a second meaningful block fits.

#### Mixing guardrails

- Mixed does not mean random. Blocks should share a useful theme, skill relationship, or explicit coverage reason where possible.
- A 25-minute plan normally includes at most two major skill contexts.
- Do not add a token activity from every section for the appearance of balance.
- Do not use mixing to avoid an uncomfortable pass-critical weakness.
- Do not use focus to let all other sections become stale.

### 4.6 Fixed exam date and urgency

**Decision:** A date changes the value of time, realism, and coverage. It does not change what the learner has demonstrated.

| Exam context | Coaching effect |
|---|---|
| No date | Optimize for durable readiness, broad evidence, and efficient progression; recommend booking only when later criteria are earned |
| Considering a date | Use the proposed horizon for planning scenarios, but label it tentative and do not sacrifice foundations merely to make the date look feasible |
| Booked, more than 21 days | Keep normal repair/coverage balance, progressively increase target-condition evidence, and close unknown sections early |
| Booked, 8–21 days | Increase TELC-specific, timed, and mock-linked work; concentrate on recoverable pass-risk; use the Stage 17 21-day mode when defined |
| Booked, 0–7 days | Protect known strengths, rehearse execution, resolve only the highest-value remaining risks, reduce large new learning, and preserve rest/confidence; use the Stage 17 7-day mode when defined |
| Date has passed / exam completed | Stop ordinary readiness coaching and enter the Stage 02 post-exam path |

Additional rules:

1. The urgency band can raise a confirmed or evidence-backed candidate’s scheduling priority, but cannot promote an unresolved event into a known weakness.
2. Deadline pressure increases the value of TELC-specific task patterns, time management, interaction, and realistic conditions.
3. When available study time is insufficient, the coach states the trade-off plainly and prioritizes expected recoverable points plus exam execution. It does not inflate readiness or promise coverage.
4. A learner who books before being ready receives the best deadline-aware plan and an honest risk explanation, not a blocked experience.
5. Heavy new repair immediately before the exam is selected only when the expected benefit clearly outweighs confusion, fatigue, and lost rehearsal time.
6. Exact mock placement, tapering, and rest rules belong to Stages 16–17; this engine must be able to reserve time for them once defined.

### 4.7 How mock exams affect upcoming sessions

**Decision:** Mocks are high-strength evidence and rehearsal events that can materially reorder the next plan. They do not bypass diagnosis or mistake-memory safeguards.

#### Before an upcoming mock

- reserve the required time as a distinct commitment rather than fragmenting it into a normal daily plan;
- close essential format/instruction gaps before using the result as target-condition evidence;
- use only a brief warm-up that does not expose answers or exhaust the tested capability;
- avoid filling the prior session with heavy work that makes fatigue the dominant measurement;
- explain whether the mock’s purpose is baseline, section diagnosis, consistency, timing, stamina, or ready-to-book evidence.

#### After a mock

1. Preserve the section, task, rubric, timing, assistance, completeness, and technical conditions.
2. Separate knowledge/language, strategy, timing, attention, fatigue, and evaluation uncertainty.
3. Identify at most **two immediate coaching priorities**, led by written/oral pass risk and recoverable impact.
4. Treat one fine-grained error as a strong candidate unless the historical weakness is already confirmed; do not create many permanent labels from one mock.
5. Put urgent clarification or targeted repair into the next one to three suitable sessions.
6. Require fresh transfer outside the failed content before treating the repair as successful.
7. Prefer a section-level retest after material repair before repeating a full mock, unless Stage 16 or the fixed date makes another full rehearsal more valuable.
8. A passing mock raises confidence but normally calls for consistency evidence, not a permanent ready state after one attempt.
9. An incomplete or technically compromised mock contributes only valid partial evidence and is not silently scored as a complete failure.
10. A mock that contradicts stable history lowers confidence and creates a clarifier; repeated coherent realistic evidence should eventually dominate older assisted practice.

### 4.8 Learner override without destroying personalization

**Decision:** The coach recommends; the learner controls the day. Every plan supports the following overrides:

- change today’s duration;
- choose **lighter energy**, **no audio**, **no microphone**, or another relevant environment constraint;
- postpone a block;
- replace it with one of two or three useful alternatives;
- focus on a particular exam section or known weakness;
- browse/select other exam-relevant practice;
- stop early and continue later.

Override rules:

1. Never record refusal, postponement, or stopping as inability or a mistake.
2. Record preference/context separately so the current session can adapt; do not create a permanent trait from one choice.
3. Re-rank the remaining time and present alternatives near the same priority, duration, and equipment needs where possible.
4. If the learner bypasses a pass-critical gap or time-sensitive due check, state the consequence once in calm language: what will remain unknown or at risk and when it will return.
5. Repeated avoidance does not force the task. It triggers a clearer trade-off and, where possible, a shorter/lower-friction evidence route.
6. Chosen activities still update the learner model when their evidence is valid. Personalization continues from what the learner actually did.
7. Opting out of a section cannot be converted into a readiness claim; the evidence remains missing or stale.
8. Preference may decide close ties and improve adherence, but routine personalization must not become “always serve the favorite skill.”
9. Changing today’s duration does not silently change the normal default; the learner can choose to save it explicitly later.

Example trade-off:

> You can switch to Reading today. Speaking will stay the main readiness gap because we still have little recent oral evidence. I’ll offer the 8-minute Speaking check again in your next suitable session.

### 4.9 “Why this today?” explanation

**Decision:** Every recommended session has a short, evidence-backed explanation generated from structured reasons, not free-form motivational copy.

The default explanation contains:

1. **Priority:** the dominant skill, weakness, due check, or evidence gap;
2. **Evidence:** what recent observation or missing/stale evidence created the priority;
3. **Exam value:** why it matters for TELC B1 or a written/oral gate;
4. **Timing:** why it is useful today—due review, available time, mock/date, or coverage;
5. **Outcome:** what the session is expected to repair, verify, or measure.

Show no more than three concise reasons by default. Allow more detail on demand. Do not expose internal pseudo-precise weights.

Examples:

> **Why today:** Speaking interaction is your largest oral evidence gap. This 18-minute block checks how you respond to an alternative, then repairs the pattern if needed. Your exam is in 18 days, so fresh oral evidence is more valuable than another strong Reading task today.

> **Why today:** The Writing content-point check returns now because you repaired it two days ago. A fresh message will show whether the strategy stayed; the rest of the session refreshes Listening, which is beginning to age.

> **Why today:** We are not reteaching grammar. Your untimed Writing is functional, but the last mock was incomplete. Today’s task tests planning and pace under a shorter time target.

When the plan changes materially after new evidence, the coach names the change: “Yesterday’s mock made timed Writing the priority.” When no single issue dominates, it says so and explains the coverage choice.

### 4.10 Partial completion and resumption

**Decision:** Evidence is committed at meaningful activity boundaries. The session is re-planned from the remaining needs; it is not an all-or-nothing checklist and does not create a backlog.

#### What is preserved

- submitted/scored objective attempts;
- valid completed Writing or Speaking evidence and supported rubric results;
- completed repair steps and whether the solution/model was exposed;
- valid fresh retries and due checks;
- elapsed context, assistance, timing mode, and technical conditions;
- unfinished drafts when the later data policy permits, clearly marked unsubmitted/incomplete.

#### Interruption rules

| Interruption point | Resume behavior | Evidence treatment |
|---|---|---|
| Between activity blocks | Offer Resume today; later return re-ranks the unfinished blocks | Completed evidence stands |
| During an unsubmitted objective cluster | Resume if content integrity is preserved; otherwise replace with a fresh equivalent | Do not score missing answers as ability failure |
| During Writing/Speaking preparation or draft | Resume the draft if valid and desired; otherwise start fresh | Mark incomplete; evaluate only dimensions responsibly observable |
| After attempt, before feedback | Preserve the attempt and provide pending feedback later | Original evidence retains its original conditions |
| After explanation/model, before retry | Resume with a **fresh equivalent retry**, not the exposed original | Repair is incomplete; no independent mastery claim |
| After immediate retry, before delayed transfer | Session may end normally; schedule the delayed check | Responsiveness recorded, weakness not yet repaired |
| During a timed activity | Continuing after a pause may remain useful practice but cannot be called continuous exam-timed evidence | Preserve the pause/condition explicitly |
| During a mock | Follow Stage 16 rules; this engine must not relabel a paused/incomplete mock as fully realistic | Use only valid partial evidence |

#### Return timing

- **Same-day return:** default to resume when the activity remains valid and the learner has enough time; show the remaining estimate.
- **Later-day return:** re-rank unfinished optional blocks against new evidence, due reviews, date changes, and available time. Do not blindly carry yesterday’s plan.
- **After missed days:** select the highest-value due/stale items that fit. Do not demand that every missed review be completed.
- **After repeated early stops:** offer a shorter default or smaller activity boundaries, while preserving the exam goal and without inferring low ability.

The end summary reports **what was completed**, **what evidence was gained**, and **what remains**. It does not show a failed session percentage or punish the learner for stopping.

### 4.11 Plan status and completion semantics

A session may end as:

| Status | Meaning |
|---|---|
| Completed | The dominant commitment reached its meaningful evidence/learning boundary; optional blocks may have been re-ranked away |
| Partially completed | Some valid work exists, but the dominant commitment did not reach its intended boundary |
| Paused | A valid resumable state exists and the learner intends to continue |
| Replanned | The learner changed time/context and accepted a different useful commitment |
| Blocked | A technical, content, permission, or evaluation problem prevented valid completion |

These are coaching states, not rewards or failures. Only learner responses create capability evidence; session status itself does not.

## 5. Sample 25-Minute Sessions

The examples show the decision model in action. Exact task formats and rubrics remain for later stages.

### Sample A — Foundation/Bridge learner, no exam date

**State:** Listening details around appointments are an Active weakness at Bridge difficulty; a Reading restriction repair is due; Speaking has one low-confidence sample but is not the most urgent gap today.

| Time | Activity | Why selected |
|---:|---|---|
| 3 min | Fresh Reading restriction check | Due 7-day retention; valid natural check protects the earlier repair |
| 16 min | Appointment Listening block: fresh attempt → distinction repair → new audio retry | Reachable confirmed weakness with common exam value; records replay/support dependence |
| 4 min | Short unassisted Listening transfer | Tests whether the repair works without answer exposure |
| 2 min | Summary and next priority | Explains evidence gained and keeps Speaking visible for a later suitable session |

**Why this today:** The due Reading check would lose timing value if postponed, but Listening remains the dominant block because appointment details have failed in two fresh tasks and are reachable with a short repair. No date means durable transfer outranks immediate mock pressure.

### Sample B — Booked exam in 18 days, oral evidence is the bottleneck

**State:** Written evidence is near the current pass range. Speaking interaction is weak/under-evidenced; the learner has microphone access and normal energy.

| Time | Activity | Why selected |
|---:|---|---|
| 3 min | Retrieve two response/alternative phrases without a model | Activates the exact interaction behavior without answer-bearing support |
| 17 min | Fresh planning exchange: attempt → feedback → narrow interaction repair → new exchange | Dominant oral pass-risk, direct modality evidence, deadline relevance |
| 3 min | One timed follow-up turn | Adds target-condition execution evidence without starting a second skill |
| 2 min | Summary and next oral check | States whether the blocker was language, interaction, or uncertainty |

**Why this today:** Speaking is the weaker pass gate and still lacks enough recent direct evidence. With 18 days remaining, one coherent oral block is worth more than a mixed session or another comfortable Reading task.

### Sample C — Failed mock revealed timed Writing execution risk

**State:** The message was communicatively adequate but unfinished; one required point was omitted. Grammar evidence is otherwise stable, so the cause is provisionally timing/checking rather than general language weakness.

| Time | Activity | Why selected |
|---:|---|---|
| 4 min | Clarifying planning task: select and order required content points | Resolves whether instruction understanding or checking behavior caused the omission |
| 15 min | Fresh Writing response with a practice-time target | Tests planning and completion on new content; avoids reteaching stable grammar |
| 4 min | Self-check against required points and submit | Directly verifies the exam-strategy repair |
| 2 min | Summary and retest plan | Keeps the fine weakness provisional until independent recurrence/transfer supports it |

**Why this today:** Yesterday’s mock made timed completion the highest-value uncertainty. The session tests the suspected cause on fresh content before labeling a broad Writing weakness.

### Sample D — Balanced coverage day with no dominant blocker

**State:** No high/pass-critical weakness is active. A Listening number check is due, Language Elements evidence is aging, and Reading is strong and fresh.

| Time | Activity | Why selected |
|---:|---|---|
| 4 min | Fresh audio number contrast | Due retention in the correct modality |
| 11 min | Language Elements contextual task at current difficulty | Replaces aging evidence and checks a meaningful TELC pattern |
| 8 min | Short Writing use of one connector from the task | Collects direct productive verification without assuming cross-modal transfer |
| 2 min | Summary | Explains that the session was mixed because no single risk dominated |

**Why this today:** There is no urgent blocker, so the plan protects a due Listening repair, refreshes aging Language Elements evidence, and uses Writing to verify—not assume—productive transfer.

### Sample E — Learner has 25 minutes but requests a low-energy/no-audio day

**State:** Listening is nominally the highest priority, but audio is not feasible. A Writing content-point retention check is also due; Reading inference is an Active but lower priority weakness.

| Time | Activity | Why selected |
|---:|---|---|
| 5 min | Writing content-point plan/check | Due, quiet, low setup, and produces valid retention evidence |
| 15 min | Focused Reading inference attempt and narrow repair | Best available high-value reachable block without audio |
| 3 min | Fresh Reading retry | Completes the repair boundary |
| 2 min | Summary and rescheduled Listening note | Makes the trade-off explicit without treating the override as failure |

**Why this today:** Audio is unavailable, so Listening remains pending rather than being replaced by fake evidence. The plan uses the best valid alternative and returns Listening in the next suitable session.

## 6. Edge Cases / Failure or Uncertainty Handling

| Situation | Coaching-engine behavior | What it must not do |
|---|---|---|
| Initial diagnostic is only provisional | Favor one reachable observed need and one small decision-relevant evidence gap | Pretend sparse evidence supports a precise optimal plan |
| No usable evidence in a pass-critical skill | Schedule the smallest feasible direct sample | Infer it from another modality or score it as zero |
| Highest-risk target is far above current ability | Choose a prerequisite, scaffolded attempt, or diagnostic contrast | Fill the session with demoralizing B1 failure |
| Too many reviews are due after inactivity | Select the few highest-impact/time-sensitive checks and reschedule the rest | Create a backlog or shame message |
| One result contradicts stable history | Lower confidence and choose a clarifier/fresh task | Rebuild the week around one anomaly without diagnosis |
| No reviewed fresh content exists for the exact node | Use a broader reviewed equivalent or postpone the fine check | Generate/display low-quality content merely to satisfy the schedule |
| Productive evaluation is pending/unavailable | Continue with valid objective/due work and label productive evidence pending | Fabricate feedback or repeatedly pay for reevaluation |
| Microphone/audio unavailable | Re-plan to another useful activity and keep the oral/listening gap explicit | Treat typed work as direct oral/audio evidence |
| Learner repeatedly chooses a strong skill | Respect the choice, show the unresolved pass-gate trade-off, and offer a smaller alternative later | Force the task or declare readiness despite missing evidence |
| Learner is fatigued during a task | Preserve context, reduce evidence confidence when justified, and offer a later clarifier | Diagnose a broad regression solely from late-session decline |
| Estimated plan runs long | Remove/postpone the lowest-value optional block at a meaningful boundary | Ask the learner to rush or silently exceed the promised time |
| Task finishes early | Offer an optional high-value due/coverage item or end with the earned result | Add filler merely to use every minute |
| Timed task is paused | Keep it as useful practice/partial evidence with the true timing context | Call it continuous exam-timed evidence |
| Fixed date is unrealistically close | Prioritize recoverable points, execution, and honest risk communication | Inflate readiness or promise complete repair |
| Low-confidence Corpus relevance/tag | Broaden the task/cause and lower fine-grained priority | Treat uncertain metadata as learner truth |
| Learner changes/removes the date | Recalculate urgency while preserving all evidence/history | Reset progress or keep artificial deadline pressure |

### Failure to assemble a valid plan

If no valid recommended activity fits the available time, environment, and content quality, Bestehen says so plainly and offers the closest responsible choices: change the duration, enable the required modality, use a broader reviewed task, or pause. The product must prefer a transparent limitation over a low-quality or falsely scored activity.

### Recommendation uncertainty

When two paths are genuinely close, the coach may say: “Both are useful today; I chose Listening because it has older evidence. You can switch to Writing without losing the plan.” Uncertainty in prioritization does not require a premium model or a false single best answer.

## 7. Relationship to Other Bestehen Stages

- **Stage 03 — Initial Diagnostic:** supplies the provisional evidence, session preference, gaps, and first-plan inputs; Stage 06 generalizes the first deterministic recommendation.
- **Stage 04 — Learner Model:** supplies capability, confidence, freshness, conditions, direct-evidence lanes, rollups, and written/oral bottlenecks.
- **Stage 05 — Mistake Memory:** supplies candidate/known status, cause confidence, priority, reachability, repair state, recurrence, and due checks.
- **Stage 07 — Core Learning Loop:** defines the exact internal shape and learner experience of the dominant attempt/repair/retry block.
- **Stage 08 — A1→B1 Progression:** defines the detailed support and difficulty step chosen when the highest-priority target is not yet reachable.
- **Stages 09–13 — Skill Coaching:** define candidate activity formats, TELC task mappings, valid evidence, evaluation, cognitive load, and repair behavior by skill.
- **Stage 14 — Review:** integrates and calibrates all due items, spacing intervals, natural opportunities, and backlog behavior. It must preserve Stage 06’s time and pass-risk balance.
- **Stage 15 — TELC Readiness:** supplies calibrated section weights, pass gates, bottleneck rules, and evidence thresholds used by Tier 1 and exam-impact comparison.
- **Stage 16 — Mock Exams:** supplies exact mock commitments, cadence, completeness, scoring, and post-mock evidence. It must preserve the preparation/recovery effects here.
- **Stage 17 — Ready to Book:** supplies exact eligibility and final 21-day/7-day programs; Stage 06 schedules those commitments without changing their meaning.
- **Stage 18 — Coach Personality:** refines explanation and override language while preserving the calm evidence/reason/outcome structure.
- **Stage 19 — Information Architecture:** makes Today’s Plan dominant, exposes duration and reasons, and supports override/resume without becoming a dense scheduler.
- **Stage 20 — Progress/Motivation:** may recognize completed priorities and repaired weaknesses but cannot turn session completion into the primary goal.
- **Stage 21 — Content Strategy:** provides reviewed, fresh, anti-repetition activities tagged with duration, difficulty, relevance, evidence goal, and quality.
- **Stage 22 — Corpus → App Contract:** supplies versioned relevance, frequency, task/skill relationships, difficulty, and content-pattern intelligence.
- **Stage 23 — Notifications:** may remind learners of a high-value due session but must not turn internal due items into a noisy backlog.
- **Stage 24 — Account/Data:** preserves partial drafts, session/evidence history, preferences, and cross-device resumption according to the final privacy contract.
- **Stage 25 — Accessibility/Device:** defines which timing, modality, and environment accommodations preserve valid evidence.
- **Stage 26 — Analytics:** calibrates whether priorities produce transfer, coverage, readiness accuracy, sustainable completion, and acceptable cost.
- **Stage 27 — Cost Boundaries:** sets portfolio-wide limits; this stage requires routine recommendation computation to remain negligible in cost.

### Cross-stage guardrails

Later stages may tune weights, windows, and duration presets, but they must preserve:

- a 25-minute normal daily recommendation unless user evidence justifies revisiting the default;
- one dominant priority rather than random activity accumulation;
- separate written/oral pass-risk protection;
- weakness, review, freshness, and coverage as distinct needs;
- reachability and fatigue without lowering the target or fabricating evidence;
- date/mock urgency that never raises mastery/readiness;
- learner override without punishment or loss of personalization;
- structured, evidence-backed “Why this today?” explanations;
- meaningful-boundary saving and honest partial/timed evidence;
- deterministic, low-cost routine scheduling.

## 8. Cost Notes

The Daily Coaching Engine should have **negligible marginal AI cost**. Routine session assembly does not justify a language-model call.

### Preferred low-cost default

- compute learner state, freshness, due checks, priority tiers, candidate filtering, and tie-breaking deterministically;
- use Corpus relevance/difficulty/relationships and content metadata that are precomputed, versioned, and cached;
- assemble “Why this today?” from reviewed templates and structured reasons;
- maintain a reviewed pool of activity patterns with duration, cognitive load, modality, evidence goal, and freshness metadata;
- reuse/pre-generate content variants and audio in batches rather than generate every daily plan live;
- use the same Writing/Speaking evaluation already required by the activity; never make a second call merely to rank tomorrow’s plan;
- keep unresolved diagnoses broad and schedule a clarifying task instead of purchasing speculative precision;
- re-plan locally/deterministically when the learner changes time, energy, or equipment.

### When more expensive computation could be justified

A higher-quality recommendation or plan-explanation model may be considered only if later evaluation shows that the deterministic engine repeatedly mishandles complex combinations of productive-skill evidence, booked-date trade-offs, or ambiguous post-mock causes **and** that better planning materially improves transfer or readiness calibration. Even then:

1. deterministic hard constraints and tier order remain authoritative;
2. the model ranks or explains a bounded candidate set rather than inventing activities;
3. calls are reserved for exceptional/high-impact planning moments, not every session;
4. results are stored and reused until new evidence changes the decision;
5. the fallback is always the deterministic plan with transparent uncertainty.

Cheaper task/content fallbacks include a broader reviewed task, cached repair pattern, pre-generated equivalent form, or postponed fine-grained check. Cost is never a reason to show invalid content, skip a pass-critical modality indefinitely, or claim evidence that was not collected.

## 9. Decisions Made

1. Set **25 minutes** as the default daily session, with 10-minute Quick, 45-minute Extended, and 5–60-minute custom options.
2. Defined the normal Standard plan as one dominant priority plus limited due/secondary work, normally no more than two major skill contexts.
3. Defined the objective as risk-adjusted expected readiness gain per useful learner minute.
4. Chose a lexicographic priority hierarchy followed by a simple ordinal within-tier comparison rather than an opaque precision score.
5. Defined explicit balancing rules for TELC weighting, written/oral bottlenecks, weaknesses, spaced review, evidence freshness, fatigue, exam urgency, and section coverage.
6. Defined focused versus mixed-session selection and mixing guardrails.
7. Defined date-aware behavior for no date, tentative date, booked more than 21 days, booked 8–21 days, and the final 7 days without letting dates alter readiness.
8. Defined how upcoming and completed mocks reorder sessions, including at most two immediate priorities, clarification, repair, transfer, and retest behavior.
9. Defined learner overrides for time, energy, modality, postponement, replacement, focus, and stopping without punishment or loss of personalization.
10. Defined the evidence/reason/exam-value/timing/outcome contract for **“Why this today?”**
11. Defined meaningful-boundary saving, same-day resume, later re-ranking, interrupted repair chains, and honest treatment of paused timed work.
12. Defined tie-breaking rules, candidate requirements, pseudologic, plan statuses, and failure handling.
13. Defined a deterministic, cached, template-driven low-cost default with no premium model needed for routine scheduling.

## 10. Open Questions / Deferred Decisions

### Open owner questions

**None.** Stage 06 can be responsibly shaped from the existing product context.

### Deferred product decisions

- exact interaction and activity-boundary UX inside Attempt → Diagnose → Repair → Retry — Stage 07;
- calibrated support/difficulty transition thresholds — Stage 08;
- final skill-specific task inventory, cognitive-load estimates, and evaluation rules — Stages 09–13;
- final review intervals, due-window flexibility, and scheduling calibration — Stage 14;
- exact TELC section/task/rubric weights, readiness bands, pass gates, and point-impact estimates — Stage 15;
- exact mini/section/full mock duration, cadence, pause/resume, and retest rules — Stage 16;
- precise 21-day/7-day schedules, tapering, and ready-to-book constraints — Stage 17;
- learner-facing UI, notification cadence, and saved-plan placement — Stages 19 and 23;
- final data retention/sync and accessibility policy — Stages 24–25;
- numerical coefficient calibration, A/B evaluation, and model-upgrade thresholds — Stage 26;
- algorithms, services, storage, and model/provider selection — post-shaping architecture work.

The duration presets, date bands, activity-count guardrails, and ranking dimensions are implementable product defaults. They should be recalibrated from completion quality, repair transfer, section coverage, mock outcomes, and cost—not optimized merely for session starts or time in app.

## 11. Definition of Done Check

- [x] Choose default daily session duration.
- [x] Support configurable session lengths.
- [x] Define the optimization objective for session assembly.
- [x] Balance:
  - [x] exam weighting,
  - [x] weakest areas,
  - [x] spaced review,
  - [x] skill freshness,
  - [x] learner fatigue,
  - [x] exam-date urgency,
  - [x] section coverage.
- [x] Define focused vs mixed-session logic.
- [x] Define how mock exams affect upcoming sessions.
- [x] Define how a fixed exam date changes priorities.
- [x] Allow learner override without destroying personalization.
- [x] Explain “why this today?”
- [x] Define partial-session completion behavior.
- [x] Include decision pseudologic and tie-breaking rules.
- [x] Include representative 25-minute sessions.
- [x] Define a financially sustainable recommendation model and explicit premium-computation fallback.

**Stage 06 is complete when, given a learner state and 25 minutes, Bestehen can choose a coherent plan, explain the competing priorities it balanced, preserve learner agency, and continue honestly after interruption.**
