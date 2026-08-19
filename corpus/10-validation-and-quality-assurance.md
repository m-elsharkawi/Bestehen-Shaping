# Bestehen / Corpus — Stage 10: Validation and Quality Assurance

> **Status:** Authoritative Stage 10 product-shaping decision  
> **Product:** Bestehen / Corpus  
> **Initial domain:** German A2–B1 exam and exam-style material  
> **Primary downstream customer:** Bestehen / App  
> **Core principle:** Corpus data is production-ready only for the uses whose structural integrity, extraction quality, trust, rights, and evidence-independence gates it actually passes; uncertainty must remain local rather than being hidden by a single “valid” flag.

## 1. Purpose and Scope

Stage 10 defines how Bestehen / Corpus determines whether extracted and enriched material is **structurally faithful, internally coherent, sufficiently complete, and accurate enough for a specific downstream use**. It expands the pipeline-level `Validate` responsibility from Stage 08 into a measurable QA system with explicit rules, error classes, quality gates, manual sampling, benchmark expectations, and regression requirements.

The stage must protect Bestehen / App from the most damaging Corpus failures:

- teaching or scoring against the wrong answer;
- treating malformed extraction as real exam structure;
- losing or mislinking a required image, table, audio track, transcript, or scoring component;
- allowing OCR/ASR/model artifacts to masquerade as source truth;
- publishing precise semantic metadata whose extraction method is not accurate enough for that use;
- allowing duplicate or unresolved-dependent material to inflate evidence;
- allowing trusted provenance to hide a local extraction defect;
- allowing a technically clean extraction to hide weak authenticity, unresolved rights, or quarantine state.

This is **product shaping, not implementation architecture**. It defines the observable quality contract and release behavior. It does not choose a test framework, parser library, OCR/ASR/model vendor, database constraint mechanism, dashboard stack, sampling implementation, or CI system.

### 1.1 Stage objective

**Corpus should be able to explain exactly why a field, item, task, document, or derived signal is safe for a stated production use, what was checked, what remains uncertain, and what happens when a later parser/model change makes quality better or worse.**

### 1.2 Product invariants

1. **Validation is use-specific.** “Valid for topic analysis” does not imply “valid to score a learner.”
2. **Source truth and extraction truth are separate.** A source can contain a typo; OCR can introduce a different typo; QA must distinguish them.
3. **Trust does not repair extraction.** Tier A provenance does not make corrupted text or a wrong audio link production-ready.
4. **Extraction quality does not upgrade trust.** A perfectly parsed Tier C mock remains Tier C evidence.
5. **Rights are an independent gate.** QA cannot turn reference-only content into reusable content.
6. **The smallest affected scope is held.** One bad item should not discard an intact exam unless the defect implies broader corruption.
7. **Correctness-critical mistakes receive the strictest gates.** A wrong answer or scoring relationship is more harmful than an omitted low-risk topic tag.
8. **Model self-confidence is never sufficient evidence of quality.** Auto-publication depends on benchmark performance, input quality, deterministic checks, and independent validation where appropriate.
9. **No silent repair of source material.** Corrections or inferred reconstructions are explicit derived assertions with provenance.
10. **Benchmark thresholds are initial policy, not fake precision.** They are recalibrated as the gold dataset and real failure history grow.
11. **Regression is a product failure even when a new model is newer or cheaper.** Changes must prove they preserve required quality.
12. **Personal-project economics matter.** Cheap deterministic checks run broadly; expensive models and manual review concentrate on high-impact ambiguity.

---

## 2. Inputs / Existing Decisions

Stage 10 preserves the shared Product Overview, Identity, both shaping checklists, and Corpus Stages 01–09.

### 2.1 Stage 01 — mission and useful-corpus standard

`corpus/01-product-mission-and-boundaries.md` established that a useful corpus is measured by structural quality, trust, deduplication integrity, analytical usefulness, downstream usefulness, and maintainability rather than raw file count. Stage 10 turns structural quality into measurable gates.

### 2.2 Stage 02 — provenance and imperfect inputs

`corpus/02-source-strategy.md` established support for HTML, PDF, DOC/DOCX, scans/images, audio, video, and archives; automated and manual intake; dead/moved sources; mirrors; and permanent provenance. QA therefore must cover multiple modalities and must not assume every accepted source is a clean official PDF.

### 2.3 Stage 03 — authenticity and confidence

`corpus/03-trust-authenticity-confidence.md` established A/B/C/D evidence-confidence tiers, local confidence, disputed/quarantine states, and use-specific confidence gates. B+ is the normal minimum for correctness-sensitive production use, difficulty influence, App learning priorities, generation grounding, and direct learner exposure, with stricter answer-consistency requirements where a specific answer is treated as correct.

**Stage 10 does not create a second trust score.** It measures whether the extraction/derivation is faithful enough to use the Stage 03 evidence responsibly.

### 2.4 Stage 04 — rights

`corpus/04-rights-and-usage-metadata.md` established `REUSABLE`, `REUSABLE_WITH_CONDITIONS`, `REFERENCE_ONLY`, `UNKNOWN_REVIEW_REQUIRED`, and `PROHIBITED` operational states. Validation may check that required rights metadata exists and that publication respects the current rights gate, but it cannot infer permission from linguistic or structural quality.

### 2.5 Stage 05 — canonical exam model

`corpus/05-canonical-exam-model.md` defined Source Observation → Document → Exam/Test Set → Section → optional Part → Task → Item, plus separately addressable Instructions, Stimuli, Response Options, Answers, Explanations, Scoring Rules, and Assets. It also distinguished **source incompleteness**, **extraction incompleteness**, and **linking incompleteness**. Stage 10 validates those distinctions rather than collapsing them into one completeness percentage.

### 2.6 Stage 06 — taxonomy

`corpus/06-exam-and-skill-taxonomy.md` requires assignment-level role, confidence, origin, version, and review state. It set an initial benchmark posture of about **95% measured precision or better** before high-impact taxonomy mappings can auto-publish, with broader/provisional tags preferred when fine-grained precision is insufficient.

### 2.7 Stage 07 — difficulty and relevance

`corpus/07-difficulty-and-relevance-models.md` requires separate L/R/T/A/P difficulty profiles, Generic-B1/TELC relevance, estimate confidence, unknown/N/A handling, and versioned methods. Stage 10 validates prerequisite inputs and benchmark behavior; it does not collapse uncertainty by forcing every dimension to a number.

