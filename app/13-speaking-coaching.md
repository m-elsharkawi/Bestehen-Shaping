# Bestehen / App — Stage 13: Speaking Coaching

> **Status:** Authoritative Stage 13 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Speaking promise:** Rehearse the actual communicative work of TELC B1 with enough support to start around A1, then remove that support until the learner can speak, react, negotiate, and complete all three oral tasks under credible exam conditions.

## 1. Purpose and Scope

This document defines the complete learner-facing Speaking coaching experience for Bestehen / App.

Speaking must feel like rehearsal with an exam coach and a useful partner, not like open-ended chatbot conversation, a pronunciation-imitation app, or a transcript-correction exercise. The product has to develop and measure two related but distinct capabilities:

1. **spoken production** — can the learner express the intended meaning in understandable B1 German?; and
2. **interaction** — can the learner listen, respond, ask, negotiate, repair, share the floor, and move a joint task forward with another person?

Those capabilities are not interchangeable. A good monologue can provide strong production evidence but cannot prove interaction. A typed response can be useful preparation but cannot provide oral evidence. A transcript can help diagnose language but is not the learner's voice and cannot become the sole source of truth for pronunciation or fluency.

Stage 13 applies the existing **Observe → Attempt → Diagnose → Repair → Retry → Remember** loop and the P0→P4 progression model to the current TELC B1 oral examination. It defines:

- all current TELC B1 Speaking parts;
- solo practice and interactive partner practice for every part;
- fixed/prerecorded and adaptive AI-partner behavior;
- voice capture, transcript, turn-taking, preparation, and timing behavior;
- the detailed Speaking evaluation rubric and its mapping to official TELC criteria;
- fair treatment of accent, pronunciation, uncertainty, and technical failure;
- useful phrase/structure recommendations and oral repair;
- planning-together scenarios;
- timed/full oral simulation;
- the evidence contract supplied to the independent oral-readiness model;
- a cost-controlled default and explicit upgrade points for higher-quality/real-time speech.

This is product shaping, not implementation architecture. It does not choose a speech-to-text provider, speech model, TTS vendor, audio codec, streaming protocol, database, voice-activity algorithm, or final readiness formula.

### In scope

- current TELC B1 oral task families;
- lower-difficulty P0–P4 Speaking variants;
- solo and genuine interactive practice;
- microphone/voice-response product requirements;
- transcript display and uncertainty;
- preparation notes, task timing, and full oral simulation behavior;
- turn-taking, prompting, silence, rescue, and interruption boundaries;
- original discussion/planning scenario families;
- productive and interactive evaluation;
- oral evidence quality and readiness contribution;
- low-cost and premium speech/partner modes.

### Out of scope

- final calibrated oral-readiness formula and exact minimum evidence counts — Stage 15;
- complete mock cadence and cross-section mock UX — Stage 16;
- ready-to-book thresholds — Stage 17;
- final coach copy system — Stage 18;
- final screen hierarchy — Stage 19;
- generalized content-generation QA and anti-duplication — Stage 21;
- final Corpus → App payload/API — Stage 22;
- audio retention, deletion, export, and privacy implementation choices — Stage 24;
- accessibility equivalence/accommodations for target-condition evidence — Stage 25;
- evaluator-bias measurement and real-outcome calibration — Stage 26;
- model/vendor/streaming/storage architecture.

---

## 2. Inputs / Existing Decisions

Stage 13 preserves the project overview, identity, and App Stages 01–12:

- Bestehen is a calm, direct, evidence-based **personal German exam coach**.
- TELC B1 is the only launch target. Cheap seams for later exams are welcome only where they do not weaken TELC B1.
- A learner may begin around A1. The task remains exam-shaped while language load, scaffolding, partner complexity, timing, and independence change.
- Readiness is the primary progress concept; written and oral pass risk remain separate.
- Speaking production and **interactive speaking** are separate direct-evidence lanes in the learner model.
- Another modality cannot initialize Speaking mastery. Typed rehearsal never becomes oral evidence.
- The Stage 03 diagnostic uses a cheap 45–90 second oral sample plus a fixed two-turn planning exchange and deliberately leaves sustained interaction/full oral readiness weakly evidenced.
- The learner model already defines Speaking capabilities for task fulfillment, comprehensibility, fluency, vocabulary, grammar, interaction, proposing/agreement/disagreement, negotiation, repair strategies, organization, preparation-time use, and timing.
- Pronunciation is judged through **intelligibility and communicative impact**, not similarity to a native accent.
- Poor recording quality, transcription failure, or evaluator uncertainty cannot be converted into poor learner performance.
- Mistake Memory records production/interaction shortfalls only when attribution is defensible; technical failure is not a learner mistake.
- The Daily Coaching Engine must protect missing/stale oral evidence and may devote nearly a full 25-minute session to interactive Speaking rather than favor cheaper objective skills.
- Stage 07 requires Speaking repair to remain oral when the target is oral, emphasizes only one or two high-impact behaviors per loop, and requires a fresh partner turn for interaction retry.
- Stage 07 also establishes that a fixed/prerecorded partner is preferable for routine interactions when it can test the behavior; a live generative partner is justified only when adaptive exchange adds material value.
- Stage 08 uses **P0 Supported Foundation → P1 Guided A2 → P2 A2/B1 Bridge → P3 Independent B1 Training → P4 Target Conditions**, by task family rather than one global level.
- Phrase banks, sentence starters, planning frames, and other answer-bearing production supports progressively fade. Their use before submission stays attached to the evidence.
- P4 measured attempts use exact target constraints and defer coaching until measurement ends.
- Real/reference exams define what must be rehearsed. Learner-facing practice should normally be original where exact reuse rights are unclear.
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
- a strong emphasis on direct exchange between participants.

The detailed official model test describes the three parts as:

| ID | Target part | Approx. model-test time | Core communicative job | Model-test maximum |
|---|---|---:|---|---:|
| **S1** | **Einander kennenlernen** / Get to know each other | ~3 min | Talk about oneself, ask the partner questions, respond naturally, and handle an occasional additional prompt | 15 |
| **S2** | **Über ein Thema sprechen** / Discuss a topic | ~6 min | Convey the viewpoint on one's own input, understand the partner's different input, exchange opinions and experience, and react to the partner | 30 |
| **S3** | **Gemeinsam etwas planen** / Plan something together | ~6 min | Propose, justify, react, negotiate alternatives, decide what will be done, and agree who does what | 30 |

The model-test oral total is **75 points**, or 25% of the overall 300-point exam. The same model test states that written and oral components have separate 60% pass requirements, making **45/75** the oral minimum in that blueprint. Stage 15 owns the final readiness interpretation.

Official sources used for this verification:

- `https://www.telc.net/sprachpruefungen/deutsch/zertifikat-deutsch-telc-deutsch-b1/`
- `https://shop.telc.net/media/catalog/product/file/2/0/20201225_5061-b00-010301_web.pdf`

**Product rule:** exact part names, timings, point values, task mechanics, preparation rules, and rubric mappings are **versioned target knowledge**. The current telc page confirms the high-level three-part/15-minute/20-minute-preparation shape; the detailed downloadable model test remains the launch blueprint for the part mechanics and rubric behavior. Before a task is labelled **P4**, a Speaking mock is called TELC-realistic, or official-aligned points feed readiness, the approved target blueprint must be revalidated.

### 3.2 Preparation behavior

