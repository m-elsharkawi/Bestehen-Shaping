# Bestehen / App — Stage 13: Speaking Coaching

> **Status:** Stage 13 product shaping — speaking experience and interaction model defined; evaluation/readiness/cost completion follows in this stage
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Speaking promise:** Rehearse the actual communicative work of TELC B1 with enough scaffolding to start around A1, then remove support until the learner can speak, react, negotiate, and complete all three oral tasks under credible exam conditions.

## 1. Purpose and Scope

This document defines the complete learner-facing Speaking coaching experience for Bestehen / App. Speaking must feel like rehearsal with an exam coach and a useful partner, not like open-ended chatbot conversation and not like pronunciation imitation.

The product has to solve two related but distinct problems:

1. help the learner **produce understandable B1 German** for the task at hand; and
2. help the learner **interact with another person**: listen, respond, ask, negotiate, repair, share the floor, and move the task toward a useful outcome.

Those are not interchangeable. A good monologue can demonstrate speaking production but cannot prove interaction. A typed response can help the learner prepare language but cannot provide oral evidence. A transcript can help diagnose language, but it is not the learner's voice and must not become the sole source of truth for pronunciation or fluency.

Stage 13 applies the existing **Observe → Attempt → Diagnose → Repair → Retry → Remember** loop and the P0→P4 progression model to the current TELC B1 oral examination. It defines:

- all three target Speaking parts and the skills behind them;
- solo and partner practice for each part;
- AI-partner roles and turn-taking behavior;
- voice capture and transcript behavior;
- preparation and timing rules;
- planning-together scenarios and interaction contracts;
- the product boundary between ordinary asynchronous/turn-based speech and later real-time voice;
- the evidence conditions that later evaluation, oral readiness, mocks, content, privacy, accessibility, and analytics stages must preserve.

The second half of this stage defines the detailed evaluation rubric, accent fairness, feedback/repair, oral-readiness evidence, uncertainty handling, and cost-control policy.

This is product shaping, not implementation architecture. It does not choose a speech-to-text provider, speech model, TTS vendor, audio codec, streaming protocol, database, voice-activity algorithm, or final readiness formula.

### In scope

- current TELC B1 oral task families;
- lower-difficulty P0–P4 Speaking variants;
- solo practice and genuine interactive practice;
- fixed/prerecorded and adaptive AI-partner behavior;
- microphone/voice-response product requirements;
- transcript display and uncertainty;
- preparation notes, task timing, and full oral simulation behavior;
- turn taking, partner prompting, silence, rescue, and interruption boundaries;
- original scenario families for discussion and planning;
- oral evidence classification by partner type and realism.

### Out of scope

- final calibrated oral-readiness formula and minimum evidence counts — Stage 15;
- complete mock cadence and cross-section mock UX — Stage 16;
- ready-to-book thresholds — Stage 17;
- final coach copy system — Stage 18;
- final screen hierarchy — Stage 19;
- generalized content-generation QA and anti-duplication — Stage 21;
- final Corpus → App payload/API — Stage 22;
- audio retention, deletion, export, and privacy implementation choices — Stage 24;
- accessibility equivalence and accommodations for target-condition evidence — Stage 25;
- evaluator-bias measurement and real-outcome calibration — Stage 26;
- model/vendor/streaming/storage architecture.

---

## 2. Inputs / Existing Decisions

Stage 13 preserves the project overview, identity, and App Stages 01–12:

- Bestehen is a calm, direct, evidence-based **personal German exam coach**.
- TELC B1 is the only launch target. Cheap seams for later exams are welcome only where they do not weaken TELC B1.
- A learner may begin around A1. The task stays exam-shaped while language load, scaffolding, partner complexity, timing, and independence change.
- Readiness is the primary progress concept and written/oral pass risk stays separate.
- Speaking production and **interactive speaking** are separate direct-evidence lanes in the learner model.
- Another modality cannot initialize Speaking mastery. Typed rehearsal never becomes oral evidence.
- The Stage 03 diagnostic already uses a cheap 45–90 second oral sample plus a fixed two-turn planning exchange. It deliberately leaves sustained interaction and full oral readiness weakly evidenced.
- Speaking capability already includes task fulfillment, comprehensibility, fluency, vocabulary, grammar, interaction, proposing/agreement/disagreement, negotiation, repair strategies, organization, preparation-time use, and timing.
- Pronunciation is judged through **intelligibility and communicative impact**, not similarity to a native accent.
- Poor audio, transcription failure, or evaluator uncertainty cannot be converted into poor learner performance.
- Mistake Memory records production/interaction shortfalls only when attribution is defensible; a technical failure is not a learner mistake.
- The Daily Coaching Engine must protect missing/stale oral evidence and may devote nearly a full 25-minute session to an interactive Speaking block rather than favor cheaper objective skills.
- Stage 07 already requires Speaking repair to remain oral when the target is oral, normally emphasize only one or two high-impact behaviors, and use a fresh partner turn for interaction retry.
- A fixed/prerecorded partner is preferred for routine interactions when it can test the behavior; a live generative partner is justified only when adaptive exchange adds material value.
- Stage 08 uses **P0 Supported Foundation → P1 Guided A2 → P2 A2/B1 Bridge → P3 Independent B1 Training → P4 Target Conditions**, by task family rather than one global level.
- Phrase banks, sentence starters, planning frames, and other answer-bearing production supports progressively fade. Their use before submission remains attached to the evidence.
- P4 measured attempts use exact target constraints and defer coaching until measurement ends.
- Real/reference exams define what must be rehearsed. Learner-facing practice should normally be original where reuse rights are unclear.
- Recurring premium AI calls must earn their cost; reviewed content, deterministic checks, batching, caching, and cheaper models are preferred when quality is sufficient.

No earlier product decision is reversed. Stage 13 makes the Speaking behavior that Stages 03, 04, 07, and 08 deliberately left incomplete concrete.

---

## 3. Current TELC B1 Speaking Target

### 3.1 Verification and versioning rule

The target was rechecked on **19 August 2026** against the current official telc product page and the official `Zertifikat Deutsch / telc Deutsch B1 — Übungstest 1`.

The current official product page continues to describe:

- **3 Speaking parts**;
- approximately **15 minutes** for the oral examination;
- normally **2 participants**;
- **20 minutes preparation time**;
- a strong emphasis on direct exchange between the participants.

The detailed official model test describes the three parts as:

| ID | Target part | Approx. model-test time | Core communicative job | Model-test maximum |
|---|---|---:|---|---:|
| **S1** | **Einander kennenlernen** / Get to know each other | ~3 min | Talk about oneself, ask the partner questions, respond naturally, and handle an occasional additional prompt | 15 |
| **S2** | **Über ein Thema sprechen** / Discuss a topic | ~6 min | Convey the viewpoint on one's own input, understand the partner's different input, exchange opinions and experience, and react to the partner | 30 |
| **S3** | **Gemeinsam etwas planen** / Plan something together | ~6 min | Propose, justify, react, negotiate alternatives, decide what will be done, and agree who does what | 30 |

The model-test oral total is **75 points**, or 25% of the overall 300-point exam. The same model test states that the written and oral components have separate 60% pass requirements, making **45/75** the oral minimum in that blueprint. Final readiness logic remains Stage 15's responsibility.

Official sources used for this verification:

- `https://www.telc.net/sprachpruefungen/deutsch/zertifikat-deutsch-telc-deutsch-b1/`
- `https://shop.telc.net/media/catalog/product/file/2/0/20201225_5061-b00-010301_web.pdf`

**Product rule:** exact part names, timings, point values, task mechanics, and preparation rules are **versioned target knowledge**. The current telc page confirms the high-level three-part/15-minute/20-minute-preparation shape; the detailed downloadable model test remains the launch blueprint for part mechanics and rubric behavior. Before a task is labelled **P4**, a full Speaking simulation is called TELC-realistic, or the App converts performance into official-aligned points, the current approved blueprint must be revalidated.

### 3.2 Preparation behavior in the current model test

The detailed model test gives participants all oral task sheets for **20 minutes of preparation**. They may make notes on separate provided sheets and take those notes into the oral exam, but should not simply read them aloud. Participants do not prepare together and do not use dictionaries, phones, or other aids during that preparation.

Bestehen uses that behavior as the P4 launch simulation contract. The App may offer much more scaffolding during training, but that scaffolding must not leak into target-condition evidence.

