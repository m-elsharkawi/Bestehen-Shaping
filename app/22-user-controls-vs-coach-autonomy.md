# Bestehen / App — Stage 22: User Controls vs Coach Autonomy

> **Status:** Authoritative Stage 22 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Control promise:** Bestehen makes the highest-value preparation decision by default, while the learner can deliberately change what, how long, and how realistically they practice without losing ownership of their data or corrupting the meaning of readiness evidence.

## 1. Purpose and Scope

This document defines the boundary between **coach autonomy** and **learner control** in Bestehen / App.

Earlier stages deliberately made Bestehen a coach rather than a catalog. The coach chooses the recommended work, remembers mistakes, protects due review, adapts support, increases realism, and interprets readiness. Those same stages also establish that the learner may shorten, replace, skip, choose a mock early, request assistance, or deliberately practice another useful area without being punished.

Stage 22 turns those principles into one durable control model. It defines:

- what the coach controls automatically;
- what the learner may override and what remains non-overridable because it defines evidence truth rather than preference;
- the two dominant paths: **Coach me** and **Just practice X**;
- learner controls for section, duration, difficulty, mocks, review, and assistance;
- how overrides affect personalization, learner evidence, readiness, review, and future recommendations;
- how Bestehen explains a deviation from its recommendation without nagging or shaming;
- how the product avoids a settings maze that would weaken the exam-coach identity;
- representative user flows and edge cases;
- the product-level Corpus → App contract required by the current live Stage 22 checklist, whose numbering is temporarily out of sync with this stage prompt.

This is product shaping, not architecture. It does not choose settings storage, recommendation algorithms, API transport, UI component implementations, model vendors, or service boundaries.

### Core decision

**Bestehen uses a strong coached default with lightweight in-context overrides, not a global “autonomy slider.”**

The product has three layers of control:

1. **Coach default:** one recommended next action and coherent session assembled from the learner’s evidence and target.
2. **Light adjustment:** change today’s time, swap one block, postpone a due item, request/remove practice assistance, or choose a different useful coach alternative.
3. **Deliberate practice:** enter **Train** and choose a section, task family, weakness, review obligation, or mock even when it is not the coach’s first recommendation.

The learner controls **what they choose to do**. Bestehen controls **what that attempt truthfully means** for the learner model and readiness.

---

## 2. Inputs / Existing Decisions

Stage 22 preserves the shared Product Overview, shared Identity, and App Stages 01–21.

### 2.1 Coach-led default already established

Stages 01, 02, 06, and 19 establish that:

- Bestehen is a **personal German exam coach**, not a generic course or giant exercise catalog;
- the normal entry point answers **“What should I do today?”**;
- the standard daily session is 25 minutes, with Quick 10-minute and Extended 45-minute presets plus bounded custom durations;
- the coach normally presents one dominant priority and no more than two major skill contexts;
- every meaningful recommendation must have a learner-specific exam-readiness reason;
- Train exists as a **secondary** path for deliberate choice rather than as the default home experience.

Stage 22 does not weaken that hierarchy.

### 2.2 Learner override is already valid

Earlier stages already decide that:

- the learner may shorten, replace, skip, or choose another useful activity;
- learner override does not erase personalization and is not treated as failure;
- a learner may choose target/exam mode early;
- a learner may start a mock before the coach recommends it;
- review may be postponed or skipped without shame or punitive backlog;
- repair may be skipped;
- assistance may be requested in training, with the evidence condition recorded;
- a learner may stop or interrupt an activity, though the resulting evidence claim may become narrower or invalid for target-condition purposes.

Stage 22 makes the consequences consistent across the product.

### 2.3 Evidence conditions are not preference settings

Stages 04, 07, 08, 14–17 establish that:

- missing evidence is unknown, not zero;
- assisted and unassisted evidence remain distinct;
- open, practice-timed, and target-condition evidence remain distinct;
- answer-bearing help, extra Listening playback, transcript/model exposure, pauses, or other non-target support can change the evidence claim;
- target-condition validity depends on reproducing the constraints being claimed;
- Readiness and Ready-to-Book are evidence interpretations, not learner-editable statuses;
- technical or content invalidation is not learner failure;
- one self-selected activity counts just as honestly as a coach-selected activity when its content and conditions are otherwise equivalent.

The learner therefore may choose a different path, but cannot relabel assisted work as unassisted or a compromised mock as fully target-condition.

### 2.4 Review and progression guardrails

Stage 14 defines review as due coaching obligations, not a card deck. Stage 08 defines P0 Supported Foundation → P4 Target Conditions by task family rather than a single global difficulty level.

Stage 22 therefore rejects two tempting controls:

- a global “never review this” switch that silently destroys the coach’s evidence obligations; and
- a global CEFR/difficulty slider that overrides all task-family evidence.

The learner gets deliberate local controls instead.

### 2.5 Coach communication guardrails

Stage 18 requires fact → meaning → next action, direct but non-shaming language, and neutral handling of learner overrides. Stage 20 rejects engagement mechanics that punish missed days or pressure the learner into low-value activity.

Stage 22 applies those rules when the learner chooses something other than the recommendation.

### 2.6 Stage numbering reconciliation

The live `Bestehen_App_Product_Shaping_Checklist.md` currently names Stage 22 **“Define Corpus → App Product Contract”**, while the Stage 22 agent prompt that governs this document is **“Define User Controls vs Coach Autonomy.”**

This is a repository continuity mismatch, not a reason to discard either requirement. This document therefore:

1. treats **User Controls vs Coach Autonomy** as the primary Stage 22 product objective required by the agent prompt; and
2. includes a complete product-level **Corpus → App Product Contract** in Section 10 so every checkbox in the live Stage 22 checklist is also resolved.

No earlier shaping decision is reversed by this reconciliation.

---

## 3. Decisions and Rationale

## 3.1 The coach owns the default; the learner owns the choice

**Decision:** Bestehen must always be capable of making a recommendation without asking the learner to configure the recommendation engine.

The learner should normally see:

- one recommended action;
- expected duration;
- the dominant reason;
- what the work should repair, verify, or clarify;
- an obvious Start/Continue action;
- a lightweight adjustment path.

The learner does not need to choose section weights, scheduler coefficients, evidence windows, or a difficulty algorithm before the coach can help.

