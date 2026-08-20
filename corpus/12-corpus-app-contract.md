# Bestehen / Corpus — Stage 12: Contract with Bestehen / App

> **Status:** Authoritative Stage 12 product-shaping decision  
> **Product:** Bestehen / Corpus  
> **Primary downstream customer:** Bestehen / App  
> **Core principle:** Corpus supplies stable, rights-aware, evidence-qualified exam intelligence; App turns that intelligence into learner-specific coaching, original practice, evaluation, and readiness without rediscovering Corpus logic or receiving restricted source expression by default.

## 1. Purpose and Scope

Stage 12 defines the stable **conceptual product contract** between Bestehen / Corpus and Bestehen / App. It answers:

- what categories of information App can consume from Corpus;
- what App may ask Corpus for when selecting or generating practice;
- how requests differ for assisted A1, genuine A2, A2/B1 bridge, independent B1, and target-condition B1 work;
- how Corpus-derived patterns can ground original exercises without copying restricted source material;
- which provenance, confidence, rights, quality, and version information travels with Corpus outputs;
- what happens when Corpus data changes, a taxonomy evolves, a source is reclassified, or material is removed;
- which responsibilities remain permanently on the Corpus side versus the App side.

This is a **product contract, not an API specification**. It deliberately does not choose REST, GraphQL, RPC, database sharing, event streams, file bundles, serialization formats, cache technology, deployment topology, or client/server boundaries. Later architecture may implement the contract in the simplest maintainable way, provided the semantics below remain intact.

### 1.1 Contract objective

**Bestehen / App should be able to ask for trustworthy exam patterns and target intelligence at the level of abstraction it needs, receive enough evidence and restriction context to use them safely, and remain insulated from raw Corpus ingestion, trust, rights, deduplication, and analytics mechanics.**

### 1.2 Boundary rule

The established boundary remains authoritative:

- **Corpus answers:** “What do the exams and credible exam-style evidence show, how strong is that conclusion, how difficult/target-relevant is it, and what may downstream systems do with the source-derived material?”
- **App answers:** “What should this learner do now, how much help should they receive, how did they perform, what should be repaired/retried, and what does the evidence mean for readiness?”

Corpus may produce a pattern that is highly important for TELC B1. Only App decides whether a particular learner practices it today.

### 1.3 What this contract does not turn Corpus into

Stage 12 does **not** turn Corpus into:

- a learner-profile store;
- a session planner;
- a readiness calculator;
- a learner-facing exercise library;
- an on-demand AI tutor;
- a real-time exercise-generation service that owns learner-specific prompts;
- a public API/product;
- a substitute for App content QA or learner evaluation.

Corpus owns **reference evidence and reusable exam intelligence**. App owns the learner experience and final learner-facing practice artifact.

---

## 2. Inputs / Existing Decisions

Stage 12 preserves the Product Overview, Identity, both live shaping checklists, Corpus Stages 01–11, and the shaped App progression/learner-model boundary.

### 2.1 Mission and product boundary — Corpus Stage 01

Stage 01 established that Corpus is an exam-data and intelligence product whose primary customer is App, that TELC B1 is the strongest target signal while Corpus remains broader than TELC, and that App should not need to rebuild provenance, trust, rights, deduplication, or exam-intelligence logic.

### 2.2 Provenance and source lifecycle — Corpus Stage 02

Stage 02 established candidate/source-observation/material distinctions, permanent provenance subject to stronger takedown requirements, source version history, mirror/alternate handling, dead-source history, and both automated and manual intake.

### 2.3 Trust/confidence — Corpus Stage 03

Stage 03 established:

- authenticity status is separate from evidence confidence and rights;
- A/B/C/D confidence tiers with local confidence at source, document, exam, task, and item scope;
- B+ as the default minimum for production learning-priority evidence, generation grounding, and direct learner exposure;
- direct exposure additionally requires rights permission and no unresolved correctness/structure dispute;
- low-confidence material can contribute bounded context but cannot become learner-facing ground truth merely because it exists in Corpus;
- confidence changes are auditable and must trigger downstream reevaluation when materially relevant.

### 2.4 Rights and takedown — Corpus Stage 04

Stage 04 established `REUSABLE`, `REUSABLE_WITH_CONDITIONS`, `REFERENCE_ONLY`, `UNKNOWN_REVIEW_REQUIRED`, and `PROHIBITED`; action-level permissions/obligations; component-level mixed rights; immediate takedown holds; and the distinction among source expression, source-specific non-reconstructive metadata, and aggregate intelligence.

Reference-only/unknown-rights evidence may still support allowed non-reconstructive intelligence. It may not be sent to App as exact/close source content merely because it is analytically useful.

### 2.5 Canonical exam model — Corpus Stage 05

Stage 05 established Source Observation → Document → Exam/Test Set → Section → optional Part → Task → Item, plus separately addressable Instructions, Stimuli, Response Options, Answers, Explanations, Scoring Rules/Rubrics, and Assets. It also established explicit completeness and version/source relationships.

### 2.6 Shared skill graph — Corpus Stage 06 / App learner model

Stage 06 established the multi-axis, versioned taxonomy and stable node identities used by the App learner model: provider/exam metadata, CEFR, section, task shape, topic, grammar, vocabulary/domain/functional language, Reading, Listening, Writing, Speaking, strategy, reasoning, and distractor patterns.

Assignments carry role, confidence, origin, evidence, version, and review state. Taxonomy migration must never silently manufacture learner mastery.

### 2.7 Difficulty and relevance — Corpus Stage 07

Stage 07 established separate CEFR, L/R/T/A/P difficulty, Generic-B1 (`GB1`) relevance, TELC-B1 (`TELC`) relevance, estimate uncertainty, currentness, and evidence influence. App combines these task-side facts with learner-side ability and conditions; Corpus does not personalize global difficulty to one learner.

### 2.8 Publication/QA/independence — Corpus Stages 08–10

Published Corpus data is capability-scoped, not universally “valid.” Partial publication is allowed. Deduplication/independence is applied before decision-grade analytics. Correctness-sensitive use is stricter than low-risk context use. App must therefore consume the **eligibility for the requested use**, not infer it from a generic published flag.

### 2.9 Analytics — Corpus Stage 11

Stage 11 established three App-facing roles for analytics:

1. **exam-priority priors**;
2. **exercise-generation grounding**;
3. **readiness evidence design**.

