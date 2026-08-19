# Bestehen / App — Stage 12: Writing Coaching

> **Status:** Authoritative Stage 12 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Writing promise:** Judge whether the learner's own message is likely good enough for B1, show the few changes most likely to protect or win exam points, and make the learner prove those changes in fresh writing rather than replacing their German with polished model prose.

## 1. Purpose and Scope

This document defines the complete learner-facing Writing coaching model for Bestehen / App. It turns the existing learner-model, Mistake Memory, daily-coaching, core-loop, and A1→B1 progression decisions into a concrete product contract for TELC B1 Writing.

Writing is a productive skill, so the App cannot rely on answer keys alone. It must evaluate open learner text while avoiding two failure modes:

1. grading every surface error as though B1 meant native-like German; and
2. returning an attractive rewritten answer that teaches little and then accidentally treating the model's German as learner evidence.

The central product question is:

**Would this response likely function well enough at TELC B1, what is most likely costing points, and what should the learner change themselves next?**

Stage 12 defines:

- the current TELC B1 target format and official rubric mapping;
- prompt/scenario categories and explicit required content points;
- Bestehen's finer coaching dimensions and their relationship to the official criteria;
- the B1-sufficiency standard;
- learner-facing correction presentation and correction limits;
- repair, learner revision, and fresh rewrite/transfer;
- reusable patterns and template guardrails;
- timed and target-condition Writing behavior;
- evidence passed into the learner model and later readiness model;
- evaluator consistency, calibration, confidence, disagreement, and failure handling;
- a low-cost AI strategy with deterministic checks, reuse/caching, batching, and selective stronger-model escalation.

This is product shaping rather than architecture. It does not choose a model vendor, prompt framework, editor implementation, storage design, API, queue, or final readiness formula.

### In scope

- informal and semi-formal TELC B1 email Writing;
- P0–P4 lower-difficulty and target-condition variants;
- task completion, communicative success, organization/cohesion, vocabulary, grammar/formal accuracy, register, and email conventions;
- correction prioritization and feedback examples;
- repair and fresh productive transfer;
- target-condition timing and assistance boundaries;
- Writing evidence and Mistake Memory outputs;
- AI evaluator quality and cost policy.

### Out of scope

- final cross-skill review scheduler — Stage 14;
- final TELC pass/readiness coefficients and evidence minimums — Stage 15;
- full-mock sequencing and complete written-exam simulation — Stage 16;
- ready-to-book thresholds — Stage 17;
- final coach copy system and information architecture — Stages 18–19;
- generalized content-generation QA across the App — Stage 21;
- final Corpus → App technical contract — Stage 22;
- final privacy/retention policy for raw learner text — Stage 24;
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
- AI/model corrections and model answers are **not learner evidence**. Only the learner's own original or subsequently revised production counts as learner production, and revision after answer/model exposure is weaker evidence than a clean fresh response.
- Mistake Memory requires a defensible cause and independent recurrence before a fine-grained known weakness is created.
- Same-item repetition and immediate post-model success are weak learning evidence. Retained repair requires fresh delayed transfer.
- The Daily Coaching Engine protects Writing evidence gaps, pass-critical weaknesses, due repair, realism progression, and coverage rather than favoring cheaper objective skills.
- The canonical loop prioritizes task fulfillment and comprehensibility over polishing every surface error and normally keeps repair within roughly 2–6 minutes, ordinarily under eight minutes.
- Stage 07 already requires Writing diagnosis to select at most one or two point-relevant repair targets and says a model answer is teaching material, not learner evidence.
- Stage 08 progression uses **P0 Supported Foundation → P1 Guided A2 → P2 A2/B1 Bridge → P3 Independent B1 Training → P4 Target Conditions**, by task family/capability profile rather than one global level.
- Assistance offered but unused does not weaken evidence. Assistance used before submission remains attached to the attempt.
- P3/P4 measured attempts defer coaching until submission; P4 uses exact target constraints.
- Real/reference material defines the target; learner practice should normally use original content when exact reuse rights are unclear.
- Bestehen is initially a personal project, so recurring premium-model calls must earn their cost.

No earlier App decision is materially changed by Stage 12.

---

## 3. Current TELC B1 Writing Target

### 3.1 Verification and versioning rule

The target was rechecked on **19 August 2026** against the official telc `Zertifikat Deutsch B1, Übungstest Version 1` and current official telc product information.

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

The current task instructions encourage planning the order and email form before writing. The scoring guidance treats the product as a personal or semi-formal email and evaluates whether the text fits that communicative situation.

Official references used for this Stage 12 verification:

- `https://www.telc.net/sprachpruefungen/deutsch/zertifikat-deutsch-telc-deutsch-b1/`
- `https://shop.telc.net/media/catalog/product/file/2/0/20201225_5061-b00-010301_web.pdf`

**Product rule:** exact target format, scoring, and timing are **versioned exam knowledge**. Before an attempt is labelled P4/target-condition or used as a readiness anchor, the App must rely on a currently verified target blueprint. A historical task may remain useful general Writing evidence after a format change, but it must not silently retain target-condition status.

### 3.2 What the official rubric means for Bestehen

The official three criteria are the scoring anchor. Bestehen may expose finer coaching dimensions, but it must not pretend those finer dimensions are additional official TELC criteria.

#### Criterion I — Aufgabenbewältigung / task management

The current rubric maps the four required content points directly to A–D:

| TELC band | Current task-management meaning |
|---|---|
| A | All four content points are handled appropriately |
| B | Three content points are handled appropriately |
| C | Two content points are handled appropriately |
| D | One or no content point is handled appropriately |

A content point can count even when treated briefly, provided it is relevant, meaningful, and understandable. Bestehen must therefore avoid teaching the false rule that every content point needs a long paragraph.

If the response has little or no connection to the prompt, the official rubric treats this as wrong topic and all criteria receive D. If the broad topic is present but the communicative situation is wrong, task management may be D while language criteria are still judged. Bestehen must preserve that distinction because it changes both diagnosis and evidence validity.

#### Criterion II — Kommunikative Gestaltung / communicative design

This criterion covers range and appropriateness of language, text logic, cohesion/coherence, connectors, register, vocabulary range, and realization of the communicative purpose. The target is not elaborate prose. A B1 response should be able to connect simple elements into a coherent linear message, use enough vocabulary for familiar purposes, and sustain an appropriate relationship with the recipient.

Personal/semi-formal email characteristics and register matter. Missing or unstable register, disconnected content points, and unusable linking can lower this criterion even when individual sentences are grammatically understandable.

#### Criterion III — Formale Richtigkeit / formal accuracy

This criterion covers grammatical control together with spelling, punctuation, and written-form accuracy. The official guidance gives **comprehensibility priority**: not every grammatical error has equal impact, and systematic errors can still be compatible with B1 when the intended meaning remains mostly clear.

That directly supports Bestehen's existing principle: correct what protects communication and exam points before polishing harmless imperfections.

### 3.3 B1 sufficiency is the target, not A-band perfection

**Decision:** Bestehen coaches toward **stable B1-sufficient performance**, with stronger A-band behavior welcomed but not required as the default repair target.

The learner-facing question is not “How do we make this native-like?” It is “What would move this from risky/under-B1 behavior to a defensible B1 response?”

For language criteria, the current official guidance distinguishes approximately:

