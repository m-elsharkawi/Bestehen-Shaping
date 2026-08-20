# Bestehen / Corpus — Final Product Specification

> **Status:** Authoritative Stage 17 product specification  
> **Product:** Bestehen / Corpus  
> **Primary downstream customer:** Bestehen / App  
> **Initial operating posture:** Internal-first, one-owner personal project  
> **Initial acquisition domain:** German A2, B1, and mixed A2–B1 exam and exam-style material  
> **Primary target signal:** TELC B1, with deliberately broader cross-provider evidence  
> **Authority rule:** This document is the consolidated product handoff for design and architecture. Stages 01–16 remain authoritative for detailed rationale, examples, calibration notes, and edge cases. Where a compact statement here appears to conflict with an earlier stage, the explicit reconciliation in this document controls; otherwise the earlier detailed rule remains in force.

---

## 1. Purpose and Scope

### 1.1 Mission

**Bestehen / Corpus turns a broad, provenance-preserving collection of German A2–B1 exam material into trustworthy, rights-aware, deduplicated exam intelligence that Bestehen / App can use to decide what matters for TELC B1 learning, practice, and readiness.**

Corpus is an **exam-data and intelligence product**, not a learner-facing course, generic scraper, public exam mirror, or raw exercise bank. Its job is to answer:

> **What do credible A2/B1 exams and exam-style materials show, how strong is that evidence, how may it be used, and what should Bestehen / App know about the patterns?**

Bestehen / App answers the separate learner-specific questions:

> **What should this learner practice now, how much help should they receive, how did they perform, what should be repaired, and what does their evidence mean for TELC B1 readiness?**

### 1.2 Primary customer and internal users

The primary customer is **Bestehen / App**. The project owner/operator is the primary internal human user. Corpus may later support research or other consumers, but the launch product does not require a public Corpus UI, public API, multi-tenancy, external developer access, billing, or a commercial data product.

### 1.3 Initial collection scope

Corpus initially collects German **A2, B1, and mixed A2–B1** exam or genuinely exam-shaped material from:

- TELC B1 — highest target priority;
- TELC A2–B1;
- Goethe B1 and A2;
- ÖSD B1 and A2;
- DTZ A2–B1;
- established educational publishers;
- identifiable language schools and teachers;
- public repositories and archives;
- credible unofficial exam collections;
- public forums/shared documents when they provide useful leads, fragments, corroboration, or historical evidence;
- standalone A2/B1 exam-style exercises when they contribute useful task/skill evidence.

A1 is **not** an initial Corpus acquisition target. Bestehen / App may make target skills accessible to an A1 learner through scaffolding and progression. Incidental A1 or B2+ material inside an otherwise relevant source may be preserved and labeled without expanding the acquisition mission.

### 1.4 Supported input forms

The product accepts, registers, and can attempt to derive evidence from:

- HTML;
- PDF, including native and scanned PDFs;
- DOC/DOCX;
- images and scans;
- audio;
- video where it contains useful exam evidence;
- ZIP/archive containers.

Automation depth may vary by format. Product support means provenance and useful evidence can be represented without pretending every format is equally cheap or equally automatable.

### 1.5 Explicit initial non-goals

Corpus does not initially attempt to be:

- a general German-language or course-content corpus;
- an A1-to-C2 acquisition program;
- a learner-profile or learner-attempt store;
- a learner-facing exercise library;
- an authoritative TELC scoring/certification service;
- a public mirror of copyrighted source files;
- an exhaustive archive of every German exam ever published;
- a public submission service;
- an authenticated crawler for third-party paid/private sites;
- an always-on AI service;
- an enterprise moderation, compliance, or security platform.

### 1.6 Product success

Corpus success is not measured by document count. A useful Corpus has:

1. **representative coverage** of providers, A2/B1 levels, sections, task families, media, and evidence tiers;
2. **faithful structure** down to the response/scoring-addressable unit;
3. **explicit provenance and trust** with uncertainty preserved locally;
4. **independent rights/usage decisions** that prevent unsafe reuse;
5. **duplicate neutrality** so mirrors and copied material cannot manufacture prevalence;
6. **actionable analytics** about vocabulary, grammar, topics, tasks, skills, reasoning, distractors, progression, difficulty, and TELC relevance;
7. **a stable Corpus → App contract** that lets App consume exam intelligence without rebuilding Corpus logic;
8. **measurable QA and regression gates** for every production capability;
9. **maintainable one-owner operations** without direct database surgery;
10. **financial sustainability** under the personal-project cost envelope.

---

## 2. Inputs / Existing Decisions and Traceability

The final specification consolidates every earlier Corpus shaping document plus the shared product overview and identity.

| Source shaping document | Final-spec responsibility inherited |
|---|---|
| `01_Bestehen_Product_Overview.md` | Umbrella product purpose; Corpus/App separation; learn through TELC; readiness-centered App goal |
| `02_Bestehen_Identity.md` | Calm, diagnostic, evidence-driven posture; no implication of official TELC affiliation |
| `corpus/01-product-mission-and-boundaries.md` | Mission, primary customer, acquisition scope, non-goals, useful-corpus definition |
| `corpus/02-source-strategy.md` | Source categories, discovery/manual intake, formats, provenance, revisit behavior |
| `corpus/03-trust-authenticity-confidence.md` | Authenticity states, confidence dimensions/tiers/gates, review/dispute/quarantine |
| `corpus/04-rights-and-usage-metadata.md` | Rights statuses, action permissions, mixed-rights handling, takedown/removal |
| `corpus/05-canonical-exam-model.md` | Canonical source-to-item model, shared stimuli/assets, scoring, incompleteness |
| `corpus/06-exam-and-skill-taxonomy.md` | Versioned multi-axis taxonomy/skill graph, assignment roles, migrations |
| `corpus/07-difficulty-and-relevance-models.md` | CEFR separation, L/R/T/A/P difficulty, GB1 and TELC relevance, uncertainty |
| `corpus/08-ingestion-and-extraction-pipeline.md` | Conceptual pipeline, partial failure, review/publish/reprocessing semantics |
| `corpus/09-deduplication-strategy.md` | Content identity, derivative lineage, analytical independence, evidence counting |
| `corpus/10-validation-and-quality-assurance.md` | Capability-scoped production readiness, Q0–Q3 severity, quality vector and gates |
| `corpus/11-corpus-analytics.md` | Evidence-aware prevalence, exploratory/decision-grade analytics, App-facing intelligence |
| `corpus/12-corpus-app-contract.md` | Pattern-first conceptual contract, information families, App/Corpus ownership boundary |
| `corpus/13-operations-and-review-experience.md` | Owner-only operations inbox, safe edits, audit, source controls, reprocessing, health |
| `corpus/14-cost-scale-and-automation.md` | Scale envelope, cheap-first ladder, retries/crawl/storage limits, cost budgets |
| `corpus/15-security-privacy-and-abuse-boundaries.md` | No learner-data store, untrusted-input boundary, permissions, retention, future hardening triggers |
| `corpus/16-initial-corpus-benchmark.md` | 16-slot seed benchmark contract, gold core, acceptance gates, immutable benchmark releases |

### 2.1 Reconciliation outcome

No Stage 01–16 product decision needs to be reversed.

One wording distinction is important for architecture handoff: **Stage 16 fully specifies the benchmark dataset contract but intentionally does not claim the concrete source files have already been acquired and annotated.** Product shaping is therefore complete; implementation/bootstrap must instantiate the first real `corpus-benchmark-1.0.0`. This is not an unresolved product or owner question.

---

## 3. Consolidated Decisions and Rationale

### 3.1 The six axes that must never be collapsed

Every architecture must preserve these as different concepts:

1. **Source/provenance** — where the evidence came from and what it claims to be.
2. **Authenticity/evidence confidence** — how strongly Corpus should trust it for a given use.
3. **Rights/usage** — what may be done with source expression.
4. **Difficulty/relevance** — how demanding and how target-relevant the material appears.
5. **Extraction/QA readiness** — whether Corpus recovered and derived the data accurately enough for a specific capability.
6. **Content identity/independence** — whether the observation adds new underlying evidence or is a mirror/derivative.