It also established that generation consumes abstract pattern intelligence, not verbatim source expression, and that weak results fall back to a broader parent pattern, anchor-only target fact, explicit insufficient-evidence state, or curated target default.

### 2.10 App progression — App Stage 08

App Stage 08 established five skill-specific realism rungs:

- P0 Supported Foundation;
- P1 Guided A2;
- P2 A2/B1 Bridge;
- P3 Independent B1 Training;
- P4 Target Conditions.

Corpus acquisition remains A2/B1; App may scaffold Corpus-derived target skills down to A1-accessible work. Stage 12 must therefore support an **assisted A1 use case without pretending Corpus owns an A1 source corpus**.

No earlier decision is materially changed by Stage 12.

---

## 3. Decisions and Rationale

## 3.1 Contract around capabilities, not raw tables or source files

**Decision:** App consumes named **Corpus capabilities** rather than reaching into Corpus storage or rebuilding its internal logic.

The contract has six required information families from the Stage 12 checklist, plus governance/version context:

1. raw/reference content;
2. structured metadata;
3. aggregate statistics;
4. skill relationships;
5. exercise-generation patterns/constraints;
6. difficulty/relevance signals;
7. provenance, confidence, rights, QA, and version/change context that governs the first six.

This separation is intentional. App can ask for a generation-ready pattern without receiving a restricted source passage; ask for a target profile without receiving every raw URL; or inspect exact reusable content when a valid product flow genuinely needs it.

## 3.2 Prefer task/pattern intelligence over source-item delivery

**Decision:** The default App interaction is **pattern-first**, not source-item-first.

Corpus is evidence; App practice is primarily original. Even when a source item is legally reusable, App should use exact source content only when direct reference material is itself useful—for example a deliberately labeled reference/model experience—and not merely because copying it is easier than generating original practice.

The normal practice path is:

**eligible Corpus evidence → abstract pattern/constraint blueprint → original App exercise → App QA/delivery/evaluation**.

This reduces rights fragility, memorization risk, duplicate exposure, and dependence on a small official source set.

## 3.3 Corpus returns use eligibility, not ingredients App must reinterpret

**Decision:** For every material output, Corpus should tell App whether it is eligible for the requested capability under the current trust, rights, QA, duplicate/currentness, and publication state.

App should not need to reproduce rules such as:

- “B+ generation grounding”;
- whether an answer is correctness-ready;
- whether a source is quarantined;
- whether two observations are mirrors;
- whether reference-only source text may be displayed;
- whether a TELC-specific prevalence result is decision-grade;
- whether a taxonomy assignment is provisional.

The underlying facts remain available for explanation/audit where useful, but Corpus owns the eligibility decision for Corpus-derived material.

## 3.4 App requests a desired learning/exam pattern, not a learner profile

**Decision:** App may describe the **desired practice target** to Corpus, but it does not send personal learner state in order for Corpus to choose the exercise.

App can ask conceptually for:

- target exam/profile: TELC B1;
- section/task family;
- stable taxonomy node(s) and assignment role desired;
- progression/use profile (P0–P4 or equivalent A1-assisted/A2/bridge/B1 target);
- difficulty envelope/dimensions;
- target/generic relevance requirements;
- topic/domain or diversification constraints;
- reasoning/distractor pattern when relevant;
- modality/media requirements;
- timing/playback/interaction constraints;
- whether exact reusable reference content is requested or abstract generation grounding only.

App keeps private learner attributes—mastery, mistakes, readiness, exam date, fatigue, prior exposure, preferences, session time—inside App and uses them **before** making this request.

### Why

This keeps the boundary clean, avoids turning Corpus into a personal-data service, and makes Corpus pattern retrieval/cacheability much cheaper.

## 3.5 Original generation belongs to App; generation grounding belongs to Corpus

**Decision:** Corpus owns the **generation blueprint**, not the learner-facing generated exercise.

Corpus describes what a faithful fresh task should preserve. App creates, validates, stores, schedules, presents, and evaluates the final exercise.

This means Corpus may say:

> Build a B1/TELC-relevant Reading matching task whose primary skill is constraint filtering, whose topic is housing, whose distractor family includes one plausible keyword-overlap option that violates a time constraint, and whose linguistic/reasoning demands fall in the stated envelope.

Corpus should **not** need to send the wording of the source advertisements that led to that conclusion.

## 3.6 Contract and data/model versions are separate

**Decision:** The compatibility of the Corpus/App contract must not be conflated with taxonomy, analytics, or difficulty-model versions.

A response may be compatible with the same contract shape while its taxonomy version, target profile, difficulty model, rights decision, or analytic snapshot has changed. App must be able to identify both kinds of change.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Information family 1 — Raw / reference content

### Purpose

Raw/reference content exists for explicit source-backed use, operator/debug inspection, benchmark/reference experiences, or flows where exact reuse is both allowed and product-appropriate.

### What App may receive

Where the requested use passes all gates, App may receive relevant source-backed components such as:

- exact instruction/prompt/stimulus/question text;
- response options;
- answer/scoring/rubric material;
- source media/assets;
- provider-native labels/order/timing/playback constraints;
- completeness and version context;
- attribution/notice requirements;
- stable Corpus identities and source lineage.

### Default behavior

Raw/reference content is **not included in ordinary pattern/generation responses**.

For `REFERENCE_ONLY`, `UNKNOWN_REVIEW_REQUIRED`, or `PROHIBITED` material, App receives no exact source expression for learner-facing use. Corpus can instead return:

- abstract structure;
- taxonomy mappings;
- difficulty/relevance;
- aggregate pattern intelligence;
- non-reconstructive provenance/evidence summary;
- an explicit “exact content unavailable for requested use” result.

### Composite rule

A composite reference task must pass eligibility for every required component. If text is reusable but an image/audio asset is restricted, Corpus should either:

- return the text with the asset explicitly unavailable/replacement-required when the experience remains coherent; or
- declare the composite reference use ineligible.

App must not silently substitute an unrelated component and still present the result as the original source task.

---

## 4.2 Information family 2 — Structured exam metadata

### Purpose

Structured metadata lets App reason about exam shape without rereading source documents.

### Required categories

App must be able to consume, where applicable:

- canonical entity identity and hierarchy: Exam/Test Set, Section, Part, Task, Item;
- Instructions/Stimuli/Response Options/Answers/Scoring Rules/Assets as relationships, not duplicated blobs;
- normalized provider/exam family and provider-native labels;
- CEFR scope, including A2, B1, A2/B1 mixed, and uncertainty;
- normalized Section and task facets: activity family, response mechanic/cardinality, stimulus form, interaction shape;
- timing, playback, preparation, reference, and response constraints established by source evidence;
- completeness/source-extraction-linking states;
- answer/scoring readiness for correctness-sensitive use;
- task/item taxonomy assignments with assignment role/confidence/origin/review state;
- current/historical/superseded target-format status where format currency matters.

### App rule

App uses canonical normalized semantics for behavior and provider-native fields for faithful reference/exam realism. It must not infer that provider-native labels have the same meaning across providers without the normalized mapping.

---

## 4.3 Information family 3 — Aggregate statistics / exam intelligence

### Purpose

Aggregate intelligence tells App what patterns are common, target-relevant, transferable, or underrepresented without exposing source expression.

### Required categories

App must be able to consume decision-grade results for:

- vocabulary/domain/functional-language prevalence;
- grammar exposure/tested-dependency/productive-demand prevalence;
- topic prevalence;
- task/response/stimulus/interaction-shape prevalence;
- skill/competency prevalence;
- provider comparisons;
- A2 → mixed A2/B1 → B1 progression;
- TELC-vs-generic-B1 comparisons;
- reasoning-pattern and distractor-pattern prevalence;
- high-value co-occurrence combinations;
- difficulty distributions by relevant scope;
- target coverage and evidence concentration/sufficiency.

### Every decision-grade analytic carries conceptually

- subject/pattern identity;
- metric family;
- scope/filter;
- counting unit;
- eligible denominator/coverage where meaningful;
- independent support/effective evidence mass or conservative support description;
- result/prevalence/distribution;
- A/B/C/source/provider concentration summary where material;
- sufficiency label;
- currentness/target-profile context where relevant;
- taxonomy/analytic version and recomputation identity;
- allowed downstream role: priority, generation grounding, readiness-evidence design, or exploratory only.

### App rule

App should normally consume the **decision-grade result and its sufficiency**, not recompute prevalence from raw item counts. Exploratory results may be used for internal inspection but must not directly change learner priority/readiness.

---

## 4.4 Information family 4 — Skill graph and relationships

### Purpose

Corpus provides the shared semantic graph App uses to attach learner evidence and choose related practice.

### App must be able to consume

- stable opaque node IDs;
- current human labels/descriptions and node family/type;
- hierarchy (`is_a`/parent-child);
- curated relationships such as prerequisite/support/counterpart/contrast;
- validated empirical relationships such as `co_occurs_with` with scope/evidence strength;
- task-pattern relationships such as `typically_tested_by` and `typically_uses_reasoning`;
- distractor-target relationships;
- node lifecycle state;
- taxonomy version;
- aliases and provider-native mappings where needed;
- migration/successor/predecessor rules for rename, merge, split, reparent, deprecation, and retirement.

### Relationship guardrail

App must preserve relationship semantics:

- co-occurrence is not prerequisite;
- receptive counterpart is not productive mastery;
- related skill can influence content selection before it influences learner evidence;
- a taxonomy change may lower certainty or require fresh evidence but must not manufacture learner mastery.

---

## 4.5 Information family 5 — Exercise-generation pattern / constraint blueprint

### Purpose

The blueprint is the core bridge between broad reference evidence and original learner-facing practice.

### 4.5.1 Required blueprint fields conceptually

A generation blueprint should contain only the information needed to reproduce the **exam-relevant pattern**, including as applicable:

1. **Target identity**
   - target exam/profile;
   - Section/task family;
   - progression/use profile;
   - CEFR target/context.

2. **Task mechanics**
   - activity family;
   - response mechanic/cardinality;
   - stimulus form;
   - interaction shape;
   - expected number/range of Items where the pattern depends on it;
   - structural constraints that affect the solve/response.

3. **Primary tested capability**
   - stable primary taxonomy node(s);
   - permitted secondary/supporting/context nodes;
   - assignment roles;
   - reasoning pattern(s);
   - strategy behavior only when the task is meant to train it.

4. **Content envelope**
   - realistic topic/domain distribution;
   - vocabulary/functional-language demand;
   - grammar demand where relevant;
   - register/communicative function for productive tasks;
   - anti-repetition/diversity guidance.

5. **Difficulty envelope**
   - CEFR context separate from L/R/T/A/P ranges/bands;
   - task-length/input-density expectations;
   - productive-demand expectations;
   - uncertainty/broader fallback when fine difficulty is not supported.

6. **Distractor / wrong-option behavior** for objective items
   - eligible distractor families;
   - wrong-option composition tendencies;
   - decisive evidence/reasoning relationship;
   - correctness-ready basis required for any claimed distractor pattern.

7. **Delivery constraints**
   - timing pressure/target timing where appropriate;
   - listening speed/speaker/noise/playback envelope;
   - preparation/reference rules;
   - productive interaction/turn-taking constraints;
   - P4 exact target-condition requirements only when verified/current evidence supports them.

8. **Grounding quality**
   - decision-grade/anchor/broader-fallback status;
   - independent support/sufficiency summary;
   - TELC and GB1 relevance;
   - confidence/currentness notes that materially limit the blueprint.

9. **Rights-safe generation constraints**
   - generation must be original rather than a close adaptation when source expression is restricted/unknown;
   - no source text, answer-option wording, transcript, image, or reconstructive excerpt included by default;
   - any permitted direct component is explicitly identified with its action-level rights/conditions;
   - prohibited/held material contributes no new grounding where Stage 04 disallows it.

10. **Traceability**
    - blueprint stable identity/revision;
    - taxonomy/difficulty/analytics/target-profile versions used;
    - non-reconstructive grounding manifest sufficient to audit why the pattern exists without exposing restricted expression to normal App generation flows.

### 4.5.2 What a blueprint must not become

A blueprint is invalid if it is effectively a disguised source item—for example:

- the same passage with names changed;
- the same answer choices in different order;
- a translated or lightly paraphrased reference-only prompt;
- a transcript summarized so closely that it substitutes for the original;
- a unique source-specific combination detailed enough to reconstruct the source expression.

If Corpus cannot describe the pattern without reconstructive detail, it should return a broader abstraction or withhold generation grounding.