The detailed model test gives participants all oral task sheets for **20 minutes of preparation**. They may make notes on separate provided sheets and use those notes in the oral exam, but should not simply read them aloud. Participants do not prepare together and do not use dictionaries, phones, or other aids during preparation.

Bestehen uses that behavior as the P4 launch simulation contract. Training can offer much more support, but that support must not leak into target-condition evidence.

### 3.3 Official rubric anchor

The model-test rubric evaluates each Speaking part independently on four official criteria:

1. **Ausdrucksfähigkeit** — content-/role-appropriate expression, vocabulary, and realization of speaking intent;
2. **Aufgabenbewältigung** — participation in the conversation, discourse/compensation strategies, and fluency;
3. **Formale Richtigkeit** — syntax and morphology;
4. **Aussprache und Intonation** — pronunciation/intonation according to how deviations affect understanding.

Bestehen uses finer dimensions for coaching, but those dimensions do **not** become invented official criteria. Section 12 maps the finer rubric back to the official anchor.

---

## 4. Speaking Task Model

### 4.1 S1 — Get to know each other

**Target behavior:** reciprocal personal exchange, not a memorized self-introduction speech.

A strong S1 attempt normally demonstrates that the learner can:

- answer common personal questions with enough detail to sustain exchange;
- ask the partner relevant questions instead of waiting passively;
- react to an answer with a short follow-up when natural;
- move among familiar topics such as home, family, learning German, work/study, languages, free time, or similar everyday domains;
- handle one unexpected but familiar follow-up without collapsing into a prepared script;
- remain understandable and reasonably continuous with B1-sufficient language.

**Anti-pattern:** a flawless 60-second biography with no partner-directed behavior provides production evidence but weak S1 interaction/task evidence.

### 4.2 S2 — Discuss a topic

**Target behavior:** exchange information and viewpoints from **different inputs**, then discuss the topic rather than deliver two independent mini-presentations.

A valid S2 task contains paired inputs about the same familiar topic, normally with meaningfully different positions or experiences. The learner should:

1. understand their own input;
2. explain its main view to the partner in their own words;
3. listen to the partner's different view;
4. state their own opinion and give a reason;
5. bring in personal or plausible experience where useful;
6. respond to the partner—agree, disagree, qualify, compare, ask, or follow up;
7. keep the exchange moving without the system scripting every next sentence.

The partner must not reveal the learner's unseen counterpart input before the relevant exchange. S2 depends on genuine information difference.

### 4.3 S3 — Plan something together

**Target behavior:** jointly produce an actionable plan through negotiation.

A valid S3 scenario gives both speakers a shared goal and several dimensions to decide together. The learner should be able to:

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

There is **no single correct plan**. Evaluation focuses on the communicative process and whether a coherent agreement emerges, not on matching a model solution.

---

## 5. P0 → P4 Speaking Progression

Speaking progression is tracked separately for **S1 personal exchange**, **S2 discussion**, **S3 planning**, and fine-grained capabilities such as intelligibility, fluency, or negotiation. A learner can be P3 in S1 and P1 in S3 interaction.

| Rung | Speaking experience | Partner behavior | Support | Timing / evidence claim |
|---|---|---|---|---|
| **P0 Supported Foundation** | One or two meaningful oral turns using concrete A1/early-A2 language | Fixed prompt/response, patient and predictable | Phrase bank, sentence starters, key vocabulary, planning frame visible | Open time; supported speech/response evidence only |
| **P1 Guided A2** | Short reciprocal exchange; simple opinion/reason; one planning choice | Mostly fixed, with reviewed follow-ups | Selective starters and functional phrases; support increasingly on request | Soft turn/task targets; emerging independent oral use |
| **P2 A2/B1 Bridge** | Full B1 mechanism with controlled language load and several turns | Scenario-controlled partner with limited adaptive branches | Most support on request; phrase bank reduced | Generous part timers; B1-shaped interaction with support recorded |
| **P3 Independent B1** | Original B1-equivalent tasks and sustained exchange | Adaptive turn-based partner normal for S2/S3; fixed partner remains useful for drills | No default answer-bearing help; practice help marks the attempt assisted | Target-time probes and unassisted B1 evidence |
| **P4 Target Conditions** | Current verified TELC-equivalent three-part oral behavior | Exam-role partner using target-like interaction, no coaching | Only target-permitted preparation notes; no phrase/model help in measured block | Exact verified prep/part conditions; readiness-grade evidence when technically/evaluatively valid |

### 5.1 Promotion is behavior-specific

Promotion requires direct evidence that the relevant behavior works with less support.

Examples:

- S1 loses sentence starters after repeated independent answering and questioning.
- S2 moves from fixed counter-opinions to adaptive discussion after the learner can reliably paraphrase an input and state a reasoned view.
- S3 moves from a proposal menu to open planning after independent proposal, response, and alternative behaviors emerge.
- Pronunciation support fades when intelligibility is stable even if grammar remains guided.

If a B1 exchange is unreachable, the coach steps down **one dimension**—language load, turn count, partner complexity, or support—rather than globally demoting Speaking.

---

## 6. Practice Modes

### 6.1 Solo oral drill

**Decision:** Every part has a useful solo mode, but solo work is never presented as a substitute for genuine interaction evidence.

Solo mode is cheap, immediate, lower-pressure, and especially useful for repair. It captures **actual voice** whenever oral evidence is intended.

#### S1 solo

Use reviewed prompts for familiar personal topics. Some prompts require the learner to formulate a question they would ask a partner or add a follow-up to an imagined response.

Useful forms:

- 20–40-second personal answer;
- answer + reason/example;
- hear a simple partner statement and record a follow-up question;
- unexpected familiar follow-up to reduce memorized-introduction dependence.

Evidence: production, relevance, fluency, language, and intelligibility. It does **not** establish sustained turn-taking.

#### S2 solo

The learner receives one original input card and records:

1. a short paraphrase of the input view;
2. their own opinion and reason;
3. a personal example/experience where appropriate;
4. a response to one or two fixed recorded contrasting statements.

The last step creates limited response evidence, but full interactive mastery remains unproven because the partner cannot truly react to the learner.

#### S3 solo

The learner receives a planning goal and constraints, then records:

- an opening proposal;
- a reason;
- a response to a fixed counterproposal/constraint;
- an alternative;
- a final spoken summary of a plausible agreement.

This is valuable repair/preparation but still bounded interaction evidence.

### 6.2 Scripted/fixed partner rehearsal

**Decision:** A reviewed fixed/prerecorded partner is the **default low-cost interactive mode** for P0–P2, the diagnostic, targeted repairs, and repeatable phrase/turn-taking drills.

Scenario-specific branches may include:

- neutral follow-up;
- agreement;
- disagreement;
- request for a reason;
- practical constraint;
- alternative proposal;
- clarification request.

A fixed partner can provide direct evidence of responding to a partner turn, but interaction confidence remains bounded because partner adaptability and unpredictability are limited.

### 6.3 Adaptive turn-based AI partner

**Decision:** Adaptive turn-based interaction is the normal high-value mode for P2/P3 S2 and S3 when the learner's previous meaning genuinely needs to change the next turn.

The AI partner acts as a **peer participant during the attempt, not as the coach**. It must:

- stay inside the assigned scenario, role, viewpoint, and difficulty;
- respond to what the learner actually said when meaning is recoverable;
- keep turns short enough to preserve learner speaking time;
- ask natural follow-ups selectively rather than interrogating every turn;
- introduce only the scenario's intended amount of friction/constraint;
- disagree/counterpropose when the task needs negotiation, but not manufacture conflict just to be interesting;
- let the learner initiate and steer part of the exchange;
- avoid teaching, correcting, translating, or supplying model language until the measured attempt ends;
- avoid silently simplifying German below the declared rung;
- use natural B1-reachable partner language rather than unnecessarily advanced language;
- preserve paired-input secrecy in S2;
- cooperate toward a decision in S3 instead of blocking convergence indefinitely.

The partner has a **scenario contract**, not unrestricted chatbot freedom. Allowed goals, facts, preferences, hidden constraints, and escalation bounds are defined before the attempt so evidence remains interpretable.

### 6.4 Target-condition partner simulation

P4 is a measured oral simulation. The partner behaves like a plausible exam peer, and the coach disappears from the exchange.

Requirements:

- target-like language and reciprocity;
- no teaching or hints;
- no phrase suggestion during the attempt;
- no artificial rescue that makes the learner's task easier than normal partner behavior;
- stable scenario facts and paired inputs;
- target preparation/timing contract;
- all feedback deferred until the measured block ends.

A generative partner is useful for variability, but **real-time full-duplex voice is not required for P4 validity by product definition**. Credible turn-based oral interaction can provide strong evidence if turns, pauses, timing, and partner behavior remain target-like. Real-time voice is a quality/realism upgrade, not the foundation of the product.

---

## 7. Turn-Taking Behavior

### 7.1 Default interaction model

**Decision:** The launch/default experience is **clear turn-based voice**, not continuous always-listening conversation.

This provides an obvious floor, prevents endpointing errors from masquerading as learner interruptions, keeps cost predictable, and still tests the core TELC behaviors: listen, respond, ask/follow up, negotiate, and share turns.

The learner can end a turn explicitly. Automatic end-of-turn detection may exist, but the product must provide recovery/control if it cuts off too early.

### 7.2 Pauses

The partner tolerates ordinary B1 planning pauses. It must not jump in after every hesitation, filler, reformulation, or short silence. Fluency evaluation may record disruptive pauses, but interaction behavior must not create the problem it later scores.

When silence is clearly sustained:

- **practice:** one neutral open prompt may restart the exchange; repeated rescue is recorded as support/interaction evidence;
- **P4:** only target-like neutral conversational prompting is permitted. No vocabulary, translation, sentence starter, or answer-bearing clue is supplied.

### 7.3 Interruptions and overlap

Natural overlap can occur in a real pair exam, but interruption handling is **not required for the first cost-controlled product**.

A later real-time voice upgrade may add:

- interruption/barge-in;
- short backchannels;
- overlapping starts;
- more natural floor transfer.

Upgrade only when this materially improves interaction/stamina realism or a measured learner need. It is not a prerequisite for ordinary S2/S3 practice merely because the technology exists.

### 7.4 Dominance and passivity

The partner should neither monopolize the exchange nor force an exact 50/50 word split.

Evaluate communicative behavior instead:

- did the learner contribute without repeated prompting?;
- did they create openings for the partner?;
- did they respond to partner content?;
- did they ask/follow up when useful?;
- did they negotiate rather than deliver disconnected speeches?

If the AI partner itself dominates or fails to provide a fair opening, affected interaction evidence is invalid or lower-confidence; the learner is not penalized for partner failure.

### 7.5 Communication repair

Repair strategies can be positive B1 behavior. The learner may:

- ask for repetition/clarification;
- paraphrase when a word is missing;
- self-correct while keeping the turn moving;
- check understanding;
- reformulate a proposal.

Self-correction is not automatically a grammar/fluency penalty. Only repeated or disruptive repair that materially harms task completion or understanding affects the relevant dimension.

---

## 8. Planning-Together Scenario Model

### 8.1 Scenario families

S3 uses original/reviewed familiar B1 scenarios such as:

- organizing a small event, celebration, meeting, or group activity;
- planning a day trip, visit, excursion, or local outing;
- helping a friend/classmate/neighbour with a practical task;
- organizing a course/class/community activity;
- planning transport, food, materials, invitations, tickets, or responsibilities for a shared goal;
- coordinating a simple project, appointment, or group decision.

The bank must be broader than one recurring “party” template while remaining in familiar B1 domains.

### 8.2 Required scenario structure

Every S3 scenario conceptually defines:

- one shared objective;
- normally **4–6 negotiable dimensions** such as time, place, participants, transport, budget, food/materials, responsibilities, or sequence;
- facts both speakers know;
- optional partner preferences or one modest hidden constraint that creates a reason to react;
- several acceptable outcomes;
- an explicit convergence condition: a workable shared plan, not a canonical answer;
- functional-language opportunities such as propose, justify, ask, agree, disagree, offer alternative, assign task, confirm.

The task must be solvable without obscure cultural knowledge or one “smart” solution.

### 8.3 Difficulty controls

- **P0:** 2–3 concrete decisions, visible options, one fixed counterproposal.
- **P1:** 3–4 decisions, simple open proposals, one clear constraint.
- **P2:** 4–5 decisions, less language support, more than one reasonable trade-off.
- **P3:** full open B1 planning with independently generated proposals and varied partner response.
- **P4:** current target-like scenario length, instructions, notes, timing, and interaction behavior.

Increasing difficulty means authentic negotiation load, not making the partner obstinate or the scenario artificially complicated.

---

## 9. Voice Input Requirements

### 9.1 Voice is required for oral evidence

**Decision:** A valid Speaking evidence attempt requires the learner's actual voice. Typed answers, selected phrases, or text chat can support preparation/repair but never initialize or improve oral mastery as though speech were observed.

The product must support:

- microphone permission requested **at the point of the first Speaking action**, not as a generic onboarding wall;
- a quick input check before a meaningful measured attempt;
- clear indication that audio is being captured;
- actual response duration and turn boundaries;
- association of each learner turn with scenario/partner turn, preparation condition, support used, and timing mode;
- a learner-controlled way to end/recover a turn if automatic detection fails;
- technical-quality validation before pronunciation, fluency, grammar, or vocabulary evidence is trusted.

### 9.2 Restart rules

- **P0–P2 ordinary practice:** restart before submission is allowed. Only the submitted response becomes direct evidence; repeated rehearsals/restarts remain support/practice context where useful.
- **P3 target-time probe:** restart is restricted according to the declared evidence goal. Restarting can convert clean evidence to practice evidence.
- **P4:** no coaching-driven redo inside the measured part. A true technical failure invalidates the affected attempt and may justify a fresh equivalent replacement; it does not count as failure.

### 9.3 Audio-quality gate

Before evaluator output affects the learner model, distinguish at least:

- usable audio;
- usable with limitations;
- unusable/invalid.

Clipping, severe background noise, missing segments, wrong microphone, or endpointing that removes meaningful speech cannot become “poor pronunciation,” “weak grammar,” or “low fluency.” A partly usable attempt may support only the dimensions that remain defensible.

Exact signal thresholds remain implementation/calibration decisions.

---

## 10. Transcript Behavior

### 10.1 Transcript is companion evidence, not ground truth

**Decision:** Automatic transcripts are explicitly **provisional**. They support diagnosis, learner review, vocabulary/grammar inspection, and navigation through recording. They do not replace audio for intelligibility, fluency, pronunciation, or disputed wording.

