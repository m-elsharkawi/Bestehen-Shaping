# Bestehen / App — Stage 02: Complete Learner Journey

> **Status:** Authoritative Stage 02 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** TELC B1
>
> **Journey promise:** From the first visit onward, the learner always knows where they are, what is holding them back, and the highest-value next action.

## 1. Purpose and Scope

This document defines the complete learner journey for Bestehen / App, from a first visit at roughly A1 through diagnostic evidence, daily coaching, increasingly realistic exam practice, mock exams, an evidence-earned ready-to-book state, booked-exam preparation, and post-exam return.

It also defines recovery paths after missed days, long absences, weak performance, and failed mocks. It is a product model, not an implementation or screen specification. Later stages will determine exact diagnostic duration, readiness formulas, coaching weights, information architecture, notification rules, and technical mechanisms without needing to invent major journey states.

The journey is organized around **exam readiness**, not lesson or unit completion. The coach owns prioritization; the learner retains control.

## 2. Inputs / Existing Decisions

Stage 02 preserves the decisions in the product overview, identity, and Stage 01 product thesis:

- Bestehen / App is a calm, direct, evidence-based **personal German exam coach**.
- TELC B1 is the only launch target; future exam extensibility may be preserved only where it is cheap and does not weaken TELC B1.
- A learner may start around A1. Assistance adapts, but the destination remains authentic B1 exam performance.
- German is learned through exam-shaped activity, not through a conventional A1 → A2 → B1 chapter sequence.
- The core loop is **Observe → Attempt → Diagnose → Repair → Retry → Remember**.
- Readiness is the primary progress concept, with written and oral pass risk kept visible separately.
- Assisted or untimed success is useful learning evidence but is weaker readiness evidence than recent, unassisted, timed performance.
- Corpus supplies evidence and patterns; the learner experiences coaching, not a Corpus browser.
- Readiness is an estimate, never a guarantee or a claim of official TELC scoring.
- Recurring cost and maintainability matter because Bestehen begins as a personal project.

Stage 01 deliberately deferred exact formulas, thresholds, durations, skill-specific task behavior, and screen structure. This stage defines where those later decisions operate in the journey without pre-empting them.

## 3. Journey Principles

### 3.1 Start with a useful action, not an account wall

The learner should be able to state the goal, supply the minimum planning context, and begin the diagnostic before being asked for non-essential profile data. Exact authentication and sync behavior remain for Stage 24, but the product requirement is that setup friction must not obscure the exam-coach value proposition.

### 3.2 Make every state answer three questions

Every major return point should answer:

1. **Where am I?** Current written/oral readiness status and the quality of supporting evidence.
2. **What is holding me back?** One or two prioritized blockers, not a wall of analytics.
3. **What should I do next?** One recommended action sized to the learner's available time, with a short “why this?” explanation.

### 3.3 Treat the journey as coach-led, not gate-led

The coach recommends a path but does not lock the learner into a rigid sequence. The learner may inspect other skills, shorten a session, or start a mock early. Overrides do not erase personalization; the coach records the resulting evidence and continues to recommend the highest-value next move.

### 3.4 Progress skill by skill

Assistance and realism advance independently by skill. A learner can be in realistic reading practice while still receiving strong support in listening or speaking. Journey labels describe the learner's current coaching phase; they are not a single global language level.

### 3.5 Recover without punishment

A missed day, a long absence, or a poor result changes the plan and the confidence of the evidence. It does not reset progress, destroy a streak as punishment, or trigger shame-based copy.

### 3.6 Readiness must be earned and reversible

“Ready” is a current evidence-backed state, not a permanent badge. New contradictory evidence or stale evidence may move the learner back to “readiness under review” with a clear explanation and recovery plan.

## 4. End-to-End Journey Map