---

## 4.6 Information family 6 — Difficulty and relevance signals

App must be able to consume these signals separately:

- **CEFR** classification/scope;
- **L — Linguistic difficulty**;
- **R — Task/reasoning difficulty**;
- **T — Time-pressure difficulty**;
- **A — Audio difficulty**;
- **P — Productive-skill difficulty**;
- optional section-aware composite only when sufficiently supported;
- estimate confidence/uncertainty and model/rubric version;
- **GB1 — Generic B1 relevance**;
- **TELC — TELC B1 relevance**;
- relevance support/sufficiency/currentness;
- target delivery facts such as timing/playback when they are source facts rather than inferred difficulty.

### App interpretation rule

Corpus difficulty is **task-side demand**. App learner difficulty is the interaction between that demand and learner state.

Therefore App may use Corpus difficulty to choose a task envelope, but it must not treat `R=70` as “this learner is 70% likely to fail,” and Corpus must not personalize the score from one learner’s struggle.

---

## 4.7 Governance envelope — what accompanies Corpus outputs

**Decision:** Every App-consumable Corpus result carries a governance envelope appropriate to the capability. Exact physical fields are architecture decisions; the following meanings are product requirements.

### Always required for decision-grade intelligence

- stable result/record identity and revision;
- capability/use eligibility;
- current/superseded/withdrawn state;
- Corpus contract major/minor compatibility identity;
- relevant taxonomy/model/analytics/target-profile versions;
- evidence sufficiency/confidence summary;
- last/current recomputation or effective-version context;
- material limitations that change App behavior (e.g. anchor-only, not prevalence, unresolved currentness, broader fallback).

### Required when source-specific material is involved

- authenticity/confidence at the most local relevant scope;
- effective usage status;
- action-level permission relevant to the requested use;
- attribution/notice/license obligations and exact credit fields where required;
- component-level restriction when mixed rights/confidence exist;
- source/provider identity as observed/normalized without implying official affiliation;
- source/version/provenance identifiers;
- takedown/reclassification state if applicable.

### Required for aggregate/pattern intelligence

Normal App flows do **not** require every raw URL. They require a non-reconstructive evidence summary sufficient to understand:

- support strength;
- whether target-provider evidence exists;
- provider/source-family concentration;
- independence treatment;
- currentness;
- whether the conclusion is decision-grade, anchor-only, or insufficient.

An internal operator/debug path may request deeper provenance lineage by stable IDs without making that lineage part of every learner-session payload.

---

## 4.8 How App requests suitable exam patterns

### 4.8.1 Conceptual request

An App pattern request is a **desired practice specification**, not a database query. It may include:

- target: TELC B1;
- use profile: assisted foundation / A2 / A2-B1 bridge / independent B1 / target conditions;
- Section/task facets;
- primary skill/competency/reasoning node(s);
- desired difficulty envelope;
- topic/domain include/exclude preferences for variety;
- media modality;
- target realism/delivery constraints;
- whether a generation blueprint, target-profile fact, aggregate prior, reference content, or several of these are needed.

Corpus returns the best eligible result under the evidence rules, not necessarily an exact match fabricated from weak evidence.

### 4.8.2 Fallback order when no exact decision-grade match exists

1. return a broader parent skill/task pattern with stronger support;
2. relax non-essential topic/context constraints while preserving the target skill and task mechanism;
3. return an anchor-only verified target fact without unsupported prevalence;
4. return a trusted generic-B1 transferable pattern where App explicitly permits that fallback;
5. return `insufficient evidence` and let App use its curated content fallback.

Corpus must not silently satisfy a request by promoting C-only evidence or by inventing a precise pattern.

---

## 4.9 Progression/use profiles: A1-assisted, A2, A2/B1, and authentic B1

**Decision:** Corpus does not need an A1 source corpus to serve the A1 learner. App requests the **same target capability at a different realism/difficulty profile**, aligned with App Stage 08.

| Requested use | App progression mapping | What Corpus should return | What Corpus must not imply |
|---|---|---|---|
| **Assisted A1 / early-A2** | **P0 Supported Foundation** | A lower-demand precursor blueprint tied to a real A2/B1/TELC-relevant task/skill; simple topic/domain and difficulty envelope; which reasoning mechanic must remain; evidence about A2/B1 progression; support-safe simplification dimensions | That Corpus has observed authentic A1 TELC B1 material; that the simplified learner-facing output itself is a source-authentic A1 exam item |
| **A2** | **P1 Guided A2** | Genuine A2 evidence/pattern where available, complete small task mechanics, A2 language/difficulty envelope, selective support-compatible delivery | That an A2 task is B1 readiness evidence |
| **Mixed A2/B1** | **P2 A2/B1 Bridge** | B1-shaped or target-relevant mechanics/reasoning combined with A2→B1 progression evidence and controlled mixed language/difficulty; limited support; delivery closer to target | That every source unit is literally labeled mixed when the bridge is an analytic abstraction across evidence |
| **Authentic B1 practice** | **P3 Independent B1 Training** | Genuine B1 linguistic/reasoning/productive demand, decision-grade TELC/GB1 relevance, normal task length/constraints, unassisted-capable blueprint | That “authentic B1” means verbatim authentic source content |
| **Authentic target conditions** | **P4 Target Conditions** | Current verified target mechanics, exact target timing/playback/reference/interaction constraints where known, B1 target difficulty distribution, TELC-specific coverage requirements | Unsupported certainty about current format, or generic-B1 behavior substituted for target-specific conditions when format matters |

### 4.9.1 P0 simplification rule

At P0, App may simplify:

- vocabulary frequency/load;
- sentence length/complexity;
- amount of text/audio/output;
- number/confusability of distractors;
- number of constraints/evidence points;
- production openness;
- timing/playback pressure;
- assistance availability.

But the blueprint should preserve the **exam-relevant causal core**: the skill, reasoning operation, communicative function, or task mechanism that makes this practice a precursor to the target.

If simplification removes that core, Corpus should identify the result as a prerequisite repair concept rather than a target-pattern exercise.

### 4.9.2 P3/P4 authenticity terminology

In this contract, **authentic B1 difficulty/conditions** means faithful difficulty, task shape, language demand, and exam behavior. It does **not** mean the final exercise is an authentic provider item. Exact source content is a separate reference-content mode and remains rights/confidence gated.

---

