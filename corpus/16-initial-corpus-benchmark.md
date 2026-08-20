# Bestehen / Corpus — Stage 16: Initial Corpus Benchmark

> **Status:** Authoritative Stage 16 product-shaping decision  
> **Product:** Bestehen / Corpus  
> **Primary operator:** One owner in the personal-project phase  
> **Primary downstream customer:** Bestehen / App  
> **Core principle:** The initial benchmark is a small, deliberately representative and adversarial slice of the A2/B1 source universe. It must be broad enough to expose extraction, taxonomy, trust, rights, deduplication, media, and partial-source failures, but small enough for one owner to adjudicate carefully and rerun whenever Corpus behavior changes.

---

## 1. Purpose and Scope

Stage 16 establishes the **representative seed and gold-standard benchmark contract** that later architecture and implementation must use to prove that Bestehen / Corpus works on realistic material rather than only on clean happy-path files.

The benchmark has four jobs:

1. prove that the Stage 05 canonical model can represent realistic cross-provider A2/B1 material;
2. measure whether Stage 08 extraction and Stage 06 enrichment meet the Stage 10 production-quality gates;
3. prove that Stage 03 trust, Stage 04 rights, and Stage 09 deduplication preserve uncertainty and do not create unsafe false certainty;
4. provide a small, versioned regression suite that every materially meaning-changing parser, model, rule, taxonomy, or pipeline change can replay before replacing the last-known-good behavior.

This remains **product shaping, not source acquisition or implementation**. This document does not claim that the concrete files have already been downloaded, does not invent source URLs, and does not choose parsers, OCR/ASR systems, model vendors, test frameworks, storage technology, or CI tooling. Instead it defines **concrete benchmark slots and selection criteria**. During implementation/bootstrap, the owner fills those slots with real sources that meet the criteria and records their actual provenance.

### 1.1 Benchmark objective

**A later implementation should fail this benchmark when it mishandles a realistic source boundary—even if it performs perfectly on clean official PDFs.**

The benchmark is therefore intentionally not statistically representative of the eventual production corpus. It **over-samples hard and dangerous cases** because its primary role is qualification and regression, not prevalence estimation.

### 1.2 Benchmark versus production corpus

The Stage 14 low planning envelope remains much larger: roughly 3,000–8,000 canonical Items once Corpus has moved beyond the benchmark seed. The Stage 16 benchmark is a curated test fixture inside that future corpus, not a target corpus size and not the dataset from which final frequency conclusions should be drawn.

---

## 2. Inputs / Existing Decisions

Stage 16 preserves the shared Product Overview, Identity, both live shaping checklists, and Corpus Stages 01–15.

### 2.1 Scope and source breadth — Stages 01–02

- Initial acquisition is German **A2, B1, and mixed A2–B1** material.
- TELC B1 is the strongest target signal, while TELC A2–B1, Goethe A2/B1, ÖSD A2/B1, DTZ A2–B1, established educational material, teacher/school material, repositories/archives, unofficial collections, public shared material, and standalone exam-style exercises are in scope.
- HTML, PDF, DOC/DOCX, scans/images, audio, video, and archives are accepted Corpus formats, although not every format must have equal automation depth at launch.
- Partial material is useful evidence when incompleteness remains explicit.
- Different URLs are observations, not automatically independent exams.

### 2.2 Trust and rights — Stages 03–04

- Authenticity status, evidence confidence, and usage rights are independent.
- Evidence confidence uses A/B/C/D tiers plus quarantine/review state.
- Rights use `REUSABLE`, `REUSABLE_WITH_CONDITIONS`, `REFERENCE_ONLY`, `UNKNOWN_REVIEW_REQUIRED`, and `PROHIBITED`, with action-level permissions and conditions.
- Unknowns remain unknown; public accessibility never grants reuse permission.
- A benchmark must therefore include cases where trust and rights point in different directions.

### 2.3 Canonical model and taxonomy — Stages 05–07

- The canonical hierarchy is Source Observation → Document → Exam/Test Set → Section → optional Part → Task → Item, with Instructions, Stimuli, Response Options, Answers, Explanations, Scoring Rules/Rubrics, and Assets separately addressable.
- The normalized taxonomy covers provider/exam, CEFR, Section, task shape, topic, grammar, vocabulary/domain, Reading/Listening skills, Writing/Speaking competencies, strategy, reasoning, and distractors.
- High-impact fine taxonomy mappings require about **95% measured precision or better** before normal auto-publication.
- CEFR, multidimensional difficulty, generic-B1 relevance, TELC relevance, trust, and rights remain separate signals.

### 2.4 Pipeline, deduplication, and QA — Stages 08–10

The benchmark must exercise the conceptual lifecycle:

**Discover → Fetch → Normalize → Parse → Segment → Classify → Extract Answers → Extract Assets → Enrich → Validate → Deduplicate → Review → Publish**.

Stage 10 already sets the initial gold-standard envelope and quality posture:

- approximately **12–20 source packages/documents/exam fragments**;
- **300–500 Items**;
- **40–60 Tasks** with manually verified boundaries/shared Stimuli;
- **25–40 Listening Task/Item mappings**;
- at least **50 task-relevant Asset relationships**;
- deliberate exact, reformatted, fragment, derivative, related-variant, and independent comparison cases;
- approximately **70/30 development/holdout** benchmark separation;
- **≥98% structural precision and ≥97% structural recall**;
- **≥99% correctness-link precision and ≥97% recall**;
- **≥95% high-impact taxonomy precision**;
- **≥99% meaning-critical text/OCR/ASR fidelity**;
- **100% required metadata completeness** for a claimed production capability;
- **≥99% critical Asset and item/answer-critical audio-link precision**;
- **≥99% automatic duplicate/evidence-collapse precision**;
- **zero accepted Q0 escapes**.

Stage 16 does not weaken those gates. It supplies the concrete benchmark composition and completes the remaining calibration policy.

### 2.5 Analytics, App contract, operations, cost, and security — Stages 11–15

- Decision-grade analytics use independent, quality-weighted evidence rather than raw URL/file counts.
- App normally consumes pattern-first, rights-safe intelligence rather than source expression.
- Benchmark/gold records receive high review priority in the operations inbox.
- Gold annotation is allowed to exceed routine steady-state review-time budgets because it purchases reusable automation confidence.
- Cheap/local/deterministic processing is the default; paid stronger-model work is selective.
- Every external file/URL is untrusted input; benchmark status never bypasses security preflight or retention/takedown rules.

No earlier product decision is replaced by Stage 16.

---

## 3. Decisions and Rationale

## 3.1 Use one seed benchmark with a detailed gold core

**Decision:** The initial benchmark has two nested scopes.

| Scope | Initial target | Purpose |
|---|---:|---|
| **Seed benchmark** | **16 source-package slots**, normally producing roughly **450–650 Items**, **55–75 Tasks**, and **60–90 task-relevant Asset relationships** once instantiated | Exercise realistic provider/source/format breadth and provide smoke/regression coverage beyond the manually detailed subset |
| **Gold core** | **12–14 of the 16 package slots**, contributing roughly **320–420 manually adjudicated Items**, **45–55 Tasks**, **28–36 Listening Task/Item mappings**, and **55–70 Asset relationships** | Qualification metrics, threshold calibration, detailed regression, and frozen development/holdout evaluation |

The ranges are intentionally approximate because provider packages differ in structure. **Composition and failure-case coverage matter more than filling an Item quota.** If 330 carefully chosen Items already cover every required benchmark cell, the owner should not annotate another hundred low-value near-identical Items merely to increase the count.

All 16 seed packages receive at least a **manual package-level provenance/authenticity/rights review**. The gold core receives the detailed structural/extraction/taxonomy/dedup annotations defined below.

### Why not gold-annotate everything?

A fully detailed 600-Item benchmark would add owner effort faster than it adds distinct failure coverage. The 12–14-package gold core stays inside the Stage 10 target while the remaining seed packages provide format/provider smoke coverage and future candidates for benchmark expansion.

## 3.2 The benchmark is deliberately target-weighted, not TELC-only

**Decision:** B1 and TELC receive more benchmark weight because Bestehen / App targets TELC B1, but the benchmark must preserve enough A2 and cross-provider evidence to expose overfitting.

Target composition for the gold core:

- approximately **55–65% B1 evidence** by adjudicated Item/Task coverage;
- approximately **35–45% A2 or mixed A2–B1 evidence**;
- TELC evidence is the largest single provider family, but **no more than roughly half of the gold core** should come from TELC;
- Goethe, ÖSD, and DTZ must each be represented when suitable official/authority material is available;
- third-party and unofficial evidence must be represented rather than relegated to non-gold smoke tests.

These are balancing targets, not statistical weights for production analytics.

## 3.3 The benchmark must include negative and uncertain examples

A benchmark containing only records that should eventually publish normally cannot validate uncertainty handling.

At least one seed/gold case must exercise each of these outcomes where a real suitable source can be acquired:

- high-confidence official/anchor evidence;
- strong third-party/mock evidence;
- conditional but useful evidence;
- weak/origin-uncertain or quarantinable evidence;
- rights `REFERENCE_ONLY` or `UNKNOWN_REVIEW_REQUIRED` despite useful/high-confidence exam evidence;
- a reusable or conditionally reusable third-party source where rights are clearer than authenticity;
- incomplete/fragmentary material;
- a disputed or detached relationship that must remain unresolved until evidence supports linking.

A suspected fake source is useful as a negative control **only when a real candidate exists**. Stage 16 does not require inventing a fake public source. An origin-uncertain or materially misrepresented candidate is sufficient to test the safe default.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Concrete 16-slot seed composition

The benchmark is instantiated by filling the following slots with real material. A single real package may satisfy several format/section needs, but a slot should not be silently removed merely because another package is convenient; substitutions must preserve the reason the slot exists.

