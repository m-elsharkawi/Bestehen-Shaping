# Bestehen / App — Stage 07: Core Learning Loop

> **Status:** Authoritative Stage 07 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** TELC B1
>
> **Loop promise:** Every useful activity turns an exam-relevant attempt into a diagnosis, the smallest responsible repair, a fresh transfer check, and durable coaching evidence.

## 1. Purpose and Scope

This document turns **Observe → Attempt → Diagnose → Repair → Retry → Remember** into the concrete coaching loop used across Bestehen / App.

The loop is the product behavior inside the diagnostic follow-up, daily coaching block, review, weak-area practice, and post-mock recovery. It defines:

- what each state means to the learner and the coach;
- the working UI behavior and state transitions;
- when a state may be compressed, deferred, or skipped;
- how long repair should take;
- what makes retry content equivalent but genuinely fresh;
- what immediate retry success does and does not prove;
- how the loop adapts to objective questions, Listening, Writing, and Speaking;
- when deterministic evaluation is sufficient and when AI adds enough value to justify its cost;
- the evidence produced at every state and how it connects to the learner model and Mistake Memory.

This is a product model, not a screen architecture, state-machine implementation, model-provider decision, or final modality rubric. Stages 09–13 will refine skill-specific formats; Stage 19 will decide screen composition; architecture may choose how to implement the states. Those later decisions must preserve the learner contract and evidence boundaries defined here.

### Core decision

**Every learning activity follows one coaching philosophy, but not every activity displays six separate screens.**

The system must always know which loop state it is in and preserve the relevant evidence. The learner sees only the steps that add value. A clear correct answer may move from Attempt through a compressed Diagnose directly to Remember. A mock defers diagnosis and repair until the measured block ends. A productive response may wait for evaluation. Compression is allowed; fabricated learning evidence is not.

### The two meanings of Observe

Earlier project context used Observe partly for Corpus intelligence: Bestehen observes recurring exam patterns before choosing what to teach. Stage 07 preserves that meaning and makes its learner-facing consequence concrete.

Observe has two coordinated sides:

1. **Coach-side observation:** use Corpus intelligence, the learner model, Mistake Memory, today’s plan, content quality, and target conditions to select a valid activity.
2. **Learner-side orientation:** show the goal, task, conditions, and permitted support needed for a fair attempt—without teaching the answer first.

Observe is therefore not a passive lesson and not solution exposure. In familiar activities it may be almost invisible.

## 2. Inputs / Existing Decisions

Stage 07 preserves the project overview, identity, and App Stages 01–06:

- Bestehen is a calm, direct, evidence-based personal German exam coach.
- A learner may start around A1, while the destination remains authentic TELC B1 performance.
- German is learned through exam-shaped activity rather than a textbook chapter sequence.
- Readiness, not lesson completion, is the primary progress concept.
- Written and oral pass risk remain separate.
- Assistance is valid learning context and must be recorded; assisted success is weaker readiness evidence than unassisted target-condition success.
- The learner model uses an evidence ledger plus derived capability, confidence, freshness, and readiness states.
- Evidence strength depends on difficulty, assistance, timing, independence, evaluation quality, content quality, and realism.
- A wrong answer is not automatically a fine-grained weakness. Diagnosis must preserve cause confidence and may remain unresolved.
- Mistake Memory groups the original attempt, repair, and same-session retry into one episode. Independent recurrence and retention require fresh later occasions.
- A same-item retry or production after seeing a model answer is weak learning evidence.
- A known weakness is repaired only through successful delayed transfer across fresh tasks and time.
- The daily coach normally gives a 25-minute session with one dominant priority, limited mixing, meaningful-boundary saving, and learner override.
- Routine recommendation, scoring, state updates, and explanations should be deterministic and inexpensive when quality is sufficient.
- Writing and Speaking evaluation may use AI, but a second model call must not exist merely to update the learner model or Mistake Memory.
- Corpus supplies task patterns, stable skill nodes, difficulty/relevance, distractor intelligence, and content relationships; the App owns learner evidence and coaching.

There are no contradictions with earlier stages. This document resolves the interaction, duration, retry, and modality behavior deliberately deferred to Stage 07.

## 3. The Canonical Loop

### 3.1 State model

~~~mermaid
stateDiagram-v2
    [*] --> Observe
    Observe --> Attempt
    Attempt --> Diagnose
    Diagnose --> Remember: sufficient success or no repair
    Diagnose --> Repair: coachable blocker
    Diagnose --> Attempt: invalid or unfair attempt
    Repair --> Retry
    Retry --> Remember: success or stop boundary
    Retry --> Diagnose: one useful re-diagnosis
    Remember --> [*]
~~~

The dominant path is linear. Branches exist to protect validity, prevent unnecessary teaching, and avoid endless repair loops.

### 3.2 State and evidence contract