## 4.10 Grounding original exercises without copying restricted source material

### 4.10.1 Default grounding path

For normal App practice:

1. Corpus selects decision-grade abstract evidence/patterns.
2. Corpus emits a non-reconstructive generation blueprint and grounding manifest.
3. App generates an original stimulus/task/options/prompt/audio script or productive scenario.
4. App validates that the generated artifact satisfies the blueprint.
5. App applies its own correctness/content QA and anti-repetition checks before learner use.
6. App records the blueprint/version used so future debugging can explain why the exercise existed.

No step requires sending restricted source expression into the learner-facing generation path by default.

### 4.10.2 Ground from multiple independent patterns where possible

**Decision:** For original practice, prefer **pattern synthesis from multiple independent B+ evidence units/analytics** over adapting one source item.

Benefits:

- makes the result less source-specific;
- reduces memorization/derivative risk;
- better represents true recurring exam patterns;
- reduces the chance that one source defect becomes a generated template;
- gives more content diversity.

One verified official target source may anchor a format/requirement, but prevalence/content-generation choices should still use broader eligible evidence where available.

### 4.10.3 Restricted-source rule

For `REFERENCE_ONLY` or `UNKNOWN_REVIEW_REQUIRED` evidence:

- allowed abstract/non-reconstructive pattern intelligence may contribute according to Stages 03/04/11;
- exact text/audio/image/options/transcripts and reconstructive summaries do not enter learner-facing generation;
- no close translation, paraphrase, reordered-choice copy, names/dates substitution, or source-specific scene recreation;
- if the only useful representation of a pattern is reconstructive, do not use that source for generation grounding.

### 4.10.4 Reusable-source rule

Even for `REUSABLE`/`REUSABLE_WITH_CONDITIONS` content:

- App should distinguish **direct reference use** from **original generation**;
- direct source components are included only when the requested action and all conditions allow it;
- an attribution obligation that applies to direct source use must not be silently lost by the contract;
- if a no-derivatives condition applies, direct unmodified use may be allowed while source-derived adaptation/generation is not;
- original generation can still prefer the abstract blueprint to avoid unnecessary source dependence.

### 4.10.5 Generated-output similarity failure

If an App-generated exercise is later found to be materially too close to restricted source expression:

- retire/quarantine the generated exercise;
- stop new delivery;
- regenerate from a broader/more diverse blueprint;
- preserve the incident for generation QA;
- do not reinterpret the restricted source as reusable simply because the generated output already existed.

The exact anti-copy/similarity implementation and calibrated threshold are deferred to architecture/benchmark work; the **product requirement is independent wording/expression and non-reconstructive grounding**.

---

## 4.11 Provenance and attribution behavior

### 4.11.1 Three provenance levels

**Decision:** Provenance is exposed at the minimum level needed for the App capability.

#### Level A — evidence summary (default for analytics/blueprints)

Return non-reconstructive provenance such as:

- evidence tier mix/sufficiency;
- target-provider support yes/no/strength;
- independent material count/range or support class;
- provider/source-family concentration;
- currentness/historical status;
- grounding manifest IDs/revisions.

This lets App trust/explain the result without receiving every source URL or restricted expression.

#### Level B — source lineage (internal drill-down/reference flows)

Return relevant source/document/exam/task identities, normalized/observed provider information, source/version relationship, and current confidence/rights state. This is for operator/debug/reference use, not normal learner UI.

#### Level C — required learner-facing attribution

When exact reusable source content is shown and attribution/license conditions require it, Corpus returns the **exact obligation** App must satisfy, including as applicable:

- credited author/provider/rightsholder text;
- source/title;
- required link/reference;
- license/notice text or identifier;
- modification/no-modification notice;
- any scope/placement condition material to compliance.

If App cannot satisfy a required condition, the exact-content use is ineligible and App falls back to original practice.

### 4.11.2 Attribution is not endorsement

Displaying source/provider attribution must not imply that TELC or any provider endorses or is affiliated with Bestehen. Corpus returns factual provenance; App identity/copy must preserve the independent-product boundary.

---

## 4.12 Contract versioning and compatibility

### 4.12.1 Version the conceptual contract

**Decision:** Corpus → App compatibility uses semantic versions conceptually:

- **Patch:** clarification/optional metadata correction with no behavioral incompatibility;
- **Minor:** additive/backward-compatible capability/field/status that older App consumers may safely ignore;
- **Major:** breaking semantic change requiring App adaptation, such as changed meaning of eligibility/status, removed required field/capability, incompatible request semantics, or changed interpretation that could alter learner behavior if ignored.

The exact version negotiation mechanism is architecture.

### 4.12.2 Payload versions remain independently visible

App responses also identify the versions/revisions that can change meaning while the contract itself remains compatible, including where relevant:

- taxonomy release;
- taxonomy assignment/model version;
- difficulty/relevance model/rubric;
- analytics snapshot/method;
- target exam/profile/currentness revision;
- canonical source/exam/task revision;
- rights/confidence decision revision;
- generation blueprint revision.

### 4.12.3 Stable IDs and mutable revisions

- Stable canonical/taxonomy/pattern identities do not change for ordinary label/metadata corrections.
- Material semantic changes create a new revision/version or successor identity according to the owning stage’s migration rules.
- Retired IDs are not reused for different meaning.
- App-created learner events should retain the Corpus IDs/revisions that were in force when the activity was delivered, so history can be interpreted rather than silently rewritten.

### 4.12.4 Compatibility behavior

For an unsupported **major** contract version, App must not silently reinterpret the response. Product-safe choices are to use a last-supported compatible snapshot/capability if available or fail the affected Corpus-dependent action and use an App-curated fallback.

For additive minor changes, App may ignore unknown optional concepts only when the response explicitly remains eligible under the supported semantics.

Architecture decides whether compatibility is negotiated by request, deployment coordination, bundle version, or another mechanism.

---

## 4.13 Change, reclassification, and removal behavior

### 4.13.1 Every material change has an impact class

Corpus should distinguish at least these downstream-impact classes:

1. **Metadata-only/non-semantic** — label/description/provenance clarification that does not change eligibility or meaning.
2. **Pattern/intelligence changed** — difficulty, prevalence, relevance, currentness, taxonomy mapping, or blueprint changed enough to affect future selection/generation.
3. **Correctness/structure invalidated** — answer, scoring, task mapping, asset link, or structural fact is no longer safe for learner evaluation.
4. **Trust/authenticity downgraded** — source/item evidence influence changes and affected analytics/blueprints may need recomputation.
5. **Rights/direct-use revoked or conditioned** — exact content/derivative use is no longer allowed under the requested action.
6. **Takedown/prohibited/purge** — source expression and affected downstream use must stop immediately; derived intelligence disposition follows Stage 04.
7. **Taxonomy semantic migration** — rename/reparent/merge/split/retire changes how historical learner evidence projects into the current graph.
8. **Target-currentness change** — an older target format/rule remains historical evidence but no longer defines current P4 behavior.

Exact delivery of change notifications is architecture, but App must be able to discover the current state before new use and reconcile cached/persisted Corpus-backed material.

### 4.13.2 Rights-only removal

If source expression becomes prohibited/removed while non-reconstructive intelligence may legally/policy-wise remain:

- stop new exact source delivery immediately;
- invalidate any direct-source reusable-content eligibility;
- identify/review App exercises that materially used source expression or close derivatives;
- aggregate/pattern intelligence may remain if Stage 04 says retain and it remains analytically valid;
- blueprint provenance records that cite a removed source remain non-content tombstone lineage where allowed;
- future generation uses the current eligible blueprint/grounding set, not the removed expression.

### 4.13.3 Trust/correctness invalidation

If a source/item is discovered to be fake, misclassified, structurally wrong, or keyed incorrectly:

- affected analytics/difficulty/relevance/blueprints are recomputed or downgraded;
- current pattern requests must not return the invalidated conclusion as decision-grade;
- source-backed exercises using the incorrect answer/structure are retired;
- App historical learner attempts remain historical events but must be eligible for **evidence repair/reinterpretation** because the measuring instrument may have been wrong;
- Corpus provides enough impact identity/scope for App to identify affected attempts; App decides how learner state/readiness is repaired.

### 4.13.4 Taxonomy migration

Corpus supplies the Stage 06 migration semantics. App preserves historical events and projects forward conservatively:

- rename/reparent with unchanged meaning preserves identity/evidence;
- merge combines without double-counting the same event;
- split reduces certainty and requires fresh direct evidence before strong child mastery;
- retired nodes stop receiving new assignments;
- material meaning change uses a new node rather than rewriting history.

### 4.13.5 Target-profile/currentness change

When verified current TELC behavior changes:

- retain the older profile as historical evidence;
- mark it non-current for target-condition requests;
- recompute current TELC priority/coverage where needed;
- P4 requests use the current verified target profile;
- App may keep old mock attempts as historical learner evidence but should not treat obsolete format coverage as fully satisfying current target-format evidence.

### 4.13.6 No silent hard deletion

Where policy permits, removed/retired Corpus identities remain as non-content tombstones with status/reason/successor or impact scope sufficient to prevent accidental reuse and explain historical App records.

A legal/privacy/security decision may require stronger purge; the contract must support that stronger disposition rather than assuming tombstones are always retainable.

---

## 4.14 Request/capability catalogue

The following conceptual capabilities are sufficient for product shaping. Architecture may combine them.

| Capability App needs | Typical question | Corpus responsibility |
|---|---|---|
| **Target profile** | “What does current TELC B1 require/represent here?” | Return verified current task/section/delivery/coverage facts plus uncertainty/currentness |
| **Pattern selection** | “Give me an eligible pattern for this skill at P2.” | Match task/skill/progression/difficulty/relevance using decision-grade evidence and fallback rules |
| **Generation blueprint** | “How should a fresh equivalent task behave?” | Return non-reconstructive task/skill/content/difficulty/distractor/delivery constraints and grounding quality |
| **Structured reference** | “What is the canonical shape of this exam/task?” | Return normalized canonical structure, provider-native context, completeness, relevant QA/confidence |
| **Reference content eligibility** | “May App show/use this exact component?” | Return current action eligibility, local trust/QA gate, rights/conditions/attribution |
| **Exam-priority prior** | “How important/common is this pattern for TELC/general B1?” | Return decision-grade analytics/relevance with sufficiency/concentration |
| **Skill graph** | “How does this weakness relate to other skills/tasks?” | Return stable nodes/relationships/version/migrations |
| **Difficulty envelope** | “What task demand should P1/P3 practice target?” | Return CEFR + L/R/T/A/P distribution/uncertainty, not learner difficulty |
| **Provenance drill-down** | “Why does Corpus believe this?” | Return source/evidence lineage appropriate to internal/reference use |
| **Change/reconciliation state** | “Is this cached pattern/task/version still current?” | Return current/superseded/withdrawn/migration/impact information |

These are conceptual product capabilities, not mandated endpoints.

---

## 4.15 Responsibility matrix

| Responsibility | Corpus | App |
|---|---:|---:|
| Discover/acquire/reference source material | **Owns** | No |
| Preserve source provenance/version history | **Owns** | Stores only Corpus references needed for delivered activities |
| Authenticity/confidence evaluation | **Owns** | Consumes result; does not recalculate |
| Rights/action eligibility for source-derived material | **Owns** | Must enforce returned conditions in learner-facing use |
| Canonical exam normalization | **Owns** | Consumes |
| Deduplication/independent-evidence treatment | **Owns** | Does not reconstruct from URLs |
| Shared taxonomy definitions/relationships/migrations | **Owns** | Uses as learner-model coordinate system |
| Global difficulty/relevance | **Owns** | Combines with learner state |
| Corpus aggregate analytics/target priors | **Owns** | Uses as exam-side priors |
| Generation blueprint / pattern grounding | **Owns** | Requests/consumes |
| Final original exercise generation | No | **Owns** |
| Generated exercise content QA/correctness | Provides constraints/reference facts | **Owns final learner-facing artifact QA** |
| Learner profile/mastery/mistakes/recency | No | **Owns** |
| Daily/session selection | Supplies priors/patterns | **Owns** |
| Assistance/scaffolding selection | Supplies task-side difficulty/progression intelligence | **Owns** |
| Learner attempt/evaluation | No | **Owns** |
| Readiness/predicted score/pass-risk interpretation | Supplies target evidence design | **Owns** |
| Historical learner-evidence repair after Corpus invalidation | Supplies affected Corpus scope/impact | **Owns learner-state repair** |
| Privacy-safe aggregate learner calibration input later | May consume qualified aggregate signals | **Owns personal data and aggregation boundary** |

