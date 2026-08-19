# Bestehen / App — Stage 20: Progress and Motivation

> **Status:** Authoritative Stage 20 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Motivation promise:** Make real movement toward passing visible and emotionally sustainable without creating a second game economy that competes with Readiness.

## 1. Purpose and Scope

This document defines how Bestehen / App communicates progress and supports motivation after the learner has begun training.

Earlier stages already establish the product's central progress concept: **Readiness** is the evidence-backed answer to whether the learner could currently meet both TELC B1 pass gates. Stage 20 does not add another score beside it. Its job is to make the journey motivating when Readiness moves slowly, temporarily falls, cannot yet be calculated, or stays flat while important underlying capability improves.

The stage therefore defines:

- the primary/secondary progress hierarchy;
- whether streaks, XP, achievements, currencies, and similar mechanics belong;
- meaningful exam-oriented milestones;
- weekly progress summaries;
- how regressions, stale evidence, noisy results, and plateaus are communicated;
- what the learner should feel after a strong, weak, inactive, or flat week;
- which progress mechanics belong on the Progress surface shaped in Stage 19;
- low-cost defaults appropriate to a personal project.

This is product shaping, not visual design or implementation architecture. It does not choose chart libraries, animation systems, storage schemas, notification infrastructure, or analytics pipelines. Stage 23 may later decide reminder/notification behavior and Stage 26 may calibrate heuristics from real learner data. Those stages must preserve the hierarchy and guardrails defined here.

### Core decision

**Readiness remains the only primary progress concept. Bestehen launches with no XP, no virtual currency, no classic daily streak, and no collectible achievement system. It uses restrained, evidence-backed Milestones and a secondary weekly consistency signal to make preparation progress visible without rewarding activity for its own sake.**

A learner should leave the Progress experience thinking:

> **I know whether I am closer to passing, what genuinely improved even if the headline score did not move, what currently limits me, and what the coach will do next.**

---

## 2. Inputs / Existing Decisions

Stage 20 preserves the shared Product Overview, shared Identity, and App Stages 01–19.

### 2.1 Readiness is already authoritative

Stage 15 establishes the learner-facing readiness model:

- **Evidence building / Not enough evidence**, **Not ready**, **Borderline**, and **Safe pass range** are the current readiness states;
- the **Readiness Index** is shown only when evidence is sufficient;
- the index is the weaker of the estimated Written and Oral target-performance percentages, not a pass probability;
- Written and Oral remain separate because the current target has independent pass gates;
- predicted component ranges and evidence confidence explain uncertainty;
- assisted, weak, stale, or non-target evidence may support learning without directly setting the target-performance estimate;
- Readiness is reversible as new evidence arrives, old evidence ages, evaluators are corrected, or the target blueprint changes.

Stage 17 separately defines **Ready to Book** as an action gate over Stage 15 Readiness plus recent consistency evidence. It is not a second score and can reopen when evidence changes.

Stage 20 must not create any mechanic that weakens those distinctions.

### 2.2 Capability progress is richer than one readiness number

Stages 04, 05, 08, and 14 already define meaningful underlying progress:

- capability can move through **Unknown → Not yet demonstrated → Emerging → Functional → Reliable → Target-evidenced**;
- a mistake pattern can move through candidate/known/repairing/repaired/resolved states and may reopen later;
- assistance can reduce while performance remains stable;
- a task family can move from Supported Foundation toward Target Conditions;
- evidence can become broader, fresher, more realistic, or more confident;
- a repair may survive delayed fresh transfer even before the overall readiness bottleneck changes.

These are legitimate motivational signals because they represent changed capability or stronger evidence, not mere app activity.

### 2.3 Missed days are not punishment events

Stage 02 explicitly establishes recovery without punishment. A missed day or long absence changes evidence freshness and the next plan; it does not erase learning, destroy progress, or justify shame-based copy.

Stage 14 similarly rejects a punitive review backlog. A learner returning after time away receives reprioritized work, not accumulated debt.

A classic streak mechanic that treats one missed calendar day as a failure would conflict with these decisions.

### 2.4 Mocks and booking already define meaningful high-stakes moments

Stage 16 establishes that:

- one clean passing full mock is one strong correlated occasion;
- two clean passing full mocks on separate days are the milestone at which the learner has **repeated a pass in full simulation**;
- mock labels do not add hidden readiness weight.

Stage 17 establishes that Ready to Book requires stronger current consistency than merely one pass and may be earned without requiring two full mocks when lower-cost component confirmations provide equivalent decision evidence.

Stage 20 uses those states as milestones; it does not alter their scoring or gates.

### 2.5 Coach personality constrains celebration

Stage 18 requires earned encouragement and explicitly rejects praise for opening the app, trivial tapping, tiny noisy score movement, or activity volume. Good encouragement names the capability or evidence that improved. Poor performance is communicated directly without shame or a forced positive spin.