At the same time, the recommendation is **advisory, not compulsory**. The learner can practice something else, shorten the commitment, postpone a due review, or choose a mock. Bestehen responds by preserving the resulting evidence and recomputing the next recommendation.

### Why this balance

Too little learner control would make the coach feel paternalistic and brittle when the learner has a real constraint: ten minutes instead of twenty-five, no microphone, a desire to rehearse Reading before class, or a deliberate wish to see a full mock early.

Too much configuration would make the learner self-diagnose and self-schedule the product, reducing Bestehen to an exercise library with a recommendation badge.

The correct model is **strong default, easy local override, truthful consequences**.

---

## 3.2 Use two explicit learner paths: “Coach me” and “Just practice X”

**Decision:** Bestehen exposes two conceptually distinct starting intents.

### Path A — Coach me

This is the default path from Coach/Home.

The learner says, in effect:

> **Use what you know about me and choose the best next work.**

The coach chooses the priority, activity mix, specific content, working difficulty, normal support posture, due review placement, and evidence goal within the learner’s available time.

The learner may adjust the plan, but the starting point is a recommendation.

### Path B — Just practice X

This is the secondary deliberate path from Train and contextual shortcuts.

The learner says, in effect:

> **I know what I want to work on right now; give me a valid version of it.**

`X` can be:

- Reading;
- Language Elements;
- Listening;
- Writing;
- Speaking;
- a specific task family;
- a known weakness;
- due Review;
- a mini/section/full mock;
- a coach-approved alternative surfaced from the current plan.

Bestehen still chooses valid, fresh, rights-safe content and records the conditions. It does **not** stop being a coach merely because the learner selected the area.

### Required distinction

**Coach me changes the recommendation source. Just practice X changes the learner’s immediate intent. Neither changes the evidence rules.**

A self-selected clean P4 Listening task can be strong Listening evidence. A coach-selected hint-assisted Reading task remains assisted evidence. Selection source is not a readiness weight.

---

## 3.3 Do not create a “coach control” percentage or personality setting

**Decision:** There is no setting such as:

- Coach autonomy: 0–100%;
- Strict / balanced / relaxed coach;
- Always follow my interests;
- Always choose the easiest task;
- Never make me do Speaking;
- Ignore review for this skill;
- Count practice as exam evidence.

Such settings would force learners to understand and tune the optimization model, create contradictory states, and make “Bestehen knows what I should do next” less credible.

Preference is handled through **small direct controls at the moment it matters**.

---

## 4. Control Matrix

### 4.1 Authoritative control matrix

| Area | Coach controls automatically | Learner can override / choose | Non-overridable truth | Effect of override |
|---|---|---|---|---|
| **Daily priority** | Which need is highest-value now: pass risk, due repair, evidence gap, realism, freshness, or coverage | Choose another useful area or coach alternative | The unresolved blocker/evidence gap remains in the model | New activity is recorded normally; original priority may remain/reappear |
| **Session duration** | Builds the normal plan around the usual/default duration, 25 min by default | Choose Quick 10, Standard 25, Extended 45, or bounded custom time; change only today or usual default | A full/section mock is not silently compressed into a normal session | Plan is rebuilt to the available time; unfinished work is re-prioritized, not marked failed |
| **Section / skill** | Chooses section based on learner need and exam impact | Choose Reading, Language Elements, Listening, Writing, Speaking, Review, Weakness, or Mock from Train | Readiness still requires direct evidence across required written/oral areas | Self-selected valid evidence counts; neglected priorities remain visible |
| **Task family** | Chooses the specific exam/task pattern that best addresses the need | Choose a task family when deliberate practice is desired | The App must still use a valid task mechanism and reviewed content | Evidence applies only to the task family/capabilities actually tested |
| **Difficulty / progression** | Chooses a reachable P0–P4 working profile by task family | In ordinary practice choose **Easier**, **Recommended**, or **Harder / More exam-like** where valid content exists | Learner cannot relabel a task’s actual difficulty or target-condition validity | Result is recorded at the served difficulty; one override result does not become a punitive global level change |
| **Assistance** | Chooses what support is default, on request, repair-only, or absent for the current rung | Request translations, hints, slower audio, replay, phrase support, or choose less help during ordinary practice | Assistance actually used remains attached to evidence; target attempts cannot keep full target-condition status after prohibited help | Assisted success helps learning; clean less-assisted success can strengthen independence evidence |
| **Review** | Schedules due transfer/retention and protects high-value obligations in the daily plan | Start due review, postpone, skip for today, or choose it directly | Skipping is not success/failure and cannot be interpreted as repaired; evidence may age | Obligation is re-prioritized/rescheduled; no punitive backlog |
| **Repair** | Recommends the narrow repair when diagnosis supports it | Do repair now, skip it, or stop after diagnosis | Skipping cannot be recorded as repair completion or mastery | Original attempt remains valid; unresolved issue may return later |
| **Retry / fresh check** | Recommends fresh equivalent transfer after repair when useful | Do now, postpone, or stop if time is over | Exposed/same-item content cannot count as fresh transfer | Transfer remains due if not completed |
| **Mock timing** | Recommends mini/section/full mock when result is likely decision-useful | Start any available mock early from Train | Scope, current blueprint, timing, playback, no-help, evaluation, and validity rules determine the claim | Early mock gives whatever evidence its valid measured scope supports; coach may still recommend repair before another mock |
| **Pause / stop** | Suggests meaningful stop boundaries | Stop any ordinary activity; pause/resume where the mode permits it | A target-condition block cannot be paused beyond its allowed rule and still claim unchanged full validity | Completed valid units may be retained; compromised scope is downgraded or invalidated honestly |
| **Explanation language** | Applies the shaped language progression by learner context | Set preferred explanation language / request more German or more support within usable bounds | German exam content and target-condition task rules remain what they are | Changes explanation/support, not German ability evidence unless it reveals answer-bearing information |
| **Content selection** | Selects fresh, rights-safe, quality-approved content and prevents near-repeat exposure | Learner may choose the area or mock form when options are explicitly offered | Learner cannot force quarantined, rights-uncertain, stale-target, ambiguous, or invalid content into readiness evidence | No negative effect; the App supplies another valid item/form |
| **Readiness interpretation** | Calculates and explains Written/Oral estimates, confidence, pass band, blockers, and Ready-to-Book status | Learner may inspect evidence and choose what to practice next | Learner cannot manually set readiness, pass status, evidence confidence, TELC weights, or mark a weakness resolved | New valid evidence can change the state; preference alone cannot |
| **Exam date / goal** | Uses target/date to alter urgency and plan | Set/change/clear intended or booked exam date | Date does not increase ability or readiness | Priorities/realism/cadence change; evidence history remains |