| State | Learner purpose and experience | Coach behavior | Evidence produced |
|---|---|---|---|
| **Observe** | Understand what to do, why it matters, the conditions, and what help is allowed | Select a valid fresh activity; set target node/task, difficulty, assistance, timing, replay/reference rules, and evidence goal | Planning/context record only. No mastery evidence |
| **Attempt** | Try the exam-shaped task before being shown the answer or repair | Keep the response environment clean; record response, help used, timing, replay, completeness, and technical conditions | Primary evidence observation, graded from excluded to target-condition strength |
| **Diagnose** | Learn what happened and the smallest defensible reason | Validate content/evaluation; separate outcome from cause; choose one primary cause and at most one contributor; state confidence or unresolved status | Outcome attribution, manifestation, cause confidence, candidate/known pattern link. Diagnosis itself is not new mastery evidence |
| **Repair** | Fix only the blocker that prevented useful performance | Give the smallest explanation, contrast, cue, phrase, strategy, or controlled practice needed to make another attempt meaningful | Repair exposure, support/model exposure, learner interaction, and completion. Not independent mastery evidence |
| **Retry** | Prove the idea can be used on new content rather than recite the revealed answer | Serve fresh equivalent content in the same direct-evidence lane at an appropriate condition; remove answer-bearing help | Same-session fresh-transfer evidence linked to the original episode. Stronger than same-item repetition, but not retained mastery |
| **Remember** | See what changed, what remains uncertain, and when it returns | Commit valid evidence, update capability/mistake state, schedule delayed transfer or monitoring, and explain the next consequence | Derived state/lifecycle changes and due checks. Remember creates no new ability evidence by itself |

### 3.3 Working learner-facing labels

The canonical state names remain authoritative in product documents. The working UI may use shorter labels:

| Canonical state | Working UI language | Typical learner-facing element |
|---|---|---|
| Observe | **Goal** or **Before you start** | Goal/reason, instructions, conditions, available help |
| Attempt | **Try** | The task and response controls |
| Diagnose | **What happened** | Result, decisive evidence, likely cause, confidence |
| Repair | **Quick repair** | One focused explanation or micro-practice |
| Retry | **Fresh check** | “New task, same skill” and the new response |
| Remember | **What changed** | Evidence summary, status, and next return |

Stage 18 may refine exact language and Stage 19 may combine several elements on one surface. Later design must retain the semantic distinctions even when labels or screens change.

## 4. Detailed UI and Interaction Rules

### 4.1 Observe

Observe normally shows:

- the task goal in one sentence;
- why this task is in today’s plan when it is not already obvious;
- expected time;
- task format and success requirement;
- difficulty/support condition in plain language;
- timer, replay, transcript, reference, or preparation rules where relevant;
- available assistance and how using it affects the evidence claim;
- an accessibility or equipment fallback when the modality needs one.

Observe must not:

- reveal the correct answer, decisive cue, model response, or exact repair before the attempt;
- overwhelm a familiar learner with a full tutorial;
- imply that accepting language support is failure;
- call a task exam-timed when the real constraints are not active.

For a familiar due check, Observe can be one line plus a Start action. For a new task family, it can include an unscored format example that does not expose the live item.

### 4.2 Attempt

Attempt is the cleanest state in the loop.

- Feedback is withheld until the learner submits or the task ends.
- The learner can use only the support declared in Observe.
- Help used before submission is attached to the evidence; help merely offered is not.
- Post-submission feedback never retroactively changes the original attempt’s assistance status.
- Objective tasks show a clear submission boundary.
- Writing and Speaking distinguish preparation, response, and submission.
- A self-correction made before final submission under the allowed rules is part of the attempt, not a mistake episode.
- Skips, blanks, partial responses, and timeouts are distinguished.
- Technical failure is never treated as inability.

When the learner requests answer-bearing help before a meaningful response, the activity may transition into Repair, but the original evidence is recorded as assisted/incomplete rather than invented as an independent attempt.

### 4.3 Diagnose

Diagnose follows a layered order:

1. **Validate the attempt:** Was the task, media, response, and evaluator valid?
2. **State the outcome:** Correct, partially successful, incorrect, incomplete, invalid, or pending.
3. **Show the decisive evidence:** The answer cue, missed content point, rubric behavior, or observable task action.
4. **Select the narrowest defensible cause:** Vocabulary, grammar, listening recognition, misunderstanding, strategy, attention slip, production, timing, or unresolved/mixed.
5. **State confidence:** Confirmed, likely, possible, or unresolved in learner-friendly language.
6. **Choose the next branch:** Remember, Repair, a clarifying probe, or a valid new Attempt.

Rules:

- Show one primary diagnosis and at most one material contributor by default.
- Do not turn every surface error in Writing or Speaking into a repair target.
- Prioritize task fulfillment, comprehensibility, interaction, and recurring/high-impact patterns over native-like perfection.
- A correct objective answer may receive a one-line confirmation and skip repair.
- If guessing or an ambiguous reasoning path could materially distort the evidence, use one short cue-selection or explanation check. Do not demand justification after every correct answer.
- When the cause is uncertain but important, Diagnose may contain a brief contrastive probe. The result refines the cause; it is not an excuse for speculative feedback.
- When evaluation is pending, show that state and continue with other valid work. Do not fabricate diagnosis.

### 4.4 Repair

Repair must answer three questions:

1. What exact pattern blocked the task?
2. What cue, rule, phrase, or behavior changes the result?
3. Can the learner use it once with enough support to make a fresh retry fair?

The normal repair shape is:

- one practical explanation;
- one or two contrasting examples or an audio/interaction contrast;
- at most a few controlled actions when needed;
- an explicit transition to a fresh check.

Repair rules:

- Repair the cause, not merely the visible wrong answer.
- Use practical language before grammar terminology.
- Reuse reviewed repair patterns when they fit.
- Show model answers only when their learning value justifies the exposure; record that exposure.
- A revision of the original Writing/Speaking response may be useful controlled practice, but it does not replace a fresh retry.
- If the diagnosed target is too difficult, repair the smallest reachable prerequisite and keep the original target open.
- If a learner already demonstrates the needed concept during diagnosis, compress repair and move to retry.
- The learner may skip repair. The original evidence remains valid, no repair success is claimed, and the issue returns according to priority.
- Never keep the learner in an indefinite explanation/drill loop.