Stage 20 therefore treats celebration as **acknowledgement of evidence**, not entertainment layered over every action.

### 2.6 Progress already has a home

Stage 19 defines **Progress** as one of four primary destinations, responsible for meaningful evidence-backed change and history. It explicitly says Progress must not be replaced by engagement metrics. Coach and Readiness remain the primary daily and current-state surfaces.

Stage 20 fills that Progress surface with the hierarchy below; it does not change the Stage 19 navigation.

### 2.7 No earlier document requires amendment

No Stage 20 decision contradicts the shared Identity or App Stages 01–19. This stage makes their existing anti-gamification and earned-progress principles concrete. No earlier shaping document needs to be changed.

---

## 3. Decisions and Rationale

## 3.1 Use a four-level progress hierarchy

**Decision:** Bestehen presents progress in this order:

| Priority | Progress layer | Learner question | Examples | Product role |
|---|---|---|---|---|
| **1 — Primary** | **Current Readiness** | “How close am I to passing now?” | Readiness state/index when valid; Written and Oral; confidence; Ready-to-Book status | The only headline progress concept |
| **2 — Secondary** | **Capability and evidence movement** | “What actually got better or became more trustworthy?” | Weakness resolved; support removed; target-condition success; confidence improved; skill became reliable | Makes real progress visible before/without headline score movement |
| **3 — Secondary** | **Milestones** | “Which meaningful exam-preparation thresholds have I crossed?” | Diagnostic complete; first full-mock pass; Oral Safe; Ready to Book | Historical, evidence-backed moments worth acknowledging |
| **4 — Tertiary** | **Preparation consistency** | “Did I give the plan enough opportunities this week?” | Prepared on 3 days; completed 2 of 3 high-value commitments | Context only; never a readiness substitute |

Raw minutes, questions answered, activities completed, words encountered, review items cleared, or app openings may exist in detailed history or internal analytics. They are **not motivational progress metrics** because they do not by themselves demonstrate improved exam performance.

### Why this hierarchy

A learner can genuinely improve while the Readiness Index stays flat because:

- the weaker pass component has not yet changed;
- evidence is not yet strong/realistic enough to set the target estimate;
- a repaired capability has not yet survived enough delayed transfer;
- confidence is improving before the point estimate moves;
- one section improved while another remains the bottleneck.

Showing only Readiness would make those weeks feel empty. Showing XP instead would solve the emotional problem by creating a misleading second objective. The secondary capability/evidence layer preserves motivation **without changing what success means**.

---

## 3.2 Do not launch a classic daily streak

**Decision:** Bestehen does **not** launch with a classic daily streak counter, longest streak, streak freeze, streak rescue, or “streak broken” event.

A classic streak is rejected because it:

- makes a calendar boundary more emotionally salient than exam value;
- can push the learner toward easy five-minute activity merely to protect a number;
- conflicts with the existing missed-day recovery model;
- punishes travel, illness, work pressure, or deliberate rest despite unchanged capability;
- creates a strong loss-aversion mechanic unrelated to whether Written or Oral performance improved;
- adds UX rules and notification pressure without strengthening the exam-coach proposition.

### Replacement: weekly preparation consistency

Bestehen may show a low-key **weekly consistency signal** such as:

- `Prepared on 3 days this week`
- `2 of 3 recommended commitments completed`
- `You gave Speaking two fresh evidence opportunities this week`

This signal is deliberately:

- weekly rather than a fragile day-by-day chain;
- descriptive rather than scored;
- reset neutrally at the next week, with no “loss” event;
- subordinate to Readiness and capability change;
- absent when it would add guilt without a useful coaching interpretation.

A **preparation day** counts only when the learner completes at least one valid coaching commitment or measured attempt that the product considered useful. Opening the app, reading a tip, or keeping a screen active does not count. A valid 5–10 minute micro-session can count when it genuinely satisfies a due check, repair, or evidence goal.

The product does not compare this signal with other learners and does not turn it into a competitive rank.

---

## 3.3 Do not use XP, levels, or virtual currency

**Decision:** Bestehen launches with **no XP, coins, gems, hearts/lives, energy, virtual currency, or activity-derived learner level**.

XP is especially unsuitable because it creates a second progress scale whose unit cannot honestly compare:

- one Reading multiple-choice item;
- a 30-minute Writing sample;
- a difficult S3 interaction;
- a delayed retention check;
- a full target-condition mock.

Any weighting chosen would either be arbitrary or become a hidden readiness-like formula. It would also make low-cost/easy objective work easier to farm than high-value productive practice.

The same rule applies to content unlocking based on activity points. Learners should receive harder or more realistic work because direct evidence supports it, not because they crossed an XP threshold.

---