~~~mermaid
flowchart TD
    A["First visit"] --> B["Goal and time setup"]
    B --> C["Progressive diagnostic"]
    C --> D["Starting readiness snapshot"]
    D --> E["Coach-led daily training"]
    E --> F["Increasingly realistic evidence"]
    F --> G["Mini, section, and full mocks"]
    G --> H{"Written and oral evidence stable?"}
    H -- "Not yet" --> I["Targeted repair plan"]
    I --> E
    H -- "Yes" --> J["Ready to book"]
    J --> K["Booked-exam preparation"]
    K --> L["Exam and outcome follow-up"]
    E -. "Missed days or long break" .-> M["Return recheck"]
    M --> E
~~~

The diagram shows the dominant journey, not a rigid funnel. Learners may arrive with an exam already booked, may begin mocks earlier by choice, and may move between training and realistic evidence repeatedly.

## 5. Journey States and Transitions

Journey state is separate from skill-level difficulty and from the readiness score. A learner can occupy one journey state while different skills use different support levels.

| State | Entry condition | Coach's primary job | Learner-facing message | Normal exit |
|---|---|---|---|---|
| 0. Unconfigured visitor | First visit or local data cleared | Explain the exam-coach promise and ask only for essential setup | “Train for TELC B1. Start by showing me where you are.” | Goal context supplied |
| 1. Goal configured | TELC B1 selected implicitly at launch; date/status and study context captured | Turn intent and available time into a diagnostic plan | “I’ll build a starting picture, then choose your first training.” | Diagnostic started |
| 2. Diagnostic in progress | First diagnostic activity begun | Collect broad evidence without overwhelming an A1 learner | “This adapts as we learn what you can already do.” | Minimum baseline completed or learner pauses |
| 3. Baseline established | Enough evidence exists for a useful first plan, even if some areas remain uncertain | Explain starting readiness, uncertainty, blockers, and next step | “This is a starting estimate, not a verdict.” | First recommended session accepted or alternative chosen |
| 4. Foundation coaching | One or more skills require substantial assistance | Build exam-relevant language and strategies through scaffolded tasks | “We’re building the skills behind the exam, with support where you need it.” | Skill-specific evidence supports reduced assistance |
| 5. Guided exam training | Learner handles exam-shaped tasks with limited support | Reduce hints, increase authentic complexity, and test transfer | “You’re solving more of the task independently.” | Sufficient unassisted evidence or a new repair need |
| 6. Exam-condition evidence building | At least some skills can be tested unassisted and/or timed | Collect realistic evidence and expose pass-critical gaps | “Now we need evidence under conditions closer to the exam.” | Mock, targeted repair, or readiness review |
| 7. Readiness under review | Evidence is near the pass range, incomplete, stale, or contradictory | Close evidence gaps and test consistency without overclaiming | “You’re close, but this decision still needs stronger evidence.” | Back to repair/evidence building or forward to ready |
| 8. Ready to book | Separate written and oral criteria, recency, realism, breadth, and consistency requirements are met | Explain why the recommendation is justified and what uncertainty remains | “Your recent evidence supports planning the real exam.” | Learner books, delays while maintaining readiness, or new evidence reopens review |
| 9. Booked-exam preparation | Learner has a confirmed exam date, whether booked before or after readiness | Protect the highest-value points, rehearse execution, and manage deadline risk | “Your date is fixed; this plan protects the areas that matter most.” | Exam day |
| 10. Exam completed / outcome pending | Learner marks the exam completed | Offer decompression, a short reflection, and optional light maintenance | “The exam is done. Record what you remember now or come back when results arrive.” | Result recorded, follow-up dismissed, or learner returns later |
| 11a. Passed | Learner reports a pass | Close the goal, summarize demonstrated growth, and offer optional maintenance or a future goal | “You passed. Here is the evidence trail that got you there.” | Journey complete or optional new goal |
| 11b. Not passed / partial result | Learner reports a non-pass or a failed component | Reframe the result as high-value evidence, rebase the plan, and protect retained strengths | “This result tells us exactly where the next attempt needs to change.” | Focused re-entry diagnostic and coaching |