Transcript/evaluator confidence remains separate from learner performance.

### 10.2 Visibility

| Context | Transcript behavior |
|---|---|
| P0–P2 clean attempt | Hidden while speaking; available after submission/exchange |
| P3 independent attempt | Hidden during clean attempt; answer-bearing live text before submission makes practice assisted |
| P4 measured simulation | Hidden for the entire measured oral block; available only after measurement ends |
| Diagnosis/repair | Show the relevant turn/excerpt rather than necessarily a wall of text |
| Accessibility use | Stage 25 defines accommodations; preserve whether the accommodation changes the capability claimed |

### 10.3 Uncertainty and learner correction

When recognition is uncertain, mark the uncertain span instead of silently inventing a word and then correcting the learner for it.

The learner may indicate **“I said something else”** or correct the displayed transcript for review. Such an edit:

- may help interpretation of intended lexical/grammatical content;
- does not alter the original audio;
- does not retroactively prove pronunciation/intelligibility;
- is an uncertainty/correction event, not a rewritten original attempt.

If disputed wording materially affects a high-impact judgment, re-evaluate from audio or leave the dimension uncertain. Low-confidence ASR must never manufacture a Mistake Memory pattern.

### 10.4 Feedback highlighting

The transcript may highlight:

- the one or two repair targets selected by the coach;
- a successful phrase worth retaining;
- a turn where partner content was not addressed;
- a segment with evaluator uncertainty.

It should **not** underline every imperfect ending or filler in red. The goal is B1-sufficient communication and exam-point protection, not native-like transcript cleanup.

---

## 11. Preparation and Timed Simulation

### 11.1 Preparation progression

Preparation itself is a trainable strategy.

| Rung | Preparation behavior |
|---|---|
| **P0** | Open preparation; visible prompt interpretation; phrase bank/planning frame may be used |
| **P1** | Short suggested prep; learner chooses a few useful words/ideas; support still available |
| **P2** | Part-specific timed prep drills and note-making; most language support on request |
| **P3** | Target-like preparation practice with learner-created notes/no default answer-bearing support; some sessions use the full target preparation window |
| **P4** | Current verified **20-minute shared preparation window for all three oral task sheets**, no coaching/model/translation help, target-like notes only |

Bestehen trains **brief idea/keyword notes**, not complete speeches to read aloud.

### 11.2 Timed part practice

Current model-test launch targets are approximately:

- S1: **3 minutes**;
- S2: **6 minutes**;
- S3: **6 minutes**.

These are P4/current-blueprint budgets, not punishment timers for foundation learners.

P0/P1 is open or softly timed. P2 uses generous timers. P3 introduces target-time probes. P4 uses exact verified target behavior.

### 11.3 Full oral simulation

A P4 Speaking simulation is one measured commitment:

1. receive all three task sheets/role inputs;
2. prepare for the verified target window;
3. complete S1, S2, and S3 in sequence;
4. receive no coaching, transcript, phrase bank, translation, or score between parts;
5. finish the measured block;
6. only then evaluate, diagnose, and feed repair work into future sessions.

The App may show neutral timing/orientation equivalent to an interlocutor keeping the exam moving. It must not create harsher countdown pressure than the target.

A part-only P4 probe can exist for evidence collection, but it is labelled a **target-condition part probe**, not a full oral mock.

### 11.4 Pause/resume

Ordinary practice can pause at meaningful boundaries. A P4 full oral simulation does not offer convenience pause/resume inside the measured exchange. Connectivity/audio failure is a technical invalidation, not a language failure.

---

## 12. Evaluation Rubric

### 12.1 Core evaluation principle

**Decision:** Bestehen evaluates whether the learner is **communicatively sufficient for B1 and the target task**, not how close their speech is to ideal/native German.

Every evaluated Speaking attempt returns:

1. observable performance by the six coaching dimensions below;
2. **evaluation confidence** for each dimension;
3. the evidence condition: task/rung, assistance, timing, partner mode, technical quality, and transcript quality;
4. only when appropriate, an **official-TELC-aligned estimate** against the four official criteria.

A performance estimate and confidence in that estimate are separate. A dimension can be “likely B1-sufficient, low confidence” or “below current target, high confidence.”

### 12.2 Six coaching dimensions

| Coaching dimension | What Bestehen judges | What it must not do | Main official anchor |
|---|---|---|---|
| **Task completion** | Whether the learner performs the communicative job of the current part and covers the important required moves | Reward mere speech volume or memorized language unrelated to the task | Ausdrucksfähigkeit + Aufgabenbewältigung |
| **Interaction** | Relevance to partner turns, initiative, reciprocity, questions/follow-ups, negotiation, response to proposals, repair, and keeping exchange moving | Use raw turn count or exact 50/50 talking time as the score | Aufgabenbewältigung |
| **Fluency** | Continuity sufficient to communicate: manageable pausing, pace, restart/reformulation, and ability to finish the contribution | Penalize every hesitation, filler, or self-correction; use words/minute as a universal B1 threshold | Aufgabenbewältigung |
| **Vocabulary** | Sufficient range/availability for the role/topic, appropriate functional phrases, understandable word choice, and ability to paraphrase around gaps | Reward advanced vocabulary for its own sake or penalize simple but effective B1 wording | Ausdrucksfähigkeit |
| **Grammar** | Syntax/morphology control, with errors weighted by frequency and effect on meaning/communication | Count all grammatical errors equally or require native-like accuracy | Formale Richtigkeit |
| **Intelligibility / pronunciation** | How easily a reasonable listener can understand the message, including pronunciation/intonation only insofar as they affect understanding | Score accent similarity, “native-ness,” or ASR agreement | Aussprache und Intonation |

These six dimensions are **coaching dimensions**, not six official score columns. They support explanation, repair selection, learner-model updates, and the later readiness model.

### 12.3 Task-completion rules by part

#### S1

A task-complete S1 contribution shows reciprocal getting-acquainted behavior, normally including:

- relevant personal information across several familiar prompts;
- at least some partner-directed questioning/responding;
- enough elaboration to sustain exchange;
- handling of a reasonable follow-up.

A memorized self-presentation without exchange limits task/interaction evidence even if the German is accurate.

#### S2

A task-complete S2 contribution normally includes:

- conveying the core idea of the learner's source/input without simply reading it;
- receiving/responding to the partner's different input;
- expressing a personal view;
- giving at least a simple reason and, when natural, experience/example;
- engaging with the partner's view rather than only delivering a monologue.

Small inaccuracies that do not destroy the source meaning are language/content evidence; a response that reverses or misses the source's central position is a task/content problem.

#### S3

A task-complete S3 contribution normally demonstrates:

- proposals on relevant planning dimensions;
- reaction to partner proposals;
- reasons/constraints where needed;
- alternatives or compromise when there is disagreement;
- enough convergence to reach a workable shared plan;
- assignment/confirmation of responsibilities when the scenario calls for them.

There is no penalty for choosing a different valid plan from a model scenario.

### 12.4 Interaction subskills

Interaction is recorded through observable behavior rather than personality judgments:

- **responsiveness** — addresses the partner's actual content;
- **initiative** — contributes without repeated external prompting;
- **reciprocity** — asks, follows up, invites response, or otherwise gives the partner a natural floor;
- **negotiation** — agrees/disagrees/qualifies and proposes alternatives;
- **repair** — handles misunderstanding or lexical gaps constructively;
- **convergence** — in S3, helps move the pair toward a decision.