### 4.15.1 Generated content does not become Corpus truth automatically

An App-generated exercise is not a new source exam simply because it uses a Corpus blueprint. Its learner performance belongs to App. A future calibrated aggregate may inform Corpus pattern/difficulty models under Stage 07 rules, but generated content must not inflate “what real/reference exams contain” analytics as though it were independent corpus evidence.

---

## 5. Edge Cases / Failure or Uncertainty Handling

### 5.1 App asks for an A1 pattern but Corpus acquisition starts at A2

Return a P0 precursor blueprint grounded in the target skill/task/progression evidence. Mark the learner-facing simplification as an App transformation. Do not invent source-authentic A1 evidence.

### 5.2 Only one verified official TELC example supports a format

Return it as an **anchor/current target fact** if appropriate, not a prevalence claim. The App may represent the required format, but should not infer relative frequency from one example.

### 5.3 Many C-tier sources support a pattern

The pattern may appear exploratorily with bounded support, but Corpus must not return it as a decision-grade learning-priority/generation blueprint solely from C-tier volume.

### 5.4 B+ task has disputed answer key

It may support task structure/topic/skill/difficulty facts that do not depend on correctness. It cannot supply correctness-ready answer/distractor grounding until the dispute is resolved.

### 5.5 Reference content is reusable, but one asset is unknown-rights

Return component-level eligibility. App may use permitted independent components only if the task remains coherent and is not misrepresented as the unchanged original. Otherwise fall back to an original blueprint.

### 5.6 Exact content is reusable only with attribution

Return the exact obligation. If App cannot render/satisfy it in that flow, the direct-source request is ineligible even though the source status is reusable-with-conditions.

### 5.7 Exact content may be redistributed but not adapted

Direct unmodified reference use may be eligible; generation/adaptation from the source expression is not. App should use the abstract multi-source pattern blueprint instead.

### 5.8 Generation blueprint has strong TELC relevance but weak currentness

Return currentness uncertainty and do not use it for P4 exact target conditions. App can use it for generic/independent B1 practice only if the requested fallback permits.

### 5.9 App asks for a very narrow co-occurrence with sparse evidence

Back off to a broader pair/parent pattern, or return insufficient evidence. Do not turn one striking triple into a generation rule.

### 5.10 A source is removed after an exercise was generated

- If the exercise used only an eligible non-reconstructive pattern and the retained/current blueprint remains decision-grade, it may continue to be valid.
- If the exercise materially used source expression, a close derivative, a now-invalid answer, or a withdrawn target fact, retire/review it according to the impact class.

### 5.11 A taxonomy node splits after learner history exists

Corpus returns migration semantics. App keeps historical evidence but reduces certainty for the new children and collects new direct evidence rather than cloning mastery.

### 5.12 Target TELC format changes

Current P4 requests switch to the new verified target profile. Old source evidence remains historical. App should explain learner evidence gaps rather than pretending an obsolete mock proves current-format coverage.

### 5.13 Contract major version is unsupported

Do not silently consume it. Use a last-supported compatible snapshot/capability where available or an App-curated fallback. Product behavior must fail safely rather than reinterpret eligibility/version meaning.

### 5.14 Corpus returns no decision-grade pattern

This is a valid product outcome. App may use a curated pattern/content fallback or a broader Corpus-supported pattern. “No evidence” must not be converted into a fabricated precise prior.

### 5.15 Learner repeatedly fails a Corpus-low-difficulty pattern

App records a learner-specific weakness and may request easier/scaffolded variants. Corpus does not globally raise difficulty from one learner.

### 5.16 App-generated item performs unexpectedly poorly across many learners later

App may eventually send privacy-safe aggregate calibration evidence. Corpus can update pattern/difficulty priors only under the Stage 07 ability/condition-aware calibration rules. It must not count the generated item as independent reference-exam prevalence evidence.

---

## 6. Relationship to Other Bestehen Stages

### Corpus Stage 13 — Operations

Operations must later make this contract maintainable: review source/pattern eligibility, inspect provenance, correct taxonomy/rights/confidence, trigger reprocessing, and see which downstream App capabilities are affected.

### Corpus Stage 14 — Cost, Scale, and Automation

Stage 14 should size precomputed pattern/analytics bundles, caching/recomputation, model tiers, and processing budgets around this contract. Stage 12 deliberately avoids per-learner Corpus inference.

### Corpus Stage 15 — Security and Abuse

Stage 15 must confirm Corpus does not store personal learner data and must protect source/raw material, untrusted inputs, internal provenance, and any future aggregate calibration channel.

### Corpus Stage 16 — Benchmark Corpus

The benchmark must validate the accuracy/quality gates that make this contract safe: taxonomy mappings, difficulty/relevance, deduplication, source trust/rights classification, correctness-ready answers, and enough representative patterns to exercise P0–P4 requests.

### Corpus Stage 17 — Final PRD

The final Corpus PRD should treat this document as the authoritative Corpus → App responsibility/consumption contract.

### App learner model and progression

App must continue to use the shared stable taxonomy graph, keep direct-evidence modalities separate, and treat P0–P4 as skill-specific realism profiles. Corpus supplies pattern intelligence; App owns progression state.

### App reading/listening/language-elements/writing/speaking stages

Each skill experience may ask for different blueprint facets, but they should all use this common contract rather than defining separate source/rights/confidence semantics.

### App readiness and mocks

Corpus defines target evidence distribution, task/skill/difficulty/condition coverage, and current target facts. App remains responsible for scoring learner evidence, independent written/oral pass constraints, mock assembly/delivery, and readiness interpretation.

---

## 7. Cost Notes

Stage 12 should add **very little recurring runtime cost** if implemented according to the earlier Corpus decisions.

### 7.1 Preferred low-cost default

- Precompute and version taxonomy, difficulty/relevance, target profiles, analytics, and generation blueprints during Corpus ingestion/reprocessing.
- Cache common target/profile/pattern results; the same TELC/P2 Reading pattern can serve many learner decisions.
- Keep learner personalization inside App so Corpus requests remain cacheable and do not require per-user inference.
- Return compact governance/evidence summaries by default; deeper provenance is requested only for reference/debug/admin use.
- Reuse one blueprint across many original App exercises with anti-repetition/diversity constraints rather than paying Corpus to analyze the corpus again for every exercise.
- Recompute only affected outputs when source confidence, rights, taxonomy, currentness, or model versions change.
- Use deterministic contract eligibility from already-computed states rather than another AI call.