## 3.4 Use Milestones, not a collectible achievement system

**Decision:** Bestehen uses **Milestones** as restrained historical acknowledgements of meaningful exam-preparation thresholds. It does not launch an achievement collection or badge economy.

Milestones are:

- generated from existing evidence/state transitions;
- tied to exam capability, evidence quality, mock performance, or a consequential journey state;
- displayed once when earned and retained in Progress history;
- non-transferable into points, currency, ranks, access, or readiness bonuses;
- not designed around rarity tiers, secret objectives, completion sets, or badge hunting;
- allowed to remain in history even when the current state later regresses.

The current state and the historical milestone remain separate. For example, the Progress history may truthfully say **“Ready to Book first reached 19 August”** even if current evidence later becomes stale and the active booking recommendation reopens.

### Visual/interaction tone

Milestone acknowledgement should be restrained: a clear card, short state change, or subtle motion is enough. Confetti, loot-opening behavior, spinning rewards, mascot celebrations, or repeated full-screen interruptions do not fit the coach identity.

---

## 3.5 Any gamification-like mechanic is constitutionally secondary

**Decision:** The following guardrail applies to every current or future motivational mechanic:

> **If a mechanic can cause the learner, coach, or product to prefer activity that is worse for exam readiness merely because it preserves or increases the mechanic, the mechanic is invalid.**

Therefore motivational mechanics may **never**:

- alter the Stage 15 Readiness Index, component estimates, confidence, or evidence tiers;
- alter Stage 17 Ready-to-Book gates;
- add hidden weight to mocks or repaired weaknesses;
- influence answer correctness, productive evaluation, or mistake diagnosis;
- outrank the Daily Coaching Engine's pass-risk, due-repair, evidence-gap, reachability, or coverage priorities;
- lock high-value content behind activity volume;
- reward choosing an easier activity instead of the coach's higher-value recommendation;
- create lives, penalties, debt, or lost progress after mistakes or missed days;
- turn leaderboard/social comparison into a product objective.

Motivation follows evidence. Evidence never bends to motivation.

---

## 3.6 Weekly progress is a coaching review, not a usage report

**Decision:** The weekly progress summary is an **evidence-led coaching review**. It is not a Sunday activity recap and does not require a rigid calendar-week quota.

A summary is normally offered after a meaningful review window of approximately seven days **when enough new evidence exists to say something useful**. If the learner studies irregularly, it may be triggered by enough meaningful evidence rather than exactly by the calendar.

The summary answers:

1. **Where are you now?** — current Readiness, Written/Oral state, and confidence when available.
2. **What changed?** — one to three meaningful capability/evidence changes.
3. **What is the strongest new evidence?** — e.g. retained repair, first clean target-condition result, stronger mock, or improved evidence confidence.
4. **What still limits you?** — one primary blocker or evidence gap.
5. **Did the evidence become stronger or weaker?** — support/timing/freshness/contradiction context where relevant.
6. **What is next week's coaching focus?** — normally one primary priority and, when useful, one secondary commitment.
7. **How consistent was preparation?** — optional low-key footer, never the headline.

A weekly summary should compare the current state with the most recent **meaningful prior baseline**, not mechanically compare every internal score tick with seven days ago.

---

## 3.7 Communicate regressions by separating performance, evidence, and uncertainty

**Decision:** Bestehen must not use the word “regression” as a catch-all for every downward readiness movement.

There are four materially different cases:

| Case | What changed | Learner-facing interpretation |
|---|---|---|
| **Confirmed current performance decline** | Repeated comparable direct evidence is materially worse | Say the affected capability/component has become a current risk; name the evidence and next repair/retest |
| **Readiness reduced by new contradictory evidence** | One or more stronger recent target-condition results conflict with older success | Say the estimate moved because newer evidence is weaker; collect/repair enough to establish whether the change persists |
| **Confidence fell because evidence aged or became incomplete** | Ability was not shown to decline; current evidence became less decision-grade | Say the estimate is less certain/current, not that the learner “got worse” |
| **One noisy/anomalous result** | A single result breaks an otherwise coherent pattern | Do not declare regression; repair obvious losses and collect a fresh comparable check |

Historical capability and milestones are not erased when the current readiness state falls. The product may say a previously resolved weakness has **reopened** when the Mistake Memory criteria support it, but it never says the learner has “lost everything” or resets a course-like progress bar.

---

## 3.8 Treat plateaus as a coaching signal, not a learner failure

**Decision:** A plateau is a signal that the current intervention may no longer be producing useful movement. It is not a motivational label such as “stuck.”

### Initial launch heuristic

Bestehen may label a **potential plateau** when all of the following are true:

- the same pass-relevant blocker or directly comparable task/capability has received at least **three independent useful opportunities**;
- those opportunities span at least approximately **14 days**, so same-session noise is excluded;
- the evidence conditions are comparable enough to interpret the trend;
- there is no material capability, independence, confidence, or target-condition improvement;
- a technical/evaluator/content issue does not better explain the pattern.

These numbers are an initial product heuristic, not a psychometric constant. Stage 26 may recalibrate them.

### Plateau response

A plateau causes a **strategy change**, not a larger dose of the same drill. The coach should choose one of:

- re-diagnose the root cause;
- test a missing prerequisite;
- change the repair format or context;
- temporarily reduce one causal difficulty dimension;
- test whether assistance dependence or timing is the real blocker;
- use a broader/fresher transfer task;
- collect a clarifying measured sample.

The weekly summary should explicitly recognize hidden progress when Readiness is flat:

> “Readiness is unchanged, but Writing content coverage is now reliable on fresh prompts. Oral interaction remains the bottleneck, so the headline number has not moved yet.”

---

## 3.9 Define the intended emotional outcome of each week

Motivation is not maximized excitement. It is the learner's willingness to continue because the product makes the situation understandable and improvable.

| Week type | What the learner should feel | Product behavior |
|---|---|---|
| **Strong week** | Earned confidence and direction | Name the capability/evidence that improved; relate it to Readiness; keep the next priority visible |
| **Flat but useful week** | Progress is still legible | Explain what improved underneath the headline and why the bottleneck kept Readiness stable |
| **Weak week** | Oriented, not judged | State the real risk plainly, preserve prior history, show exactly how the plan changes |
| **Plateau** | The strategy can change | Treat repeated flat evidence as a coaching problem to diagnose, not a willpower problem |
| **Inactive / missed week** | Easy to resume without debt | Say there is too little new evidence for a progress claim; recheck freshness and restart with one useful commitment |
| **Readiness regression** | Current risk is actionable rather than catastrophic | Explain which evidence changed the estimate and what will confirm/reverse the conclusion |

The desired overall feeling is:

> **“My preparation is being measured fairly. Good evidence is earned, bad evidence is useful, and I always know the next move.”**

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Progress surface model

The Stage 19 Progress destination should use the following information hierarchy:

1. **Current progress headline**
   - Readiness state/index when valid;
   - Written and Oral status;
   - current Ready-to-Book state when material.
2. **Since the last meaningful baseline**
   - one to three capability/evidence changes;
   - no celebration for tiny internal numeric noise.
3. **Milestones**
   - latest meaningful milestone and timeline access.
4. **Trend / history**
   - Readiness changes with explanations;
   - repaired/reopened weakness events;
   - target-condition/realism progression;
   - meaningful mock events.
5. **Weekly coaching reviews**
   - current/previous weekly summaries.
6. **Preparation consistency**
   - optional tertiary signal, visually below evidence-backed progress.
7. **Detailed history**
   - attempts/activity available for inspection without presenting volume as success.

Progress should not open with “minutes studied,” “questions answered,” “XP earned,” or a streak calendar.

---

## 4.2 What qualifies as a meaningful progress event

A progress event should normally satisfy at least one of these conditions:

- changes a current Readiness band, component estimate, confidence, or Ready-to-Book gate materially;
- changes a capability band or weakness lifecycle state based on valid independent evidence;
- proves a capability under a stronger condition: less assistance, stronger timing, target playback, genuine interaction, or target conditions;
- closes a meaningful evidence gap;
- shows a repair survived delayed transfer;
- creates a defined Milestone;
- reveals a confirmed decline/reopened weakness that changes coaching priority.

The product should **suppress or aggregate**:

- tiny readiness/index fluctuations that do not change the learner's interpretation;
- multiple item-level changes from the same correlated attempt;
- repeated same-session Retry events as if they were independent milestones;
- routine review completions that do not change capability/evidence state;
- activity-volume events.

### Initial material-change rule

For learner-facing Readiness history, a numeric movement should be highlighted only when it either:

- changes a learner-facing readiness band/gate/confidence interpretation; or
- crosses a currently configured **material movement threshold** that Stage 26 may calibrate.

Until calibrated, the product should prefer **state-change and cause-based explanations** over celebrating every one-point movement. There is no need to invent a permanent ±N-point rule in Stage 20.

---

## 4.3 Required launch Milestones

The following seven Milestones satisfy the Stage 20 checklist and are the launch baseline.