### 4.2 The key boundary: choice versus interpretation

The simplest rule for later design is:

> **The learner controls intent and participation. Bestehen controls the semantics of the evidence.**

This is the line that preserves both autonomy and defensibility.

---

## 5. Detailed Product Model / Rules

## 5.1 “Coach me” flow rules

When the learner starts from Coach:

1. Bestehen presents the top recommendation and duration.
2. The learner may start directly.
3. **Adjust plan** exposes only controls likely to matter now, normally:
   - available time today;
   - swap the main block for one or two coach-approved alternatives;
   - postpone a due review within a safe window;
   - use an equipment/environment fallback;
   - choose “I want to practice something else” to enter Train.
4. The coach rebuilds the plan without making the learner edit weights.
5. The resulting activity records its actual conditions and evidence as normal.
6. After completion, Coach remains the dominant return path.

### Coach alternatives

The coach may expose **one to three useful alternatives**, not a full catalog disguised as a recommendation menu.

Examples:

- `10 min — Listening retention check`;
- `25 min — Speaking interaction, recommended`;
- `20 min — Writing component retest`.

Each alternative includes a short trade-off when material.

Example:

> **Speaking is still the top blocker. If you need a quieter session, do the 10-minute Listening check instead; it is useful, but it will not close the oral evidence gap.**

---

## 5.2 “Just practice X” flow rules

The Train path must remain curated enough that the learner does not need to understand the entire learner model.

Recommended hierarchy:

1. **Coach alternatives** — useful options already relevant now.
2. **Review** — due/high-value review obligations.
3. **Weaknesses** — current known or high-priority patterns.
4. **Mocks** — mini/section/full.
5. **Practice a skill** — Reading, Language Elements, Listening, Writing, Speaking.
6. Within a skill, optionally choose a task family and practice mode.

### Practice mode choices

For ordinary skill practice, the learner may choose:

- **Recommended** — coach-selected difficulty/support;
- **Easier / More support** — lower load or more assistance;
- **Harder / More exam-like** — higher load, less help, and/or stronger timing where valid;
- **Target conditions** — only when the product can actually reproduce the target conditions and label the resulting evidence honestly.

The UI should not expose raw P0/P1/P2/P3/P4 terminology as the main learner control unless later design testing shows it is helpful. The internal rungs remain the evidence model.

### After deliberate practice

Bestehen must reconnect the activity to coaching rather than leave the learner inside an endless catalog.

A typical summary is:

> **Useful Reading evidence. Your restriction scanning held up on fresh B1 practice. Speaking is still the main readiness blocker, so it remains the recommended next session.**

This is informative, not corrective of the learner’s choice.

---

## 5.3 Session-duration control

### Stable preference versus today’s constraint

The product distinguishes:

- **usual session length** — a stable preference used as a planning default; and
- **time available today** — a one-session override that should not rewrite the stable preference.

Changing today from 25 to 10 minutes should not require entering Settings.

### Reassembly rules

When time is shortened:

1. keep one high-value complete commitment if possible;
2. avoid starting a repair that cannot reach a meaningful save boundary;
3. protect a pass-critical/due item when it can fit;
4. defer lower-value secondary work;
5. save completed valid evidence;
6. re-evaluate the remainder tomorrow rather than carrying a rigid checklist.

When time is increased:

- deepen the dominant priority first;
- then add a genuinely useful second block;
- do not fill time merely to reach the requested duration.

---

## 5.4 Difficulty controls

### Learner-facing decision

Bestehen supports local **Easier / Recommended / Harder or More exam-like** controls in ordinary practice.

It does not expose “set my German to A2” as a master setting.

### Easier

Choosing Easier may change one or more of:

- linguistic load;
- distractor closeness;
- task length;
- information density;
- speech speed;
- production burden;
- default support.

Evidence remains valid for the difficulty actually served. It may demonstrate a reachable prerequisite or assisted capability, but it does not become target-condition evidence.

### Harder / More exam-like

Choosing Harder may increase:

- authentic B1 language;
- task length;
- distractor similarity;
- inference demand;
- timing;
- playback restriction;
- open production;
- reduced support.

The App should normally permit the request when valid content exists, even if the coach would not have chosen it today.

A poor harder result is useful evidence, not a punishment. It may show that the chosen condition is not yet stable, but **one learner-requested stretch attempt must not mechanically demote a whole skill**.

### Target conditions

Target conditions are not a difficulty aesthetic. They require the currently verified target blueprint and relevant constraints.

If those conditions cannot be reproduced, the product may offer “more exam-like practice” but must not call it a clean target-condition attempt.

---

## 5.5 Assistance control

### Ordinary practice

The learner may request support that the current practice mode permits, including:

- word translation;
- sentence explanation;
- grammar hint;
- vocabulary preview;
- slower/careful audio;
- extra replay;
- phrase bank or sentence starter;
- planning/checklist support;
- answer-narrowing help after a meaningful attempt;
- transcript/model material during repair.

Assistance use is never framed as cheating in learning mode. It is simply a different evidence condition.

### Less assistance by learner choice

The learner may also turn off optional support and attempt a cleaner version sooner. If the content and conditions are otherwise valid, that cleaner attempt can create stronger independence evidence.

### Assistance during a measured target attempt

If the learner requests prohibited answer-bearing help during a clean P4/mock block, Bestehen must explain the consequence **before exposing the help**.

Recommended pattern:

> **I can show the hint, but this part will stop counting as clean target-condition evidence. Continue as practice?**

Actions:

- **Show help and continue as practice**;
- **Keep target conditions**;
- **Stop / return later** where mode rules permit.

The app must not repeatedly ask “Are you sure?” after the learner has made the choice.

---

## 5.6 Mock autonomy

### Learner may start mocks early

**Decision:** Full, component, section, and mini mocks are not locked behind readiness gates.

The coach may advise against a full mock when:

- the same mock question has already been answered and a retest would add little;
- recent repair should be checked with a smaller component mock first;
- oral equipment/partner conditions are not valid;
- not enough fresh validated content is available;
- a full mock would consume substantial time without answering a new decision question.

