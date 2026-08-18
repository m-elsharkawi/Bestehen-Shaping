# Bestehen / App — Stage 03: Initial Diagnostic

> **Status:** Authoritative Stage 03 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** TELC B1
>
> **Diagnostic promise:** Establish a useful, honest starting plan across all five exam areas without making an A1 learner sit a long B1 placement test.

## 1. Purpose and Scope

This document defines the initial diagnostic that moves a new learner from minimal onboarding context to a personalized first daily recommendation. It sets the duration, adaptive content mix, task blueprint, initial evidence and confidence rules, learner-facing result, learner-model initialization contract, early-exit behavior, and low-cost operating default.

The diagnostic is a **routing and personalization experience**, not a mock exam, official CEFR placement test, or pass prediction. It must answer enough of “Where should the coach start?” to make Day 1 useful while preserving “not enough evidence” wherever the sample cannot support a stronger conclusion.

This is product shaping rather than implementation design. Later stages may choose storage, models, providers, interfaces, exact item banks, and calibrated formulas. They must preserve the behavior and honesty requirements defined here.

## 2. Inputs / Existing Decisions

This stage preserves the project overview, identity, Stage 01 product thesis, and Stage 02 learner journey:

- Bestehen / App is a calm, direct, evidence-based personal German exam coach.
- A learner may start around A1, but learning remains exam-shaped and aimed at authentic TELC B1 performance.
- The launch target is TELC B1 only.
- Reading, Language Elements, Listening, Writing, and Speaking all need an initial signal; one skill must not be inferred from another.
- Assistance adapts by skill. Assisted performance is useful for training decisions but is weaker readiness evidence.
- Written and oral pass risk must remain visible separately.
- The first result is a starting readiness snapshot, not a score reveal or a promise.
- The first recommended session should demonstrate Attempt → Diagnose → Repair → Retry → Remember around a reachable, high-value blocker.
- The diagnostic must be progressive, adaptive, resumable, and useful even when some evidence remains missing.
- Recurring cost and maintainability matter because Bestehen begins as a personal project.

There are no contradictions with the earlier App shaping documents. This stage makes Stage 02's progressive diagnostic concrete.

## 3. Decisions and Rationale

### 3.1 Target duration and completion model

**Decision:** The default diagnostic is a **20-minute adaptive core**, with an expected completion range of **18–22 minutes**.

- A learner clearly in the foundation range should finish in approximately **12–16 minutes** because harder probes exit early.
- A learner showing strong A2 or B1-adjacent performance may receive useful extension tasks, but the diagnostic has a **hard 30-minute ceiling**.
- The flow is resumable between task blocks. Completed evidence is retained.
- “Diagnostic complete” means every skill was offered and either produced a usable signal or was explicitly marked not evidenced. It does not mean every skill has high confidence.
- A **minimum useful baseline** exists after usable evidence in at least three of the five areas, including at least one receptive/objective area and one productive area. At that point the App may create a provisional first plan while prioritizing missing evidence.
- Below that minimum, progress is still saved, but the primary next action is to resume the diagnostic rather than present a confident personalized plan.

This duration is long enough to touch every pass-relevant area and short enough to avoid behaving like a traditional placement test. A fixed short test would undersample stronger learners; a fixed full B1 test would be demoralizing and inefficient for the intended A1 starting profile.

### 3.2 Adaptive A1/A2/B1 content mix

**Decision:** Content mix is adaptive by skill rather than a fixed test-wide quota. Self-reported experience chooses a respectful starting point but never counts as evidence.

| Route | Typical served mix within objective diagnostic work | Use |
|---|---:|---|
| Foundation | About 60% A1/early-A2, 40% A2 bridge, 0% additional B1 probes after the learner has clearly hit a wall | Establish an accessible floor and useful starting support |
| Bridge, the default when uncertain | About 20% A1/early-A2, 60% A2/bridge, 20% short B1 probes | Separate foundation needs from emerging B1 capability |
| B1-probe | About 0% A1, 30% A2/bridge confirmation, 70% B1-style probes | Avoid wasting the time of a learner already preparing at B1 |

These percentages are routing targets, not scoring weights or promises that every learner sees a precise quota. Reading, Language Elements, and Listening route independently. Writing and Speaking use the same exam-relevant scenario with different scaffolding and output expectations rather than forcing a percentage of prompts at each CEFR band.

