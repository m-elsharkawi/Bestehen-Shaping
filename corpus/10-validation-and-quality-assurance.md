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

- referenced local/retained asset payload exists or the unavailable state is explicit;
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

A missing asset is Q0/Q1 when the candidate cannot interpret/solve/score the task without it. Decorative images, optional thumbnails, or redundant representations may be Q2/Q3.

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
- answer-critical speech (numbers, dates, times, prices, negation, restrictions, speaker corrections, names/entities) is accurately captured enough for the claimed use;
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

Deterministic consistency is necessary but not sufficient. The benchmark and manual sampling program defined later in this document must detect systematic semantic failure; such a method loses auto-publication eligibility even if it emits syntactically perfect data.

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
- **Stage 16:** will instantiate the representative benchmark corpus and manually annotate the concrete gold records according to the contract defined by Stage 10.
- **Stage 17:** should incorporate this QA contract into the final Corpus PRD.

---

## 7. Cost Notes — Part A

The default validation path should be financially cheap:

- deterministic structural/cardinality/reference checks run broadly;
- source-provided metadata, checksums, MIME/media decoding, and stable rules are preferred over AI interpretation;
- local/open-source language/OCR/ASR checks are appropriate where benchmark quality is sufficient;
- only affected pages/segments/fields are reprocessed after a failure;
- premium-model review is never required merely because a cheaper method expresses uncertainty;
- low-value C/D duplicate/noisy material may remain limited or unresolved instead of consuming review budget.

The detailed AI cross-check, manual-sampling, benchmark, and regression cost policy follows in the completed Stage 10 document.