- **A:** B1 well fulfilled / upper part of target level;
- **B:** B1 fulfilled / target level;
- **C:** approximately A2;
- **D:** approximately A1 or below.

Bestehen therefore treats **B** as the central practical sufficiency anchor for routine coaching. A B-like response is not labelled weak merely because a stronger model can rewrite it more elegantly.

### 3.4 Do not invent an official word-count threshold

**Decision:** Bestehen does not present an invented minimum or ideal word count as a TELC rule when the currently verified task does not state one.

Length is interpreted functionally:

- too little text may make required content impossible to cover or make the message incoherent;
- unnecessary length can increase time pressure and error exposure;
- sufficient length is whatever allows the learner to address the required points clearly in the available time.

Training may later surface empirically useful planning ranges as **Bestehen coaching heuristics**, but they must be labelled as such and must not be scored as official criteria.

---

## 4. Prompt and Required-Content Model

### 4.1 One official task family, multiple practice scenario categories

**Decision:** At launch, Writing has one target task family — **write/reply with an informal or semi-formal functional email addressing four content points** — but the practice bank uses scenario categories to create breadth and prevent memorization.

These are generation/coverage categories, not claims that TELC publishes separate Writing subtests:

| Scenario category | Typical communicative functions | Example content-point shapes |
|---|---|---|
| **Visit / invitation / social plan** | accept/decline, suggest activities, give practical advice, arrange | what to do; when; what to bring; preparation |
| **Arrange / change / cancel** | propose a time, explain a conflict, apologize, offer an alternative | reason; new time; alternative; confirmation |
| **Request information / help** | ask for details, explain need, specify constraints, request response | purpose; dates; conditions; questions |
| **Respond to information or an offer** | react, choose, justify, ask a follow-up, state preference | choice; reason; question; next step |
| **Problem / complaint / resolution** | describe a problem, explain impact, request action, propose resolution | what happened; consequence; requested action; availability |
| **Personal update / experience / advice** | describe an event, give opinion, recommend, explain future plan | experience; opinion/reason; advice; next action |
| **Study / work / course coordination** | explain situation, request/confirm arrangement, provide reason, clarify next step | context; availability; request; confirmation |

A generated prompt should normally test several communicative functions rather than four variants of “give information.” Corpus evidence may later re-rank category frequency and function combinations without turning frequency into learner weakness.

### 4.2 Recipient/register is a first-class prompt axis

Every Writing prompt explicitly defines:

- recipient relationship;
- informal or semi-formal register expectation;
- communicative purpose;
- source message/context;
- four required content points at P4;
- whether any point has multiple semantic components;
- allowed preparation/support condition;
- time condition;
- target blueprint/version provenance.

A prompt must not rely on hidden knowledge of who the recipient is. Register can be coached only if the relationship is clear.

### 4.3 Required content points are explicit structured targets

**Decision:** Every prompt represents each content point as a separately assessable semantic obligation rather than one unstructured instruction string.

For each content point, the product must conceptually know:

- learner-facing wording;
- communicative intent — e.g. suggest, explain, request, advise, answer, justify, confirm;
- required semantic component(s);
- acceptable interpretation space;
- whether brief treatment can still be sufficient;
- whether it may reasonably be combined with another point;
- evaluator confidence when deciding fulfillment.

This enables the coach to say **“You covered 3 of 4 points; the missing one is how your friend should prepare for the trip”** rather than returning a vague “task completion: 75%.”

### 4.4 Content-point fulfillment states

| State | Meaning | Scoring use |
|---|---|---|
| **Fulfilled** | Relevant, meaningful, and understandable answer to the point | Counts toward Criterion I |
| **Partly fulfilled** | Some required meaning exists, but a material component is missing or too unclear | Useful coaching evidence; does not automatically count as fully handled |
| **Not fulfilled** | Missing, irrelevant, contradictory to task need, or not understandable enough | Does not count |
| **Uncertain** | Evaluator cannot responsibly decide because meaning or content metadata is ambiguous | Lower confidence; do not fabricate precision |

At P4, the official A/B/C/D estimate follows appropriately handled content points. Bestehen preserves the per-point state so repair can target the missing obligation rather than merely showing a band.

### 4.5 Lower-difficulty progression

| Rung | Writing experience | Typical content points | Assistance / independence | Evidence claim |
|---|---|---:|---|---|
| **P0 Supported Foundation** | Short exam-shaped functional message using concrete familiar language | 2, occasionally 3 | Phrase bank/sentence starters/planning frame may be visible by default; open time | Supported production and basic content coverage |
| **P1 Guided A2** | Complete short email with simple sequencing and recipient awareness | Usually 3 | Selective starters/checklist; light/on-request vocabulary support | Functional A2 Writing with emerging independence |
| **P2 A2/B1 Bridge** | B1-shaped email with controlled language load and authentic communicative functions | 3–4 | Most help on request; open original sentences; soft/generous timing | B1-shaped task handling with limited support |
| **P3 Independent B1** | Full original B1-equivalent email task | 4 | No default answer-bearing help; practice timing and target-time probes | Independent B1 Writing evidence |
| **P4 Target Conditions** | Current verified TELC-equivalent target task | 4 | Exact 30-minute condition; no coaching/model/template help during measured response; feedback after submission | Strong target-condition Writing evidence |

A scaffolded response can show useful progress, but it does not prove the same capability as an independently written P4 response.

---

## 5. Evaluation Model and TELC Rubric Mapping

### 5.1 Official estimate and coaching dimensions stay separate

**Decision:** Bestehen returns two related outputs:

1. **TELC-aligned estimate:** predicted A/B/C/D for each official criterion, optional raw-point equivalent where appropriate, and evaluation confidence.
2. **Coaching diagnosis:** finer internal dimensions that explain what to repair.

The finer dimensions are never presented as invented official TELC sub-scores.

### 5.2 Rubric map

| Bestehen coaching dimension | What is judged | Primary TELC relationship | Product rule |
|---|---|---|---|
| **Task completion** | Number and adequacy of required content points; relevance to task/situation | Criterion I — Aufgabenbewältigung | Preserve each Leitpunkt separately; do not reward verbosity over adequacy |
| **Communicative success** | Can the recipient understand what the learner wants to say/do and does the message achieve its purpose? | Cross-cutting synthesis, strongest in II and constrained by III | This is coaching interpretation, not a fourth official criterion |
| **Structure / cohesion** | Logical order, connected content points, linear progression, useful connectors | Criterion II — Kommunikative Gestaltung | Prefer simple coherent linking over forced advanced connectors |
| **Vocabulary** | Sufficient range/precision for familiar task, functional phrases, paraphrase when needed | Criterion II | Penalize insufficiency that restricts expression; native-like range is not required |
| **Grammar / written accuracy** | Syntax, morphology, spelling, punctuation, and effect of errors on comprehension | Criterion III — Formale Richtigkeit | Weight communicative impact and recurrence, not raw error count |
| **Register / recipient fit** | Informal vs semi-formal relationship, address/politeness consistency, purpose-appropriate phrasing | Criterion II | A greeting alone cannot rescue wrong/inconsistent register |
| **Greeting / closing / email conventions** | Appropriate salutation, opening/closing behavior, recognizable email form where relevant | Mainly Criterion II | Important text-type evidence; do not invent penalties for metadata not required by current scoring guidance |
| **Timing / completion** | Whether a complete usable response is produced under the active time condition | Evidence condition feeding I–III and readiness | Timing is not a fourth TELC criterion |

