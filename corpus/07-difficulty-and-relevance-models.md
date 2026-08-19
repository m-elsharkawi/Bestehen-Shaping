# Bestehen / Corpus — Stage 07: Difficulty and Relevance Models

> **Status:** Authoritative Stage 07 product-shaping decision  
> **Product:** Bestehen / Corpus  
> **Initial domain:** German A2–B1 exam and exam-style material  
> **Primary downstream customer:** Bestehen / App  
> **Core principle:** CEFR describes the competence band a task targets; difficulty describes how demanding this particular evidence is and why; generic B1 relevance describes broad exam value; TELC relevance describes value to the target exam. These signals remain separate from source confidence, rights, and learner mastery.

## 1. Purpose and Scope

Stage 07 defines how Bestehen / Corpus describes **how hard exam evidence is, why it is hard, how relevant it is to broad B1 preparation, how relevant it is specifically to TELC B1, and how certain Corpus is about those estimates**.

The problem is deliberately broader than assigning one label such as `B1` or one opaque “difficulty score.” Two tasks can both be valid B1 tasks while placing very different demands on vocabulary, reasoning, speed, audio processing, or productive performance. Likewise, a difficult Goethe B1 task may be valuable generic B1 evidence without being especially representative of TELC B1 format, while a relatively easy TELC task may be extremely important because it reflects a recurring target-exam pattern.

This stage therefore establishes four separate concepts:

1. **CEFR classification** — which competence band the material targets or is declared to target.
2. **Difficulty profile** — how demanding this specific task/item/stimulus is across relevant difficulty dimensions.
3. **Generic B1 relevance** — how useful the evidence is for understanding and training broad B1 exam competence across providers.
4. **TELC B1 relevance** — how strongly the evidence should influence conclusions about the launch target exam.

Each estimated signal also carries **estimate uncertainty/confidence**. Source authenticity/evidence confidence from Stage 03 remains a separate gate controlling how strongly the estimate may influence aggregates.

This is product shaping, not statistical or software architecture. It defines conceptual scores, starting formulas, aggregation rules, confidence gates, recalibration behavior, and edge-case handling. It does not choose an item-response model, database schema, model vendor, feature-extraction implementation, analytics engine, or UI.

### 1.1 Stage objective

**Corpus should be able to say not only “this is B1,” but “this is linguistically moderate, reasoning-heavy, low time pressure, highly TELC-relevant, and still uncertain because the estimate is based on one B-tier source”—without collapsing those facts into one misleading number.**

### 1.2 Product invariants

1. **CEFR is not numerical difficulty.** An A2 task may be harder than an easy B1 task on one or more dimensions without changing its CEFR purpose.
2. **Difficulty is multidimensional.** Linguistic, reasoning/task, timing, audio, and productive demands are separate signals.
3. **A composite difficulty score is optional convenience, not the source of truth.** The dimension profile remains authoritative for diagnosis and matching.
4. **Generic B1 relevance and TELC B1 relevance are separate.** Cross-provider value must not be mistaken for target-format relevance.
5. **Relevance is not confidence.** A task may look highly TELC-relevant while the evidence supporting that claim is weak.
6. **Provider identity is not authenticity.** Stage 03 remains authoritative for trust and officiality.
7. **Rights never determine difficulty or relevance.** Reference-only evidence can inform difficulty/relevance when confidence permits.
8. **Unknown is not zero.** Missing timing, missing audio, missing rubric, or unresolvable features remain unknown rather than “easy.”
9. **Not applicable is not unknown.** Audio difficulty is genuinely N/A for a reading task; it is unknown for a listening task whose audio is missing.
10. **Difficulty estimates are versioned and recalibratable.** Initial model-derived scores are priors, not permanent truth.
11. **Real learner performance must be condition-aware and ability-aware before it changes global Corpus difficulty.** Raw percent-correct is not enough.
12. **Single-user personalization belongs to App.** Corpus does not turn one learner’s struggle into a global item-difficulty fact.

---

## 2. Inputs / Existing Decisions

Stage 07 preserves the shared Product Overview, Identity, both live shaping checklists, and Corpus Stages 01–06.

### 2.1 Stage 01 — mission and target boundary

`corpus/01-product-mission-and-boundaries.md` established that:

- Corpus is broader than TELC while TELC B1 is the strongest target signal;
- Corpus must distinguish general A2/B1 evidence from TELC-specific conclusions;
- App needs difficulty and TELC relevance with uncertainty attached;
- stable exam intelligence should be precomputed rather than generated per learner interaction.

### 2.2 Stage 02 — source strategy

`corpus/02-source-strategy.md` established that official, established-provider, teacher, unofficial, repository/archive, forum/shared, and standalone exercise evidence may all enter Corpus, but source category is not itself confidence. Mirrors are observations rather than extra independent evidence, and older versions remain available as historical evidence.

### 2.3 Stage 03 — trust, authenticity, and confidence

`corpus/03-trust-authenticity-confidence.md` is a hard dependency for this stage. It established:

- evidence-confidence tiers **A/B/C/D** with default eligible aggregate weights **1.00 / 0.70 / 0.25 / 0.00**;
- Quarantined evidence has zero downstream influence;
- **B+ is the default minimum for production difficulty-model influence/calibration**;
- C-tier material may receive provisional difficulty metadata for exploration but must not calibrate production difficulty aggregates;
- learning-priority changes should normally be supported by at least two independent A/B materials, with target-provider evidence for TELC-specific claims;
- one verified official TELC source can establish that a target format/requirement exists, but does not by itself prove prevalence;
- confidence does not decay merely because evidence is old; current target relevance is a Stage 07 concern.

Stage 07 adopts these rules rather than defining a second trust system.

### 2.4 Stage 04 — rights

`corpus/04-rights-and-usage-metadata.md` established that rights are independent from trust and relevance. Reference-only material may still contribute non-reconstructive metadata such as difficulty/relevance when Stage 03 permits. Learner-facing reuse remains separately rights-gated.

### 2.5 Stage 05 — canonical exam model

`corpus/05-canonical-exam-model.md` established the structural units to which difficulty can attach. Difficulty/relevance may be estimated at Item, Task, Stimulus, Asset, Section, and Exam scope where meaningful. Shared passages/audio are represented once, preventing repeated questions from multiplying the same source burden.

### 2.6 Stage 06 — taxonomy

`corpus/06-exam-and-skill-taxonomy.md` established that:

- CEFR classification is explicitly separate from numerical difficulty;
- Listening conditions such as speed, noise, number of speakers, and playback constraints are difficulty/evidence properties, not learner-skill nodes;
- taxonomy defines **what is tested** while Stage 07 defines **how demanding and target-relevant it appears**;
- provider metadata, task shape, skill, reasoning, distractor, topic, grammar, vocabulary, and productive competencies are available as inputs to difficulty/relevance estimation;
- taxonomy assignments themselves have confidence/origin and cannot be treated as perfect input merely because the source is trusted.

### 2.7 Relationship to Bestehen / App

The App already distinguishes assisted/unassisted, timed/untimed, passive/productive, and modality-specific learner evidence. Corpus difficulty must therefore describe the **task and exam conditions**, not a particular learner’s experienced difficulty. The App combines Corpus task difficulty with learner state to decide whether an activity is appropriate and how much evidence a performance should contribute to readiness.