But when a valid mock exists, the learner may normally start it anyway.

### Deviation explanation

Example:

> **I recommend a Writing component retest before another full mock because it is the only current written blocker. A full mock is still available if you want whole-exam rehearsal.**

This protects learner agency while preserving the coach’s recommendation.

### No hidden penalty

A self-initiated mock is not discounted because it was self-initiated. Evidence strength depends on actual validity, freshness, target conditions, and evaluation quality.

---

## 5.7 Review autonomy

### Learner actions

For a due review obligation, the learner may:

- **Do now**;
- **Later today / postpone** when the due window permits it;
- **Skip for today**;
- **Practice the broader skill instead**, when a natural valid opportunity may satisfy the same obligation;
- **Stop** after a meaningful boundary.

### What the coach does

- preserves the due obligation until it is actually satisfied or superseded by valid natural evidence;
- may re-prioritize it later;
- reduces current confidence/freshness naturally if decision-relevant evidence ages;
- never converts avoidance into a learner capability failure;
- never creates an ever-growing debt count designed to induce guilt.

### Repeated avoidance of a pass-critical area

If the learner repeatedly chooses around a pass-critical area, the coach should surface the consequence once, concretely.

Example:

> **You’ve chosen other practice while Speaking remains the current booking blocker. I’ll keep recommending it. If a full Speaking session feels too much, use the 10-minute interaction option.**

Do not infer a psychological cause or lower Speaking ability merely from the avoidance.

---

## 5.8 Override effects on personalization

### What personalization may learn from choice

Learner choice may update **planning preferences**, such as:

- usual session length;
- preference for shorter/longer commitments when explicitly saved;
- explanation language;
- whether microphone/audio is available now;
- preferred time windows later defined in Stage 23;
- repeated desire for a lighter format as a prompt to offer a smaller high-value alternative.

### What personalization must not infer from choice alone

Do not infer:

- “the learner is good at Reading” because they choose Reading often;
- “the learner is bad at Speaking” because they avoid it;
- “the learner hates mocks” because they postponed one;
- “the weakness is repaired” because they skipped review;
- “the learner wants the coach to stop recommending X” merely because they overrode it several times;
- political/psychological/personality attributes or other unrelated profile data.

Performance evidence and explicit preferences remain separate.

### Preference can shape presentation, not exam truth

Repeated learner choices may cause the coach to offer a more acceptable format first—such as a 10-minute Speaking interaction instead of a 25-minute block—but not to erase the pass-critical priority.

---

## 5.9 Override effects on evidence and readiness

### Authoritative rule

**Evidence is weighted by what happened, not by who selected the activity.**

| Override event | Learner-model effect | Readiness effect |
|---|---|---|
| Choose a non-recommended skill and complete a clean valid task | Normal direct evidence for that skill/task | Counts normally if Stage 15 conditions are met |
| Choose Easier | Valid evidence at easier/assisted condition | Usually learning/progression evidence, not target-condition anchor |
| Choose Harder | Valid evidence at served harder condition | Can strengthen or challenge estimates if target-mappable and valid |
| Request hint/translation/replay before submission | Attempt becomes assisted for affected claim | Readiness contribution reduced according to existing evidence rules |
| Choose no optional help | Evidence is unassisted if no answer-bearing help was used | Stronger only to the extent other conditions are also valid |
| Skip recommended work | No new capability evidence | No direct penalty; missing/stale evidence may continue limiting confidence |
| Skip repair | Original attempt remains; repair unproven | No invented improvement |
| Skip fresh retry | Transfer remains untested | No retained-repair claim |
| Postpone review | Due state persists or moves within safe window | No direct score penalty; evidence may age naturally |
| Start mock early | Normal evidence for measured valid scope | No discount for being self-selected |
| Pause/ask for prohibited help in P4/mock | Completed valid subparts may remain valid; affected scope is downgraded/invalidated | Target-condition credit narrows accordingly |
| Stop session early | Completed valid attempts remain evidence | No “incomplete session” readiness penalty beyond missing evidence |

### No compliance metric

Bestehen must not maintain or show a hidden “followed coach recommendation” score that influences readiness.

Recommendation acceptance may be useful product analytics later, but it is not evidence of German ability.

---

## 5.10 Explaining deviations from the recommendation

### Four explanation categories

When the learner chooses something else, the product should normally use one of four compact explanations:

1. **Useful, lower priority**
   - “Reading is useful, but Speaking is still the current pass blocker.”
2. **Different evidence strength**
   - “The hint will help you learn this; the result will count as assisted practice.”
3. **Measured-condition consequence**
   - “Pausing here means this will no longer be a clean full-mock result.”
4. **Opportunity-cost warning**
   - “Another full mock will take about three hours; the current decision can be answered by a 30-minute Writing retest.”

### Explanation rules

- Explain the **consequence**, not the learner’s supposed motive.
- Use one compact warning at the decision point when it materially changes evidence or time value.
- Allow the learner to continue after the consequence is understood.
- Do not repeatedly reopen the warning during the same choice.
- Do not use red/error styling for an ordinary autonomy decision.
- Do not say “wrong choice” or “you ignored your coach.”
- At the end, reconnect the result to the current recommendation if it remains relevant.

### When no explanation is needed

Do not explain every small deviation. Changing today from 25 to 20 minutes, choosing an equally useful coach alternative, or opening a weakness detail should not generate a warning merely because the learner did something other than the primary CTA.

---

## 6. Settings Boundary: Preventing Configuration from Weakening the Coach

## 6.1 Permanent Settings should remain small

Stage 19 already defines Settings as a utility surface rather than a daily destination.

The initial stable preference set should contain only preferences that remain useful across sessions, such as:

- preferred explanation language;
- usual session length;
- audio/microphone setup and supported accessibility preferences;
- display/accessibility preferences later finalized in Stage 25;
- reminder/schedule preferences later finalized in Stage 23;
- account/data controls later finalized in Stage 24.

Exact screen grouping is a design decision, but the product boundary is fixed: **Settings configure the environment; they do not become an editor for the coaching model.**

## 6.2 Keep transient choices out of Settings

These belong in context:

- time available today;
- Easier / Recommended / Harder for this practice;
- ask for a hint;
- extra replay in practice;
- skip/postpone this review;
- practice another skill now;
- start a mock;
- continue an invalidated target attempt as practice.

A learner should not need to preconfigure those decisions globally.