A shy learner is not penalized for being quiet as a trait. Only observable task behavior matters.

### 12.5 Fluency rules

B1 fluency can include pauses, reformulation, fillers, and self-correction. Bestehen judges whether those features **materially interrupt the communicative flow**.

Do not use a single words-per-minute target. A slower but coherent learner may be more B1-sufficient than a fast learner who produces disconnected or incomprehensible speech.

Fluency evidence may consider:

- sustained phrase/sentence production;
- pause placement and length when reliable;
- repeated abandoned starts;
- amount of partner/examiner rescue needed;
- completion within the declared task time.

Technical endpointing delays and system latency are excluded.

### 12.6 Vocabulary rules

Vocabulary is sufficient when the learner can realize the speaking intent with familiar B1-reachable language.

Positive evidence includes:

- adequate topic words;
- useful functional language for opinions/proposals/reasons/alternatives;
- paraphrasing around a missing word;
- choosing a simple understandable expression instead of freezing.

Do not downgrade a learner simply because a stronger synonym exists. A memorized phrase counts as strong productive vocabulary evidence only when used appropriately and spontaneously in fresh contexts.

### 12.7 Grammar rules

Grammar feedback follows the Stage 12 principle: **protect communication before perfection**.

- isolated errors that do not impair understanding can still be B1-sufficient;
- repeated errors that confuse time, actor, relation, or speaking intent deserve higher priority;
- an evaluator should avoid converting one uncertain transcript form into a grammar weakness;
- a speaking grammar weakness is confirmed through direct speech evidence, not imported automatically from Language Elements or Writing.

### 12.8 Intelligibility/pronunciation rules

Pronunciation evaluation asks one question first:

**Did pronunciation/intonation make the learner materially harder to understand?**

The current official rubric itself anchors pronunciation to impact on understanding. Bestehen therefore uses listener effort/meaning loss rather than accent conformity.

Useful sub-observations may include:

- a sound contrast that repeatedly changes or obscures a word;
- word stress that repeatedly blocks recognition;
- sentence stress/intonation that materially obscures communicative intent;
- numbers/names/details that are repeatedly misunderstood because of production.

A feature is not a weakness merely because it differs from a native speaker.

### 12.9 Learner-facing performance bands

Routine coaching uses plain-language bands rather than fake numerical precision:

| Band | Meaning |
|---|---|
| **Strong for this target** | Behavior is comfortably functional at the declared rung/condition |
| **B1-sufficient** | The communicative job is achieved with normal B1 imperfections |
| **Borderline / unstable** | Some required behavior succeeds, but point risk or consistency is material |
| **Below current target** | The dimension repeatedly prevents or seriously weakens task success at the declared condition |
| **Not enough valid evidence** | Technical/evaluator/task evidence is insufficient to judge responsibly |

At P0–P2, the product may say “functional at this working level” instead of implying B1 sufficiency.

### 12.10 Official-aligned estimate

When a P3/P4 attempt is sufficiently complete and evaluation confidence is adequate, Bestehen may additionally estimate the four official A/B/C/D criteria and their current blueprint point equivalents.

Guardrails:

- label it **TELC-aligned estimate**, never “official TELC score”;
- preserve the official four-criterion structure instead of summing the six coaching dimensions;
- show uncertainty when evaluator confidence is weak;
- do not display official-like points for a highly scaffolded P0/P1 micro-drill;
- Stage 15 determines how these estimates aggregate into readiness.

---

## 13. Fair Treatment of Accent and Uncertainty

### 13.1 Accent policy

**Decision:** Bestehen does **not penalize accent**. It penalizes only pronunciation/intonation behavior that materially reduces intelligibility under a fair listening condition.

Therefore:

- no comparison against a “native accent” or one prestige accent;
- no requirement to eliminate first-language influence;
- no negative feedback merely because vowels/consonants sound non-native when the word remains clear;
- no preference for one German regional accent as the learner target;
- no reward for accent imitation disconnected from communicative success.

Learner-facing language should say, for example, “This word was hard to understand because the stress changed the word shape” rather than “Your accent is too strong.”

### 13.2 ASR is not a pronunciation judge

A speech recognizer failing to transcribe a word does **not** prove that a human listener would fail to understand it.

If ASR and the acoustic/semantic evidence disagree:

- lower evaluation confidence;
- use audio-capable evaluation where available;
- collect a fresh sample if needed;
- never create a pronunciation weakness from ASR failure alone.

### 13.3 Pronunciation weakness threshold

A fine-grained pronunciation/intelligibility weakness normally requires one of:

- repeated intelligibility impact across fresh oral opportunities; or
- one very clear, high-impact target-condition pattern plus confirmation.

A single unusual proper name, borrowed word, technical term, or noisy recording does not become a durable weakness.

### 13.4 Evaluator uncertainty

Every evaluator can return **not judgeable** or lower confidence. That is a product feature, not a failure to produce a score.

Confidence falls when:

- audio quality is marginal;
- transcript is uncertain where grammar/vocabulary judgment depends on exact wording;
- partner behavior was unfair or malformed;
- a sample is too short/incomplete;
- content/task metadata is ambiguous;
- low-cost and higher-quality evaluators materially disagree;
- the learner's response is valid but outside expected scripted patterns.

Uncertainty reduces the strength of learner-model/readiness updates. It does not default to the lower performance band.

---

## 14. Feedback, Repair, and Useful Phrases

### 14.1 Feedback order

After a normal Speaking attempt, feedback follows this order:

1. **Task verdict:** what communicative job succeeded or remained incomplete.
2. **One earned strength:** a concrete behavior, not generic praise.
3. **Top one or two point-relevant repairs:** never an exhaustive transcript correction.
4. **Evidence:** the relevant turn/audio/transcript excerpt, with uncertainty shown where applicable.
5. **Usable pattern/phrase:** only if it directly repairs the observed behavior.
6. **Oral rehearsal:** learner says/uses the repaired behavior.
7. **Fresh oral retry:** new prompt or partner turn tests transfer.
8. **Remember:** save the result and schedule later oral transfer if needed.

### 14.2 What feedback prioritizes

Order of repair priority:

1. task not completed / wrong communicative move;
2. interaction breakdown;
3. intelligibility breakdown;
4. fluency breakdown that prevents task execution;
5. vocabulary/grammar pattern with meaningful communicative or recurring exam impact;
6. lower-impact surface errors only when recurring and worth the learner's time.

This protects B1 sufficiency and avoids turning Speaking into grammar proofreading.

### 14.3 Useful phrase recommendations

**Decision:** Recommend **small functional phrase sets**, not complete memorized speeches.

A normal repair offers roughly **2–4 short reusable stems** tied to the observed behavior. Examples:

| Function | Example stems |
|---|---|
| Ask/follow up | `Und wie ist das bei dir/Ihnen?` · `Warum ist das für dich/Sie wichtig?` |
| Report an input | `In dem Text geht es darum, dass …` · `Die Person meint, dass …` |
| Give an opinion/reason | `Ich denke, dass …, weil …` · `Aus meiner Erfahrung …` |
| Agree/qualify | `Da stimme ich dir/Ihnen zu.` · `Teilweise ja, aber …` |
| Disagree politely | `Ich sehe das etwas anders, weil …` |
| Propose | `Wie wäre es, wenn …?` · `Wir könnten …` |
| React to a proposal | `Das klingt gut, aber …` |
| Offer alternative | `Dann könnten wir stattdessen …` |
| Converge/confirm | `Dann einigen wir uns auf …` · `Also übernehme ich … und du/Sie …` |
| Repair communication | `Wie meinst du/meinen Sie das?` · `Ich meine damit …` |