---

## 3. Decisions and Rationale

## 3.1 Use a difficulty profile, not one universal difficulty number

**Decision:** Every eligible task/item should have a **difficulty profile** across the applicable dimensions:

- **L — Linguistic difficulty**
- **R — Task/reasoning difficulty**
- **T — Time-pressure difficulty**
- **A — Audio difficulty**
- **P — Productive-skill difficulty**

The dimensions are scored independently on a provisional **0–100 rubric scale**, with `unknown` and `not_applicable` states.

The profile is authoritative. A section-aware composite may be derived for ranking or coarse matching, but the App and analytics should preserve the dimensions because two tasks with the same composite can require very different capabilities.

### Why this model is preferred

A one-number model creates several product failures:

- a simple-language question with a very deceptive distractor looks identical to a linguistically dense but straightforward question;
- a listening task with easy language but fast, noisy speech is mislabeled;
- a writing task with simple prompt language but heavy content/interaction requirements is understated;
- assistance cannot target the actual source of difficulty;
- future learner-performance recalibration cannot explain which component was misestimated.

A profile keeps the product useful for both Corpus analytics and App coaching.

## 3.2 Use 0–100 as a rubric scale, not a pseudo-scientific probability

**Decision:** Each difficulty dimension uses a 0–100 score anchored to explicit descriptors. The score is **not** an estimated probability of failure and is **not** a CEFR conversion.

Initial interpretation:

| Score | Interpretation within the A2–B1 Corpus domain |
|---:|---|
| **0–19** | Very low demand on this dimension |
| **20–39** | Low demand |
| **40–59** | Moderate demand |
| **60–79** | High demand |
| **80–100** | Very high / unusually demanding within the in-scope domain |

Important guardrails:

- `0` does not mean “A1.”
- `100` does not mean “B2.”
- Scores are comparable only when the same versioned rubric/model is used.
- Adjacent numbers should not be treated as meaningfully different until empirical calibration supports that precision.
- Product UI/consumer logic should normally use bands plus the profile, not behave differently because one item is 61 and another is 62.

## 3.3 Keep CEFR as a categorical target/context label

**Decision:** CEFR remains the Stage 06 classification (`A2`, `B1`, `A2_B1_mixed`, etc.). Numerical difficulty describes demand **inside or around that targeted competence band**.

Examples:

- A very clean B1 reading question may have `CEFR=B1`, `L=42`, `R=35`.
- A dense A2 task with several constraints may have `CEFR=A2`, `L=48`, `R=62`.
- The second task being numerically harder on reasoning does not automatically make it B1.
- A mixed A2–B1 exam may contain locally classified A2 and B1 items with overlapping difficulty distributions.

CEFR/difficulty disagreement is a **review signal**, not an automatic relabeling rule. If an item repeatedly appears far outside the expected range for its declared level, Corpus should review level classification, extraction quality, and difficulty features rather than silently forcing one signal to match the other.

## 3.4 Use two separate relevance scores

**Decision:** Corpus produces two relevance signals, each on a provisional 0–100 scale:

1. **Generic B1 Relevance (`GB1`)** — how useful this evidence is for understanding and training broadly transferable B1 exam competence across providers.
2. **TELC B1 Relevance (`TELC`)** — how strongly this evidence should influence conclusions specifically about the target TELC B1 exam.

This allows meaningful combinations:

| Evidence | Generic B1 relevance | TELC B1 relevance |
|---|---|---|
| Current official TELC B1 task | Usually high | Usually very high |
| Established Goethe/ÖSD B1 task testing a common skill | High | Moderate unless TELC corroboration exists |
| Strong TELC-style third-party mock | Moderate/high | Potentially high score, but estimate confidence/influence is bounded by Stage 03 trust and target-support evidence |
| A2 task showing progression into B1 skill | Moderate | Low/moderate depending on TELC continuity |
| Generic German worksheet with weak exam shape | Low | Low |

Relevance determines **importance**, not whether a source may be reused and not whether its content is trustworthy enough to influence decisions.

## 3.5 Keep score, estimate confidence, and evidence influence separate

**Decision:** Every derived difficulty/relevance signal conceptually has three layers:

1. **Estimated value** — e.g. `R=68`, `TELC=84`.
2. **Estimate confidence/uncertainty** — how certain Corpus is that this value is approximately correct given extraction quality, feature completeness, model validation, and corroboration.
3. **Evidence influence weight** — how strongly this record may affect an aggregate, controlled primarily by Stage 03 confidence, independence/deduplication, target alignment, and currentness.

This prevents a dangerous shortcut such as “high TELC relevance = high trust.” An unverified but realistic TELC-style mock may be scored as highly target-aligned while still having medium/low estimate confidence and bounded aggregate influence.

## 3.6 Preserve estimated and empirical difficulty separately

**Decision:** Initial difficulty is an **estimated content/condition model**. Future real learner performance may create an **empirical calibration layer**. Corpus must preserve both rather than overwriting the original estimate.

Conceptually:

- `estimated_difficulty_profile` — cold-start estimate from source/task features;
- `empirical_difficulty_profile` — calibrated from qualified learner-performance aggregates when sufficient data exists;
- `effective_difficulty_profile` — conservative blend selected according to empirical evidence quality;
- `calibration_context` — population, conditions, sample quality, version, and date range.

This makes model improvements auditable and allows later agents to compare “what Corpus predicted” with “what learners actually experienced.”

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Difficulty attachment and aggregation scopes

Difficulty may attach at different canonical scopes because the cause of difficulty lives in different places.

| Scope | Typical difficulty information |
|---|---|
| **Stimulus** | Linguistic complexity of a passage; information density; visual/layout burden |
| **Audio Asset / listening Stimulus** | Speech rate, clarity, speaker/acoustic conditions, density, playback constraints |
| **Item** | Decisive reasoning operation, distractor confusability, response mechanic |
| **Task** | Shared instructions, multi-item reasoning burden, productive output demand, timing |
| **Section** | Distribution of task/item difficulty under section conditions |
| **Exam/Test Set** | Distribution/profile across sections, not merely one flat average |

### Aggregation rule

Section/Exam difficulty should normally expose:

- weighted mean or median for coarse comparison;
- spread/range or upper-quartile challenge;
- dimension profile;
- evidence/coverage quality.

A single mean must not hide a section containing several very easy tasks and one pass-critical high-demand task. Later analytics may choose the exact statistical summary, but the product requirement is to preserve distribution information.

## 4.2 Common dimension-scoring rules

Each dimension score should be based on observable features or validated semantic classifications, not on model intuition alone.

Every estimate should retain conceptually:

- point/band estimate;
- feature/component breakdown where available;
- method/origin (`deterministic`, `curated`, `model_estimated`, `empirically_calibrated`, etc.);
- model/rubric version;
- estimate confidence and uncertainty interval/band;
- input completeness;
- source/item confidence gate;
- relevant taxonomy assignment confidence.

When a component is **not applicable**, remove it from that dimension’s denominator. When a component should apply but is **unknown**, do not silently renormalize it away; lower estimate confidence or withhold the dimension.

---

## 4.3 Linguistic difficulty (`L`)

### Definition