## 6.3 Explicit non-settings

The learner must not receive settings to edit:

- TELC section weights or pass thresholds;
- Readiness Index formula;
- evidence recency windows;
- evaluator confidence;
- learner-model mastery values;
- weakness lifecycle status;
- Corpus source confidence;
- review scheduling coefficients;
- task-quality approvals;
- target blueprint;
- rights/usage classifications;
- content freshness rules;
- per-section time allocation presented as official where TELC does not define one;
- “count assisted work as unassisted.”

These are product/evidence semantics, not preferences.

## 6.4 No advanced-settings escape hatch at launch

Do not hide the same complexity under an “Advanced” section merely because power users might enjoy tuning it. Add a persistent setting only when:

1. it reflects a real enduring learner preference or accessibility need;
2. setting it once is better than choosing it in context;
3. it does not let the learner accidentally falsify evidence semantics;
4. it materially improves preparation enough to justify the extra product surface.

---

## 7. Representative User Flows

## Flow 1 — Default “Coach me” day

**State:** Speaking is the current oral blocker. A Listening retention check is also due. The learner’s usual session is 25 minutes.

1. Coach opens with: **“25 min — Speaking interaction first. Oral evidence is the current booking blocker; then we’ll do a 4-minute Listening check.”**
2. Learner taps Start.
3. Bestehen runs the Speaking block at the recommended current support level.
4. Due Listening review is satisfied by a fresh short audio task.
5. Summary states what changed and the likely next recommendation.

**Control principle:** the learner did not configure weights, order, or review scheduling; the coach handled the decision.

---

## Flow 2 — “I only have 10 minutes”

**State:** Same recommendation as Flow 1.

1. Learner taps **Adjust plan → 10 min today**.
2. Bestehen does not shrink a 20-minute interaction into an invalid fragment.
3. It rebuilds the plan around a compact Speaking interaction or the due Listening check, depending on which can form the better complete commitment.
4. Deferred work is re-prioritized later.

Example copy:

> **10 minutes works. We’ll do a compact Speaking interaction; it still addresses the oral blocker.**

**Evidence effect:** only completed valid attempts count; no penalty exists for not completing the original 25-minute plan.

---

## Flow 3 — “Just practice Reading” while Speaking is recommended

1. Learner enters **Train → Reading**.
2. Bestehen shows Recommended Reading practice plus optional task-family/mode choice.
3. A compact note says: **“Reading is useful, but Speaking remains the current pass blocker.”**
4. Learner continues.
5. Reading evidence is recorded normally.
6. End summary acknowledges the Reading result and returns Speaking as the next recommendation.

**No penalty:** Readiness does not discount the Reading evidence because it was self-selected.

---

## Flow 4 — Learner chooses harder practice

1. Coach recommends Bridge-level Listening with one optional extra replay.
2. Learner chooses **More exam-like**.
3. Bestehen serves normal-speed B1 audio with tighter playback rules, still clearly labelled as practice unless full P4 constraints apply.
4. Learner performs poorly.
5. Result says what the harder attempt showed; it does not globally demote Listening from one stretch result.
6. Coach may recommend a narrower repair or returning to the prior reachable condition next time.

Example:

> **At normal speed, the restrictions were missed twice. That gives us a useful stretch signal; we’ll repair that pattern before using this condition as the default.**

---

## Flow 5 — Learner requests help during a target-condition attempt

1. Learner starts a clean target-condition Listening part.
2. They request an extra replay that the target rule does not permit.
3. Before playing it, Bestehen says: **“I can replay it, but this part will stop counting as clean target-condition evidence.”**
4. Learner chooses **Continue as practice**.
5. The extra replay is provided.
6. The measured evidence scope is downgraded; the original first-play response remains preserved.

**Control principle:** help is available; evidence truth is not negotiable.

---

## Flow 6 — Learner starts a full mock before recommendation

**State:** The coach currently recommends a 30-minute Writing retest before another full mock.

1. Learner enters **Train → Mock Exams → Full Mock**.
2. Bestehen states the trade-off once: **“A Writing retest would answer the current readiness question faster. A full mock is still useful if you want whole-exam rehearsal.”**
3. Learner starts the full mock.
4. If target conditions are valid, the mock evidence is treated exactly like any other clean mock.
5. Post-mock coaching uses the result normally.

**No lock, no hidden evidence penalty, no repeated nagging.**

---

## Flow 7 — Learner postpones review repeatedly

1. A high-value Speaking interaction review becomes due.
2. Learner skips it for today twice across several sessions while doing other work.
3. Bestehen never records those skips as failed Speaking.
4. Because the oral evidence remains decision-relevant and aging, the coach keeps it high in the plan.
5. The coach offers a smaller viable format:
   - `10-minute interaction check`, or
   - full standard Speaking block.
6. It explains once: **“Speaking is still the booking blocker; skipping the check leaves that evidence unresolved.”**

**Personalization effect:** offer a lower-friction form; do not erase the priority.

---

## Flow 8 — Learner stops a full mock midway

1. The learner completes a valid Reading + Sprachbausteine measured block, then stops.
2. Bestehen saves the completed block’s valid evidence.
3. The attempt is no longer a clean **full mock** and contributes no full-exam sequencing/endurance claim.
4. The learner is not told they failed the mock simply because they stopped.
5. Coach decides whether the completed written evidence changes the next plan.

---

## Flow 9 — Learner chooses “Easier” after a difficulty wall

1. A recommended B1 Reading task is too hard today.
2. Learner selects **Easier**.
3. Bestehen serves a lower-language-load task preserving the same reading behavior.
4. Successful performance becomes valid working-level evidence and informs the next reachable rung.
5. The product does not say the learner “lost B1.”

---

## Flow 10 — Learner changes the exam date

1. Learner changes the intended exam date from four months away to six weeks away.
2. Bestehen recalculates urgency and likely realism/mock cadence.
3. Historical capability evidence remains untouched.
4. Current readiness does not rise because the date became closer.
5. If the new date is risky, Coach says so directly and changes the plan.

---

## 8. Edge Cases / Failure or Uncertainty Handling

### 8.1 Learner always chooses a strength

Do not block the behavior. Continue to provide valid practice, but keep the bottleneck visible and make a smaller high-value alternative easy to start.

Do not turn repeated choice into a hidden preference that suppresses pass-critical work.

### 8.2 Learner always asks for maximum help

