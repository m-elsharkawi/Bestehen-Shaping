# Bestehen / App — Stage 16: Mock Exams

> **Status:** Authoritative Stage 16 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Mock promise:** Rehearse the constraints that actually matter, turn realistic performance into trustworthy readiness evidence, and convert lost points into focused coaching without letting one good or bad simulation become false certainty.

## 1. Purpose and Scope

This document defines the complete mock-exam model for Bestehen / App: **mini-mocks, section/component mocks, and full mocks**.

Mocks have two jobs that ordinary practice cannot fully replace:

1. **measurement** — collect fresh evidence under increasingly authentic TELC B1 constraints; and
2. **rehearsal** — expose timing, sequencing, playback, preparation, interaction, stamina, and execution problems that isolated practice can hide.

Mocks are not a separate curriculum and are not a magical readiness multiplier. They use the same learner model, evidence ledger, Mistake Memory, progression conditions, and readiness logic already defined in earlier stages. A valid target-condition result is strong because of **what was measured and under which constraints**, not because the screen was labelled “mock.”

This stage defines:

- full, section/component, and mini mock modes;
- target timing and measured-block rules;
- pause, stop, interruption, and resume semantics;
- Listening playback restrictions;
- Speaking simulation and partner behavior;
- TELC-aligned scoring and pass-result wording;
- post-mock analysis and learner-model updates;
- mock recommendation cadence and retest logic;
- how repeated passing mocks strengthen readiness evidence;
- source/reference versus original/generated mock content;
- rights-safe learner-facing behavior;
- bounded AI cost for Writing and Speaking evaluation and oral interaction.

This is product shaping, not implementation architecture. It does not choose a database, state-machine library, model vendor, audio stack, content-generation pipeline, storage system, or final Ready-to-Book threshold.

### Core decision

**Mocks are scope-labelled P4 measurement commitments. Bestehen gives target-condition credit only to the exact task units and constraints that were reproduced cleanly. A full mock adds sequencing/endurance evidence, but it receives no secret score bonus and remains one correlated evidence occasion.**

---

## 2. Inputs / Existing Decisions

Stage 16 preserves the project overview, identity, and App Stages 01–15.

### 2.1 Existing evidence and coaching constraints

- Bestehen is a calm, direct, evidence-based **exam coach**. Readiness, not completion or streaks, is the central progress concept.
- Written and oral pass risk remain independent. Strong written performance cannot hide weak/unknown oral evidence and vice versa.
- The learner model uses an evidence ledger. Mastery, confidence, freshness, assistance, timing, and readiness contribution remain separate.
- Stage 04 classifies valid recent target-condition evidence as **E4**, but one multi-item mock is still one correlated occasion for confidence.
- Missing or invalid evidence is **unknown**, never silently converted into zero capability.
- Stage 05 allows one realistic mock failure to create a high-priority candidate/provisional blocker, but normally requires fresh independent recurrence before creating a fine-grained known weakness.
- Stage 06 requires post-mock coaching to surface at most **two immediate priorities**, then use clarification, repair, fresh transfer, and usually a section retest before another full mock.
- Stage 07 defers Diagnose → Repair → Retry until the measured mock block ends. No between-item coaching is permitted in target-condition measurement.
- Stage 08 defines P4 as exact target format, difficulty, timing, playback/reference/preparation constraints, no answer-bearing help during the measured attempt, and deferred coaching.
- A pause, restart, extension, transcript, hint, translation, or other non-target support may remain useful practice but cannot silently retain an unchanged target-condition claim.
- Stage 14 allows valid mock evidence to satisfy due review obligations when the mock directly tests the relevant capability and condition.
- Stage 15 already owns readiness scoring, written/oral pass gates, evidence recency, predicted ranges, and the rule that a mock result has no additional hidden weight beyond its valid E4 evidence.

### 2.2 Current launch blueprint snapshot

The target blueprint was already reverified by Stages 09–15 on **19 August 2026**. Stage 16 consumes that versioned project knowledge rather than treating the following as permanent constants.

| Target block / area | Current launch behavior | Current points / gate |
|---|---|---:|
| Reading + Sprachbausteine | Shared **90-minute** block; no invented official per-part minute split | Reading 75 + Sprachbausteine 30 |
| Listening | Approx. **30 minutes**; H1 once, H2 twice, H3 twice | 75 |
| Writing | One current-format email, exact **30-minute** condition | 45 |
| Written component | Reading + Sprachbausteine + Listening + Writing | **225**; pass gate **135/225** |
| Oral preparation | Current verified **20-minute** preparation window for all three oral tasks | — |
| S1 | Get to know each other, approx. **3 min** | 15 |
| S2 | Discuss a topic, approx. **6 min** | 30 |
| S3 | Plan something together, approx. **6 min** | 30 |
| Oral component | Full S1 → S2 → S3 simulation | **75**; pass gate **45/75** |

Before a mock is labelled **current TELC-realistic**, Bestehen must use the currently approved blueprint version. A later blueprint change can reduce the target-format relevance of an old mock without erasing the learner capability that was genuinely demonstrated.

### 2.3 No conflict with Stage 15 readiness

Stage 15 remains authoritative for the learner-facing readiness state:

- Readiness Index is driven by the weaker written/oral component, not an overall total that hides a failed component.
- “Safe pass range” requires adequate recent, direct, target-condition coverage and confidence; one passing mock cannot manufacture it when the evidence base is otherwise narrow.
- One valid mock can move estimates materially, narrow uncertainty, and refresh target-condition evidence.
- Repeated coherent E4 evidence should eventually dominate older assisted/untimed evidence.

Stage 16 defines **how mock evidence is produced and repeated**, not a second readiness formula.

---

## 3. Decisions and Rationale

### 3.1 Use three mock modes, each with an honest evidence scope

**Decision:** Bestehen exposes three learner-facing mock modes:

| Mode | Typical commitment | Primary purpose | What it may claim |
|---|---:|---|---|
| **Mini-mock** | Normally **8–25 min** | Compact target-pressure probe, early exposure, or post-repair verification | Only the task units/conditions actually measured |
| **Section / component mock** | One complete exam area/block or one complete pass-gated component | Diagnose a section, timing pattern, or oral/written component without paying the fatigue cost of the whole exam | Complete scope named by the mock; no claims about omitted areas |
| **Full mock** | All current target components | Rehearse the complete examination package and produce the strongest App-generated cross-section evidence | Full written and oral result when every required component is valid/evaluated; sequencing/endurance only where actually reproduced |

“Mini” does not mean easy. “Full” does not mean more heavily weighted. The labels describe **scope**, not difficulty or score multiplier.

### 3.2 A mock result is immutable; coaching creates new evidence afterward