Examples of combinations that must remain valid:

- Tier A official evidence can be `REFERENCE_ONLY`.
- Openly reusable material can still be Tier C or D evidence.
- A high-TELC-relevance item can be low-confidence.
- A perfectly parsed document can still be quarantined or rights-prohibited.
- A trusted original and a clean mirror can share content identity but retain different source-level provenance/rights observations.

### 3.2 Uncertainty is data, not an error to hide

`unknown`, `not_applicable`, `disputed`, `review_required`, `unresolved_dependency`, `incomplete`, and `provisional` are legitimate product states. Corpus must never invent a missing answer, task, audio link, rights permission, officiality claim, taxonomy leaf, or score merely to create a complete-looking record.

### 3.3 Local evidence wins for high-risk use

A trusted parent does not rescue a bad child. Correctness, direct learner exposure, fine taxonomy, asset links, and similar high-risk uses use the **most specific relevant confidence/QA state**. One bad item should not discard an otherwise useful exam unless the defect demonstrates broader corruption.

### 3.4 Publication is capability-scoped

There is no universal `production_ready=true` meaning “safe for everything.” A unit can be ready for task-frequency analytics while not ready for correctness scoring, source reuse, or independent prevalence counting. Publication is a promotion decision for a stated capability and must carry remaining restrictions.

### 3.5 Corpus is broad; TELC B1 remains the target authority signal

Cross-provider evidence exists to understand generic B1 competence, A2→B1 progression, and provider differences. TELC B1 evidence receives the strongest target weight for claims about the target exam. Cross-provider frequency cannot silently become TELC prevalence, and a TELC-specific pattern can be important even when uncommon elsewhere.

### 3.6 Source evidence informs practice; App practice is normally original

The preferred flow is:

**eligible Corpus evidence → abstract pattern/constraint blueprint → original App exercise → App QA/delivery/evaluation**.

Exact source content is a special reference-content path, not the normal practice path. This reduces rights fragility, memorization, and dependency on a small official sample set.

### 3.7 Cheap, offline, reusable intelligence is the economic default

Corpus enrichment is precomputed, batched, cached, and reused. App sessions do not trigger routine Corpus AI inference. Premium processing and human review are selective escalations for correctness, current TELC facts, benchmark truth, rights/takedown decisions, unique coverage, and other high-impact ambiguity.

---

## 4. Detailed Product Model and Rules

## 4.1 Source strategy and intake

### 4.1.1 Source categories and acquisition priority

| Priority | Source category | Main value | Important guardrail |
|---|---|---|---|
| **P0** | Official exam providers | Target format, scoring context, provider-specific behavior | Official category is not a rights permission or automatic local correctness guarantee |
| **P1** | Established educational publishers | High-quality authored practice and progression evidence | Reputation is evidence, not automatic trust/reuse |
| **P1** | Language schools and identifiable teachers | Realistic practice and broader task variants | Claimed official/real-exam status remains a claim until verified |
| **P1/P2** | Public repositories and archives | Historical/vanished material, alternate formats, corroboration | Hosting location is not original authorship or new independent evidence |
| **P2** | Unofficial exam collections | Breadth where official material is sparse | Require explicit provenance/confidence/dedup treatment |
| **P3** | Forums and public shared documents | Leads, fragments, historical clues, discussion/corroboration | Treat links/claims as candidates, not automatic evidence truth |
| **P2** | Standalone exam-style exercises | Task, skill, vocabulary, grammar, reasoning evidence | Do not infer full-exam balance from standalone tasks |

Both automated coverage-driven discovery and owner manual URL/file submission are required. All intake paths converge on the same provenance, trust, rights, security, validation, and deduplication model. Manual material receives no automatic trust.

Corpus preserves source observations when URLs move, die, redirect, or are mirrored, subject to stronger takedown/privacy/security deletion requirements. Default source revisit posture is monthly for the most important official/current target pages, quarterly for other active high-value sources, and semiannually for stable/lower-value sources, with event/manual revisit when warranted.

Different URLs are not different exams by default. Corpus never requires bypassing login, paywalls, CAPTCHAs, private groups, bot protections, access controls, or source rate limits.

---

## 4.2 Canonical conceptual data model

### 4.2.1 Core hierarchy

**Source Observation → Document → Exam / Test Set → Section → Part (optional) → Task → Item / Question → Answer / Scoring**

with **Instruction, Stimulus, Response Option, Explanation, Scoring Rule/Rubric, and Asset** as separately addressable supporting concepts.

The hierarchy expresses semantic responsibility, not page layout or provider vocabulary.

### 4.2.2 Entity responsibilities

| Concept | Product meaning |
|---|---|
| **Source Observation** | Place/context where material was seen or supplied: URL, archive snapshot, repository path, manual file, etc.; carries observation-specific provenance, access, claims and rights evidence |
| **Document** | Concrete versioned content-bearing artifact such as booklet PDF, answer key, HTML task page, transcript, scoring guide or scan set |
| **Exam / Test Set** | Coherent assessment package or exam-shaped set presented as belonging together; may be complete, partial or fragmentary |
| **Section** | Functional normalized exam division while preserving provider-native labels |
| **Part** | Optional meaningful intermediate provider/task grouping; never invented merely to fit one provider |
| **Task** | Coherent activity with shared instructions/stimulus/response behavior |
| **Item / Question** | Smallest response/scoring-addressable unit; composite parent/child only when subparts are genuinely independently answerable/scorable |
| **Instruction** | Candidate directions; separate from tested language for ordinary tested-content frequency |
| **Stimulus** | Tested input: passage, short texts, audio/video, image, table, form, notice, advertisement, chart, speaking card, etc. |
| **Response Option** | Candidate answer/selection material, including shared option banks |
| **Answer** | Source/reference answer assertion, accepted response, sample response or curated resolution; learner answers belong to App |
| **Explanation** | Source or curated explanatory evidence, distinguishable from tested source content |
| **Scoring Rule / Rubric** | Point values, partial-credit/all-or-nothing behavior, cardinality, totals, productive rubrics, conversions and provider-specific rules |
| **Asset** | Addressable image, scan, audio, video, diagram, form, answer-sheet component or other media |

The model is not a strict tree. One Document may contribute to several Exams/Tasks; one Exam may combine booklet, key, scoring guide and audio; one Stimulus/Asset may serve many Items; and many Source Observations may point to one underlying work.

Shared Stimuli/Assets are represented once and linked, preventing duplicated content frequency, processing cost, rights work, and removal work.

### 4.2.3 Completeness and provider semantics

Supported completeness states are conceptually `complete`, `intentional_excerpt`, `incomplete_known_missing`, and `completeness_unknown`.

Corpus separately tracks:

1. **source incompleteness** — acquired material itself lacks expected content;
2. **extraction incompleteness** — source contains material Corpus failed/not yet extracted;
3. **linking incompleteness** — components exist but their relationship is not verified.

Provider-native names, numbering, order, timing and special rules are preserved alongside canonical semantics. Provider-specific extensions are allowed only for irreducible behavior and must not become dependencies for generic cross-provider analytics.

---

## 4.3 Authenticity, evidence confidence, and trust rules

### 4.3.1 Authenticity status

| Status | Meaning |
|---|---|
| **Verified official** | Credibly established as issued/published by the claimed provider/authority |
| **Verified official-derived copy** | Non-officially hosted copy credibly matched to verified official underlying material |
| **Verified third-party / mock** | Authorship/origin reasonably established as non-official exam-prep material |
| **Claimed official — unverified** | Claims real/official origin without sufficient provenance proof |
| **Origin uncertain** | Corpus cannot responsibly establish official or third-party origin |
| **Suspected misrepresented / fake** | Evidence suggests material origin/exam identity may be materially false |