### 4.5 Retry

Retry is presented explicitly as **new content testing the same skill**.

The learner should know:

- the answer itself is different;
- the underlying capability is the same;
- the result checks whether the repair transferred;
- support and timing conditions that apply now.

Retry rules:

- Use the same direct-evidence lane as the weakness being tested.
- Use content with no solution exposure and no near-duplicate answer path.
- Preserve the target capability and approximate working difficulty.
- Use the same or less answer-bearing assistance than the repair.
- Record all remaining language support, replay, timing, and model exposure.
- A technically invalid retry is excluded and replaced only when another valid attempt is reasonable.
- One same-session re-diagnosis is allowed after failure; repeated cycles are capped by the repair time/attempt rules below.

### 4.6 Remember

Remember is mandatory as system behavior, even when its visible UI is only a short summary.

It states:

- what the learner demonstrated;
- whether the repair was merely helpful, passed a fresh same-session check, or remains unresolved;
- what evidence condition was used;
- whether a candidate, known weakness, stabilization, or monitoring state changed;
- when or where the skill will be checked again;
- the next session consequence if material.

Examples:

> You solved a new restriction task without a hint. The repair helped; this returns in two days to check whether it stayed.

> Your message now covers all three required points, but this was a guided revision. A fresh message will test it next time.

> The cause is still unclear. I saved the result without labeling a weakness and will use one short comparison later.

Remember must not:

- call immediate success “mastered,” “repaired,” or “resolved”;
- turn an invalid/technical event into learner evidence;
- hide support use;
- imply readiness changed materially when only weak same-session evidence exists;
- show an activity-completion reward instead of the learning consequence.

## 5. When States May Be Skipped, Compressed, or Deferred

| Situation | Allowed loop shape | Evidence consequence |
|---|---|---|
| Familiar activity / due check | Observe is compressed to goal and conditions | No loss if task validity remains clear |
| Clearly correct objective attempt with adequate evidence | Observe → Attempt → brief Diagnose → Remember | No Repair or Retry needed |
| Correct answer but possible guess materially affects a high-value claim | Attempt → brief Diagnose probe → Remember or Repair | Confidence stays limited until the probe resolves it |
| Invalid task, broken audio, input failure, or unsupported evaluator | Attempt → Diagnose invalidation → new Attempt or exit | Excluded evidence; no learner mistake |
| Cause unresolved and low impact | Attempt → Diagnose → Remember | Preserve broad result; wait for a natural clarifier |
| Cause unresolved and high impact | Attempt → Diagnose/clarifying probe → Repair only if supported | Do not buy or invent precision prematurely |
| Attention slip with strong contrary evidence | Attempt → brief Diagnose/checking cue → Remember | Candidate/monitoring only; no generic lesson |
| Learner skips repair | Attempt → Diagnose → Remember | No repair/transfer claim; issue may return later |
| Learner skips retry or runs out of time | Attempt → Diagnose → Repair → Remember | Repair exposure is saved; fresh transfer remains due |
| Productive evaluation is pending | Observe → Attempt → pending Diagnose; continue elsewhere | No final repair or fine weakness until supported evaluation arrives |
| Less than 10 minutes available | Compact complete loop or one due transfer check | Do not start a repair that cannot reach a meaningful boundary |
| Diagnostic or mock measurement | Observe → Attempt block; Diagnose/Repair/Retry deferred | Preserve clean measurement; run loop after the measured block |
| Exam mode | Observe and Attempt under exam rules; all coaching deferred | No between-item teaching; later repair uses fresh content |
| No valid fresh retry exists | Repair → Remember with transfer pending | Never reuse exposed content merely to complete the UI |
| First attempt succeeds but evidence remains too narrow for a later decision | Remember may schedule a later fresh verification | Do not force an immediate retry solely to fill the loop |

### Non-skippable product semantics

- **Attempt** cannot be skipped when the product intends to claim new learner evidence.
- **Diagnose** cannot be skipped after a meaningful shortfall, though it may remain broad or pending.
- **Remember** cannot be skipped by the system; all valid evidence and uncertainty must be preserved.
- **Repair** and **Retry** are conditional. Their absence must not be disguised as completed learning.

## 6. Repair Duration and Loop Limits

### 6.1 Default duration

**Decision:** A repair inside a normal activity should usually take **2–6 minutes** and must normally remain under **8 minutes**.

| Context | Normal repair range | Boundary |
|---|---:|---|
| Simple objective distinction or strategy cue | 1–3 min | One explanation/contrast, then retry |
| Listening-recognition contrast | 2–5 min | Short focused audio work, not repeated full passages |
| Writing task/rubric or language repair | 3–8 min | One or two high-impact dimensions only |
| Speaking production/interaction repair | 3–8 min | One behavior/phrase pattern plus oral rehearsal |
| 10-minute Quick session | 1–3 min | Preserve enough time for a valid fresh check |
| 25-minute dominant coaching block | 2–6 min normally | Repair should not consume the whole block |
| Need exceeds 8 min | End or convert to a dedicated future coaching block | Do not disguise a broad lesson as micro-repair |

The time range is a product default, not a promise that every learner moves at the same pace. Accessibility accommodations may increase elapsed time without changing the intended scope.