The default entry is A2/bridge difficulty. A learner who identifies as a beginner may start one step lower; a learner already preparing for B1 may start one step higher. The system steps down quickly when the choice was too difficult and steps up only after observable success.

### 3.3 All five skills receive a direct initial signal

**Decision:** Each major area receives its own task block. No area is imputed from another, and typed speaking never substitutes for oral evidence.

| Area | Core diagnostic task | Target time | Initial signal |
|---|---|---:|---|
| Reading | Two short exam-shaped microtasks, normally 4–6 scored decisions across functional texts, matching, scanning, gist, or detail; the second cluster adapts | 3–4 min | Comprehension at served difficulty, scanning/detail behavior, synonym or distractor handling, assistance dependence |
| Language Elements | One adaptive contextual cloze or sentence-choice cluster with normally 6–8 decisions | 3 min | Grammar and vocabulary-in-context signal, especially connectors, prepositions/case, word order, and common functional language where sampled |
| Listening | Two short reusable audio clips with normally 4–5 scored decisions; one gist and one detail-focused cluster | 4 min | Gist/detail comprehension, numbers/dates/times where sampled, speed/replay dependence, distractor or negation sensitivity |
| Writing | One time-boxed functional message with explicit content points and optional skill-appropriate scaffolding | 4–5 min | Task coverage, communicative clarity, organization/register, and sampled vocabulary/grammar control |
| Speaking | A 45–90 second total spoken sample: a brief personal response plus a two-turn planning microexchange with a fixed partner prompt and follow-up | 3–4 min | Task completion, basic fluency, comprehensibility, sampled language control, and a limited interaction response |
| Orientation and result | Short instructions, permissions at point of use, and the starting snapshot | About 2 min | No scored evidence |

The exact TELC task mapping and full skill rubrics remain for Stages 09–13. Stage 03 locks the minimum breadth and the fact that each initial signal must be grounded in an actual response from that skill.

### 3.4 Lightweight writing sample

**Decision:** Writing uses one original, reusable functional scenario such as requesting information, changing an arrangement, responding to an invitation, or explaining a simple problem. The learner sees **two or three explicit content points** and a visible time box.

- Default/bridge expectation: roughly **40–60 words** in up to five minutes.
- Foundation route: sentence starters, a small vocabulary bank, and an acceptable shorter response of roughly **25–40 words**. Every support used is recorded.
- B1-probe route: no sentence starters by default and a target of roughly **60–80 words**, still shorter than a full mock task.
- The learner may submit unfinished work. The product evaluates only what is observable and distinguishes incomplete evidence from demonstrated inability.
- The initial sample measures the dimensions it can see; it does not establish stable writing readiness from one response.

A single short message gives a direct production signal at tolerable onboarding cost. Multiple essays would improve reliability but would turn onboarding into an exam and create unnecessary evaluation expense.

### 3.5 Lightweight speaking sample

**Decision:** Speaking uses a short recorded sequence rather than a free-form AI conversation:

1. a simple personal response of about 20–30 seconds;
2. a fixed, pre-recorded partner prompt asking the learner to propose or choose something and give a reason;
3. a fixed follow-up that introduces a small conflict or constraint and asks for an alternative.

Expected total learner speech is **45–90 seconds**. The flow can offer one replay of the instruction and skill-appropriate phrase support, with those supports recorded.

This produces a limited but genuine signal for speech production and response behavior without paying for a live generative partner. It does **not** adequately establish sustained interaction, turn-taking, pronunciation quality, or full oral pass readiness. Those dimensions remain low-confidence or not evidenced until later speaking practice.

If microphone access is unavailable, the learner may rehearse or type for learning value, but the result must say **Speaking: not enough oral evidence**. A typed response cannot initialize oral performance as if speech had been observed.

### 3.6 Routing, early exit, and extension behavior

**Decision:** Adaptation protects the learner from unnecessary difficulty while preserving enough evidence to choose a next step.

Initial routing heuristics for objective task clusters are:

- **Step up** after at least three scorable decisions with approximately 75% or better unassisted performance and no sign that the task was misunderstood.
- **Stay near the current difficulty** when performance is mixed, approximately 40–74%, or when assistance materially changed the result.
- **Step down or stop harder probing** after approximately one-third or fewer correct, two consecutive no-meaningful-response events, or clear failure to understand the task even after one simpler explanation.
- Thresholds are routing heuristics, not readiness scoring cutoffs. They must later be tuned against observed diagnostic completion, transfer, and learner performance.

When a learner is clearly below real B1 difficulty in an area:

1. stop additional B1 probes for that area;
2. offer one easier or scaffolded confirmation task;
3. record the highest difficulty at which a meaningful response was observed and the assistance required;
4. move on rather than repeat failures;
5. keep the learner-facing language neutral: “We’ll start this skill with more support.”

A global foundation route may be used when all early receptive blocks show the same pattern. Even then, Writing and Speaking are still offered in scaffolded form so productive ability is not silently treated as zero or inferred from objective work.

Strong learners receive no more than one useful extension cluster per receptive area. Extensions exist to find a better starting ceiling, not to prove readiness during onboarding.

### 3.7 Scoring and evidence model

**Decision:** Diagnostic results are stored as evidence observations, not converted directly into a single placement score.

Every observation must preserve, at product level:

- skill and sampled subskill;
- task pattern and served difficulty band;
- response/result and rubric dimensions that were actually observed;
- whether the response was correct, partially successful, incomplete, skipped, or invalid;
- assistance offered and assistance used;
- replay/reference use where relevant;
- time context, while recognizing that most diagnostic work is lightly time-boxed rather than exam-timed;
- evaluation method and evaluation confidence;
- technical-quality flags such as inaudible audio or interrupted playback;
- diagnostic context so later readiness can distinguish onboarding evidence from realistic mock evidence.

#### Objective areas

Reading, Language Elements, and Listening are scored deterministically against reviewed answer keys. Raw percentage is not compared across different difficulty routes as if the tasks were equivalent. The starting state combines:

- accuracy at the served difficulty;
- the highest difficulty with a meaningful unassisted signal;
- support dependence;
- response completeness;
- breadth of sampled task clusters.

Latency may help detect task friction or support future coaching, but it is not a penalty in the initial untimed/lightly time-boxed diagnostic unless the learner fails to respond within a generous boundary.

#### Productive areas

Writing and Speaking use a compact rubric and return dimension-level signals rather than a single authoritative grade.

Writing dimensions sampled:

- required content coverage;
- communicative comprehensibility;
- basic organization and register;
- vocabulary sufficiency for the task;
- grammar control sufficient to preserve meaning.

Speaking dimensions sampled:

- response/task completion;
- basic fluency;
- comprehensibility/intelligibility;
- vocabulary and grammar visible in the sample;
- response to the fixed interaction turn.

Pronunciation must not be reduced to accent similarity. If audio quality or evaluation capability cannot support a responsible intelligibility judgment, that dimension remains uncertain.

A tentative mistake cause from the diagnostic may initialize a candidate signal, but it does not become a durable “known weakness” from one event. Stage 05 will define when repeated evidence promotes a candidate into mistake memory.

### 3.8 Confidence and uncertainty

**Decision:** Confidence is explicit per skill and per sampled dimension. The initial diagnostic can produce **not evidenced, low, or moderate confidence**, but never high confidence.

| Confidence | Initial meaning |
|---|---|
| Not evidenced | No valid response exists, the task was skipped, a technical failure invalidated it, or the dimension was not sampled |
| Low | One usable cluster or productive sample exists, evidence is heavily assisted/incomplete, or evaluation quality is limited |
| Moderate | Objective evidence covers at least two task clusters or about six independent decisions, includes an unassisted signal, and is internally coherent; a productive dimension may reach moderate only when the single sample is sufficiently complete and evaluation quality is good |
| High | Not available from the initial diagnostic; requires broader, repeated, recent evidence outside onboarding |

Additional rules:

- Writing and Speaking overall confidence normally remain **low** after one lightweight sample even if some individual dimensions are moderately clear.
- Oral readiness confidence remains low because sustained interaction and full speaking-task breadth are not covered.
- Contradictory results lower confidence rather than being averaged into false precision.
- The overall written/oral snapshot inherits bottleneck uncertainty; confidence is not averaged upward by a strong Reading result when Writing is missing.
- Missing evidence is displayed as a gap and converted into a near-term collection task.
- Assisted evidence can establish a training starting point but cannot support strong readiness language.

