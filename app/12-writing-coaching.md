# Bestehen / App — Stage 12: Writing Coaching

> **Status:** Stage 12 product-shaping decision — in progress
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Writing promise:** Judge whether the learner's own message is likely good enough for B1, show the few changes most likely to protect or win exam points, and make the learner prove those changes in a fresh message rather than replacing their German with polished model prose.

## 1. Purpose and Scope

This document defines the learner-facing Writing coaching model for Bestehen / App. It turns the existing learner-model, mistake-memory, progression, and core-loop decisions into a concrete product contract for B1 writing.

Writing is a productive skill, so the App cannot rely on answer keys alone. It must evaluate open learner text while avoiding two common failure modes: grading every surface error as though B1 meant native-like German, and giving an attractive rewritten answer that teaches little and produces misleading evidence. The central product question is therefore:

**Would this response likely function well enough at TELC B1, what is most likely costing points, and what should the learner change themselves next?**

This stage defines:

- the current TELC B1 target format and rubric mapping;
- prompt/scenario categories and explicit required content points;
- Bestehen's internal evaluation dimensions and their relationship to TELC criteria;
- the B1-sufficiency standard;
- learner-facing feedback and correction behavior;
- repair, learner revision, and fresh rewrite/transfer;
- reusable patterns and template guardrails;
- timing and target-condition behavior;
- evidence passed into the learner model and later readiness model;
- evaluator consistency, calibration, confidence, disagreement, and failure handling;
- a low-cost AI strategy with deterministic checks, reuse/caching, batching, and selective stronger-model escalation.

This is product shaping rather than architecture. It does not choose a model vendor, prompt framework, storage design, editor implementation, API, or final readiness formula.

### In scope

- informal and semi-formal TELC B1 email writing;
- P0–P4 lower-difficulty and target-condition variants;
- task completion, communicative success, organization, vocabulary, grammar/formal accuracy, register, and email conventions;
- correction prioritization and examples;
- evaluation confidence and calibration requirements;
- Writing evidence and mistake-memory outputs;
- low-cost evaluation policy.

### Out of scope

- final cross-skill review scheduler — Stage 14;
- final TELC pass/readiness coefficients — Stage 15;
- full-mock sequencing and complete written-exam simulation — Stage 16;
- ready-to-book thresholds — Stage 17;
- final coach copy system and information architecture — Stages 18–19;
- generalized content-generation QA across the App — Stage 21;
- final Corpus → App technical contract — Stage 22;
- model providers, serving architecture, storage, queues, and implementation details.

---

## 2. Inputs / Existing Decisions

Stage 12 preserves the project overview, identity, and App Stages 01–11:

- Bestehen is a calm, direct, evidence-based **personal German exam coach**.
- TELC B1 is the launch target and the learner may start around A1.
- German is learned through exam-shaped activity rather than a traditional course sequence.
- The core loop is **Observe → Attempt → Diagnose → Repair → Retry → Remember**.
- Readiness is the primary progress concept, with written and oral pass risk kept separate.
- Writing is a direct productive-evidence lane. Recognition or cloze performance cannot substitute for Writing production evidence.
- Mastery, confidence, freshness, assistance dependence, timing, and readiness contribution remain separate.
- The initial diagnostic already uses a short functional message with explicit content points; one diagnostic sample normally leaves overall Writing confidence low.
- The learner model already requires Writing evidence for task fulfillment/content coverage, communicative success, organization/cohesion, register, vocabulary, grammar control, relevant conventions, planning/revision, and completion in time.
- AI/model corrections and model answers are **not learner evidence**. Only the learner's own original or subsequently revised production counts.
- Mistake Memory requires a defensible cause and independent recurrence before a fine-grained known weakness is created.
- Same-item repetition and immediate post-model success are weak learning evidence. Retained repair requires fresh delayed transfer.
- The Daily Coaching Engine protects Writing evidence gaps, pass-critical weaknesses, due repair, realism progression, and coverage rather than favoring cheaper objective skills.
- The canonical loop prioritizes task fulfillment and comprehensibility over polishing every surface error and normally keeps repair within roughly 2–6 minutes, ordinarily under eight minutes.
- Stage 08 progression uses **P0 Supported Foundation → P1 Guided A2 → P2 A2/B1 Bridge → P3 Independent B1 Training → P4 Target Conditions**, by task family/capability profile rather than one global level.
- Assistance offered but unused does not weaken evidence. Assistance used before submission remains attached to the attempt.
- Real/reference material defines the target; learner practice should normally use original content when exact reuse rights are unclear.
- Bestehen is initially a personal project, so recurring premium-model calls must earn their cost.