Linguistic difficulty describes the language-processing burden of the tested input/prompt itself. It is separate from the logical operation required to solve the item and separate from the amount/quality of language a learner must produce.

### Initial components

| Component | Starting weight | What increases difficulty |
|---|---:|---|
| **Lexical demand** | **35%** | Less frequent/less familiar B1 vocabulary, idiomatic or abstract wording, denser lexical variety, weaker clue redundancy, paraphrastic distance |
| **Syntax/morphology demand** | **30%** | Longer dependency spans, subordinate/relative structures, case/reference complexity, dense inflection, multiple clause relations |
| **Cohesion/reference tracking** | **20%** | Pronoun/reference chains, discourse markers, cross-sentence linking, ellipsis, implicit referents |
| **Input density/length burden** | **15%** | More information per unit, longer relevant text, several short texts to compare, limited redundancy |

**Initial conceptual formula:**

`L = 0.35*lexical + 0.30*syntax + 0.20*cohesion + 0.15*density`

All subcomponents use the same 0–100 rubric scale.

### Rules

- For Reading/Listening, `L` measures the language in the tested stimulus plus answer/prompt wording that must be understood.
- For Writing/Speaking, `L` measures the linguistic complexity of the **prompt/input**, while required output capability belongs mainly to `P`.
- Vocabulary/grammar merely present but irrelevant to the answer should not automatically raise `L` as strongly as language that must actually be processed.
- Paraphrase distance can contribute to lexical demand, while the act of matching the paraphrase belongs to `R`/Reading skill.
- Instructions may contribute when misunderstanding them creates genuine task difficulty, but ordinary administrative instruction text should not dominate the linguistic score.

---

## 4.4 Task/reasoning difficulty (`R`)

### Definition

Task/reasoning difficulty describes the cognitive/exam-solving operation required after the learner can basically understand the language. It does **not** claim to measure intelligence.

### Initial components

| Component | Starting weight | What increases difficulty |
|---|---:|---|
| **Reasoning-operation complexity** | **25%** | Multiple sequential operations, inference, updating, constraint filtering, integration rather than direct retrieval |
| **Evidence integration/dispersion** | **25%** | Relevant evidence spread across sentences/texts/speakers; several cues must be combined |
| **Distractor/competitor confusability** | **25%** | Plausible near-matches, partial truths, shared keywords, superseded information, subtle scope/negation differences |
| **Response-mechanic complexity** | **15%** | Matching banks, multi-select cardinality, ordering, several linked fields, error-prone response rules |
| **Working-memory/attention burden** | **10%** | Retaining several constraints, tracking speaker/reference changes, comparing many candidates before choosing |

**Initial conceptual formula:**

`R = 0.25*operations + 0.25*integration + 0.25*distractors + 0.15*response_mechanic + 0.10*memory`

### Rules

- A direct explicit-fact question with difficult vocabulary can have high `L` but low `R`.
- A simple-language matching task with many plausible competitors can have low/moderate `L` but high `R`.
- Distractor difficulty requires a defensible answer and mechanism. Disputed keys block high-confidence distractor-based scoring.
- Productive tasks can have reasoning/planning demand, but output scope, interaction, and language production are represented primarily by `P`.
- Task instructions that impose selection cardinality or unusual response rules can raise response-mechanic difficulty.

---

## 4.5 Time-pressure difficulty (`T`)

### Definition

Time-pressure difficulty describes **how demanding the required work is relative to the available exam time and irreversibility constraints**. It is not merely the number of minutes printed on the page.

### Initial components

| Component | Starting weight | What increases difficulty |
|---|---:|---|
| **Work-to-time ratio** | **50%** | More text/audio/options/output per available minute; tighter section budget |
| **Navigation/response overhead** | **20%** | Many items/options/pages/fields, matching transfer, answer-sheet overhead, repeated context switching |
| **Irreversibility/limited opportunity** | **15%** | One-pass or limited-play input, no return, fixed transition, expiring preparation time |
| **Buffer scarcity** | **15%** | Little reasonable checking/recovery time after normal completion |

**Initial conceptual formula:**

`T = 0.50*work_time_ratio + 0.20*overhead + 0.15*irreversibility + 0.15*buffer_scarcity`

### Rules

- If the provider/source does not establish an applicable time limit, `T=unknown`, not zero.
- A standalone untimed teacher exercise may have no exam-condition `T`; an App training mode can later impose its own timing, but that is App exercise configuration rather than source truth.
- Listening playback restrictions contribute to `A` and may also affect `T` when they materially remove recovery time. Avoid double-counting the same feature at full weight in both dimensions.
- Productive preparation time and response time are part of the timing profile; spontaneity/planning complexity also contributes to `P`.
- Learner slowness is not Corpus time pressure. App compares learner time with task `T` and target conditions.

---

## 4.6 Audio difficulty (`A`)

### Definition

Audio difficulty describes the acoustic and spoken-input burden of a listening stimulus. It applies to genuine audio/video listening evidence, not to a transcript alone.

### Initial components

| Component | Starting weight | What increases difficulty |
|---|---:|---|
| **Speech rate / pause structure** | **25%** | Faster rate, short pauses, fewer natural processing gaps |
| **Clarity / connected speech** | **20%** | Reductions, elisions, less careful articulation, weaker segmentation cues |
| **Speaker complexity** | **15%** | More speakers, quick turn changes, less obvious speaker identity, overlap |
| **Acoustic conditions** | **15%** | Background noise, room effects, phone/loudspeaker quality, uneven volume |
| **Information density** | **15%** | Many relevant facts, numbers, changes, conditions, low redundancy per time unit |
| **Playback constraints** | **10%** | Limited replay, one-pass delivery, little preview/recovery where source-defined |

**Initial conceptual formula:**

`A = 0.25*rate + 0.20*clarity + 0.15*speakers + 0.15*acoustics + 0.15*density + 0.10*playback`

### Rules

- Transcript complexity contributes to `L`; audio-specific realization contributes to `A`.
- If audio is missing but a transcript exists, `A=unknown`; do not infer acoustic difficulty from text.
- Synthetic or regenerated App audio has its own delivery-condition difficulty. Corpus source `A` should describe the observed source asset/version.
- Accent variation matters only insofar as it affects intelligibility/processing in the observed target context. Do not encode accent prejudice as difficulty.
- Number/date/time corrections can increase both `A` information density and `R` update-after-correction demand; the profile intentionally shows both burdens.

---

## 4.7 Productive-skill difficulty (`P`)

### Definition

Productive difficulty describes how demanding a Writing or Speaking task is to complete at B1-sufficient communicative quality. It is not a score of a learner’s response.

### Initial common components

| Component | Starting weight | What increases difficulty |
|---|---:|---|
| **Content/task scope** | **20%** | More required points, constraints, functions, or information that must be covered coherently |
| **Language range/control demand** | **20%** | Broader lexical/grammatical resources needed to fulfill the task naturally enough at B1 |
| **Organization/coherence demand** | **15%** | Longer structure, sequencing, linking, argument/plan organization |
| **Spontaneity/planning constraint** | **15%** | Less preparation, faster response, more on-the-fly formulation |
| **Interaction/contingency demand** | **15%** | Responding to partner, turn-taking, negotiation, adapting to new input |
| **Register/convention demand** | **10%** | Formality, recipient fit, email conventions, polite negotiation, task-format constraints |
| **Output length/continuity demand** | **5%** | Longer sustained writing/speech or greater continuity before task completion |