**Decision:** Once a measured block ends, its original responses, conditions, and score remain the mock result. Post-mock explanation, replay, model answers, repair, revision, and fresh retries create **new learning evidence** and never rewrite the original mock.

This keeps the readiness history auditable and prevents a repaired answer from retroactively turning a failed simulation into a pass.

### 3.3 Reproduce constraints only when they add real evidence value

**Decision:** The App does not add “realism theater.” A mock reproduces target constraints because they affect exam performance:

- shared time allocation;
- exact audio playback opportunities;
- continuous measured blocks;
- preparation rules;
- no coaching/translation/model help;
- target task order where relevant;
- partner interaction;
- deferred feedback;
- realistic task length and completion pressure.

The App must not invent harsher countdowns, artificial stress, fake examiner hostility, or unofficial per-part time limits.

### 3.4 Target-condition validity is granular

**Decision:** A mock has a validity state at both the overall mock and the smallest useful scored unit/part.

If a full mock is interrupted after a valid 90-minute Reading + Sprachbausteine block, that completed block may remain useful target-condition evidence even though the **full mock** no longer provides complete cross-section sequencing/endurance evidence. Likewise, a technical failure in one Listening asset does not automatically erase valid Writing evidence.

This granular behavior prevents both extremes: treating a compromised full mock as perfectly valid or throwing away every fair completed result.

### 3.5 Mock cadence is event-driven, not a calendar quota

**Decision:** The coach recommends a mock when its result is likely to change a coaching/readiness decision. It does not prescribe “one mock every Sunday” regardless of learner state.

Mini and section mocks carry most ongoing measurement. Full mocks are deliberately less frequent because they consume time, concentration, content forms, productive-evaluation cost, and recovery capacity.

### 3.6 Two passing full mocks are a consistency milestone, not a hidden readiness gate

**Decision:** Every valid target-condition mock contributes evidence immediately. There is no “nothing counts until mock #2.”

However:

- **one** passing full mock is one strong correlated occasion;
- **two independent passing full mocks on separate days** are the default point at which Bestehen may say the learner has **repeated a pass in full simulation**;
- a third or later pass provides diminishing confidence/breadth value rather than an arbitrary bonus.

This is a **mock-consistency milestone**, not a new Ready-to-Book rule. Stage 15 can reach strong readiness from equivalent distributed E4 evidence, and Stage 17 decides whether repeated full-mock passing is required for booking advice.

### 3.7 Original reviewed simulations are the default learner-facing mock content

**Decision:** Exact source/reference exams define the target mechanism, scoring, difficulty, audio behavior, and content characteristics. They are not automatically learner-playable assets.

Learner-facing mocks default to **original, reviewed, target-calibrated forms** unless the specific source asset has confirmed reuse rights. Public accessibility is not redistribution permission.

### 3.8 Productive evaluation is bounded, not free and not always premium

**Decision:** A full mock can justify real AI cost because Writing and Speaking need open-response judgment, but that cost is tightly bounded:

- objective sections are deterministic;
- normal mock Writing uses one structured low-cost evaluation;
- normal mock Speaking uses one structured post-block evaluation plus only the speech/transcription work needed to judge it;
- an adaptive partner is paid for only where real interaction adds evidence value, primarily S2/S3;
- a stronger/second evaluator is invoked once only when the sample is high-impact and the standard evaluator is too uncertain or contradictory.

No extra model call is required for readiness recomputation, Mistake Memory, post-mock prioritization, or summary prose.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Common mock contract

Every mock, regardless of size, must declare before Start:

- **scope:** exact task families/blocks included;
- **purpose:** baseline, target-pressure probe, section diagnosis, timing, consistency, stamina, or readiness evidence;
- **expected commitment:** measured duration plus any target preparation;
- **rules:** help, playback, notes, pause, restart, and feedback restrictions;
- **content freshness:** no answer exposure that would invalidate independence;
- **target blueprint version:** the exam definition being simulated;
- **equipment needs:** audio and/or microphone where relevant;
- **result promise:** what score/pass statement the scope can and cannot support.

Once the learner starts a measured block, the App becomes an exam environment rather than a coach. Coaching resumes only after the block ends or the learner stops the simulation.

### Mock validity labels

A completed mock/part can be:

| Label | Meaning |
|---|---|
| **Clean target-condition** | Current blueprint, valid fresh content, correct timing/playback/prep/interaction, no answer-bearing help, no material interruption |
| **Valid but modified** | Useful attempt, but one condition such as extra time/replay/help/pause changed the claim; normally practice/P3-strength for affected dimensions |
| **Partially valid** | Some completed units remain defensible, but the overall block/full-mock claim is incomplete |
| **Invalid / excluded** | Technical/content/partner/evaluator failure makes the affected result unfair or unsupported |
| **Pending evaluation** | Measured response is valid, but productive scoring is not yet trustworthy/available |

The learner sees plain language, not evidence-tier jargon.

---

## 4.2 Mini-mocks

### Definition

A **mini-mock** is a compact, no-coaching measured block that covers one complete target unit/part or a small coherent cluster of target behaviors, normally in **8–25 minutes**.

Examples:

- a complete H1 or H3 Listening target-playback probe;
- one current-format Reading task family at B1 difficulty;
- one full SB1/SB2 target-format set with a clearly labelled Bestehen pace target;
- one S1/S2/S3 target-condition part probe;
- a short mixed objective cluster designed to test concentration/timing across two related target families.

### Product rules

1. Mini-mocks are useful **before the learner is ready for a whole section** because they expose the feeling of no-help/deferred-feedback measurement without wasting a full form.
2. They may also verify a repair under more realistic conditions before another section/full mock.
3. A mini-mock receives E4 only for units whose target condition is actually definable and reproduced. For example, exact H1 playback can be target-condition part evidence.
4. Reading and Sprachbausteine mini-mocks cannot claim the **official shared 90-minute allocation condition** because no official standalone minute split exists. They remain strong B1/pace evidence until measured inside the combined block.
5. An isolated Speaking part may be a target-condition **part probe**, as already allowed by Stage 13, but it does not replace the full 20-minute-preparation + S1→S2→S3 oral simulation.
6. Mini-mocks do not receive overall pass/fail labels unless their scope itself has a real official pass gate. Most do not.
7. No repair occurs inside the mini-mock. Post-result repair uses separate fresh content.

### Recommendation triggers

Recommend a mini-mock when:

- the learner understands the task mechanism and a target-pressure probe would be informative;
- a known/repaired weakness needs a realistic verification;
- the learner has too little time or energy for a full section but a valid compact measurement fits;
- evidence is stale/assisted and one small clean attempt can close a decision-relevant gap;
- a booked date creates urgency but a full mock would currently be mostly format confusion or fatigue.

A learner may select a mini-mock earlier; a low score is diagnostic evidence, not a progression punishment.