No earlier App decision is materially changed by Stage 12.

---

## 3. Current TELC B1 Writing Target

### 3.1 Verification and versioning rule

The target was rechecked on **19 August 2026** against the official telc `Zertifikat Deutsch B1, Übungstest Version 1` and the current telc shop/product information.

The current verified target is:

| Target property | Current verified behavior |
|---|---|
| Subtest | Schriftlicher Ausdruck / Writing |
| Output | One **informal or semi-formal email** |
| Task source | A short incoming message/scenario that establishes recipient, purpose, and situation |
| Required content | **Four Leitpunkte / content points** |
| Time | **30 minutes** |
| Official criteria | I **Aufgabenbewältigung**, II **Kommunikative Gestaltung**, III **Formale Richtigkeit** |
| Criterion bands | A / B / C / D |
| Raw value per criterion | A = 5, B = 3, C = 1, D = 0 |
| Writing maximum | Raw criterion sum is multiplied by three: **45 points** maximum |
| Exam weight | **15%** of the 300-point overall exam |

The official task also asks the candidate to think about an appropriate order, greeting, introduction, and closing before writing. The current assessment guidance treats Writing as a personal or semi-formal email and evaluates whether the text fits that communicative situation.

**Product rule:** exact target format, scoring, and timing are **versioned exam knowledge**. Before an attempt is labelled P4/target-condition or used as a readiness anchor, the App must rely on a currently verified target blueprint. A historical task may remain useful general Writing evidence after a format change, but must not silently retain target-condition status.

### 3.2 What TELC's rubric means for Bestehen

The official three criteria are the scoring anchor. Bestehen may expose finer coaching dimensions, but it must not pretend those finer dimensions are extra official TELC criteria.

#### Criterion I — Aufgabenbewältigung / task management

The current rubric maps the four required content points directly to A–D:

| TELC band | Current task-management meaning |
|---|---|
| A | All four content points are handled appropriately |
| B | Three content points are handled appropriately |
| C | Two content points are handled appropriately |
| D | One or no content point is handled appropriately |

A content point can count even when treated briefly, provided it is relevant, meaningful, and understandable. Bestehen must therefore avoid teaching the false rule that every content point needs a long paragraph.

If the response has little or no connection to the writing prompt, the official rubric treats this as wrong topic and all criteria receive D. If the broad topic is present but the communicative situation is wrong, task management may be D while language criteria are still judged. Bestehen must model this distinction because it changes both diagnosis and evidence validity.

#### Criterion II — Kommunikative Gestaltung / communicative design

This criterion covers the range and appropriateness of language, text logic, cohesion/coherence, connectors, register, vocabulary range, and realization of the communicative purpose. The target is not elaborate prose. A B1 response should be able to connect simple elements into a coherent linear message, use enough vocabulary to handle familiar purposes, and sustain the appropriate relationship with the recipient.

The current official guidance also makes clear that personal/semi-formal email characteristics and register matter. Missing or unstable register, disconnected content points, and unusable linking can lower this criterion even if individual sentences are grammatically understandable.

#### Criterion III — Formale Richtigkeit / formal accuracy

This criterion covers grammatical control together with spelling, punctuation, and written-form accuracy. The current official guidance explicitly gives **comprehensibility priority**: not every grammatical error has equal impact, and systematic errors can still be compatible with B1 when the intended meaning remains mostly clear.

That aligns directly with Bestehen's existing principle: correct what protects communication and exam points before polishing harmless imperfections.

### 3.3 B1 sufficiency is the target, not A-band perfection

**Decision:** Bestehen coaches toward **stable B1-sufficient performance**, with stronger A-band behavior welcomed but not required as the default repair target.

The learner-facing question is not “How do we make this native-like?” It is “What would move this from risky/under-B1 behavior to a defensible B1 response?”

For language criteria, the official rubric distinguishes roughly:

- **A:** B1 well fulfilled / upper part of target level;
- **B:** B1 fulfilled / target level;
- **C:** approximately A2;
- **D:** approximately A1 or below.

Bestehen therefore treats **B** as the central practical sufficiency anchor for routine coaching. A response with B-level communicative design and formal accuracy is not labelled “bad” merely because a premium model can rewrite it more elegantly.

### 3.4 Do not invent an official word-count threshold

**Decision:** Bestehen does not present an invented minimum or ideal word count as a TELC rule when the currently verified task does not state one.

