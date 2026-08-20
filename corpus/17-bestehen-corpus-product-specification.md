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

A1 is **not** an initial Corpus acquisition target. The App may make target skills accessible to an A1 learner through scaffolding and progression. Incidental A1 or B2+ material inside an otherwise relevant source may be preserved and labeled without expanding the acquisition mission.

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
| `02_Bestehen_Identity.md` | Calm, diagnostic, evidence-driven product posture; no implication of official TELC affiliation |
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

There is no universal `production_ready=true` meaning “safe for everything.” A unit can be:

- ready for task-frequency analytics;
- ready for topic/skill intelligence;
- not ready for correctness scoring;
- not ready for direct source reuse;
- not independent enough to count in decision-grade prevalence.

Publication is a promotion decision for a stated capability and must carry the restrictions that remain.

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

| Default acquisition priority | Source category | Main value | Important guardrail |
|---|---|---|---|
| **P0** | Official exam providers | Target format, scoring context, provider-specific behavior | Official source category is not a rights permission or automatic local correctness guarantee |
| **P1** | Established educational publishers | High-quality authored practice and progression evidence | Publisher reputation is evidence, not automatic trust/reuse |
| **P1** | Language schools and identifiable teachers | Realistic practice and broader task variants | Claimed official/real-exam status remains a claim until verified |
| **P1/P2** | Public repositories and archives | Historical/vanished material, alternate formats, corroboration | Hosting location is not original authorship or new independent evidence |
| **P2** | Unofficial exam collections | Breadth where official material is sparse | Require explicit provenance/confidence/dedup treatment |
| **P3** | Forums and public shared documents | Leads, fragments, historical clues, discussion/corroboration | Treat links/claims as candidates, not automatic evidence truth |
| **P2** | Standalone exam-style exercises | Task, skill, vocabulary, grammar, reasoning evidence | Do not infer full-exam balance from standalone tasks |

### 4.1.2 Discovery and manual intake

Both are required:

- automated, coverage-driven discovery from known providers, targeted queries, bounded link neighborhoods, repositories and archives;
- owner manual URL submission;
- owner manual file submission for lawfully possessed files, scans, downloaded/gated material, or sources without durable public URLs.

All paths converge on the same provenance, trust, rights, security, validation, and deduplication model. Manual material receives no automatic trust.

### 4.1.3 Source lifecycle

Corpus preserves source observations even when URLs move, die, redirect, or are mirrored, subject to stronger takedown/privacy/security deletion requirements. Default source revisit posture is:

- monthly for the most important official/current target pages;
- quarterly for other active high-value sources;
- semiannually for stable/lower-value sources;
- event/manual revisit where a known source change, rights issue, target-format change, or regression justifies it.

Different URLs are not different exams by default.

---

## 4.2 Canonical conceptual data model

The product model is deliberately independent of database/storage technology.

### 4.2.1 Core hierarchy

**Source Observation → Document → Exam / Test Set → Section → Part (optional) → Task → Item / Question → Answer / Scoring**

with **Instruction, Stimulus, Response Option, Explanation, Scoring Rule/Rubric, and Asset** as separately addressable supporting concepts.

The hierarchy expresses semantic responsibility, not page layout or provider vocabulary.

### 4.2.2 Entity responsibilities

| Concept | Product meaning |
|---|---|
| **Source Observation** | A place/context where material was seen or supplied: URL, archive snapshot, repository path, manual file, etc. Carries observation-specific provenance, access, claims and rights evidence. |
| **Document** | A concrete versioned content-bearing artifact such as booklet PDF, answer key, HTML task page, transcript, scoring guide or scan set. |
| **Exam / Test Set** | A coherent assessment package or exam-shaped set presented as belonging together. May be complete, partial or fragmentary. |
| **Section** | Functional normalized exam division such as Reading, Language Elements, Listening, Writing or Speaking, while preserving provider-native labels. |
| **Part** | Optional meaningful intermediate provider/task grouping. Never invented merely to fit one provider's hierarchy. |
| **Task** | Coherent activity with shared instructions/stimulus/response behavior. |
| **Item / Question** | Smallest response/scoring-addressable unit. Composite parents/children are allowed only when the source truly contains independently answerable/scorable subparts. |
| **Instruction** | Candidate directions about what to do. Kept separate from tested language for ordinary content-frequency analytics. |
| **Stimulus** | Tested input shared by one or more tasks/items: passage, short texts, audio/video segment, image, table, form, notice, advertisement, chart, speaking card, etc. |
| **Response Option** | Candidate answer/selection material, including shared option banks where applicable. |
| **Answer** | Source/reference answer assertion, accepted response, sample response or curated resolution. Learner answers belong to App, not Corpus. |
| **Explanation** | Source or curated explanatory evidence, kept distinguishable from tested source content. |
| **Scoring Rule / Rubric** | Point values, partial-credit/all-or-nothing behavior, cardinality, section totals, productive rubrics, conversions and provider-specific rules. |
| **Asset** | Addressable image, scan, audio, video, diagram, form, answer-sheet component or other media. |

