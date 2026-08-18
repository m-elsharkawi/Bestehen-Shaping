# Bestehen / App — Stage 04: Learner Model

> **Status:** Authoritative Stage 04 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** TELC B1
>
> **Model promise:** Replace broad labels such as “weak at listening” with specific, evidence-backed capability states that tell the coach what to train, how much support to use, and how certain the conclusion is.

## 1. Purpose and Scope

This document defines the multidimensional learner state used by Bestehen / App. The model must support precise coaching from an uneven A1 starting point through authentic TELC B1 evidence without turning one score, one placement label, or one AI judgment into false certainty.

The learner model has four jobs:

1. represent what the learner can currently do at a particular difficulty and under particular conditions;
2. preserve the evidence, uncertainty, mistake recurrence, and assistance dependence behind that conclusion;
3. roll fine-grained capabilities into honest task-, section-, written-, and oral-level views;
4. connect the learner’s history to the stable skill nodes and exam intelligence supplied by Bestehen / Corpus.

This is a product model, not a storage schema, model-provider choice, or final TELC readiness formula. It defines the information and behavior later design and architecture must preserve. Stage 05 owns the full mistake-memory lifecycle, Stage 15 owns calibrated TELC readiness and pass logic, and Stages 09–13 own the final task maps and rubrics. Those stages may refine thresholds, but they should not need to invent the learner state from scratch.

### Core decision

**Bestehen models a learner as an evidence-backed overlay on a shared skill graph, not as a global CEFR level and not as a collection of completed lessons.**

Each capability state answers:

- **What?** The exact grammar, vocabulary, comprehension, production, topic, or strategy node.
- **In which lane?** Reading recognition, listening recognition, writing production, speaking production, or interactive use.
- **At what difficulty?** Foundation, Bridge to B1, or target B1 evidence difficulty.
- **Under what conditions?** Assisted or unassisted; open, practice-timed, or exam-timed; replay/reference constraints; task and topic context.
- **How well?** Current capability estimate and mastery band.
- **How sure are we?** Evidence confidence, coverage, consistency, recency, and evaluation quality.
- **What happened before?** Mistake episodes, repairs, retries, delayed transfer, and recurrence.

Mastery, confidence, freshness, and readiness are separate concepts. A learner can have a strong historical capability whose evidence is stale, a weak capability supported by high-confidence evidence, or promising assisted performance that is not yet readiness evidence.

## 2. Inputs / Existing Decisions

This stage preserves the project overview, identity, and App Stages 01–03:

- Bestehen is a calm, direct, evidence-based personal German exam coach.
- The learner may start around A1, while the destination remains authentic TELC B1 performance.
- German is learned through exam-shaped activity, not a conventional chapter curriculum.
- Readiness is the primary progress concept, but it must not be manufactured before adequate evidence exists.
- Written and oral pass risk remain separate; a strong component must not hide a pass-critical weak one.
- Assistance adapts by skill. Assisted success can guide learning but is weaker readiness evidence than recent, unassisted, timed work.
- Reading, Language Elements, Listening, Writing, and Speaking must receive direct evidence; one skill is not inferred from another.
- The initial diagnostic creates a provisional state with at most moderate confidence overall and normally low overall confidence for Writing and Speaking.
- Diagnostic evidence records served difficulty, assistance, timing/replay/reference conditions, evaluation quality, technical flags, and provenance.
- A single diagnostic mistake is a candidate signal, not a durable known weakness.
- The coach must explain where the learner is, what is holding them back, and what to do next.
- Corpus provides the taxonomy, task patterns, difficulty/relevance signals, and skill relationships; the App owns personal evidence and coaching.
- The initial product must be affordable: deterministic updates and precomputed intelligence are preferred to always-on AI.

No earlier decision is changed. Stage 04 makes the provisional initialization contract from Stage 03 durable and aggregatable.

## 3. Decisions and Rationale

### 3.1 Use an evidence ledger plus derived state

**Decision:** Every valid attempt creates an evidence observation. Learner states are derived summaries of those observations; they do not replace or overwrite the history.

This allows the system to explain changes, re-evaluate old evidence after calibration improves, recover from a bad evaluator, and distinguish a true regression from one anomalous task. It also avoids a fragile model in which a single mutable “mastery percentage” loses the conditions and reasoning behind it.

The first model has four layers:

| Layer | Purpose | Examples |
|---|---|---|
| Learner and goal context | Stable personal planning context, not mastery evidence | Target TELC B1, exam date/status, available study time, journey phase, accessibility conditions |
| Evidence observations | What actually happened in a task or evaluated response | Result, rubric dimensions, difficulty, assistance, timing, replay, evaluator confidence, technical validity |
| Capability and mistake states | Derived per-node learner overlay | Grammar production emerging; listening detail reliable untimed; appointment vocabulary recurring gap |
| Exam rollups | Interpretable task, section, written, and oral summaries | Listening target-condition estimate, section confidence, written evidence coverage, oral bottleneck |

Self-report and declared prior experience may route content, but they do not enter mastery as performance evidence.

### 3.2 Model capability by node, lane, difficulty, and condition

**Decision:** A fine-grained learner state is never only “skill + score.” Its minimum conceptual key is:

**Corpus skill node × ability lane × target/difficulty context**

Condition facets—assistance, timing, replay/reference use, and task realism—remain attached to evidence and summarized separately. The model should not explode into a permanent state for every possible combination; it keeps one capability state with condition-specific evidence summaries and comparable-pair indicators.

The core ability lanes are:

1. **Reading recognition/comprehension**
2. **Listening recognition/comprehension**
3. **Writing production**
4. **Speaking production**
5. **Interactive speaking use**, when interaction has actually been observed

Grammar and vocabulary nodes may receive evidence in several lanes. Reading evidence cannot initialize Listening, Writing, or Speaking mastery. Writing evidence cannot initialize Speaking. Typed speaking rehearsal remains learning activity, not oral evidence.

### 3.3 Use mastery bands backed by a non-learner-facing estimate

**Decision:** Each capability maintains a normalized internal capability estimate for aggregation and calibration, but the product uses evidence-aware bands rather than presenting false decimal precision to the learner.

The initial bands are:

| Band | Meaning |
|---|---|
| Unknown / not evidenced | No valid direct evidence exists for this node and lane |
| Not yet demonstrated | Valid attempts exist, but the learner has not yet shown functional use at the served accessible difficulty |
| Emerging | Success is inconsistent, limited to narrow examples, or depends on substantial help |
| Functional | The learner usually succeeds at the current working difficulty, possibly with light support or without time pressure |
| Reliable | Success repeats across fresh variants and occasions with little or no assistance |
| Target-evidenced | Recent direct evidence shows reliable use at relevant B1 difficulty under the condition being claimed; timing must also be demonstrated when timing is part of the claim |

“Target-evidenced” for a vocabulary or strategy node does not mean the learner is ready to pass a section. It only states that this fine-grained capability has suitable evidence. Section readiness still depends on breadth, task-pattern coverage, weighting, conditions, and pass constraints.

The internal estimate is a calibration tool, not a learner promise. Stage 15 may use it to predict target-condition performance, but the interface should normally show plain-language states, evidence confidence, and the specific condition.

### 3.4 Separate four concepts that are often collapsed

| Concept | Question | Example |
|---|---|---|
| Capability/mastery | How likely is successful use at the stated difficulty and condition? | Functional at Bridge listening detail |
| Confidence | How trustworthy is that estimate? | Low: only one valid clip |
| Freshness/stability | How current and retained is the evidence? | Aging; last checked 43 days ago |
| Readiness contribution | How relevant is this evidence to passing TELC B1 now? | Limited because it was assisted and untimed |

A low mastery estimate can have high confidence after repeated failures. A high assisted capability can have moderate confidence but low readiness contribution. Old reliable evidence remains historical capability while current confidence weakens.

## 4. Detailed Product Model and Rules

### 4.1 Common learner-capability state

Every fine-grained state must be able to express the following conceptual fields:

| Field group | Required product meaning |
|---|---|
| Identity | Stable Corpus node reference, taxonomy version, learner ability lane, and target exam context |
| Current capability | Internal normalized estimate, learner-facing mastery band, current working difficulty, and highest recently demonstrated difficulty |
| Evidence volume | Valid observations, effective evidence units, distinct tasks/forms, distinct sessions/days, and first/last observation |
| Conditions | Unassisted/assisted evidence split; open/practice-timed/exam-timed split; replay/reference and realism context where applicable |
| Assistance dependence | Unknown, independent, succeeds with light support, or support-dependent, based on comparable evidence rather than one help request |
| Timing status | Not measured, within target, inconsistent, or currently over target for a defined task pattern |
| Confidence | None, low, medium, or high, plus the main reason the band is limited |
| Freshness/stability | Fresh, aging, stale, or historical-only; stability earned through successful spaced evidence |
| Trend | Improving, stable, declining/contradictory, or insufficient evidence; never inferred from two incomparable tasks |
| Mistake/repair summary | Recent and lifetime independent recurrence, latest cause confidence, last repair, immediate retry, and delayed transfer result |
| Provenance and quality | Links to evidence observations, evaluator method/confidence, content/tag confidence, and technical validity |

The model must preserve “not measured” separately from poor performance. Missing evidence is never silently converted to zero.

### 4.2 Grammar mastery

Grammar is represented as exam-relevant concept nodes, not textbook chapters. Examples include word order, subordinate clauses, connectors, cases, preposition-case combinations, modal verbs, tense choice, relative structures, negation, agreement, and inflection where those patterns affect exam performance.

For each grammar node, Bestehen tracks separate evidence for:

- recognition/interpretation in Reading;
- recognition in Listening where the form carries meaning;
- contextual selection in Language Elements;
- controlled production in a constrained repair or cloze;
- spontaneous production in Writing;
- spontaneous production in Speaking;
- preservation of meaning and communicative impact, not merely surface error count.

Grammar mastery dimensions are:

1. **Form recognition** — notices the relevant form or relationship.
2. **Meaning/function** — understands what the form changes.
3. **Contextual choice** — selects an appropriate form among plausible alternatives.
4. **Construction** — can produce the structure when prompted.
5. **Spontaneous control** — uses it appropriately without the answer being cued.
6. **Robustness** — retains the capability across topics, fresh tasks, and relevant time pressure.

A multiple-choice success supplies direct evidence for contextual selection, not automatic evidence for spontaneous production. A correct spontaneous use in Writing or Speaking is strong productive evidence and may provide weak supporting evidence for recognition, but it does not prove broad comprehension of every variant.

Grammar errors that do not damage meaning can still be recorded, but later writing/speaking scoring must weight them according to B1 communicative sufficiency rather than native-level perfection.

### 4.3 Vocabulary and domain mastery

Vocabulary is represented through word/phrase/concept groups and domain nodes rather than a single “words known” count. Synonyms, paraphrases, collocations, separable forms, functional phrases, and common exam expressions can be related without pretending they are interchangeable.