| Milestone | Trigger | Learner meaning | Example acknowledgement | Important guardrail |
|---|---|---|---|---|
| **Starting picture established** | Stage 03 initial diagnostic is completed across all five offered areas, with each area producing a signal or explicit “not evidenced” state | Bestehen has enough structure to coach intelligently | “Starting picture established. We know where to begin; this is a baseline, not a pass result.” | Completing the diagnostic does not imply B1 readiness |
| **First section reaches target range** | One exam section first reaches Bestehen's section-level target/pass-range interpretation with recent direct unassisted target-mappable evidence and at least Medium confidence | One part of the written/oral picture has become credibly target-level | “Listening has reached the target range on current evidence. That is a section milestone, not a separate official TELC pass.” | Do not invent an official standalone section pass gate where TELC has none |
| **Oral enters Safe pass range** | Stage 15 Oral first enters **Safe pass range** | Current oral evidence is safely above the pass line under the launch readiness model | “Oral is now in the safe pass range. Written still determines whether overall readiness is safe.” | Historical milestone remains even if current Oral later reopens |
| **Written enters Safe pass range** | Stage 15 Written first enters **Safe pass range** | Current written evidence is safely above the pass line under the launch readiness model | “Written is now in the safe pass range. Oral still matters independently.” | Do not average the two components |
| **First full-mock pass** | First clean, current-target full mock clears both current Written and Oral pass gates | The learner has demonstrated a complete simulated pass once | “You cleared both pass gates in one clean full simulation. Strong evidence—one run is not consistency yet.” | No hidden readiness bonus; one mock is one correlated occasion |
| **Repeated full-mock pass** | Two independent clean passing full mocks on separate days, as defined in Stage 16 | A complete simulated pass has repeated | “You have now repeated a full-mock pass. That makes the result more credible than a one-off good day.” | This is a consistency milestone, not a new Ready-to-Book rule |
| **Ready to Book** | Stage 17 Gates A–F are satisfied | Current evidence supports the consequential decision to book | “Ready to book. Written and Oral are both safely in range and recent measured evidence has repeated. This is a preparation estimate, not a guarantee.” | Current recommendation remains reversible |

### “First section in pass range” terminology

The checklist uses “first section in pass range,” but TELC B1 does not give every individual section a standalone official pass/fail gate. Bestehen therefore uses this as a **coaching milestone**, not an official TELC result.

The underlying section-level target range must be derived from the Stage 15 target-performance model and only shown when the section evidence is good enough to support it. Copy must say **section target range** or **section estimate in range**, not “you passed Listening” unless the target actually defines an independent pass gate.

---

## 4.4 Additional capability Milestones allowed at launch

A small number of evidence-backed capability milestones may complement the required seven when they make lower-readiness progress visible:

| Optional Milestone | Example trigger | Why it is useful |
|---|---|---|
| **First clean target-condition evidence** | First valid P4 attempt in a task family/section | Makes the transition from supported learning to real measurement visible |
| **First retained repair** | A known weakness survives its first delayed fresh transfer | Rewards retention, not same-session memorization |
| **Weakness resolved** | Mistake Memory reaches its resolved state after required transfer/retention | Shows that a recurring source of lost points has genuinely changed |
| **Support removed successfully** | Performance stays stable after a material assistance type is removed | Makes independence visible even before readiness moves |

These should remain sparse. If the milestone feed begins to fire every session, the threshold is too low.

The launch does **not** include milestones such as:

- 10 sessions completed;
- 100 questions answered;
- 1,000 words seen;
- seven app opens;
- 60 minutes studied;
- “perfect day” for clearing arbitrary tasks.

Those are usage events, not demonstrated exam progress.

---

## 4.5 Weekly progress-summary contract

### Trigger

A weekly review becomes eligible when either:

- approximately seven days have passed since the last meaningful weekly review **and** enough new valid evidence exists; or
- enough material evidence has accumulated that a coaching review is useful even for an irregular learner.

When there is too little new evidence, the product may still show a lightweight status message but must not invent a trend.

### Required content order

**1. Current readiness**

- overall band/index only when Stage 15 allows it;
- Written / Oral status;
- confidence/evidence warning when material.

**2. What changed this week**

Choose up to three events in this order:

1. Readiness/Ready-to-Book state change;
2. pass-critical component/section change;
3. capability/weakness/realism/evidence-confidence change;
4. mock consistency milestone.

Do not fill empty space with activity statistics.

**3. Strongest evidence**

Examples:

- clean P4 target-condition result;
- retained repair on a fresh delayed task;
- first/repeated full-mock pass;
- productive behavior repeated independently;
- evidence confidence raised through broader clean samples.

**4. Current blocker**

One primary blocker or evidence gap by default, aligned with the Daily Coaching Engine.

**5. Next-week focus**

One dominant coaching objective and, when useful, one secondary obligation. The summary should explain why they have the highest expected exam value.

**6. Optional consistency footer**

For example:

> `Prepared on 3 days · 2 planned commitments completed`

No adjective such as “bad,” “poor,” or “excellent” is attached to the raw count. Meaning comes from whether the resulting evidence moved preparation forward.

### Low-activity week

When little or no valid evidence exists:

> “There is not enough new evidence for a progress claim this week. Your history is unchanged. We’ll start with one short freshness check and rebuild the current picture.”