Stage 15 will define the calibrated readiness-confidence model. These rules constrain the first result so it cannot outrun the evidence.

### 3.9 CEFR display

**Decision:** The diagnostic does **not** show a single estimated CEFR level as its headline result.

A global label such as “You are A2” would hide uneven skills, imply a placement precision the short sample cannot support, and shift attention away from exam readiness. The primary learner-facing language is:

- **Foundation** — start with substantial support;
- **Bridge to B1** — use guided A2/B1 work and reduce help;
- **B1 evidence building** — begin or continue realistic B1 probes;
- **Not enough evidence** — collect a missing or invalid sample.

Skill detail may state the **difficulty of tasks successfully attempted**, for example “handled A2-style reading with little help.” That is a description of observed task evidence, not a certified CEFR estimate of the person. If CEFR terminology is shown in details, it must be approximate, skill-specific, and paired with confidence.

### 3.10 Learner-facing result

**Decision:** The result is a calm starting snapshot with no celebratory score reveal and no precise pass probability.

It contains:

1. **Starting phase:** Foundation, Bridge to B1, or B1 evidence building, chosen as a coaching summary rather than a global language level.
2. **Written and oral status:** shown separately, each with evidence confidence and any missing area.
3. **Five skill signals:** current working difficulty/support need, one concise observation, and confidence.
4. **One observed strength:** only when supported by evidence.
5. **One or two priorities:** the highest-value blockers or evidence gaps.
6. **Evidence caveat:** “This is a starting estimate. It will change as you complete unassisted and timed work.”
7. **First recommended session:** duration, activity outline, and a plain-language “why this first?”
8. **Resume path:** if the diagnostic is provisional, a visible option to finish missing samples.

The diagnostic may say “Too early to judge pass readiness.” It must not display a precise readiness percentage merely to make the dashboard look complete.

Example:

> **Starting phase: Bridge to B1**
>
> Reading gives us a moderate early signal at A2/B1 bridge difficulty. Listening details are a clearer blocker, and Speaking still has low evidence from one short sample.
>
> **Start here — 22 minutes:** repair appointment times and restrictions, retry them in a fresh listening task, then collect one short speaking follow-up.
>
> **Why this first:** it targets an observed high-value weakness and closes an oral evidence gap.

### 3.11 Learner-model initialization

**Decision:** The diagnostic initializes a provisional learner state rather than a permanent placement label.

For each skill and sampled subskill, it supplies:

- provisional working difficulty and next recommended difficulty;
- observed performance signal;
- assistance dependence;
- initial confidence and evidence coverage;
- timing/replay/reference context;
- sampled productive rubric dimensions;
- candidate vocabulary, grammar, comprehension, production, or strategy issues;
- technical limitations and explicit evidence gaps;
- provenance back to the diagnostic task and evaluation.

It also supplies shared coaching inputs:

- exam date/status and declared study-time context from onboarding;
- initial journey phase;
- first-session eligibility;
- areas that must be sampled soon;
- which evidence is diagnostic, assisted, untimed, incomplete, or unassisted.

Stage 04 will define the durable learner-model schema, decay, mastery, and cross-skill relationships. It must be able to represent this provisional baseline without turning sparse diagnostic signals into stable mastery claims.

### 3.12 First daily recommendation

**Decision:** The first recommendation is created by a small, explainable priority rule rather than an AI-generated study plan.

Priority order:

1. If an entire pass-critical component lacks usable evidence, schedule the smallest feasible evidence task, unless a known permission/accessibility block makes it impossible.
2. Otherwise select a weakness that is both exam-relevant and supported by at least low-confidence evidence.
3. Prefer a **reachable repair opportunity** over the absolute weakest task when the latter is still too difficult for a meaningful attempt.
4. Fit the activity to the learner's declared session time.
5. Demonstrate the core loop with an attempt, narrow diagnosis/repair, and a fresh retry.
6. Add at most one short secondary evidence-gap task when time remains.
7. Explain the recommendation using the observed signal, TELC relevance, and expected evidence gained.

A missing Speaking sample is prioritized, but not allowed to block all training if microphone access is unavailable. In that case the plan targets the best observed blocker and keeps oral evidence visibly pending.