For a vocabulary concept, track:

- form-to-meaning recognition in text;
- sound-to-meaning recognition in audio;
- meaning-to-form recall;
- recognition of synonym/paraphrase relationships;
- contextual selection and collocation;
- productive availability in Writing;
- productive availability in Speaking;
- reliable use under a relevant topic and task context.

Domain mastery summarizes breadth and availability within topics such as housing, appointments, work, travel, health, services, scheduling, and social arrangements. It is not a count of viewed cards. It derives from direct encounters across multiple words/phrases and tasks.

Rules:

- Reading recognition does not initialize listening recognition; sound recognition requires audio evidence.
- Recognition does not initialize productive recall.
- A word supplied by a vocabulary preview, answer hint, or model response counts as assisted use.
- A correct spontaneous productive use is stronger productive evidence than choosing the word from options.
- Repeated success with the same prompt or memorized phrase provides limited breadth evidence.
- Unknown words may affect a task result, but a wrong task answer does not penalize every vocabulary tag. Only diagnosed or directly observed gaps receive negative node evidence.

### 4.4 Reading skills

The initial Reading skill family includes:

- identifying gist and text purpose;
- scanning for names, dates, places, conditions, and other target details;
- detailed comprehension;
- synonym and paraphrase recognition;
- local and cross-sentence inference;
- recognizing writer/speaker intention or stance where tested;
- matching texts, headings, people, notices, or needs;
- distinguishing restrictions, negation, exceptions, and qualifiers;
- distractor rejection;
- managing unknown vocabulary without abandoning the task;
- relevant time allocation and checking.

Reading evidence is tagged to the exact task pattern and served linguistic difficulty. A correct answer may support a targeted reading node, but should not automatically lift every skill associated with the item. A wrong answer updates a fine node only when the response pattern or diagnosis supports that attribution; otherwise it remains section/task-pattern evidence with an unresolved cause.

### 4.5 Listening skills

The initial Listening skill family includes:

- gist and situation recognition;
- detail extraction;
- numbers, dates, times, prices, names, and spelled information;
- negation, restrictions, exceptions, and corrections;
- speaker intention, attitude, and communicative purpose;
- inference from spoken context;
- synonym/paraphrase recognition in speech;
- distractor rejection and revision when speakers change or correct information;
- coping with authentic speed, reductions, connected speech, and varied voices;
- maintaining attention across the clip or sequence;
- using the permitted listening opportunity strategically.

Listening evidence records audio difficulty, speed, number of speakers, clarity/noise, playback rule, and replay use where available. Slower audio and repeated playback are valid learning conditions, not failure, but they do not establish the same target-condition capability as first-play or exam-rule performance.

A missed answer after understanding the audio but overlooking the task instruction may be a strategy error rather than a listening-recognition failure. The model preserves the distinction instead of applying a generic Listening penalty.

### 4.6 Writing competencies

Writing is modeled through rubric dimensions, each supported by direct response evidence:

- task fulfillment and required content-point coverage;
- communicative success and comprehensibility;
- organization, progression, and cohesion;
- register and appropriateness for purpose/recipient;
- vocabulary sufficiency, range, and functional phrase use;
- grammar control to the degree it protects meaning;
- conventions required by the task, such as greeting and closing where relevant;
- planning, revision, and completion within the available time.

The model preserves prompt category, expected content points, response length/completeness, assistance used, time mode, and evaluator confidence. One overall writing grade must not erase dimension variation: a learner may cover the task well but have weak organization, or use adequate language but omit a required point.

Writing capability is based on B1 sufficiency and communicative outcome, not distance from native-like prose. AI corrections or rewritten ideal answers are not themselves learner evidence. Only what the learner produced or subsequently revised counts.

### 4.7 Speaking competencies

Speaking is modeled through:

- task fulfillment and relevance;
- comprehensibility/intelligibility;
- fluency and continuity;
- vocabulary sufficiency and functional phrase use;
- grammar control sufficient to preserve meaning;
- interaction: listening/responding, turn-taking, follow-up, and keeping the exchange moving;
- proposing, agreeing, disagreeing, negotiating, and offering alternatives;
- repair strategies when a word or structure is missing;
- organization of a short presentation or personal contribution where required;
- use of preparation time and completion within task timing.

Production and interaction are separate lanes. A monologue can provide speaking-production evidence but cannot establish interaction mastery. A fixed two-turn diagnostic supplies only limited interaction evidence, as decided in Stage 03.

Pronunciation is evaluated through intelligibility and communicative impact, not accent similarity. Poor recording quality or unreliable transcription cannot be interpreted as poor speaking; affected dimensions remain not evidenced or low-confidence.

### 4.8 Exam-strategy skills

Exam strategy is modeled as observable behavior linked to task patterns, not generic advice the learner has read. Initial nodes include:

- understanding instructions and response format;
- allocating time and moving on;
- scanning before detailed reading;
- eliminating distractors for a defensible reason;
- handling unknown words;
- checking restrictions, negation, units, and required content points;
- protecting attention during one-chance or limited-play audio;
- planning and checking Writing;
- using Speaking preparation time;
- sustaining interaction and recovering when stuck;
- making a best supported response rather than leaving avoidable blanks.

Strategy mastery requires either observable interaction data or a response/diagnosis that supports the conclusion. Correctness alone does not prove good strategy, and slowness alone does not prove poor time management. Strategy states remain task-pattern-specific until evidence supports transfer.

### 4.9 Topic familiarity