### 3.3 The official rubric remains the scoring anchor

The model-test rubric evaluates every Speaking part independently on four official criteria:

1. **Ausdrucksfähigkeit** — content-/role-appropriate expression, vocabulary, and realization of speaking intent;
2. **Aufgabenbewältigung** — participation in the conversation, discourse/compensation strategies, and fluency;
3. **Formale Richtigkeit** — syntax and morphology;
4. **Aussprache und Intonation** — pronunciation/intonation according to how deviations affect understanding.

Bestehen may expose finer coaching dimensions, but those dimensions must map back to this official anchor rather than pretend to be extra official TELC criteria. Detailed mapping and evaluation rules are defined later in this document.

---

## 4. Speaking Task Model

### 4.1 S1 — Get to know each other

**Target behavior:** reciprocal personal exchange, not a memorized self-introduction speech.

A strong S1 attempt normally demonstrates that the learner can:

- answer common personal questions with enough detail to sustain exchange;
- ask the partner relevant questions rather than wait passively;
- react to an answer with a short follow-up when natural;
- move among familiar topics such as home, family, learning German, work/study, languages, free time, or similar everyday domains;
- handle one unexpected but familiar follow-up without collapsing into a prepared script;
- remain understandable and reasonably continuous while using B1-sufficient language.

**Anti-pattern:** a flawless 60-second biography with no partner-directed behavior is not full S1 evidence. It supplies production evidence but weak interaction/task evidence.

### 4.2 S2 — Discuss a topic

**Target behavior:** exchange information and viewpoints from **different inputs**, then discuss the topic rather than deliver two independent mini-presentations.

A valid S2 task contains paired inputs about the same familiar/accessible topic, normally with meaningfully different positions or experiences. The learner should:

1. understand their own input;
2. explain its main view to the partner in their own words;
3. listen to the partner's different view;
4. state their own opinion and give a reason;
5. bring in personal or plausible experience where useful;
6. respond to the partner—agree, disagree, qualify, compare, ask, or follow up;
7. keep the exchange moving without needing the system to script every next sentence.

The partner must not reveal the learner's unseen counterpart input before the relevant exchange. S2 depends on genuine information difference.

### 4.3 S3 — Plan something together

**Target behavior:** jointly produce an actionable plan through negotiation.

A valid S3 scenario gives both speakers a shared goal and several dimensions that can be decided together. The learner should be able to:

- make concrete proposals;
- give simple reasons;
- ask the partner what they think;
- respond to a proposal rather than ignore it;
- agree, disagree politely, or partially agree;
- offer an alternative when a proposal does not work;
- negotiate practical constraints;
- divide responsibilities where relevant;
- converge on a shared plan rather than only list possibilities;
- summarize or confirm the resulting agreement when useful.

There is **no single correct plan**. The product evaluates the communicative process and whether a coherent agreement emerges, not whether the learner chooses a model answer.

---

## 5. P0 → P4 Speaking Progression

Speaking progression is tracked separately for **S1 personal exchange**, **S2 discussion**, **S3 planning**, and relevant fine-grained capabilities such as intelligibility or negotiation. A learner can be P3 in S1 but P1 in S3 interaction.

| Rung | Speaking experience | Partner behavior | Support | Timing/evidence claim |
|---|---|---|---|---|
| **P0 Supported Foundation** | One or two meaningful oral turns using concrete A1/early-A2 language | Fixed prompt/response, patient and predictable | Phrase bank, sentence starters, key vocabulary, planning frame visible | Open time; supported speech/response evidence only |
| **P1 Guided A2** | Short reciprocal exchange; simple opinion/reason; one planning choice | Mostly fixed but can choose among reviewed follow-ups | Selective starters and functional phrases; support on request grows | Soft turn/task targets; emerging independent oral use |
| **P2 A2/B1 Bridge** | Full B1 mechanism with controlled language load and several turns | Scenario-controlled partner with limited adaptive branches | Most support on request; phrase bank reduced | Generous part timers; B1-shaped interaction with recorded support |
| **P3 Independent B1** | Original B1-equivalent tasks and sustained exchange | Adaptive turn-based partner is normal for S2/S3; fixed partner still useful for drills | No default answer-bearing help; help in practice marks attempt assisted | Target-time probes and unassisted B1 evidence |
| **P4 Target Conditions** | Current verified TELC-equivalent 3-part oral behavior | Exam-role partner using target-like interaction, no coaching | Only target-permitted preparation notes; no phrase/model help in measured block | Exact verified prep/part conditions; readiness-grade evidence when technically/evaluatively valid |