The exact daily optimization function belongs to Stage 06. Stage 03 locks the input and first-plan behavior.

## 4. Detailed Product Model / Rules for this Stage

### 4.1 Diagnostic flow

1. **Set expectations:** “This takes about 20 minutes, adapts by skill, and can be paused.”
2. **Choose an initial route:** Use self-view and prior preparation only to choose the first difficulty.
3. **Sample Reading:** Route within the block and stop hard probes early when appropriate.
4. **Sample Language Elements:** Use contextual decisions rather than isolated grammar trivia.
5. **Sample Listening:** Use short reusable audio; record replay/help.
6. **Request microphone at point of use:** Explain what the short sample adds and what happens if permission is declined.
7. **Collect Writing and Speaking:** Their order may be swapped to reduce fatigue or accommodate microphone context; both remain required offers.
8. **Evaluate available evidence:** Objective areas immediately; productive areas provisionally if evaluation is delayed.
9. **Show the starting snapshot:** Separate observed signal, uncertainty, and missing evidence.
10. **Offer the first plan:** One primary high-value loop and, if useful, one small evidence-gap task.

The diagnostic is not required to use this exact screen order. The product requirements are breadth, adaptation, transparent evidence, and a short path to the first useful plan.

### 4.2 Completion states

| State | Condition | Product behavior |
|---|---|---|
| Complete baseline | All five areas offered; each has usable evidence or an explicit not-evidenced reason | Show full starting snapshot and first plan |
| Provisional baseline | Minimum useful baseline met, but one or two areas remain missing or invalid | Show a clearly provisional snapshot, first plan, and near-term completion task |
| Incomplete | Minimum useful baseline not met | Save progress, show what was learned without broad conclusions, and make Resume diagnostic the primary action |
| Evaluation pending | Tasks completed but productive evaluation is unavailable or delayed | Use objective evidence to create only a provisional plan; do not invent productive scores |
| Invalidated block | Technical interruption, corrupt audio, or unusable recording | Exclude the block from ability scoring and offer a short retry |

### 4.3 Content requirements

Diagnostic content must be:

- original or clearly reusable, grounded in Corpus-derived task patterns rather than copied from restricted reference exams;
- reviewed before routine use;
- tagged by skill, task pattern, difficulty, assistance compatibility, answer/rubric, and evaluation limits;
- stable enough that results are comparable over time, while rotating among equivalent forms to reduce memorization;
- downloadable/reusable where possible so every learner does not trigger content generation.

Corpus confidence and usage rights remain separate. A high-confidence reference exam may shape the task pattern without granting permission to display its exact content.

### 4.4 Product guardrails

- Do not begin with a full B1 mock.
- Do not require a learner to fail repeated B1 items to prove they are below B1.
- Do not infer Speaking from Writing, Listening from Reading, or production from multiple-choice success.
- Do not call one short productive sample “oral/written readiness.”
- Do not convert self-reported level into mastery evidence.
- Do not average missing evidence into a zero score.
- Do not treat assistance as failure; record it as context.
- Do not compare raw percentages across different difficulty routes without adjustment.
- Do not show a global CEFR placement label as the main outcome.
- Do not block Day 1 coaching merely because confidence is not yet high.
- Do not use a premium AI conversation simply to make the diagnostic feel personalized.

## 5. Edge Cases / Failure or Uncertainty Handling