**Initial conceptual formula:**

`P = 0.20*scope + 0.20*language_demand + 0.15*organization + 0.15*spontaneity + 0.15*interaction + 0.10*register + 0.05*continuity`

For a component that is genuinely N/A, such as interaction in an individual writing task, the applicable components are renormalized.

### Writing-specific interpretation

Writing difficulty rises with:

- number and interaction of required content points;
- need to explain, justify, propose, complain, compare, or negotiate rather than simply state facts;
- register/convention requirements;
- organizational length and coherence burden;
- time pressure and revision constraints.

A sample answer does not define productive difficulty by its sophistication. Difficulty is based on what the task/rubric requires for sufficient performance.

### Speaking-specific interpretation

Speaking difficulty rises with:

- interaction and contingency;
- need to listen/respond, propose, disagree, negotiate, justify, repair, and maintain exchange;
- limited preparation;
- sustained monologue/continuity requirements;
- changing partner input or constraints;
- simultaneous task fulfillment and interaction management.

A monologue has `interaction=N/A`; collaborative planning normally has substantial interaction demand.

### Rubric uncertainty rule

If productive instructions exist but rubric/scoring evidence is missing, `P` may still be estimated from observable prompt demands but must carry lower confidence. Do not infer hidden provider expectations merely to complete the score.

---

## 4.8 Section-aware composite difficulty

**Decision:** Corpus may derive a **Composite Difficulty Index (`D`)** for sorting, coarse matching, or aggregate analysis, but it must always retain the underlying profile.

Starting section weights:

| Section | Linguistic `L` | Reasoning `R` | Timing `T` | Audio `A` | Productive `P` |
|---|---:|---:|---:|---:|---:|
| **Reading** | 40% | 45% | 15% | N/A | N/A |
| **Language Elements** | 50% | 40% | 10% | N/A | N/A |
| **Listening** | 20% | 25% | 10% | 45% | N/A |
| **Writing** | 15% | 15% | 15% | N/A | 55% |
| **Speaking** | 15% | 10% | 15% | N/A by default | 60% |

`D = weighted mean of applicable known dimensions`.

### Composite guardrails

1. These weights are **starting product defaults**, not empirically validated constants.
2. The profile is more important than the composite.
3. `N/A` dimensions are removed/renormalized.
4. `Unknown` dimensions are **not** silently removed when they should apply. If known-dimension coverage represents less than about **75% of expected composite weight**, Corpus should withhold the composite or label it partial/low-confidence.
5. Integrated tasks should normally expose a profile rather than force one section formula; a documented blend may be used only when the task structure supports it.
6. The App may create its own **learner challenge estimate** using Corpus `D` plus learner mastery/conditions. That learner-specific value is not written back as Corpus difficulty.

---

## 4.9 Difficulty estimate confidence and AI uncertainty

**Decision:** Every non-trivial estimated difficulty score must carry **estimate confidence** separately from Stage 03 source confidence.

### Drivers of estimate confidence

Initial product factors are:

- **input/feature completeness** — are the relevant text, audio, timing, rubric, choices, and task relationships present?
- **extraction quality** — is OCR/ASR/layout/audio mapping trustworthy enough for the features used?
- **taxonomy/tag confidence** — are the primary skill/reasoning/distractor mappings reliable?
- **method benchmark quality** — has the scoring/classification method been validated for this section/task family?
- **cross-method/source agreement** — where multiple defensible signals exist, do they agree?

Stage 03 evidence confidence remains an external publication/influence gate; it is not duplicated inside the estimate-confidence score.

### Initial confidence bands

| Estimate confidence | Meaning | Default posture |
|---|---|---|
| **High (80–100)** | Inputs largely complete; method is benchmarked/reliable for this task type; no material contradiction | Fine score/band can be used for normal App matching and analytics when Stage 03 confidence also passes |
| **Medium (60–79)** | Useful estimate with some uncertainty | Use the band/profile; avoid fine ranking where small differences matter |
| **Low (<60)** | Missing/weak inputs, unvalidated method, or meaningful disagreement | Internal/provisional use; App should prefer broader band or unknown rather than precise score |

The thresholds are starting defaults for product behavior, not calibrated probabilities.

### Uncertainty interval/band

Before empirical calibration, the score should support an explicit **uncertainty envelope**, for example:

- High confidence: approximate narrow band around the point estimate;
- Medium: broader band;
- Low: broad band or only qualitative difficulty category.

A starting representation may use roughly **±8 / ±15 / ±25 points** for High / Medium / Low confidence. These are **engineering/product uncertainty envelopes, not statistical confidence intervals** and should be replaced by benchmark-derived error distributions when Stage 16/real data supports that.

### AI-specific rule

A model’s self-reported confidence is not sufficient. AI-estimated difficulty becomes production-grade only after benchmark evidence demonstrates acceptable error for the relevant dimension/task slice. Until then, machine estimates remain provisional or are expressed as broad bands.

---

## 4.10 Generic B1 relevance (`GB1`)

### Definition

Generic B1 relevance estimates how much a task/pattern should matter when reasoning about **broad B1 exam competence**, independent of TELC-specific format.

### Initial components

| Component | Starting weight | Meaning |
|---|---:|---|
| **B1 level fit** | **30%** | How directly the evidence targets B1 competence rather than mainly A2 progression or incidental higher/lower material |
| **Skill/task centrality** | **25%** | Whether it tests a stable, important B1 exam capability rather than a one-off content quirk |
| **Cross-provider recurrence** | **25%** | Independent appearance across credible B1 exam families/materials |
| **Transfer/generalization value** | **20%** | Whether the underlying skill/pattern transfers across topics/providers and can productively shape training |

**Initial conceptual formula:**

`GB1 = 0.30*level_fit + 0.25*centrality + 0.25*cross_provider + 0.20*transfer`

### Relevance bands

| Score | Meaning |
|---:|---|
| **80–100** | Very high / core B1 relevance |
| **60–79** | Strong relevance |
| **40–59** | Moderate/supporting relevance |
| **20–39** | Weak/specialized relevance |
| **0–19** | Incidental or effectively out of scope for B1 prioritization |

### Rules

- A2 evidence can have moderate GB1 when it strongly represents a precursor/progression pattern, but it should not score as if it directly demonstrates B1 performance.
- One provider-specific oddity should not become highly generic merely because it is official.
- Cross-provider recurrence is computed only over independent eligible evidence; mirrors do not count.
- Relevance can apply to taxonomy nodes/patterns as well as individual tasks once Stage 11 aggregates evidence.

---

## 4.11 TELC B1 relevance (`TELC`)

### Definition

TELC relevance estimates how much evidence should influence **what Bestehen teaches, generates, benchmarks, and emphasizes because TELC B1 is the launch target**.

### Initial components