### 5.1 Promotion is behavior-specific

Speaking does not move up because the learner has “finished” a phrase bank. Promotion requires direct evidence that the learner can perform the relevant behavior with less support.

Examples:

- S1 can lose sentence starters after the learner repeatedly answers and asks personal questions without them.
- S2 can move from fixed counter-opinions to adaptive discussion after the learner can reliably summarize an input and state a reasoned view.
- S3 can move from a visible proposal menu to open planning after the learner can independently propose, respond, and offer an alternative.
- A pronunciation support should fade when intelligibility is stable, even if grammar remains guided.

If a B1 exchange is unreachable, the coach steps down **one dimension**—language load, turn count, partner complexity, or support—rather than globally demoting Speaking.

---

## 6. Practice Modes

### 6.1 Mode A — Solo oral drill

**Decision:** Every Speaking part has a useful solo mode, but solo work is never presented as a substitute for interaction evidence.

Solo mode is valuable because it is cheap, immediate, lower-pressure, and suitable for repairs. It always captures **actual voice** when oral evidence is intended.

#### S1 solo

A sequence of reviewed prompts asks the learner to answer about familiar personal topics. At least some prompts require the learner to **formulate a question they would ask a partner** or add a follow-up to an imagined partner response.

Useful solo exercises:

- 20–40-second personal answer;
- answer + one reason/example;
- hear a simple partner statement and record a natural follow-up question;
- unexpected familiar follow-up to reduce memorized-introduction dependence.

Evidence: speaking production, task relevance, fluency, language, intelligibility. It does **not** establish sustained turn-taking.

#### S2 solo

The learner receives one original input card and records:

1. a short paraphrase of the input view;
2. their own opinion and reason;
3. a personal example/experience when appropriate;
4. a response to one or two **fixed recorded contrasting statements**.

The last step creates limited response evidence, but because the partner cannot truly react to the learner, full interactive mastery remains unproven.

#### S3 solo

The learner receives a planning goal and constraints, then records:

- an opening proposal;
- a reason;
- a response to a fixed counterproposal or constraint;
- an alternative;
- a final spoken summary of a plausible agreement.

This is excellent repair/preparation for planning language but is still bounded interaction evidence.

### 6.2 Mode B — Scripted/fixed partner rehearsal

**Decision:** A reviewed fixed/prerecorded partner is the **default low-cost interactive mode** for P0–P2, the diagnostic, targeted repairs, and many repeatable phrase/turn-taking drills.

The partner uses scenario-specific branches such as:

- neutral follow-up;
- agreement;
- disagreement;
- request for a reason;
- practical constraint;
- alternative proposal;
- clarification request.

The learner's response determines the branch only when that can be decided cheaply and reliably. A fixed partner must not pretend to understand arbitrary meaning it did not evaluate.

This mode can provide direct evidence of **responding to a real partner turn**, but its interaction confidence is bounded because partner adaptability and unpredictability are limited.

### 6.3 Mode C — Adaptive turn-based AI partner

**Decision:** Adaptive turn-based interaction is the normal high-value mode for P2/P3 S2 and S3 when the target behavior genuinely depends on the learner's previous utterance.

The AI partner acts as a **peer participant during the attempt, not as the coach**. It must:

- stay inside the assigned scenario, role, viewpoint, and difficulty;
- respond to what the learner actually said, not a generic script when meaning was recoverable;
- keep its turns short enough to preserve learner speaking time;
- ask natural follow-ups selectively rather than interrogating every turn;
- introduce at most the scenario's intended amount of friction/constraint;
- disagree or counterpropose when the task calls for negotiation, but not manufacture conflict solely to be “interesting”;
- let the learner initiate and steer part of the exchange;
- avoid teaching, correcting, translating, or supplying model language until the measured attempt ends;
- avoid silently simplifying its German below the declared rung;
- use natural B1-reachable partner language rather than showing off advanced German;
- preserve paired-input secrecy in S2;
- cooperate toward a decision in S3 rather than block convergence indefinitely.