| Slot | Required source selection criterion | Level / role | Preferred format or stress case | Expected trust role |
|---|---|---|---|---|
| **B01** | Current or clearly versioned **official TELC B1** model/practice package with answer/scoring evidence and listening media where distributed | B1, primary target anchor | Native PDF + audio; complete package preferred | Likely A anchor after adjudication |
| **B02** | A second **independent TELC B1** official/current or historically relevant package/section resource that is not merely a mirror of B01 | B1, target breadth/currentness | Prefer HTML or materially different packaging from B01 | Likely A anchor |
| **B03** | Official **TELC A2–B1** mixed-level representative package | Mixed A2–B1, progression + TELC-family continuity | PDF + audio where available | Likely A anchor |
| **B04** | Official **Goethe B1** representative/model package | B1, cross-provider anchor | PDF + audio where available | Likely A anchor |
| **B05** | Official **Goethe A2** representative/model package | A2 progression anchor | PDF/HTML; audio where available | Likely A anchor |
| **B06** | Official **ÖSD B1** representative/model package | B1 cross-provider anchor | PDF and relevant media | Likely A anchor |
| **B07** | Official **ÖSD A2** representative/model package | A2 cross-provider anchor | PDF/HTML and relevant media | Likely A anchor |
| **B08** | Official/authority-backed **DTZ A2–B1** representative package | Mixed A2–B1 cross-provider anchor | PDF + audio where available | Likely A/B anchor depending on provenance chain |
| **B09** | Established educational publisher's public **B1 exam-prep sample** with identifiable authorship/provenance | B1 third-party quality case | Native PDF or DOC/DOCX preferred | Expected A/B or B |
| **B10** | Established publisher, language school, or teacher **A2/mixed exam-style HTML** set with identifiable source context | A2/mixed third-party + HTML case | HTML with embedded assets if possible | Expected B |
| **B11** | Credible school/teacher/publisher material emphasizing **Writing and/or Speaking**, with explicit prompt/rubric/instruction structure | B1 productive-task case | DOC/DOCX, HTML, or PDF | Expected B/C depending on evidence |
| **B12** | Useful **unofficial B1 mock/collection** that appears structurally credible but has weaker provenance than established sources | B1 unofficial-positive case | PDF/HTML; answer key preferred | Expected B/C |
| **B13** | **Imperfect scanned/image-heavy A2/B1 source** with real OCR/layout difficulty and at least one known missing/cropped/partial element | A2/B1 imperfect-input case | Scan/image-heavy PDF or images | Expected C or locally mixed |
| **B14** | **Fragmentary repository/archive/shared-document case** with a detached answer key, detached asset, or cross-document relationship that cannot be assumed from filenames alone | Any in-scope level; linking/provenance stress | PDF/HTML/DOCX/audio fragment | Expected C/D or mixed |
| **B15** | Real **origin-uncertain, claimed-official-unverified, malformed, or otherwise low-trust candidate** useful for safe-negative classification | A2/B1 claimed scope | Any supported format | Expected C/D/quarantine; never pre-label final truth |
| **B16** | A naturally occurring **mirror/reformatted/derivative family** tied to another seed item, chosen specifically to exercise copied, reformatted, excerpted, or lightly altered content | Deduplication stress | Cross-format preferred: PDF↔scan/HTML/DOCX; audio variant if available | Trust/rights remain observation-specific |

### Slot substitution rule

If a precise format/provider artifact is genuinely unavailable or cannot be lawfully/safely acquired, replace the slot with the closest source that preserves the **test purpose**, record the substitution rationale, and add the missing cell to benchmark backlog. Do not fabricate a source simply to satisfy a table row.

## 4.2 Required provider, tier, level, section, and format coverage

### Provider and source-family minimums

The instantiated seed must contain:

- TELC B1;
- TELC A2–B1;
- Goethe B1 and A2;
- ÖSD B1 and A2;
- DTZ A2–B1;
- at least **three non-official source families** across publisher/school/teacher/unofficial/repository/shared material.

### Evidence-confidence coverage

Because Stage 03 tiers are adjudicated outcomes rather than source labels, the benchmark **seeks** enough diversity to end with roughly:

- **6–8 Tier A** package/document anchors;
- **3–5 Tier B** trusted cases;
- **2–3 Tier C** conditional cases;
- **1–2 Tier D or quarantined/negative-control cases**.

If manual adjudication places a chosen source in a different tier, preserve the truth. Add/replace a benchmark slot only when the resulting benchmark no longer covers an important tier behavior.

### Major exam sections

The gold core must contain all five normalized launch sections:

- Reading;
- Language Elements / Sprachbausteine **where the provider actually has that functional section**;
- Listening;
- Writing;
- Speaking.

Minimum gold coverage should normally include:

- **≥10 Reading Tasks**;
- **≥6 Language Elements Tasks** across applicable providers/material;
- **≥10 Listening Tasks**;
- **≥8 Writing Tasks/Items**;
- **≥8 Speaking Tasks/Items**.

Productive tasks naturally contain fewer objective Items; they are not underrepresented merely because their Item count is lower.

### Format minimums

The seed benchmark must contain at least:

- **6 native-text PDF packages/fragments**;
- **2 HTML sources**;
- **2 scan/image-heavy sources or source components**, at least one imperfect/partial;
- **5 source packages with audio or listening assets**, yielding the Stage 10 target of **25–40**, preferably **28–36**, gold Listening Task/Item mappings;
- **1 DOC/DOCX source when a representative in-scope source is reasonably available**.

Video remains optional for the initial benchmark, consistent with Stage 10. When video becomes a meaningful production source, add a benchmark case in a future minor release rather than weakening the existing audio requirement.

## 4.3 Required failure/stress families

The gold benchmark must contain explicit adjudicated cases for:

1. clean native extraction;
2. OCR-heavy scan with meaning-critical text;
3. incomplete/partial source;
4. detached answer key or cross-document link;
5. clean audio mapping;
6. awkward audio/transcript/alignment case;
7. missing or broken critical Asset;
8. mixed confidence inside one package;
9. mixed rights inside one package or composite task;
10. exact byte/content mirror;
11. reformatted/cross-format copy;
12. fragment/excerpt;
13. derivative/lightly edited content;
14. related variant that should **not** be collapsed as exact evidence;
15. genuinely independent look-alike;
16. shared Stimulus referenced by several Items;
17. conflicting or suspicious answer/key assertion where the safe result is dispute/hold rather than forced correctness;
18. provider-native structure that differs from TELC so the canonical model cannot pass by TELC-specific assumptions.

### Audio-specific dedup stress

Where suitable material exists, include at least one of:

- same recording transcoded/trimmed;
- same script re-recorded by another voice;
- independent recordings with similar topic/wording.

This verifies Stage 09's rule that independence may differ for linguistic-content frequency versus acoustic-difficulty evidence.

## 4.4 Gold-core annotation policy

### 4.4.1 What is manually adjudicated

For every applicable gold unit, manual truth must capture:

- Source Observation and package/document identity;
- canonical Section/Part/Task/Item boundaries and containment;
- source page/region/track/segment evidence supporting the annotation;
- Instructions versus Stimuli/tested content;
- response mechanics, cardinality, answer options/slots;
- answer/key/scoring assertions and exact supporting source/version;
- source incompleteness versus extraction/linking incompleteness;
- task-critical Assets and expected relationships;
- audio Task/Item alignment at the finest **defensible** granularity;
- provider/exam family, CEFR scope, normalized Section, and task facets;
- selected **high-impact** taxonomy assignments: primary/secondary tested skill, reasoning/distractor where applicable, and other mappings needed to measure Stage 06's gate;
- meaning-critical text/audio tokens for OCR/ASR fidelity measurement;
- duplicate/derivative/independence ground truth for selected comparison families;
- expected Q0/Q1 findings for deliberately imperfect cases;
- authenticity status and evidence-confidence tier/gates at the scope needed to test Stage 03 behavior;
- rights operational status, important action-level permissions/conditions, and mixed-rights scope needed to test Stage 04 enforcement.

Gold annotation does **not** require exhaustive labeling of every optional topic, grammar feature, vocabulary concept, or low-risk taxonomy leaf. Annotate what is required to qualify the production capabilities and challenge cases.

### 4.4.2 Minimum annotation for non-gold seed packages

The 2–4 seed packages outside the detailed gold core still receive manually reviewed:

- provenance/source identity;
- provider/claimed exam/level;
- package completeness notes;
- authenticity status/evidence tier;
- rights operational status;
- top-level Section/task coverage;
- known duplicate/derivative relationships to gold records;
- security/retention restrictions relevant to replay.

They can later be promoted into the gold core without changing their stable benchmark identity.

### 4.4.3 Adjudication rule

Gold truth is based on **inspectable source evidence and documented product rules**, not model majority vote.

For ambiguity:

1. prefer direct source/provider/license/provenance evidence;
2. use a second independent manual pass for correctness-critical, rights, officiality, or difficult duplicate cases when the first judgment is not obvious;
3. if the evidence genuinely cannot resolve the question, the gold label is the appropriate **unknown/disputed/unresolved/review-required** state—not a guessed answer;
4. any later correction creates a new benchmark version with rationale.

A stronger paid model may assist comparison, but it is never the adjudicator of record for the gold set.

## 4.5 Development and holdout split

**Decision:** The detailed gold core is split approximately **70% development / 30% holdout**.

The split is made at the **underlying content/derivative family level**, not by randomly splitting Items.

Rules:

- all mirrors, reformats, fragments, derivatives, and known common-origin variants of one content family stay in the same split;
- shared answer keys/audio/assets stay with the source family they qualify;
- one provider may appear in both splits, but the exact underlying exam/work may not;
- the development set may be used to tune thresholds, prompts, parsers, rules, and model choices;
- the holdout set is not used for tuning and is evaluated only for qualification, scheduled benchmark health checks, or regression investigation;
- if a small slice has too few examples to support a meaningful holdout claim, report exact counts and mark the slice **holdout-weak** rather than pretending statistical confidence.

The holdout split should normally contain at least:

- one TELC B1 anchor family;
- one non-TELC official family;
- one A2/mixed family;
- one imperfect/unofficial or difficult format family;
- one duplicate/derivative comparison family;
- listening/audio evidence.

## 4.6 Extraction acceptance criteria

The Stage 10 targets become the initial Stage 16 qualification gates.

| Quality area | Initial benchmark target | Failure behavior |
|---|---|---|
| **Structural extraction** | **≥98% precision, ≥97% recall** on required entities/relationships; no accepted Q0 structural error | Slice/method does not qualify for normal production use; keep last-known-good or route affected units to review |
| **Correctness-critical answer/key/scoring linking** | **≥99% precision, ≥97% recall**; no known systematic wrong-answer class | Wrong/ambiguous links are held; unlinked is safer than wrongly linked |
| **Meaning-critical text/OCR/ASR** | **≥99% exact correctness** on annotated meaning/answer-critical tokens/relations | Any Q0 token error blocks the affected capability and triggers investigation |
| **Required metadata completeness** | **100%** for every claimed capability | Capability cannot be advertised as production-ready while required metadata is absent |
| **Critical Asset linkage** | **≥99% precision**, with no known Q0 wrong-asset association | Leave unlinked/review-required instead of forcing relationship |
| **Audio item/answer-critical alignment** | **≥99% precision** for auto-published fine alignment | Fall back to defensible coarser Task-level alignment when fine precision does not qualify |
| **Q0 escape rate** | **0 accepted Q0 escapes** | Release/slice qualification fails until understood and contained |