---

## 4.3 Section and component mocks

### Definition

A **section mock** reproduces one complete target area/block or one complete pass-gated component. The product always names the scope explicitly rather than using one ambiguous “section test” label.

### Launch section/component menu

| Mock scope | Target-realistic contract | Result semantics |
|---|---|---|
| **Reading + Sprachbausteine block** | Full current structure in the **shared 90 minutes**, no invented split, no coaching | Objective point contribution across Reading 75 + SB 30; timing/allocation evidence; no standalone official pass gate |
| **Listening section** | Full H1→H2→H3 sequence, current audio, H1 once / H2 twice / H3 twice, no replay/seek/transcript | 75-point Listening contribution plus playback/attention evidence; no invented standalone pass gate |
| **Writing section** | Full current prompt, **30 minutes**, no model/translation/language correction | 45-point TELC-aligned estimate when evaluator confidence is sufficient; no invented standalone official Writing pass gate |
| **Written component mock** | Reading+SB → Listening → Writing using the current target block order/rules and only target-authorized transitions | **225-point** written result; may state whether the current **135/225** written gate was cleared when all required evidence is valid |
| **Oral component mock** | **20-minute** target prep, then S1→S2→S3 with valid partner interaction and no coaching | **75-point** oral result; may state whether the current **45/75** oral gate was cleared when evaluation is valid |

A Reading-only or SB-only full-format exercise may exist as focused target-like practice or a mini/area probe. It must not be presented as complete official timing evidence because the target shares the 90-minute budget.

### When to recommend a section/component mock

Default recommendation requires:

- the learner understands the included task formats;
- direct evidence exists for most included task families, so the mock measures performance rather than onboarding;
- the result will resolve a meaningful timing, playback, interaction, freshness, or readiness question;
- required media/equipment/evaluator quality is available;
- the learner has enough time/energy to finish the measured block fairly.

Exception: with a booked near-term exam, the coach may recommend an earlier section/component baseline even when performance is likely weak, because learning the size and cause of the risk can be more valuable than waiting for a comfortable score.

---

## 4.4 Full mocks

### Definition

A **full mock** completes every current target component using one coherent fresh mock form/package:

1. complete **written component** under current target blocks and rules;
2. complete full **oral component** with target preparation and S1→S2→S3 interaction;
3. wait for all required productive evaluation;
4. produce one final full-mock result and post-mock coaching plan.

The App does not invent a stricter relationship between written and oral scheduling than the verified target requires. The oral simulation may be a separate appointment/block when that better matches the current blueprint or partner logistics. If written and oral are not completed in one planned rehearsal day, the result is still a **complete mock package**, but Bestehen does not claim unmeasured whole-day endurance.

### Full-mock eligibility recommendation

The coach normally recommends the **first full mock** when:

- every major target task family has been encountered at least once;
- the learner can make a meaningful unassisted B1 attempt in every major written/oral area;
- basic format confusion is no longer likely to dominate the score;
- microphone/audio setup and productive evaluation are ready;
- there is enough fresh target-equivalent content to avoid recent answer exposure;
- the result is likely to change readiness, pacing, or coaching priority.

This is a recommendation gate, not a lock. The learner can choose an earlier baseline.

A **booked exam** is the principal exception: if the date is near and realistic risk is still unknown, an early full baseline may be more valuable than postponing realistic evidence.

### Full-mock measured behavior

- No correctness feedback, coaching, translation, grammar hints, model answers, extra audio playback, transcript, or phrase bank inside measured blocks.
- Target-permitted notes and ordinary non-answer-bearing access support remain distinct from learning help.
- Written responses and objective selections are final for the mock when the applicable target block ends.
- Speaking partner behavior is target-like and non-coaching.
- Technical validity is checked before learner performance is penalized.
- Post-mock repair begins only after the measured scope being scored has ended.

### What full mocks add beyond section mocks

Full mocks uniquely add evidence about:

- moving through multiple written areas under cumulative attention load;
- shared written time allocation and recovery from a difficult part;
- completion discipline and decision-making under sustained pressure;
- the difference between isolated strong sections and component-level consistency;
- complete written and oral pass-gate results in one mock package.

They do **not** automatically provide more fine-grained mastery evidence per item than an equivalent clean section mock, and they do not count as several independent confidence occasions merely because they contain many tasks.

---

## 4.5 Timing and continuous-block rules

### Exam-realistic timing

Target-condition timing is taken from the current blueprint, not from a hard-coded generic mock timer.

Current launch anchors are:

- Reading + Sprachbausteine: one shared **90-minute** measured block;
- Listening: target audio sequence of roughly **30 minutes**, governed primarily by the audio and exact playback rules;
- Writing: exactly **30 minutes**;
- oral preparation: **20 minutes** for all three tasks;
- oral performance: S1 ~3, S2 ~6, S3 ~6 minutes under current target behavior.

### Timer behavior

- The App may show elapsed/remaining time equivalent to a fair exam aid but must not create harsher pressure than the target.
- When the target uses shared time, the learner controls allocation. Bestehen may teach a personal strategy before/after mocks, but it must never present its preferred split as an official rule.
- Reaching a target deadline ends the measured response according to the target behavior. Anything completed afterward can be useful practice but is not the same target-condition result.
- Timing evidence records both completion and whether the learner had to leave items/required content unfinished.
- Accessibility accommodations are preserved explicitly and Stage 25 determines target-equivalence; they are not automatically classified as cheating or slowness.

---

## 4.6 Pause, stop, resume, and interruption

### Learner control is unconditional

The learner may **stop any mock at any time**. Bestehen never traps the learner inside a simulation for evidence purity.

The product consequence is an evidence label, not punishment.

### Convenience pause inside a measured block

**Decision:** A normal convenience pause is not permitted while claiming continuous P4 target conditions for that block.

If the learner pauses inside:

- the 90-minute Reading + Sprachbausteine block;
- a continuous Listening sequence;
- the 30-minute Writing response;
- the measured S1/S2/S3 oral exchange;

then the affected block loses its unchanged continuous-target claim unless a future Stage 25 accommodation explicitly defines the pause as target-equivalent.

### What remains valid after an interruption

1. Completed prior independent blocks remain valid if their conditions were unaffected.
2. A completed self-contained task part may retain unit-level evidence when its own target conditions were fully met, even if the larger section can no longer claim full continuity.
3. Unanswered items are recorded as **not completed in this simulation**, not automatically transformed into broad language weakness.
4. Technical/system/partner interruption is never scored as learner inability.
5. A material technical failure invalidates or qualifies only the affected evidence where possible.

### Resume choices

After an interruption, the learner may:

- **continue for practice** from the saved point, clearly labelled non-clean/modified timing evidence; or
- **end the mock** and keep valid completed evidence; or
- later take a **fresh equivalent clean block/form** for a new target-condition result.