Do not render a flat chart as if inactivity demonstrated regression.

---

## 4.6 Regression communication model

Every downward event should follow Stage 18's **fact → meaning → next action** structure.

### Confirmed performance decline

Example:

> **Fact:** “Oral moved from Safe to Borderline after two recent target-condition attempts fell below the range.”
>
> **Meaning:** “This is a current oral pass risk. The decline is concentrated in S3 interaction; your earlier Reading/Writing progress is unchanged.”
>
> **Next action:** “Next: one focused S3 repair, then a fresh measured oral retest.”

### Evidence becoming stale

Example:

> “Your Written estimate is less certain this week because the latest clean Writing evidence is aging. We do not have evidence that your Writing got worse; we need one fresh 30-minute response before treating the current estimate as strong.”

### One anomalous result

Example:

> “This mock was below your recent pattern. One result is not enough to call a regression. We’ll repair the two largest losses, then retest the affected component.”

### Reopened weakness

Example:

> “Restriction scanning had been resolved, but the same error returned in two fresh target-condition Reading tasks. That weakness is open again, so it returns to the plan.”

The product never shows lost XP, lost levels, lost badges, or a streak reset alongside these events.

---

## 4.7 Plateau communication model

When the launch plateau heuristic is met, use neutral language such as **“progress is stable here”** or **“this approach is not moving the result yet.”** Avoid “stuck,” “failing to improve,” or motivational pressure.

Example:

> “Listening restrictions are still at the same level after three fresh checks across two weeks. Repeating the same drill is unlikely to help. We’ll re-check whether the blocker is sound recognition or task strategy, then change the repair.”

If the headline Readiness is flat while underlying evidence improves:

> “Readiness stayed at 58/100. That does not mean nothing changed: Writing content coverage is now reliable on fresh prompts. Oral interaction is still the weaker pass component, so the headline number has not moved yet.”

A plateau event should normally create a visible plan-change consequence; otherwise the label adds little value.

---

## 4.8 Good-week and bad-week example messaging

### Strong week

> **Oral entered the safe pass range this week.** Two recent measured interactions held without a phrase bank, and oral evidence confidence is now Medium. Written is still the weaker component, so next week focuses on one clean timed Writing response and Listening maintenance.

Desired feeling: **earned confidence** — “I am closer because specific evidence improved.”

### Flat but productive week

> **Readiness is unchanged at 58/100.** Your Writing content coverage moved from inconsistent to reliable on fresh prompts, but Oral interaction remains the bottleneck. Next week keeps S3 interaction first and uses Writing only for maintenance.

Desired feeling: **progress remains legible** — “The number is flat for a reason, not because my work was pointless.”

### Weak week

> **This week exposed one clear pass risk:** Listening restrictions are failing under target playback. That becomes next week’s first repair. Your previously resolved Reading weakness remains resolved, and no progress has been reset.

Desired feeling: **orientation** — “The evidence changed the plan; I know what to do next.”

### Inactive week

> **There is not enough new evidence for a progress claim this week.** Your history is unchanged, but some current evidence is getting older. We’ll return with one short freshness check instead of a backlog.

Desired feeling: **easy re-entry** — “I can resume without paying a game penalty.”

### Ready-to-Book milestone

> **Ready to book.** Written and Oral are both safely in range, the latest full mock passed both gates, and each component has a recent independent confirmation. This is a preparation estimate, not a guarantee of the real result.

Desired feeling: **measured confidence** — “The recommendation was earned from evidence.”

---

## 5. Edge Cases / Failure or Uncertainty Handling

### 5.1 Readiness cannot yet be calculated

A foundation learner may make meaningful progress for weeks before Stage 15 allows a numeric index. Progress must still show:

- support being reduced;
- capabilities becoming Functional/Reliable;
- weaknesses being repaired;
- target-condition evidence first becoming available;
- confidence/coverage improving;
- meaningful diagnostic/retention milestones.

Do not fill the missing readiness number with XP or a course-completion percentage.

### 5.2 Readiness is flat because the other component is the bottleneck

When Written improves but Oral remains lower, the overall Readiness Index may stay unchanged by design. Progress explicitly explains the bottleneck and shows Written improvement as secondary progress.

This is not a scoring flaw; it is the intended consequence of respecting independent pass gates.

### 5.3 Readiness falls because evidence is older, not because performance fell

Use evidence language:

- “less current”;
- “confidence reduced”;
- “needs a fresh check.”

Do not say “you lost skill” without comparable direct evidence.

### 5.4 One bad mock after several good results

A single clean mock is strong evidence and should affect Readiness according to Stage 15, but Stage 20 copy must not leap straight to “you regressed.” Explain that the new result conflicts with the recent pattern and collect enough fresh evidence to determine whether it persists.