**Decision:** Topic familiarity is a context/facet state, not a substitute for language mastery.

For each relevant topic/domain, track:

- exposure breadth across different tasks and subtopics;
- receptive lexical familiarity in Reading and Listening separately;
- productive availability in Writing and Speaking separately;
- performance relative to the learner’s usual level on comparable task difficulty;
- confidence and recency;
- overfamiliarity risk when repeated content makes performance look stronger than transfer.

A single failed health task does not establish “weak at health.” Topic weakness requires repeated underperformance or directly diagnosed lexical gaps across independent evidence. Topic familiarity mainly helps content selection, vocabulary repair, and coverage. Section aggregation must use varied topics so familiarity with housing or appointments cannot create a false readiness signal.

### 4.10 Passive/receptive versus productive ability

The first model enforces the following transfer rules:

1. Reading, Listening, Writing, Speaking production, and interactive speaking remain separate direct-evidence lanes.
2. Receptive success may suggest what to test productively, but does not raise productive mastery.
3. Spontaneous productive success may add reduced supporting evidence to the underlying concept’s receptive availability, because production normally implies access to meaning, but it cannot establish broad recognition across forms or modalities.
4. Controlled production after a prompt is weaker than spontaneous production.
5. Writing never initializes Speaking, and Reading never initializes Listening.
6. Cross-lane relationships influence recommendations and diagnostic hypotheses before they influence mastery.

This asymmetry prevents a learner who recognizes a connector in a cloze from being treated as able to use it in speech.

### 4.11 Assistance model

Assistance is recorded by type, timing, and whether it was used:

| Assistance class | Examples | Evidence treatment |
|---|---|---|
| None | Normal instructions only | Eligible for unassisted evidence |
| Access/non-answer-bearing | Replay of instructions, font/accessibility support, clarification of interaction mechanics | Does not reduce ability evidence unless it changes the tested capability |
| Language support | Vocabulary preview, translation, sentence explanation, slowed audio, phrase bank | Valid assisted capability evidence |
| Strategy hint | Reminder to scan restrictions or check content points | Assisted strategy/task evidence |
| Answer-narrowing hint | Elimination cue, highlighted evidence location, partial answer structure | Weak learning evidence for independent mastery |
| Model/solution exposure | Model answer, transcript, direct correction before retry | Subsequent immediate performance is repair evidence, not independent mastery |

Only help used before the scored response changes the attempt’s assistance status. Help offered but not used does not make an attempt assisted. Post-response feedback does not retroactively weaken the original attempt.

Assistance dependence is inferred from comparable evidence:

- **Unknown** — too little paired evidence.
- **Independent** — succeeds without assistance on suitable fresh tasks.
- **Light-support responsive** — performance becomes functional with non-answering or small language support.
- **Support-dependent** — meaningful success is currently observed mainly after answer-bearing or substantial support.

Assistance dependence can be skill-specific. It is not a global learner label.

### 4.12 Timing model

Timing uses three explicit modes:

1. **Open/untimed** — time may be measured for context but is not a performance constraint.
2. **Practice-timed** — a generous or skill-building target is active.
3. **Exam-timed** — the task follows the relevant target-exam time constraint.

Each timed observation preserves the applicable target, actual completion, unfinished status, and any accessibility accommodation. The derived timing state for a task pattern is:

- not measured;
- within target;
- inconsistent/near boundary;
- currently over target or incomplete under time.

Untimed success establishes knowledge/skill but not time-pressure reliability. Timed failure does not automatically lower the underlying language node: the diagnosis may update timing/strategy instead, or both if the evidence supports both. Stage 25 defines accommodation behavior; the learner model must preserve accommodated conditions rather than treating them as generic slowness.

### 4.13 Evidence observation

Every scored or evaluated learner response must be able to record:

| Dimension | Required meaning |
|---|---|
| Provenance | Attempt, task/content version, session, date, diagnostic/practice/review/retry/mock context |
| Target mapping | Section, task pattern, primary skill nodes, secondary/prerequisite nodes, topic, and taxonomy version |
| Outcome | Correct/partial/incorrect, rubric dimension result, incomplete, skipped, or invalid |
| Difficulty | Linguistic, reasoning/task, audio/production, and target relevance as available |
| Conditions | Assistance offered/used, timing mode, replay/reference/transcript/model exposure, and realism |
| Independence | First attempt, immediate retry, delayed transfer, repeated item, or fresh equivalent task |
| Evaluation | Deterministic/rubric/AI/human method, evaluator confidence, and dimensions actually supported |
| Quality | Technical validity, content quality, tag confidence, and anomaly flags |
| Explanation | Diagnosed cause when supported; otherwise explicitly unresolved |

One response can contribute to several relevant nodes, but it is still one evidence event. Aggregation must not count it multiple times as independent evidence.

### 4.14 Evidence strength

The first product uses a small ordinal hierarchy with provisional relative weights. These weights are internal defaults for update impact and are designed to be recalibrated; they are not displayed to learners.

| Tier | Initial relative weight | Typical evidence |
|---|---:|---|
| E0 — excluded | 0 | Technical failure, corrupt content, unsupported evaluator judgment, skipped task |
| E1 — weak learning signal | 0.25 | Answer-bearing assistance, same-item retry, immediate post-model production, low-confidence secondary attribution |
| E2 — standard observation | 0.5 | Valid diagnostic sample, assisted fresh task, or unassisted but narrow/untimed evidence |
| E3 — strong direct evidence | 1.0 | Fresh equivalent task, direct node attribution, suitable difficulty, unassisted result, trustworthy evaluation |
| E4 — target-condition anchor | 1.5 | Recent B1-relevant, unassisted, exam-timed/realistic task or mock dimension with strong content/evaluation quality |