### 2.8 Stage 08 — ingestion and extraction lifecycle

`corpus/08-ingestion-and-extraction-pipeline.md` established the conceptual lifecycle **Discover → Fetch → Normalize → Parse → Segment → Classify → Extract Answers → Extract Assets → Enrich → Validate → Deduplicate → Review → Publish**. It requires partial publication, local holds, exception-based human review, traceable model derivations, and conservative auto-accept.

Stage 08 also set a starting target of roughly **99% precision for correctness-critical machine-linked answer/key/scoring outputs**, subject to Stage 10/16 benchmark evidence. Stage 10 formalizes that requirement and the surrounding release criteria.

### 2.9 Stage 09 — deduplication and independence

`corpus/09-deduplication-strategy.md` requires non-destructive duplicate relationships, conservative automatic collapse, observation/content/independence separation, and benchmark validation of duplicate thresholds. QA must therefore verify that production analytics never bypass unresolved or incorrect independence treatment.

No earlier shaping decision is replaced by Stage 10.

---

## 3. Decisions and Rationale

### 3.1 Validation is layered, not one pass/fail flag

**Decision:** A unit is evaluated through five independent layers:

1. **representation integrity** — was source content/assets recovered faithfully enough;
2. **structural consistency** — do canonical entities and relationships form a coherent exam/task model;
3. **semantic/correctness quality** — are answers, language, taxonomy, and derived signals accurate enough for their intended use;
4. **governance completeness** — are provenance, confidence, rights, derivation, review, and independence states present and compatible with publication;
5. **use-specific production gate** — does the resulting unit meet every prerequisite for the concrete downstream use.

A failure in one layer blocks only the uses that depend on it, unless the defect demonstrates broader corruption.

### 3.2 Production readiness is capability-scoped

**Decision:** Corpus does **not** define one global `production_ready=true` that implies universal fitness. The Stage 08 publication classes remain authoritative, while Stage 10 defines a **production-readiness profile** for the intended capability.

Examples:

- a reading Task can be production-ready for structural/task-frequency analytics while its detached answer key keeps it unready for learner scoring or distractor analysis;
- a Listening Task can be ready for topic/skill analysis from a reliable source transcript while audio difficulty remains unready because the recording is missing;
- a reference-only source can be production-ready for non-reconstructive aggregate intelligence while remaining ineligible for direct App exposure;
- an Item with unresolved duplicate dependency can be internally searchable but not counted as independent evidence in production frequency analytics.

This keeps quality honest and prevents one missing field from either blocking all value or being ignored entirely.

### 3.3 Error severity is based on potential downstream harm

**Decision:** Validation findings use four severity classes.

| Severity | Product meaning | Examples | Default action |
|---|---|---|---|
| **Q0 — Critical / blocker** | Could make the App teach/score incorrectly, violate a hard governance gate, or materially corrupt decision-grade analytics | wrong answer linked as authoritative; quarantined/prohibited content published; independent-mirror inflation; wrong exam/version key attached; required listening track mapped to the wrong task; structural corruption changes what is scored | Hold the affected use immediately; reprocess/review before production publication |
| **Q1 — Major** | Materially changes task meaning, structure, semantic interpretation, difficulty, or App prioritization but is unlikely to create an immediate governance violation | missing required Item; OCR drops negation/date/price; wrong primary skill; broken critical image; task/item boundary error; substantial transcript/alignment error | Hold affected field/unit/use; targeted correction/review; may allow unaffected uses |
| **Q2 — Minor** | Reduces completeness or precision but does not materially change the answer, tested proposition, core task shape, or high-level analytics | optional metadata omitted; non-critical punctuation/layout loss; overly broad but not wrong semantic tag; missing decorative asset | Publish only if the relevant capability gate still passes; queue correction opportunistically |
| **Q3 — Advisory / observation** | Unusual, low-confidence, or potentially improvable condition that does not currently violate a production gate | uncommon provider label; low-value optional enrichment absent; style anomaly in source material | Record for monitoring; no automatic hold |

Severity is assigned to the **finding**, not permanently to the source. One document can contain a Q0 disputed answer and many unaffected production-ready tasks.

### 3.4 Validation prioritizes precision where false acceptance is harmful

For correctness, identity, rights enforcement, provenance, and automatic duplicate collapse, a false acceptance can directly contaminate downstream behavior. Auto-publication therefore prioritizes **precision** over maximum recall. Missing a usable answer link is less harmful than confidently teaching the wrong answer.

For low-risk broad metadata, recall can be more permissive when uncertain outputs remain provisional or are backed off to a broader parent category.

### 3.5 No single scalar “Corpus quality score”

**Decision:** Corpus quality is represented as a **quality vector and release gates**, not one blended percentage. A scalar can hide a catastrophic answer-key defect behind excellent metadata completeness.

The primary dimensions are:

- structural accuracy;
- extraction fidelity;
- correctness/key accuracy;
- semantic/taxonomy accuracy;
- asset and audio-link integrity;
- required-metadata completeness;
- duplicate/independence accuracy;
- benchmark/regression health;
- manual-sample defect rates;
- coverage of the representative benchmark slices.

Operators may later summarize these dimensions visually, but no weighted composite may override a failed hard gate.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Exam-structure validation

**Decision:** Structure validation combines deterministic invariants, source-to-canonical consistency checks, completeness declarations, and selective semantic review.

### 4.1.1 Required structural checks

Where applicable, validate:

- every published child has a valid parent or an explicitly detached/unresolved state;
- order and numbering are coherent with the source evidence, while allowing legitimate provider-native gaps;
- Section/Part/Task/Item boundaries do not overlap impossibly or duplicate the same source region accidentally;
- an Item is the smallest response/scoring-addressable unit consistent with Stage 05;
- shared Stimuli are linked once and reused rather than copied as independent evidence;
- Response Options match the Item response mechanic and cardinality;
- multiple-correct, matching, cloze, productive, and composite Items have internally consistent response/scoring representation;
- Instructions and tested content are not accidentally collapsed where that would distort tested-language analytics;
- declared source completeness matches the represented structure;
- source incompleteness, extraction incompleteness, and linking incompleteness remain distinct;
- provider-native labels/order are preserved even when normalized Section/Task taxonomy differs;
- scoring rules, item counts, and totals are internally coherent when the source provides enough evidence to check them;
- no suppressed/quarantined child silently contributes to an active parent aggregate.