### 6.2 Retry and cycle cap

The normal loop permits:

- one fresh equivalent retry after repair;
- one short re-diagnosis after a failed or partial retry;
- one additional micro-adjustment and second fresh check only when the cause remains defensible, the total repair scope stays within the eight-minute boundary, and the learner is not showing fatigue or frustration.

After two failed fresh checks in the same episode, or once the repair boundary is reached:

- stop the loop at a meaningful boundary;
- record what remains unresolved or support-dependent;
- adjust the working difficulty or prerequisite if appropriate;
- schedule later practice/transfer;
- do not continue until the learner guesses correctly.

A successful check at a deliberately easier prerequisite proves that prerequisite only. The original higher-difficulty weakness stays open.

## 7. Retry Equivalence and Anti-Memorization Contract

### 7.1 What must stay equivalent

The immediate retry should preserve enough of the problem to test the repaired capability:

- primary skill node or diagnosed cause;
- direct evidence lane;
- task mechanism or reasoning pattern;
- approximate working difficulty;
- intended rubric dimension;
- relevant assistance/timing target;
- quality and TELC-relevance band.

Keeping the immediate task mechanism stable helps isolate whether the repair worked.

### 7.2 What must change

The retry must change all answer-bearing surface content and normally several contextual features:

- text, sentence, audio, communicative prompt, or partner turn;
- names, dates, places, objects, numbers, or required details;
- correct answer position and distractor wording for objective tasks;
- wording and synonym/paraphrase path;
- speaker, recording, or announcement details for Listening;
- scenario, content points, recipient, or constraint for Writing;
- partner proposal, conflict, follow-up, or topic details for Speaking.

The retry must not be:

- the same item with choices reordered;
- a near-paraphrase whose answer is obvious from the explanation;
- a blank filled with the exact model phrase just shown;
- the original Writing/Speaking response after a model answer;
- content recently exposed elsewhere in the session;
- an easier task silently presented as proof of the original claim.

### 7.3 Three transfer levels

| Level | Purpose | Variation |
|---|---|---|
| **Immediate fresh check** | Show same-session responsiveness/initial transfer | Same task mechanism and lane; new surface content and answer |
| **Delayed transfer** | Show the repair remained available without answer exposure | New task on another occasion; change topic/details and may vary task form |
| **Broader/target transfer** | Support Reliable, Target-evidenced, or repaired status | New context/form and, when relevant, less assistance or realistic timing |

Stage 21 owns exact content-generation, deduplication, and anti-repetition mechanisms. The product requirement is that content metadata or review must be able to distinguish same-item repetition, near-duplicate content, fresh equivalent content, and broader transfer.

## 8. Retry Success and Failure Criteria

### 8.1 Universal immediate-success criteria

An immediate retry passes only when:

1. the task is valid and fresh enough;
2. it directly tests the repaired capability in the observed lane;
3. the learner meets the answer or B1-sufficient rubric requirement for that targeted dimension;
4. the support/timing condition is recorded and is no more answer-bearing than the claim allows;
5. no technical or evaluator uncertainty invalidates the dimension;
6. success is not merely copying the model or repeating the revealed answer.

The state recorded is **responsive to repair** or **same-session fresh transfer passed**. It is not Repaired, Resolved, Stable, or Target-evidenced by itself.

### 8.2 Modality-specific immediate success

| Modality | Immediate retry success |
|---|---|
| Objective question | Correct response on fresh equivalent content. When guessing is a material risk, the learner also identifies the decisive cue or succeeds on a second compact equivalent check |
| Listening | Correctly extracts the targeted gist/detail from new audio under the declared playback/speed condition; transcript or answer-bearing support is removed |
| Writing | A new prompt or compact new response demonstrates the targeted rubric behavior, such as covering all required points or using the repaired structure spontaneously; unrelated minor errors do not cancel targeted success |
| Speaking | A new oral response/exchange demonstrates the targeted behavior intelligibly; interaction repair requires an actual new partner turn, not a monologue or typed answer |

### 8.3 Partial, assisted, and failed outcomes

- **Partial success:** update only the supported dimension; schedule another fresh check.
- **Success with language support:** record guided transfer, not independent transfer.
- **Success after model exposure on essentially the same answer:** weak repair evidence only.
- **Failure for the same cause:** one micro-adjustment may follow within the loop cap.
- **Failure for a different cause:** re-diagnose; do not claim the repair failed when a new blocker caused the result.
- **Failure at unreachable difficulty:** step down to a prerequisite; retain the original target.
- **Invalid retry:** exclude it and offer a replacement only if the session can still end responsibly.
- **Repeated failure:** end the loop, preserve uncertainty/support need, and schedule a better-sized future block.

### 8.4 When a weakness is actually repaired

Stage 05 remains authoritative:

- at least one successful delayed fresh-transfer opportunity normally 1–3 days later moves a repairing weakness toward Stabilizing;
- Repaired normally requires at least three successful fresh relevant opportunities across three occasions spanning at least 14 days, a majority unassisted, no recurrence after the last repair, and direct success in the original lane;
- high/pass-critical target-condition weaknesses also require a recent success under the relevant B1/target condition;
- a later retention opportunity around 30–60 days supports Resolved.

Stage 07 supplies the immediate evidence episode and schedules the first delayed return. It does not weaken those gates.

## 9. Modality Adaptations

### 9.1 Objective questions

This family includes multiple choice, matching, cloze, true/false, short deterministic responses, and other reviewed answer-key tasks in Reading and Language Elements.