Strength is reduced when content/tag confidence is low, the evaluator cannot support the dimension, the item was recently repeated, or multiple outcomes come from the same repair episode. Difficulty mismatch is preserved rather than hidden: success on a much easier task may be strong evidence at that difficulty but weak evidence for target B1 capability.

Guardrails:

- A correct answer supplies full positive evidence only to the directly tested node/task pattern. Prerequisite nodes receive at most reduced supporting evidence.
- A wrong answer penalizes a fine-grained node only when diagnosis or response design supports that cause. Otherwise it updates the task/section signal and creates an unresolved diagnostic need.
- One event has a capped effect and cannot move a well-supported capability several bands.
- An immediate successful retry records repair responsiveness; a later fresh, unassisted transfer task is needed for reliable mastery.
- Repeated answers to the same content do not count as independent breadth.

### 4.15 Mastery updates

The initial update model is deliberately simple:

1. Validate the observation. Exclude technically invalid or unsupported dimensions.
2. Attribute the result to one or a small number of primary nodes. Secondary nodes receive reduced weight.
3. Normalize the outcome within its task/rubric and served difficulty; do not compare raw percentages across unequal difficulty as if equivalent.
4. Apply evidence-strength, recency, evaluation-quality, and tag-confidence weight.
5. Blend the result with the existing state while capping single-event movement.
6. Recalculate condition summaries, confidence, trend, and mastery band.
7. Preserve the event and explanation so the movement is auditable.

Recent evidence matters more, but one realistic failure does not erase a stable history. Repeated coherent realistic evidence should eventually dominate older assisted evidence. Exact blending coefficients are implementation/calibration parameters; the product requirements are monotonic explainability, bounded single-event impact, and separation of conditions.

### 4.16 Confidence

Confidence is based on five factors:

1. **Effective volume** — accumulated evidence strength, not raw click count.
2. **Breadth** — distinct forms, prompts, task patterns, and topics where relevant.
3. **Independence** — different sessions/days and fresh tasks rather than one repair chain.
4. **Consistency** — whether comparable evidence agrees.
5. **Quality and recency** — trustworthy content/evaluation and evidence current enough for the claim.

Initial bands:

| Band | Implementable default |
|---|---|
| None | No valid direct evidence |
| Low | One usable episode, less than 2 effective evidence units, heavy assistance, narrow coverage, or weak evaluation |
| Medium | At least 2 effective units across at least two independent tasks/episodes, including an unassisted signal, with no major unresolved contradiction |
| High | At least 5 effective units across at least three occasions and fresh variants, including recent strong direct evidence at the claimed difficulty/condition and adequate coverage |

Additional constraints:

- Stage 03’s initial diagnostic remains capped at moderate confidence; overall Writing and Speaking normally remain low after one short sample.
- High confidence in a productive or interactive competency requires evidence on multiple days and prompts.
- Major contradictory evidence lowers confidence by at least one band until a clarifying task resolves it.
- High volume cannot compensate for only one repeated item, only assisted work, or an evaluator that cannot support the dimension.
- Confidence attaches to the claim. The learner can have high confidence for “functional with support” and low confidence for “exam-timed B1.”

These thresholds are starting defaults. Stage 26 must validate whether they predict later performance without making evidence collection unnecessarily slow.

### 4.17 Recency, decay, and stability

**Decision:** Time does not delete learning or automatically rewrite a learner as weak. Instead, Bestehen separates historical capability from current freshness and readiness usefulness.

Initial freshness bands for ordinary capability states:

| Freshness | Default treatment |
|---|---|
| Fresh: 0–30 days since relevant evidence | Full use for current coaching estimates |
| Aging: 31–60 days | Reduced current confidence; suitable for a short refresh rather than a reset |
| Stale: 61–120 days | Cannot alone support “reliable now”; prioritize a recheck before high-stakes conclusions |
| Historical-only: over 120 days | Retained as a prior and progress history, but not treated as current evidence until refreshed |

Stage 15 may impose shorter windows for ready-to-book, timed mocks, and pass-critical claims. The first learner model uses one understandable default rather than separate decay curves for every node.

Stability is earned by successful evidence separated over time:

- **Unproven** — one episode or only immediate retry success.
- **Recent** — repeated fresh success, but not yet shown after a meaningful interval.
- **Stable** — success on fresh tasks across at least three occasions spanning at least two weeks, including unassisted use.

Stable evidence decays in confidence more slowly for daily coaching, but still becomes stale for readiness. A new weak result first creates contradiction and a recheck need; it does not instantly erase stable historical capability.

### 4.18 Mistake history and recurrence frequency

Stage 04 defines the state that Stage 05’s mistake-memory rules will consume.

A mistake episode links:

- the original evidence observation;
- affected task pattern and candidate/confirmed node;
- cause category and diagnosis confidence;
- modality, topic, difficulty, assistance, timing, and evaluator quality;
- whether it was the first attempt, immediate retry, or delayed transfer;
- repair offered/completed;
- immediate retry outcome;
- later fresh-transfer outcome;
- current status such as unresolved, responsive to repair, recurring, or not recently observed.

The history is additive. A later success does not erase that the error occurred; it changes the derived current state.

Recurrence is calculated from **independent failure episodes**, not raw wrong clicks:

- multiple wrong responses and the immediate retry inside one repair loop count as one episode;
- the same repeated item does not create independent recurrence;
- a new fresh task in another session may create a new episode;
- both lifetime and recent-window recurrence are retained;
- opportunities/exposures are retained so three failures in four opportunities is distinguishable from three in forty;
- cross-topic and cross-modality recurrence are visible without automatically merging mastery.

Descriptive recurrence bands for the first model are:

| Band | Meaning |
|---|---|
| Isolated | One independent episode |
| Repeated | Two independent episodes |
| Recurring | At least three independent episodes across at least two sessions/days |
| Persistent under target conditions | Recurring pattern remains in recent unassisted or timed B1-relevant evidence |

These bands describe frequency; Stage 05 decides exact promotion to a known weakness, priority increases, repair status, and spaced-return scheduling.

### 4.19 Section-level exam performance

The learner model maintains rollups for:

- Reading;
- Language Elements / Sprachbausteine;
- Listening;
- Writing;
- Speaking;
- the written exam component;
- the oral exam component.

Each section state contains:

| Section field | Meaning |
|---|---|
| Current target-condition estimate | Expected performance range at relevant B1 difficulty and stated assistance/timing conditions |
| Training-condition estimate | Current performance at the learner’s working difficulty, even when assisted or untimed |
| Task-pattern coverage | Which relevant task types have direct evidence and which remain unknown |
| Competency/skill contributors | Fine nodes most responsible for the estimate |
| Confidence and freshness | Evidence quality, breadth, consistency, and recency |
| Realism coverage | Proportion and breadth of unassisted, timed, replay-constrained, or mock evidence |
| Bottlenecks | Pass-relevant weak or unknown contributors that should not be averaged away |
| Evidence provenance | Main observations causing the current state or change |

Aggregation follows these product rules:

1. **Evidence flows upward:** response/rubric → task pattern → section → written/oral component. A section score never creates mastery evidence downward.
2. **Use the target blueprint:** task patterns and rubric dimensions are weighted by their TELC B1 importance, supplied by the target-exam definition and informed by Corpus. Exact weights belong to Stages 09–15.
3. **Do not equally average fine skills:** a long list of minor vocabulary nodes must not overwhelm a required writing dimension or task pattern.
4. **Keep missing evidence unknown:** uncertainty widens the predicted range and lowers confidence; missing Speaking is not scored as zero and is not imputed from Writing.
5. **Apply bottleneck guards:** a pass-critical task pattern or productive dimension can limit the section status even when the weighted mean looks healthy.
6. **Keep conditions separate:** assisted/untimed training performance and unassisted/exam-timed target performance are shown as different views, not blended into one flattering number.
7. **Avoid duplicate evidence:** one item tagged to several nodes contributes once to the section observation.
8. **Prefer ranges to premature points:** before calibration, section output is a performance band/range with confidence and evidence gaps, not a claimed official score.

For the written component, Reading, Language Elements, Listening, and Writing remain visible as separate contributors. Speaking forms the oral component and retains separate production/interaction evidence. The model may provide an overall coaching summary, but it must not average written and oral components into a state that hides failure risk in either. Stage 15 defines the exact TELC pass gates and final readiness representation.

### 4.20 Corpus skill graph connection

**Decision:** Corpus owns the shared, versioned definition of skills; the App owns the learner overlay.

Corpus provides:

- stable node identifiers and human-readable definitions;
- node type: grammar, vocabulary/domain, reading, listening, writing, speaking, strategy, topic, task pattern, or relationship;
- relationships such as prerequisite, related, often-confused, receptive/productive counterpart, and task-pattern relevance;
- TELC relevance, generic A2/B1 relevance, frequency, and evidence confidence;
- task/content mappings and mapping confidence;
- taxonomy version and migration mappings when nodes change.

The App stores against those nodes:

- learner evidence observations;
- capability/mastery, conditions, confidence, freshness, and trend;
- mistake/repair recurrence;
- current coaching priority and evidence gaps;
- target-specific interpretation for TELC B1.

Rules:

- Corpus frequency/relevance changes coaching priority, not the learner’s demonstrated mastery.
- Corpus source authenticity and usage rights do not become learner capability fields.
- Low-confidence content-to-node tagging reduces attribution strength. The event may still support a broader task/section state.
- When no reliable fine node exists, the App records a broader provisional classification rather than inventing precision.
- Raw/reference source content is not required in the learner model.
- The App may add an App-specific state such as “evidence needed” or “repair responsive,” but must not fork the canonical definition of the language skill.

#### Taxonomy version changes

Evidence retains the node and taxonomy version used when it was created. Corpus supplies migration mappings:

- **rename/definition clarification:** preserve the state;
- **merge:** combine evidence without double-counting shared events;
- **split:** distribute prior evidence as reduced-confidence supporting evidence and request direct confirmation for the new child nodes;
- **retire:** preserve historical evidence and map forward where possible;
- **changed task relationship:** recalculate rollups without rewriting the original observation.

A taxonomy update must never silently reset progress or silently create high-confidence mastery in a newly split node.

### 4.21 Journey and coaching context

The learner model also preserves goal context needed by later stages:

- TELC B1 target;
- exam status/date;
- available weekly and session time;
- current journey phase;
- explanation/accessibility conditions that affect evidence interpretation;
- evidence gaps that block stronger claims;
- current working difficulty and assistance recommendation per major skill;
- last meaningful readiness/section review and reasons for change.

These fields help the daily coach use the learner model, but they are not themselves mastery. A fixed exam date increases priority and urgency; it never inflates capability or readiness.