### 4.2.3 Relationship rules

The model is not a strict tree:

- one Document may contribute to several Exams/Tasks;
- an Exam may be assembled from a booklet, separate key, scoring guide and audio assets;
- one Stimulus or Asset may be shared by many Items;
- one source observation may point to several Documents/Assets;
- many observations may point to the same underlying content;
- rights, confidence and quality can differ among components.

Shared Stimuli/Assets are represented once and linked, preventing duplicated text frequency, duplicated processing cost, and duplicated rights/removal work.

### 4.2.4 Completeness

Supported completeness states are conceptually:

- `complete`;
- `intentional_excerpt`;
- `incomplete_known_missing`;
- `completeness_unknown`.

Corpus separately tracks:

1. **source incompleteness** — the acquired source itself lacks expected material;
2. **extraction incompleteness** — the source contains material Corpus failed/not yet extracted;
3. **linking incompleteness** — components exist but their relationship is not verified.

Missing dependencies such as key, audio, transcript, page, rubric or asset remain explicit.

### 4.2.5 Provider-native semantics

Provider-native names, numbering, order, timing and special rules are preserved alongside canonical semantics. Provider-specific extensions are allowed only when a meaningful behavior cannot be represented generically. Extensions must not become mandatory dependencies for generic cross-provider analytics.

---

## 4.3 Authenticity, evidence confidence, and trust rules

### 4.3.1 Authenticity status

Authenticity is categorical and separate from evidence confidence:

| Status | Meaning |
|---|---|
| **Verified official** | Credibly established as issued/published by the claimed provider/authority |
| **Verified official-derived copy** | Non-officially hosted copy credibly matched to verified official underlying material |
| **Verified third-party / mock** | Authorship/origin reasonably established as non-official exam-prep material |
| **Claimed official — unverified** | Claims real/official origin without sufficient provenance proof |
| **Origin uncertain** | Corpus cannot responsibly establish official or third-party origin |
| **Suspected misrepresented / fake** | Evidence suggests material origin/exam identity may be materially false |

Similarity to official material can increase evidence confidence; it **cannot** by itself establish officiality.

### 4.3.2 Confidence dimensions

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

A provisional 0–100 score is the weighted achieved evidence over applicable maximum. `Unknown` contributes no positive evidence while remaining in the denominator; genuinely `Not applicable` dimensions are removed.

The number is an internal comparison/recalculation aid, not scientific precision.

### 4.3.3 Confidence tiers and analytical weights

| Tier | Initial band | Meaning | Default eligible aggregate weight |
|---|---:|---|---:|
| **A — Anchor** | 85–100 | Strongly defensible evidence, no unresolved critical integrity issue | 1.00 |
| **B — Trusted** | 70–84 | Reliable for most analytical/product-support uses | 0.70 |
| **C — Conditional** | 50–69 | Useful with meaningful uncertainty | 0.25 |
| **D — Weak** | 0–49 | Retain for provenance/discovery/review; no normal decision influence | 0.00 |
| **Quarantine** | separate state | Serious fake/tamper/integrity concern pending resolution | 0.00 |

Tier A requires established origin quality; claimed-official-unverified, origin-uncertain and suspected-fake material cannot become A. A verified third-party mock can become A if its evidence quality genuinely warrants it.

### 4.3.4 Trust granularity and hard gates

Confidence must be representable at **source, document, exam/test-set, task and item** scope. Local evidence can raise or lower a child relative to its parent.

Hard product gates include:

- suspected fake/tampered/misrepresented exam identity → quarantine until resolved;
- answer-key consistency 0–1 on objective material → block correctness-dependent use;
- expected key missing → allow appropriate structure/language/topic evidence but not correctness truth;
- local language quality 0–1 → cap/block affected language-content/generation use;
- severe structural inconsistency → block/cap whole-exam structure while salvageable local tasks may remain usable;
- claimed official but unverified → never label verified official or Tier A;
- unresolved high-impact conflict → mark disputed and withhold high-risk use rather than choose a side by score.

### 4.3.5 Use thresholds

- C+ may contribute bounded exploratory/aggregate context using confidence weights.
- **B+** is the default minimum for production difficulty influence, App learning-priority evidence, generation grounding and direct source exposure.
- Learning-priority changes normally require at least **two independent A/B underlying materials**.
- One verified official TELC source can establish that a target rule/format exists; it cannot establish prevalence by itself.
- Direct source exposure also requires rights permission, local QA/correctness eligibility and no unresolved dispute.

---

## 4.4 Rights and usage model

Rights are an independent downstream gate. Public accessibility, officiality, high confidence, target relevance, search-engine indexing or widespread mirroring do not grant reuse permission.

### 4.4.1 Operational usage statuses

| Status | Product posture |
|---|---|
| **REUSABLE** | Documented permission supports intended direct use, subject to exact action fields and trust/QA/product suitability |
| **REUSABLE_WITH_CONDITIONS** | Reuse is allowed only when attribution, non-commercial, share-alike, no-derivatives, territory, time, asset or other recorded obligations can be satisfied |
| **REFERENCE_ONLY** | May support allowed internal analysis/intelligence, but exact source expression and close/reconstructive derivatives are not approved for learner redistribution |
| **UNKNOWN_REVIEW_REQUIRED** | Rights evidence is insufficient/conflicting; conservative default blocks direct learner reuse, redistribution, close adaptation and commercial assumption |
| **PROHIBITED** | Active use is blocked because of explicit restriction, takedown, acquisition/policy problem or reviewed decision |

### 4.4.2 Authoritative action-level fields

The operational status is a human-friendly summary. Downstream authorization is controlled by action-specific decisions such as:

- redistribution permission;
- derivative/adaptation permission;
- commercial-use permission;
- attribution requirement and exact obligation;
- share-alike/no-derivatives/non-commercial conditions;
- source/asset-specific exclusions;
- private/classroom/internal-only scope;
- territory/channel/time restrictions;
- any custom condition materially affecting use.

### 4.4.3 Mixed rights

Rights can attach at source/material/component scope. A source-level license may seed descendants only when its scope genuinely covers them; a more specific local rule overrides inheritance.

For a composite learner-facing task, the **most restrictive required component governs**. Reusable text paired with restricted audio/image is not an unchanged reusable composite unless the component can be removed/replaced without misrepresenting the source experience.

### 4.4.4 Reference intelligence versus source expression

`REFERENCE_ONLY` and, where policy permits, `UNKNOWN_REVIEW_REQUIRED` material may still support non-reconstructive intelligence such as:

- canonical task structure;
- taxonomy tags and abstract skill relationships;
- difficulty/relevance evidence;
- aggregate prevalence;
- generation constraints/patterns that do not reproduce the source expression.

The normal App practice path therefore remains independently worded original content.

### 4.4.5 Takedown and reclassification

A credible takedown/serious rights concern creates an immediate hold on affected direct use, export, source-derived generation and normal reprocessing. Corpus must be able to:

- identify affected raw/reconstructive/source-specific outputs;
- suppress/delete them according to the decision;
- invalidate affected App/reference outputs;
- recompute analytics without the source or purge derived data if required;
- retain only the minimum non-content provenance/audit/prevention fingerprint allowed by policy;
- prevent accidental re-ingestion from mirrors.

Rights can move in either direction as evidence or product context changes. Every behavior-changing reclassification is audited and triggers downstream reevaluation.

---

## 4.5 Exam and skill taxonomy

### 4.5.1 Taxonomy shape

Corpus uses one **versioned multi-axis controlled graph**, not a single giant tree. Canonical families are:

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

The initial graph should remain maintainable for a personal project: prefer a low-hundreds core of strategically useful concepts over thousands of micro-skills.

### 4.5.2 Assignment semantics

Every assignment conceptually carries:

- stable canonical node ID;
- assignment role such as `primary_tested`, `secondary_tested`, `prerequisite_supporting`, `context`, `incidental_present`, or `distractor`;
- assignment confidence;
- origin/method: source-explicit, deterministic, human-curated, AI-suggested, benchmark-qualified auto-accepted, or migrated;
- supporting evidence/provenance;
- taxonomy version;
- review/provisional state.

A feature merely present in a passage is not automatically something the item deliberately tests.

### 4.5.3 Stable section and CEFR concepts

Normalized launch sections are Reading, Language Elements where the provider genuinely has that functional section, Listening, Writing and Speaking, plus integrated/other/unknown where needed.

CEFR supports `A2`, `B1`, `A2_B1_mixed`, incidental below-A2/above-B1 and `unknown`. Parent CEFR is context/prior, not automatic child truth. CEFR remains distinct from numerical difficulty.

### 4.5.4 Skills, strategy, reasoning and distractors stay separate

- **skill/competency** = capability demonstrated;
- **strategy** = behavior used to execute the exam effectively;
- **reasoning pattern** = logical/evidential operation required;
- **distractor pattern** = how a wrong option is made plausible.

The separation is necessary for diagnosis and original task generation.

### 4.5.5 Taxonomy versioning and learner-model safety

Stable node identity must not depend on display labels. Taxonomy releases can rename, reparent, merge, split, deprecate or retire nodes through explicit migrations.

Rules:

- rename keeps identity when meaning is unchanged;
- merge maps predecessor evidence to the successor with preserved provenance;
- split must **not** clone old learner mastery into every child; App lowers certainty or waits for new direct evidence according to the migration contract;
- reparenting changes graph organization without inventing learner evidence;
- deprecated/retired nodes retain history and successor guidance where applicable;
- App must know taxonomy version and migration semantics separately from the Corpus/App contract version.

High-impact fine taxonomy assignments may auto-publish only after the relevant benchmark slice reaches roughly **≥95% precision** with no systematic learner-diagnosis failure. Otherwise use a broader qualified parent, a provisional assignment or review.

---

## 4.6 Difficulty and TELC relevance

### 4.6.1 Separate concepts

Corpus maintains four distinct outputs:

1. CEFR target/context;
2. multidimensional task difficulty;
3. Generic-B1 relevance (`GB1`);
4. TELC-B1 relevance (`TELC`).

Each derived estimate also carries method/version and estimate uncertainty. Stage 03 confidence and Stage 09 independence separately determine how strongly the estimate can influence aggregates.

### 4.6.2 Difficulty profile

Applicable dimensions use a provisional 0–100 rubric:

- **L — Linguistic difficulty**;
- **R — Task/reasoning difficulty**;
- **T — Time-pressure difficulty**;
- **A — Audio difficulty**;
- **P — Productive-skill difficulty**.

Interpretation bands are very low 0–19, low 20–39, moderate 40–59, high 60–79, very high 80–100 within the A2/B1 Corpus domain. The scores are not pass/fail probabilities and do not convert directly to CEFR.

The dimension profile is authoritative. A composite may be used for ranking/coarse matching but must not erase the reason a task is hard.

### 4.6.3 Generic and target relevance

`GB1` answers how useful the evidence is for broad B1 exam competence. `TELC` answers how strongly it should influence claims specifically about TELC B1.

A high-quality Goethe/ÖSD item can be strong GB1 evidence with only moderate TELC relevance. A current TELC target pattern can be extremely TELC-relevant even if it is not broadly common elsewhere.

### 4.6.4 Evidence contribution

Decision-grade relevance/priority evidence conceptually combines:

**Independence × Stage-03 confidence weight × target alignment × currentness × scope fit**.

Safeguards:

- C-tier evidence is capped at about **15%** of effective evidence mass for published relevance/priority conclusions;
- when eligible official TELC evidence exists, third-party/unofficial material should normally be no more than about **35%** of effective support for a high-confidence TELC-specific conclusion;
- provider/source volume cannot overpower independent target evidence;
- missing/unknown dimensions do not become zero/easy.

### 4.6.5 Future empirical recalibration

Launch difficulty is a source/task estimate. Later, qualified aggregate learner-performance data may create a separate empirical calibration layer when App can provide privacy-safe, condition-aware, ability-aware evidence. Preserve estimated and empirical difficulty separately and blend only when the empirical evidence is sufficient.

Single-user struggle never becomes a global Corpus difficulty fact.