### 5.3 Task-completion rules

Task completion is judged before surface correction.

- Every required point is checked independently.
- A short sentence can satisfy a point if it is relevant and understandable.
- Two points may be satisfied in one sentence when both meanings are present.
- A point with multiple required components may be only partly fulfilled when a material component is absent.
- Repeating the prompt without adding a meaningful answer does not satisfy the point.
- A grammatically weak sentence can still satisfy the point when its intended answer is clear.
- A polished paragraph that ignores the required point earns no task-fulfillment credit for that point.

### 5.4 Communicative-success rules

Communicative success asks whether a real recipient could follow and act on the message.

The coach considers whether:

- purpose is recognizable;
- response fits the situation;
- important information is understandable;
- references to actor/time/place do not create critical ambiguity;
- requests, proposals, reasons, advice, or answers are explicit enough;
- errors do not repeatedly force the reader to guess.

This dimension prevents the App from saying “grammar bad” when the email still works or “all points covered” when the message is technically complete but practically confusing.

### 5.5 Structure / cohesion rules

B1-sufficient structure means a **clear linear message**, not sophisticated essay architecture.

Good-enough behavior includes:

- content points in a sensible order;
- simple paragraph breaks where useful;
- common connectors used correctly enough;
- sentences that do not read as four unrelated answers pasted together;
- basic sequencing/reference that lets the reader follow the message.

Do not push decorative connector density. Simple links such as `und`, `aber`, `weil`, `deshalb`, `dann`, `zuerst`, and `danach` are valuable when they genuinely connect meaning.

### 5.6 Vocabulary rules

B1-sufficient vocabulary means enough language to handle the familiar communicative purpose, sometimes using paraphrase.

Distinguish:

- **gap:** learner cannot express an important required idea;
- **imprecise but functional:** a better word exists, but intended meaning is clear;
- **repetition:** material only when it noticeably constrains communication/cohesion;
- **wrong word/collocation:** important when it changes meaning or makes a phrase hard to understand;
- **advanced improvement:** optional, never a default repair target.

### 5.7 Grammar and formal-accuracy rules

The evaluator judges grammar through **primacy of comprehensibility**, not surface cleanliness.

| Impact | Effect | Default priority |
|---|---|---|
| **Critical** | Meaning is reversed; actor/time/request becomes unclear; content point becomes unintelligible | High |
| **Material** | Comprehension noticeably slows or a repeated system error makes several sentences uncertain | High/medium |
| **Minor** | Intended meaning remains obvious; local ending/article/punctuation issue has little reading cost | Low unless recurrent and easy to repair |
| **Style-only** | Grammatically acceptable but less elegant than a model response | No correction by default |

A response with systematic errors can still be B1-sufficient when intended meaning remains predominantly clear. Conversely, a short polished response that fails the task is not rescued by accuracy.

### 5.8 Register rules

Register is evaluated from the whole recipient relationship, not isolated pronouns.

Check whether:

- address form (`du`/`Sie`) fits the relationship;
- salutation and closing fit;
- requests/politeness are appropriate enough;
- register does not oscillate materially;
- tone fits purpose without requiring native-like nuance.

A single typo in a greeting is not equivalent to using the wrong relationship throughout the email.

### 5.9 Greeting, closing, and email conventions

The learner should normally produce:

- an appropriate greeting;
- a brief opening where useful;
- a body that covers the required points;
- an appropriate closing/farewell;
- a recognizable email-like communicative form.

The current task material may encourage a subject line as part of planning. The current scoring guidance does **not** require Bestehen to invent standalone penalties for letter metadata such as sender, recipient, date, or subject line. These can be taught as useful form where relevant without being misrepresented as separate official scoring points.

---

## 6. B1-Sufficiency Decision

### 6.1 Learner-facing verdict

One Writing sample does not receive a global “you will pass Writing” label. Use one of four task-level verdicts:

| Verdict | Meaning |
|---|---|
| **Likely B1-sufficient for this task** | Official-criterion estimate is centered on B or better with adequate evaluator confidence and no major validity issue |
| **Borderline / one repair away** | One criterion is near the B/C boundary, evidence is incomplete, or a small number of high-impact issues dominate |
| **Below B1 on this task** | One or more criteria show clear C/D-like behavior under the attempted condition |
| **Cannot judge reliably** | Prompt, response, language, technical capture, or evaluator disagreement prevents a responsible estimate |

This is task evidence, not a readiness declaration. Stage 15 decides how repeated samples combine.

### 6.2 Do not average away task failure

A linguistically strong response that misses the required task/situation remains risky. A response that covers all points but is hard to understand also remains risky. The three official criteria stay visible rather than collapsing immediately into one flattering percentage.

Stage 12 does **not** invent a separate official Writing pass gate that TELC does not define. Later readiness logic may model Writing risk inside the written component, but must preserve the actual target scoring structure.

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

## 7. Correction Presentation

### 7.1 Layer feedback from exam consequence to language detail

**Decision:** Writing feedback appears in this order:

1. **B1-sufficiency verdict + confidence** — the direct answer to “good enough for B1?”
2. **Three official criterion estimates** — A/B/C/D-like with short evidence-based reasons.
3. **Content-point coverage** — four explicit states at P4; identify the exact missing/uncertain point.
4. **The one or two corrections that matter most now** — point-protecting, learnable, and evidence-backed.
5. **Targeted annotations in the learner's own text** — only where they support those priorities.
6. **Optional “Other notes”** — minor or stylistic observations, collapsed by default.
7. **Next action** — revise, micro-repair, fresh check, or move on.

The first screen/view must not be a wall of red underlines.

### 7.2 Correction emphasis limit

**Decision:** A normal Writing response emphasizes **two** correction targets. The hard maximum is **three** only when a distinct missing task obligation must be shown alongside two independent point-relevant language/communication issues.

The active Repair step still follows Stage 07: **one primary and at most one secondary repair target**.

Priority order:

1. wrong topic/situation or missing required content;
2. meaning/communicative failure;
3. register/text-type failure that materially affects Criterion II;
4. repeated grammar/vocabulary/structure issue with B1 scoring impact;
5. timing/checking behavior causing omission/incompletion;
6. isolated minor language errors;
7. style-only improvements.

Items 6–7 are normally not emphasized when higher-value work exists.

### 7.3 Show minimal correction, not replacement prose

For a selected language issue, feedback uses:

- the learner's original phrase;
- the smallest useful correction or contrast;
- one sentence explaining why it matters;
- a quick learner action when needed.

Example:

> **Your sentence:** `Ich kann nicht kommen weil ich muss arbeiten.`
>
> **Repair:** `Ich kann nicht kommen, weil ich arbeiten muss.`
>
> **Why this matters:** the message was understandable, so this is not a task failure. The recurring pattern is verb position after `weil`; fix that pattern rather than rewriting the paragraph.

### 7.4 Feedback examples

#### B1-sufficient despite errors

Learner excerpt:

> `Liebe Anna, danke für deine Einladung. Ich komme sehr gern. Am Samstag können wir im Park gehen und danach etwas essen. Ich bringe auch Kuchen mit. Was soll ich noch mitbringen? Viele Grüße, Samir`

Coach behavior:

> **Likely B1-sufficient.** The message works, the relationship is appropriate, and the required ideas are understandable. `im Park gehen` should be `in den Park gehen`, but that one error does not make the email below B1. Fix it, then move to a fresh task rather than polishing every sentence.

#### Missing content point outranks grammar

> **Main issue: task management.** Your German is understandable, but you answered only three required points. Add **how your friend should prepare** before spending time on article endings. Missing that point can cost more than the minor grammar errors in this message.

#### Register mismatch

> **Main issue: recipient fit.** The task is to write to a course organizer, but the email switches between `du` and `Sie`. Choose one semi-formal relationship and keep it consistent. Your vocabulary does not need to become more advanced.

#### Too many surface errors

> I found more language errors than we should repair at once. Two patterns matter most: **verb position after subordinate connectors** and **unclear requests**. We will repair those now; the remaining minor endings are saved as observations and will only become priorities if they recur.

### 7.5 Full corrected/reference versions are optional and delayed

A fully corrected or model response is **not** the default feedback artifact.

If the learner explicitly asks to see one, or the coach determines that a reference is useful after the learner has attempted a revision:

- label it **Reference version — not your score or evidence**;
- keep it B1-appropriate rather than turning it into C1 prose;
- highlight only the patterns relevant to the repair;
- record model/reference exposure;
- treat same-prompt production after exposure as guided/weak evidence;
- require fresh unexposed writing for independent transfer.

---

## 8. Repair and Rewrite Workflow

### 8.1 Canonical flow

**Decision:** Writing uses the common loop with two distinct productive follow-ups: **learner revision** and **fresh rewrite/transfer**.

1. **Observe** — show purpose, recipient, content points, time condition, and permitted support without giving answer-bearing language.
2. **Attempt** — learner writes their own message; original submission is locked as the evidence event.
3. **Diagnose** — score/estimate the three official criteria, explicit content points, and supported coaching dimensions; choose one primary and at most one secondary target.
4. **Repair** — 2–6 minute narrow intervention, ordinarily under eight minutes.
5. **Learner revision** — learner changes the relevant part of their own response. This is controlled/guided practice and proves responsiveness, not independent mastery.
6. **Fresh rewrite / Retry** — use new content requiring the same underlying behavior, with no answer-bearing exposure. This may be a compact new message/paragraph or a complete fresh email depending on the target.
7. **Remember** — record what transferred, what remains uncertain, and when a delayed fresh Writing check is due.

### 8.2 Repair type by diagnosed cause

| Diagnosis | Narrow repair | Fresh productive check |
|---|---|---|
| Missing content point / checking strategy | Reconstruct the four obligations; create a tiny pre-submit checklist | Different prompt with new content points; learner checks all before submit |
| Communicative purpose unclear | State what the recipient must understand/do; rewrite one request/proposal | New request/proposal to a different recipient/context |
| Structure/cohesion | Reorder 3–4 message ideas; add only the needed simple connector | New compact email requiring logical sequence |
| Vocabulary gap | Supply/contrast the needed functional phrase or paraphrase route | New topic requiring the same function with different surface vocabulary |
| Grammar pattern | One practical rule + one controlled contrast | New sentence/message segment where learner produces the pattern spontaneously |
| Register | Contrast informal/semi-formal address and one request/closing | Fresh recipient relationship requiring the corrected register |
| Greeting/closing | Pick/build an appropriate pair for the recipient | New email where learner supplies them without a bank |
| Timing/incompletion | Plan obligations, prioritize content, use a final check | Fresh timed task; preserve language level while changing timing condition |
| Cause unresolved | One small clarifier or another fresh sample | Do not buy or invent a fine repair prematurely |

### 8.3 When a full fresh email is required

A compact retry can prove one targeted behavior in the same session. A **complete fresh email** is required before claiming broader improvement in:

- overall task fulfillment;
- full communicative design;
- sustained register;
- complete target-time execution;
- readiness-grade Writing performance.

### 8.4 Same-prompt revision is valuable but weak for readiness

Learner revision after feedback can show:

- understanding of the correction;
- ability to apply the specific repair;
- self-editing skill;
- whether the repair made the message clearer.

It does **not** prove the learner would have produced the same behavior independently on a new exam task. It therefore remains lower-strength evidence than fresh unassisted transfer.

### 8.5 Do not force endless rewrites

If the learner fails the same target after one useful re-diagnosis inside the Stage 07 loop cap:

- stop the same-session cycle;
- preserve the evidence;
- schedule a better-sized focused block or prerequisite;
- do not demand a third/fourth rewrite merely to obtain a green state.

---

## 9. Reusable Patterns and Templates

### 9.1 Teach functions, not one memorized letter

**Decision:** Bestehen provides a **functional pattern library**, not a universal model email to memorize.

Useful pattern families include:

- greeting a friend vs semi-formal recipient;
- acknowledging the incoming message;
- giving a reason;
- accepting/declining;
- proposing a time/activity;
- asking for information;
- giving advice;
- explaining a problem;
- offering an alternative;
- linking sequence/contrast/cause;
- closing appropriately.

Patterns should have several natural variants so the learner practices choice and adaptation.

### 9.2 Safe planning skeleton

A reusable planning pattern may be:

1. recipient/register;
2. brief opening/response to context;
3. the four required content obligations in a sensible order;
4. one or two simple links where needed;
5. closing;
6. final content-point/register check.

This is a **planning behavior**, not a script containing answer language.

### 9.3 Template availability by progression rung

| Rung | Template behavior |
|---|---|
| **P0** | Visible sentence frames/phrase bank and content checklist may be default; evidence is explicitly assisted |
| **P1** | Selective frames and functional phrase choices; learner fills more original language |
| **P2** | Planning skeleton is visible; phrase bank is optional/on request and marks affected production assisted |
| **P3** | No default answer-bearing template; learner may use a neutral four-point planning checklist; phrase help makes ordinary practice assisted |
| **P4** | No App-provided phrase bank, model, grammar hint, or answer-bearing template during the measured response; only target-permitted conditions apply |

### 9.4 Responsible-template guardrails

- Do not promise that a memorized opening/closing guarantees points.
- Do not teach advanced stock phrases merely because they look impressive.
- Do not require the same connector in every email.
- Do not penalize ordinary learned phrases that are appropriately adapted; reusable language is normal exam preparation.
- If a long memorized block is poorly adapted to the prompt, score what it actually communicates; do not reward it for complexity.
- If model/reference language was exposed in the current learning episode, preserve that support condition.
- A template can reduce planning load; it must not make missing content points invisible.

---

## 10. Timed Writing Mode

### 10.1 Timing ladder

Writing follows Stage 08 rather than inventing a parallel timing model:

| Mode | Typical rung | Behavior | Evidence meaning |
|---|---|---|---|
| **Open Writing** | P0–P1 | No countdown pressure; elapsed time may be observed for planning | Language/task learning, no target-time claim |
| **Pace awareness** | P1–P2 | Soft guidance or post-task pace feedback; no punitive cutoff | Early execution evidence |
| **Practice timed** | P2–P3 | Visible generous target, consistent with Stage 08's roughly 125–150% transition where comparable | Timed practice; over-target response remains valid learning evidence |
| **Target-time probe** | P3 | Full B1-equivalent prompt, no learning help, target-time or near-target condition | Strong independent B1/timing evidence |
| **P4 target condition** | P4 | **Exact current 30-minute Writing condition**, no coaching during the attempt | Strongest standalone Writing evidence before/inside mocks |