### 5.5 A previously earned milestone no longer describes the current state

Keep the historical event and show the current state separately.

Example:

- history: `Ready to Book first reached 19 Aug`;
- current state: `Readiness under review — oral evidence is no longer current`.

This preserves truth without turning milestones into permanent promises.

### 5.6 Learner repeatedly chooses easy work

Do not withhold valid evidence or shame the choice, but do not reward it with a stronger progress mechanic. Weekly progress should make the consequence clear:

> “You practiced Reading consistently, but Oral remains under-evidenced, so current Readiness cannot improve responsibly. The highest-value next step is a Speaking sample.”

There is no XP system that lets activity volume disguise the gap.

### 5.7 Learner studies intensely in one day

A long single day can produce useful evidence, but it does not automatically equal stable progress. Milestones requiring independent occasions, delayed transfer, or mock consistency keep their existing rules. The weekly summary may recognize the work without treating correlated same-day repetitions as retained mastery.

### 5.8 Technical or evaluator failure

Invalid attempts do not become negative progress. If a Writing/Speaking evaluation is pending or low-confidence, the weekly summary says the result is pending/uncertain rather than filling the gap with a motivational interpretation.

### 5.9 Target blueprint changes

If a TELC blueprint update invalidates some P4 claims, historical milestones remain historical, while current Readiness and Ready-to-Book state are recomputed under the approved new target. Copy must explain that the exam target changed; it must not imply the learner suddenly lost German ability.

---

## 6. Relationship to Other Bestehen Stages

### Stage 02 — Complete Learner Journey

Stage 20 makes the already-defined weekly/monthly progress moments concrete. It preserves the return-after-absence rule: no punishment, no streak loss, no backlog theater.

### Stage 04 — Learner Model

Capability, confidence, freshness, and readiness contribution remain separate. Stage 20 consumes those states for progress messaging; it does not create a second mastery model.

### Stage 05 — Mistake Memory

Repair/resolution/reopening events are meaningful progress history. Immediate retry success remains too weak to earn “resolved” or “mastered” celebration.

### Stage 06 — Daily Coaching Engine

Progress mechanics cannot alter the engine's priority hierarchy. The weekly summary's “next week” focus should normally match the same pass-risk/evidence logic used for daily planning.

### Stage 08 — A1 → B1 Progression

Support reduction and movement toward P4 are legitimate progress even before Readiness is numerically available. This is especially important for an A1/A2 learner.

### Stage 14 — Review and Spaced Repetition

A review item matters when it proves retention or changes a weakness/capability state. “Cards cleared” is not a progress metric.

### Stage 15 — TELC Readiness

Stage 15 remains the only readiness formula and primary progress headline. Stage 20 never adds XP, milestone bonuses, consistency multipliers, or hidden weights.

### Stage 16 — Mock Exams

Stage 20 consumes the first passing full mock and repeated passing full mocks as milestones exactly as Stage 16 defines them. Mock labels do not create additional readiness weight.

### Stage 17 — Ready to Book

Ready to Book is the strongest launch milestone because it is a consequential evidence gate. Its historical milestone may remain while the current recommendation later reopens.

### Stage 18 — Coach Personality and Behavior

All progress messages follow earned encouragement, fact → meaning → next action, and uncertainty-aware language. No generic cheerleading is introduced by Stage 20.

### Stage 19 — Information Architecture and Core Screens

No navigation change is required. Coach remains the default daily surface, Readiness owns the current pass picture, and Progress owns history, weekly reviews, milestones, and secondary capability/evidence change.

### Stage 21 — Content Strategy

Content quantity must not become a motivational goal. A content strategy should optimize fresh, valid evidence and learning transfer rather than supplying endless items for XP/achievement farming.

### Stage 23 — Reminders and Notifications

Later reminder design may surface a due review, exam-date risk, weekly review, or meaningful milestone. It must not reintroduce streak-loss pressure or generic “come back to protect your streak” notifications.

### Stage 26 — Analytics and Success Metrics

Stage 26 should validate whether these mechanics improve preparation without distorting behavior. It should calibrate:

- what readiness movement is material enough to highlight;
- the potential-plateau heuristic;
- whether the weekly consistency signal predicts useful preparation or merely activity;
- whether milestone acknowledgement changes persistence without increasing easy-task farming;
- whether weekly summaries improve completion of high-value next actions.

Engagement alone must not become evidence that the motivation model is successful.

---

## 7. Cost Notes

Stage 20 has **no meaningful new recurring-cost requirement** if implemented as shaped.

### Preferred low-cost default