These are generic product examples, not a fixed phrase curriculum.

### 14.4 Phrase guardrails

- Recommend a phrase because it solves an observed behavior or high-value upcoming task—not because “B1 learners should memorize phrases.”
- Show variants appropriate to informal/formal address when relevant.
- Avoid long chunks that let the learner fake task mastery.
- Phrase use during a clean P3/P4 attempt is assistance if supplied by the App before submission.
- A phrase becomes productive evidence only when the learner later uses it appropriately in fresh speech without answer-bearing support.
- Stage 14 may schedule useful phrases for review, but review must return them to oral/interactive use rather than become a standalone flashcard product.

### 14.5 Oral repair formats

Typical repair formats:

- **interaction:** hear a partner turn → choose/construct a response function → say it → fresh partner response;
- **fluency:** plan three keywords → deliver one 20–40-second continuous answer → repeat once only when repair purpose is explicit → fresh prompt later;
- **vocabulary:** retrieve/paraphrase a needed idea orally in a new sentence;
- **grammar:** one practical contrast → say two short examples → fresh task turn;
- **intelligibility:** listen/contrast only the problematic word/phrase → say it in context → fresh communicative use;
- **S3 negotiation:** proposal → partner constraint → alternative → agreement.

The learner should normally return to exam-shaped speaking within the Stage 07 repair boundary.

---

## 15. Evidence Contract and Oral Readiness Contribution

### 15.1 Speaking is the oral component, not a decorative subskill

**Decision:** Speaking evidence feeds an **independent oral readiness model** and cannot be averaged away by strong written performance.

Under the currently verified model-test blueprint:

- Speaking is the entire 75-point oral component;
- S1 contributes 15 points;
- S2 contributes 30;
- S3 contributes 30;
- oral passing requires 45/75 in that blueprint.

Stage 15 owns the calibrated prediction/readiness formula, but it must consume this current blueprint as versioned target information and preserve the independent oral pass gate.

### 15.2 Evidence-strength ladder

Speaking evidence is classified by what it can legitimately claim:

| Evidence class | Example | Readiness role |
|---|---|---|
| **Excluded / non-oral** | typed answer, unusable recording, malformed partner exchange | No oral readiness effect |
| **Supported learning evidence** | P0/P1 voice with phrase bank or heavy scaffold | Useful for coaching; very weak readiness contribution |
| **Independent production evidence** | unassisted solo P2/P3 response | Useful for production dimensions; cannot prove sustained interaction |
| **Bounded interaction evidence** | fixed/prerecorded partner exchange | Direct response/turn evidence, but limited adaptability/unpredictability |
| **Adaptive B1 interaction evidence** | unassisted P3 S2/S3 with valid adaptive partner | Stronger interaction evidence; timing/blueprint may still be non-target |
| **Target-condition part evidence** | valid P4 S1/S2/S3 probe | Strong readiness anchor for that part/dimensions |
| **Full target-condition oral evidence** | valid current-blueprint three-part simulation with target prep/timing and no coaching | Strongest App-generated oral readiness anchor before a real exam result |

### 15.3 Minimum product gates before strong oral-readiness language

Stage 15 will set exact counts/recency/calibration, but Stage 13 locks qualitative gates. Strong oral-readiness language cannot be based only on:

- solo monologues;
- one diagnostic sample;
- heavily assisted attempts;
- only S1;
- only fixed-partner exchanges;
- untimed practice;
- invalid/low-quality audio;
- transcript-only scoring.

Before confidence can become strong, evidence must eventually cover:

1. **all three current target parts**;
2. genuine interaction in S2 and S3;
3. unassisted B1-level performance;
4. target-like preparation/timing;
5. valid intelligibility evidence;
6. more than one fresh context/partner scenario so memorized content does not dominate;
7. sufficiently recent evidence according to Stage 15.

### 15.4 Bottleneck behavior

The oral model must not allow a large amount of easy S1 or solo evidence to hide missing/weak S2/S3 interaction.

Likewise, an otherwise strong oral estimate must remain uncertainty-limited if intelligibility cannot be judged because of persistent technical-quality problems.

There is no invented “must pass each speaking part separately” rule here. The current official gate is the overall oral minimum; Bestehen may nevertheless use **internal bottleneck warnings** to prevent fragile readiness estimates.

### 15.5 Required observation metadata

Every meaningful Speaking observation must conceptually preserve enough context for later re-evaluation:

- target blueprint/version;
- S1/S2/S3 and task/scenario identity;
- progression rung/difficulty;
- solo/fixed/adaptive/target partner mode;
- preparation duration/type and notes/support available;
- assistance offered/used;
- timing mode and actual response/part duration;
- learner/partner turn sequence and material rescue/prompt events;
- audio technical quality;
- transcript confidence and disputed/corrected spans;
- six coaching-dimension outcomes and confidence;
- official-aligned A/B/C/D estimate when applicable, with confidence;
- evaluator method/version/confidence;
- content/scenario quality flags;
- immediate repair/retry linkage and later transfer linkage.

This is a product data contract, not a storage schema.

### 15.6 Readiness explanation examples

Learner-facing oral readiness should be explainable, for example:

> **Oral evidence is improving, but confidence is still limited.** Your S1 personal exchange is consistently B1-sufficient. We still need a recent unassisted S3 planning exchange under target timing.

or:

> **Main oral blocker: interaction in Part 2.** Your German is generally understandable, but you often state your view without responding to the partner's argument. That keeps oral readiness below the safe range.

Stage 15 decides exact readiness labels/percentages; Stage 13 requires this causal explainability.

---

## 16. Evaluation Quality and Cost-Controlled Voice Approach

### 16.1 Product cost principle

**Use the cheapest voice/evaluation path that can make the required coaching decision responsibly.**

Speaking is the skill most likely to create recurring AI cost, so Bestehen must not make premium real-time voice a requirement for every oral turn.

### 16.2 Preferred launch/default stack at product level

The default behavior is intentionally provider-agnostic:

1. **Reviewed original scenarios and fixed partner assets** are reused heavily for P0–P2, diagnostics, repairs, and quick reviews.
2. Learner voice is captured only when a Speaking action needs it; the product does not require an always-open microphone.
3. Routine solo/fixed-partner practice can complete without a live generative partner.
4. When transcription is useful, perform **one low-cost transcription pass per completed utterance/block/session as appropriate**, not a premium transcription request for every acoustic event.
5. Deterministic observables—task timing, support use, turn order, retries, partner rescue, scenario completion flags—are computed without a premium language model.
6. Use **one structured low-cost productive evaluation** for a completed Speaking block where open-ended judgment is needed. Its result should populate feedback, learner state, and Mistake Memory; do not buy a second model call just to restate the same judgment.
7. Phrase recommendations should come from reviewed/cached weakness→function mappings whenever possible, with generation only for unusual cases.
8. Reuse/caching applies to partner prompts, TTS/audio assets, scenario variants, evaluation explanations, and repair material whenever learner-specific generation adds little value.

Architecture may realize these requirements in different ways; the product decision is the **call/quality behavior**, not the vendor or protocol.

### 16.3 Cost tiers