Similarity to official material can increase evidence confidence; it **cannot** by itself establish officiality.

### 4.3.2 Confidence dimensions and tiers

Applicable dimensions use a 0–4 evidence scale plus `Unknown` and `Not applicable`.

| Dimension | Initial weight |
|---|---:|
| Provider reputation / provenance quality | 20% |
| Similarity to known exam structure | 15% |
| Language quality | 10% |
| Answer-key presence | 5% |
| Answer-key consistency | 15% |
| Similarity to trusted material | 10% |
| Internal structural consistency | 10% |
| Corroboration across independent sources | 15% |

A provisional 0–100 score is the weighted achieved evidence over applicable maximum. `Unknown` contributes no positive evidence while remaining in the denominator; genuinely `Not applicable` dimensions are removed. The number is an internal aid, not scientific precision.

| Tier | Initial band | Meaning | Default eligible aggregate weight |
|---|---:|---|---:|
| **A — Anchor** | 85–100 | Strongly defensible evidence | 1.00 |
| **B — Trusted** | 70–84 | Reliable for most analytical/product-support uses | 0.70 |
| **C — Conditional** | 50–69 | Useful with meaningful uncertainty | 0.25 |
| **D — Weak** | 0–49 | Provenance/discovery/review only by default | 0.00 |
| **Quarantine** | separate state | Serious fake/tamper/integrity concern pending resolution | 0.00 |

Tier A requires established origin quality; uncertain/unverified origin cannot become A. A verified third-party mock can become A if evidence quality genuinely warrants it.

Confidence must be representable at source, document, exam/test-set, task and item scope. Local evidence can raise or lower a child relative to its parent.

### 4.3.3 Hard gates and use thresholds

- suspected fake/tampered/misrepresented identity → quarantine until resolved;
- answer-key consistency 0–1 on objective material → block correctness-dependent use;
- expected key missing → allow appropriate structural/language/topic evidence, not correctness truth;
- severe local language or structural defect → cap/block the affected capability at the smallest safe scope;
- claimed official but unverified → never verified official or Tier A;
- unresolved high-impact conflict → `disputed`; withhold high-risk use.

C+ may contribute bounded exploratory/aggregate context. **B+** is the default minimum for production difficulty influence, App learning-priority evidence, generation grounding and direct source exposure. Learning-priority changes normally require at least **two independent A/B underlying materials**. One verified official TELC source can establish that a target rule/format exists, but not its prevalence. Direct source exposure also requires rights and QA eligibility.

---

## 4.4 Rights and usage model

Rights remain independent from authenticity, confidence, public accessibility, source category and target relevance.

### 4.4.1 Operational statuses

| Status | Product posture |
|---|---|
| **REUSABLE** | Documented permission supports intended direct use, subject to action fields and trust/QA/product suitability |
| **REUSABLE_WITH_CONDITIONS** | Reuse only when all recorded obligations/restrictions can be satisfied |
| **REFERENCE_ONLY** | Allowed internal/reference intelligence; exact source expression and close/reconstructive derivatives not approved for learner redistribution |
| **UNKNOWN_REVIEW_REQUIRED** | Conservative default when evidence is insufficient/conflicting; blocks direct learner reuse, redistribution, close adaptation and commercial assumption |
| **PROHIBITED** | Active use blocked because of explicit restriction, takedown, acquisition/policy problem or reviewed decision |

Authoritative action decisions cover redistribution, derivative/adaptation, commercial use, attribution, share-alike/no-derivatives/non-commercial requirements, scope/asset exclusions, territory/channel/time conditions, and custom obligations.

Rights can attach at source/material/component scope. The most specific applicable rule wins, and a composite use is governed by its most restrictive required component.

`REFERENCE_ONLY` and, where policy permits, `UNKNOWN_REVIEW_REQUIRED` material may still support non-reconstructive intelligence such as structure, taxonomy, difficulty/relevance, prevalence, and abstract generation constraints.

A credible takedown/serious rights concern immediately holds affected direct use/export/source-derived generation/reprocessing. Corpus must support removal/suppression, App invalidation, recomputation without source, stronger purge when required, and a minimal prevention tombstone only when lawful and useful.

---

## 4.5 Exam and skill taxonomy

Corpus uses a versioned **multi-axis controlled graph**, not one giant tree. Families are:

1. provider/exam metadata;
2. CEFR scope;
3. normalized section;
4. task activity family / response mechanic / stimulus form / interaction shape;
5. topic/context;
6. grammar;
7. vocabulary/domain and functional language;
8. Reading skills;
9. Listening skills;
10. Writing competencies;
11. Speaking competencies;
12. exam strategy;
13. reasoning patterns;
14. distractor patterns.

Prefer a low-hundreds strategically useful core over thousands of difficult-to-govern micro-skills.

Every assignment carries a stable node ID, role (`primary_tested`, `secondary_tested`, `prerequisite_supporting`, `context`, `incidental_present`, `distractor`, etc.), confidence, origin/method, supporting evidence, taxonomy version and review state. Presence in a passage is not automatically a tested skill.

Normalized launch sections are Reading, Language Elements where the provider genuinely has that functional section, Listening, Writing and Speaking, plus integrated/other/unknown. CEFR supports A2, B1, A2/B1 mixed, incidental out-of-scope and unknown; CEFR is not numerical difficulty.

Skills/competencies, strategy, reasoning and distractor patterns stay distinct because they lead to different diagnoses and generation constraints.

Stable node identity must not depend on display labels. Taxonomy releases can rename, reparent, merge, split, deprecate or retire nodes through explicit migrations. Splits **must not clone learner mastery** into every new child. App receives taxonomy version/migration semantics separately from the Corpus/App contract version.

High-impact fine taxonomy assignments may auto-publish only after the relevant benchmark slice reaches roughly **≥95% precision** with no systematic learner-diagnosis failure. Otherwise use a broader qualified parent, provisional assignment, or review.

---

## 4.6 Difficulty and TELC relevance

Corpus keeps CEFR, difficulty, Generic-B1 relevance and TELC-B1 relevance separate.

Applicable difficulty dimensions use a provisional 0–100 rubric:

- **L — Linguistic difficulty**;
- **R — Task/reasoning difficulty**;
- **T — Time-pressure difficulty**;
- **A — Audio difficulty**;
- **P — Productive-skill difficulty**.

Bands are very low 0–19, low 20–39, moderate 40–59, high 60–79, very high 80–100 within the A2/B1 Corpus domain. These scores are not pass/fail probabilities and do not map directly to CEFR. The dimension profile is authoritative; a composite is optional convenience.

`GB1` describes broad B1 usefulness. `TELC` describes target-exam alignment. Every estimate carries uncertainty and derivation version.

Decision-grade contribution conceptually combines:

**Independence × Stage-03 confidence weight × target alignment × currentness × scope fit**.

Safeguards include approximately **15% maximum C-tier effective evidence mass** in published relevance/priority conclusions and, when eligible official TELC evidence exists, normally no more than about **35% third-party/unofficial effective support** for a high-confidence TELC-specific conclusion.

Launch difficulty is estimated. Later qualified App performance data may create a separate empirical calibration layer when it is privacy-safe, condition-aware and ability-aware. Single-user struggle never becomes global Corpus difficulty truth.

---

## 4.7 Ingestion, extraction, review, publication, and reprocessing

### 4.7.1 Canonical conceptual lifecycle

**Discover → Fetch → Normalize → Parse → Segment → Classify → Extract Answers → Extract Assets → Enrich → Validate → Deduplicate → Review → Publish**

These are product responsibilities, not required physical jobs. Architecture may combine or parallelize them while preserving traceability, partial state, and gates.