| Component | Starting weight | Meaning |
|---|---:|---|
| **Target format/task alignment** | **30%** | How closely the task mechanics, section role, response behavior, reasoning/distractor shape, and delivery conditions match TELC B1 evidence |
| **Direct TELC support** | **25%** | Strength/directness of evidence that the pattern belongs to the TELC B1 target family |
| **TELC recurrence/prevalence** | **20%** | Independent recurrence across eligible TELC/TELC-relevant materials |
| **Scoring/section exposure** | **15%** | How much the pattern can affect target-exam points, section performance, or pass-critical preparation |
| **Currentness** | **10%** | Whether evidence remains representative of the current target format rather than a superseded/historical configuration |

**Initial conceptual formula:**

`TELC = 0.30*format_alignment + 0.25*direct_support + 0.20*recurrence + 0.15*score_exposure + 0.10*currentness`

The same 0–100 relevance bands used for GB1 apply.

### TELC-specific rules

1. **One verified official TELC source can establish existence/requirement** and produce strong direct-support evidence, but cannot by itself establish prevalence.
2. **Relative priority/frequency should normally require at least two independent A/B materials**, preserving Stage 03’s corroboration rule.
3. A non-TELC B1 task can have meaningful TELC relevance when its skill/pattern is independently corroborated in TELC, but cross-provider recurrence alone does not prove TELC format.
4. A third-party TELC-style mock can score high on format alignment while still carrying lower estimate confidence/influence if provenance or target support is weaker.
5. Historical official TELC evidence does not lose authenticity with age. Its **currentness component** falls only when there is evidence that the relevant format/rule/pattern has changed or become less representative.
6. If currentness is unknown, preserve uncertainty rather than automatically penalizing every older source by date.
7. TELC relevance must not be used to imply affiliation, endorsement, or official status.

---

## 4.12 Provider/source weighting principles

Provider/source weighting is used when **aggregating evidence**, not as a replacement for the individual relevance score.

### 4.12.1 Evidence contribution formula

A conceptual contribution weight for an observation/material is:

`EvidenceContribution = Independence × Stage03ConfidenceWeight × TargetAlignment × Currentness × ScopeFit`

Where:

- **Independence** neutralizes mirrors/duplicates/derivatives according to Stage 09. Until independence is resolved, count conservatively rather than assuming distinct evidence.
- **Stage03ConfidenceWeight** uses Stage 03’s A/B/C/D defaults where the use permits that tier.
- **TargetAlignment** expresses how directly the evidence family informs the analytical question.
- **Currentness** applies only where format currency matters; authenticity does not decay automatically.
- **ScopeFit** prevents a standalone fragment from being treated as evidence of whole-exam section balance, or an A2 task as direct B1 prevalence evidence.

These factors should remain inspectable rather than being collapsed into an unexplained source reputation number.

### 4.12.2 Starting target-alignment multipliers for TELC-specific aggregates

These are **priors for aggregate evidence contribution**, not hard relevance scores and not trust judgments.

| Evidence family | Starting TELC target-alignment prior |
|---|---:|
| **Verified/current TELC B1 target material** | **1.00** |
| **Verified official-derived copy of the same TELC material** | Same underlying prior, but **not another independent unit** |
| **TELC A2–B1 / closely related TELC-family progression evidence** | **0.75** |
| **B+ verified third-party TELC-style mock/practice** | **0.60** |
| **Established non-TELC B1 provider evidence** | **0.40** before task-specific TELC corroboration |
| **Generic B1 third-party B+ evidence without TELC-specific support** | **0.30** |
| **A2 non-TELC progression evidence** | **0.20** |
| **Unresolved/weak target identity** | Conservative/low until reviewed; never promoted by resemblance alone |

Task-level evidence can justify a different effective alignment from the family prior, but the reason must be explicit. For example, a Goethe reading pattern independently shown to recur in trusted TELC tasks can become more relevant to the TELC-specific analytical question than the initial provider prior suggests.

### 4.12.3 Starting alignment for generic B1 aggregates

For a **generic B1** question, established B1 evidence from TELC, Goethe, ÖSD, DTZ, and other credible established providers should generally begin on similar footing after Stage 03 confidence/independence treatment. Third-party B+ evidence may contribute meaningfully without a blanket penalty simply because it is unofficial; its actual confidence and independence matter more.

A2 evidence receives lower direct B1-prevalence weight but can receive meaningful progression/support weight.

### 4.12.4 Provider weighting principles

- **Target exam first, not target exam only.** TELC dominates TELC-specific claims; cross-provider evidence strengthens general language/skill conclusions.
- **Officiality anchors target facts, not all prevalence.** One official example can prove existence, not frequency.
- **Credible unofficial material adds breadth, not authority by repetition.** B+ unofficial material can materially contribute; mirrors and low-confidence copies cannot.
- **Current format evidence beats historical format evidence for present-target behavior**, while historical evidence remains useful for stable skills and progression.
- **Provider/source weighting never overrides a local defect.** A disputed item in official material remains disputed.

---

## 4.13 Limiting low-confidence and unofficial influence

**Decision:** Stage 03’s tier rules are strengthened with explicit Stage 07 aggregate caps.

### Difficulty calibration

- **A/B only** may calibrate production difficulty aggregates.
- A contributes at Stage 03 weight `1.00`; B at `0.70`.
- **C contributes zero to production difficulty calibration**, even though a provisional difficulty annotation may exist for internal exploration.
- D and Quarantined contribute zero.

### Published relevance / priority analytics

- A/B evidence must materially support every decision-grade aggregate conclusion.
- C may contribute supporting context at Stage 03 weight `0.25`, but its **total effective contribution is capped at 15% of aggregate evidence mass** for a published relevance/priority result.
- A C-only evidence set returns **insufficient decision-grade evidence**, not a confident relevance score.
- C evidence alone may not move a pattern into a higher relevance band or create a learner-priority recommendation.
- D/Quarantined evidence has zero influence.

The 15% cap is an initial safety default to be tested in Stage 16/11 rather than a permanent statistical constant.

### Unofficial-material guardrail for TELC-specific claims

Unofficial does **not** mean untrusted; Stage 03 confidence remains authoritative. However, target-exam claims should remain anchored in target evidence.

Initial rule:

- When eligible official TELC evidence exists for a TELC-specific aggregate, **unofficial/third-party evidence should normally provide no more than 35% of effective support for a “high-confidence” target-specific conclusion**.
- If third-party evidence provides most of the support because official material is sparse, Corpus may still surface a high estimated TELC-relevance **candidate**, but the relevance-confidence band must remain provisional/medium or lower until target evidence improves.
- Third-party consensus cannot override a contradictory verified current official TELC requirement without manual review.

This cap applies to **confidence in the target-specific conclusion**, not to whether third-party material may exist in the corpus or receive a high task-level alignment score.

---

## 4.14 Relevance-confidence and evidence sufficiency

A relevance score needs an uncertainty/confidence layer just like difficulty.

### High-confidence TELC relevance generally requires

- strong/clear task-format mapping;
- B+ supporting evidence;
- duplicate-neutral independent support appropriate to the claim;
- at least one direct TELC-relevant source for target-specific conclusions;
- adequate currentness evidence when provider format may have changed;
- no unresolved local structural/key conflict that changes the interpretation.

### Evidence sufficiency rules

- **Existence/requirement claim:** one verified official Tier A TELC source may be enough.
- **Relative recurrence/priority claim:** normally at least **two independent A/B materials**, preserving Stage 03.
- **High-confidence provider-pattern prevalence:** should use more than one underlying target evidence unit when available; Stage 11/16 will set empirical support thresholds.
- **Generic B1 claim:** can be strongly supported by independent A/B evidence across established providers even when no TELC source is involved.