Resuming the same exposed form after a convenience pause does not become a second independent mock, and restarting the same known answers does not restore freshness.

### Target-authorized boundaries

Pauses/breaks that are explicitly part of the current target blueprint are preserved as target conditions. The App must not invent extra breaks and must not remove officially permitted ones merely to make the mock feel harder.

---

## 4.7 Listening playback restrictions

Listening mocks inherit Stage 11 exactly.

### Current target rule

| Part | Playback in clean target-condition mock |
|---|---|
| H1 | Each spoken text **once** |
| H2 | The longer conversation/interview **twice** |
| H3 | Each short functional text **twice** |

### Measured-block behavior

During clean Listening measurement:

- no extra replay;
- no rewind/seek/loop;
- no speed change;
- no transcript/captions that reveal the tested speech content;
- no vocabulary preview beyond target material/instructions;
- no correctness feedback or repair between items when the target flow would not provide it.

Volume/device controls that do not alter the linguistic content are not learner assistance.

### Playback failure

If audio fails, clips, skips, plays the wrong asset, or becomes materially inaudible:

- invalidate the affected item/part rather than scoring it as a miss;
- preserve unaffected valid units;
- offer a fresh equivalent later or immediately when fairness and fatigue allow;
- never grant a compensating replay of the same content and still call the original attempt clean P4 unless the current target/accommodation rules explicitly allow it.

---

## 4.8 Speaking simulation

### Target contract

A full oral mock follows the Stage 13 P4 contract:

1. receive all three current task sheets/role inputs;
2. prepare for the current **20-minute** window without translation/model/phrase help;
3. complete **S1 → S2 → S3** in sequence;
4. use only target-like neutral examiner/partner prompting;
5. receive no score, transcript, phrase recommendation, correction, or coach rescue between parts;
6. evaluate only after the measured oral block ends.

### Partner modes

| Partner mode | Mock use | Evidence consequence |
|---|---|---|
| **Fixed/prerecorded branch** | Mini-mocks, S1, targeted repair, lower-cost bounded response probes | Can provide real oral response evidence but limits sustained/adaptive interaction confidence |
| **Adaptive turn-based partner** | Default for meaningful S2/S3 section/full oral mocks | Strong interaction evidence when scenario fidelity, fairness, timing, and partner behavior are valid |
| **Human partner** | Optional high-fidelity path when available | Strong interaction evidence; still requires valid task/timing/evaluation |
| **Full-duplex premium voice** | Optional realism upgrade, not launch requirement | Adds natural overlap/backchannel realism; receives no automatic scoring bonus |

A full target-condition oral mock cannot claim strong S2/S3 interaction merely from a monologue or typed response. If the partner cannot adapt enough to make the learner respond to actual partner meaning, interaction confidence remains limited.

### Partner behavior guardrails

The mock partner must:

- stay in role and at suitable B1 conversational complexity;
- respond to the learner's meaning without coaching it;
- provide a fair opening for the learner to participate;
- use disagreement, constraints, or follow-ups when the scenario calls for them;
- not supply missing vocabulary, complete the learner's sentence, reveal a model answer, or rescue repeatedly;
- not become adversarial or unnaturally difficult merely to simulate pressure.

Partner failure invalidates or reduces the affected interaction evidence; it is never a learner mistake.

### Speaking restarts

- No convenience redo of a submitted/finished target-condition turn merely because the learner dislikes it.
- A real microphone/partner/system failure can invalidate the affected turn and justify a fresh equivalent replacement.
- Re-recording after hearing feedback or seeing the transcript is practice/repair evidence, not the original mock result.

---

## 4.9 Scoring

### 4.9.1 Use the current TELC point model where the scope supports it

For a current verified full mock, the launch scoring model is:

| Area | Maximum |
|---|---:|
| Reading | 75 |
| Sprachbausteine | 30 |
| Listening | 75 |
| Writing | 45 |
| **Written total** | **225** |
| Speaking | 75 |
| **Overall raw total** | **300** |

A **full mock clears the current mock pass result only when both are true**:

- written result is at least **135/225**; and
- oral result is at least **45/75**.

A total such as 180/300 never overrides a failed written or oral component.

Learner-facing wording uses **“Mock result”** or **“cleared the pass threshold in this simulation,”** not “you passed TELC.”

### 4.9.2 Section/component result rules

- Objective Reading, Sprachbausteine, and Listening items use reviewed deterministic keys.
- Writing uses the current official three-criterion mapping and returns an official-aligned point estimate only when evaluator confidence is sufficient.
- Speaking uses the current official-aligned part/criterion mapping and returns a point estimate only when audio, partner, and evaluator quality are sufficient.
- A **written component mock** may state whether 135/225 was cleared.
- A **full oral component mock** may state whether 45/75 was cleared.
- Individual Reading, Sprachbausteine, Listening, or Writing area mocks show points/contribution and coaching interpretation, but Bestehen does **not invent standalone official pass thresholds** for areas that do not have one.
- Mini-mocks show scoped score/accuracy/criterion behavior and target-condition validity; they do not extrapolate a fake whole-exam pass from a small sample.

### 4.9.3 Pending or invalid productive evaluation

If Writing or Speaking evaluation is pending, low-confidence, or invalid in a way that prevents trustworthy official-aligned points:

- show objective results that are already valid;
- label the productive component **pending / cannot judge reliably**;
- do not issue a final written/full pass/fail result that depends on the missing score;
- keep valid timing/task evidence;
- do not purchase arbitrary certainty merely to fill the result card.

### 4.9.4 No extra mock multiplier

Mock evidence enters Stage 15 through the normal E4/recency/evaluator-quality logic. The App does not multiply a score because it came from a full mock, nor give an extra readiness bonus for “passing.”

Full mocks add **coverage, sequencing, allocation, and consistency evidence**, which can legitimately narrow uncertainty. That is the benefit.

---

## 4.10 Post-mock analysis

### Analysis timing

No instructional post-mortem appears until the measured block is over. For a full mock, the learner may choose to see a block-level summary after the written component, but detailed coaching still must not contaminate an oral component that is intended to remain a clean continuation of the same mock package.

### Default post-mock sequence

1. **Validity first** — what was clean, modified, interrupted, pending, or excluded?
2. **Headline result** — written/oral pass-gate result only where the scope and evaluation support it.
3. **Section/part breakdown** — points, official-aligned criterion estimates, and task-family outcomes.
4. **Execution analysis** — time allocation, unfinished work, Listening playback/attention, Writing completion, oral preparation/interaction, and technical flags.
5. **Cause grouping** — separate language/knowledge, listening recognition, strategy, timing, attention, fatigue/stamina, interaction, content/evaluator uncertainty, and technical causes.
6. **Select at most two immediate priorities** — led by written/oral pass risk and expected recoverable points.
7. **Explain evidence impact** — what changed in readiness, confidence, or evidence coverage and why.
8. **Create the recovery plan** — clarification/repair in the next suitable sessions, fresh transfer, then the smallest retest that can prove improvement.
9. **Recommend the next mock only if justified** — not as an automatic “try again.”