| State | Required product outcome |
|---|---|
| **Discover** | Register candidate, discovery route, relevance/coverage clues and source context |
| **Fetch** | Obtain permitted payload plus transport/redirect/version evidence; fetch success never implies safety/trust/rights |
| **Normalize** | Non-destructively prepare archives/pages/media/encodings for processing |
| **Parse** | Recover machine-readable source text/layout/OCR/media references with region/page lineage |
| **Segment** | Map source regions to canonical Exam/Task/Item/Instruction/Stimulus/etc. without inventing structure |
| **Classify** | Apply source-explicit/deterministic provider, CEFR, section and task-shape normalization |
| **Extract Answers** | Preserve answer/key/scoring assertions with exact origin; missing/conflicting remains missing/disputed |
| **Extract Assets** | Inventory/link media and allow orphan/unresolved assets rather than forced links |
| **Enrich** | Add semantic taxonomy, difficulty/relevance, reasoning/distractors and other derived intelligence with method/version/confidence |
| **Validate** | Apply structural, extraction, correctness, metadata, governance and capability-specific gates |
| **Deduplicate** | Resolve or conservatively bound duplicate/derivative/independence before evidence counting |
| **Review** | Resolve high-impact ambiguity or deliberately preserve restriction/unknown/dispute |
| **Publish** | Promote only the fields/capabilities that pass their current eligibility requirements |

### 4.7.2 Failure and intervention states

Corpus supports localized states such as:

- `retry_pending` / `retry_exhausted`;
- `reprocess_candidate`;
- `blocked_dependency`;
- `review_required`;
- `disputed`;
- `quarantined`;
- `rejected_as_evidence`;
- `prohibited` / `takedown_hold`;
- `superseded`;
- limited/provisional publication.

The default failure philosophy is **salvage first, isolate the smallest affected scope**. Extraction failure must not be mislabeled as source absence. Linking uncertainty must not become an invented relationship.

### 4.7.3 Review priority and human overrides

Human review is exception-based and impact-prioritized:

1. Q0 correctness/scoring, takedown/prohibition, security or direct-exposure risk;
2. current TELC target facts;
3. benchmark/gold/regression blockers;
4. issues materially changing decision-grade analytics/App priorities;
5. unique evidence filling important coverage gaps;
6. repeated ambiguity whose one-time correction prevents future work;
7. low-value C/D/duplicate/optional metadata last.

Human changes are explicit curated corrections/overrides, not silent source rewriting. They retain actor, time, rationale/evidence and previous value. Automation cannot silently overwrite a reviewed decision; it may surface a conflict for owner resolution.

### 4.7.4 Reprocessing

Reprocessing starts at the **earliest affected conceptual stage**, preserves prior derivations/audit, preserves applicable curator overrides, and recomputes only dependent outputs. A new model/version creates a reprocessing opportunity, not an automatic whole-corpus backfill.

---

## 4.8 Duplicate, derivative, and analytical-independence behavior

Corpus never uses one `duplicate=true/false` flag to answer all identity questions. It separates:

1. observation identity;
2. content identity;
3. derivative/lineage relationship;
4. analytical independence for a specific metric.

### 4.8.1 Relationship classes

| Relationship | Default evidence treatment |
|---|---|
| **BYTE_EXACT_COPY** | Same content; zero additional independent evidence |
| **CONTENT_EXACT_COPY** | Same substantive content after allowed normalization; zero additional independent evidence |
| **REFORMATTED_COPY** | Same underlying content in different layout/container/scan/OCR/branding; zero additional independent evidence |
| **DERIVATIVE_COPY** | Common-origin inherited content with edits/annotations/re-recording/etc.; inherited content does not add full independent evidence |
| **FRAGMENT_OF / CONTAINS_FRAGMENT** | Shared region counted once; genuinely new non-shared content evaluated separately |
| **RELATED_VARIANT** | Common template/lineage plausible but materially new solve/listen/write/speak instance; may count separately while lineage remains visible |
| **INDEPENDENT** | Full independent evidence subject to other gates |
| **UNRESOLVED_DEPENDENCY** | Similarity suggests dependence but cannot be safely resolved; production counting remains conservative |

Near-duplicate means evidence of **common content origin**, not merely semantic similarity or a common exam pattern.

Conflicting answer keys do not create two items. The content family remains one item with multiple answer assertions and a local dispute.

Shared assets do not make whole exams duplicates. Independence can be use-specific: a re-recorded identical listening script is dependent for lexical/script frequency but may provide distinct acoustic-difficulty evidence.

### 4.8.2 Canonical preferences are three separate decisions

Corpus distinguishes:

- **canonical provenance anchor** — best-supported origin;
- **preferred processing representation** — cleanest/most complete version for extraction;
- **preferred downstream reusable representation** — rights/product-safe representation if exact reuse is desired.

One observation need not satisfy all three roles.

### 4.8.3 Comparison strategy and evidence counting

Use cheap-to-expensive comparison: raw fingerprint → normalized content fingerprint → structural/local fingerprints → fuzzy lexical/media candidates → semantic escalation only when impact justifies it.

Comparison normalization removes presentation noise but preserves meaning-critical German orthography, numbers, dates, prices, times, negation, options/cardinality and other content that can change the answer.

Decision-grade analytics distinguish:

- source/observation count;
- canonical content occurrence count;
- independent evidence count or conservative range.

Deduplication/independence is applied **before** confidence/relevance weights are summed.

---

## 4.9 Validation, quality assurance, and production gates

### 4.9.1 Quality model

Quality is a vector, not one scalar score. Required dimensions include:

- structural accuracy;
- extraction fidelity;
- correctness/key accuracy;
- taxonomy/semantic accuracy;
- asset/audio-link integrity;
- required metadata completeness;
- duplicate/independence accuracy;
- benchmark/regression health;
- manual-sample defect rates;
- representative slice coverage.

Validation is layered across representation integrity, structural consistency, semantic/correctness quality, governance completeness and capability-specific readiness.

### 4.9.2 Error severity

| Severity | Meaning | Default response |
|---|---|---|
| **Q0 — Critical** | Can teach/score incorrectly, violate a hard governance gate, or materially corrupt decision-grade analytics | Immediate hold of affected capability; no production acceptance |
| **Q1 — Major** | Materially changes meaning/structure/difficulty/priority | Hold affected unit/field/use; correct/review |
| **Q2 — Minor** | Reduces completeness/precision without changing core meaning | Publish only if relevant capability still passes; repair opportunistically |
| **Q3 — Advisory** | Low-risk anomaly/monitoring observation | Record; no automatic hold |

### 4.9.3 Initial benchmark qualification gates

| Capability | Initial gate |
|---|---|
| Structural extraction | **≥98% precision, ≥97% recall**, no accepted Q0 structural error |
| Correctness-critical answer/key/scoring linking | **≥99% precision, ≥97% recall** |
| Meaning-critical text/OCR/ASR | **≥99% exact correctness** on annotated answer/meaning-critical tokens/relations |
| Required metadata completeness | **100%** for every claimed production capability |
| Critical Asset linkage | **≥99% precision** |
| Fine audio item/answer-critical alignment | **≥99% precision**; fall back to coarser defensible alignment when not qualified |
| Q0 escape rate | **0 accepted Q0 escapes** |
| High-impact taxonomy auto-publication | **≥95% precision**, target **≥85% opportunity coverage/recall**, no systematic wrong learner lane |
| Automatic zero-additional-evidence collapse | **≥99% precision**, zero genuinely independent benchmark cases auto-collapsed |
| Exact/reformatted duplicate recall | **≥97%** |
| Derivative/fragment safe-routing recall | **≥90%** to dependent or conservative unresolved state |
| `Verified official` / official-derived automatic classification | **100% precision** |
| Overall authenticity-category agreement | **≥95%** |
| Evidence-tier exact agreement | **≥90%**, **≥98% within one adjacent tier**, Stage-03 hard gates 100% |
| Automatic direct-reuse authorization (`REUSABLE`/conditional) | **100% precision** on initial gold benchmark; zero unsafe reuse upgrades |
| Overall rights-status agreement | **≥95%** |
| Action-authorizing permission/condition decisions | **≥99% precision** |
| `PROHIBITED`/takedown active-use blocking | **100%** |