Allow assistance in learning mode. Record its use honestly and gradually suggest cleaner checks when the learner is succeeding with support.

Readiness may remain limited because target-condition independence is not yet evidenced. Explain this plainly without framing assistance as wrongdoing.

### 8.3 Learner always selects target conditions and repeatedly fails

Keep target mode available when valid, but the coach should recommend a reachable repair/prerequisite between repeated failures.

Do not waste content forms or learner confidence by serving the same unrealistic difficulty merely because the learner keeps selecting it.

### 8.4 Learner requests an invalid target condition

Examples:

- asks for a transcript during one-play Listening while still wanting the attempt counted as target-condition;
- wants unlimited pause during a timed mock;
- wants phrase-bank assistance while retaining clean Speaking readiness credit.

Bestehen allows the help/practice where useful but changes the claim. The evidence semantics cannot be overridden.

### 8.5 Learner wants an unavailable task or exhausted content family

Explain the product constraint briefly and provide the nearest valid alternative.

Do not serve near-duplicate or low-quality content merely to satisfy choice.

### 8.6 Learner chooses a low-priority area because of environment

Examples: no microphone, noisy train, cannot play audio.

This is a valid planning input. Rebuild the session around the best available useful work and defer modality-specific evidence without penalty.

### 8.7 Recommendation evidence is weak or contradictory

If the coach itself is uncertain, expose alternatives rather than pretending the recommendation is singularly correct.

Example:

> **Writing and Speaking are both plausible priorities. Speaking closes the larger evidence gap; Writing has the more recent confirmed weakness. Choose either if your setup favors one today.**

### 8.8 Content/evaluator failure occurs after learner override

Override does not make the learner responsible for a broken task. Apply the same invalidation rules as coach-selected work.

### 8.9 Learner disagrees with a diagnosis

Stage 22 does not create manual mastery editing. The learner may request another fresh check or flag an item/evaluation problem. If the content/evaluation is uncertain, confidence is reduced and the claim is re-tested. A subjective disagreement is not resolved by letting the learner type a new readiness score.

### 8.10 A learner wants no recommendations at all

Train remains usable for deliberate practice, but Bestehen continues to maintain a current recommendation in Coach. Do not add a “disable coaching forever” mode at launch because that would remove the product’s defining value. The learner can simply choose Train whenever desired.

---

## 9. Relationship to Other Bestehen Stages

### Stage 02 — Complete Learner Journey

Stage 22 operationalizes the existing decision that the journey is coach-led rather than gate-led and that the learner can inspect other skills, shorten a session, or start a mock early.

### Stage 04 — Learner Model

Override choice is planning context, not mastery. Evidence continues to be keyed to what was actually attempted and under what conditions.

### Stage 05 — Mistake Memory

Skipping a repair/review does not resolve or worsen a weakness by itself. Only direct evidence changes the weakness claim.

### Stage 06 — Daily Coaching Engine

Stage 06 remains authoritative for how the default plan is assembled. Stage 22 defines the learner-facing override contract and prevents preference from corrupting the priority tiers.

### Stage 07 — Core Learning Loop

The learner can skip/stop certain steps, but the system cannot claim evidence for a step that did not happen.

### Stage 08 — A1 → B1 Progression

Stage 22 exposes simpler learner-facing difficulty controls while preserving the internal P0–P4 evidence model and assistance semantics.

### Stages 09–13 — Skill Coaching

Each skill keeps its task-specific evidence and support rules. Stage 22 only standardizes how the learner deliberately enters or changes those modes.

### Stage 14 — Review

Review obligations remain coach-owned scheduling signals but learner-controlled participation choices.

### Stage 15 — Readiness

Readiness is non-editable evidence interpretation. Self-selected evidence counts according to its actual validity, not recommendation source.

### Stage 16 — Mocks

Mocks remain open to learner initiation. Target-condition validity and scope are not overrideable labels.

### Stage 17 — Ready to Book

Booking advice remains advisory. Learners may book earlier; the coach then optimizes the fixed date without pretending readiness changed.

### Stage 18 — Coach Personality

Deviation copy must remain calm, neutral, evidence-based, and non-shaming.

### Stage 19 — Information Architecture

This stage confirms the four-destination model: Coach is dominant; Train is the deliberate-choice surface; Settings is not a learner-model editor.

### Stage 20 — Progress and Motivation

No compliance score, streak pressure, or punishment should be introduced to coerce recommendation acceptance.

### Stage 21 — Content Strategy

Learner choice never bypasses content approval, freshness, rights, or target-blueprint validation.

### Stages 23–25

Notification, account/data, accessibility, and device choices may add enduring preferences later. They must follow the Settings boundary here and must not convert product semantics into user-adjustable knobs.

### Stage 26 — Analytics

Later analytics may measure recommendation acceptance, override frequency, evidence yield, and outcomes, but those analytics must remain separate from learner ability/readiness.

---

## 10. Corpus → App Product Contract — Stage-Checklist Reconciliation

This section resolves every item in the **current live Stage 22 checklist** while preserving Stage 21’s separation between Corpus intelligence and learner-playable App content.

### 10.1 Product boundary

**Decision:** Corpus provides **versioned exam intelligence and rights-aware reference/asset metadata**. App owns **learner state, daily prioritization, content serving/approval, practice generation/use, evidence interpretation, Readiness, and learner UX**.

Corpus does not receive or need learner performance data to decide what an individual learner should do next. The App does not require raw source material at learner runtime merely to run a session.

### 10.2 What the App requests from Corpus

At product level, the App requests a **versioned intelligence bundle** for a target/use context. The exact API shape is an architecture decision.

A request may specify:

- target exam and approved target-blueprint version;
- section/task family or capability family;
- intended content role: diagnostic, normal practice, repair, retry, review, difficulty calibration, mini-mock, section/component mock, full mock, or readiness anchor;
- progression/difficulty profile needed;
- topic/domain constraints;
- skill/capability nodes of interest;
- desired evidence strength or realism role;
- content-diversity/freshness exclusions when relevant to generation/calibration;
- whether reusable source assets are permitted/desired for the use case;
- minimum confidence/source-breadth expectations appropriate to the claim.

The App should normally request **patterns/intelligence**, not “give me a random raw exam item.”

### 10.3 What Corpus returns

Corpus returns only the information it can support, with confidence and versioning attached. A bundle may include:

- stable task-pattern identifiers and structure;
- target/provider relevance and blueprint linkage;
- topic/domain distributions;
- vocabulary frequency/relevance distributions;
- grammar/pattern frequency/relevance distributions;
- difficulty characteristics and uncertainty;
- distractor/reasoning archetypes;
- skill/capability relationships;
- audio/discourse characteristics where applicable;
- source breadth / independence indicators so mirror-heavy evidence does not look frequent;
- confidence/authenticity summaries;
- stable taxonomy/version references;
- rights/usage status for any exact asset or source fragment that might be reused;
- attribution/license obligations where reuse is allowed;
- provenance sufficient for internal audit/calibration without forcing learner-facing source exposure.

Corpus must be able to say **“insufficient evidence”** rather than manufacture a distribution or difficulty estimate.

### 10.4 How the App uses task patterns

The App uses task-pattern intelligence to:

- define the solving/communication mechanism an exercise must preserve;
- map lower-difficulty variants to the same target behavior;
- build content briefs;
- choose relevant retry/review task families;
- validate mock scope and target relevance;
- ensure a generic German drill is not mislabelled as exam-shaped evidence.

Task-pattern frequency alone never creates a learner weakness.

### 10.5 How the App uses topic frequency

Topic frequency is a **content-prior and coverage signal**, not a readiness score.

It may influence:

- how often domains appear across fresh practice;
- which domains receive earlier vocabulary exposure;
- content rotation and breadth;
- which topic contexts are useful for transfer.

It must not:

- mark a learner weak before direct evidence;
- crowd out less frequent but required task mechanics;
- turn duplicated unofficial material into false importance.

### 10.6 How the App uses vocabulary frequency

Vocabulary frequency/relevance may influence:

- lexical priorities in P0–P2 support;
- vocabulary-preview selection;
- repair examples;
- generation briefs;
- review priority when the learner has an actual gap;
- synonym/paraphrase coverage.

Frequency is a prior. Learner evidence decides whether the learner needs the item.

### 10.7 How the App uses grammar frequency

Grammar/pattern relevance may influence:

- which Language Elements concepts receive stronger baseline priority;
- which grammar targets appear in exam-shaped content;
- which cross-skill repairs are worth verifying;
- initial ordering before enough learner-specific evidence exists.

Corpus frequency cannot override a demonstrated learner bottleneck or become a conventional grammar syllabus.

### 10.8 How the App uses difficulty

Corpus difficulty signals provide a **prior and calibration reference** across:

- linguistic load;
- reasoning load;
- distractor closeness;
- task length;
- audio characteristics;
- production burden;
- target resemblance.

The App combines that intelligence with actual learner performance to choose a reachable task. Later learner performance may recalibrate difficulty estimates.

Low-confidence difficulty reduces how strongly an item is used for progression or readiness claims.

### 10.9 How the App uses TELC relevance

TELC relevance helps:

- prioritize task patterns and content characteristics for the launch target;
- choose what should be overrepresented as the exam date approaches;
- distinguish useful generic B1 evidence from target-specific evidence;
- define which content is eligible for stronger P4/mock/readiness roles when all other quality conditions pass.

TELC relevance is not usage permission and is not learner mastery.

### 10.10 How the App uses distractor patterns

Distractor intelligence informs **archetypes**, such as:

- lexical overlap with the wrong heading;
- partial-match notice/advertisement;
- corrected information in Listening;
- negation/restriction traps;
- plausible but unsupported inference;
- semantically plausible but syntactically wrong cloze choice.

The App generates or curates **new configurations**, not line-by-line reconstructions of a reference item.

Distractor patterns also help diagnosis: a wrong answer may indicate a partial-match or restriction-handling error rather than a broad language gap.

### 10.11 How the App uses skill relationships

Skill relationships inform:

- which capability nodes a task may provide evidence for;
- likely prerequisites;
- candidate cross-skill checks;
- repair selection;
- transfer opportunities;
- content brief construction.

They do **not** let the App invent mastery in a modality without direct evidence. A relationship can say “verify this in Listening” but cannot transform Reading success into Listening mastery.

### 10.12 Does the App need raw/reference source access?

**Decision:** The learner-facing App does **not** require raw/reference source access as a normal runtime dependency.

Normal App operation should use:

- cached/versioned Corpus intelligence;
- App-approved original content;
- App-approved reusable source assets whose rights metadata explicitly permits the intended use.

Raw/reference access may be useful in **internal content-authoring, QA, target calibration, or audit** workflows. That is not a learner feature and does not imply the raw material may be redistributed.

If the App receives an exact reusable asset, the rights/attribution status must travel with it. The App may never infer “reusable” from authenticity or public accessibility.

### 10.13 Behavior when Corpus lacks enough evidence

Corpus sparsity must not make the learner experience fail closed when a conservative safe fallback exists.

Fallback order:

1. **Use the currently verified official target blueprint** for target mechanics and pass-relevant constraints.
2. **Use curated App seed knowledge/content** already reviewed for the task family.
3. Use broader credible B1/A2 evidence as a lower-confidence prior where transferable.
4. Prefer generic B1 practice to a fabricated fine-grained TELC claim.
5. Lower confidence and omit unsupported frequency/difficulty statements.
6. For P4/mock/readiness use, require the stronger target/content-quality gates already defined. If they cannot be met, do not call the activity target-realistic merely to preserve feature availability.

The coach may say:

> **We have enough verified structure to practice this task, but not enough corpus evidence yet to claim a precise frequency ranking.**

This is an internal/product confidence concept; routine learner copy should surface it only when it materially changes a recommendation or evidence claim.

### 10.14 Version compatibility expectations

**Decision:** Corpus intelligence is **versioned and backward-tolerant at product level**.

Required behavior:

- every bundle exposes its Corpus/taxonomy/target-blueprint version or equivalent provenance;
- App-approved content records the intelligence/blueprint assumptions under which it was created or calibrated when those assumptions affect evidence validity;
- additive/new intelligence may improve future content without invalidating prior learner history automatically;
- a material target-blueprint or taxonomy change triggers re-evaluation of affected content/evidence claims rather than silent reinterpretation;
- the App can continue using the last known compatible, approved intelligence/content when Corpus is temporarily unavailable;
- incompatible or low-confidence changes fail conservatively: retain historical learner evidence where still meaningful, lower target relevance when necessary, and require revalidation before new P4/readiness claims;
- compatibility rules are product semantics; exact version-negotiation/API mechanisms are architecture decisions.