## 5. Edge Cases / Failure or Uncertainty Handling

| Situation | Learner-model behavior | Coaching consequence |
|---|---|---|
| No evidence for a skill | State is unknown/not evidenced, never zero | Schedule the smallest feasible evidence task |
| One diagnostic sample | Create a provisional state under Stage 03 confidence caps | Start useful training but avoid strong readiness language |
| Strong assisted, weak unassisted performance | Preserve both; mark assistance dependence | Continue scaffolded repair and schedule a fresh unassisted check |
| Strong untimed, weak timed performance | Keep language capability and timing/strategy risk distinct | Train pace/execution before reteaching everything |
| Immediate retry succeeds | Record repair responsiveness at weak evidence strength | Schedule delayed transfer; do not mark reliable yet |
| One realistic mock contradicts stable practice | Add strong contradictory evidence and reduce confidence | Diagnose, run a focused clarifier, and avoid an instant total reset |
| Repeated realistic failures | Let recent strong evidence dominate old assisted success | Raise bottleneck priority and reassess section status |
| Topic-specific success after repeated same content | Reduce breadth/independence strength | Rotate topic/form before generalizing mastery |
| Objective answer wrong but cause unclear | Update task-pattern result; keep fine cause unresolved | Ask a small diagnostic question or use a later equivalent task |
| AI evaluation uncertain | Update only supported dimensions at reduced strength | Request another sample or lower confidence; do not invent a score |
| Audio/recording technical failure | Exclude affected observation/dimensions | Retry without penalizing Listening/Speaking |
| Learner returns after months | Preserve history as historical-only and lower current confidence | Run short targeted rechecks, not a full reset |
| Skills are uneven | Maintain independent lanes, difficulties, and conditions | Recommend the highest-value reachable blocker |
| Corpus tag changes | Recalculate through version mapping with confidence safeguards | Preserve progress and surface only meaningful coaching changes |
| Accessibility changes timing | Preserve accommodation context | Do not diagnose general slowness solely from accommodated time |

### Contradictory evidence

Contradiction is a first-class state, not noise to be hidden by an average. The model should ask:

1. Were task difficulty, assistance, timing, topic, or content quality different?
2. Did the evaluator support the same dimension?
3. Is one event an immediate retry, repeated content, or technical anomaly?
4. Is the change large enough and repeated enough to suggest real regression or improvement?

Until resolved, the estimate may remain near its prior value while confidence drops and a clarifying fresh task becomes a priority.

### Sparse evidence across a large graph

The product should not attempt to populate every possible node from inference. Fine-grained states exist only where direct or defensible supporting evidence exists. Broader task/section states may have more confidence than individual nodes. Coaching should prefer collecting evidence at decision-relevant gaps rather than exhaustively testing the taxonomy.

## 6. Relationship to Other Bestehen Stages

- **Stage 03 — Initial Diagnostic:** supplies the provisional observations, condition flags, difficulty route, and confidence caps that initialize this model.
- **Stage 05 — Mistake Memory:** uses mistake episodes and recurrence fields to define known-weakness promotion, priority, resolution, explanation, and spaced return.
- **Stage 06 — Daily Coaching Engine:** consumes mastery, relevance, recurrence, staleness, evidence gaps, difficulty, assistance dependence, urgency, and available time.
- **Stage 07 — Core Learning Loop:** produces the linked attempt → diagnosis → repair → retry → delayed-transfer evidence episodes.
- **Stage 08 — A1→B1 Progression:** defines the detailed skill-specific difficulty and assistance transitions represented here.
- **Stages 09–13 — Skill Coaching:** finalize TELC task maps, rubrics, exact node coverage, and evidence interpretation for Reading, Language Elements, Listening, Writing, and Speaking.
- **Stage 14 — Review:** uses recency, stability, recurrence, and productive/receptive lanes to schedule retained practice.
- **Stage 15 — TELC Readiness:** calibrates section weights, target-condition prediction, evidence minimums, written/oral pass gates, displayed bands, and outcome-based recalibration.
- **Stage 16 — Mock Exams:** supplies high-strength, realistic section/task evidence without bypassing fine-grained diagnosis.
- **Stage 17 — Ready to Book:** sets stricter recency, consistency, timed/unassisted, and written/oral evidence requirements.
- **Stage 19 — Information Architecture:** decides how much of the model is visible while keeping the primary learner view understandable.
- **Stage 21 — Content Strategy:** ensures tasks carry reviewed node, difficulty, topic, answer/rubric, and quality metadata.
- **Stage 22 — Corpus → App Contract:** turns the conceptual skill-graph connection and versioning expectations into the full product contract.
- **Stage 24 — Account/Data:** defines retention, portability, deletion, sync, and privacy for the evidence history.
- **Stage 25 — Accessibility/Device:** defines accommodations and input fallbacks that the model must preserve as evidence context.
- **Stage 26 — Analytics:** validates confidence thresholds, update weights, decay windows, skill attribution, section predictions, and calibration.
- **Stage 27 — Cost Boundaries:** sets portfolio-wide operating limits for evaluation and classification.

### Cross-stage guardrail

Later stages may tune numerical defaults, but they must preserve:

- direct evidence by modality;
- mastery separate from confidence, freshness, and readiness;
- assistance and timing as explicit conditions;
- missing evidence as unknown;
- a traceable evidence history;
- separate written and oral risk;
- section aggregation that cannot hide bottlenecks;
- learner state connected to versioned Corpus nodes.

## 7. Cost Notes

This stage adds **no required per-attempt premium AI call** beyond evaluation already needed for a task.