Metrics are reported by meaningful slices—provider, level, format, section, clean/imperfect input, development/holdout—not only as one overall percentage.

Risk-stratified manual QA initially samples about **10% of a new/changed slice** and **3% of a stable qualified slice**, while gold benchmark records receive full required adjudication. A new method cannot replace last-known-good production behavior merely because it is newer, cheaper, or better on average.

---

## 4.10 Corpus analytics

Corpus produces **evidence-aware intelligence**, not naked counts.

### 4.10.1 Analytical lanes

| Lane | Evidence posture | Allowed use |
|---|---|---|
| **Exploratory** | C+ may contribute with weights; unresolved dependency can be ranges; sparse support allowed | Operator research, pattern discovery, coverage/review targeting; not direct learner priority/readiness |
| **Decision-grade** | Material A/B support; C capped; D/quarantine zero; independence, scope, currentness and QA gates pass | App priority priors, generation grounding, target profile, readiness-evidence design |

### 4.10.2 Result envelope

A decision-grade analytical output conceptually carries:

- subject/pattern identity;
- metric family;
- scope/filter;
- counting unit;
- raw/observation count where useful;
- canonical content occurrence count where useful;
- independent support count/range;
- eligible denominator and denominator coverage;
- effective evidence mass after weighting;
- prevalence/distribution result;
- A/B/C contribution and provider/source concentration where material;
- sufficiency/uncertainty label;
- taxonomy/analytics/model version and recomputation identity;
- allowed downstream roles.

The default language is **denominator-aware prevalence**, not raw frequency.

### 4.10.3 Required analytical families

Corpus must provide:

- vocabulary/functional-language exposure prevalence, density, spread and section/task distribution;
- grammar exposure, tested-dependency and productive-demand prevalence;
- topic prevalence;
- task/response/stimulus/interaction-shape prevalence;
- Reading/Listening skill and Writing/Speaking competency prevalence;
- provider comparisons;
- A2 → mixed A2/B1 → B1 progression analysis;
- TELC-vs-generic-B1 comparisons;
- reasoning-pattern and distractor-pattern analysis where correctness evidence permits;
- co-occurrence across skills, topics, grammar, vocabulary, task shape, reasoning and distractors;
- difficulty distributions and evidence coverage/concentration.

Three frequency concepts remain distinct:

1. **exposure frequency** — how often content is encountered;
2. **tested-dependency frequency** — how often success materially depends on the feature;
3. **exam-structure prevalence** — how often a task/section/response pattern appears in representative assessment structures.

A shared Stimulus counts once for lexical exposure even when multiple Items reference it. A standalone exercise cannot establish whole-exam balance. Provider volume does not become authority.

### 4.10.4 App-facing roles

Analytics feed three Corpus → App roles:

1. **exam-priority priors**;
2. **exercise-generation grounding**;
3. **readiness evidence design**.

They do not own learner mastery, schedule, readiness, or personalized decisions.

---

## 4.11 Contract with Bestehen / App

The contract is conceptual and capability-oriented; architecture may implement it through the simplest maintainable transport.

### 4.11.1 Required information families

App must be able to consume:

1. **raw/reference content** — only for explicitly eligible, product-appropriate reference use;
2. **structured exam metadata** — canonical hierarchy, provider-native details, response/scoring/media relationships, completeness;
3. **aggregate statistics/intelligence** — decision-grade prevalence, comparison, progression, target profile;
4. **skill graph and relationships** — stable IDs, node types, relationships, versions and migrations;
5. **exercise-generation patterns/constraints** — abstract blueprints, not default source wording;
6. **difficulty/relevance signals** — CEFR, L/R/T/A/P, GB1/TELC, uncertainty;
7. **governance/version context** — eligibility, provenance summary, confidence, rights, QA, currentness, contract/taxonomy/analytics versions.

Corpus returns **use eligibility**, not merely ingredients App must reinterpret. App should not need to rebuild the B+ gate, rights policy, quarantine logic, correctness readiness, deduplication or decision-grade analytics rules.

### 4.11.2 Practice-pattern request

App may request a desired pattern using:

- target exam/profile;
- section/task family;
- stable taxonomy nodes and desired assignment role;
- progression/use profile;
- difficulty envelope;
- TELC/GB1 relevance requirements;
- topic/diversification constraints;
- reasoning/distractor pattern;
- modality/media needs;
- timing/playback/interaction constraints;
- exact reusable reference content versus abstract generation grounding.

App does **not** need to send learner mastery, mistakes, readiness, exam date, fatigue, prior exposure, preferences or session time to Corpus. It uses that private learner state to decide the request before calling the Corpus capability.

### 4.11.3 Progression profiles

Corpus supports App requests spanning the established progression semantics:

- **P0 Supported Foundation** — App scaffolds a Corpus-derived target skill into A1-accessible work;
- **P1 Guided A2**;
- **P2 A2/B1 Bridge**;
- **P3 Independent B1 Training**;
- **P4 Target Conditions**.

This does not create an A1 Corpus acquisition scope.

### 4.11.4 Ownership boundary

| Corpus owns | App owns |
|---|---|
| Source discovery/provenance | Learner identity/profile/preferences |
| Authenticity/confidence and rights | Learner attempts/responses/history |
| Canonical exam structure and taxonomy | Session/day planning and scaffolding |
| Deduplication/independence | Original learner-facing exercise creation |
| Global difficulty/relevance | Exercise QA/presentation/evaluation |
| Decision-grade exam analytics | Feedback, repair, retry and coaching |
| Generation blueprints/constraints | Learner mastery and readiness calculation |
| Corpus-side publication eligibility | Final learner-facing eligibility/content policy |

When a source is reclassified/removed or a taxonomy/target-profile version changes, Corpus identifies affected outputs and publishes the changed eligibility/version. App invalidates or reevaluates affected source-backed/reference content and dependent blueprints according to the contract. Original App exercises retain blueprint/version lineage rather than becoming anonymous content.

---

## 4.12 Operations and review experience

A polished bespoke admin dashboard is **not** required at launch. A minimal owner-only **operations surface is required** so ordinary maintenance does not require direct database surgery.

### 4.12.1 Minimum areas

1. **Operations Inbox** — prioritized exceptions with saved views;
2. **Record / Review Detail** — source evidence, structured state, trust/rights/QA/dedup/taxonomy context, history and safe actions;
3. **Source Controls & Intake** — manual URL/file submission, source registry, allow/block, mirrors/dead-source context;
4. **Reprocessing & Change Actions** — scoped reprocess, quarantine/restore, rights/takedown actions and downstream-impact visibility;
5. **Corpus Health** — quality/backlog/coverage/independence/cost/regression health vector.

Specialized inbox views cover discovery, ingestion status, extraction failures, duplicate review, authenticity review, rights review, low-confidence records and taxonomy corrections.

No fixed SLA is needed for the one-owner phase; age and impact are visible and sortable.

### 4.12.2 Governed manual actions

The owner may correct provenance, completeness, confidence, rights, structure, answer links, duplicate relationships, taxonomy assignments, difficulty/relevance reviews and quarantine/restore states at the smallest affected scope. Source expression is not silently rewritten.

Every consequential human or automated change is auditable: actor type, timestamp, previous/new state, rationale/evidence, method/model/rule/taxonomy version, related finding/review, and downstream capability impact.

Allow/block controls govern acquisition behavior only; they do not grant trust or rights. Takedown/security blocks are stronger governed states and cannot be silently reversed by later discovery.

---

## 4.13 Cost, scale, and automation

### 4.13.1 Planning envelopes