Length is interpreted functionally:

- too little text may make required content impossible to cover or make the message incoherent;
- unnecessary length can increase time pressure and error exposure;
- sufficient length is whatever allows the learner to address the four points clearly in the available time.

Training may later surface empirically useful planning ranges as **coaching heuristics**, but they must be labelled as such and must not be scored as official criteria.

---

## 4. Prompt and Required-Content Model

### 4.1 One official task family, multiple practice scenario categories

**Decision:** At launch, Writing has one target task family — **reply/write an informal or semi-formal functional email with four content points** — but the exercise bank uses scenario categories to create breadth and prevent memorization.

These categories are **practice-generation and coverage categories**, not claims that TELC publishes separate official subtests:

| Scenario category | Typical communicative functions | Example content-point shapes |
|---|---|---|
| **Visit / invitation / social plan** | accept/decline, suggest activities, give practical advice, ask/answer arrangements | what to do; when; what to bring; preparation |
| **Arrange / change / cancel** | propose a time, explain a conflict, apologize, offer an alternative | reason; new time; alternative; confirmation |
| **Request information / help** | ask for details, explain need, specify constraints, request response | purpose; dates; conditions; specific questions |
| **Respond to information or an offer** | react, choose, justify, ask a follow-up, add a preference | choice; reason; question; next step |
| **Problem / complaint / resolution** | describe problem, explain impact, request action, propose resolution | what happened; consequence; requested solution; availability |
| **Personal update / experience / advice** | describe an event, give an opinion, recommend, explain future plan | experience; opinion/reason; advice; next action |
| **Study / work / course coordination** | explain situation, request/confirm arrangement, provide reason, clarify next step | context; availability; request; confirmation |

A generated prompt should normally test several communicative functions rather than four variants of “give information.” Corpus evidence should later re-rank category frequency and typical function combinations without turning frequency into learner weakness.

### 4.2 Recipient/register is a first-class prompt axis

Every Writing prompt explicitly defines:

- recipient relationship;
- informal or semi-formal register expectation;
- communicative purpose;
- source message/context;
- four required content points at P4;
- whether any point has multiple components;
- allowed preparation/support condition;
- time condition;
- blueprint/version provenance.

A prompt must not rely on hidden knowledge of who the recipient is. Register can be coached only if the relationship is clear.

### 4.3 Required content points are explicit structured targets

**Decision:** Every prompt stores each content point as a separately assessable semantic obligation rather than one unstructured instruction string.

For each point, the product needs to know conceptually:

- the learner-facing wording;
- the communicative intent, such as suggest, explain, request, advise, answer, justify, or confirm;
- required semantic component(s);
- acceptable interpretation space;
- whether a very brief treatment can still be sufficient;
- relationship to another content point, if they may reasonably be answered together;
- evaluator confidence when deciding whether the point was fulfilled.

This enables the coach to say **“You covered 3 of 4 points; the missing one is preparation for the trip”** instead of returning a vague “task completion: 75%.”

### 4.4 Content-point fulfillment states

Bestehen uses four coaching states per required point:

| State | Meaning | Official mapping use |
|---|---|---|
| **Fulfilled** | Relevant, meaningful, and understandable answer to the point | Counts toward Criterion I |
| **Partly fulfilled** | Some required meaning is present, but a material component is missing or too unclear | Does not automatically count as fully handled; evaluator must decide against rubric |
| **Not fulfilled** | Missing, irrelevant, contradictory to task need, or not understandable enough | Does not count |
| **Uncertain** | Evaluator cannot responsibly decide because meaning is ambiguous or the prompt/content metadata is weak | Lower evaluation confidence; do not fabricate precise scoring |

At P4, the official A/B/C/D mapping is based on the number of appropriately handled points. Bestehen preserves the underlying per-point result so repair can target the missing obligation rather than merely showing a band.

### 4.5 Lower-difficulty progression

The task mechanism remains recognizable while linguistic and production load change:

| Rung | Writing experience | Content points | Assistance / independence | Evidence claim |
|---|---|---:|---|---|
| **P0 Supported Foundation** | Short exam-shaped functional message using concrete familiar language | Usually 2 explicit points, occasionally 3 | Phrase bank/sentence starters/planning frame may be visible by default; open time | Supported production and basic content coverage |
| **P1 Guided A2** | Complete short email with simple sequencing and recipient awareness | Usually 3 points | Selective starters/checklist; light/on-request vocabulary support | Functional A2 writing with emerging independence |
| **P2 A2/B1 Bridge** | B1-shaped email with controlled language load and authentic communicative functions | 3–4 points | Most help on request; open original sentences; soft/generous timing | B1-shaped task handling with limited support |
| **P3 Independent B1** | Full original B1-equivalent email task | 4 points | No default answer-bearing help; practice timer and target-time probes | Independent B1 Writing evidence |
| **P4 Target Conditions** | Current verified TELC-equivalent target task | 4 points | Exact 30-minute condition; no coaching/model/template help during measured response; feedback after submission | Strong target-condition Writing evidence |

A scaffolded response can show useful progress, but it does not prove the same capability as an independently written P4 response.

---

## 5. Bestehen Evaluation Model and TELC Rubric Mapping

### 5.1 Official score and coaching dimensions stay separate

**Decision:** Bestehen produces two related outputs:

1. **TELC-aligned estimate:** predicted A/B/C/D for each of the three official criteria, raw-point equivalent where appropriate, and confidence.
2. **Coaching diagnosis:** finer internal dimensions that explain what to repair.

The finer dimensions must not be displayed as invented official sub-scores unless clearly labelled as Bestehen coaching evidence.

### 5.2 Rubric map

| Bestehen coaching dimension | What is judged | Primary TELC relationship | Product rule |
|---|---|---|---|
| **Task completion** | Number and adequacy of required content points; relevance to task/situation | Criterion I — Aufgabenbewältigung | Preserve each Leitpunkt separately; do not reward verbosity over adequacy |
| **Communicative success** | Can the recipient understand what the learner wants to say/do, and does the message achieve its purpose? | Cross-cutting, strongest in II and constrained by III | This is a coaching synthesis, not a fourth official criterion |
| **Structure / cohesion** | Logical order, connected content points, paragraphing/linear progression, useful connectors | Criterion II — Kommunikative Gestaltung | Prefer simple coherent linking over forced advanced connectors |
| **Vocabulary** | Sufficient range/precision for familiar task, functional phrases, paraphrase when needed | Criterion II | Penalize only where insufficiency/repetition materially restricts expression; native-like range not required |
| **Grammar / written accuracy** | Syntax, morphology, spelling, punctuation, and whether errors impede fast comprehension | Criterion III — Formale Richtigkeit | Weight errors by communicative impact and systematic recurrence, not raw error count |
| **Register / recipient fit** | Informal vs semi-formal relationship, consistent address/politeness, purpose-appropriate phrasing | Criterion II | A greeting alone cannot rescue wrong/inconsistent register |
| **Greeting / closing / email conventions** | Appropriate salutation, opening/closing behavior, recognizable email form where relevant | Mainly Criterion II | Important as text-type evidence; do not invent penalties for letter metadata not required by current rubric |
| **Timing / completion** | Whether a complete usable response is produced under the active time condition | Evidence condition feeding I–III and later readiness | Timing is not a fourth TELC criterion; it changes evidence realism and may cause omissions |

### 5.3 Task completion rules

Task completion is judged before surface correction.

- Every content point is checked independently.
- A short sentence may satisfy a point if it is relevant and understandable.
- Two points may be satisfied in one sentence when both meanings are present.
- If a point contains more than one component, one answered component can still provide partial coaching credit but must not automatically be called fully fulfilled.
- Repeating the prompt without adding a meaningful answer does not satisfy the point.
- A grammatically weak sentence can still satisfy the content point if its intended answer remains understandable.
- A beautiful paragraph that ignores the required point does not earn task-fulfillment credit.

### 5.4 Communicative-success rules

Communicative success asks whether a real recipient could follow and act on the message.

The coach considers:

- purpose is recognizable;
- response fits the situation;
- important information is understandable;
- references such as pronouns/time/place do not create critical ambiguity;
- requests, proposals, reasons, advice, or answers are sufficiently explicit;
- language errors do not repeatedly force the reader to guess.

This dimension is especially useful in feedback because it prevents the App from saying “grammar bad” when the email still works, or “all points covered” when the message is technically complete but practically confusing.

### 5.5 Structure / cohesion rules

B1-sufficient structure means a **clear linear message**, not sophisticated essay architecture.

Good-enough behavior includes:

- content points in a sensible order;
- simple paragraph breaks when useful;
- common connectors used correctly enough;
- sentences that do not read as four unrelated answers pasted together;
- basic reference and sequencing that lets the reader follow the message.

Do not push the learner toward decorative connector density. `und`, `aber`, `weil`, `deshalb`, `dann`, `zuerst`, `danach`, and similar common links are valuable when they genuinely connect meaning.