### Transition rules

- Transitions are driven by evidence quality and goal context, not by completing a fixed number of lessons.
- A weak result may change priorities without changing the overall state. State changes are reserved for meaningful journey shifts.
- Any readiness-related transition must explain which evidence caused it.
- A learner who books early enters booked-exam preparation immediately; the coach must show risk honestly rather than withholding the countdown experience.
- The learner can revisit setup at any time. A changed exam date triggers replanning, not loss of history.
- The passed state closes the TELC B1 goal but does not imply that all German skills are mastered.

## 6. Detailed Product Journey

### 6.1 First visit and value framing

The first experience should make the product category unambiguous:

- Headline: **Train for TELC B1. Know when you're ready.**
- One short explanation: Bestehen diagnoses where exam points are being lost, chooses the next training, and builds an evidence-backed readiness view.
- Primary action: **Build my starting plan**.
- Secondary path: a concise “How it works” explanation of attempt, diagnosis, repair, retry, and readiness.
- The product must not open on a course catalog, placement-level selector, subscription pitch, or full mock.

The first visit should set the expectation that the learner may begin below B1 and will not be judged for that.

### 6.2 Onboarding

Onboarding is a short planning conversation, not a profile questionnaire. It captures:

| Input | Product use | Default / fallback |
|---|---|---|
| Target | TELC B1 is preselected at launch | Do not present unsupported exams |
| Exam status | No date, considering a date, or already booked | “No date yet” |
| Date | Creates urgency and countdown when known | Continue toward ready-to-book without inventing a deadline |
| Weekly availability | Sizes recommendations and sets a realistic pace | Offer a modest editable default |
| Typical session time | Shapes the first and daily plans | Offer short, standard, and long choices |
| Self-view and prior preparation | Helps the diagnostic start at a respectful difficulty | Treat as a hint, never as evidence |
| Explanation language and accessibility needs | Keeps instructions usable | Use the safest supported default and allow later change |

The learner can skip non-essential inputs. Microphone permission is requested only when a speaking action actually needs it, with a clear explanation and fallback.

Three date paths are supported:

1. **No date:** Build readiness first; the product later earns the right to recommend booking.
2. **Considering a date:** Plan against the target while distinguishing aspiration from demonstrated readiness.
3. **Already booked:** Activate deadline-aware coaching immediately and show risk honestly, even if current evidence is weak.

Exact onboarding screen count and account timing belong to Stages 19 and 24.

### 6.3 Initial diagnostic

The diagnostic is progressive, adaptive, and resumable. It is not a full TELC mock and does not assume the learner already understands B1 tasks.

Product behavior:

- Begin with a brief mixed sample that can separate “comfortable,” “needs support,” and “not yet evidenced.”
- Collect initial evidence across Reading, Language Elements, Listening, Writing, and Speaking.
- Adapt linguistic difficulty and assistance by skill.
- Use lightweight productive samples rather than postponing writing and speaking indefinitely.
- Allow pause/resume and provide a useful provisional plan if the learner stops after the minimum viable evidence.
- Never infer oral readiness from reading or grammar performance.
- If a skill cannot be sampled, label it **not enough evidence** and prioritize a future sample.
- Explain that assisted diagnostic success helps choose training but does not prove exam readiness.

Stage 03 will define exact duration, item mix, samples, and learner-model initialization.

### 6.4 First readiness result

The first result is a **starting readiness snapshot**, not a score reveal or pass/fail verdict. It contains:

1. Current journey phase, such as Foundation Coaching or Guided Exam Training.
2. Separate written and oral status.
3. Evidence confidence/coverage for each, including “not enough evidence.”
4. The strongest observed capability.
5. The top one or two blockers.
6. The first recommended session, its duration, and “why this first?”
7. A plain-language note that estimates change as realistic evidence accumulates.

At this point the product may use broad state labels and directional indicators. It must not manufacture a precise pass probability before Stage 15 defines a calibrated representation.

Example:

> **Starting point: Foundation Coaching**
>
> Reading gives us a useful early signal. Speaking is still unknown, and listening vocabulary is your clearest blocker. Your first 22-minute session will repair appointment language and test it again in a fresh listening task.

### 6.5 First recommended session

The first session should prove the coaching loop in one sitting. It should:

- fit the learner's declared available time;
- target one reachable, high-value blocker revealed by the diagnostic;
- begin with a short attempt rather than a generic explanation;
- diagnose the likely reason points were lost;
- provide a narrow repair;
- use a fresh equivalent retry;
- record what changed;
- finish with an updated evidence note and the next likely priority.

The first session should normally create a small but earned success without selecting an artificially easy activity. Product copy explains the choice: “Listening: appointment details blocked two diagnostic answers, and this pattern is common in exam tasks.”

Exact session composition and prioritization weights belong to Stages 06 and 07.

### 6.6 Daily return and training

The default Home/Coach state presents one recommended plan, with:

- total estimated time;
- two or three components at most;
- the dominant readiness reason;
- any due review;
- what evidence the session is expected to add;
- controls to shorten, postpone, or replace an activity.

A typical session may include:

1. a brief due review or warm-up;
2. one primary exam-shaped attempt;
3. diagnosis and targeted repair if needed;
4. a fresh retry;
5. a short secondary evidence task when time permits;
6. an end summary: what improved, what remains, and what comes next.

Daily training is not a mandatory checklist. Partial completion retains valid evidence and the unfinished remainder is re-evaluated against tomorrow's priorities rather than blindly carried over.

### 6.7 Weekly and monthly progress moments

**Weekly coaching review** appears after a meaningful week of activity, or after enough new evidence if the learner studies irregularly. It reports:

- movement in written and oral readiness;
- one capability that became more reliable;
- one persistent blocker;
- assistance/realism changes;
- evidence gaps;
- the coach's focus for the next week.

**Monthly or major progress review** is evidence-triggered as well as calendar-aware. It compares the current state with the previous meaningful baseline, shows whether gains survived over time, and proposes one of three directions:

- continue the current plan;
- shift priority because progress has stalled or risk changed;
- introduce more realistic practice or a mock.

If the learner has little activity, the review says evidence is stale or insufficient; it does not display a demotivating flat progress report or pretend inactivity is regression.

### 6.8 Transition into realistic exam conditions

Realism increases independently for each skill along several dimensions:

- linguistic complexity;
- amount of help;
- allowed replay or reference use;
- task length;
- time pressure;
- task sequencing and fatigue;
- scoring strictness.

The coach recommends a step toward realism when recent performance at the current support level is sufficiently stable and a realistic attempt is more informative than further assisted practice. It can step back temporarily after repeated failure, but should identify the specific support being restored and how it will be removed again.

A learner can choose exam mode early. The result is recorded honestly; an early poor result becomes diagnostic evidence, not a penalty.

Stage 08 defines the assistance ladder and detailed transition criteria.

### 6.9 Mock-exam journey and cadence

Mocks exist to measure and rehearse, not to unlock content.

- **Mini-mocks** provide early, low-burden exposure and evidence across a small cluster of tasks.
- **Section mocks** test a complete written or oral area under realistic constraints.
- **Full mocks** test whole-exam execution, endurance, timing, and pass-critical consistency.

Cadence is event-driven rather than a universal weekly quota:

1. Offer a first mini-mock once the learner understands the basic task flow.
2. Recommend section mocks when the relevant skills can produce useful unassisted evidence.
3. Recommend a first full mock when enough sections have been exposed to realistic conditions, or earlier when a booked date makes a baseline urgent.
4. Use each mock result to change the next plan.
5. Do not repeat a full mock immediately just to chase a pass. Repair material blockers first, then retest with fresh content.
6. Increase realistic rehearsal as the exam approaches while preserving recovery time and avoiding burnout.

Stage 16 will set exact formats, scoring, timing, pause behavior, and detailed cadence.