### 4.1.2 Structural anomalies

The following normally produce Q0/Q1 findings depending on impact:

- one Item linked to the wrong Stimulus or Task;
- omitted/duplicated answerable units;
- wrong response cardinality;
- a full exam inferred from a fragment;
- an answer-key page segmented as tested content;
- two exam editions accidentally combined;
- a table/form flattened so relationships required to solve the task are lost;
- incorrect Section/Task boundary that changes provider-format analytics.

Harmless differences such as page breaks, decorative headings, or missing printed numbers do not fail validation when the semantic structure is otherwise clear.

### 4.1.3 Structural publication rule

A structure is production-ready for decision-grade structural analytics only when:

- all relevant Q0/Q1 structural findings are resolved or explicitly scoped out;
- required relationships are verified or conservatively left detached;
- completeness state is honest;
- the extraction/segmentation method is benchmark-qualified for the relevant format/provider slice, or the unit is manually reviewed.

---

## 4.2 Answer-key and scoring validation

**Decision:** Correctness validation treats every answer or scoring claim as evidence-backed and local. No model may silently promote an inferred answer into a source answer.

### 4.2.1 Required checks for objective items

Where applicable, validate:

- the answer assertion points to the correct exam edition, Section/Task, Item, and option/slot;
- response cardinality matches the Item definition;
- the key uses only valid response options/labels;
- item numbering/counts agree between question material and key;
- detached keys are not linked from filename similarity alone;
- source-provided errata/superseding versions are respected;
- competing plausible keys become a local `disputed` state instead of majority-vote truth;
- where semantic validation is feasible, the keyed answer is consistent with the Stimulus, prompt, negation/restrictions, and scoring rule;
- OCR/ASR uncertainty on answer-critical tokens is below the allowed gate or triggers review.

### 4.2.2 Productive tasks

Writing and Speaking must not be forced into fake single-answer validation. QA instead verifies that source rubrics, content points, sample responses, scoring descriptors, preparation/time constraints, and task requirements are linked to the correct productive Task/Item and preserve their source status.

### 4.2.3 Correctness-ready gate

An objective answer may be treated as production correctness ground truth only when:

1. the local Stage 03 confidence/use gate passes;
2. the answer relationship is explicit/deterministically verifiable **or** produced by a benchmark-qualified correctness-critical method;
3. no unresolved competing key/scoring assertion exists;
4. structural and source-version checks pass;
5. answer-critical extraction quality passes;
6. the relevant method meets the Stage 08 starting **~99% precision** threshold on the applicable gold slice, subject to later recalibration;
7. any rights requirement for the downstream action independently passes.

If these conditions fail, the answer can remain visible as source evidence/candidate material without being used as authoritative correctness truth.

---

## 4.3 Language-quality validation

**Decision:** Language QA distinguishes **source-language quality** from **extraction-language fidelity**.

### 4.3.1 Source-language checks

For tested German, validate or estimate:

- language is predominantly the expected German variety for the task, allowing multilingual instructions/supporting material where source-appropriate;
- wording is coherent enough to function as an exam item;
- spelling/grammar/register are plausible for the claimed A2/B1 exam context;
- instructions are interpretable and response expectations are clear;
- distractors/options are linguistically well-formed enough to be meaningful;
- claimed provider/level language does not contain systematic anomalies that should lower Stage 03 confidence or trigger review.

A source can genuinely contain an error. Corpus preserves it as source evidence and records a source-quality finding rather than silently “fixing” the original.

### 4.3.2 Extraction-fidelity checks

Validate that parsing/OCR/ASR did not introduce meaning-changing corruption, especially:

- negation and polarity;
- numbers, dates, times, prices, percentages, units;
- umlauts, `ß`, word boundaries, and diacritics where they distinguish content;
- modal verbs/particles and restrictions;
- question marks, blank positions, option labels, and line/table relationships;
- proper nouns/entities when they determine an answer;
- audio corrections or superseded information.

### 4.3.3 Language-quality consequences

- A source-level linguistic defect affects evidence confidence and language suitability; it is not an extraction bug.
- An extraction defect blocks only fields/uses that depend on the corrupted region, unless corruption is widespread.
- Automated grammar/spell tools may flag anomalies but must not automatically rewrite source content.
- Fine-grained language enrichment backs off to unknown/broader metadata when input fidelity is inadequate.

---

## 4.4 Metadata-completeness validation

**Decision:** Completeness is evaluated against the **entity type and intended capability**, not by demanding every possible field on every record.

### 4.4.1 Base governance metadata required for production publication

Every production-active unit/derived output must be traceable to enough information to establish:

- source observation/material identity and provenance lineage;
- canonical entity identity and scope;
- current completeness state;
- extraction/derivation origin, method/rule/model version, and processing version where applicable;
- local evidence confidence/review state or a valid inherited Stage 03 state;
- rights status/evidence scope relevant to the action;
- current/superseded status;
- duplicate/derivative/independence treatment where the metric can be distorted by copying;
- taxonomy version for taxonomy assignments;
- estimate/rubric version and uncertainty for difficulty/relevance signals;
- unresolved dependencies/findings that constrain use.

### 4.4.2 Capability-specific required metadata

Examples:

- correctness use requires a validated Answer/Scoring relationship;
- Listening difficulty requires actual audio and sufficient acoustic evidence; a transcript alone is insufficient;
- learner-priority analytics require confidence/relevance/independence context;
- source-content exposure requires rights/action permission plus local confidence and integrity;
- high-impact taxonomy use requires assignment role, origin, version, and benchmark-qualified confidence.

### 4.4.3 Completeness metric rule

Required-field completeness for a claimed production capability must be **100%**: if a required gate field is missing, the capability is not ready. Optional enrichment coverage is measured separately and may be incomplete without making the base entity invalid.

This prevents a misleading overall “92% complete” score from hiding the fact that the missing 8% contains the one field required to use the record safely.

---

## 4.5 Asset-integrity and broken-asset validation

**Decision:** Assets are validated for existence, integrity, role, and linkage—not merely URL reachability.

Where applicable, validate:

- referenced retained asset payload exists or the unavailable state is explicit;
- payload can be decoded/opened as the expected modality;
- type, dimensions/duration/basic media properties are plausible;
- source fingerprint/version matches the asset relationship used by the Task/Stimulus;
- the asset is not an error page, placeholder, zero-byte/corrupt file, or unrelated download;
- the relationship to Document/Stimulus/Task/Item is explicit or has sufficient linkage evidence;
- required images/tables/forms preserve enough layout to perform the task;
- source-required audio/video is present for capabilities that claim exam-realistic media behavior;
- rights/local confidence overrides for the asset are available when they differ from the parent;
- derived OCR crops/transcripts/audio tracks remain traceable to the source asset.

### Critical versus non-critical assets

A missing asset is Q0/Q1 when the candidate cannot interpret, solve, or score the task without it. Decorative images, optional thumbnails, or redundant representations may be Q2/Q3.

**Rule:** Broken optional media must not block valid textual analytics; missing tested media must not be ignored merely because the surrounding text parsed successfully.

---

## 4.6 Audio-question alignment validation

**Decision:** Listening alignment uses the **coarsest defensible mapping**, with stricter validation as alignment gets closer to answer-bearing item segments.

### 4.6.1 Required checks

Where applicable, validate:

- the audio belongs to the correct provider/exam edition/Section/Task;
- track order and Task/Item ranges agree with source evidence;
- declared/derived segment boundaries are within the correct asset and do not overlap impossibly;
- transcript origin is explicit (`source_provided`, human-corrected, ASR-derived, partial, or absent);
- transcript/ASR timestamps and alignment method/version are traceable;
- item-level alignment is not invented when only Task-level evidence exists;
- answer-critical speech such as numbers, dates, times, prices, negation, restrictions, speaker corrections, and names/entities is accurately captured enough for the claimed use;
- re-recorded/shared-script relationships from Stage 09 do not create false independent content evidence;
- audio difficulty remains `unknown` when the actual recording is missing even if a transcript exists.

### 4.6.2 Alignment readiness levels

- **Task-ready:** the correct track/segment is defensibly linked to the Task/Stimulus.
- **Item-ready:** an Item-specific segment is defensibly linked and benchmark quality supports item-level use.
- **Answer-critical-ready:** the answer-bearing segment passes the stricter correctness-critical validation gate.

A coarser alignment may still be production-ready for task-level Listening analytics without qualifying for item-level answer diagnosis.

---

## 4.7 Error propagation and hold scope

Validation findings propagate only as far as required by dependency.

| Finding | Must block | May remain usable |
|---|---|---|
| Wrong objective answer link | correctness-dependent use for affected Item/Task | topic/structure/language evidence if otherwise valid |
| OCR corruption in one option | exact option/answer/distractor use | unaffected Tasks/Items and broad source metadata |
| Missing required image | direct simulation and semantics depending on image | unrelated textual Tasks |
| Missing audio | Listening realism/audio difficulty | transcript-based broad semantic evidence if clearly labeled |
| Uncertain duplicate dependency | independent-frequency/corroboration claim | inventory/search and conservative bounded analytics |
| Missing optional topic tag | topic-specific output | structural/correctness outputs |
| Source rights unknown | direct source-content reuse | allowed internal/non-reconstructive analysis under Stage 04 |
| Quarantine/takedown | normal active use of affected scope | only the audit/provenance behavior explicitly permitted by earlier stages |

**Rule:** validation should salvage correct evidence, but never by weakening a gate that protects the learner or decision-grade analytics.

---

## 4.8 Cross-checking strategy for AI/model extraction

**Decision:** Model-generated extraction/enrichment uses a **risk-based cross-check ladder**. Bestehen does not run two or three premium models over every item.

### Pass 0 — deterministic/source checks

Before a model result is trusted, apply available cheap evidence:

- source numbering and explicit cross-references;
- cardinality and option validity;
- page/region/track bounds;
- known provider/section structure;
- source-provided key/rubric relationships;
- language/media decoding checks;
- duplicate/version relationships;
- required metadata and governance gates.

A deterministic contradiction defeats model agreement.

### Pass 1 — primary extraction

Use the cheapest benchmark-qualified method for the relevant format/field. It may be deterministic, local/open-source, or a low-cost model. The output remains traceable to method/model/prompt/schema version.

### Pass 2 — independent verification when impact requires it

For correctness-critical or otherwise high-impact fields, an independent verifier should evaluate the **source evidence and proposed relation**, not merely echo the primary model's reasoning. The verifier should output an agreement/disagreement/result classification with its own derivation metadata.

Independence can come from:

- deterministic evidence plus a model;
- two materially different extraction prompts/tasks;
- two separately benchmarked methods;
- a model plus a human check;
- different model families when the cost is justified.

Using a second expensive model family is **not mandatory** when a source-explicit relation or deterministic validator is stronger evidence.

### Disagreement behavior

- Agreement never overrides a hard contradiction in source evidence.
- Disagreement on a low-risk field backs off to unknown/broader/provisional metadata.
- Disagreement on a high-impact field routes to manual review or one stronger adjudication step.
- Repeated model voting is not a substitute for evidence. Two models repeating the same mistaken OCR text do not make it source truth.
- There is no open-ended “ask more models until they agree” loop.

### Where full multi-pass extraction is required

Full independent dual-pass extraction is reserved for:

- gold-standard annotation/benchmark comparison;
- a new or materially changed extraction method before it earns auto-publication;
- correctness-critical answer/scoring relations lacking explicit deterministic linkage;
- difficult OCR/ASR regions containing answer-critical content;
- high-value TELC evidence whose ambiguity could materially change App priorities;
- regression investigation after a sampled Q0/Q1 escape.

For stable low-risk broad metadata, one benchmark-qualified pass plus deterministic validation and manual sampling is sufficient.

---

## 4.9 Manual QA sampling

**Decision:** Bestehen uses **risk-stratified sampling**, not uniform review and not 100% human approval of all production data.

### 4.9.1 Always-review population

Human review is required for the affected scope when:

- a correctness-critical output does not meet the benchmark-qualified auto-accept rule;
- plausible answer keys/scoring rules conflict;
- a high-impact source/version/audio relationship remains ambiguous;
- a Q0/Q1 validator finding cannot be resolved deterministically;
- a gold-standard record is being created or changed;
- a proposed automation would overwrite a curator correction;
- a sampled failure triggers escalation under the rules below.

### 4.9.2 Routine sample rates

These are starting operational product defaults and can be adjusted when evidence accumulates:

| Method/slice state | Manual sample of auto-published non-trivial outputs | Purpose |
|---|---:|---|
| **New or materially changed method/slice** | **10%**, minimum **25**, maximum **100** reviewed units for the affected release/batch | Discover systematic failure before broad trust |
| **Stable qualified slice** | **3%**, minimum **20**, maximum **50** reviewed units per meaningful release/batch | Detect drift/escapes cheaply |
| **Small batch below the minimum** | Review all units until the minimum evidence is accumulated across batches | Avoid declaring stability from tiny samples |
| **Gold/benchmark critical fields** | **100%** manual annotation/adjudication | Establish evaluation truth |

A “slice” should separate materially different risk groups such as native PDF versus scan/OCR, objective answers versus broad topics, Listening versus Reading, official versus imperfect unofficial material, and major provider/task families when behavior differs.

### 4.9.3 Oversampling rules

Sampling must deliberately over-represent:

- scanned/OCR-heavy pages;
- ASR-derived Listening material;
- detached answer keys and cross-document links;
- item-level audio alignment;
- high-TELC-relevance evidence;
- new providers/layouts/formats;
- C-tier-but-useful material near a production gate;
- derivative/duplicate clusters whose decision affects analytics;
- historically error-prone patterns.

### 4.9.4 Escalation from sample findings

- **Any Q0 escape:** immediately hold the affected method/slice for the impacted capability, inspect the failure class since the last known-good version, and re-evaluate release eligibility.
- **One Q1 escape:** add at least **25 targeted reviews** from the same slice/failure class.
- **A second materially similar Q1 in the expanded sample:** hold that method/slice for the affected capability until corrected or explicitly downgraded to provisional output.
- **Q2/Q3 findings:** trend and repair opportunistically unless they cluster into a systematic higher-impact failure.
- A slice that has passed **three consecutive releases/batches** without Q0/Q1 sampled escapes may use the stable 3% rate; a regression resets it to the new/changed 10% posture.

The exact notion of release/batch is an implementation detail. The product requirement is that sampling follows processing-method changes and meaningful ingestion cohorts rather than an arbitrary calendar alone.

---

## 4.10 Definition of production-ready Corpus data

**Decision:** “Production-ready” means **normal eligible use for a named capability**, not “present in the database” and not “fully enriched.”

Every production-ready capability must pass four gates.

### Gate A — integrity

- no unresolved Q0/Q1 finding relevant to the capability;
- required structural/content/asset relationships are verified or explicitly conservative;
- extraction fidelity is sufficient for the exact fields consumed.

### Gate B — method qualification

- deterministic rules are demonstrably appropriate, or the parser/model/method meets the benchmark threshold for that field/slice;
- required cross-checking has passed;
- any human correction remains authoritative unless explicitly superseded with review.

### Gate C — governance and evidence

- provenance and derivation are traceable;
- Stage 03 confidence/review gates pass for the intended use;
- Stage 04 rights gates pass when the action involves source expression or restricted processing;
- Stage 09 duplicate/independence treatment is resolved or conservatively bounded for analytics;
- quarantine/takedown/prohibition states are honored.

### Gate D — completeness for the capability

- every required metadata/input field for that capability is present;
- unknown versus N/A is represented correctly;
- unresolved dependencies are compatible with the capability rather than silently ignored.

### 4.10.1 Capability examples

| Capability | Additional readiness requirement |
|---|---|
| **Structural analytics** | validated hierarchy/relationships/completeness; no requirement for an answer key if the metric does not depend on correctness |
| **Semantic/topic/skill analytics** | input text/media fidelity sufficient; taxonomy method qualified for the granularity used; confidence/independence gates applied |
| **Correctness ground truth** | local B+ trust as applicable, validated answer/scoring relation, no dispute, correctness-critical benchmark gate |
| **Difficulty/relevance influence** | Stage 07 prerequisite inputs available, B+ influence gate, estimate method qualified, uncertainty retained |
| **App learning-priority input** | decision-grade analytics supported by independent A/B evidence according to Stage 03/07/09; no provisional-only evidence driving priority alone |
| **Exercise-generation grounding** | B+ local evidence, validated structure/semantics/correctness where required, no unresolved harmful conflict, rights/process route permitted |
| **Direct source-content use** | all relevant integrity/trust gates plus Stage 04 `REUSABLE` or satisfiable `REUSABLE_WITH_CONDITIONS`; product suitability remains an App decision |

`limited/provisional` Stage 08 publication is **not** production-ready for a decision-grade capability merely because an operator can inspect it.

---

## 4.11 Corpus quality metrics and starting targets

**Decision:** Quality is measured against the gold dataset and manual production samples, reported by **slice as well as overall**. Overall accuracy cannot hide a weak scan, Listening, unofficial, or provider-specific slice.

### 4.11.1 Core metrics

| Quality area | Primary metric | Starting production target / gate | Notes |
|---|---|---|---|
| **Structural extraction** | entity/relationship precision and recall | **≥98% precision, ≥97% recall** on required structural entities/relations for the qualified slice, plus no Q0 structural acceptance | Exact final target may vary by entity after Stage 16 evidence |
| **Correctness-critical answer/key/scoring linking** | precision first; recall tracked | **≥99% precision**, **≥97% recall**, and no unresolved known systematic wrong-answer class | Preserves Stage 08 conservative posture |
| **High-impact taxonomy mapping** | precision | **≥95% precision** for the relevant benchmark slice | Preserves Stage 06; broader tags may be used when leaf precision is insufficient |
| **Meaning-critical text/OCR/ASR fidelity** | exact correctness on annotated critical tokens/relations | **≥99%** on answer/meaning-critical annotations, with any Q0 token error blocking affected capability | General character accuracy is secondary to semantic fidelity |
| **Required metadata completeness** | required-field presence/validity | **100%** for every claimed production capability | Optional enrichment coverage is reported separately |
| **Critical asset linkage** | precision and broken/missing detection | **≥99% precision** on task-critical asset relationships; no known Q0 wrong-asset association | Recall remains important but unlinked is safer than wrongly linked |
| **Audio Task/Item alignment** | mapping precision | **≥99% precision** for auto-published item/answer-critical alignment; coarser Task-level alignment is used when item precision cannot qualify | Do not fake timestamp precision |
| **Automatic duplicate/evidence collapse** | precision first | **≥99% precision** on benchmarked auto-collapse decisions with no known Q0 independent-evidence collapse class | Recall is tracked; unresolved candidates remain conservative |
| **Q0 escape rate** | count/rate in gold + manual sample | **0 accepted Q0 escapes** in the evaluated release/slice | Any escape triggers hold/investigation |
| **Q1 sampled defect rate** | sampled Q1 findings | Track by slice; repeated Q1 invokes escalation rather than being averaged away | Initial emphasis is control limits, not a cosmetic corpus-wide target |