| State | Product behavior |
|---|---|
| Observe | State the task objective, format, working condition, and any allowed hints; use an unscored format example only when needed |
| Attempt | Withhold correctness; record answer, hint use, timing, and completeness |
| Diagnose | Score deterministically; show the decisive text/context cue; use item metadata or one contrast to distinguish vocabulary, grammar, misunderstanding, distractor strategy, or attention slip |
| Repair | Give one distinction, practical rule, cue-marking behavior, or short controlled choice |
| Retry | New item with the same node/reasoning pattern, new surface content, rotated correct position, and fresh distractors |
| Remember | Save task/node evidence, cause confidence, repair responsiveness, and due transfer if needed |

Rules:

- The answer key establishes outcome, not automatically root cause.
- A correct answer normally ends the loop. Check reasoning only when the evidence claim is high-value and guessing is plausible.
- Deterministic feedback is the default. Routine objective items do not justify AI calls.
- Ambiguous or contested items are invalidated or broadened; the learner is not penalized.

### 9.2 Listening

| State | Product behavior |
|---|---|
| Observe | State gist/detail goal, playback rule, speed/support condition, and whether note-taking is allowed |
| Attempt | Play the full valid clip under the declared rules; record replay, speed, response, and technical quality |
| Diagnose | Separate unknown meaning from sound recognition, missed detail/negation, speaker correction, instruction misunderstanding, attention, or strategy |
| Repair | Use only the relevant excerpt, transcript contrast, sound/number contrast, or listening cue; slowed audio is allowed as recorded learning support |
| Retry | Use new audio with comparable target information, fresh wording/details, and a declared playback/speed condition; remove the transcript and answer-bearing cue |
| Remember | Save direct audio-lane evidence, playback dependence, technical validity, cause confidence, and the next audio transfer check |

Rules:

- Seeing the word in a transcript and understanding it after the attempt can distinguish Listening recognition from Vocabulary.
- A written recognition quiz cannot prove a Listening repair.
- A failed audio block caused by playback or recording quality is invalid, not a learner mistake.
- Exam-mode replay rules are preserved in measured attempts. Learning repair may temporarily alter speed/replay, but target transfer later restores realistic conditions.
- Reviewed/pre-generated audio is preferred to live per-attempt generation.

### 9.3 Writing

| State | Product behavior |
|---|---|
| Observe | Show purpose, recipient/register, explicit content points, time/length guidance, and allowed scaffolding |
| Attempt | Capture the learner’s own message; preserve draft/submission, time mode, assistance, and completeness |
| Diagnose | Evaluate task fulfillment first, then communicative clarity, organization/register, vocabulary, and grammar control; select at most one or two point-relevant repair targets |
| Repair | Use a content-point plan/check, one practical structure or phrase distinction, or a short guided revision; avoid wholesale rewriting |
| Retry | Prefer a fresh compact prompt or new paragraph/message segment that requires the same rubric behavior; a revision of the original is controlled practice only |
| Remember | Save supported rubric dimensions, evaluator/confidence, assistance/model exposure, immediate transfer, and future full-task verification |

Rules:

- A full second message is not required after every error. The retry may be a compact new response if it directly tests the target dimension.
- A later complete fresh task is required before generalizing to full Writing performance or target conditions.
- Minor non-native errors that preserve B1-sufficient communication do not automatically become mistake-memory priorities.
- A model answer is teaching material, not learner evidence.
- AI is valuable for rubric evaluation and natural-language diagnosis, but explicit content-point checks, length, submission, timing, and known deterministic rules should be handled without AI first.
- If evaluation is pending or uncertain, save the response and show limited/pending feedback rather than inventing a grade.

### 9.4 Speaking

| State | Product behavior |
|---|---|
| Observe | Show the scenario, role, preparation time, task/interaction goal, recording/partner rules, and allowed phrase support |
| Attempt | Capture an actual oral response or exchange; preserve audio quality, transcription confidence, timing, assistance, and partner turns |
| Diagnose | Prioritize task fulfillment, comprehensibility, fluency/continuity, interaction, and point-relevant language control; distinguish speaking production from interaction |
| Repair | Rehearse one phrase behavior, repair strategy, intelligibility contrast, response pattern, or interaction move; keep it oral where the target is oral |
| Retry | Use a new oral prompt or exchange with a different proposal/constraint/follow-up; interaction success requires a new partner turn |
| Remember | Save direct oral/interaction evidence, evaluator confidence, technical flags, support/model exposure, transfer result, and due oral check |

Rules:

- Typed rehearsal may support learning but never substitutes for direct oral evidence.
- A monologue cannot prove an interaction repair.
- Pronunciation is judged by intelligibility and communicative impact, not accent similarity.
- Transcription failure or noisy audio cannot be interpreted as poor German.
- A fixed/pre-recorded partner can support many routine interactions. A live generative partner is justified only when genuine adaptive exchange materially tests the target behavior.
- Speaking feedback should target at most one or two high-impact behaviors per loop.

## 10. AI Versus Deterministic Feedback

### 10.1 Decision principle

**Use the cheapest method that can make the required coaching decision responsibly.**

AI is not used to make the coach feel conversational. It is used when the learner response is open-ended or the distinction cannot be evaluated reliably from reviewed keys, task metadata, explicit rules, or structured learner interaction.

### 10.2 Capability matrix