Metrics must be reported both overall and by meaningful slice: provider family, level, format, Section, clean versus imperfect input, and development versus holdout. A strong clean-PDF score cannot hide failure on scans or audio.

## 4.7 Taxonomy acceptance criteria

**Decision:** Taxonomy qualification is safety-weighted: precision for learner-impacting assignments matters more than maximizing leaf coverage.

Initial gates:

1. **High-impact auto-published assignments** such as `primary_tested`, reasoning pattern, distractor pattern, and other mappings that directly affect learner diagnosis/generation must achieve **≥95% precision** on the applicable gold slice.
2. **High-impact opportunity coverage/recall** should target **≥85%** on benchmark cases that genuinely support a fine mapping. Falling below this does not justify unsafe guesses; it means the method is too incomplete for broad automation and must use broader/provisional tags or selective review.
3. Normalized Section and explicit task-shape mappings that are structurally/deterministically recoverable are evaluated with the structural-quality gate rather than receiving a looser semantic-classification target.
4. There must be **zero known systematic misclassification class** that would repeatedly attribute learner evidence to the wrong direct-evidence lane or productive/receptive capability.
5. A method that misses the fine-label gate may still qualify at a broader parent taxonomy node when that parent mapping itself meets its benchmark target.

The benchmark reports precision, recall/coverage, confusion pairs, and `unknown/provisional` rate separately. A model cannot appear accurate merely by refusing to classify every difficult case.

## 4.8 Deduplication acceptance criteria

**Decision:** Deduplication is evaluated as a safety decision about evidence independence, with additional relationship-class diagnostics.

Initial targets:

- **Automatic zero-additional-evidence collapse precision: ≥99%**, with **zero benchmark cases where genuinely independent evidence is auto-collapsed** into one evidence unit.
- **Exact/content-exact/reformatted mirror recall: ≥97%** on gold cases that should be recognized through normal qualified processing.
- **Derivative/fragment safety-routing recall: ≥90%**: at least 90% of known dependent derivative/fragment cases must be classified as dependent **or conservatively `UNRESOLVED_DEPENDENCY`**, rather than granted full independence.
- `RELATED_VARIANT` and genuinely `INDEPENDENT` look-alikes must not be collapsed merely because semantic similarity is high.
- Relationship-class exact accuracy is reported as a diagnostic, but **safe independence treatment is the hard gate**. Ambiguous near-duplicates may remain unresolved without failing the benchmark if their evidence contribution is conservatively bounded.

This preserves Stage 09's deliberate asymmetry: a false automatic collapse is more harmful than leaving an ambiguous pair unresolved.

## 4.9 Authenticity and evidence-confidence acceptance criteria

Authenticity evaluation measures the Stage 03 **product classification**, not a metaphysical claim that every source's true history is knowable.

Initial targets:

1. Assignment of **`Verified official` or `Verified official-derived copy` must have 100% precision** on the gold benchmark. Resemblance or repeated community claims are never enough.
2. Across adjudicated authenticity categories, target **≥95% exact category agreement** with gold truth.
3. There must be **zero unsafe upgrades** from `Claimed official — unverified`, `Origin uncertain`, or `Suspected misrepresented/fake` to `Verified official` without the required provenance evidence.
4. A deliberate low-trust/negative-control case must result in the expected safe behavior: bounded influence, dispute, quarantine, or another Stage 03-compliant restriction; it must not become decision-grade merely because extraction looks clean.
5. Evidence-confidence tiering should reach **≥90% exact A/B/C/D tier agreement** and **≥98% agreement within one adjacent tier** on the annotated benchmark scopes.
6. Stage 03 hard caps/gates—such as disputed answer use, officiality requirements for Tier A, and quarantine—must be enforced **100%** on applicable benchmark cases.

The tier targets are initial calibration targets, not claims of scientific precision. More important than an A/B boundary disagreement is preserving every hard gate that prevents unsafe downstream influence.

## 4.10 Rights-classification acceptance criteria

Rights gold labels represent Bestehen's **operational classification from the evidence available at annotation time**, not definitive legal judgments.

Initial targets:

1. **Zero unsafe reuse upgrades.** No gold case labeled `REFERENCE_ONLY`, `UNKNOWN_REVIEW_REQUIRED`, or `PROHIBITED` may be auto-classified as reusable for an action that the gold evidence does not permit.
2. `REUSABLE` and `REUSABLE_WITH_CONDITIONS` decisions used for automatic learner-facing/direct reuse require **100% precision** on the initial gold benchmark.
3. Overall operational status should reach **≥95% exact agreement** across the five Stage 04 statuses.
4. Required action-level permission/condition decisions used to authorize an action should achieve **≥99% precision**; when a condition/scope is uncertain, the correct fallback is `unknown`/review, not permissive inference.
5. **100% of `PROHIBITED`/takedown-hold cases** must block the affected active use.
6. Mixed-rights composite cases must enforce the **most restrictive relevant component** unless the restricted component is explicitly removed/replaced in a product-valid way.
7. No source may receive broader rights because it is official, Tier A, public, mirrored widely, or easy to extract.