| Tier | Default use | Partner | Evaluation | Relative recurring cost |
|---|---|---|---|---|
| **Tier 0 — Scripted oral practice** | P0–P2, diagnostic, repair, quick review | Reviewed/prerecorded/fixed branches | Deterministic observables + optional low-cost post-response evaluation | Lowest |
| **Tier 1 — Adaptive turn-based** | P2/P3 S2/S3 when meaning must shape the next turn | Small/cheap adaptive text/voice turn generation or reviewed branching | One post-block structured evaluator; stronger only when needed | Moderate and bounded |
| **Tier 2 — High-fidelity oral assessment** | Selected P4 probes/full simulations, conflicting evidence, important readiness anchors | Higher-quality adaptive partner when necessary | Higher-quality audio/multimodal evaluator or second-pass adjudication | Selective premium |
| **Tier 3 — Real-time full-duplex voice** | Optional realism upgrade, advanced interaction/stamina work | Low-latency natural voice with interruption/backchanneling | Same evidence rules; not automatically a better score | Highest; not routine |

### 16.4 When a stronger evaluator is justified

Escalate beyond the low-cost evaluator only when the result could materially change coaching/readiness and one of these is true:

- P4/full oral simulation is being used as a readiness anchor;
- intelligibility/pronunciation is central and transcript-based evaluation is insufficient;
- low-cost evaluation confidence is low on a pass-relevant dimension;
- evaluator outputs conflict materially with recent comparable evidence;
- the learner disputes a high-impact transcript/evaluation and audio is available;
- periodic calibration/quality sampling requires it.

Do **not** escalate merely because the learner made grammar errors or because premium output sounds nicer.

### 16.5 Real-time/high-quality voice upgrade points

Real-time full-duplex voice becomes valuable when:

- turn interruption/backchanneling/floor recovery is a demonstrated interaction weakness;
- the learner is close to the exam and higher conversation realism has clear rehearsal value;
- Stage 26 evidence shows turn-based practice under-predicts real oral performance;
- the learner explicitly chooses a high-realism rehearsal mode and cost allows it.

Until then, turn-based voice remains the recommended default because it preserves the core exam behaviors at substantially lower technical and recurring-cost burden.

### 16.6 Cheaper fallback behavior

If adaptive voice or premium evaluation is unavailable/too expensive:

- use reviewed fixed partner branches;
- collect direct voice and turn-based production evidence;
- provide deterministic task/timing/support feedback;
- run a cheaper transcript-based evaluation with explicit limits;
- leave unsupported intelligibility/interaction dimensions as low-confidence/not evidenced;
- schedule a later high-quality sample only when readiness actually needs it.

The product must degrade **confidence**, not invent quality.

---

## 17. Edge Cases / Failure or Uncertainty Handling

### Microphone denied/unavailable

Allow non-oral planning, phrase study, or typed rehearsal for learning, but display **Speaking: not enough oral evidence**. Do not initialize speaking/readiness from text.

### Recording is clipped/noisy/incomplete

Invalidate affected dimensions. Offer a fresh equivalent response when appropriate. Do not diagnose pronunciation, fluency, vocabulary, or grammar from missing speech.

### Transcript is wrong

Mark uncertainty, permit learner correction/flagging, and avoid negative grammar/vocabulary conclusions from the disputed span. Escalate audio review only when material.

### AI partner misunderstands or goes off scenario

Partner failure is not learner failure. Preserve valid learner production evidence where defensible, invalidate affected interaction evidence, and restart with a fresh fair partner turn/scenario if needed.

### Partner is too helpful/easy

Mark the exchange as assisted or lower-realism. It may still be learning evidence but cannot silently become P4 interaction evidence.

### Partner is too difficult/dominant

Reduce or invalidate interaction confidence. Difficulty must come from B1-relevant language/task load, not an adversarial partner.

### Learner gives a memorized speech

Credit intelligible language actually produced, but limit task/interaction/generalization evidence when it does not react to the live prompt/partner.

### Learner uses a memorized useful phrase appropriately

Credit the behavior when it fits the situation. The phrase becomes stronger spontaneous evidence only when it recurs appropriately across fresh contexts without App support.

### Learner pauses for a long time

Distinguish normal planning from inability. One neutral practice reprompt may occur; repeated rescue is recorded. Do not infer a vocabulary/grammar cause without supporting evidence.

### Learner switches to another language

Treat the missing German communicative move as task/language evidence only where fair. Do not label it a pronunciation problem. Lower rungs may use another language in explanation/repair, but measured oral responses are German-target responses.

### Learner self-corrects repeatedly

Self-correction is positive when it repairs meaning while maintaining flow. Only disruptive repeated repair affects fluency/task management.

### Learner reaches a different valid plan

S3 has multiple valid outcomes. Score interaction/convergence, not agreement with a model plan.

### P4 simulation is interrupted by connectivity/system failure

Mark the affected measured block invalid. Do not retain an apparent timed failure. A later clean simulation supplies the evidence.

### Evaluation disagrees with learner history

Do not overwrite the learner model from one anomalous AI score. Lower confidence, compare conditions/content, and collect or escalate a fresh high-value sample.

### Accessibility changes the target condition

Preserve the accommodation/context and defer equivalence rules to Stage 25. Do not silently call a modified condition identical to the target before that product policy is shaped.

---

## 18. Relationship to Other Bestehen Stages

### Stage 14 — Review and Spaced Repetition

Speaking corrections, useful phrases, grammar/vocabulary production gaps, interaction moves, and exam strategies may enter review. Review must return them to **oral productive use**, not only recognition cards.

### Stage 15 — TELC Readiness

Consumes Stage 13's evidence classes, current part weights/pass constraint, condition metadata, dimension confidence, and official-aligned estimates. It must maintain an independent oral readiness result and prevent solo/assisted evidence from substituting for interactive target evidence.

### Stage 16 — Mock Exams

Uses the P4 full oral simulation contract: target preparation, S1→S2→S3 sequence, no coaching between parts, target-like partner behavior, deferred feedback, and versioned blueprint validation.

### Stage 17 — Ready to Book

Must require adequate recent oral evidence. A learner with strong written readiness but missing interactive S2/S3 target evidence cannot be treated as confidently ready.

### Stage 18 — Coach Personality

Refines the wording of B1-sufficiency, difficult feedback, confidence, and uncertainty. It must preserve Stage 13's calm, specific, non-accent-shaming behavior.

### Stage 19 — Information Architecture

Must provide clear Speaking states for preparation, mic check, partner turn, learner turn, post-attempt evidence, audio/transcript review, repair, and fresh retry without turning every semantic state into a separate screen.

### Stage 21 — Content Strategy

Owns generation/QA/anti-duplication for S1 prompts, paired S2 inputs, S3 scenarios, partner constraints, and fresh retries. It should use original content grounded in Corpus patterns unless exact source reuse is permitted.

### Stage 22 — Corpus → App Contract

Corpus should eventually supply task-pattern intelligence, topic/function frequency, difficulty, phrase/interaction patterns, target relevance, source confidence, and target-blueprint versioning. The App owns learner evidence, partner session behavior, evaluation, and personalization.

### Stage 24 — Account/Data/Portability

Must decide raw audio/transcript retention, deletion/export, privacy-sensitive AI handling, and whether the learner can opt out of retaining raw recordings after evaluation. Stage 13 only requires that the evaluation and evidence contract can distinguish audio/transcript availability.