These are **starting qualification targets**, not eternal constants. Stage 16 may reveal that a particular field needs a stricter or differently defined metric. Lowering a correctness-critical threshold requires explicit product evidence, not convenience.

### 4.11.2 Secondary health metrics

Track without using them to override hard gates:

- percentage of production-active units covered by benchmark-qualified methods;
- optional metadata coverage by family;
- proportion of units held/provisional/review-required;
- Q0/Q1 findings by source type, provider, format, section, model/parser version, and extraction mode;
- manual-review yield and time spent per resolved high-impact defect;
- percentage of Listening material at Task-ready, Item-ready, and answer-critical-ready alignment levels;
- benchmark slice coverage gaps;
- regression pass/fail history by processing method;
- unresolved duplicate-dependency population that materially widens analytics ranges.

Raw corpus size remains a separate capacity/coverage metric and is never a substitute for these quality indicators.

---

## 4.12 Gold-standard benchmark dataset

**Decision:** Bestehen maintains one **versioned, manually adjudicated gold-standard QA dataset** that acts as the stable contract for extraction and validation quality. Stage 10 defines the benchmark; Stage 16 selects and instantiates the concrete source records.

### 4.12.1 Initial target size

The first useful gold set should target approximately:

- **12–20 source packages/documents/exam fragments**;
- **300–500 Items** across objective and productive task families;
- **40–60 Tasks** with manually verified canonical boundaries and shared Stimuli;
- **25–40 Listening Task/Item mappings** spanning clean and difficult alignment cases;
- at least **50 task-relevant Assets/asset relationships** including images/tables/forms/audio;
- deliberate duplicate/derivative families sufficient to test exact, reformatted, fragment, derivative, related-variant, and independent cases.

The target is intentionally hundreds, not tens of thousands. A small representative gold set that is carefully reviewed is more useful to a personal project than a huge weakly annotated benchmark.

### 4.12.2 Required representation

The gold set must include, as available in the Stage 16 seed corpus:

- TELC B1 as the strongest target signal;
- TELC A2–B1 and cross-provider Goethe/ÖSD/DTZ evidence;
- both A2 and B1;
- Reading, Language Elements where applicable, Listening, Writing, and Speaking;
- native-text PDF;
- scanned/image-heavy PDF or image input;
- HTML;
- DOC/DOCX or equivalent document-layout input when a representative source exists;
- audio and at least one awkward alignment/transcription case;
- at least one imperfect but useful unofficial source;
- an incomplete/fragmentary source;
- a detached answer-key or cross-document relationship;
- a duplicate/mirror/reformatted cluster;
- at least one derivative/near-duplicate case where over-collapse would be harmful;
- mixed-confidence and mixed-rights examples where QA must preserve governance rather than infer it.

Video may be added when it becomes a meaningful Corpus source, but it is not required to block the initial benchmark if the current seed corpus provides no representative video task.

### 4.12.3 Gold annotations

For each applicable unit, human annotation should capture:

- canonical Section/Part/Task/Item boundaries and containment;
- source regions/pages/tracks supporting the annotation;
- Instructions versus Stimuli/tested content;
- response mechanics/cardinality/options;
- answer/key/scoring assertions and their exact evidence/source version;
- source incompleteness versus extraction/linking incompleteness;
- task-critical Assets and expected relationships;
- audio Task/Item alignment at the defensible granularity;
- provider/exam family, CEFR scope, normalized Section, and task facets;
- high-impact taxonomy assignments needed to evaluate Stage 06 precision;
- meaning-critical text/audio tokens for OCR/ASR validation;
- duplicate/derivative/independence ground truth for selected families;
- expected Q0/Q1 validation findings for deliberately imperfect cases;
- benchmark-relevant confidence/rights expectations where later stages need to test enforcement.

Gold data records source truth and QA truth; it does not need to annotate every optional topic or linguistic feature simply because the taxonomy can express it.

### 4.12.4 Annotation/adjudication process

1. **Primary manual annotation** from the source evidence.
2. **Independent second review** for correctness-critical answers/scoring, critical asset/audio links, duplicate-collapse truth, and any case used as a hard release gate.
3. **Adjudication** of disagreements with a concise evidence note; do not hide disagreement by averaging labels.
4. **Freeze a benchmark version.** Corrections create a new benchmark version with history rather than silently rewriting old results.
5. Add real production incidents to a separate **incident/replay set**, and promote representative cases into future gold versions when they reveal a missing failure class.

### 4.12.5 Development versus holdout

To prevent tuning against the entire benchmark, the initial gold set should be split approximately:

- **70% development/visible benchmark** — used while improving extraction rules/prompts;
- **30% holdout** — used for qualification/regression decisions and not repeatedly hand-tuned against.

The split should preserve provider, format, section, scan/audio, and difficulty/error diversity rather than being random by individual Item when that would leak many Items from one document into both sides.

For very small slices where a 70/30 split would be meaningless, keep the whole slice visible but require manual sampling and explicitly record that holdout evidence is weak until Stage 16 grows it.

### 4.12.6 Relationship to Stage 16

Stage 10's checklist wording says “build a manually annotated gold-standard dataset.” At the **product-shaping** level, this stage completes that requirement by defining the benchmark contract, annotation truth, qualification metrics, target size, composition, and review rules. **Stage 16 is responsible for selecting the concrete source seed set and carrying out the initial annotations during benchmark-corpus establishment.** This is a planned sequencing decision, not an unresolved product question.

---

## 4.13 Regression expectations

**Decision:** Any change that can alter published Corpus meaning must prove itself against the frozen gold benchmark and known incident cases before replacing the last-known-good production output.

### 4.13.1 Changes that require regression evaluation

At minimum:

- parser/layout/segmentation changes;
- OCR or ASR method/model/version changes;
- answer-key/scoring linker changes;
- audio-alignment changes;
- semantic classifier/model/prompt/schema changes;
- taxonomy mapping/rule/version changes;
- difficulty/relevance extraction logic changes where prerequisite QA is affected;
- duplicate normalization/fingerprint/threshold changes;
- validation rules or production-gate changes;
- source-version normalization that can merge/split records;
- model/provider replacement for cost reasons.