| Situation | Evidence treatment | Learner experience / next action |
|---|---|---|
| Learner is clearly below the first difficulty | Stop harder probes, collect one scaffolded confirmation, preserve assistance context | “We’ll start here with support,” then continue to the next skill |
| Learner is already strong | Step up quickly and use a small number of B1 probes | Extend only until a useful ceiling is found; never turn onboarding into a mock |
| Skills are uneven | Maintain independent routes and confidence | Show skill-specific starting needs rather than one level |
| Learner stops early | Retain valid blocks | Resume later; show a provisional plan only if the minimum useful baseline exists |
| Writing is blank or extremely short | Distinguish skipped, misunderstood, timed out, and attempted-but-limited | Offer one simpler prompt or mark not enough evidence; do not silently score zero |
| Microphone permission is denied | No oral ability is inferred | Explain the evidence gap and offer a later permission retry; typed rehearsal remains learning only |
| Recording is noisy or speech recognition fails | Mark technical quality and exclude unsupported dimensions | Offer one short retry; do not interpret transcription failure as poor German |
| Listening audio fails | Invalidate that block rather than showing the transcript as a replacement | Retry with working audio or mark Listening not evidenced |
| Productive evaluator is unavailable | Keep the response and show evaluation pending | Build only a provisional plan from other evidence; evaluate once, not repeatedly |
| Self-view conflicts with performance | Trust observed evidence for routing while keeping the learner's context | Explain adaptation neutrally; do not confront the learner with a “wrong” self-rating |
| Objective results contradict each other | Lower confidence and choose a later clarifying task | Avoid a sharp placement conclusion from noisy few-item evidence |
| Assistance is requested frequently | Record the highest meaningful assisted performance | Start with suitable scaffolding; never count it as equivalent to unassisted readiness |
| Accessibility requires more time | Preserve evidence and mark timing context | Do not penalize extra time in onboarding; later timed-mode accommodations are shaped separately |
| Very limited connectivity | Reuse cached tasks/audio where available | Preserve completed evidence; defer only the blocks that truly require connectivity |

## 6. Relationship to Other Bestehen Stages

- **Stage 04 — Learner Model:** must represent the provisional per-skill state, evidence provenance, assistance, timing, confidence, evaluation quality, and gaps defined here.
- **Stage 05 — Mistake Memory:** decides when tentative diagnostic causes become durable weaknesses and how they recur.
- **Stage 06 — Daily Coaching Engine:** generalizes the explainable first-plan rule into ongoing session assembly.
- **Stage 07 — Core Learning Loop:** defines the exact attempt, diagnosis, repair, retry, and remember experience used in the first recommended session.
- **Stage 08 — A1→B1 Progression:** owns the full assistance ladder and calibrated movement between foundation, bridge, and realistic B1 work.
- **Stages 09–13 — Skill Coaching:** own complete task mappings, detailed scoring rubrics, explanations, and repair behavior. They must preserve the direct initial signal defined for each area.
- **Stage 15 — TELC Readiness:** decides the final readiness representation, weighting, evidence minimums, pass constraints, and calibration. It must keep initial diagnostic evidence weakly weighted and uncertainty visible.
- **Stage 18 — Coach Personality:** refines the exact language for starting phases, weakness, and uncertainty.
- **Stage 19 — Information Architecture:** decides screens and navigation while preserving the short, resumable flow and clear transition to Today's Plan.
- **Stage 21 — Content Strategy:** supplies reviewed original diagnostic forms and quality/rotation rules.
- **Stage 24 — Account/Data:** decides local/account storage, sync, audio retention, and deletion while preserving resumability and learner control.
- **Stage 25 — Accessibility/Devices:** defines input, permission, timing, transcript, and low-connectivity accommodations.
- **Stage 26 — Analytics:** measures completion, route accuracy, later transfer, diagnostic-to-plan usefulness, evaluation quality, and cost.
- **Stage 27 — Cost Boundaries:** sets portfolio-wide limits; this stage already defines the low-cost diagnostic default.

### Corpus relationship

Corpus provides patterns, difficulty/relevance signals, topics, vocabulary/grammar frequency, and distractor evidence used to design diagnostic forms. The App owns learner routing, evidence interpretation, confidence, and the coaching output. Diagnostic items should usually be original, reviewed App content rather than raw reference material.

## 7. Cost Notes

### Preferred low-cost default

The routine diagnostic should require:

- **zero per-user generation calls** for Reading, Language Elements, Listening, Writing prompts, Speaking prompts, or feedback copy;
- reviewed objective items with deterministic answer scoring;
- pre-recorded human audio or pre-generated, reviewed audio cached and reused across learners;
- at most one short speech-to-text operation for the 45–90 second Speaking sample;
- at most one batched low-cost rubric evaluation covering the Writing response and Speaking transcript, after deterministic checks;
- cached templates for the starting snapshot and first-plan explanation;
- deterministic routing and recommendation logic.

A premium model is **not** invoked by default during onboarding. If the cheap productive evaluation is uncertain, unavailable, or contradictory, the correct fallback is lower confidence and another future sample—not an automatic premium call. A later high-stakes readiness or mock decision may justify premium reevaluation under rules defined in the skill/readiness stages.