A benchmark release remains valid for historical regression even if current real-world rights later change, but current compliance uses the latest rights state. If a takedown or retention rule requires raw benchmark material to be deleted, deletion wins over benchmark reproducibility; the affected benchmark version becomes partially non-replayable and a replacement case is added in a new release.

## 4.11 Benchmark versioning

**Decision:** The benchmark is released as an immutable, named artifact using semantic-style versions:

`corpus-benchmark-MAJOR.MINOR.PATCH`

The first fully instantiated and adjudicated benchmark is **`corpus-benchmark-1.0.0`**.

Each release must identify conceptually:

- the 16 benchmark slot identities and the concrete source observations/packages used;
- stable benchmark case IDs independent of filenames/URLs;
- source/document/content fingerprints sufficient to detect accidental substitution;
- gold annotation release and adjudication notes;
- development/holdout membership;
- duplicate/derivative family membership;
- taxonomy version;
- validation/rule versions relevant to expected outcomes;
- authenticity/confidence and rights evidence snapshot/date;
- known retention/takedown limitations;
- expected failure/hold/quarantine outcomes;
- benchmark metric definitions.

### Version-change rules

- **PATCH** — correct an annotation/evidence note or narrow benchmark defect without changing metric meaning or intended composition. Recompute results and preserve the previous release metadata.
- **MINOR** — add/replace benchmark cases, add a new provider/format/failure slice, or expand gold coverage while preserving evaluation semantics.
- **MAJOR** — change gold-label meaning, core metric definitions, required capability gates, split semantics, or composition philosophy in a way that makes old and new qualification results not directly comparable.

A benchmark release is immutable. Corrections create a new version; they do not rewrite old benchmark truth in place.

## 4.12 Regression-testing policy

The benchmark supports four regression layers:

| Layer | Data | Use |
|---|---|---|
| **Seed smoke regression** | All 16 seed packages | Detect fetch/normalize/parse/format/provider breakage and unexpected package-level state changes |
| **Development gold regression** | ~70% detailed gold | Tune and rapidly compare parser/model/rule/taxonomy changes |
| **Frozen holdout qualification** | ~30% detailed gold | Decide whether a materially meaning-changing change may replace last-known-good behavior |
| **Incident replay set** | Every confirmed production Q0/Q1 escape or important historical defect | Prevent known failures from returning even when they were not in the original benchmark |

### Qualification rule for a change

A materially meaning-changing parser/model/rule/taxonomy/dedup change may replace the last-known-good production method only when:

1. every hard Stage 16 capability gate relevant to that change passes on the appropriate gold and holdout slices;
2. there are **zero accepted Q0 regressions**;
3. no new systematic Q1 failure class appears;
4. precision-oriented safety metrics do not regress below the last-known-good method merely to gain recall, unless a documented product decision explicitly accepts the trade-off and all hard gates still pass;
5. incident replay cases pass;
6. slice reports show that aggregate gains are not hiding a regression on scans, audio, unofficial material, one provider, one Section, or one level.

The exact CI/test-runner mechanics are architecture decisions. The product requirement is that this qualification evidence exists before promotion.

### Small-slice rule

The benchmark is intentionally small. For a slice with a very small denominator, report **exact numerator/denominator and the individual failing cases** rather than presenting a percentage as if it were statistically precise. A slice may be marked `insufficient benchmark support` even when all current examples pass.

## 4.13 Benchmark growth and retirement

Add a case to a future minor release when it provides a **new failure surface**, such as:

- a new provider structure;
- a new source format/media relationship;
- a newly observed extraction incident;
- a rights/authenticity boundary not already represented;
- a duplicate pattern that fooled the current method;
- a taxonomy distinction that becomes high-impact;
- a new current TELC target-format fact.

Do not grow the benchmark merely because more content is available.

A case can be retired from the **active replay set** when it is legally/security-wise unavailable, obsolete for the intended behavior, or redundant with stronger cases. Its historical metrics/identity remain documented unless policy requires deletion. Replacement should preserve the failure class whenever that class still matters.

---

## 5. Edge Cases / Failure or Uncertainty Handling

### 5.1 A required provider/format source cannot be acquired

Do not invent one and do not bypass access controls. Record the unfilled slot, substitute the closest lawful source that preserves the test purpose, and keep the missing cell visible as benchmark debt.

The initial `1.0.0` benchmark should not be declared complete while a **mandatory checklist requirement**—A2/B1, all major sections, HTML, PDF, audio, or an imperfect unofficial source—is absent. Optional DOC/DOCX/video coverage may be deferred when no representative source is reasonably available.

### 5.2 A gold source contains an actual source error

Preserve the source error as source truth and annotate the expected QA finding. Do not silently correct the benchmark source text/key. If a curator establishes a corrected interpretation, store it as a separate adjudicated assertion with evidence.

### 5.3 An answer remains genuinely disputed