### 10.15 Cost and runtime boundary for the contract

Normal learner attempts should **not** require a live Corpus search or AI analysis call.

Preferred model:

- Corpus computes/curates intelligence asynchronously outside the learner attempt;
- App consumes versioned cached bundles and approved content;
- generation/QA is batched and cached where possible;
- stronger Corpus review or AI processing is triggered by new sources, blueprint change, low-confidence/high-value patterns, or content-authoring needs—not every user click.

This preserves both products’ independence and keeps the personal-project operating model affordable.

---

## 11. Cost Notes

### 11.1 User-control model

This stage has **minimal inherent recurring cost**.

The preferred control model is mostly deterministic product behavior:

- plan reassembly from existing learner state;
- evidence-condition flags;
- validated content selection;
- static/templated deviation explanations;
- normal learner-model updates;
- in-context controls rather than AI-generated settings conversations.

No premium AI call is justified merely because the learner changed duration, selected Reading, postponed review, requested a hint that already exists, or chose a mock.

### 11.2 When AI cost is already justified elsewhere

Overrides may lead into capabilities that already have legitimate cost, for example:

- Writing evaluation;
- Speaking transcription/evaluation;
- genuinely adaptive S2/S3 partner interaction;
- rare content/evaluator ambiguity escalation.

Stage 22 does not add a second AI call to explain the override. Use deterministic/template language whenever the reason is already structured.

### 11.3 Corpus → App contract cost

The low-cost default is precomputed/versioned intelligence plus cached approved content. A live per-attempt Corpus query or model-based recommender is unnecessary and would weaken offline tolerance and independence without improving the core coaching decision enough to justify the spend.

Upgrade later only if measured product quality shows that dynamic Corpus retrieval creates material incremental value that cannot be achieved through periodic bundle refreshes.

---

## 12. Decisions Made

1. **Strong coached default:** Coach/Home continues to present one primary recommendation and remains the dominant daily journey.
2. **Learner choice is advisory-safe:** the learner may choose another useful activity, shorten the plan, skip/postpone work, request assistance, or start mocks early.
3. **Two explicit paths:** **Coach me** for delegated prioritization and **Just practice X** for deliberate learner choice.
4. **No autonomy slider:** learner control is local and contextual rather than a global percentage/strictness setting.
5. **Evidence truth is non-overridable:** assisted, timed, paused, target-condition, freshness, content validity, and readiness semantics are determined by what actually happened.
6. **Self-selected evidence is first-class:** recommendation source does not change evidence weight.
7. **Skipping is not failure:** no compliance score, ability penalty, or shame behavior is attached to overriding the coach.
8. **Difficulty control is local:** Easier / Recommended / Harder or More exam-like; no global CEFR slider.
9. **Assistance is available in learning mode:** using it changes evidence condition, not learner worth; prohibited help during target measurement converts affected scope to practice/non-clean evidence.
10. **Mocks remain learner-startable:** the coach can recommend a better use of time, but does not lock valid mocks behind readiness.
11. **Review remains coach-prioritized but learner-controlled:** due obligations persist until satisfied by valid evidence; no punitive backlog.
12. **Deviation explanations are concise and consequence-based:** useful/lower priority, evidence-strength change, measured-condition change, or opportunity-cost warning.
13. **Settings stay small:** stable environment/preferences only; no learner-model, TELC-weight, readiness-formula, or scheduler editing.
14. **Repeated avoidance changes presentation, not exam priority:** offer smaller viable formats, but keep pass-critical blockers visible.
15. **Corpus → App product contract is resolved:** App requests versioned intelligence; Corpus returns patterns, frequencies, difficulty, relevance, distractor/skill relationships, confidence/provenance, and rights metadata; App does not require raw learner-runtime source access.
16. **Corpus sparsity fails conservatively:** verified official blueprint + curated App seed + lower-confidence broader evidence; no invented precision.
17. **Versioned/cached Corpus intelligence is the low-cost default:** no per-attempt live Corpus or premium-AI dependency.

---

## 13. Open Questions / Deferred Decisions

### No owner-blocking product questions

No owner decision is required to complete Stage 22.

### Deferred to design / architecture

The following do not block product shaping:

- exact wording and placement of `Adjust plan`, `Just practice X`, Easier/Harder, and target-condition controls;
- whether a local override is implemented as buttons, sheets, menus, or another interaction pattern;
- exact persistence/storage of stable preferences versus one-session choices;
- recommendation and override analytics event schema;
- exact Corpus API/transport, cache format, version-negotiation protocol, or service topology;
- exact UI treatment for partially invalidated mock scopes;
- empirical thresholds for when repeated avoidance should trigger the compact consequence explanation.

These implementation/design choices must preserve the behavioral and evidence contract in this document.

---

## 14. Definition of Done Check

- [x] What the coach controls automatically is defined.
- [x] What learners can override is defined.
- [x] Section control is defined.
- [x] Duration control is defined.
- [x] Difficulty control is defined.
- [x] Mock control is defined.
- [x] Review control is defined.
- [x] Assistance control is defined.
- [x] **Coach me** versus **Just practice X** paths are defined.
- [x] Override effects on personalization are defined.
- [x] Override effects on evidence and Readiness are defined.
- [x] Deviation-explanation behavior is defined.
- [x] Settings boundaries prevent over-configuration from weakening the coach identity.
- [x] Representative user flows cover common and difficult override cases.
- [x] Edge cases and uncertainty behavior are defined.
- [x] Cost impact and low-cost defaults are explicit.
- [x] The live checklist’s current Stage 22 Corpus → App product-contract requirements are also fully resolved.
- [x] What the App requests from Corpus is defined.
- [x] What Corpus returns is defined.
- [x] App use of task patterns, topic frequency, vocabulary frequency, grammar frequency, difficulty, TELC relevance, distractor patterns, and skill relationships is defined.
- [x] Raw/reference source-access need is decided.
- [x] Insufficient-Corpus behavior is defined.
- [x] Version-compatibility expectations are defined.
- [x] No major product decision from this stage is left for the design or architecture agent to invent.

**Stage 22 is done when Bestehen can strongly recommend a next move, the learner can deliberately choose another useful move, and both sides can trust that the resulting evidence still means exactly what the product says it means.**