For full-task P3 practice, Stage 08's approximately 110–125% range may be used while the learner is transitioning to the exact 30-minute condition. Those ratios are **Bestehen progression defaults**, not official TELC time rules.

### 10.2 Time-management coaching

The coach teaches a simple behavior:

- identify recipient and four obligations before writing;
- spend most of the available time producing a complete understandable response;
- reserve a final moment to check missing points, register, and one or two recurring language risks.

Bestehen may later personalize the split from learner evidence. It must not present a fixed “X minutes planning / Y writing / Z checking” allocation as an official TELC rule.

### 10.3 Target-condition assistance boundary

During clean P4 Writing:

- no model response;
- no sentence starters or phrase bank;
- no translation/grammar hints;
- no coach feedback before submission;
- no language-correcting feature that materially supplies German the learner did not produce, unless a later verified target/accommodation policy explicitly permits it;
- feedback and repair begin after the measured response is finished.

Basic input/accessibility support that does not change the linguistic capability is treated separately and is finalized by Stage 25.

If autocorrection, translation, or another language-changing aid is used in a way that affects the response, the attempt can remain useful practice but must not be labelled clean P4 evidence.

### 10.4 Timeout, pause, and interruption

- A response unfinished at 30 minutes is evaluated **as submitted/observable**, with incompletion and timing preserved.
- Timed incompletion does not automatically become a grammar weakness.
- A learner may continue after time in ordinary practice, but the completed-after-time version is not identical to 30-minute target evidence.
- Pausing a measured response for a non-exam-like reason converts it to interrupted/practice evidence unless Stage 16/25 later defines an equivalent condition.
- Technical interruption that materially changes fairness invalidates or qualifies timing evidence rather than penalizing the learner.
- An unsubmitted draft is not silently scored as a completed exam response.

---

## 11. Writing Evidence and Readiness Handoff

### 11.1 Evidence emitted by a valid Writing attempt

| Evidence group | Required product meaning |
|---|---|
| Target | Writing section/task family, target blueprint/version |
| Prompt | Category, communicative purpose, recipient/register, four content-point definitions |
| Response | Learner text, completeness/submission state, descriptive length |
| Official estimate | Criterion I/II/III predicted band and raw-equivalent where appropriate |
| Content coverage | Per-point fulfilled/partly/not/uncertain plus evidence/rationale |
| Coaching dimensions | Communicative success, structure, vocabulary, grammar impact, register, conventions, timing |
| Assistance | Phrase bank/template/translation/grammar/model/reference support offered and used |
| Timing | Open/practice/target mode, elapsed time, within/over target, pause/interruption |
| Independence | Original attempt, same-prompt revision, immediate fresh retry, delayed transfer, repeated/exposed prompt |
| Evaluation | Deterministic/AI/human method, evaluator version, confidence, supported dimensions, disagreement flags |
| Validity/quality | Prompt ambiguity, language-detection, technical issues, content quality, target-version validity |
| Diagnosis | Primary manifestation/cause, optional contributor, confidence/unresolved state |
| Repair | Repair type, model exposure, learner revision result |
| Provenance | Diagnostic/daily/review/P3/P4/mock context and date |

Word count may be stored as descriptive execution metadata; it is not an invented scoring criterion.

### 11.2 Evidence-strength ordering

The later learner/readiness model should preserve approximately this order, consistent with Stage 04:

1. **Excluded:** invalid prompt/evaluator/technical attempt — no learner impact.
2. **Weak learning signal:** same-prompt revision after detailed feedback/model exposure; heavy phrase-bank dependence.
3. **Standard/bridge evidence:** valid assisted or untimed fresh response at P1/P2; useful for coaching/progression.
4. **Strong direct evidence:** fresh unassisted B1-equivalent P3 response with trustworthy evaluation.
5. **Target-condition anchor:** recent P4/current-target 30-minute response with no answer-bearing support and high evaluation quality.

A high-quality fresh mock Writing response may also be a target-condition anchor under Stage 16.

### 11.3 How Writing affects readiness

**Decision:** Writing contributes only to the **written** side of TELC readiness. It never raises oral readiness.

Stage 12 supplies:

- current official-criterion behavior;
- task/category/register coverage;
- B1-sufficiency history;
- assistance dependence;
- timing/completion evidence;
- evaluator confidence;
- recency/freshness;
- recurring task/communication/language bottlenecks;
- P3/P4/mock realism.

Stage 15 decides the final numerical/ordinal aggregation, section weighting, minimum evidence, confidence, and written pass-risk model.

### 11.4 Readiness guardrails

- One B1-sufficient email is **not** “Writing ready.”
- Diagnostic and guided revisions have low readiness weight even when the final text looks good.
- Multiple prompts/contexts are needed before strong generalization; exact minimums belong to Stage 15.
- Evidence should include both recipient/register conditions relevant to the target bank over time rather than only one memorized scenario.
- Stronger evidence replaces—not erases—the historical supported journey.
- A recurring C/D-like criterion or repeated timed incompletion remains a visible Writing risk; it must not be hidden by averaging minor strengths.
- Conversely, Stage 12 must not invent a standalone official Writing pass threshold. Stage 15 models how Writing affects the real written-component pass constraint.
- Low-confidence AI evaluation contributes less or nothing to a readiness movement until clarified.
- Same-prompt model-exposed revision can demonstrate learning but cannot anchor readiness.
- P4 target-condition evidence should be prioritized before strong ready-to-book language.

### 11.5 Learner-facing readiness wording examples

> **Writing is improving, but target-time evidence is still thin.** Your last two unassisted messages were B1-like, but only one was completed in the 30-minute condition. A fresh timed task will tell us whether the pace is reliable.

> **Task management is the current Writing risk.** Your language is generally understandable, but required points were missed in two recent fresh messages. We will repair the checking behavior before another target-condition sample.

> **This revision is better, but it is learning evidence.** You corrected the register after feedback. A new email to a different recipient will show whether you can do it independently.

---

## 12. AI Evaluation Consistency and Calibration

### 12.1 AI is an evaluator, not the source of truth

**Decision:** AI evaluation is versioned, benchmarked, confidence-aware, and bounded by the official rubric plus deterministic validity rules. A model may help interpret open language; it cannot silently invent a fourth TELC criterion, impose native-level style, or override an invalid prompt.

The normal evaluation output must be structured enough to reproduce the coaching decision:

- Criterion I/II/III predicted band;
- per-content-point status;
- supported coaching dimensions;
- one primary and optional one contributing diagnosis;
- selected correction targets and impact;
- evaluation confidence and uncertainty reason;
- wrong-topic/wrong-situation/invalid flags;
- evidence snippets/rationales sufficient for human review without requiring hidden reasoning.

### 12.2 Deterministic checks happen before AI

Before paying for open-text evaluation, handle cheaply where possible:

- prompt/version validity;
- response exists and is submitted;
- timing/assistance/model-exposure state;
- descriptive length;
- obvious technical corruption;
- exact target-condition eligibility;
- known prompt content-point metadata;
- cached evaluation lookup.

Greeting/closing presence may be detected deterministically as a weak signal, but semantic appropriateness, implicit content-point fulfillment, clarity, register, and B1 language quality normally require contextual evaluation.

### 12.3 Calibration corpus

Before an evaluator version is allowed to materially influence readiness, maintain a **rights-safe human-reviewed Writing benchmark** that deliberately covers:

- official A/B/C/D behavior for all three criteria;
- especially the **B/C sufficiency boundary**;
- all major practice scenario categories;
- informal and semi-formal recipients;
- all four/three/two/one-point coverage patterns;
- wrong-topic and wrong-situation cases;
- clear vs ambiguous content-point paraphrases;
- B1-sufficient responses with many harmless errors;
- polished but task-incomplete responses;
- common grammar/vocabulary/register/cohesion failures;
- timed incompletion;
- short and long-but-functional responses;
- non-native but understandable phrasing.

The set can begin small for the personal project and expand where evaluator errors appear. Exact benchmark size is an implementation/validation choice; **coverage of the decision boundaries is mandatory, raw quantity is not a substitute**.

Where affordable, the highest-value B/C boundary subset should be reviewed by two competent German evaluators, ideally including telc-familiar assessment experience. Routine learner attempts do not require two humans.

### 12.4 Initial evaluator quality gates

These are **Bestehen launch QA gates**, not official psychometric claims. They are intentionally concrete so Stage 26 can detect regression and later recalibrate them.

On the human-reviewed benchmark, an evaluator used for scored practice should initially achieve:

| Measure | Initial gate |
|---|---:|
| Per-content-point fulfilled/not-fulfilled decision agreement | **≥ 90%** |
| Official criterion-band exact agreement | **≥ 80%** |
| Official criterion-band agreement within one adjacent band | **≥ 95%** |
| Gross disagreement of two or more bands | **≤ 5%** |
| B1-sufficiency classification agreement around B-or-better vs C/D | **≥ 90%** on the deliberately sampled boundary set |

For **readiness-grade** use, the evaluator must also show no obvious systematic tendency to over-score B/C boundary responses. If false B1-sufficient judgments cluster in a category/register/error type, that slice is downgraded or escalated until repaired even when aggregate metrics pass.

These thresholds are starting product defaults. Stage 26 should change them only with evidence about learner outcomes, human agreement, and the cost/benefit of stricter evaluation.

### 12.5 Consistency requirements

- Cache an evaluation for the same response + prompt version + rubric version + evaluator version + relevant condition context so the learner does not receive a different score merely by reopening the page.
- Re-run the benchmark whenever the evaluator model, instructions, rubric mapping, or post-processing changes materially.
- Track exact-band, adjacent-band, B/C-boundary, and content-point disagreement separately.
- Record evaluator version with evidence so later calibration can reinterpret old results without rewriting history silently.
- Do not repeatedly rescore the same learner response to hunt for a preferred result.
- If evaluation changes after a model upgrade, preserve the original learner-visible event and clearly version any recalibrated readiness interpretation.
- Style preference differences must not cause score instability when official behavior is unchanged.

### 12.6 Confidence and escalation

Return **high / medium / low** evaluation confidence based on:

- prompt validity and metadata quality;
- clarity of content-point evidence;
- distance from A/B/C/D boundaries;
- consistency among rubric signals;
- evaluator benchmark performance for the relevant slice;
- unusual language/code-switching or ambiguous meaning;
- conflict with a second evaluator when one is invoked.

Escalate only when the decision matters:

- likely B/C boundary on a P4/mock/readiness sample;
- low confidence on a sample that could materially move written readiness;
- strong conflict with recent high-quality Writing evidence;
- learner disputes a plausible high-impact judgment;
- evaluator slice is known to be weak;
- first/cheap evaluator returns contradictory criterion/content-point outputs.

A low-confidence ordinary practice response normally gets another fresh sample or broad feedback rather than an expensive arbitration.

### 12.7 Disagreement policy

When two evaluators disagree materially:

1. check prompt/response validity and deterministic metadata first;
2. if one output violates the explicit rubric/content-point facts, discard it;
3. if disagreement is one adjacent band and not readiness-critical, show a range/borderline state with lower confidence;
4. if a B/C or ≥2-band disagreement can materially affect readiness, use the configured stronger evaluator or human calibration path once;
5. store the resolution and do not continue model-voting indefinitely;
6. if uncertainty remains, preserve **cannot judge reliably** and collect a fresh sample.

Uncertainty is preferable to false scoring precision.

---

## 13. Low-Cost Evaluation Modes

### 13.1 Four product modes

| Mode | Cost | What learner receives | Readiness effect |
|---|---|---|---|
| **W0 — Self-check / deterministic** | Near zero | Content-point checklist, timing/completeness facts, stored draft, reviewed generic reminders; no claimed rubric score | None until a trustworthy evaluation exists |
| **W1 — Standard evaluated practice** | One low-cost structured evaluation on submit | TELC-aligned criterion estimate, content-point coverage, top corrections, repair inputs | Normal practice evidence weighted by conditions/confidence |
| **W2 — Strengthened evaluation** | Cheap first pass + one stronger/second evaluator only when trigger fires | Higher-confidence boundary/high-impact decision | Eligible for stronger P4/mock/readiness contribution when quality is adequate |
| **W3 — Human calibration / rare review** | Manual bounded cost/time | Benchmark labels, disputed exemplar review, evaluator QA | Calibration source; not a routine per-attempt product requirement |

### 13.2 Standard practice should be one call, not a chain

A normal submitted Writing response should require at most **one low-cost model evaluation** that returns all supported information needed for:

- official criterion estimate;
- content-point coverage;
- coaching dimensions;
- diagnosis/cause confidence;
- correction priorities;
- repair selection inputs;
- learner-model/Mistake-Memory update.

Do **not** make separate routine calls for scoring, correction, explanation prose, Mistake Memory, readiness update, and tomorrow's plan.

### 13.3 Stronger model justification

A stronger/more expensive evaluator is justified when **both** are true:

1. the sample is high-value — P4, mock, readiness/ready-to-book evidence, or a genuinely disputed important judgment; and
2. the cheap evaluator is too uncertain, contradictory, or known to be weak for that slice.

It is not justified merely because the response contains many grammar errors or because premium prose sounds nicer.

### 13.4 Caching and reuse

Cache/reuse:

- evaluation result for unchanged response/prompt/rubric/evaluator version;
- common feedback templates;
- reviewed repair patterns;
- functional phrase/pattern banks;
- benchmark evaluations for regression testing;
- pre-generated prompt pools and fresh equivalents;
- optionally reviewed B1 reference responses for teaching after learner revision.

A learner reopening feedback or repeating a view should not create another model charge.

### 13.5 Batching

Batch where interactivity is not required:

- generation of original Writing prompts and variants;
- rubric-aligned exemplar creation;
- benchmark regression runs;
- offline ambiguity/content-point metadata review;
- expansion of thin prompt categories;
- periodic evaluator quality sampling.

Do not delay a submitted learner response merely to force interactive evaluations into a large batch if one low-cost call is already affordable. Cost optimization should not damage the core coaching loop.

### 13.6 Zero/low-cost fallback when AI is unavailable

If open-text evaluation is unavailable:

- save the learner's response and its exact attempt conditions;
- run W0 deterministic checks;
- let the learner self-check the four content points and recipient/register;
- show reviewed planning/checking reminders without claiming a grade;
- mark rich evaluation **pending/not available**;
- do not move readiness from the unavailable evaluation;
- continue with other valid practice;
- evaluate later only if still useful and permitted by the data policy.

The fallback is honest incomplete evidence, never a fabricated B1 score.