- Milestones are deterministic state-transition events derived from evidence already produced by earlier stages.
- Weekly summaries select their facts deterministically from Readiness, learner-model, Mistake Memory, mock, and coaching-priority state.
- Learner-facing text can use a small reviewed library of parameterized coach templates.
- Preparation consistency is simple event aggregation and does not require AI.
- Regression/plateau classification uses existing structured evidence and transparent heuristics.
- No XP ledger, virtual economy, badge inventory, social ranking, or reward backend is required by the product.

### AI policy

A premium model call is **not justified** merely to phrase a milestone or weekly summary. The expensive work—where needed—already occurs upstream when Writing/Speaking evidence is evaluated.

A future richer natural-language summary could use a cheap or batched model **after** the relevant evidence and conclusions are deterministically selected. The deterministic template remains the fallback and the model must not choose the readiness interpretation itself.

### What would justify upgrading later

Additional spend is justified only if Stage 26 shows that richer personalized summarization materially improves adherence to high-value coaching recommendations without changing evidence semantics. It is not justified because generated copy feels more conversational.

---

## 8. Decisions Made

1. **Readiness remains the only primary progress concept.**
2. Progress has four levels: current Readiness; capability/evidence movement; Milestones; tertiary preparation consistency.
3. **No classic daily streak** launches. Bestehen uses a low-key weekly consistency signal instead.
4. **No XP, virtual currency, hearts/lives, activity-derived level, leaderboard, or content-lock economy** launches.
5. Bestehen uses **Milestones**, not a collectible achievement/badge system.
6. Any motivational mechanic is invalid if it can outrank or distort exam-readiness coaching.
7. The launch Milestones are: starting picture established; first section reaches target range; Oral Safe; Written Safe; first full-mock pass; repeated full-mock pass; Ready to Book.
8. “First section in pass range” is explicitly a **Bestehen section-level coaching milestone**, not an invented standalone official TELC pass gate.
9. Weekly summaries are evidence-led coaching reviews, not usage reports.
10. Downward changes distinguish confirmed performance decline, contradictory evidence, stale/insufficient evidence, and one-off noise.
11. A potential plateau initially requires at least three comparable independent opportunities spanning about 14 days with no material improvement; it triggers a change in coaching strategy and is subject to Stage 26 recalibration.
12. Historical milestones remain true even if current readiness later reopens.
13. Good weeks should create earned confidence; bad weeks should create orientation and a concrete recovery plan; missed weeks should permit neutral re-entry without debt.
14. All Stage 20 mechanics can operate deterministically with effectively no new recurring AI cost.

---

## 9. Open Questions / Deferred Decisions

### No owner decision is required

Stage 20 has no unresolved product question that requires owner preference. The simplest launch model is sufficiently supported by the existing product thesis and identity.

### Deferred — analytics calibration, not product definition

Stage 26 should calibrate rather than reinvent:

- the numeric threshold, if any, for highlighting readiness movement in history;
- whether the initial three-opportunity / ~14-day potential-plateau heuristic is appropriately sensitive;
- whether the weekly preparation-consistency footer improves useful adherence or should be hidden by default;
- which optional capability milestones are valuable enough to keep sparse.

Until evidence supports a change, the defaults in this document stand.

### Deferred — visual presentation

Exact card design, charts, iconography, motion, and milestone animation are design decisions. The product requirement is restrained acknowledgement and strict hierarchy, not a specific visual component.

### Deferred — reminders

Stage 23 may decide when weekly reviews or milestones produce notifications. It must preserve the no-streak-loss/no-shame boundary.

---

## 10. Definition of Done Check

Stage 20 is product-shaped when all of the following are true:

- [x] Readiness is confirmed as the primary progress concept.
- [x] Streaks are decided: no classic daily streak; weekly preparation consistency is the low-key replacement.
- [x] XP is decided: no XP or virtual economy.
- [x] Achievements are decided: sparse evidence-backed Milestones, not a collectible badge system.
- [x] Any gamification is explicitly subordinate to exam readiness and cannot affect evidence, coaching priority, or booking logic.
- [x] The initial-diagnostic milestone is defined.
- [x] The first-section-in-target-range milestone is defined without inventing an official standalone pass gate.
- [x] The Oral Safe pass-range milestone is defined.
- [x] The Written Safe pass-range milestone is defined.
- [x] The first passing full-mock milestone is defined.
- [x] The repeated passing full-mock milestone is defined.
- [x] The Ready-to-Book milestone is defined.
- [x] Weekly progress-summary content, trigger, low-activity behavior, and hierarchy are defined.
- [x] Regression communication distinguishes actual performance, evidence aging, contradiction, and noise.
- [x] Plateau behavior and initial heuristic are defined.
- [x] The intended learner feeling after strong, flat, weak, inactive, and regression weeks is defined.
- [x] Recurring-cost impact and deterministic low-cost defaults are explicit.

**Done:** Motivation reinforces preparation by making evidence-backed capability and readiness movement visible. It does not replace the exam goal with an arbitrary game loop.