The partner has a **scenario contract**, not unrestricted chatbot freedom. Its allowed goals, facts, preferences, hidden constraint(s), and escalation bounds are defined before the attempt so the resulting evidence remains interpretable.

### 6.4 Mode D — Target-condition partner simulation

P4 is a measured oral simulation. The partner behaves like a plausible exam peer, and the coach is absent from the interaction.

Requirements:

- target-like language and reciprocal behavior;
- no teaching or hints;
- no phrase suggestion during the attempt;
- no rescue that makes the learner's task easier than a normal counterpart unless the target role naturally permits a neutral conversation prompt;
- stable scenario facts and paired inputs;
- target preparation/timing contract;
- all feedback deferred until the measured block ends.

A generative partner is useful here for scenario variability, but **real-time full-duplex voice is not required for P4 validity by product definition**. Credible turn-based oral interaction can collect strong evidence if turns, pauses, timing, and partner behavior remain target-like. Real-time voice becomes a quality upgrade, discussed later in this document.

---

## 7. Turn-Taking and Partner Behavior

### 7.1 Default interaction model

**Decision:** The default Speaking experience is **clear turn-based voice**, not continuous always-listening conversation.

This gives the learner an obvious floor, prevents endpointing errors from masquerading as interruptions, keeps operating cost predictable, and still tests the core TELC behavior: listening to a partner, producing a relevant response, asking/following up, negotiating, and sharing turns.

The learner can end a turn explicitly. Automatic end-of-turn detection may exist, but the product must always provide a recovery/control when it cuts off too early.

### 7.2 Pauses

The partner must tolerate ordinary B1 planning pauses. It should not jump in after every hesitation, `äh`, reformulation, or short silence. Fluency evaluation may record disruptive pauses, but interaction behavior must not create the problem it later scores.

When silence is clearly sustained:

- **practice modes:** one neutral open prompt may restart the exchange; repeated rescue is recorded as support/interaction evidence, not hidden;
- **P4 simulation:** only target-like neutral conversational prompting is permitted. The system does not provide language, vocabulary, or answer-bearing clues.

### 7.3 Interruptions and overlap

Natural overlap can occur in real pair exams, but interruption handling is **not required for the first cost-controlled product**. The core launch experience may remain half-duplex/turn-based.

A later real-time voice upgrade may add:

- interruption/barge-in;
- short backchannels;
- overlapping starts;
- more natural floor transfer.

That upgrade is justified when it materially improves interaction/stamina realism or resolves a measured learner need. It must not become a prerequisite for ordinary S2/S3 practice merely because the technology exists.

### 7.4 Dominance and passivity

The partner should neither monopolize the exchange nor force an exact 50/50 word split.

The product watches for communicative behaviors instead:

- did the learner contribute without repeated prompting?
- did the learner create openings for the partner?
- did they respond to partner content?
- did they ask/follow up when useful?
- did they negotiate rather than deliver disconnected speeches?

If the AI partner itself dominates or fails to provide a fair opening, affected interaction evidence is invalid or lower-confidence; the learner is not penalized for partner failure.

### 7.5 Repair in conversation

Communication repair is a positive B1 strategy when used effectively. The learner may:

- ask the partner to repeat or clarify;
- paraphrase when a word is missing;
- self-correct while keeping the turn moving;
- check understanding;
- reformulate a proposal.

A self-correction is not automatically a grammar or fluency penalty. Only repeated/disruptive repair that materially harms task completion or understanding affects the relevant dimension.

---

## 8. Planning-Together Scenario Model

### 8.1 Scenario families

S3 practice uses original/reviewed familiar B1 scenarios such as:

- organizing a small event, celebration, meeting, or group activity;
- planning a day trip, visit, excursion, or local outing;
- helping a friend/classmate/neighbour with a practical task;
- organizing a course/class/community activity;
- planning transport, food, materials, invitations, tickets, or responsibilities for a shared goal;
- coordinating a simple project, appointment, or group decision.

The scenario bank should be broader than one recurring “party” template while remaining in familiar B1 domains.