### 6.10 “You are ready” and ready-to-book

The ready state requires evidence, not motivation. At minimum, later rules must require:

- separate written and oral pass-readiness gates;
- adequate breadth across relevant sections;
- recent evidence;
- enough timed and unassisted performance;
- consistency across more than one meaningful attempt;
- adequate confidence/coverage;
- no unresolved pass-critical blocker hidden by a stronger area.

Stage 15 defines the readiness model and Stage 17 defines exact thresholds. Stage 02 locks the journey consequence:

- If no exam is booked, the primary recommendation becomes **Plan your exam**, supported by a clear evidence explanation.
- If an exam is already booked, wording becomes **On track for your exam** rather than “book now.”
- If readiness is borderline, say what evidence is missing and offer the shortest responsible plan to resolve it.
- If evidence later weakens or becomes stale, move to **Readiness under review** and explain why. Do not silently remove a badge or overreact to one anomalous task.

### 6.11 After readiness is reached

Readiness changes the job of the coach from building capability to protecting and rehearsing it.

The learner may:

- plan/book an exam;
- set or confirm the date;
- maintain readiness while waiting for an appointment;
- rehearse weak edges and exam-day execution;
- enter deadline-specific preparation once booked.

The product should not manufacture endless levels after ready-to-book. Maintenance sessions are lighter, less frequent, and selected to prevent decay or close residual risk.

Detailed 21-day and 7-day preparation modes remain for Stage 17, but they must preserve rest, confidence, logistics, and realistic rehearsal rather than introducing large new curricula.

### 6.12 Exam day and post-exam return

Before the exam, the coach provides a concise exam-day plan: logistics reminder, pacing priorities, and a small number of personalized strategy cues. It should not recommend heavy last-minute learning.

After the learner marks the exam complete:

- pause readiness claims based on the just-completed exam;
- invite an optional quick reflection while memory is fresh;
- allow the learner to wait for the result without engagement pressure;
- offer only optional light maintenance.

When the learner returns with an outcome:

**Passed**

- acknowledge the real outcome as the strongest evidence;
- close the TELC B1 goal;
- summarize the capability and evidence journey;
- offer export/share of a progress summary if later supported;
- offer optional maintenance or a future goal without automatically expanding product scope.

**Not passed or one component failed**

- use neutral, supportive language;
- collect component scores and examiner feedback when available;
- preserve strengths and prior history;
- treat the official outcome as high-value calibration evidence;
- run a short focused re-entry diagnostic only where evidence is missing or contradicted;
- create a new plan around the failed component, remaining time, and retained strengths.

The learner should never be forced to report an outcome.

## 7. Recovery and Return Paths

| Situation | Immediate response | Evidence treatment | Next recommended action |
|---|---|---|---|
| One or a few missed days | Welcome back normally; recalculate today's plan | Preserve mastery and readiness; apply normal recency rules | A right-sized session, not a backlog |
| Long absence | Show a concise “what we knew” summary and explain that some evidence is stale | Preserve history; lower confidence only where recency matters | Short return recheck across pass-critical/stale areas |
| Diagnostic abandoned | Retain completed samples and label missing areas | Use provisional evidence with visible uncertainty | Resume diagnostic or start a limited plan that soon fills gaps |
| Single weak practice result | Diagnose before changing the whole journey | Add evidence with appropriate weight; do not erase stable history | Narrow repair and fresh retry |
| Repeated weak performance | Surface the pattern and reduce scope/assistance as needed | Increase blocker priority; lower confidence where justified | Focused repair block followed by delayed transfer test |
| Weak or failed mini/section mock | Explain failed dimensions and separate skill from execution issues | Give realistic evidence strong weight but retain prior context | Repair the top blockers before another equivalent mock |
| Failed full mock | Move readiness to under review if the result contradicts the current state | Recalculate written/oral risk; treat anomalies cautiously but repeated failure strongly | Recovery plan, section retest, then a fresh full mock |
| Learner booked while not ready | Acknowledge the fixed deadline and state risk plainly | Do not inflate readiness to match the date | Highest expected-value plan plus contingency/exam strategy |
| No microphone / speaking unavailable | Do not infer oral readiness | Mark oral evidence incomplete; typed work cannot substitute for oral performance | Permission retry, supported recording path, or defer with visible limitation |
| Low energy / little time | Preserve agency and avoid an all-or-nothing session | Record only valid completed evidence | Short due review or one high-value micro-session |
| Actual exam not passed | Treat the result as evidence, not failure of the learner | Rebase the relevant readiness model when details are available | Focused re-entry and new target plan |