Corpus should expose support counts/effective evidence mass with the result so later App/analytics logic can distinguish “high score from one anchor source” from “high score with broad recurrence.”

---

## 4.15 Aggregating task/node difficulty and relevance

Later Corpus analytics will aggregate from items/tasks into patterns, skill nodes, provider comparisons, and sections. Stage 07 locks these product rules:

1. **Deduplicate first.** Aggregate only over independent evidence units once Stage 09 resolves relationships.
2. **Apply local confidence before parent confidence.** A trusted exam does not rescue a disputed item.
3. **Apply use-specific confidence eligibility.** C may support relevance exploration but cannot calibrate production difficulty.
4. **Use weighted distributions, not just raw means.** Preserve median/percentiles/spread or equivalent distribution information.
5. **Expose support strength.** Include independent material count/effective evidence mass and confidence band.
6. **Do not let source volume dominate.** One publisher generating thousands of similar items should not overwhelm several independent exam families merely by item count.
7. **Separate item difficulty from pattern relevance.** A frequently tested pattern may be easy; a rare pattern may be very hard. Both facts matter differently to coaching.
8. **Separate relevance from scoring exposure.** A very frequent low-point detail and a less frequent pass-critical productive competency can both be important for different reasons.

---

## 4.16 Future recalibration using real learner performance

### 4.16.1 Recalibration goal

Future learner data should answer:

- Are the estimated task/dimension scores ordered correctly?
- Which feature weights are systematically wrong?
- Which task types are harder/easier than content analysis predicts?
- How much does timing/audio condition change performance?
- Which Corpus patterns transfer poorly from assisted training to exam-realistic conditions?

The goal is **not** to replace difficulty with raw success rate.

### 4.16.2 Qualified objective-task attempts

A learner attempt is suitable for **global Corpus empirical difficulty** only when the system can identify enough context to avoid contamination.

Preferred calibration evidence:

- known task/exercise version and canonical mappings;
- first-seen or otherwise non-memorized attempt;
- answer not previously exposed;
- assistance state known;
- timing state known;
- audio replay/speed condition known where applicable;
- completion/response captured reliably;
- learner ability/readiness context available in aggregate form;
- no broken/disputed key or evaluation defect.

Retries after diagnosis/repair are valuable for App learning but should not be treated as independent cold-attempt difficulty observations.

### 4.16.3 Ability adjustment is mandatory for global calibration

**Decision:** Raw percent-correct does not become global difficulty because performance is confounded by learner ability.

Future empirical calibration should use an ability-adjusted model, for example a Rasch/IRT-style latent-difficulty approach or another validated equivalent. Stage 07 does not choose the statistical implementation, but it requires the product semantics:

- high-performing learners getting an item wrong is stronger difficulty evidence than beginners getting it wrong;
- easy items completed by advanced learners do not establish A2/B1 placement by themselves;
- calibration populations/ability range must be recorded;
- difficulty estimates should not drift merely because the user population changes.

### 4.16.4 Personal-project / single-learner phase

Bestehen may initially have only one real learner. In that phase:

- learner performance **personalizes App challenge and evidence weighting**;
- repeated divergence between Corpus prediction and the learner experience may flag a task/pattern for review;
- **do not globally recalibrate Corpus item difficulty from one learner**;
- single-user results may be retained as App evidence or a candidate calibration signal, not as decision-grade global difficulty.

This preserves the distinction between “hard for this learner” and “hard in the target domain.”

### 4.16.5 When the App serves original generated exercises rather than source items

Most reference source items will not be shown directly because of rights/product strategy. Therefore:

- if the **exact calibrated item** was delivered lawfully, performance may calibrate that item/task directly;
- if the App served an **original equivalent exercise**, performance calibrates the **exercise and shared pattern/dimension model**, not the exact reference source item;
- repeated performance across many original exercises mapped to the same task/skill/reasoning pattern can recalibrate pattern-level priors and the coefficients used to estimate new Corpus items;
- Corpus must not claim “source item X has empirical difficulty 68” when no learner has actually attempted X.

### 4.16.6 Productive-task calibration

Writing/Speaking cannot use binary correctness. Qualified empirical evidence may include:

- normalized rubric attainment against B1-sufficient criteria;
- rate of full task/content-point completion;
- completion under time;
- interaction breakdown/recovery for speaking;
- evaluator confidence/reliability;
- learner ability/readiness context;
- repeated evidence across comparable prompts.

The empirical difficulty question becomes: **how demanding is this task for a learner of a given ability to achieve B1-sufficient performance under the specified conditions?**

### 4.16.7 Timing and audio recalibration

- `T` can be recalibrated using completion-time distributions, timeout/blank rates, checking-buffer behavior, and performance degradation under target timing.
- `A` can be recalibrated by comparing qualified listening performance across speed/noise/speaker/playback conditions while controlling for learner ability and Listening skill.
- Assisted/replayed/slowed attempts should not calibrate exam-realistic audio difficulty as though they were target-condition attempts.

### 4.16.8 Conservative estimated/empirical blending

**Decision:** Empirical data should gradually override the cold-start estimate rather than replacing it after a small sample.

Conceptually:

`EffectiveDifficulty = (1 - λ) * EstimatedDifficulty + λ * EmpiricalDifficulty`

where `λ` grows with **quality-adjusted effective sample size, learner-ability coverage, evaluator reliability, and condition match**.

A reasonable starting shrinkage concept is:

`λ_base = n_eff / (n_eff + 50)`

then reduce/cap `λ` when the calibration cohort is narrow, conditions mismatch, evaluator quality is weak, or data is highly clustered. The constant `50` is a conservative starting prior-strength, not a locked architecture parameter; Stage 16/real data should recalibrate it.

### 4.16.9 Recalibration targets

Learner data may update, in increasing order of risk:

1. uncertainty/error ranges for existing difficulty estimates;
2. component weights within L/R/T/A/P;
3. section composite weights;
4. pattern/task-family priors;
5. individual item/task empirical difficulty where directly observed;
6. relevance/prioritization only indirectly, when performance data demonstrates that a supposedly important pattern does or does not materially predict target exam success.

TELC relevance should not be redefined simply because learners find a pattern difficult. **Importance and difficulty remain separate.**

### 4.16.10 Privacy/product boundary

Corpus should consume only the **privacy-safe aggregate learner-performance signals necessary for calibration**. App remains the owner of personal learner history. Exact privacy/aggregation implementation belongs to the later Corpus→App contract/security stages.

---

## 5. Edge Cases / Failure or Uncertainty Handling

### 5.1 Easy B1 item

Keep `CEFR=B1` with low/moderate difficulty. Do not downgrade it to A2 simply to make the labels correlate.

### 5.2 Hard A2 item

Keep `CEFR=A2` if that remains the defensible target classification. High reasoning/timing difficulty may trigger review, but difficulty does not automatically promote CEFR.

### 5.3 Missing timing information

`T=unknown`. A source being usable untimed does not mean it has low time pressure in the real exam.

### 5.4 Listening transcript exists but audio is missing