### Learner-facing result hierarchy

The first result view answers:

- **Did this simulation clear the relevant pass gate?**
- **Which component/section cost the most recoverable points?**
- **Was the main problem German knowledge, exam execution, or uncertain/invalid evidence?**
- **What are the one or two things the coach will work on next?**
- **What evidence is needed before another mock would be useful?**

Detailed item-level review remains available, but the product does not lead with dozens of red errors.

### Failed or borderline mock recovery

After a weak full mock:

1. do not immediately repeat the whole form;
2. identify the highest-value one or two blockers;
3. repair them with the normal core loop;
4. require fresh delayed transfer outside the failed content;
5. normally use a **section/component retest** to verify material repair;
6. recommend another full mock only after the result could plausibly reveal something new, or when a fixed exam date makes full rehearsal more valuable than waiting.

One failed full mock that contradicts stable prior evidence lowers confidence and creates clarification needs. Repeated coherent target-condition failures should eventually outweigh older assisted/untimed success.

### Passing mock follow-up

After one passing full mock, the coach says the equivalent of:

> You cleared both pass thresholds in this simulation. That is strong evidence, but it is one full-mock occasion. Repeat under fresh comparable conditions before treating full-mock passing as consistent.

The next plan normally protects weak margins and remaining evidence gaps rather than serving only comfortable maintenance.

---

## 4.11 Learner-model and Mistake-Memory updates

### Evidence flow

Every valid mock response/criterion creates the same kind of evidence observation as ordinary practice, with additional mock context:

- mock type/scope and form version;
- target blueprint version;
- item/task/part;
- content provenance and novelty;
- target difficulty;
- timing/continuous-block status;
- assistance/reference/playback condition;
- response and score/criterion result;
- evaluator method/version/confidence;
- technical/content/partner validity;
- section/component/full-mock linkage;
- fatigue/stamina/context flags where defensible.

### Update rules

1. **Clean target-condition units are E4 candidates.** Their exact Stage 15 weight still depends on recency, evaluator quality, content quality, and current-target relevance.
2. **One mock is one correlated confidence occasion.** Twenty objective decisions inside one form do not become twenty independent days of evidence.
3. Task-family and rubric evidence still flow upward; a high section score does not invent mastery in every tagged grammar/vocabulary node.
4. A fine-grained mock error creates a strong candidate/provisional blocker unless a prior known weakness is being confirmed/reopened.
5. Same-root errors inside one response/form are grouped according to Stage 05 episode rules rather than inflated into recurrence.
6. A post-mock repair/retry is a new linked learning episode and cannot change the mock score.
7. Mock evidence can satisfy due Stage 14 review obligations when it directly tests the due capability in the required lane/condition.
8. Completed valid sections from an interrupted full mock may update learner state even when the overall full-mock result is unavailable.
9. Technical/content/partner/evaluator failure creates no negative learner evidence for the affected dimension.
10. Mock timing/stamina evidence is tracked separately from language mastery so a timed collapse does not automatically trigger broad reteaching.

### Readiness update

After all relevant evaluation is available, Stage 15 recomputes:

- written and oral target-condition estimates/ranges;
- readiness band/index;
- evidence confidence;
- task-family/rubric coverage;
- current bottlenecks;
- realism/freshness coverage.

The post-mock explanation names material changes. If the readiness number barely changes because one good result confirmed an already strong estimate, Bestehen says so rather than manufacturing drama.

---

## 4.12 Recommendation cadence and evidence requirements

### Principle

**Mock recommendation is triggered by information value, repair verification, and exam urgency — not by streaks or a fixed weekly quota.**

### First mini-mock

Recommend when the learner understands the relevant task mechanism and a clean no-help probe can produce useful evidence. It may occur relatively early in Foundation/Bridge work.

### First section/component mock

Recommend when:

- most included task families have direct recent evidence;
- the learner can make a meaningful attempt without basic answer-bearing help;
- format/setup is understood;
- the result will test a real question such as shared pacing, playback, complete Writing, sustained interaction, or component pass risk.

A fixed near-term exam can justify an earlier baseline.

### First full mock

Use the eligibility recommendation in Section 4.4. It should normally be the point where the coach needs a complete realism check, not the first time the learner sees half the exam formats.

### Recommending another mock after failure

Another **full** mock is not recommended merely because the previous one failed.

Default sequence:

1. analyze;
2. repair/clarify top one or two blockers;
3. get delayed fresh transfer;
4. retest the affected section/component when material;
5. repeat full only when the repair is evidenced or the exam date makes another complete rehearsal decision-useful.

The first delayed transfer may occur in 1–3 days under Stage 14. Full-mock repetition normally waits longer because meaningful change and recovery are needed.

### Recommending another mock after a pass

- A second full mock should be on **fresh content and another day**.
- Without a booked near-term exam, the normal recommendation is roughly **7–14 days later** when consistency evidence is valuable; full mocks should not usually be more frequent than about every two weeks when mini/section evidence can answer the interim questions more efficiently.
- With a booked exam inside roughly 21 days, the interval may compress when the learner has recovered and the result will influence final preparation; **about 3 days is the normal minimum separation** for two full mocks unless the learner explicitly chooses otherwise for a special rehearsal reason.
- The final-week taper and exact mock placement remain Stage 17 decisions; Stage 16 does not create a rigid last-seven-day schedule.

These intervals are initial product defaults, not psychometric facts. Stage 26 should recalibrate them from fatigue, transfer, score stability, and real-exam outcomes.

### No unnecessary mocks

Do **not** recommend another full mock when:

- the same unresolved blocker would predictably reproduce the same result;
- the learner is still recovering from a long simulation;
- the content pool would require a near-duplicate/recently exposed form;
- productive evaluation is unavailable and the full result would not answer the intended question;
- a 10–30 minute section/mini probe can provide the needed evidence more cheaply and cleanly.

---

## 4.13 How passing mocks contribute to readiness

### Every valid mock matters

There is no minimum count before evidence starts contributing. A clean passing section/full mock updates the relevant Stage 15 evidence immediately.

### Full-mock consistency states

For learner-facing mock history, Bestehen may use these descriptive states:

| State | Meaning |
|---|---|
| **No clean full-mock result yet** | Full realism has not been measured or was incomplete/invalid |
| **One full-mock pass** | Strong single-occasion evidence; consistency not yet demonstrated |
| **Repeated full-mock pass** | At least two independent clean full mocks on separate days, fresh forms, both written/oral gates cleared |
| **Mixed recent full mocks** | Recent pass/fail or materially divergent results; confidence remains limited until cause/condition is resolved |