### 4.13.2 Candidate-versus-baseline comparison

For the same benchmark inputs, compare:

- core precision/recall metrics by relevant slice;
- Q0/Q1 error counts and categories;
- field/entity-level differences from the current production baseline;
- new unknown/provisional outputs versus newly resolved outputs;
- human-curated corrections/overrides that must remain preserved;
- duplicate-cluster splits/merges and resulting independence effects;
- downstream capability eligibility changes.

### 4.13.3 Release gates

A changed method cannot replace the last-known-good method for a capability when:

- it introduces any new accepted **Q0** benchmark failure;
- correctness-critical/high-impact precision falls below the applicable threshold;
- a critical slice regresses materially while an overall average improves;
- required metadata completeness falls below 100%;
- it silently overwrites a human correction or removes traceability;
- it increases false-independent or false-collapse behavior enough to change decision-grade analytics without review;
- it changes rights/quarantine enforcement in a more permissive direction without explicit policy evidence.

For non-critical metrics, a small local regression may be accepted only when the overall product trade-off is documented, the hard gates still pass, the affected slice is understood, and the expected benefit is material (for example much better scan recall without a meaningful loss in safe precision).

### 4.13.4 No “newer model wins” rule

A cheaper/newer model may be retained as a candidate or used for lower-risk fields without replacing the existing method for high-risk fields. The last-known-good derived data remains valid until a replacement passes the same capability gate.

### 4.13.5 Benchmark evolution

- Gold annotations are versioned and immutable within a benchmark release.
- Corrections create a new benchmark version with rationale.
- New production incidents are added to the replay set immediately and to future gold versions selectively.
- Reports identify the benchmark version and method version together.
- When the benchmark composition expands, old-version metrics remain available so apparent improvements caused only by dataset changes are visible.

---

## 5. Edge Cases / Failure or Uncertainty Handling

### 5.1 Official source with a suspected typo or wrong answer

Official provenance does not suppress QA. Preserve the source assertion, mark the local conflict, seek errata/independent evidence where useful, and block authoritative correctness use until resolved. The rest of the source may remain production-ready.

### 5.2 Unofficial mock with excellent extraction

High extraction quality can make the data structurally usable but does not upgrade Stage 03 authenticity/evidence confidence. Downstream influence remains capped by trust/relevance rules.

### 5.3 Clean transcript but missing recording

The transcript can support bounded semantic analysis if its provenance/confidence allows it. Audio difficulty, acoustic realism, and exam-realistic Listening simulation remain unavailable.

### 5.4 OCR “correction” that changes the source

Keep the OCR output as a derived representation, retain the visual source region, and mark any curator/model correction separately. Never overwrite what the source visibly contains.

### 5.5 Partial exam with honest boundaries

A partial exam can pass QA for the intact represented Tasks when completeness is explicit. It fails any capability that claims full-exam structure, total scoring, or section balance not actually observed.

### 5.6 Multiple mirrors agree on the same wrong key

Mirror count is not independent corroboration. Stage 09 independence is applied before confidence or validation can treat agreement as supporting evidence.

### 5.7 Model outputs are internally consistent but systematically wrong

Deterministic consistency is necessary but not sufficient. Benchmark slices and manual production samples detect systematic semantic failure; the method loses auto-publication eligibility even if its emitted structure is syntactically perfect.

### 5.8 Gold truth itself is uncertain

If two careful reviewers cannot resolve source truth, the benchmark label is `disputed`/excluded from the corresponding exact metric rather than forcing a false gold answer. The case remains valuable as a review-routing benchmark.

### 5.9 A parser improves recall by making more guesses

More populated fields do not automatically mean higher quality. If precision or Q0/Q1 safety falls below the capability threshold, the added guesses remain provisional or are rejected even if coverage rises.

### 5.10 A stable method encounters a genuinely new source layout

Existing qualification does not automatically transfer. The new layout/source-format slice begins under the new/changed sampling posture until enough evidence demonstrates that the method generalizes safely.

---

## 6. Relationship to Other Bestehen Stages

- **Stage 03:** remains authoritative for authenticity/evidence confidence; QA never replaces the A/B/C/D model.
- **Stage 04:** remains authoritative for rights; QA only ensures the gate is present and honored.
- **Stage 05:** supplies the entities and relationships structure validation checks.
- **Stage 06:** supplies taxonomy semantics and the ~95% high-impact precision posture.
- **Stage 07:** supplies difficulty/relevance semantics and estimate uncertainty.
- **Stage 08:** supplies lifecycle, review, derivation traceability, and publication states; Stage 10 defines the measurable validation contract inside that lifecycle.
- **Stage 09:** supplies duplicate/independence semantics that must pass before decision-grade analytics.
- **Stage 11:** must consume only capability-eligible evidence and must expose quality/independence limitations where material.
- **Stage 12:** must expose enough quality/restriction metadata for App to know what Corpus output is safe to consume.
- **Stage 13:** should surface QA findings, review backlog, benchmark health, and regression failures operationally.
- **Stage 14:** will set concrete cost/scale budgets around the QA policy.
- **Stage 16:** will instantiate the representative benchmark corpus and manually annotate concrete gold records according to the contract defined here.
- **Stage 17:** should incorporate this QA contract into the final Corpus PRD.

### Cross-stage rule for later agents

**Decision-grade Corpus analytics and App-facing signals must never consume “published” as a blanket quality flag. They consume an output only when the output is production-ready for that specific capability and the independent Stage 03/04/09 gates also pass.**

This is the most important Stage 10 contract to preserve downstream.

---

## 7. Cost Notes

Validation has meaningful processing cost, but the chosen model deliberately avoids expensive recurring QA on every item.

### 7.1 Preferred low-cost default

1. **Run deterministic checks broadly.** Cardinality, references, counts, media decoding, hashes/fingerprints, required metadata, version relationships, and structural invariants are cheap and repeatable.
2. **Use local/open-source processing when benchmark-qualified.** OCR, ASR, language checks, and broad semantic classification do not require premium APIs by default.
3. **Batch semantic QA offline.** Corpus intelligence is precomputed; Bestehen / App should not trigger QA/model calls per learner session.
4. **Cross-check only high-impact outputs.** Low-risk metadata uses one qualified pass plus sampling; correctness-critical fields get independent validation.
5. **Reprocess only affected dependencies.** A taxonomy-model change does not rerun OCR; an ASR improvement does not redownload stable PDFs.
6. **Keep last-known-good outputs.** A new cheaper model does not force a risky migration.
7. **Allow low-value ambiguity to remain unresolved.** C/D duplicate/noisy material can stay limited rather than consuming money or owner time.