Estimate `L` from the transcript if appropriate and confidence permits; `A=unknown`. Do not infer speech rate/noise/clarity from text.

### 5.5 Audio exists but transcript/ASR is unreliable

`A` may still be partially measurable from acoustic features, but `L`/information-density estimates requiring transcript semantics have lower confidence. Preserve separate uncertainties.

### 5.6 Writing/speaking task without rubric

Estimate observable prompt/output demands conservatively; lower `P` confidence. Do not invent hidden scoring expectations.

### 5.7 Disputed objective answer

Reasoning/distractor components depending on the disputed correctness remain unknown/blocked. Linguistic or topic features independent of the key may remain usable.

### 5.8 One very old official TELC exam

It may remain Tier A authentic evidence. Currentness can be high, medium, low, or unknown depending on evidence of format continuity—not simply publication age.

### 5.9 One current official TELC model task appears once

It can establish that the task/requirement exists and may receive high TELC alignment. Prevalence/relative priority remains uncertain until independent support exists.

### 5.10 Many unofficial mirrors contain the same mock

Count one underlying evidence unit after deduplication. Mirror count does not increase confidence, recurrence, or relevance.

### 5.11 Many independent B+ third-party TELC-style mocks show one pattern absent from official evidence

Surface it as a candidate target pattern with bounded TELC relevance-confidence. It may affect exploratory analytics, but should not become a high-confidence target requirement/prevalence claim without target corroboration.

### 5.12 Current official evidence contradicts older or unofficial evidence

Preserve the disagreement. For current target behavior, verified current official evidence normally receives the strongest direct-target/currentness contribution. Escalate when the contradiction materially changes App priorities or format assumptions.

### 5.13 Standalone exercise is very difficult

Difficulty may be estimated normally for its Task/Item. Do not use the standalone exercise to infer whole-exam difficulty or section balance.

### 5.14 Mixed A2–B1 exam

Keep Exam-level CEFR mixed. Estimate local task/item difficulty independently. Aggregate progression analysis should compare distributions rather than invent one “A2.6/B1.2” pseudo-level.

### 5.15 Integrated receptive/productive task

Report all applicable dimensions. Prefer the difficulty profile over a forced section composite unless the provider’s structure supplies a defensible weighting.

### 5.16 Learners perform better because they saw the same item before

Treat repeat exposure/memorization as contaminated for cold-item empirical difficulty. Keep it useful for App review/retention evidence, not global first-attempt calibration.

### 5.17 Generated exercise is harder than its reference pattern

Calibrate the generated exercise separately and use the divergence to improve pattern/dimension generation controls. Do not rewrite the reference item’s difficulty unless direct evidence supports it.

### 5.18 One learner repeatedly fails a low-difficulty item family

App should treat this as a learner weakness. Corpus may flag the model for review but does not globally raise difficulty from one learner.

### 5.19 Large learner dataset comes mostly from beginners

Ability-adjust before global calibration. Raw failure rate would otherwise make ordinary B1 tasks look artificially extreme.

### 5.20 Rights takedown removes source expression

When Stage 04 allows retention of non-reconstructive metadata, difficulty/relevance may remain as historical intelligence with removal provenance. If the evidence itself is invalidated, recompute/discount according to Stage 03/04.

---

## 6. Relationship to Other Bestehen Stages

### Stage 08 — Ingestion Pipeline

Stage 08 should define where deterministic features are extracted, where semantic difficulty/relevance enrichment occurs, how estimate origin/model/rubric version is recorded, and how unknown/partial inputs trigger reprocessing or review. Ingestion success must not imply a complete difficulty profile.

### Stage 09 — Duplicate and Near-Duplicate Detection

Stage 09 is required before recurrence/relevance/provider weighting is decision-grade. Mirrors and derivatives must be neutralized before evidence mass is calculated. Difficulty may be copied/inherited between confirmed exact duplicates only with provenance/version logic; adaptations may have different difficulty.

### Stage 10 — Validation and QA

Stage 10 should validate difficulty-component inputs, AI estimate error by section/dimension, audio/timing extraction, productive-demand mapping, and relevance classification. Production estimates need benchmark-based quality rather than model self-confidence.

### Stage 11 — Corpus Analytics

Stage 11 should implement duplicate-neutral weighted distributions, effective evidence mass, provider comparisons, TELC-vs-generic B1 relevance, A2→B1 difficulty progression, and low-confidence caps defined here.

### Stage 12 — Corpus → App Contract

The App should be able to consume:

- CEFR separately from difficulty;
- L/R/T/A/P profile and optional composite;
- difficulty estimate confidence/uncertainty and version;
- GB1 and TELC relevance separately;
- relevance confidence/support strength;
- applicable exam-condition facts such as timing/playback;
- provenance/rights only where needed for source-backed use.

The App should not need to reconstruct source weighting from raw URLs.

### Stage 13 — Corpus Operations

Operations should support review of anomalous CEFR/difficulty mismatches, low-confidence high-relevance candidates, outdated/currentness questions, model-versus-empirical divergence, and manual overrides with rationale.

### Stage 14 — Cost, Scale, and Automation

Stage 14 should make difficulty/relevance enrichment offline, cached, and incremental. Expensive model review should be reserved for high-impact ambiguity or benchmark failures, not every item.

### Stage 15 — Security and privacy boundary

Any future learner-performance feedback into Corpus must be aggregate/privacy-safe and must not turn Corpus into the personal learner-data store.

### Stage 16 — Initial Benchmark Corpus

The benchmark should manually annotate representative L/R/T/A/P profiles, GB1/TELC relevance, and uncertainty across providers/sections/source tiers. It should test whether starting weights order examples sensibly, measure model error, and recalibrate the provisional thresholds/uncertainty envelopes.

### Stage 17 — Final Product Specification

The final PRD must preserve the separation among CEFR, difficulty, relevance, confidence, rights, and learner mastery, plus the empirical-recalibration path.

### Relationship to Bestehen / App

Corpus answers:

> **How demanding is this exam evidence, why is it demanding, and how much should it matter for the target?**

App answers:

> **How difficult is this for this learner right now, what assistance should be used, and what does the result mean for readiness?**

The two values are connected but intentionally not identical.

---

## 7. Cost Notes

Difficulty/relevance enrichment has meaningful ingestion/reprocessing cost but **should create no per-learner recurring inference requirement**.

### 7.1 Preferred low-cost default

- Extract deterministic features first: text/audio length, response cardinality, option counts, source timing, playback rules, speaker count where reliable, scoring exposure, provider/CEFR/section/task metadata.
- Reuse Stage 06 taxonomy tags rather than asking another model to rediscover the same task/skill/reasoning concepts.
- Use local/open-source or lower-cost models for lexical/syntactic metrics and broad semantic difficulty when benchmark quality is adequate.
- Analyze a shared Stimulus/audio once and reuse its L/A features across dependent Items.
- Batch semantic difficulty/relevance estimation offline.
- Cache scores by content/model/taxonomy/rubric version and only recompute when a relevant input changes.
- Keep low-confidence estimates broad/provisional instead of paying to resolve every case.
- Reserve human/premium-model review for high-value TELC evidence, benchmark examples, anomalous model disagreement, productive tasks where cheap models are materially unreliable, and cases that would change learner priorities.

### 7.2 Cheaper fallback