The gold result is `disputed`/not correctness-ready. The benchmark tests whether Corpus **withholds unsafe correctness**, not whether the model guesses the answer a human reviewer happens to prefer.

### 5.4 Rights are legally ambiguous

The gold operational label is `UNKNOWN_REVIEW_REQUIRED` or the reviewed conservative status. The benchmark tests consistent product policy, not legal speculation.

### 5.5 Authenticity cannot be established

Keep `Claimed official — unverified` or `Origin uncertain`. Similarity to a trusted exam may improve evidence confidence without upgrading officiality.

### 5.6 A duplicate case is genuinely ambiguous

`UNRESOLVED_DEPENDENCY` is a valid gold answer when the available evidence cannot defensibly distinguish derivative from independent origin. The regression requirement is that production analytics bound its evidence conservatively.

### 5.7 A benchmark source is removed or subject to takedown

Stage 04/15 removal rules override benchmark convenience. Remove/suppress raw material as required, retain only permitted non-reconstructive identity/history, mark the affected benchmark release partially non-replayable, and replace the case in a new benchmark version.

### 5.8 One package dominates Item count

Do not allow a large cloze/reading set to dominate benchmark metrics. Use per-slice reporting and, where necessary, cap or stratify sampled Items so one package cannot make the overall number look good while other providers/formats fail.

---

## 6. Relationship to Other Bestehen Stages

### Stage 03 — Trust / authenticity

Stage 16 provides the manually adjudicated anchor, unofficial, uncertain, and negative-control cases needed to calibrate provenance/officiality classification and A/B/C/D confidence behavior.

### Stage 04 — Rights

Stage 16 verifies safe status/permission decisions, especially unknown/reference-only evidence, conditional reuse, mixed-rights composites, and prohibited/takedown behavior. It does not turn product policy into legal advice.

### Stage 05 — Canonical model

The benchmark is the proof set for representing complete exams, fragments, shared Stimuli, detached keys/assets, productive tasks, and provider-native structures without TELC-only assumptions.

### Stage 06 — Taxonomy

The gold subset establishes the first production-stable taxonomy qualification baseline and tests high-impact assignment precision. Taxonomy evolution must preserve benchmark compatibility/versioning.

### Stage 07 — Difficulty/relevance

Difficulty/relevance values may be included in benchmark reports, but Stage 16 does not fabricate accuracy targets for uncalibrated numerical difficulty. The gold set primarily validates prerequisite extraction/taxonomy/currentness inputs and can later support separate expert/learner calibration.

### Stage 08 — Pipeline

Every benchmark package must be replayable through the same conceptual lifecycle as production material; benchmark-only shortcuts must not replace real pipeline behavior.

### Stage 09 — Deduplication

Stage 16 supplies the exact/reformatted/fragment/derivative/variant/independent and audio cases needed to calibrate provisional similarity thresholds and enforce safety-weighted independence treatment.

### Stage 10 — QA

Stage 16 **instantiates** the Stage 10 gold contract and accepts its hard quality gates as the starting benchmark thresholds.

### Stage 11 — Analytics

The benchmark does not establish production prevalence. It verifies that mirror/derivative and confidence/rights treatment does not corrupt the evidence units that analytics will later consume.

### Stage 12 — Corpus → App contract

Benchmark qualification determines whether a Corpus capability is safe enough to publish through the conceptual App contract. The App should never receive a restricted source merely because it is part of the benchmark.

### Stage 13 — Operations

Gold/benchmark cases and benchmark regressions are high-priority operational records. Corrections, reprocessing, and benchmark-version changes remain auditable.

### Stage 14 — Cost

Gold creation is a deliberate one-off investment outside routine review-time targets. The benchmark is intentionally hundreds of Items so one owner can maintain it.

### Stage 15 — Security

Benchmark sources remain untrusted external input and do not bypass file/URL safety, model-input isolation, secret boundaries, sanitization, retention, or takedown rules.

### Stage 17 — Final Corpus specification

Stage 17 should treat this document as the authoritative benchmark/acceptance-test baseline and include its composition, quality gates, versioning, and regression role in the final PRD rather than inventing a separate test corpus.

---

## 7. Cost Notes

The benchmark has **low recurring cash cost but meaningful one-time owner-time cost**.

### Preferred low-cost default

- Acquire only sources that fill a benchmark slot/failure cell; do not crawl broadly for benchmark purposes.
- Reuse raw downloads and derived representations; do not pay repeatedly to process identical content.
- Use deterministic/native extraction and local/free OCR/ASR where it meets the measurement need.
- Batch any paid model comparisons offline.
- Use premium/stronger models only for a narrow ambiguity where cheaper processing cannot meet a benchmark gate and resolving the ambiguity materially changes the product result.
- Manually inspect narrow rights/authenticity/correctness questions rather than paying for repeated model voting.
- Keep the frozen benchmark small; add a case only when it contributes a new failure surface.

### What would justify more spend later

Additional paid processing or expert review is justified when:

- a high-value TELC or correctness-critical slice repeatedly misses its gate;
- audio/OCR quality cannot be measured/qualified cheaply;
- a new format becomes important enough to App/Corpus behavior to deserve its own benchmark slice;
- real production incidents show the current benchmark is missing a dangerous failure class;
- legal review is required before a material can be operationally classified for the intended use.