### Failed-mock recovery sequence

1. **Stabilize:** State the result without catastrophizing: one mock is important evidence, not a final verdict.
2. **Separate causes:** Distinguish knowledge/skill gaps, exam strategy, timing, fatigue, misunderstanding, and evaluation uncertainty.
3. **Prioritize:** Select at most two pass-critical blockers.
4. **Repair:** Run focused coaching at the minimum necessary support level.
5. **Transfer:** Test the same underlying skill on fresh content outside the failed mock.
6. **Retest:** Use a section mock before another full mock unless the fixed date makes a full rehearsal more valuable.
7. **Reassess:** Explain the readiness movement and evidence confidence.

## 8. Representative Moments

| Moment | What the learner sees | What the coach does | Evidence consequence |
|---|---|---|---|
| A1 learner completes a partial diagnostic | “Reading is an early strength. Speaking is not yet measured.” | Builds a first session around a reachable listening blocker | Creates a provisional baseline without fake completeness |
| First successful repair | “You caught the time restriction in a new task.” | Marks immediate transfer, schedules later review | Learning evidence improves; readiness changes little until realism/retention grow |
| Strong reading, weak speaking | Separate written/oral view with speaking as the priority | Keeps skill difficulty independent and recommends a short speaking sample | Prevents averaging away oral risk |
| Learner returns after six weeks | “Your history is safe; we need to refresh three stale areas.” | Runs a short recheck rather than restarting onboarding | Restores confidence selectively |
| First failed full mock | Clear section breakdown and two blockers | Pauses ready-to-book consideration and starts repair | Realistic evidence materially changes priorities |
| First passing full mock | “You cleared this mock; repeat under similar conditions before treating it as stable.” | Protects against overconfidence and schedules targeted follow-up | Moves toward readiness but does not make one pass decisive |
| Ready with no date | Evidence summary plus “Plan your exam” | Switches from capability building to maintenance/booking support | Locks a dated evidence snapshot and monitors staleness |
| Exam already booked but risk remains | “Your date is in 18 days. Oral interaction remains below range.” | Prioritizes expected exam impact and execution | Date increases urgency, never score |
| Learner reports a pass | Completion summary and optional next step | Records the outcome for future calibration | Real outcome supersedes proxy evidence for validation |
| Learner reports a non-pass | Component-focused recovery plan | Preserves strengths and targets the failed area | Official result becomes strong recalibration evidence |

## 9. Edge Cases / Failure or Uncertainty Handling

### Learner is far below B1

Use simple language and heavy scaffolding inside exam-shaped tasks. Describe the state as **building the foundations for the exam**, not as repeated failure. Do not show a precise readiness percentage based mainly on assisted A1 work.

### Learner is already near B1

Let the adaptive diagnostic accelerate toward realistic tasks. Do not force foundation coaching merely because it is the first visit. A near-B1 learner may reach section mocks quickly once minimum evidence is collected.

### Learner has uneven skills

Avoid a single placement label. Show different training/realism needs by skill and keep both written and oral risk visible.

### Evidence is sparse or contradictory

Prefer “not enough evidence” or “readiness under review.” Ask for the smallest sample that would resolve the uncertainty. Never fill missing oral evidence from other skills.

### Learner repeatedly overrides recommendations