If a fine-grained estimate cannot be produced cheaply and reliably:

- return a broader difficulty band;
- leave the affected dimension unknown;
- use a trusted section/task-family prior with low confidence;
- keep the record out of production aggregates until better evidence arrives.

Unknown is cheaper and safer than fabricated precision.

### 7.3 What justifies higher spend later

Higher-cost processing is justified when benchmark/learner data shows that cheaper estimates materially damage:

- task matching/progression for an A1→B1 learner;
- diagnosis of why an activity is hard;
- TELC-specific prioritization;
- mock-exam realism;
- difficulty calibration for high-value task families;
- benchmark/gold-standard quality.

### 7.4 Learner-data calibration cost

Global learner-performance recalibration should be **periodic/batched**, not recomputed on every attempt. The App can update personal learner state immediately while Corpus receives aggregated calibration batches later when enough evidence exists.

No expensive real-time statistical or AI pipeline is a Stage 07 product requirement.

---

## 8. Decisions Made

1. Difficulty is a five-dimension profile: Linguistic (`L`), Task/Reasoning (`R`), Time Pressure (`T`), Audio (`A`), and Productive Skill (`P`).
2. Each dimension uses a provisional 0–100 rubric scale with explicit qualitative bands, `unknown`, and `not_applicable`.
3. CEFR remains categorical and is not derived from the numerical difficulty score.
4. CEFR/difficulty disagreement triggers review rather than automatic relabeling.
5. `L` measures lexical, syntactic, cohesion/reference, and input-density burden.
6. `R` measures reasoning operations, evidence integration, distractor confusability, response mechanics, and working-memory/attention burden.
7. `T` measures work relative to available time, response/navigation overhead, irreversibility, and buffer scarcity; missing timing is unknown rather than easy.
8. `A` measures rate, connected-speech clarity, speaker complexity, acoustic conditions, information density, and playback restrictions; transcript-only evidence cannot establish audio difficulty.
9. `P` measures productive content scope, language demand, organization, spontaneity/planning, interaction, register/conventions, and continuity, with writing/speaking-specific interpretation.
10. Section-aware composite difficulty is allowed for coarse ranking, but the dimension profile remains authoritative and composites are withheld when too much expected input is unknown.
11. Every estimated difficulty/relevance score carries estimate confidence/uncertainty separately from Stage 03 evidence confidence.
12. AI self-confidence is insufficient; production use requires benchmarked estimate quality.
13. Corpus maintains separate **Generic B1 Relevance (`GB1`)** and **TELC B1 Relevance (`TELC`)** scores.
14. GB1 uses B1 fit, skill/task centrality, cross-provider recurrence, and transfer value.
15. TELC relevance uses target format alignment, direct TELC support, TELC recurrence, scoring/section exposure, and currentness.
16. Provider/source weighting is applied during evidence aggregation through independence, Stage 03 confidence, target alignment, currentness, and scope fit rather than one opaque provider-reputation score.
17. Initial target-alignment priors favor direct TELC B1 evidence while still allowing cross-provider and B+ third-party evidence to contribute.
18. Production difficulty calibration uses **A/B evidence only**; C/D/Quarantine cannot calibrate production difficulty.
19. For decision-grade relevance analytics, C evidence is capped at **15% effective evidence mass**, cannot be the sole basis for a result, and cannot alone raise a relevance band/learner priority.
20. For high-confidence TELC-specific conclusions with official TELC evidence available, third-party/unofficial evidence should normally contribute no more than **35% of effective support**; sparse-target cases remain provisional rather than being suppressed entirely.
21. Recurrence/prevalence claims remain duplicate-neutral and normally require at least two independent A/B materials, while one verified official TELC source can establish target-format existence.
22. Initial model-derived difficulty and future empirical difficulty are stored separately and combined conservatively only when qualified learner evidence exists.
23. Global learner-performance calibration must be ability-aware, condition-aware, first-attempt/exposure-aware, and version-aware; raw percent-correct is insufficient.
24. In the personal/single-learner phase, performance personalizes the App but does **not** globally recalibrate Corpus difficulty.
25. Performance on original App exercises calibrates those exercises and shared task/pattern models, not reference source items the learner never attempted.
26. Productive empirical difficulty uses B1-sufficient rubric attainment and condition/evaluator quality rather than binary correctness.
27. Empirical evidence gradually overrides cold-start estimates through conservative shrinkage; a provisional `n_eff/(n_eff+50)` blending concept is the starting calibration prior, not a locked implementation constant.
28. Difficulty and relevance enrichment should be offline/batched/cached and requires no per-session AI calls.

---

## 9. Open Questions / Deferred Decisions

### 9.1 Owner questions

**None.** The established product goals are sufficient to choose conservative starting difficulty/relevance models without an owner preference blocking Stage 07.

### 9.2 Deliberately deferred calibration/product-detail decisions

The following are intentionally deferred because they require benchmark or real-user evidence:

- final component weights inside L/R/T/A/P;
- final section composite weights;
- final uncertainty envelopes and benchmark error tolerances;
- exact effective-evidence thresholds for “high-confidence prevalence” beyond the inherited two-source minimum;
- empirical learner sample-size requirements for specific task families;
- whether later calibrated difficulty should expose a probability-like interpretation in addition to the rubric score;
- exact relationship between empirically calibrated task difficulty and App readiness weights.

Stages 10, 11, 14, and 16 plus future learner data should recalibrate these without changing the conceptual separation defined here.

### 9.3 Architecture/implementation decisions intentionally not made

Database fields, feature extraction libraries, NLP/readability formulas, ASR/acoustic analysis stack, statistical item-response implementation, embedding/model provider, batch orchestration, cache keys, privacy aggregation mechanism, API representation, and UI are intentionally open.

---

## 10. Definition of Done Check

| Stage 07 checklist requirement | Decision captured | Where |
|---|---|---|
| Define linguistic difficulty | **Yes** | 4.3 |
| Define task/reasoning difficulty | **Yes** | 4.4 |
| Define time-pressure difficulty | **Yes** | 4.5 |
| Define audio difficulty | **Yes** | 4.6 |
| Define production difficulty for writing/speaking | **Yes** | 4.7 |
| Separate CEFR from numerical difficulty | **Yes** | 3.3, 4.8 |
| Define TELC relevance separately from generic B1 relevance | **Yes** | 3.4, 4.10–4.11 |
| Define provider/source weighting principles | **Yes** | 4.12 |
| Limit low-confidence material in aggregate insights | **Yes** | 4.13–4.15 |
| Represent uncertainty in AI-estimated difficulty | **Yes** | 4.9 |
| Plan learner-performance recalibration | **Yes** | 4.16 |
| Preserve Stage 03 confidence gates | **Yes** | 2.3, 4.12–4.14 |
| Preserve rights independence | **Yes** | 1.2, 2.4 |
| Define cost-sensitive defaults | **Yes** | Section 7 |
| Owner blocker remains | **No** | 9.1 |

**Stage 07 product-shaping status: complete.** The Corpus can now distinguish CEFR from multidimensional actual difficulty, keep broad B1 relevance separate from TELC B1 relevance, bound weak/unofficial evidence, represent estimate uncertainty, and evolve toward empirical calibration without confusing global task difficulty with one learner’s experience.