If speech-to-text is unavailable, the App retains the recording only according to the later data policy and marks affected dimensions as pending/not evidenced. If all AI evaluation is unavailable, objective results can still initialize a provisional first plan.

### Upgrade triggers

A more expensive evaluation path is justified only if later validation shows that the low-cost approach materially misroutes learners, gives unsafe productive feedback, or weakens readiness calibration. Before upgrading, prefer better rubrics, reviewed examples, batching, prompt/model tuning, and a second short sample.

This stage has modest recurring-cost impact: one short transcription and one batched cheap evaluation per completed diagnostic. All other routine work should be deterministic or precomputed.

## 8. Decisions Made

1. Set a 20-minute adaptive core, a 12–16 minute foundation route, and a hard 30-minute ceiling for stronger learners.
2. Defined complete, provisional, incomplete, pending-evaluation, and invalidated diagnostic states.
3. Chose an adaptive per-skill A1/A2/B1 mix with Foundation, Bridge, and B1-probe routes.
4. Defined direct initial evidence for Reading, Language Elements, Listening, Writing, and Speaking.
5. Defined a short functional Writing sample with explicit content points and recorded scaffolding.
6. Defined a 45–90 second Speaking sample with a personal response and a fixed two-turn planning exchange.
7. Defined early exit from hard probes, one easier confirmation, and independent skill routing.
8. Defined diagnostic evidence fields, deterministic objective scoring, compact productive rubrics, and candidate—not permanent—mistake signals.
9. Capped initial confidence at moderate and productive overall confidence normally at low.
10. Rejected a global CEFR placement label; selected skill-specific Foundation, Bridge to B1, B1 evidence building, and not-enough-evidence language.
11. Defined the learner-facing starting snapshot with separate written/oral status, five skill signals, blockers, evidence gaps, and the first plan.
12. Defined the provisional learner-model initialization contract and explainable first-recommendation rule.
13. Chose a low-cost default using reviewed reusable content, deterministic routing/scoring, one short transcription, and at most one batched cheap productive evaluation.
14. Defined honest fallbacks for missing permissions, technical failures, sparse/contradictory evidence, abandoned diagnostics, and unavailable AI evaluation.

## 9. Open Questions / Deferred Decisions

### Open owner questions

**None.** The diagnostic can be responsibly shaped from the existing product decisions.

### Deferred product decisions

- Durable learner-model schema, mastery update rules, and confidence decay — Stage 04.
- Exact promotion of diagnostic mistakes into recurring weakness memory — Stage 05.
- Ongoing session optimization weights — Stage 06.
- Full assistance ladder and empirically calibrated transition thresholds — Stage 08.
- Exact TELC task mappings and full skill-specific rubrics — Stages 09–13.
- Readiness formula, displayed bands, minimum evidence, written/oral gates, and outcome calibration — Stage 15.
- Exact screens, visual hierarchy, and permission UI — Stage 19.
- Final content-generation, review, and rotation policy — Stage 21.
- Audio retention, privacy, deletion, and sync behavior — Stage 24.
- Accessibility accommodations and supported input methods — Stage 25.
- Model/provider selection and technical architecture — post-shaping architecture work.

The numerical routing heuristics in this stage are initial product defaults. Stage 26 should validate whether they correctly minimize unnecessary difficulty while still finding a useful starting point.

## 10. Definition of Done Check

- [x] Decide target duration.
- [x] Decide A1/A2/B1 content mix.
- [x] Collect initial evidence for:
  - [x] Reading
  - [x] Language Elements
  - [x] Listening
  - [x] Writing
  - [x] Speaking
- [x] Define a lightweight speaking sample.
- [x] Define a lightweight writing sample.
- [x] Represent uncertainty where evidence is weak.
- [x] Decide whether estimated CEFR level is shown.
- [x] Define how results initialize the learner model.
- [x] Define behavior when the learner is far below real B1 difficulty.
- [x] Define the first learner-facing result and recommendation.
- [x] Define a financially sustainable routine diagnostic.

**Stage 03 is complete when personalization can begin on Day 1 without forcing a long traditional placement test or manufacturing readiness certainty.**