### Preferred low-cost default

- Objective results and reviewed rubric outputs create evidence deterministically.
- Learner-state updates, decay/freshness, confidence bands, recurrence counts, and rollups use deterministic rules.
- Corpus tags, task-pattern mappings, relevance, and difficulty are computed/reviewed ahead of learner use and cached.
- Writing/Speaking evaluation should return all needed structured dimensions in the same batched call already used for feedback; the learner model must not call another model merely to update mastery.
- Ambiguous mistake causes remain unresolved or broad rather than triggering an expensive classifier every time.
- Common explanations of score movement are assembled from evidence fields and reviewed templates.

### When more expensive evaluation is justified

A higher-quality evaluation may be invoked only when:

- a productive sample materially affects a mock, readiness, or ready-to-book decision;
- cheap evaluation is internally contradictory or below the confidence needed for that decision;
- the learner supplies new evidence that warrants reevaluation.

The fallback is a broader node, lower confidence, or another sample—not invented precision. Re-evaluation results are stored and reused. Provider, database, and model architecture remain deferred.

The meaningful recurring cost remains short speech transcription and productive evaluation defined in the relevant task stages; maintaining the learner model itself should be computationally cheap.

## 8. Decisions Made

1. Defined the learner as an evidence-backed overlay on a shared Corpus skill graph rather than a global CEFR label.
2. Chose an evidence ledger plus derived capability, mistake, and exam-rollup states.
3. Defined capability by skill node, modality/lane, difficulty, assistance, timing, and task context.
4. Defined mastery bands from unknown through target-evidenced while keeping confidence, freshness, and readiness separate.
5. Defined grammar, vocabulary/domain, Reading, Listening, Writing, Speaking, exam-strategy, and topic-familiarity dimensions.
6. Enforced direct receptive/productive and Reading/Listening/Writing/Speaking separation, with only cautious asymmetric supporting transfer.
7. Defined assistance types, assistance dependence, and the rule that offered-but-unused or post-response help does not weaken the original attempt.
8. Defined open, practice-timed, and exam-timed evidence plus separate timing status.
9. Defined the evidence observation, five evidence-strength tiers, bounded and explainable updates, and no shotgun penalties across every tag.
10. Defined confidence from volume, breadth, independence, consistency, quality, and recency, with implementable initial thresholds.
11. Defined freshness and stability, preserving historical mastery while current confidence decays.
12. Defined mistake episode history, independent recurrence frequency, and descriptive recurrence bands for Stage 05.
13. Defined task-to-section-to-written/oral aggregation, condition separation, bottleneck guards, and missing-evidence behavior.
14. Defined the versioned Corpus-to-learner overlay contract and safe behavior for node rename, merge, split, retirement, and remapping.
15. Chose a deterministic, low-cost default with premium evaluation reserved for high-impact uncertain productive evidence.

## 9. Open Questions / Deferred Decisions

### Open owner questions

**None.** The first learner model can be responsibly defined from the existing product decisions.

### Deferred product decisions

- Exact known-weakness promotion, repair, resolution, and spaced-return thresholds — Stage 05.
- Daily priority formula and session-assembly weights — Stage 06.
- Detailed assistance ladder and promotion/demotion thresholds — Stage 08.
- Final TELC task mappings, competency rubrics, and item-to-node tagging rules — Stages 09–13.
- Exact review intervals and scheduling algorithm — Stage 14.
- Exact section weights, predicted-score/readiness formula, pass constraints, minimum evidence, and stricter recency windows — Stage 15.
- Mock-specific evidence rules and cadence — Stage 16.
- Ready-to-book threshold and required number/consistency of mocks — Stage 17.
- Learner-facing visualization and which internal states are exposed — Stages 18–20.
- Full Corpus → App request/response contract and taxonomy governance process — Stage 22.
- Retention, export, deletion, privacy, and sync — Stage 24.
- Accessibility accommodation policy — Stage 25.
- Final calibrated numerical weights, decay curves, and confidence thresholds — Stage 26 using observed transfer, mock, and real-exam outcomes.
- Storage design, algorithms, model providers, and technical architecture — post-shaping architecture work.

The initial evidence multipliers, confidence thresholds, recurrence bands, and freshness windows are product defaults chosen to make the first model implementable. They must be treated as tunable calibration parameters rather than scientific constants.

## 10. Definition of Done Check

- [x] Define grammar mastery.
- [x] Define vocabulary/domain mastery.
- [x] Define reading skills.
- [x] Define listening skills.
- [x] Define writing competencies.
- [x] Define speaking competencies.
- [x] Define exam-strategy skills.
- [x] Define topic familiarity.
- [x] Define mistake history.
- [x] Define recurrence frequency.
- [x] Define recency/decay.
- [x] Define confidence in each estimate.
- [x] Separate assisted vs unassisted performance.
- [x] Separate timed vs untimed performance.
- [x] Separate passive understanding from productive ability.
- [x] Connect learner skills to the Corpus skill graph.
- [x] Define evidence strength and bounded update behavior.
- [x] Define section-level performance and written/oral aggregation.
- [x] Preserve diagnostic initialization and sparse-evidence uncertainty.
- [x] Keep the initial model implementable, calibratable, and financially sustainable.

**Stage 04 is complete when a broad statement such as “weak at listening” can be replaced by a traceable claim such as: “Listening detail for dates and restrictions is emerging at Bridge difficulty, currently replay-dependent, not yet tested under exam timing, and supported by medium-confidence evidence across three fresh tasks.”**