| Envelope | Source families | Observations | Unique Documents/Assets | Tasks | Canonical Items | Listening audio | Raw + retained derived storage |
|---|---:|---:|---:|---:|---:|---:|---:|
| **Low / seed** | 25–50 | 500–1,500 | 250–500 | 800–2,000 | 3,000–8,000 | 10–30 h | ≤25 GB |
| **Base / design center** | 75–150 | 5,000–15,000 | 1,500–3,000 | 5,000–12,000 | 20,000–50,000 | 75–200 h | 50–150 GB |
| **High / review envelope** | 300–500 | 30,000–80,000 | 8,000–12,000 | 30,000–60,000 | 120,000–200,000 | 500–1,000 h | 300–750 GB |

These are planning envelopes, not collection quotas. Corpus growth is driven by **marginal information value and coverage gaps**.

### 4.13.2 Cheap-first processing ladder

0. reject/defer low-value candidates before deep work;
1. deterministic intake;
2. deterministic structure and exact deduplication;
3. local/cheap selective OCR/ASR/layout/fuzzy extraction;
4. cheap batched semantic enrichment;
5. selective stronger-model analysis when a required high-value capability cannot meet its gate more cheaply;
6. human/legal/gold review for the highest-impact ambiguity.

At mature base scale, aim for 100% accepted material through deterministic Steps 1–2, roughly 40–60% unique tasks/items receiving some semantic/media enrichment, **≤10% stronger-model escalation**, and **≤2% exception/adjudication human review** in addition to risk-stratified QA sampling.

### 4.13.3 Retry, crawling, and storage guardrails

- transient fetch: 3 total attempts for unchanged action;
- 404/410: no immediate retry loop;
- 429: honor `Retry-After`, max 3 attempts in active cycle;
- deterministic parser: normal attempt + one materially different fallback;
- OCR/ASR: baseline + one targeted escalation only when value justifies it;
- paid semantic derivation: maximum 2 paid attempts per unchanged input/method/prompt/schema version;
- strong-model adjudication: one primary strong pass, optional independent check only for correctness/benchmark gates;
- unchanged deterministic failures are negative-cached until input/dependency/method/operator decision changes.

Default crawling is **1 concurrent request per host**, at least **2 seconds between requests** (default ceiling 0.5 req/s), with a **200-new-URL per unreviewed-host discovery-run ceiling**, while honoring stricter source rules and documented APIs.

Storage is normal through roughly **150 GB**; review storage design above **250 GB or €10/month storage cost**; treat >500 GB as high-scale. A single file above **250 MB** requires explicit value/retention review.

### 4.13.4 Cost targets

Primary variable metric: **paid processing cost per 1,000 newly processed canonical Items**.

- target: **≤€3 / 1,000 Items**;
- warning: >€3–4;
- optimize/escalate: >€4–5;
- stop/review: >€5 on a rolling ≥5,000-Item cohort absent a documented high-value exception.

Normal Corpus-specific recurring cash spend should stay **≤€25/month**, with **€50/month hard ceiling without explicit owner override**. A deliberate Stage 16 benchmark/regression/high-value backfill campaign may use **≤€75** as a separately initiated one-off allowance.

Routine steady-state owner review should normally fit around **1 hour/week**; exception review should average **≤30 minutes per 1,000 newly processed canonical Items** outside deliberate gold/benchmark work.

Cost control may reduce enrichment depth, defer ambiguity, or favor a smaller corpus; it must never weaken provenance, rights/takedown, correctness, QA/regression, duplicate neutrality, uncertainty preservation, benchmark truth, or the Corpus/App boundary.

---

## 4.14 Security, privacy, and abuse boundaries

### 4.14.1 Launch privacy boundary

Corpus is **not a learner-data store**. It does not own learner accounts, learner attempts, learner writing/voice, readiness, mistake history, advertising/device identifiers or learner analytics.

Minimal personal data may exist only for operator audit identity, public source attribution/rights provenance, or incidental source content. Derived representations should omit/redact irrelevant personal information where practical without falsifying source evidence.

### 4.14.2 External inputs are untrusted

Every URL/file/archive/page/media asset is untrusted regardless of provider reputation or owner submission.

Launch requirements:

- normal automated retrieval is HTTP/HTTPS only;
- block private/internal/link-local/metadata destinations and unsafe redirects;
- no access-control circumvention;
- preflight type/container/size/archive/resource-amplification risk before expensive processing;
- supported formats are inspected as data; macros/scripts/binaries/active source content are not executed;
- archive expansion is bounded; suspicious/encrypted/pathological archives are held rather than brute-forced;
- operations displays use inert/sanitized representations;
- source text is data for AI, never authority to invoke tools, reveal secrets, change policy, delete records, grant rights or auto-publish;
- source processing does not receive unnecessary secrets or owner-level authority;
- App has no raw-source-store/admin/secret access.

### 4.14.3 Launch authority model

- **Owner/curator:** authenticated governed operations, review/correction/block/reprocess/quarantine/rights/takedown actions;
- **automated workers/models:** derive/propose/execute explicitly allowed pipeline work; cannot silently override curated decisions or weaken hard blocks;
- **Bestehen / App:** consume published Corpus contract capabilities only.

Enterprise RBAC is deferred until more human write-capable operators exist.

### 4.14.4 Retention

Accepted unique useful raw evidence may be retained long-term while it materially supports provenance, QA, reprocessing, benchmark or rights needs and retention is permitted. Exact duplicate bytes need not be physically repeated.

Temporary regenerable intermediates are deleted after successful validation when not needed for audit/debug. Rejected/irrelevant and security-dispositioned payloads target removal within **7 days** after disposition unless an investigation justifies longer. Rights-prohibited/takedown active raw content targets the same prompt removal window where deletion is required/permitted, with only minimal allowed audit/prevention metadata retained.

Manual submissions are owner-only at launch. Public submissions, multiple operators, authenticated crawling, commercialization/public data sharing, recurring sensitive source data, or a security incident explicitly trigger re-shaping/hardening.

---

## 4.15 Initial benchmark and regression contract

The benchmark is a **product specification that implementation must instantiate**, not evidence that source acquisition has already occurred.

### 4.15.1 Seed and gold core

The initial seed contains **16 source-package slots**, normally yielding roughly **450–650 Items**, **55–75 Tasks**, and **60–90 task-relevant Asset relationships**.

The detailed gold core uses **12–14 packages**, roughly **320–420 manually adjudicated Items**, **45–55 Tasks**, **28–36 Listening Task/Item mappings**, and **55–70 Asset relationships**.

The gold core is approximately **55–65% B1** and **35–45% A2/mixed**, with TELC the largest single provider family but normally no more than about half. Goethe, ÖSD, DTZ and non-official sources remain represented so qualification cannot overfit TELC or clean official PDFs.

Mandatory source roles include:

- two independent TELC B1 anchors/resources;
- TELC A2–B1;
- Goethe B1 and A2;
- ÖSD B1 and A2;
- DTZ A2–B1;
- established publisher material;
- identifiable school/teacher HTML or equivalent;
- productive Writing/Speaking third-party material;
- credible unofficial B1 material;
- imperfect scan/image-heavy material;
- fragment/repository/archive/shared material with detached relationship stress;
- origin-uncertain/claimed-official-unverified/negative-control material;
- mirror/reformatted/derivative family.

All five launch sections are represented. Format requirements include native PDF, HTML, scans/images and audio; DOC/DOCX is included when a representative source is reasonably available; video is optional initially.

### 4.15.2 Gold truth and split

Gold annotation covers source identity, canonical structure, source regions, instructions/stimuli, response mechanics/cardinality, answer/scoring assertions, completeness, critical Assets/audio alignment, provider/CEFR/task shape, selected high-impact taxonomy, meaning-critical OCR/ASR truth, duplicate/independence truth, expected Q0/Q1 findings, authenticity/confidence and rights behavior.

Gold truth comes from inspectable evidence and documented rules, not model voting. Genuine ambiguity is labeled unknown/disputed/unresolved/review-required.

The detailed core uses approximately **70% development / 30% frozen holdout**, split at underlying content/derivative-family level so mirrors/derivatives cannot leak across the boundary.