Respect the choice and keep recording valid evidence. Explain the trade-off only when the override repeatedly leaves a pass-critical gap: “You can continue with Reading, but Speaking still has too little evidence for a readiness decision.”

### Learner changes or removes the exam date

Recalculate urgency and cadence while retaining all evidence. Removing a date returns the journey to readiness-led planning; it does not reset progress.

### Evaluation or generated feedback is uncertain

Show lower confidence, request another sample, or use a second evaluation path only when the decision is important. Do not let one uncertain AI judgment trigger a large readiness change.

### Learner cannot complete a full mock

Save valid completed evidence if the mock rules permit it, clearly distinguish incomplete from failed, and recommend a smaller section or rescheduled full attempt. Exact pause/resume policy belongs to Stage 16.

## 10. Relationship to Other Bestehen Stages

- **Stage 03 — Initial Diagnostic:** defines the exact adaptive flow, duration, evidence minimums, and productive samples used in States 2–3.
- **Stage 04 — Learner Model:** represents skill-specific difficulty, evidence, assistance, timing, recency, confidence, and journey state.
- **Stage 05 — Mistake Memory:** supplies the persistent blockers used in daily, return, and failed-mock paths.
- **Stage 06 — Daily Coaching Engine:** turns learner state, available time, urgency, evidence gaps, and review needs into the recommended plan.
- **Stage 07 — Core Learning Loop:** specifies the attempt/diagnosis/repair/retry behavior demonstrated in the first and daily sessions.
- **Stage 08 — A1→B1 Progression:** defines the skill-specific assistance and realism transitions.
- **Stages 09–13 — Skill Coaching:** define the detailed experience and evidence for each exam skill.
- **Stage 14 — Review:** defines how retained weaknesses return inside the daily journey.
- **Stage 15 — TELC Readiness:** defines the representation, calculation, confidence, pass constraints, and recalibration behind journey transitions.
- **Stage 16 — Mock Exams:** defines formats, scoring, timing, restrictions, detailed cadence, and post-mock analysis.
- **Stage 17 — Ready to Book:** defines exact eligibility, confidence language, booking support, maintenance, and 21-/7-day modes.
- **Stage 18 — Coach Personality:** refines language for weak results, readiness, recovery, and post-exam moments.
- **Stage 19 — Information Architecture:** maps this journey into screens and navigation while keeping the Coach/Home recommendation dominant.
- **Stage 20 — Progress and Motivation:** defines milestone treatment and progress summaries without turning the journey into gamification.
- **Stage 23 — Notifications:** determines reminder delivery around the journey; this document only requires that reminders be valuable and non-shaming.
- **Stage 24 — Account/Data:** decides sign-in, sync, retention, export, deletion, and post-exam data handling.
- **Stage 25 — Accessibility/Devices:** ensures diagnostic, timed tasks, audio, speaking, and return flows remain usable.
- **Stage 26 — Analytics:** measures funnel progress, transfer, calibration, recovery, and real-exam outcomes without optimizing only for engagement.

### Corpus relationship

Corpus informs task patterns, relevance, difficulty, topic frequency, distractors, and original exercise generation throughout the journey. It does not decide the learner's journey state, expose raw source internals, or substitute corpus confidence for learner evidence. If Corpus has weak coverage for a requested pattern, the App should lower content/evaluation confidence and use reviewed fallback content rather than invent certainty.

## 11. Cost Notes

Most of this journey has no reason to invoke a premium model:

- onboarding, state transitions, date logic, session assembly, return handling, progress summaries, and readiness explanations can be driven by deterministic rules plus stored evidence;
- common copy and repair explanations should use templates or cached, reviewed material;
- content pools and Corpus intelligence should be precomputed and reused;
- weekly/monthly summaries should be assembled from evidence rather than generated afresh by an expensive conversational model.

Higher-quality AI may be justified for initial or mock writing/speaking evaluation, difficult diagnosis, and selected content generation. The preferred product rule is:

1. run deterministic validation and cheap classification first;
2. invoke a suitable low-cost model only when needed;
3. reserve premium evaluation for high-impact or uncertain productive samples;
4. store and reuse the structured result;
5. cap reevaluation attempts unless new learner evidence is submitted;
6. fall back to provisional feedback and lower confidence when premium evaluation is unavailable.

The journey must remain usable when an expensive capability is temporarily unavailable. The honest fallback is incomplete evidence or delayed rich feedback, not a fabricated readiness result.

## 12. Decisions Made

1. Defined the complete first-visit → diagnostic → coaching → realistic practice → mocks → ready-to-book → booked exam → post-exam journey.
2. Chose a short, goal-and-time-focused onboarding with three exam-date paths: no date, considering a date, and already booked.
3. Defined the diagnostic as progressive, adaptive, resumable, and broad enough to include all major skills without becoming a full mock.
4. Defined the first readiness result as a confidence-aware starting snapshot with separate written/oral status, blockers, and a recommended action.
5. Defined the first session as a complete attempt/diagnose/repair/fresh-retry demonstration centered on one reachable high-value blocker.
6. Defined daily training as a coach-selected plan with clear rationale, time flexibility, valid partial completion, and learner override.
7. Defined weekly and monthly progress as evidence-aware coaching reviews rather than activity recaps.
8. Made the transition to realism skill-specific and reversible.
9. Defined event-driven progression from mini-mocks to section mocks and full mocks, with exact cadence deferred to Stage 16.
10. Defined evidence requirements and journey behavior for “ready,” while preserving exact thresholds for Stages 15 and 17.
11. Defined maintenance and booked-exam preparation after readiness rather than endless course progression.
12. Defined post-exam paths for result pending, passed, and not passed.
13. Defined non-punitive recovery after missed days, long absences, incomplete diagnostics, repeated weakness, and failed mocks.
14. Confirmed that journey orchestration should be mostly deterministic and that premium AI is reserved for high-impact evaluation or uncertain cases.

## 13. Open Questions / Deferred Decisions

### Open owner questions

**None.** The complete journey can be responsibly defined from the current product context.

### Deferred product decisions

These are deliberately left to their dedicated stages and do not block the journey:

- exact diagnostic duration, item mix, and completion minimum — Stage 03;
- learner/journey state schema and decay mechanics — Stage 04;
- exact daily duration defaults and prioritization weights — Stage 06;
- exact assistance-removal thresholds — Stage 08;
- skill-specific activity and evaluation rules — Stages 09–13;
- readiness formula, representation, confidence calculation, evidence minimums, and bands — Stage 15;
- exact mock timing, format, scoring, pause rules, and cadence — Stage 16;
- exact ready-to-book threshold and 21-/7-day preparation plans — Stage 17;
- screen/navigation structure and onboarding screen count — Stage 19;
- reminder schedules and caps — Stage 23;
- sign-in, sync, retention, and export — Stage 24;
- implementation architecture, providers, storage, and model selection — post-shaping architecture work.

## 14. Definition of Done Check

- [x] Map first visit → “book your exam.”
- [x] Define onboarding.
- [x] Define target/exam-date setup.
- [x] Define initial diagnostic.
- [x] Define first readiness result.
- [x] Define the first recommended session.
- [x] Define daily training.
- [x] Define weekly/monthly progress moments.
- [x] Define transition into realistic exam conditions.
- [x] Define mock-exam cadence.
- [x] Define “you are ready” state.
- [x] Define what happens after readiness is reached.
- [x] Define recovery after a weak mock exam.
- [x] Define return flow after missed days or long absence.
- [x] Define what happens after the actual exam if the learner returns.
- [x] Identify the main learner states and transitions.
- [x] Keep the journey coach-led and readiness-centered rather than lesson/unit-centered.
- [x] Identify recurring-cost implications and preserve a low-cost fallback.

**Stage 02 is complete when the learner's full journey can be storyboarded without inventing a new major product state.**