### 7.2 Generation cost boundary

The contract does **not** require an expensive model call inside Corpus to generate each exercise. App may later choose deterministic templates, cheaper models, cached content pools, or stronger models depending on exercise type and quality requirements.

Corpus’s role is to make those cheaper options viable by returning explicit constraints instead of requiring a model to infer the target exam pattern from raw source documents each time.

### 7.3 When higher spend is justified

Higher-cost Corpus review/recomputation is justified only when uncertainty materially affects:

- a current TELC target requirement;
- a high-impact generation blueprint;
- a correctness/scoring fact;
- a high-priority taxonomy relationship;
- a unique gap in target evidence;
- a rights/takedown decision;
- a benchmark record used to qualify automation.

No always-on premium AI or per-learner Corpus call is required by Stage 12.

---

## 8. Decisions Made

1. Corpus → App is a capability contract, not a shared database/raw-content contract.
2. The App consumes seven conceptual families: raw/reference content; structured metadata; aggregate statistics; skill relationships; generation patterns/constraints; difficulty/relevance; and governance/version context.
3. Pattern-first consumption is the default; direct source-item delivery is exceptional and rights/product-purpose gated.
4. Corpus returns current use eligibility so App does not reconstruct trust, rights, QA, deduplication, or currentness rules.
5. App describes a desired practice pattern, not the learner profile; personal learner state remains in App.
6. Corpus owns generation blueprints; App owns final original exercise generation, QA, delivery, evaluation, and learner evidence.
7. Requests support P0 assisted foundation, P1 A2, P2 A2/B1 bridge, P3 authentic B1 practice, and P4 current target conditions.
8. P0 is grounded in A2/B1/TELC-relevant precursor evidence without pretending Corpus has an A1 acquisition corpus.
9. “Authentic B1” means authentic difficulty/task behavior unless exact source content is explicitly requested and permitted.
10. Generation blueprints are non-reconstructive and prefer synthesis from multiple independent B+ evidence units/analytics rather than adaptation of one source item.
11. Reference-only/unknown-rights source expression never enters learner-facing generation by default; allowed abstract intelligence may still contribute.
12. Exact reusable content retains component-level action permissions, conditions, and required attribution.
13. Provenance has three exposure levels: compact evidence summary, internal source-lineage drill-down, and exact learner-facing attribution when required.
14. The contract uses semantic compatibility versions conceptually, separate from taxonomy, difficulty/relevance, analytics, target-profile, rights/confidence, and blueprint versions.
15. Stable IDs plus revisions preserve historical App traceability; unsupported contract major versions fail safely rather than being silently reinterpreted.
16. Changes/removals are impact-classified so rights-only removal, trust/correctness invalidation, taxonomy migration, and target-currentness changes produce different downstream behavior.
17. Rights-only removal can leave eligible non-reconstructive intelligence intact; trust/correctness invalidation requires analytical/learner-evidence reevaluation.
18. App owns learner-state repair after Corpus invalidation; Corpus supplies the affected scope and reason.
19. Generated App exercises never become independent reference-exam evidence automatically.
20. The low-cost default is offline/precomputed/cached Corpus intelligence with no per-learner Corpus AI requirement.

---

## 9. Open Questions / Deferred Decisions

### 9.1 Owner questions

**None.** The established project principles are sufficient to define this conceptual boundary without requiring an owner preference.

### 9.2 Deliberately deferred architecture/implementation decisions

- REST vs GraphQL vs RPC vs shared files/database views/other transport;
- endpoint/resource naming and concrete serialization schema;
- push change feed vs pull reconciliation vs deployment-bundled snapshots;
- cache/store technology, TTLs, synchronization, offline behavior, and retry mechanics;
- exact version-negotiation wire format;
- authentication/authorization mechanics between Corpus and App;
- physical lineage/index implementation for affected-record lookup;
- exact anti-copy/similarity algorithm and calibrated generated-content threshold;
- model/provider/template choice used by App to generate exercises;
- exact privacy/aggregation mechanism for future learner-performance calibration feedback.

These choices must preserve the product semantics in this document.

### 9.3 Deferred calibration, not missing product decisions

- Stage 16 must validate thresholds/accuracy for taxonomy, difficulty/relevance, deduplication, trust, rights, and correctness gates used by this contract.
- The exact amount of support required before specific co-occurrence/generation patterns are considered decision-grade remains governed by Stages 03/07/11 and may be recalibrated with the benchmark.
- Current TELC target facts and profiles remain versioned evidence and must be refreshed when provider evidence changes; Stage 12 does not freeze a historical target format.

---

## 10. Definition of Done Check

- [x] Every type of information App needs from Corpus is listed and assigned a purpose.
- [x] Raw/reference content is separated from structured metadata.
- [x] Aggregate statistics are a separate evidence-aware capability.
- [x] Skill graph/relationships are a separate versioned capability compatible with the App learner model.
- [x] Exercise-generation patterns/constraints are defined as non-reconstructive blueprints rather than source items.
- [x] CEFR, L/R/T/A/P difficulty, GB1 relevance, TELC relevance, uncertainty, and currentness remain separate signals.
- [x] App pattern requests are defined conceptually without choosing REST/GraphQL/database architecture.
- [x] Assisted A1, A2, mixed A2/B1, authentic B1, and exact target-condition use cases are explicitly distinguished.
- [x] Original generation is grounded in abstract multi-source evidence without copying restricted source expression.
- [x] Provenance and attribution are returned at the minimum level needed for the requested capability.
- [x] Contract compatibility and underlying taxonomy/model/data versions are independently versioned.
- [x] Source reclassification/removal behavior distinguishes rights-only, trust/correctness, taxonomy, and currentness impacts.
- [x] Corpus versus App ownership is explicit, including generated content, learner state, evaluation, and readiness.
- [x] Low-cost operation is preserved through precomputation, caching, deterministic eligibility, and no per-learner Corpus inference requirement.
- [x] No product decision in this stage requires an owner blocker.

**Stage 12 is product-complete when Bestehen / App can be designed against these capability semantics without needing its design/architecture agents to invent what Corpus returns, how trust/rights/versioning constrain it, or how original practice remains grounded and rights-safe.**