---

## 14. Edge Cases / Failure or Uncertainty Handling

| Situation | Product behavior | Must not happen |
|---|---|---|
| Wrong topic | Apply the verified rubric behavior; explain that language quality cannot rescue task relevance | Polish the German and call it B1-sufficient |
| Right broad topic, wrong communicative situation | Preserve the official distinction: task management can fail while supported language criteria are still evaluated | Collapse everything into generic “bad Writing” |
| One content point ambiguous | Mark uncertain/partial and lower confidence; use prompt semantics or another evaluator if high impact | Force a confident fulfilled/not judgment without evidence |
| Generated prompt itself is ambiguous | Invalidate/quarantine prompt and exclude learner impact | Penalize learner or pay a premium model to rationalize bad content |
| Very short response | Evaluate only observable task/language behavior; likely missing coverage is explicit | Invent an official word-count penalty |
| Very long response | Judge task, clarity, timing, and language normally; length itself is not the criterion | Reward verbosity or penalize beyond actual rubric effects |
| Many harmless grammar errors | Preserve B1-sufficiency when comprehensibility remains strong; emphasize only recurring/high-impact patterns | Rewrite into perfect German and declare original poor |
| Few errors but required points missing | Prioritize Criterion I/task repair | Let polish hide missing obligations |
| Mixed `du`/`Sie` | Diagnose recipient/register consistency | Treat one typo as equivalent to whole-text register failure |
| Learner uses translator/phrase bank in practice | Record assisted production and continue learning | Call the result clean independent/P4 evidence |
| Model/reference answer viewed before retry | Mark exposure; same-prompt revision is weak/guided evidence | Use polished revised text as readiness anchor |
| Memorized phrase used appropriately | Score normal communicative behavior | Penalize legitimate learned functional language |
| Large memorized block poorly adapted | Score actual task relevance/register/coherence; lower breadth confidence where appropriate | Reward complexity merely because language sounds advanced |
| Learner disputes feedback plausibly | Show concrete rubric/content-point reason; permit one fresh check or high-impact review | Argue from model authority |
| Evaluators disagree | Lower confidence; resolve once only when decision value justifies it | Average arbitrary model scores into fake precision |
| Evaluation service unavailable | W0 fallback/pending; no readiness movement | Block all Writing or invent score |
| Technical interruption in timed mode | Qualify/invalidate timing; preserve usable language evidence if fair | Score infrastructure failure as learner slowness |
| Autocorrect materially changes German in P4 | Mark attempt assisted/non-clean target evidence | Pretend tool-supplied language was independently produced |
| Accessibility support used | Preserve the exact condition; Stage 25 decides target equivalence | Treat access support as cheating by default |
| Learner is far below B1 | Reduce one axis, restore frames/checklist, keep functional email mechanism | Force repeated 30-minute B1 failures |
| Learner is already strong | Give concise evidence and move to fresh/timed/varied prompts | Manufacture corrections to justify coaching |
| Current TELC blueprint changes | Preserve transferable historical Writing evidence; update P4 status/scoring mapping | Erase history or keep obsolete tasks labelled current |
| Corpus lacks prompt-frequency evidence | Use conservative reviewed scenario coverage; re-rank later | Claim empirical frequency without Corpus support |

### Strong response with nothing important to repair

Bestehen is allowed to say the response is good enough and move on. It should not invent style work simply to fill a feedback panel. The next useful action is usually a fresh category/register or more realistic time condition.

### Error attribution remains conservative

One sentence may contain grammar, vocabulary, spelling, and structure issues. Mistake Memory should receive a fine cause only where the evaluator can support it. Otherwise record a broader production shortfall and test the pattern again. Do not create five recurring weaknesses from one sentence.

---

## 15. Relationship to Other Bestehen Stages

- **Stage 03 — Initial Diagnostic:** its short Writing sample remains provisional/low-confidence. Stage 12 supplies the full rubric used to interpret later samples.
- **Stage 04 — Learner Model:** stores criterion/dimension evidence, assistance, timing, independence, evaluator quality, freshness, and target-condition status. Stage 04 evidence tiers remain authoritative.
- **Stage 05 — Mistake Memory:** receives supported Writing manifestations/causes. Productive weaknesses require productive fresh transfer and independent recurrence.
- **Stage 06 — Daily Coaching Engine:** Writing can outrank cheap objective skills when it is a written-pass risk, due repair, stale evidence, or target-condition gap. Session planning does not require another evaluator call.
- **Stage 07 — Core Learning Loop:** Stage 12 preserves one/two repair targets, narrow repairs, learner revision as controlled practice, and fresh productive retry.
- **Stage 08 — A1→B1 Progression:** supplies P0–P4 assistance/timing semantics. Stage 12 fixes the Writing-specific target as one 30-minute current-format email.
- **Stage 10 — Sprachbausteine:** grammar/lexical cloze evidence may create a Writing verification opportunity, but never lowers/raises Writing production without direct Writing evidence. Productive B1 sufficiency is not cloze perfection.
- **Stage 14 — Review:** should return recurring Writing patterns through brief productive checks and natural embedding, not a separate proofreading backlog.
- **Stage 15 — TELC Readiness:** owns final written-readiness aggregation, scoring prediction, evidence minimums, recency, uncertainty, and pass constraints. It must preserve Stage 12's criterion-level, evaluator-quality, assistance, timing, and target-version evidence.
- **Stage 16 — Mock Exams:** owns full mock sequencing. Mock Writing uses the verified 30-minute condition and defers feedback; post-mock repair cannot alter the original result.
- **Stage 17 — Ready to Book:** should demand enough recent independent/target-condition Writing evidence as part of the written readiness gate defined in Stage 15.
- **Stage 18 — Coach Personality:** refines exact wording while preserving the Stage 12 principle of B1 sufficiency, limited corrections, and uncertainty without shame.
- **Stage 19 — Information Architecture:** can choose screen composition but must keep verdict, official criteria, content points, limited corrections, learner revision, and fresh check understandable.
- **Stage 21 — Content Strategy:** supplies original/reviewed Writing prompts, content-point metadata, anti-repetition, scenario coverage, and rights-aware reference material.
- **Stage 22 — Corpus → App Contract:** should expose target/task version, topic/function patterns, register, vocabulary/grammar relevance, difficulty, and source confidence needed to ground prompt generation and priority.
- **Stage 24 — Account/Data:** decides raw response/evaluation retention, deletion, export, and AI data handling. Stage 12 requires evaluator/version provenance while data exists.
- **Stage 25 — Accessibility:** determines which input/timing accommodations preserve target-condition comparability.
- **Stage 26 — Analytics:** monitors rubric agreement, B/C boundary accuracy, false-positive/false-negative sufficiency, content-point accuracy, evaluation drift, repair transfer, Writing-to-mock/real-exam calibration, and cost.
- **Stage 27 — Cost Boundaries:** sets portfolio-wide limits; Stage 12's default is one cheap evaluation per submitted standard response, selective escalation, cached reuse, and no routine multi-call agent chain.

### Cross-stage guardrails

Later stages may tune evaluation thresholds, UI, prompt mix, and readiness coefficients, but must preserve:

- current target blueprint as versioned knowledge;
- official three-criterion mapping without invented official sub-scores;
- explicit content points;
- B1 sufficiency rather than native-like polishing;
- communicative-impact weighting of errors;
- limited correction focus;
- learner revision separated from independent fresh transfer;
- model/reference answers excluded from learner evidence;
- P4 exact 30-minute/no-coaching condition;
- evaluator confidence/version/calibration attached to evidence;
- honest pending/uncertain evaluation;
- low-cost one-call standard evaluation and selective premium escalation.

---

## 16. Cost Notes

Writing has a real recurring evaluation cost because open responses need semantic/rubric judgment, but it can remain modest.

### Preferred personal-project default

- prompts and content-point metadata are authored/generated **offline in batches**, reviewed, and reused;
- deterministic validation/caching happens before AI;
- evaluate only on meaningful submission, not on every keystroke;
- normal practice uses **one low-cost structured evaluation**;
- that one result feeds feedback, learner model, Mistake Memory, and future planning;
- common feedback/repair prose is template-driven from structured findings where quality is sufficient;
- reuse reviewed functional patterns and repair assets;
- cache unchanged-response evaluations;
- no premium model is used merely to produce a prettier corrected email;
- W0 self-check mode keeps Writing usable if AI is unavailable or the learner wants near-zero-cost practice.

### Premium/stronger model trigger

Use one stronger/second evaluator only for a valid new sample when a materially important decision is both high-value and uncertain — especially a P4/mock B/C boundary or contradictory readiness anchor.

The cheaper fallback is another fresh sample, lower confidence, or a broad diagnosis. Cost is never a reason to fabricate a score or silently treat model-generated prose as learner ability.

### Human cost

Human evaluation is **not** a routine product dependency. Human effort is concentrated on:

- building and occasionally refreshing the benchmark set;
- reviewing evaluator failure slices;
- optionally resolving a rare high-impact dispute;
- validating new rubric/evaluator versions.

A small high-value calibration set is more sustainable than human-marking every personal-project response.

### Upgrade rule

Spend more only if measured evidence shows that the low-cost evaluator materially misclassifies B1 sufficiency, misses content points, produces unstable feedback, or weakens readiness calibration. Before switching to an always-expensive model, prefer:

1. better rubric instructions and examples;
2. stronger prompt/content metadata;
3. deterministic pre/post-processing;
4. benchmark-driven evaluator tuning;
5. selective escalation;
6. another fresh sample.

---

## 17. Decisions Made

1. Mapped the current TELC B1 Writing target to one 30-minute informal/semi-formal email with four content points and three official criteria.
2. Made target blueprint/scoring versioned rather than permanently hard-coded.
3. Defined seven practice scenario categories while keeping one official target task family.
4. Represented every required content point explicitly with fulfilled/partial/not/uncertain states.
5. Mapped Bestehen's coaching dimensions to the official criteria without inventing extra TELC sub-scores.
6. Made **B1 sufficiency**—centered on functional B-level behavior—the coaching target rather than native-like/A-band perfection.
7. Rejected an invented official word-count threshold.
8. Defined correction presentation from verdict → official criteria → content coverage → one/two high-value repairs → optional secondary notes.
9. Limited normal correction emphasis to two targets, with a hard maximum of three only for a distinct task-obligation plus two other material issues; active repair remains one primary plus at most one secondary target.
10. Defined minimal corrections in the learner's own prose and made full corrected/model responses optional, delayed, B1-appropriate reference material.
11. Defined the repair-and-rewrite flow: original attempt → diagnosis → narrow repair → learner revision → fresh productive retry → delayed transfer.
12. Defined responsible reusable functional patterns and a planning skeleton, with support fading from P0 to no answer-bearing template in P4.
13. Defined open, pace-aware, practice-timed, P3 target-probe, and exact 30-minute P4 Writing modes.
14. Defined the Writing evidence contract and its handoff into written readiness without pre-empting Stage 15's formula or inventing a standalone Writing pass gate.
15. Defined versioned AI evaluation, structured outputs, deterministic prechecks, calibration corpus, initial quality gates, confidence, selective escalation, and disagreement handling.
16. Defined W0–W3 cost modes, one-call standard evaluation, caching, batching, zero-cost fallback, and stronger-model triggers.
17. Preserved Mistake Memory/direct-productivity rules: same-prompt model-exposed revision is learning evidence; fresh unassisted writing is required for independence/readiness.
18. Defined edge-case behavior for wrong topic/situation, ambiguous prompts, assistance, memorized templates, AI disagreement, technical timing failures, accessibility, and blueprint changes.

---

## 18. Open Questions / Deferred Decisions

### Owner questions

**None.** Stage 12 can be responsibly shaped from the existing product context and official target material.

### Deferred product decisions

- final adaptive schedule for returning Writing mistakes and useful phrases — Stage 14;
- exact Writing contribution to written readiness, score prediction, evidence minimums, recency windows, and pass-risk thresholds — Stage 15;
- exact full-mock flow, response-sheet behavior, pause rules, and mock consistency requirements — Stage 16;
- exact ready-to-book Writing evidence minimums — Stage 17 after Stage 15;
- final learner-facing copy, bilingual explanation depth, and visual information hierarchy — Stages 18–19;
- final cross-skill prompt generation/QA, freshness, source-use, and anti-repetition policy — Stage 21;
- exact Corpus payload/interface and empirically derived scenario/grammar/topic frequencies — Stage 22;
- raw text retention, deletion, export, sync, and provider data handling — Stage 24;
- accessibility/input aids that qualify as target-condition equivalent — Stage 25;
- empirical recalibration of the evaluator quality gates, model-upgrade thresholds, and Writing-to-real-exam calibration — Stage 26;
- portfolio-wide recurring-cost ceilings and paid/free product choices — Stage 27;
- model vendor, architecture, prompt implementation, storage, and orchestration — post-shaping architecture work.

The evaluator agreement percentages in Section 12.4 are **initial QA gates**, not scientific constants or claims of official TELC equivalence. They must be recalibrated from human agreement, mock performance, and eventual real-exam outcomes.

---

## 19. Definition of Done Check

- [x] Map current TELC B1 writing format and scoring dimensions.
- [x] Define prompt categories.
- [x] Represent required content points explicitly.
- [x] Define evaluation dimensions:
  - [x] task completion,
  - [x] communicative success,
  - [x] structure,
  - [x] vocabulary,
  - [x] grammar,
  - [x] register,
  - [x] greeting/closing where relevant.
- [x] Evaluate against **B1 sufficiency**, not ideal/native German.
- [x] Decide correction presentation.
- [x] Limit the number of corrections emphasized at once.
- [x] Define repair-and-rewrite flow.
- [x] Define reusable patterns/templates responsibly.
- [x] Define timed writing mode.
- [x] Define how writing affects readiness.
- [x] Define evaluator consistency, versioning, calibration, confidence, and disagreement handling.
- [x] Include scoring-rubric mapping and learner-facing feedback examples.
- [x] Define low-cost evaluation modes, batching/caching, stronger-model triggers, and zero-cost fallback.
- [x] Preserve direct productive evidence and model-exposure boundaries from earlier stages.
- [x] Document uncertainty, edge cases, cross-stage dependencies, and deferred decisions.
- [x] Leave no owner-blocking product question unresolved.

**Done outcome:** Bestehen can answer “Would this likely be good enough for B1?”, explain the answer in TELC-aligned terms, focus the learner on the few changes that matter, and prove improvement through fresh learner-produced Writing without requiring expensive always-on AI.