### Stage 25 — Accessibility

Must define microphone fallback, speech/hearing/accessibility accommodations, captions/transcript behavior, and how modified conditions affect readiness claims.

### Stage 26 — Product Analytics and Evaluation

Must measure evaluator agreement, accent/intelligibility bias, false ASR-based errors, partner quality, repair transfer, mock-to-real oral calibration, latency/usability where relevant, and cost per evaluated Speaking block.

### Stage 27 — Business / Cost Boundaries

Can change vendor/model/tier economics but should preserve Stage 13's principle that premium voice/evaluation is selective and earns its cost.

---

## 19. Cost Notes

Speaking has **meaningful recurring-cost impact**. It is likely to be one of the most expensive capabilities in Bestehen if implemented naively.

### Preferred low-cost default

- reviewed reusable prompt/scenario banks;
- prerecorded/cached partner audio where adaptive meaning is unnecessary;
- fixed branches for early interaction and repairs;
- direct voice capture without always-on streaming;
- cheap/batched transcription only where useful;
- deterministic task/timing/support analysis;
- one structured low-cost evaluator per completed productive block rather than per sentence/turn;
- cached/reviewed phrase and repair mappings;
- selective adaptive text/voice partner only for S2/S3 where it adds measurement value.

### What justifies paying more

- P4/full oral readiness anchors;
- low-confidence pass-relevant judgments;
- pronunciation/intelligibility cases that require audio-aware evaluation;
- demonstrated need for adaptive interaction beyond fixed branches;
- near-exam high-realism rehearsals;
- calibration/quality sampling.

### What does not justify paying more

- generic conversational ambience;
- correcting every grammar error;
- live generation of prompts already safely cached;
- premium TTS for every routine fixed partner turn;
- a second AI call that merely restates an evaluator result;
- real-time full-duplex voice for a one-turn pronunciation repair.

No monetary per-session target is locked here because model/provider prices and usage patterns are architecture/business inputs that change. Stage 27 should later turn these behavioral limits into operating-cost budgets.

---

## 20. Decisions Made

1. TELC B1 Speaking is modeled as **S1 get acquainted, S2 discuss a topic, S3 plan together**, with exact target details versioned and revalidated before P4/mock/readiness use.
2. Speaking production and interaction remain separate evidence lanes.
3. Every part has solo practice, but solo practice cannot establish full interaction readiness.
4. Fixed/prerecorded partner rehearsal is the low-cost default for early rungs, diagnostics, and repairs.
5. Adaptive turn-based AI is used where previous learner meaning must shape the next S2/S3 turn.
6. The AI partner is a peer during the attempt, not a teacher or hidden examiner-coach.
7. Turn-based voice is the launch/default interaction model; real-time full-duplex voice is an optional later realism upgrade.
8. Actual learner voice is mandatory for oral evidence; typed rehearsal is learning-only.
9. Transcripts are provisional companion evidence, hidden during clean measured attempts, and cannot overrule uncertain audio.
10. Turn-taking tolerates normal B1 pauses and does not penalize learner behavior caused by partner/endpointing failure.
11. S3 scenarios have multiple valid outcomes and evaluate negotiation/convergence rather than a model plan.
12. P4 uses the current verified 20-minute preparation behavior plus target-like S1/S2/S3 timing, with coaching deferred until the block ends.
13. Six learner-facing coaching dimensions are used: **task completion, interaction, fluency, vocabulary, grammar, intelligibility/pronunciation**.
14. Those six dimensions map back to the four official TELC criteria rather than becoming invented official score columns.
15. Accent itself is never penalized; pronunciation matters only through intelligibility/communicative impact.
16. Feedback prioritizes one or two point-relevant behaviors and returns quickly to oral fresh transfer.
17. Useful phrases are short functional scaffolds, not memorized complete answers; independent later use is required for productive evidence.
18. Speaking feeds the **independent oral pass model**; strong written performance cannot compensate for missing oral evidence.
19. Strong oral-readiness language eventually requires all-part coverage, genuine S2/S3 interaction, unassisted/target-like evidence, valid intelligibility evidence, and fresh scenario breadth.
20. The cost-controlled default uses reviewed/cached assets, fixed branches, selective adaptation, deterministic observables, and one low-cost post-block evaluation; premium audio/real-time models are selectively escalated.

---

## 21. Open Questions / Deferred Decisions

### Owner questions

**None.** No product decision in Stage 13 requires owner preference or risk tolerance to proceed.

### Explicitly deferred product/architecture decisions

- final minimum number, recency window, and consistency requirements for strong oral readiness — Stage 15;
- full/section/mini-mock cadence and scoring integration — Stage 16;
- ready-to-book oral threshold — Stage 17;
- exact learner-facing wording/visualization of Speaking bands — Stages 18–19;
- generated Speaking prompt/partner QA and anti-duplication mechanics — Stage 21;
- exact Corpus payload/interface — Stage 22;
- raw audio/transcript retention/deletion/export and privacy policy — Stage 24;
- accessibility-equivalent target-condition rules — Stage 25;
- evaluator bias thresholds, gold sets, agreement targets, and outcome calibration — Stage 26;
- model providers, local/cloud processing, TTS/STT vendors, streaming architecture, and numerical audio-quality thresholds — architecture;
- whether/when full-duplex real-time voice becomes a shipped upgrade — evidence/cost decision after the cheaper turn-based product is validated.

These deferrals do not block a later design/architecture agent from understanding the intended Speaking product behavior.

---

## 22. Definition of Done Check

| Stage 13 requirement | Status | Where defined |
|---|---|---|
| Map all TELC B1 speaking parts | Done | Sections 3–4 |
| Define solo practice for each part | Done | Section 6.1 |
| Define AI partner behavior for interactive tasks | Done | Sections 6.2–6.4 |
| Define voice input requirements | Done | Section 9 |
| Define transcript behavior | Done | Section 10 |
| Task-completion evaluation | Done | Sections 12.2–12.3 |
| Interaction evaluation | Done | Sections 12.2, 12.4 |
| Fluency evaluation | Done | Sections 12.2, 12.5 |
| Vocabulary evaluation | Done | Sections 12.2, 12.6 |
| Grammar evaluation | Done | Sections 12.2, 12.7 |
| Intelligibility/pronunciation evaluation | Done | Sections 12.2, 12.8 |
| Avoid over-penalizing accent | Done | Section 13 |
| Useful phrase/structure recommendations | Done | Section 14 |
| Turn-taking behavior | Done | Section 7 |
| Planning-together scenarios | Done | Section 8 |
| Exam-like preparation time | Done | Section 11.1 |
| Timed speaking simulation | Done | Sections 11.2–11.4 |
| Feed speaking into independent oral pass model | Done | Section 15 |
| Cost-controlled voice approach + upgrade points | Done | Sections 16 and 19 |
| Conversation flows | Done | Sections 4, 6, 7, 11, 14 |
| Failure/uncertainty handling | Done | Sections 13 and 17 |
| Cross-stage handoff | Done | Section 18 |

### Stage completion statement

**Stage 13 is product-complete.** A later design or architecture agent should not need to invent what Speaking practice is, how the partner behaves, what the learner is evaluated on, how accent/uncertainty are treated, what constitutes strong oral evidence, or where a cheaper voice approach may be upgraded. Calibration, provider choice, storage, privacy, accessibility, and final readiness mathematics remain intentionally owned by their later stages.