“Repeated full-mock pass” is descriptive evidence, not a certification.

### Important guardrails

- Stage 15 **Safe pass range** may be reached without two full mocks if equivalent distributed decision-grade E4 evidence is adequate.
- Two passing full mocks do not override an active, recent pass-critical contradiction that materially changes the estimate.
- Section/component mocks can strongly support a written/oral estimate and may be more efficient than repeated full mocks.
- A third/fourth clean pass adds breadth/recency only when the content is genuinely fresh; there is no escalating mock-count bonus.
- Old passing mocks lose current-readiness influence according to Stage 15 recency, while remaining in historical progress.
- Stage 17 owns the final Ready-to-Book rule and may choose a stricter or differently composed consistency requirement based on the full evidence picture.

---

## 4.14 Source/reference exams versus generated simulations

### Content roles

| Content role | May shape target intelligence? | May be shown exactly to learner? | Mock use |
|---|:---:|:---:|---|
| **Reusable reference/source asset** | Yes | Yes, only when rights explicitly permit intended use | May appear directly in a mock if still current, fresh for learner, and quality-valid |
| **Analysis/reference-only source** | Yes, within allowed analysis/use | **No** | Supplies blueprint/pattern/difficulty intelligence; App serves original equivalent content |
| **Original authored simulation** | Yes | Yes, subject to project rights/QA | Preferred learner-facing mock content |
| **Generated original simulation** | Yes after review | Yes after rights/QA validation | Preferred scalable expansion path; never automatically P4 just because generated |
| **Unknown/review-required source** | May inform only under the eventual Corpus policy | **No by default** | Excluded from learner-facing mocks until cleared |
| **Prohibited/blocked source** | No learner use; follow removal policy | No | Never assigned; remove from future mock forms |

### Original/generated P4 quality gate

A generated or authored mock form may be labelled target-condition only when it has been reviewed for:

- current blueprint/format and scoring mapping;
- target B1 linguistic/task difficulty;
- unambiguous objective keys and distractors;
- Writing prompt validity, recipient, scenario, and four content points;
- Speaking scenario/partner-role validity and multiple acceptable outcomes where appropriate;
- audio naturalness, pronunciation-sensitive details, part-specific playback metadata, and answer validity;
- evaluator/rubric readiness for productive tasks;
- content freshness/anti-near-duplicate behavior;
- rights/provenance status for every learner-facing asset;
- no accidental answer leak or source-specific reconstruction.

Live generation immediately before a learner's high-stakes mock is **not** the default. Batch generation/review/caching is preferred so the form can be quality-gated once and reused safely with exposure controls.

### Reference material does not create permission

A source being official, public, downloadable, mirrored, or easy to find does not itself grant Bestehen permission to redistribute it. Authentication/confidence and usage rights stay separate, preserving the umbrella Corpus principle.

---

## 4.15 Rights-safe mock behavior

### App-side safe default

Until a source has an explicit reusable status, **Bestehen does not display the exact source content in a learner-facing mock**.

Instead it may use rights-safe, independently authored/generated content grounded in allowed target intelligence such as:

- task mechanism;
- item/part counts;
- timing/playback rules;
- skill/rubric requirements;
- topic/function distributions at an appropriate level of abstraction;
- distractor and difficulty characteristics;
- scoring blueprint.

The App should not create a close paraphrase designed to reconstruct a protected exam item sentence by sentence. Original simulations should be independently expressed and reviewed for substantive freshness.

### Rights status changes

If an already-used source asset is later reclassified as non-reusable/prohibited:

- stop assigning it immediately;
- remove learner access to the source asset where required;
- substitute original/reusable content for future mocks;
- preserve only non-infringing learner evidence/history that can legally remain, such as derived score/state/provenance metadata, according to Stage 24/Corpus removal policy;
- do not erase unrelated demonstrated learner capability merely because the content source changed.

The detailed legal/removal implementation belongs to Corpus rights shaping and later architecture. The learner-facing requirement is conservative: **unknown rights never become a reason to surface exact content.**

---

## 4.16 AI and operating-cost controls

### 4.16.1 Full-mock cost budget by activity type

| Mock work | Preferred default | Recurring AI cost |
|---|---|---|
| Reading / Sprachbausteine / objective Listening | Reviewed key + deterministic scoring | **Zero** |
| Post-mock objective diagnosis | Reviewed metadata + deterministic contrasts/templates | **Zero** normally |
| Writing | W1: one low-cost structured evaluation after submission | **One bounded evaluation** |
| Speaking transcription | One low-cost pass at the coarsest block/turn granularity that supports evaluation | **Bounded** |
| Speaking evaluation | One structured low-cost post-block evaluator | **One bounded evaluation** |
| S2/S3 adaptive partner | Small/cheap turn-based interaction only while meaningful adaptation is needed | **Bounded to the measured oral task** |
| Readiness recalculation | Deterministic Stage 15 logic | **Zero** |
| Mistake Memory / next-plan selection | Deterministic structured rules | **Zero** |
| Learner-facing result summary | Reviewed templates populated from structured evidence | **Zero** normally |

### 4.16.2 Premium trigger

A stronger/second evaluator or higher-fidelity voice path is justified only when **both** are true:

1. the sample is high-value — a P4/full mock, readiness/Ready-to-Book decision, or credible learner dispute; and
2. the normal evaluator/partner is below the confidence needed for the decision, materially contradictory, or known weak for that slice.

Typical triggers:

- Writing B/C boundary or criterion disagreement that can materially change written result/readiness;
- Speaking result near the oral pass boundary with low confidence;
- intelligibility judgment that transcript-only evaluation cannot support;
- adaptive partner failure or evaluator disagreement that materially affects S2/S3 interaction;
- strong conflict with recent clean evidence that cannot be explained by timing/content/technical conditions.

### 4.16.3 One escalation, then uncertainty

Do not run a model-voting chain. One configured stronger/second evaluation may adjudicate a high-impact uncertainty. If the result still cannot be trusted, preserve a range/pending/cannot-judge state and collect another fresh sample.

### 4.16.4 Cheaper fallback

If paid productive evaluation is unavailable or intentionally skipped:

- keep objective scores and timing evidence;
- save Writing/Speaking responses according to later data policy;
- run deterministic self-check/observable feedback where valid;
- mark productive official-aligned points pending/unsupported;
- withhold any written/full pass result that depends on them;
- continue coaching from the evidence that is actually trustworthy.

The product does not degrade its core truthfulness merely to make a full mock free.

---

## 5. Edge Cases / Failure or Uncertainty Handling