### 8.2 Required scenario structure

Every S3 scenario conceptually defines:

- one shared objective;
- normally **4–6 negotiable dimensions** such as time, place, participants, transport, budget, food/materials, responsibilities, or sequence;
- facts both speakers know;
- optional partner preferences or one modest hidden constraint that creates a reason to react;
- several acceptable outcomes;
- an explicit convergence condition: a workable shared plan, not a single canonical answer;
- functional-language opportunities such as propose, justify, ask, agree, disagree, offer alternative, assign task, confirm.

The task must be solvable without obscure cultural knowledge or a single “smart” solution.

### 8.3 Difficulty controls

- **P0:** 2–3 concrete decisions, visible options, one fixed counterproposal.
- **P1:** 3–4 decisions, simple open proposals, one clear constraint.
- **P2:** 4–5 decisions, less language support, more than one reasonable trade-off.
- **P3:** full open B1 planning with independently generated proposals and varied partner response.
- **P4:** current target-like scenario length, instructions, notes, timing, and interaction behavior.

Increasing difficulty means adding authentic negotiation load, not making the partner obstinate or the scenario artificially complicated.

---

## 9. Voice Input Requirements

### 9.1 Voice is required for oral evidence

**Decision:** A valid Speaking evidence attempt requires the learner's actual voice. Typed answers, selected phrases, or a text chat can support preparation/repair but must never initialize or improve oral mastery as though speech were observed.

The product must support:

- microphone permission requested **at the point of the first Speaking action**, not as a generic onboarding wall;
- a quick input check before a meaningful measured attempt;
- clear indication that audio is being captured;
- actual response duration and turn boundaries;
- association of each learner turn with the scenario/partner turn, preparation condition, support used, and timing mode;
- a learner-controlled way to end/recover a turn if automatic detection fails;
- technical-quality validation before pronunciation, fluency, grammar, or vocabulary evidence is trusted.

### 9.2 Practice restart rules

- **P0–P2 ordinary practice:** the learner may restart a recording before submission. Only the submitted attempt becomes direct evidence; repeated rehearsal/restarts are preserved as support/practice context where useful.
- **P3 target-time probe:** restart behavior is restricted according to the declared evidence goal. A restart can convert the attempt from clean evidence to practice.
- **P4:** no coaching-driven redo inside the measured part. A true technical failure invalidates the affected attempt and may justify a fresh equivalent replacement; it does not count as failure.

### 9.3 Audio-quality gate

Before evaluator output affects the learner model, the App must distinguish at least:

- usable audio;
- usable with limitations;
- unusable/invalid.

Clipping, severe background noise, missing segments, wrong microphone, or endpointing that cuts meaningful speech cannot be translated into “poor pronunciation,” “weak grammar,” or “low fluency.” A technically weak but partly usable attempt may support only the dimensions that remain defensible.

Exact signal-processing thresholds are implementation/calibration decisions.

---

## 10. Transcript Behavior

### 10.1 Transcript is companion evidence, not ground truth

**Decision:** Automatic transcripts are explicitly **provisional**. They support diagnosis, learner review, vocabulary/grammar inspection, and navigation through the recording. They do not replace audio for intelligibility, fluency, pronunciation, or disputed wording.

The evidence model preserves transcript/evaluator confidence separately from learner performance.

### 10.2 When the transcript is visible

| Context | Transcript behavior |
|---|---|
| P0–P2 clean attempt | Hidden while the learner is speaking; available after submission/partner exchange |
| P3 independent attempt | Hidden during the clean attempt; opening answer-bearing live text before submission would make the attempt assisted |
| P4 measured simulation | Hidden for the entire measured oral block; feedback/transcript available only after measurement ends |
| Diagnosis/repair | Show the relevant turn/excerpt, not necessarily a wall of text |
| Accessibility use | Stage 25 may define accommodations; the App must preserve whether the accommodation changes the capability being claimed |

### 10.3 Transcript uncertainty and learner correction

When recognition is uncertain, the UI should mark the uncertain span rather than silently invent a word and then correct the learner for it.

The learner may be allowed to indicate **“I said something else”** or correct the displayed transcript for review. Such an edit:

- may help the evaluator/coach understand intended lexical/grammatical content;
- does not alter the original audio;
- does not retroactively prove pronunciation or intelligibility;
- is stored as a correction/uncertainty event, not a rewritten original attempt.

If a disputed word materially affects a high-impact judgment, the product either re-evaluates from audio or leaves the dimension uncertain. It does not let low-confidence ASR manufacture a mistake-memory pattern.

### 10.4 Feedback highlighting

The transcript may highlight:

- the one or two repair targets selected by the coach;
- a successful phrase worth retaining;
- a turn where partner response was not addressed;
- a segment with evaluator uncertainty.

It should **not** underline every imperfect ending or filler in red. The product goal is B1-sufficient communication and exam-point protection, not native-like transcript cleanup.

---

## 11. Preparation and Timing

### 11.1 Preparation progression

Preparation itself is a trainable exam strategy.

| Rung | Preparation behavior |
|---|---|
| **P0** | Open preparation; visible prompt interpretation; phrase bank/planning frame may be used |
| **P1** | Short suggested prep; learner chooses a few useful words/ideas; support still available |
| **P2** | Part-specific timed prep drills and note-making; most language support on request |
| **P3** | Target-like preparation practice with learner-created notes and no default answer-bearing support; some sessions use the full target preparation window |
| **P4** | Current verified **20-minute shared preparation window for all three oral task sheets**, no coaching/model/translation help, target-like notes only |

Bestehen should train the learner to make **brief idea/keyword notes**, not write a complete speech to read aloud.

### 11.2 Timed part practice

The model-test launch targets are approximately:

- S1: **3 minutes**;
- S2: **6 minutes**;
- S3: **6 minutes**.

These are target-part budgets for P4/current-blueprint simulation, not punishment timers for foundation learners.

At P0/P1, time pressure is normally absent or soft. P2 uses generous timers. P3 introduces target-time probes. P4 uses the exact verified target behavior.

### 11.3 Full oral simulation

A target-condition Speaking simulation is one measured commitment:

1. receive all three task sheets / role inputs;
2. prepare for the verified target window;
3. complete S1, S2, and S3 in sequence;
4. receive no coaching, transcript, phrase bank, translation, or score between parts;
5. finish the whole measured block;
6. only then evaluate, diagnose, and feed repair work into later sessions.

The App may show neutral timing/orientation equivalent to an interlocutor keeping the exam moving. It must not use countdown pressure so aggressively that it creates an experience harsher than the target.

A part-only P4 probe can also exist for evidence collection, but it must be labelled a **target-condition part probe**, not a full oral mock.

### 11.4 Pause and interruption rules

Ordinary practice may pause between meaningful boundaries. P4 full oral simulation does not offer convenience pause/resume inside the measured exchange. A connectivity/audio failure is a technical invalidation, not a language failure, and the affected evidence must be handled accordingly.

---

## 12. Interim Decisions Made

The following product decisions are locked in this first Stage 13 pass:

- Speaking maps to three current target families: **S1 get acquainted, S2 discuss a topic, S3 plan together**.
- Exact TELC format is versioned target knowledge and must be revalidated before P4/mock/readiness use.
- Solo practice exists for every part but cannot substitute for genuine interaction evidence.
- Fixed/prerecorded partner rehearsal is the low-cost default for early rungs, diagnostics, and repairs.
- Adaptive turn-based AI partnership is justified for S2/S3 when the learner's previous meaning must change the next turn.
- The AI partner is a peer during the attempt, never a hidden coach.
- Continuous real-time full-duplex voice is an upgrade, not a launch prerequisite.
- Voice is required for oral evidence; typed responses remain learning-only.
- Transcript is provisional companion evidence, hidden during clean measured attempts, and cannot overrule uncertain audio.
- Turn-taking must tolerate B1 pauses, preserve learner agency, and treat partner/endpointing failure as evaluation uncertainty rather than learner failure.
- S3 scenarios have multiple acceptable plans and evaluate negotiation/convergence rather than a model solution.
- P4 uses a shared 20-minute target preparation window plus the current target part timings, with all feedback deferred until the measured block ends.

The remaining sections of this stage will lock evaluation, accent fairness, phrase/repair behavior, oral-readiness contribution, failure handling, and cost tiers before the stage is marked complete.