| Decision | Preferred default | When AI adds material value | Fallback |
|---|---|---|---|
| Objective answer correctness | Deterministic reviewed key | Rarely; only genuinely open semantic alternatives | Mark ambiguous/invalid or request reviewed resolution |
| Objective root cause | Item metadata, response pattern, one deterministic contrast | Ambiguous high-impact cause with no cheap clarifier | Keep broad/unresolved and collect fresh evidence |
| Listening selected-answer scoring | Deterministic key | Not needed for routine scoring | Invalidate ambiguous content |
| Listening recognition diagnosis | Transcript/audio contrast and metadata | Complex free response or uncertain productive explanation | Broader cause and another audio task |
| Writing content-point coverage | Explicit checklist plus evaluator | AI helps with paraphrased/implicit coverage | Ask learner self-check or retain low confidence |
| Writing rubric evaluation | Deterministic surface checks first, then one structured low-cost evaluation | Meaning, clarity, register, organization, and cause attribution | Partial deterministic feedback, pending/low-confidence dimensions |
| Speaking transcription | Low-cost speech-to-text when needed | Needed to inspect language content, not sufficient alone | Preserve audio if allowed and mark unsupported dimensions pending |
| Speaking rubric/interaction | Structured low-cost evaluation using audio/transcript/turn data | Comprehensibility, fluency, response relevance, interaction | Limited observable feedback and another sample |
| Repair selection | Reviewed repair map from diagnosed node/cause | Unusual productive pattern not covered by reviewed repair | Broader safe repair or defer |
| Feedback wording | Reviewed templates from structured evidence | Selected nuanced productive feedback | Template with explicit uncertainty |
| Retry content | Reviewed/pre-generated equivalent pool | Batch generation to expand weak pools; rare live generation with QA | Broader reviewed equivalent or defer |
| Remember/state updates | Deterministic learner-model and Mistake Memory rules | Never needs a separate routine call | Lower confidence / pending evaluation |

### 10.3 Invocation and confidence rules

- Objective activities should normally incur **zero per-attempt AI calls**.
- A submitted Writing or Speaking response should normally use at most **one batched low-cost evaluation** returning all supported rubric dimensions, diagnosis confidence, and feedback inputs needed by the learner model.
- Do not call another model merely to choose a repair, update memory, produce Remember text, or rank tomorrow’s plan.
- A second/higher-quality evaluation is reserved for a new valid productive sample that materially affects a mock, readiness, or ready-to-book decision and whose first evaluation is below the required confidence or contradictory.
- Reuse stored structured evaluations until new learner evidence changes the decision.
- AI feedback must identify which dimensions it can support and with what confidence.
- Low confidence produces a broad diagnosis, another sample, or a pending state—not a fine-grained known weakness.
- Generated repair/retry content should preferably be batched, cached, reviewed, and reused across learners. Real-time generation is not the normal path.
- If AI is unavailable, the loop remains usable for objective tasks and can provide partial/pending productive feedback without fabricating readiness evidence.

### 10.4 Quality threshold

AI is valuable only when it can reliably distinguish the decision that changes coaching, such as:

- whether a Writing content point was meaningfully covered;
- whether a request is comprehensible and appropriately directed;
- whether a Speaking response addressed the partner’s alternative;
- whether the cause is a specific repeated grammar pattern or only a broader production shortfall.

When it cannot support that distinction, the product must preserve uncertainty. Exact evaluator benchmarks and monitoring belong to Stages 09–13 and 26.

## 11. Edge Cases / Failure and Uncertainty Handling

| Situation | Loop behavior |
|---|---|
| Learner is far below the target task | End repeated failure, repair a reachable prerequisite, retry at that level, and keep the target-condition gap explicit |
| Learner already knows the pattern | Compress Diagnose and skip Repair/Retry unless a stronger evidence condition is genuinely needed |
| Correct by likely guess | Use a short decisive-cue check only when the claim matters; otherwise keep confidence appropriately limited |
| Several possible causes | Use one minimal clarifying contrast or remain unresolved |
| Multiple errors in one productive response | Select one or two highest-impact/recurring targets; record other supported observations without turning the loop into a full lesson |
| Learner disputes feedback | Show the concrete evidence and allow a fresh check; lower confidence when the alternative is plausible |
| Same content is accidentally served | Mark it repeated/exposed and reduce or exclude independence; replace it when feasible |
| No equivalent retry content exists | End honestly with transfer pending; use a broader reviewed task later |
| Learner uses a hint on retry | Record guided transfer; do not claim independent success |
| Repair needs more than eight minutes | Convert it into a future focused coaching block; preserve the current episode |
| Learner stops after repair | Save exposure and schedule a fresh transfer; no completion penalty |
| Session interrupted after model exposure | Resume with a fresh equivalent task, not the exposed original |
| Timed task is paused | Continue as useful practice with the pause recorded; do not call it continuous exam-timed evidence |
| Productive evaluation arrives later | Reopen the pending Diagnose state, provide feedback, and offer/schedule repair without altering original attempt conditions |
| Evaluators disagree | Lower confidence, preserve provenance, and use one higher-value fresh sample or high-stakes reevaluation |
| Technical audio/input failure | Exclude the affected evidence and offer a valid retry/fallback without diagnosis |
| Accessibility support is used | Treat non-answer-bearing access support separately; reduce ability evidence only when support changes the tested capability |
| Microphone unavailable | Keep oral evidence missing; typed work may be learning support only |
| Offline/AI unavailable | Use cached objective and reviewed repair content; save productive work as pending if it cannot be evaluated responsibly |
| Mock or exam practice | Batch the loop after the measured block; never reveal answers or repairs between measured items |
| Learner wants to continue after repeated failure | Offer a future focused block or a reachable prerequisite rather than an endless same-session drill |
| Error is B1-acceptable | Give optional feedback only if useful; do not create a durable weakness without exam/rubric impact |