### 4.15.3 Benchmark releases and promotion

The first concrete release is **`corpus-benchmark-1.0.0`**. Benchmark releases are immutable and evolve with semantic-style major/minor/patch behavior.

Regression layers are:

1. all-16 seed smoke regression;
2. development gold regression;
3. frozen holdout qualification;
4. incident replay set containing every confirmed important production Q0/Q1 escape.

A meaning-changing parser/model/rule/taxonomy/dedup change may replace last-known-good production behavior only when relevant hard gates pass, Q0 regressions are zero, no new systematic Q1 class appears, precision-oriented safety metrics remain qualified, incident replays pass, and slice reports do not hide provider/format/section/level regressions.

If an exact benchmark slot cannot be acquired lawfully/safely, do not invent or bypass access controls. Substitute the closest source preserving the failure/test purpose, record the debt, and do not declare `1.0.0` complete while a mandatory benchmark cell is missing.

---

## 5. Edge Cases / Failure and Uncertainty Handling

| Situation | Required product behavior |
|---|---|
| Official source has one wrong/disputed answer | Keep overall official provenance; localize dispute to affected answer/item; block correctness use until resolved |
| Objective task has no key | Keep structure/language/topic evidence; do not invent correctness truth |
| Writing/Speaking has no single correct answer | Treat objective-key dimensions as N/A where appropriate; use rubric/content-point evidence instead |
| Partial scan has intact tasks | Mark source/document incompleteness; keep intact tasks locally eligible when independently validated; never infer full-exam balance |
| Same exam appears at 20 URLs | Preserve 20 observations; count one underlying evidence occurrence unless independence evidence says otherwise |
| Two independent tasks are semantically similar | Similarity alone is not duplication; do not collapse without common-origin evidence |
| Same listening script re-recorded | Dependent for script/language frequency; potentially distinct acoustic-difficulty evidence |
| High-confidence official material has unclear rights | Can influence eligible abstract intelligence; direct learner reuse remains blocked |
| Openly licensed material is poor quality | Rights do not upgrade confidence; weak evidence remains weak |
| Source rights change or takedown arrives | Immediate affected-use hold; remove/suppress/recompute/invalidate according to scope; prevent mirror re-ingestion |
| New model is cheaper/better on average | Qualify on benchmark/holdout/incident replays first; no automatic corpus-wide backfill |
| Paid retry would breach budget | Defer unless Q0/current-target/benchmark-critical; keep unknown/provisional instead of overspending automatically |
| Unsafe or suspicious payload from reputable provider | Security gate wins; hold/block payload while provenance observation remains |
| Source contains prompt injection | Treat as source text only; it cannot command tools/policy/secrets/publishing |
| Taxonomy node splits | Do not clone historical learner mastery; migrate identity/evidence conservatively and request new direct evidence where needed |
| Removed source was only support for a priority | Retain historical aggregate only if policy allows; otherwise recompute and allow priority to disappear |
| Corpus is smaller than planning target but analytically sufficient | This is success; stop/slow low-value acquisition rather than collect to quota |

---

## 6. Relationship to Bestehen / App and Other Stages

### 6.1 Bestehen / App

Corpus provides the **exam evidence layer**. App remains the **exam coach**. Readiness is an App-owned learner judgment informed by Corpus target structure, scoring facts, skill graph, difficulty/relevance and evidence-design priors. Corpus never converts its source confidence or prevalence directly into a learner readiness score.

The independent written/oral pass constraints of the target exam remain part of the App readiness model; Corpus supplies verified target-format/scoring evidence needed to model those constraints but does not calculate a learner's pass probability.

### 6.2 Earlier Corpus stages

This final specification does not replace the detailed examples, matrices and edge cases in Stages 01–16. Architecture should consult the source shaping documents when implementing a specific capability. This document defines the combined invariants, launch boundary, dependency order and acceptance contract.

### 6.3 Later design and architecture

The architecture agent may optimize implementation aggressively for simplicity and cost, but it may not reinterpret product semantics such as:

- URL = exam;
- source category = confidence;
- confidence = rights;
- CEFR = difficulty;
- TELC relevance = trust;
- published = learner-safe for all uses;
- repeated mirrors = prevalence;
- AI confidence = benchmark quality;
- learner state = Corpus state.

---

## 7. Launch Requirements, Later Enhancements, and Intentionally Open Architecture

### 7.1 Launch/product-complete requirements

Product shaping covers the complete Corpus experience. Implementation may phase delivery, but the first maintainable usable Corpus must preserve these behaviors rather than inventing them later:

1. source registry plus automated discovery and owner manual URL/file intake;
2. permanent/auditable provenance subject to stronger deletion requirements;
3. trust/authenticity model and local confidence gates;
4. independent rights/usage model and takedown path;
5. canonical exam representation through task/item plus shared stimulus/scoring/assets;
6. versioned taxonomy and stable skill-node identities;
7. difficulty and Generic-B1/TELC relevance with uncertainty;
8. capability-scoped ingestion/validation/publication and selective review;
9. duplicate/derivative/independence handling before decision-grade evidence counting;
10. evidence-aware analytics;
11. stable pattern-first Corpus → App capability contract;
12. owner-only operations, audit, source controls and scoped reprocessing;
13. cost ledger, bounded retries/crawling/storage and cheap-first automation;
14. launch security/privacy boundaries and no learner-data store;
15. a concrete instantiated benchmark/gold core for every automated production capability being qualified, using the Stage 16 contract and passing the relevant gates.

Not every supported source format needs equal automation depth at first release. A safe manual/review fallback is acceptable when the product semantics and quality gates remain intact.

### 7.2 Later product enhancements triggered by evidence/scale

These are explicitly deferred until a real need exists:

- public or third-party source submissions;
- multi-user operations and role-separated review;
- public Corpus API/research UI/export product;
- automated authenticated crawling of third-party paid/private sites;
- full-video understanding when audio/captions/selected visuals are insufficient;
- much larger/high-scale corpus operation beyond formal scale-review triggers;
- stronger commercial/legal rights program for broad direct source reuse;
- learner-performance-based empirical global difficulty calibration after privacy-safe aggregated evidence exists;
- richer bulk reprocessing/dry-run/campaign tooling;
- enterprise security/compliance/monitoring controls;
- fine-grained taxonomy expansion where real App diagnosis shows the broader graph is insufficient.

These are deferred features, not gaps in launch product reasoning.

### 7.3 Intentionally open architecture/implementation decisions

The product does **not** choose:

- relational/document/graph database or physical schema;
- object/file storage technology and physical dedup layout;
- API transport (REST/GraphQL/RPC/shared data/bundle/etc.);
- queue/workflow/scheduler technology;
- crawler framework and exact discovery provider;
- parser/OCR/ASR/layout/model vendors or local runtimes;
- model names, prompts, embedding models, vector/ANN technology;
- exact hash/fingerprint/similarity algorithms after benchmark calibration;
- admin/low-code/custom operations UI technology;
- authentication/secret-manager implementation;
- sandbox/malware-scanner/HTML-sanitizer/SSRF-protection implementation;
- deployment topology/cloud provider;
- cache/index implementation;
- analytics engine/warehouse/BI technology;
- logging/telemetry/observability stack;
- CI/test-runner mechanism for benchmark regression;
- backup topology and physical deletion mechanics.

Architecture may choose the cheapest maintainable option that satisfies the product rules and measured scale envelope.

---

## 8. Cost Notes

Cost is a first-class product constraint, but **quality and exam-coaching integrity are not traded away to make Corpus free**.

### 8.1 Preferred low-cost default

- deterministic/source-explicit extraction before models;
- local/native text before OCR;
- source transcript before ASR;
- page/region/segment-selective expensive processing;
- exact dedup and derivation reuse before semantic work;
- batched offline semantic enrichment;
- broader/provisional/unknown output instead of paying for low-value false precision;
- stronger models only for benchmark-qualified high-impact slices;
- human/legal review only where correctness, rights, current TELC facts, benchmark truth, unique coverage or repeated failure justify it;
- App consumes cached/precomputed Corpus outputs rather than per-learner Corpus inference.