| Situation | Mock behavior | Readiness/coaching consequence |
|---|---|---|
| Learner stops halfway through a full mock | Save valid completed blocks; mark full mock incomplete | Use partial evidence; no fabricated full pass/fail or full endurance claim |
| Convenience pause inside a target block | Allow learner control; downgrade affected continuous-target condition | Resume as practice or retake fresh equivalent later |
| App/device crash | Technical invalidation, not learner failure | Preserve unaffected evidence; retry fresh affected scope |
| One Listening clip fails | Invalidate affected unit/part as needed | Do not lower Listening for infrastructure failure |
| Learner uses extra replay | Keep result as assisted/modified practice | Target playback independence remains unproven |
| Learner opens transcript/help during mock | Convert affected attempt/block from clean target condition | Preserve learning value without claiming E4 for altered dimensions |
| Writing evaluator unavailable | Result remains pending | Objective evidence stands; no written/full gate result requiring Writing score |
| Writing evaluators disagree near boundary | One high-value escalation or range/lower confidence | Do not average arbitrary model scores into fake precision |
| Speaking partner goes off scenario | Partner failure; invalidate/reduce interaction evidence | Preserve valid learner production where defensible; fresh fair exchange needed |
| Microphone/audio poor | Evaluate only supported dimensions or invalidate | Never turn noise/ASR failure into pronunciation/grammar weakness |
| Full mock passes but one section is fragile | Record pass and section bottleneck separately | Coach the recoverable weakness; do not claim all areas are strong |
| Full mock fails narrowly after stable passes | Strong contradictory E4; inspect conditions/cause | Lower confidence, clarify; do not erase stable history instantly |
| Repeated full failures | Recent realistic evidence gains influence | Raise pass-risk priority; repair and reassess rather than chase scores |
| Learner wants same full form immediately | May review/continue it as practice | It is not fresh independent mock evidence |
| Learner has seen the source answers | Form is contaminated for independence | Use another fresh original/reusable form |
| Generated item is ambiguous | Invalidate/quarantine item; remove learner impact | Content QA issue, not learner weakness |
| Blueprint changes | Preserve transferable historical evidence; reduce obsolete target relevance | Update future forms before calling them current TELC-realistic |
| Rights status becomes prohibited | Stop assignment/display; substitute safe content | Preserve only permitted derived learner history; no capability reset |
| Accessibility accommodation changes conditions | Preserve exact accommodation | Stage 25 decides target-equivalence; no shame or silent equivalence claim |
| Learner is far below B1 but chooses full mock | Permit baseline with clear purpose/rules | Use result diagnostically; avoid repeated full failure as teaching method |
| Learner is fatigued after long written component | Respect stop/deferral | Do not infer language regression from compromised continuation; record context when material |

### Mock form scarcity

A personal project may initially have only a small number of trustworthy P4-ready full forms. The product should protect those forms from wasteful repetition:

- use mini/section probes for frequent verification;
- reserve full forms for decisions where full scope matters;
- maintain exposure history so recent forms are not reused as independent evidence;
- prefer a smaller reviewed bank over live unreviewed generation.

---

## 6. Relationship to Other Bestehen Stages

- **Stage 02 — Complete Learner Journey:** Stage 16 operationalizes the existing mini → section → full event-driven journey and failed-mock recovery loop.
- **Stage 04 — Learner Model:** receives granular mock observations, target-condition metadata, one-occasion confidence semantics, timing/realism, and technical/evaluator validity.
- **Stage 05 — Mistake Memory:** receives strong mock candidates without shotgun-promoting every error; post-mock recurrence/repair follows existing gates.
- **Stage 06 — Daily Coaching Engine:** uses the two-priority post-mock rule, repair/clarification, fresh transfer, and section retest before another full mock.
- **Stage 07 — Core Learning Loop:** measured mock blocks defer Diagnose/Repair/Retry; post-mock coaching creates separate fresh evidence.
- **Stage 08 — A1→B1 Progression:** P4 remains an evidence condition rather than an unlocked level. Modified mocks retain useful lower-strength evidence.
- **Stage 09 — Reading:** Reading target families contribute within the shared Reading + Sprachbausteine 90-minute block.
- **Stage 10 — Sprachbausteine:** Stage 16 is where authentic shared time-allocation evidence is finally measured.
- **Stage 11 — Listening:** exact H1/H2/H3 playback restrictions and audio validity are preserved.
- **Stage 12 — Writing:** clean 30-minute Writing, official-aligned rubric, evaluator confidence, W1/W2 escalation, and post-feedback evidence boundaries remain authoritative.
- **Stage 13 — Speaking:** full oral simulation preserves 20-minute prep, S1→S2→S3, genuine S2/S3 interaction, voice validity, and cost tiers.
- **Stage 14 — Review:** clean mock observations can satisfy due review; mock failures can reopen or reprioritize patterns according to the existing lifecycle.
- **Stage 15 — TELC Readiness:** remains the only readiness formula/pass-range authority. Mocks supply E4 evidence; no secret multiplier is introduced here.
- **Stage 17 — Ready to Book:** consumes mock consistency and all other decision-grade evidence, and owns the final booking threshold plus final 21-/7-day program.
- **Stage 19 — Information Architecture:** decides final mock setup/result/history screens while preserving scope, validity, written/oral separation, and the post-mock two-priority hierarchy.
- **Stage 21 — Content Strategy:** must implement the P4 quality gate, form freshness, anti-near-duplicate policy, and reviewed batch-generation workflow defined here.
- **Stage 22 — Corpus → App Contract:** must expose versioned target intelligence, source/rights/provenance, difficulty, and task mappings needed to assemble safe forms.
- **Stage 24 — Account/Data:** owns retention/export/deletion of raw Writing, audio, transcript, partner, and historical mock data.
- **Stage 25 — Accessibility/Device:** decides which accommodations preserve target-condition equivalence and how technical checks occur.
- **Stage 26 — Analytics:** calibrates cadence, mock-to-real-exam prediction, fatigue effects, evaluator quality, score stability, content difficulty, and false confidence.
- **Stage 27 — Cost Boundaries:** can tighten portfolio-wide spend while preserving the bounded productive-evaluation and interaction behavior defined here.

### Cross-stage guardrails

Later stages may tune cadence or implementation details, but must preserve:

- mini/section/full scope labels and no scope overclaiming;
- exact target timing/playback/preparation behavior for clean P4 evidence;
- learner control to stop without being scored for technical/interruption failure;
- no convenience pause/resume while pretending the same block remained continuous target evidence;
- no coaching inside a measured target block;
- immutable original mock result plus separate post-mock learning evidence;
- objective deterministic scoring and confidence-aware productive scoring;
- independent written/oral pass gates;
- one mock as one correlated confidence occasion;
- at most two immediate post-mock coaching priorities;
- repair + fresh transfer + section retest before routine full-mock repetition after failure;
- two full passes as a descriptive consistency milestone, not a hidden Ready-to-Book gate;
- original/reusable learner content only, with unknown rights blocked by default;
- bounded AI cost and explicit uncertainty when premium evaluation is not justified.