### 5.6 Vocabulary rules

B1-sufficient vocabulary means enough language to handle the familiar communicative purpose, sometimes using paraphrase.

The evaluator should distinguish:

- **gap:** learner cannot express an important required idea;
- **imprecise but functional:** meaning is understandable although a better word exists;
- **repetition:** only material when it noticeably constrains communication/cohesion;
- **wrong word/collocation:** important when it changes meaning or makes the phrase difficult to understand;
- **advanced improvement:** optional and not a default correction target.

### 5.7 Grammar and formal-accuracy rules

The evaluator must judge grammar through the official **primacy of comprehensibility** rather than surface cleanliness.

Errors are triaged by impact:

| Impact | Example effect | Default coaching priority |
|---|---|---|
| **Critical** | meaning is reversed, recipient cannot identify actor/time/request, or a content point becomes unintelligible | High |
| **Material** | comprehension slows or repeated system error makes several sentences uncertain | High/medium depending recurrence |
| **Minor** | obvious intended meaning; local ending/article/punctuation issue with little reading cost | Low unless recurrent and easy to repair |
| **Style-only** | grammatically acceptable but less elegant than a model response | No correction by default |

A response with systematic errors can still be B1-sufficient when intended meaning remains predominantly clear. Conversely, a short polished response that fails the task is not rescued by accuracy.

### 5.8 Register rules

Register is evaluated from the whole recipient relationship, not isolated pronouns.

The coach checks:

- address form (`du`/`Sie`) fits the defined relationship;
- salutation and closing fit the relationship;
- requests and politeness are appropriate enough;
- register does not oscillate materially;
- tone fits the purpose without requiring native-like nuance.

A single typo in a greeting is not equivalent to writing an informal message to a formal recipient throughout.

### 5.9 Greeting, closing, and email conventions

The learner should normally produce:

- an appropriate greeting;
- a brief opening that fits the prompt when useful;
- the message body covering the required content;
- an appropriate closing/farewell;
- a recognizable email-like communicative form.

Bestehen should teach an appropriate subject line as useful planning practice where the target task requests it, while avoiding false claims that sender/address/date/letter metadata are required scoring elements in the current rubric.

---

## 6. B1-Sufficiency Decision

### 6.1 Learner-facing verdict language

The App should avoid a single binary “pass/fail” label from one Writing sample. It uses a verdict such as:

- **Likely B1-sufficient for this task** — official-criterion estimate is centered on B or better with adequate evaluation confidence and no major task-validity issue;
- **Borderline / one repair away** — one criterion is near the B/C boundary, evidence is incomplete, or a small number of high-impact issues dominate;
- **Below B1 on this task** — one or more criteria show clear C/D-like behavior under the attempted condition;
- **Cannot judge reliably** — prompt, response, language, technical capture, or evaluator disagreement makes a responsible estimate impossible.

This is task-level evidence, **not a readiness declaration**. Stage 15 will decide how repeated samples combine into Writing/readiness estimates.

### 6.2 Do not average away a task failure

A response that is linguistically strong but fails the required content/situation must remain risky. Likewise, a response that covers all four points but is difficult to understand because of language control must remain risky. The three official criteria stay visible separately rather than being reduced immediately to an attractive single percentage.

### 6.3 Example rubric summary

> **Likely B1-sufficient for this task — moderate confidence**
>
> **Task management: B-like** — 3 of 4 content points are clearly covered. You missed what Marianne should do to prepare before the trip.
>
> **Communicative design: B-like** — the message is easy to follow and the register fits a friend. Two sections feel disconnected, but the purpose remains clear.
>
> **Formal accuracy: B-like** — several case/article errors are visible, but they do not stop understanding.
>
> **Best next move:** add the missing preparation point, then connect the final two ideas with one simple link. Do not rewrite the whole email.

---

## 7. Initial Definition-of-Done Coverage

The following Stage 12 product decisions are already captured above:

- current TELC B1 Writing format and scoring dimensions;
- prompt categories;
- explicit required content-point model;
- task completion;
- communicative success;
- structure/cohesion;
- vocabulary;
- grammar/formal accuracy;
- register;
- greeting/closing conventions;
- evaluation against B1 sufficiency rather than ideal/native German.

Correction presentation, correction limits, repair/rewrite, templates, timed mode, readiness evidence, AI evaluation calibration, and cost strategy are completed in the remainder of this document before Stage 12 is closed.