### 7.2 When manual review is cheaper than repeated premium-model calls

For a personal project, one owner review is usually the better default when:

- the source page/key/audio is directly inspectable;
- the ambiguity concerns one or a few high-impact Items;
- two cheap passes disagree;
- the question is provenance/version linkage rather than broad-language interpretation;
- the alternative would be several premium model calls whose agreement still would not establish source truth.

Manual review has a time cost, so it should still be impact-prioritized. But paying three models to vote on a visible answer-key mismatch is both more expensive and less defensible than inspecting the source once.

### 7.3 When a premium capability is justified

A stronger paid model/service is justified selectively for:

- answer-critical OCR/ASR that cheaper processing cannot recover reliably;
- benchmark adjudication where the owner cannot confidently evaluate the German/audio/layout issue;
- a high-value TELC source whose extraction ambiguity materially affects target intelligence;
- batched difficult semantic cases where manual review would take substantially more owner time than one strong pass;
- regression diagnosis when a new method creates a systematic but hard-to-localize failure.

Even then, the result remains evidence to validate, not an automatic truth source.

### 7.4 Upgrade trigger

Increase recurring QA spend only when one of these becomes true:

- manual review becomes the dominant ingestion bottleneck;
- a cheaper method repeatedly misses a high-impact failure class;
- benchmark evidence shows a stronger model materially reduces Q0/Q1 defects;
- Corpus volume grows enough that a paid batch method costs less than equivalent owner review time;
- the App begins relying on a new high-risk signal that genuinely requires better extraction fidelity.

Stage 14 will convert these principles into processing-volume and per-1,000-item budget targets.

---

## 8. Decisions Made

1. Validation is layered and **use-specific**, not a single valid/invalid flag.
2. Production readiness is expressed per capability while preserving Stage 08 publication states.
3. QA findings use Q0 Critical, Q1 Major, Q2 Minor, and Q3 Advisory severity based on downstream harm.
4. Structure validation checks canonical hierarchy, response/scoring semantics, shared stimuli, completeness honesty, and provider-native consistency.
5. Answer validation keeps source answers, inferred answers, disputes, editions, and scoring evidence separate; correctness-critical auto-use keeps the ~99% precision posture.
6. Language QA separates source-language defects from extraction/OCR/ASR defects and protects meaning-critical tokens.
7. Required metadata completeness is 100% for the capability being claimed; optional enrichment is measured separately.
8. Asset QA validates payload integrity, semantic role, task criticality, rights/confidence scope, and relationships.
9. Listening alignment uses Task-ready, Item-ready, and answer-critical-ready levels and never invents fine timestamps from coarse evidence.
10. AI/model extraction uses deterministic checks first, a cheap qualified primary pass, and independent verification only where impact warrants it.
11. Manual QA uses risk-stratified sampling: 10% for new/changed slices, 3% for stable qualified slices, with minimum/maximum review bounds and explicit escalation rules.
12. Corpus quality is a vector of metrics rather than one scalar score.
13. Starting qualification targets include ≥98/97 structural precision/recall, ≥99% correctness-link precision, ≥95% high-impact taxonomy precision, 100% required metadata completeness, and zero accepted Q0 escapes.
14. The gold-standard QA contract targets roughly 12–20 source packages, 300–500 Items, representative modalities/providers/error cases, manual adjudication, and an approximately 70/30 development/holdout split.
15. Every materially meaning-changing parser/model/rule change must pass benchmark and incident regression before replacing the last-known-good production output.
16. Manual inspection is preferred over repeated premium-model voting when the ambiguity is narrow and source evidence is directly inspectable.

---

## 9. Open Questions / Deferred Decisions

### 9.1 Owner questions

**None.** No owner preference or risk-tolerance decision is required to complete Stage 10 product shaping.

### 9.2 Intentionally deferred to later stages / architecture

- **Concrete benchmark source identities and annotation execution:** Stage 16 will select the seed corpus and instantiate the gold records using the Stage 10 contract.
- **Exact parser/OCR/ASR/model vendors and algorithms:** architecture/implementation.
- **Physical QA/test infrastructure, CI jobs, dashboards, databases, and storage:** architecture/Stage 13.
- **Exact batch/release mechanics and retry schedules:** Stage 14/architecture; Stage 10 defines the behavioral sampling contract.
- **Final cost per 1,000 processed items:** Stage 14.
- **Final field-specific threshold recalibration:** empirical benchmark work in Stage 16 and later production evidence. The initial thresholds in this document govern until better evidence justifies changes.
- **Real learner performance as an external calibration signal:** later App/Corpus contract and Stage 07 recalibration; learner data does not replace source-level QA.

These are implementation/calibration tasks, not missing product decisions.

---

## 10. Definition of Done Check

- [x] Exam-structure validation is defined.
- [x] Answer-key and scoring validation is defined.
- [x] Language-quality checks distinguish source quality from extraction fidelity.
- [x] Metadata-completeness requirements are capability-specific and explicit.
- [x] Broken/task-critical asset validation is defined.
- [x] Audio-question alignment checks and readiness levels are defined.
- [x] AI extraction has a deterministic-first, risk-based cross-check strategy.
- [x] Manual QA sampling rates, strata, and escalation rules are defined.
- [x] Corpus quality metrics and starting qualification targets are defined.
- [x] “Production-ready corpus data” is defined as capability-scoped normal eligible use.
- [x] A manually annotated gold-standard dataset contract, size, composition, annotations, adjudication, and holdout strategy are defined; Stage 16 will instantiate the concrete records.
- [x] Regression expectations against gold/incident cases and last-known-good output are defined.
- [x] Cost control explicitly favors deterministic/local processing, selective cross-checking, bounded manual review, and premium escalation only for high-impact ambiguity.
- [x] No earlier Corpus product decision was silently replaced.

**Stage 10 product shaping is complete when the live checklist reflects these decisions and Stage 16 is understood as the concrete benchmark-instantiation stage rather than a reason to leave Stage 10 quality behavior undefined.**