There is **no requirement for always-on paid AI** in benchmark execution. Stable benchmark annotations and expected outcomes should make most regression runs deterministic and inexpensive.

---

## 8. Decisions Made

1. The initial seed benchmark uses **16 concrete source-selection slots**, with no fabricated source URLs.
2. The seed is expected to contain roughly **450–650 Items**; the detailed gold core uses **12–14 packages and roughly 320–420 Items**, within Stage 10's 300–500-Item contract.
3. B1/TELC are intentionally overweighted but A2/mixed and Goethe/ÖSD/DTZ remain mandatory cross-provider coverage.
4. The benchmark includes official, established third-party, unofficial, imperfect, fragmentary, origin-uncertain, and duplicate/derivative evidence.
5. HTML, native PDF, scan/image-heavy input, and audio are mandatory; DOC/DOCX is included when a representative source is reasonably available; video is optional initially.
6. Reading, Language Elements where applicable, Listening, Writing, and Speaking are all represented in the gold core.
7. All seed packages receive manual package-level provenance/authenticity/rights review; 12–14 packages receive detailed gold annotation.
8. The gold core uses an approximately **70/30 content-family-level development/holdout split** to prevent duplicate leakage.
9. Stage 10 extraction gates become the initial Stage 16 acceptance criteria without weakening them.
10. High-impact taxonomy auto-publication requires **≥95% precision**, with an initial **≥85% opportunity coverage/recall target** and safe broader/provisional fallback.
11. Automatic evidence collapse requires **≥99% precision**, exact/reformatted recall **≥97%**, and derivative/fragment safety routing **≥90%**.
12. `Verified official` auto-classification requires **100% precision**; overall authenticity-category target is **≥95%**, with zero unsafe officiality upgrades.
13. Rights authorization uses a **zero-unsafe-reuse** policy; reusable/conditional automatic authorization requires **100% precision** on the initial gold benchmark, with ≥95% overall status agreement and ≥99% precision on action-authorizing permission/condition decisions.
14. The first instantiated release is `corpus-benchmark-1.0.0`; benchmark releases are immutable and follow major/minor/patch evolution rules.
15. Regression uses seed smoke, development gold, frozen holdout, and incident replay layers; last-known-good production behavior is preserved when a new method does not qualify.
16. Benchmark growth is driven by new failure coverage, not by Item count.

---

## 9. Open Questions / Deferred Decisions

### 9.1 Owner questions

**None.** The existing product decisions are sufficient to establish the benchmark specification without a new owner preference.

### 9.2 Deliberately deferred implementation/acquisition decisions

- the exact URLs/files chosen to fill B01–B16;
- physical benchmark manifest/annotation file format;
- parser, OCR, ASR, embedding, or LLM implementations;
- regression test framework and CI integration;
- physical storage of raw/derived benchmark artifacts;
- exact matching/fingerprinting algorithms and similarity thresholds after calibration;
- whether a representative DOC/DOCX or later video source is available for the first concrete release;
- statistical confidence intervals once the benchmark has enough cases to justify them;
- expert/learner calibration targets for numerical difficulty/relevance, which require evidence beyond source annotation alone.

These are not missing product decisions. Architecture/implementation must preserve the composition, gold truth, safety gates, and versioning behavior defined here.

---

## 10. Definition of Done Check

- [x] A representative seed mix across TELC, Goethe, ÖSD, DTZ, third-party, unofficial, uncertain, and derivative/mirror material is specified.
- [x] Both A2/mixed and B1 are explicitly represented and balanced toward the B1 target without becoming B1-only.
- [x] Reading, Language Elements where applicable, Listening, Writing, and Speaking are required in the gold core.
- [x] HTML, native PDF, scans/images, audio, and at least one imperfect unofficial source are mandatory benchmark cells; DOC/DOCX is included when representative material is available.
- [x] A 12–14-package / 320–420-Item manually adjudicated gold core is defined inside the 16-slot seed.
- [x] Gold annotation covers canonical structure, answers/scoring, critical OCR/ASR tokens, Assets/audio links, taxonomy, trust, rights, deduplication, and expected QA findings.
- [x] Extraction accuracy targets preserve the Stage 10 hard gates.
- [x] Taxonomy accuracy and safe-fallback behavior are measurable.
- [x] Deduplication auto-collapse, mirror recall, and derivative-safe-routing targets are measurable.
- [x] Authenticity/officiality and evidence-tier expectations are measurable and safety-weighted.
- [x] Rights-classification expectations explicitly prevent unsafe reuse and test mixed/unknown/prohibited cases.
- [x] Development/holdout separation prevents duplicate-family leakage.
- [x] Benchmark semantic versioning, immutable releases, correction behavior, and takedown handling are defined.
- [x] Seed smoke, development regression, frozen holdout qualification, and incident replay use are defined.
- [x] The benchmark remains small enough for one owner and does not require always-on paid AI.
- [x] No actual source acquisition is falsely claimed and no source is invented to fill a slot.

**Stage 16 is product-shaping complete when the live Stage 16 checklist is reconciled with this document. The implementation/bootstrap phase then instantiates `corpus-benchmark-1.0.0` using real sources that satisfy these slots and preserves this document's acceptance criteria.**