### 8.2 Upgrade rule

Pay more only when a measured bottleneck affects a required product outcome: quality gate failure, persistent high-value backlog, storage/owner-time threshold, current TELC freshness, or benchmarked improvement with acceptable economics.

A premium method must have a cheaper fallback: local/deterministic processing, broader classification, unknown/provisional state, deferred processing, or targeted owner review.

### 8.3 Cost guardrails retained from Stage 14

- base design: 20k–50k canonical Items, 50–150 GB;
- paid variable target: ≤€3/1,000 Items;
- recurring Corpus cash target: ≤€25/month;
- hard paid ceiling absent owner override: €50/month;
- explicit benchmark/backfill campaign allowance: ≤€75;
- normal storage sub-budget: about ≤€5/month;
- routine owner review: around ≤1 hour/week steady state.

These are initial product guardrails and should be recalibrated from real cost logs after the first 5,000–10,000 processed Items without weakening the cheap-first principle.

---

## 9. Decisions Made

1. Corpus is a broad **A2/B1 exam-data and intelligence product** whose primary customer is Bestehen / App; TELC B1 is the strongest target signal, not the only source family.
2. A1 scaffolding belongs to App; A1 is not an initial Corpus acquisition target.
3. Official and unofficial evidence may enter Corpus; source class, authenticity/confidence and rights are independent.
4. Canonical structure is cross-provider and source-faithful: Source Observation → Document → Exam → Section → optional Part → Task → Item, with first-class shared instructions/stimuli/options/answers/scoring/assets.
5. Incompleteness and uncertainty are explicit; Corpus does not fabricate missing source truth.
6. Authenticity uses categorical status; evidence confidence uses dimensions plus A/B/C/D tiers and local hard gates.
7. Rights use five conservative operational statuses plus action-level permissions/conditions; unknown rights never become implicit reuse permission.
8. Corpus uses a stable versioned multi-axis taxonomy shared conceptually with the App learner model; taxonomy migrations never invent learner mastery.
9. CEFR, multidimensional difficulty, Generic-B1 relevance and TELC relevance remain distinct, versioned, uncertainty-aware signals.
10. The product lifecycle is Discover → Fetch → Normalize → Parse → Segment → Classify → Extract Answers → Extract Assets → Enrich → Validate → Deduplicate → Review → Publish, with partial success and scoped reprocessing.
11. Publication is capability-scoped, not a universal validity flag.
12. Deduplication preserves all observations while separating content identity, derivative lineage and metric-specific analytical independence.
13. Decision-grade prevalence uses independent, quality-weighted evidence and explicit denominators, never raw mirror/source volume.
14. Corpus analytics cover vocabulary, grammar, topic, task, skill/competency, provider, A2→B1, TELC-vs-generic-B1, reasoning/distractors, co-occurrence and difficulty distributions.
15. Corpus → App is pattern-first: Corpus supplies eligible exam intelligence/blueprints; App owns learner state, original practice, evaluation, coaching and readiness.
16. The initial one-owner operations experience is a minimal governed inbox/detail/source-control/reprocessing/health surface with append-only audit, not an enterprise dashboard.
17. The economic design center is 20k–50k canonical Items with cheap-first local/deterministic/batched processing, ≤€3/1k variable processing target and ≤€25/month normal Corpus cash envelope.
18. Corpus stores no learner data; every external input is untrusted, non-executing, sanitized/bounded, and separated from secrets/admin authority.
19. Stage 16 defines a 16-slot seed benchmark and 12–14-package gold core with explicit quality/trust/rights/dedup gates, 70/30 content-family dev/holdout split and immutable benchmark releases.
20. The first concrete benchmark `corpus-benchmark-1.0.0` is an implementation/bootstrap obligation; its source acquisition/annotation is not falsely claimed by product shaping.
21. No major product choice is left for architecture to invent. Architecture remains free to choose implementation technology, algorithms and vendors inside these semantics, gates and cost/security boundaries.

---

## 10. Open Questions / Deferred Decisions

### 10.1 Owner questions

**None.** The existing shared product principles and Stage 01–16 decisions are sufficient to produce a complete Corpus product specification without asking the owner to choose an unresolved product trade-off.

If Bestehen later becomes public/commercial, accepts third-party uploads, adds multiple human operators, or relies on broad direct redistribution/training of source material, those changed constraints should reopen the affected rights/security/operations decisions at that time. They do not block the current product.

### 10.2 Unresolved product questions

**None that block architecture.** Empirical calibration work remains, but its product behavior is already decided:

- confidence weights/bands can be recalibrated from benchmark evidence;
- difficulty/relevance models can be empirically calibrated when qualified data exists;
- dedup similarity thresholds can be recalibrated against the gold set;
- cost guardrails can be updated from measured economics;
- taxonomy may evolve through versioned migrations;
- benchmark cases can expand when new failure surfaces appear.

These are measurement/calibration activities under defined rules, not missing product choices.

### 10.3 Deferred implementation/bootstrap work

The major non-product deliverable still required before automated Corpus capabilities can claim benchmark-qualified production readiness is:

- acquire lawful/safe real sources satisfying the Stage 16 slots;
- manually adjudicate the gold core;
- publish immutable **`corpus-benchmark-1.0.0`**;
- qualify each automated production capability against its applicable gold/holdout/incident gates.

The concrete dataset does **not** yet exist merely because its specification is complete.

### 10.4 Deferred architecture decisions

All technology choices listed in Section 7.3 remain intentionally open. They are architecture decisions because the required product semantics, quality gates, cost limits, security outcomes and fallback behavior are already specified.

---

## 11. Definition of Done Check

| Stage 17 requirement | Final-spec coverage | Status |
|---|---|---|
| Final Bestehen / Corpus PRD | Entire document | Complete |
| Canonical data model | §4.2 | Complete |
| Source tiers/confidence rules | §4.1, §4.3 | Complete |
| Rights/usage classifications | §4.4 | Complete |
| Taxonomy and versioning | §4.5 | Complete |
| Ingestion and review states | §4.7, §4.12 | Complete |
| Deduplication behavior | §4.8 | Complete |
| Corpus → App responsibilities | §4.11, §6.1 | Complete |
| Analytics outputs | §4.10 | Complete |
| Quality metrics | §4.9, §4.15 | Complete |
| Explicitly deferred features | §7.2, §10 | Complete |
| Product questions separated from architecture questions | §10.1–§10.4 | Complete |
| What/where to collect | §1.3–§1.4, §4.1 | Complete |
| Trustworthiness | §4.3 | Complete |
| Rights independent from authenticity | §3.1, §4.4 | Complete |
| Exam → structured data | §4.2, §4.7 | Complete |
| Stable exam/skill taxonomy | §4.5 | Complete |
| Duplicate neutrality | §4.8 | Complete |
| Difficulty/TELC relevance | §4.6 | Complete |
| Required analytics | §4.10 | Complete |
| Exact App consumption boundary | §4.11 | Complete |
| Gold-standard benchmark product contract | §4.15 | Complete |
| Concrete gold-standard dataset instantiated | §10.3 | **Deferred to implementation/bootstrap; intentionally not falsely claimed** |
| No major product decision left for architecture | §7, §10 | Complete |

### Final product-shaping conclusion

**Bestehen / Corpus is product-shaped.** A later architecture agent can choose technology and implementation sequencing without inventing the product's mission, scope, evidence model, rights policy, exam model, taxonomy, difficulty/relevance semantics, pipeline behavior, deduplication policy, QA gates, analytics contract, App boundary, operations model, economic envelope, security boundary, or benchmark definition.

The only deliberately incomplete “dataset” artifact is the concrete Stage 16 benchmark instantiation, which is explicitly an implementation/bootstrap task under a fully defined product contract.