---

## 7. Cost Notes

Mock exams have a **meaningful but controllable recurring-cost impact** because Writing and Speaking need semantic evaluation and high-quality oral simulation may require an adaptive partner.

### Preferred personal-project default

- Build/review complete mock forms **offline in batches**; do not generate high-stakes forms live.
- Cache all approved texts, keys, audio, prompts, partner scenario states, and scoring metadata.
- Score Reading, Sprachbausteine, and selected-answer Listening deterministically.
- Use cached reviewed/native-calibrated Listening audio rather than live TTS.
- Use one W1-style low-cost Writing evaluation per submitted mock Writing response.
- Use one low-cost Speaking transcription/evaluation path per completed oral block at the coarsest granularity that still supports the rubric.
- Use adaptive partner calls only for S2/S3 turns where true response-to-meaning is necessary; fixed assets remain the cheap choice for S1 and mini/repair work.
- Generate post-mock priorities, readiness updates, and explanations deterministically from structured evidence.
- Cache evaluations by response + prompt/rubric/evaluator version so reopening a result costs nothing.

### When spending more is justified

Upgrade one productive evaluation/partner path only when the extra quality can materially change a high-impact current decision: a mock near a pass boundary, contradictory readiness evidence, poor intelligibility confidence, or a Ready-to-Book judgment.

The cheaper fallback is **lower confidence, pending points, a section retest, or another fresh sample**. It is not invented precision.

### What is explicitly not justified initially

- premium AI on every objective item;
- separate model calls for score, diagnosis, repair, summary, learner model, and readiness;
- full-duplex premium voice for every oral practice/mock;
- live generation of every mock form;
- multiple evaluator voting rounds;
- expensive human grading of routine learner mocks;
- repeated full mocks merely to generate more data when a small section probe would answer the question.

---

## 8. Decisions Made

1. Defined three scope-based mock modes: mini, section/component, and full.
2. Defined mini-mocks as compact 8–25-minute no-coaching measurement blocks with only scope-appropriate target-condition claims.
3. Defined section/component mocks for Reading+Sprachbausteine, Listening, Writing, full written component, and full oral component.
4. Defined full mocks as complete written + oral target packages with no invented same-day endurance claim when components are not actually rehearsed that way.
5. Defined target timing from the versioned blueprint, including the shared 90-minute Reading+Sprachbausteine block, approximate 30-minute Listening sequence, 30-minute Writing, 20-minute oral preparation, and current S1/S2/S3 timing.
6. Defined learner-controlled stop plus strict evidence consequences for convenience pause, resume, technical interruption, and fresh retake.
7. Locked Listening mock playback to H1 once, H2 twice, H3 twice, with no rewind/extra replay/transcript in clean P4 measurement.
8. Defined full oral simulation, partner modes, S2/S3 adaptive interaction requirements, partner-failure handling, and no coaching between parts.
9. Defined TELC-aligned scoring, independent written/oral gates, area-mock result semantics, pending productive evaluation, and no secret mock multiplier.
10. Defined post-mock analysis with validity first, component/section breakdown, cause grouping, at most two immediate priorities, evidence impact, repair plan, and selective retest.
11. Defined granular learner-model/Mistake-Memory updates, one-correlated-occasion confidence, review satisfaction, and post-mock evidence separation.
12. Defined event-driven first/repeat mock recommendations, recovery after failure, passing-mock consistency timing, and default separation guardrails.
13. Defined every valid mock as contributing evidence immediately while using two independent passing full mocks as a descriptive consistency milestone with diminishing value afterward.
14. Defined source/reference versus reusable/original/generated mock roles, P4 quality gates, and conservative rights-safe behavior.
15. Defined bounded Writing/Speaking/partner AI cost, one-escalation premium triggers, deterministic post-processing, caching, and honest low-cost fallbacks.

---

## 9. Open Questions / Deferred Decisions

### Owner questions

**None.** Stage 16 can be responsibly shaped from the existing product decisions and current verified target blueprint.

### Deferred decisions

- **Final Ready-to-Book eligibility**, including whether repeated full-mock passing is mandatory, equivalent evidence alternatives, and final 21-/7-day rehearsal/tapering — Stage 17.
- Exact visual mock setup, timer, progress, pause warning, results, history, and comparison screens — Stage 19.
- Final form-bank size, content authoring/generation workflow, quality-review thresholds, anti-near-duplicate algorithm, and source-removal operations — Stage 21 plus Corpus rights shaping.
- Raw Writing/audio/transcript/partner-event retention, export, and deletion — Stage 24.
- Which accessibility accommodations preserve an equivalent target-condition claim — Stage 25.
- Empirical tuning of 8–25-minute mini scope, 7–14-day/3-day full-mock spacing defaults, mock-consistency interpretation, fatigue/recovery, evaluator calibration, and mock-to-real-exam prediction — Stage 26.
- Portfolio-wide monetary caps and provider-specific economics — Stage 27.
- Technical state machines, streaming, model/TTS/STT providers, caching/storage architecture, and orchestration — post-shaping architecture work.

The cadence numbers in this stage are **implementable starting defaults**, not claims of psychometric precision. The product semantics — event-driven mocks, fresh forms, repair before repetition, and no confidence inflation — are the durable decisions.

---

## 10. Definition of Done Check

- [x] Define full mocks.
- [x] Define section-only/component mocks.
- [x] Define mini-mocks.
- [x] Define exam-realistic timing.
- [x] Define pause/resume behavior.
- [x] Define listening playback restrictions.
- [x] Define speaking simulation.
- [x] Define scoring.
- [x] Define post-exam/post-mock analysis.
- [x] Feed mock mistakes and valid successes into the learner model and Mistake Memory.
- [x] Define when the coach recommends another mock.
- [x] Define how passing mocks contribute to readiness and mock consistency.
- [x] Distinguish source/reference exams from original/generated simulations.
- [x] Ensure mocks respect content-usage restrictions.
- [x] Define bounded AI cost for Writing/Speaking mocks and a cheaper fallback.
- [x] Preserve the Stage 15 readiness formula, evidence minimums, and independent written/oral pass gates.
- [x] Preserve target-versioning, uncertainty, technical failure, and accessibility boundaries.

**Stage 16 is product-shaped when a learner can rehearse real target constraints at a scope appropriate to their current evidence, receive a trustworthy score only for what was actually measured, and turn every mock into a focused next coaching action without overclaiming readiness or overspending on AI.**