## 12. Representative End-to-End Examples

### 12.1 Multiple-choice Reading restriction

1. **Observe:** “Choose the notice that allows a weekday visit. No hint; about two minutes.”
2. **Attempt:** The learner chooses the wrong notice.
3. **Diagnose:** The text was found, but “außer dienstags” was overlooked. Medium-confidence restriction/comprehension cause.
4. **Repair:** Contrast “nur dienstags” and “außer dienstags,” then apply one checking cue.
5. **Retry:** A new set of notices uses different places and “nur werktags”; correct position and distractors change.
6. **Remember:** The learner succeeds without a hint. Record same-session fresh transfer, not repaired status; schedule the first delayed check in 1–3 days if the weakness is known.

### 12.2 Listening number recognition

1. **Observe:** One new announcement, normal working speed, one replay allowed.
2. **Attempt:** The learner selects 50 instead of 15.
3. **Diagnose:** The learner recognizes the correct number in the transcript, supporting a listening-recognition distinction rather than unknown vocabulary.
4. **Repair:** Short contrastive audio for fünfzehn/fünfzig.
5. **Retry:** A different speaker and announcement use a new number pair at normal working speed without transcript.
6. **Remember:** Correct with one replay. Record guided/working-condition transfer and keep target first-play evidence pending.

### 12.3 Writing content-point strategy

1. **Observe:** Write a short message covering three explicit points in five minutes.
2. **Attempt:** The message is understandable but omits one required point.
3. **Diagnose:** Language is adequate; the likely blocker is required-point checking, not general grammar.
4. **Repair:** Build a three-point micro-plan and a ten-second final check.
5. **Retry:** Write a compact new message for a different recipient with three new content points.
6. **Remember:** All points are covered. Record same-session strategy transfer; schedule a later complete fresh message before generalizing Writing performance.

### 12.4 Speaking interaction

1. **Observe:** Respond to a partner’s proposal, disagree politely, and offer an alternative.
2. **Attempt:** The learner gives a relevant monologue but does not respond to the partner’s constraint.
3. **Diagnose:** Interaction behavior is the primary shortfall; speech is otherwise comprehensible.
4. **Repair:** Rehearse one acknowledge-and-alternative pattern orally.
5. **Retry:** A new partner prompt proposes a different activity and introduces a new constraint.
6. **Remember:** The learner acknowledges and offers an alternative. Record direct same-session interaction transfer; a later fresh exchange is still required for stabilization.

## 13. Relationship to Other Bestehen Stages

- **Stage 03 — Initial Diagnostic:** the diagnostic itself preserves clean measurement; its first recommended session demonstrates this full loop.
- **Stage 04 — Learner Model:** receives attempt conditions, evidence strength, evaluator quality, retry independence, and derived updates.
- **Stage 05 — Mistake Memory:** remains authoritative for episode grouping, weakness promotion, delayed transfer, repair, resolution, and reopening.
- **Stage 06 — Daily Coaching Engine:** selects and time-bounds the dominant loop; Stage 07 defines what happens inside it.
- **Stage 08 — A1→B1 Progression:** defines the detailed assistance/difficulty ladder used by Observe, Repair, and Retry.
- **Stages 09–13 — Skill Coaching:** must refine task-specific diagnoses, repairs, rubrics, and valid retry opportunities without breaking the common loop.
- **Stage 14 — Review:** schedules delayed transfer and retention; normal practice may satisfy a due check when it provides valid fresh evidence.
- **Stage 15 — TELC Readiness:** weights evidence by realism and must not treat immediate repair responsiveness like stable target-condition evidence.
- **Stage 16 — Mock Exams:** batches diagnosis/repair after measured sections and supplies strong fresh evidence without between-item coaching.
- **Stage 17 — Ready to Book:** uses retained, realistic evidence and unresolved pass-critical weaknesses; one successful retry cannot clear a booking gate.
- **Stage 18 — Coach Personality:** refines exact language for diagnosis, uncertainty, failure, and Remember summaries.
- **Stage 19 — Information Architecture:** may combine states into screens while preserving clear attempt boundaries, support context, and evidence consequences.
- **Stage 20 — Progress and Motivation:** may recognize successful transfer and resolved weaknesses as earned progress, not reward routine clicks.
- **Stage 21 — Content Strategy:** supplies reviewed fresh-equivalent variants, relationship/freshness metadata, answer validation, and anti-repetition controls.
- **Stage 22 — Corpus → App Contract:** supplies task patterns, stable nodes, relevance, difficulty, distractor patterns, and equivalence intelligence.
- **Stage 24 — Account/Data:** defines retention for drafts, audio, responses, evaluation, and episode links.
- **Stage 25 — Accessibility/Device:** determines which access supports preserve the intended evidence condition and how modality fallback works.
- **Stage 26 — Analytics:** measures diagnosis quality, repair duration, retry validity, immediate transfer, delayed retention, false repair claims, and cost.
- **Stage 27 — Cost Boundaries:** sets portfolio-wide AI limits; routine objective loops remain deterministic.

### Cross-stage guardrails

Later stages may tune time ranges, labels, rubrics, and evaluator thresholds, but they must preserve:

- six semantic loop states with optional UI compression;
- a clean attempt before answer-bearing repair when new evidence is claimed;
- outcome separate from cause and explicit diagnosis uncertainty;
- narrow repair with a normal two-to-six-minute target and eight-minute boundary;
- fresh equivalent retry rather than same-answer repetition;
- direct evidence in the original modality/lane;
- same-session retry success as responsiveness/initial transfer, not retained repair;
- delayed fresh transfer and realistic evidence for stronger claims;
- deterministic routine objective feedback and bounded AI use for productive/ambiguous work;
- no learner penalty for technical failure, assistance, stopping, or override.

## 14. Cost Notes

The common loop itself should have negligible recurring cost.

### Preferred low-cost default

- deterministic objective scoring and answer validation;
- reviewed task metadata and repair maps for common diagnoses;
- template-driven Diagnose and Remember copy;
- pre-generated/reviewed fresh-equivalent pools;
- deterministic state transitions, evidence updates, and due scheduling;
- cached/pre-generated audio;
- one existing batched low-cost evaluation for a submitted Writing/Speaking response when needed;
- no separate call for repair selection, retry ranking, memory update, or summary wording.

### Premium path

A higher-quality evaluation may be used only for a valid new productive sample when cheaper evaluation cannot support a high-impact mock, readiness, or ready-to-book decision. It should run once, return structured reusable results, and never override deterministic validity or evidence rules.

### Cheaper fallback

Use a broader diagnosis, reviewed repair, another fresh sample, pending feedback, or lower confidence. Cost is not a reason to fabricate certainty, skip oral/productive evidence indefinitely, or serve low-quality generated content.

The main recurring-cost impact of Stage 07 is therefore limited to productive evaluation already required by Writing/Speaking. Objective and routine Listening loops should add no meaningful AI cost.

## 15. Decisions Made

1. Finalized **Observe → Attempt → Diagnose → Repair → Retry → Remember** as six semantic states with optional UI compression.
2. Reconciled Observe as both coach-side Corpus/learner evidence selection and learner-side pre-attempt orientation without solution exposure.
3. Defined the purpose, working UI, state transitions, and evidence produced by every state.
4. Defined when states may be compressed, skipped, deferred, or batched, including diagnostic, mock, exam-mode, pending-evaluation, and short-session behavior.
5. Set repair at normally 2–6 minutes, with an eight-minute boundary and a limited retry/re-diagnosis cycle.
6. Defined fresh-equivalent retry invariants, required variation, anti-memorization exclusions, and immediate/delayed/target transfer levels.
7. Defined universal and modality-specific retry success, partial/assisted/failure behavior, and the boundary between responsiveness and actual repaired status.
8. Defined the full loop for objective questions, Listening, Writing, and Speaking.
9. Defined deterministic-first evaluation, routine AI caps, productive-sample triggers, premium escalation, and honest fallbacks.
10. Defined interruption, technical failure, accessibility, uncertainty, low-proficiency, repeated-failure, and learner-skip behavior.
11. Defined modality examples and the state/evidence contract required by later design, content, readiness, and analytics stages.
12. Kept the loop affordable by requiring reusable content/repair assets and no routine premium calls.

## 16. Open Questions / Deferred Decisions

### Open owner questions

**None.** The core learning loop can be responsibly defined from the existing product decisions.

### Deferred product decisions

- exact visual screen composition, navigation, animation, and final learner-facing labels — Stages 18–19;
- calibrated assistance/difficulty transitions — Stage 08;
- final TELC task inventory, scoring rubrics, and modality-specific evaluator quality thresholds — Stages 09–13;
- exact adaptive review intervals and due-window behavior — Stage 14;
- exact readiness contribution and target-condition requirements — Stage 15;
- mock feedback timing, section boundaries, and retest rules — Stage 16;
- final generated-content QA, equivalence measurement, and anti-repetition windows — Stage 21;
- raw response/audio retention and privacy behavior — Stage 24;
- accessibility accommodations that preserve or change evidence claims — Stage 25;
- empirical repair-duration, retry-success, diagnosis-quality, and cost thresholds — Stage 26;
- storage, state-machine implementation, algorithms, services, and model/provider selection — post-shaping architecture work.

The duration ranges, retry cap, and AI invocation rules are implementable product defaults. They should be recalibrated from learner transfer, frustration, productive-evaluation quality, mock outcomes, and actual cost—not from completion rate alone.

## 17. Definition of Done Check

- [x] Finalize **Observe → Attempt → Diagnose → Repair → Retry → Remember**.
- [x] Define each step in the UI.
- [x] Define when steps may be skipped.
- [x] Define expected repair duration.
- [x] Ensure retry uses fresh equivalent content.
- [x] Define success criteria for a repaired weakness.
- [x] Define the loop for objective questions.
- [x] Define the loop for Listening.
- [x] Define the loop for Writing.
- [x] Define the loop for Speaking.
- [x] Define how assistance is offered without turning every activity into a full lesson.
- [x] Define state transitions and evidence produced by each step.
- [x] Define AI versus deterministic feedback and cost-aware fallbacks.
- [x] Include modality examples and failure/uncertainty handling.
- [x] Preserve all prior learner-model, mistake-memory, and daily-coaching evidence boundaries.

**Stage 07 is complete when every activity can be storyboarded as one consistent coaching loop, can state what evidence each state creates, and can prove transfer without confusing memorization or immediate success with retained readiness.**
