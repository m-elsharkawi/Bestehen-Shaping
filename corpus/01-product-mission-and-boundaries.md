# Bestehen / Corpus — Stage 01: Product Mission and Boundaries

> **Status:** Authoritative Stage 01 product-shaping decision  
> **Product:** Bestehen / Corpus  
> **Initial domain:** German A2–B1 exam material  
> **Primary downstream customer:** Bestehen / App  
> **Target signal:** TELC B1 is strongest, while Corpus remains broader than TELC

## 1. Purpose and Scope

This document is the product charter for Bestehen / Corpus. It locks what Corpus is for, who it serves, what it collects initially, what it deliberately does not become, what makes the corpus useful, and which conceptual capabilities must eventually exist before the product can be considered complete.

It is a product-shaping document, not an architecture specification. Later stages may choose storage, crawling mechanisms, model providers, processing jobs, schemas, infrastructure, APIs, dashboards, and implementation technology. They should not need to reinvent the product mission or boundary captured here.

### 1.1 Authoritative one-sentence mission

**Bestehen / Corpus turns a broad, provenance-preserving collection of German A2–B1 exam material into trustworthy, rights-aware, deduplicated exam intelligence that Bestehen / App can use to decide what matters for TELC B1 learning, practice, and readiness.**

### 1.2 Product promise

**Corpus should tell Bestehen / App what A2/B1 German exams repeatedly test, how strongly the available evidence supports each conclusion, and how that intelligence may be used—without confusing public availability with permission to redistribute the source material.**

The promise is not “collect as many files as possible.” A smaller body of traceable, well-structured, correctly deduplicated evidence is more valuable than a much larger archive whose origin, trustworthiness, rights, or relationship to the target exam cannot be defended.

### 1.3 Product category

Bestehen / Corpus is an **exam-data and intelligence product**. It is not:

- a learner-facing exam-preparation application;
- a generic web scraper or download archive;
- a public exam-file mirror;
- an exercise bank whose purpose is to surface source questions directly to learners;
- a generic German-language corpus;
- a replacement for Bestehen / App's learner model, coaching engine, scoring, or readiness model.

Its job is to convert fragmented exam evidence into structured, trustworthy signals that downstream product decisions can use.

## 2. Inputs / Existing Decisions

Stage 01 preserves the following established decisions from the shared product overview, identity document, Corpus checklist, and App Stage 01 shaping output:

- Bestehen teaches German through exam preparation rather than completing a conventional language course first.
- Bestehen / Corpus is separate from Bestehen / App. Corpus builds the evidence base; App turns that evidence into learner-facing coaching.
- Bestehen / App launches around TELC B1 readiness and may support learners starting around A1.
- TELC B1 is the strongest target signal, but Corpus is intentionally broader than TELC so it can distinguish provider-specific behavior from general A2/B1 German exam patterns.
- Official and unofficial material may both contribute evidence when useful.
- Authenticity/confidence and usage rights are separate dimensions. Public accessibility does not imply redistribution permission.
- Real/reference exam material helps define what is tested. The App should usually practice those patterns using original content where direct reuse is inappropriate.
- Readiness is an evidence-backed App concept. Corpus supplies evidence and intelligence but does not itself decide whether an individual learner is ready to pass.
- Bestehen is a personal project initially. Monetary cost, maintenance burden, and recurring model usage are explicit constraints.
- App Stage 01 deliberately launches with TELC B1 as the only learner-facing target while preserving cheap conceptual seams for future exam targets. Corpus should support that strategy by remaining broad enough to produce generic A2/B1 evidence and TELC-specific relevance signals separately.

No earlier Corpus stage output exists before Stage 01, and the target file did not exist when this stage began.

## 3. Decisions and Rationale

### 3.1 Primary customer and downstream consumer

**Decision:** The primary customer of Bestehen / Corpus is **Bestehen / App**, not the end learner.

Corpus succeeds when the App can consume dependable intelligence to improve product behavior such as:

- which skills, task patterns, topics, grammar, vocabulary, distractors, and reasoning patterns deserve attention;
- which patterns appear broadly across A2/B1 exams versus disproportionately in TELC B1;
- how representative or trustworthy a piece of evidence is;
- how difficult and TELC-relevant a pattern appears to be;
- which source material may be reused, transformed, cited, or only analyzed as reference;
- which apparent frequency signals are actually duplicated mirrors rather than independent evidence;
- which exam structures and pattern combinations should ground original practice generation in the App.

There are two secondary internal users:

1. **The project owner/operator**, who needs to inspect sources, resolve uncertainty, correct metadata, review rights, and judge corpus health.
2. **Later design/architecture/analysis agents**, which need a stable product definition and structured evidence rather than an uncurated pile of files.

These are internal roles. They do not make Corpus a learner-facing product.

### 3.2 Relationship with Bestehen / App

**Decision:** Corpus owns **exam evidence and exam intelligence**; App owns **learner interaction, learner state, coaching, generated practice delivery, learner evaluation, and readiness interpretation**.

The boundary is deliberately asymmetric:

- Corpus may tell App that a task pattern is frequent, a grammar structure is highly relevant, a distractor pattern is characteristic of TELC, or an example source is high-confidence but reference-only.
- App decides whether a particular learner should practice that pattern today, how much assistance to provide, how to evaluate the response, how the result changes the learner model, and what it means for readiness.

Corpus must therefore expose enough context for App to make responsible choices without requiring App to rediscover provenance, trust, rights, duplication, or provider relevance itself.

**Boundary rule:** If a capability answers “What do these exams show?” it generally belongs in Corpus. If it answers “What should this learner do now, how did they perform, or are they ready?” it generally belongs in App.

### 3.3 Initial language and level scope

**Decision:** The initial Corpus domain is **German-language exam and exam-style material at CEFR A2 and B1, including mixed A2–B1 material**.

This scope is intentionally narrower than “all German learning content” and broader than “TELC B1 model tests.” It is wide enough to reveal progression, recurring exam patterns, provider differences, and cross-provider evidence while remaining directly relevant to the target product.

A1 is important to the learner journey but is **not an initial Corpus acquisition target**. The App may scaffold A2/B1-derived skills down to A1-accessible practice. Corpus does not need to become a general A1 content library to support an A1 learner.

If an otherwise relevant A2/B1 source contains incidental A1 material, Corpus may preserve and label it rather than discard the source, but that material does not count toward initial coverage goals.

### 3.4 Exam families explicitly in scope initially

**Decision:** All exam families listed in the Stage 01 checklist are explicitly in the initial Corpus scope, with different strategic roles rather than equal target weighting.

| Exam family / source family | Initial scope | Strategic role |
|---|---|---|
| **TELC B1** | In scope — highest priority | Primary target evidence for task shape, scoring-relevant behavior, difficulty, language, and TELC-specific relevance. |
| **TELC A2–B1** | In scope — high priority | Mixed-level evidence useful for A2→B1 progression and TELC-family continuity. |
| **Goethe B1** | In scope | Strong established-provider evidence for generic B1 language, skills, topics, and cross-provider comparison. |
| **Goethe A2** | In scope | Strong A2 evidence for progression and lower-difficulty exam-shaped patterns. |
| **ÖSD B1** | In scope | Established-provider B1 evidence that broadens German exam coverage and helps separate TELC-specific from general B1 patterns. |
| **ÖSD A2** | In scope | Established-provider A2 evidence for progression and comparison. |
| **DTZ A2–B1** | In scope | Valuable mixed-level evidence, especially for distinguishing broad A2/B1 competency patterns from provider-specific formats. |
| **Other credible A2/B1 exam-style material** | In scope with explicit confidence/rights treatment | Adds breadth where official material is sparse and surfaces recurring patterns from publishers, schools, teachers, archives, repositories, shared collections, and other credible sources. |

“In scope” does **not** mean “equally trusted,” “equally weighted,” or “safe to redistribute.” Later stages must classify source confidence, rights, TELC relevance, and analytical influence independently.

### 3.5 TELC B1 as strongest target signal

**Decision:** Corpus is broad, but **TELC B1 receives the strongest target weighting whenever the question is specifically about what Bestehen / App should prepare a learner to face on TELC B1**.

The broad corpus is used to answer two different questions:

1. **What is generally important for A2/B1 German exam performance?**
2. **What is specifically characteristic, frequent, difficult, or strategically important for TELC B1?**

Corpus must preserve the distinction. A pattern that is common across Goethe, ÖSD, and DTZ but absent from trusted TELC evidence should not automatically become a top TELC priority. Conversely, a strongly TELC-specific pattern can deserve high App priority even if it is uncommon elsewhere.

The exact numerical weighting model is deferred to Stage 07. Stage 01 locks only the product principle.

### 3.6 Current product posture: internal-first, intentionally reusable

**Decision:** Bestehen / Corpus is **internal-only in its initial product scope**, serving the owner/operator and Bestehen / App. It should nevertheless be shaped as a reusable data/intelligence product rather than as ad hoc scripts tied to one one-off import.

This means:

- a stable conceptual Corpus → App contract is a product requirement;
- provenance, rights, confidence, taxonomy, and versioned intelligence must be first-class concepts;
- source-specific quirks should not leak into every downstream consumer;
- future internal tools should be able to inspect and maintain the corpus without direct database surgery.

However, the following are **not initial product requirements**:

- a public Corpus website;
- a public search engine for source exams;
- a commercial data product;
- a customer-facing API;
- third-party developer access;
- multi-tenant accounts, billing, quotas, or public API guarantees;
- research-publication features.

A future API, research UI, or broader platform is optional. Later architecture should preserve reasonable seams where cheap, but should not pay meaningful complexity or operational cost for hypothetical external consumers before the internal product proves useful.

### 3.7 Explicit initial non-goals

Bestehen / Corpus intentionally does **not** initially try to cover:

| Non-goal | Boundary |
|---|---|
| German levels outside A2/B1 as acquisition targets | A1, B2, C1, C2, beginner course material, and advanced certification corpora are not initial coverage goals. Incidental material may be preserved and labeled. |
| Languages other than German | Multilingual instructions or translations embedded in a relevant source may be retained, but non-German exam ecosystems are not a product target. |
| Every German exam provider or every historical exam | Breadth is useful only when it contributes relevant, maintainable evidence. Coverage should be representative, not indiscriminate. |
| General German-learning content | Textbooks, vocabulary lists, grammar articles, videos, and exercises without meaningful exam relevance are not collected merely because they teach German. |
| A learner-facing exercise library | Corpus material is evidence first. App practice should primarily use original items grounded in corpus patterns unless rights clearly permit direct use and direct use is product-appropriate. |
| A public file mirror | Corpus does not exist to redistribute PDFs, audio, scans, or copyrighted material simply because they are publicly reachable. |
| Official certification or authoritative scoring | Corpus may model exam evidence but does not claim provider affiliation, official status, or guaranteed exam predictions. |
| Learner profiles and learner history | Corpus does not own personal learner state. Future aggregate, privacy-safe learner-performance signals may help recalibrate difficulty, but that is a later contract and does not turn Corpus into the learner data store. |
| Generic crawling as a success metric | Discovering pages is useful only when the material can become attributable, structured, quality-controlled exam evidence. |
| Perfect archival completeness | The product optimizes for useful intelligence, not exhaustive preservation of every mirror, edition, or web copy ever published. |

### 3.8 Success means useful intelligence, not raw document count

**Decision:** Corpus success is evaluated across **coverage, structural quality, trust, deduplication, analytical usefulness, downstream usefulness, and maintainability**. Raw document/item count is a secondary capacity metric.

#### Success dimension A — Representative coverage

A useful corpus contains enough independent evidence to characterize the target domain across:

- A2, B1, and mixed A2–B1 material;
- the explicitly in-scope exam families;
- reading, language elements where applicable, listening, writing, and speaking;
- major task families and common exam contexts;
- official, reputable educational, and appropriately handled unofficial evidence.

Coverage should be measured as a matrix of meaningful domain cells, not as one total file number. Later stages will define concrete coverage metrics and benchmark targets.

#### Success dimension B — Structural quality

Published Corpus data should represent the material faithfully enough that downstream analysis does not depend on repeatedly rereading raw files. Structure should correctly preserve the relationships among source, exam, section, task, item, answer, instruction, shared passage, audio/image asset, and scoring information where present.

The exact canonical model and extraction accuracy targets are deferred to Stages 05, 10, and 16.

#### Success dimension C — Trust and provenance

Every published analytical record must remain traceable to its origin. Trust must be explicit rather than implied by inclusion.

Product invariants:

- authenticity/confidence is represented separately from usage rights;
- unknown confidence remains unknown rather than silently upgraded;
- unknown rights remain unknown/review-required rather than treated as reusable;
- conclusions derived from lower-confidence evidence can be limited or discounted;
- the operator can understand why a source or item is trusted, uncertain, quarantined, or restricted.

Detailed scoring and thresholds are deferred to Stages 03 and 04.

#### Success dimension D — Deduplication integrity

Frequency analysis must count **independent evidence**, not mirrors and reposts.

A corpus fails this criterion if one leaked or mirrored mock exam appearing on many domains can materially distort conclusions about what is common. Exact duplicates, reformatted copies, near-duplicates, and derivative relationships must therefore be modeled well enough that analytics can choose the correct evidence unit.

Detailed duplicate rules are deferred to Stage 09.

#### Success dimension E — Actionable exam intelligence

The corpus must be able to produce conclusions useful to exam coaching, including eventually:

- recurring vocabulary/domain patterns;
- grammar patterns;
- topic patterns;
- task and section frequencies;
- tested skill patterns;
- distractor and reasoning patterns;
- A2→B1 progression signals;
- provider comparisons;
- TELC-specific versus generic-B1 distinctions;
- difficulty and TELC-relevance signals;
- relationships that can ground original exercise creation.

If Corpus can only answer “find me this document” but cannot answer “what does the evidence imply we should train?”, it is not product-complete.

#### Success dimension F — Downstream usefulness to Bestehen / App

Corpus is useful only if App can consume its intelligence without rebuilding Corpus logic.

At minimum, App should eventually be able to obtain:

- exam/task/skill patterns with enough context to practice them;
- frequency/prevalence signals with evidence quality attached;
- difficulty and TELC relevance with uncertainty attached;
- provenance/rights information when raw/reference material is involved;
- taxonomy relationships compatible with the learner model;
- signals that support original exercise generation without copying restricted source content.

The exact conceptual contract is deferred to Stage 12.

#### Success dimension G — Maintainable and financially sustainable operation

Corpus should be able to grow and improve without requiring expensive processing on every App interaction or manual inspection of every low-risk field.

A useful corpus can:

- precompute and cache stable intelligence;
- batch expensive enrichment;
- reprocess affected records when methods improve;
- route ambiguity to selective human/premium-model review;
- show corpus health and review backlog;
- preserve auditability when records change.

Concrete cost targets and scale assumptions are deferred to Stage 14.

### 3.9 What does not count as success

The following are not acceptable substitutes for the success model above:

- “We collected 10,000 PDFs.”
- “The scraper visited every result page.”
- “An LLM labeled every item.”
- “All sources are public on the internet.”
- “The database has no duplicate IDs.”
- “The App can search raw text.”

Each statement can be true while the corpus remains untrustworthy or strategically useless.

## 4. Detailed Product Model / Rules for This Stage

### Rule 1 — Evidence comes before content volume

Corpus should favor a source whose provenance, structure, trust, rights, and independence can be understood over a larger batch of opaque material whose analytical value cannot be defended.

This does not mean unofficial or messy sources are excluded. It means their uncertainty must survive ingestion rather than being erased.

### Rule 2 — Authenticity and usage rights never collapse into one score

A source can be:

- highly authentic and restricted from redistribution;
- unofficial but highly realistic and useful for analysis;
- legally reusable but poor evidence of real exam behavior;
- publicly reachable yet unknown in both authenticity and rights.

Corpus must preserve these combinations. Later systems may make different decisions based on each dimension.

### Rule 3 — Provider breadth exists to improve TELC decisions, not dilute them

Goethe, ÖSD, DTZ, publishers, schools, and unofficial collections can reveal broad language and exam patterns. TELC B1 still wins when deciding what is specifically important for the launch target.

### Rule 4 — A2/B1 breadth supports progression; A1 scaffolding belongs mainly in App

Corpus should understand the lower-to-upper transition within the A2/B1 domain. App can transform that intelligence into accessible A1-starting practice. Corpus should not expand into a full A1 teaching corpus merely because the learner begins around A1.

### Rule 5 — Raw/reference material and learner-practice material are different products

A high-value source item may be reference-only. Its role can still be to reveal exam structure, vocabulary, skills, distractors, or generation patterns. The App should not assume “present in Corpus” means “safe to show verbatim.”

### Rule 6 — Independent evidence is the unit that should influence frequency

Ten mirrors of one exam are one underlying exam event for most frequency purposes, not ten independent confirmations. Corpus must preserve every source reference while neutralizing mirror inflation.

### Rule 7 — Uncertainty is data

Unknown provider, mixed level, uncertain answer key, incomplete source, ambiguous rights, low-confidence extraction, or disputed classification should be represented explicitly. Uncertainty should trigger reduced influence, review, or quarantine rather than fabricated precision.

### Rule 8 — Corpus intelligence should be inspectable and explainable

For important conclusions, a later operator or consumer should be able to understand what evidence contributed, what was discounted, and why the conclusion carries its current confidence/relevance.

This is a product requirement for trust. The exact interface and storage are implementation decisions.

### Rule 9 — Corpus should not require per-learner or per-session intelligence generation

Stable exam intelligence should normally be generated offline, incrementally, or in batches, then reused by App. The Corpus value proposition is weakened if every learner interaction requires repeating expensive source analysis.

### Rule 10 — Future externalization is optional, not a launch constraint

Conceptual boundaries should be clean enough that a future internal or external API is possible. However, public-platform concerns must not increase initial complexity unless they directly improve the Corpus → App contract or maintainability.

## 5. Minimum Conceptual Capabilities for a Complete Corpus

The complete product may be implemented in phases, but Corpus is not conceptually complete until it can perform the following jobs.

| Capability | Product responsibility | Why it is necessary |
|---|---|---|
| **Source discovery and intake** | Accept broad relevant source material from multiple source categories and formats, through automated and manual paths. | Without broad intake, evidence remains too narrow or hand-curated to reveal patterns reliably. |
| **Permanent provenance** | Preserve where material came from, when it was observed, and relationships among mirrors/versions. | Trust, takedowns, rights, and analytical defensibility depend on traceability. |
| **Canonical exam representation** | Represent supported exams, sections, tasks, items, answers, instructions, shared passages, scoring information, and media relationships without forcing everything into a TELC-only shape. | Analytics and App consumption require structured evidence rather than file-specific parsing. |
| **Authenticity/confidence model** | Assess how strongly each source/document/exam/task/item should be trusted for relevant conclusions, with uncertainty and review states. | Unofficial breadth is useful only if low-quality material cannot silently dominate. |
| **Rights/usage model** | Track what can be analyzed, reused, transformed, attributed, surfaced, or must remain restricted/unknown. | Public accessibility is not permission; App behavior depends on this distinction. |
| **Exam/skill taxonomy** | Connect items to provider, CEFR, section, task type, topic, grammar, vocabulary/domain, receptive/productive skills, strategy/reasoning, and distractor concepts. | This is the bridge from corpus evidence to learner modeling and targeted practice. |
| **Difficulty and TELC relevance** | Separate general linguistic/task difficulty from relevance to the launch exam and represent uncertainty. | App needs to know not only what exists but what matters and how challenging it is. |
| **Ingestion/enrichment lifecycle** | Turn raw material into validated structured data with predictable states, partial-failure handling, reprocessing, and review. | Corpus cannot depend on one-off manual transformation. |
| **Deduplication and evidence independence** | Detect exact/near duplicates and derivatives, choose canonical records, preserve source references, and prevent mirror inflation. | Frequency and corroboration are otherwise misleading. |
| **Validation and QA** | Validate structure, answers, assets, metadata, extraction, and corpus quality against a manually annotated benchmark. | Scale is unsafe without measurable quality. |
| **Corpus analytics** | Produce frequencies, comparisons, progression signals, skill relationships, distractor/reasoning patterns, and TELC-vs-generic-B1 intelligence. | This is what makes Corpus an intelligence product rather than an archive. |
| **Stable Corpus → App contract** | Provide raw/reference content where permitted, structured metadata, aggregate statistics, skill relationships, generation patterns, difficulty/relevance, provenance, rights, and versioning behavior. | App should not need to know Corpus internals to use trustworthy evidence. |
| **Operations and auditability** | Support review queues, corrections, reprocessing, source controls, audit history, and corpus health visibility. | A broad imperfect corpus needs maintainability without database surgery. |
| **Cost/scale controls** | Use cheap/deterministic processing where adequate, cache and batch stable work, selectively invoke expensive review, and measure processing cost. | The project must remain viable as a personal project. |
| **Security/abuse boundaries** | Handle untrusted files/URLs, permissions, retention, and submissions safely while keeping learner data outside Corpus ownership. | Broad source intake creates operational risk even for an internal product. |
| **Benchmark corpus and regression baseline** | Maintain a representative manually annotated seed set spanning providers, levels, sections, formats, and imperfect sources. | Later architecture and model changes need a defensible test target. |

These are conceptual capabilities, not a mandate to implement each as a separate service, tool, database, or model.

## 6. Edge Cases / Failure or Uncertainty Handling

### 6.1 Official source with unclear or restrictive reuse rights

Treat it as potentially high-confidence evidence while keeping raw content restricted or reference-only according to the rights model. High authenticity never overrides rights restrictions.

### 6.2 Unofficial source that closely resembles real exam material

It may enter the corpus as evidence if credible enough, but must retain lower/uncertain provenance and appropriately bounded analytical influence until confidence is established. Unknown rights must not become reusable rights by assumption.

### 6.3 Publicly available PDF with no license statement

Public accessibility may justify discovery and reference analysis where appropriate, but does not by itself grant redistribution or derivative-use permission. Mark rights as unknown/review-required until Stage 04 rules resolve the operational status.

### 6.4 One exam mirrored across many sites

Preserve the alternate source URLs for provenance and resilience, but do not allow mirror count to inflate exam frequency or corroboration. Stage 09 will define the detailed independence rules.

### 6.5 Same task rewritten or lightly reformatted

Do not force a binary duplicate/not-duplicate conclusion when the relationship is uncertain. Corpus should support exact duplicate, near-duplicate/derivative, and independent evidence concepts so analytics can apply the appropriate treatment.

### 6.6 Incomplete exam or missing answer key

Incomplete material can remain useful if its available structure or content contributes evidence. It must be labeled as incomplete and its missing answer/scoring evidence must reduce or prevent use in analyses that depend on correctness. Do not invent absent answers to make the record look complete.

### 6.7 Conflicting answer keys

Preserve the conflict rather than selecting an answer silently. Downstream influence should be reduced or blocked until validation/review resolves the issue. Detailed conflict handling belongs to Stages 03, 08, and 10.

### 6.8 Mixed A2–B1 material

Represent the mixed-level status instead of forcing one CEFR label onto the entire source. Task/item-level evidence may later allow more precise classification. Mixed-level material is explicitly valuable for progression analysis.

### 6.9 A1 content encountered during collection

If embedded in a relevant A2/B1 source, preserve and label it when useful for provenance or structure. Do not broaden discovery goals or corpus success metrics around A1 during the initial product scope.

### 6.10 Material above B1 encountered in a relevant source

Preserve necessary source context, but exclude higher-level content from A2/B1 analytics unless a later stage explicitly defines a justified use. Do not let incidental B2+ material distort difficulty or frequency conclusions.

### 6.11 Source disappears or is later reclassified

Corpus must retain enough provenance and audit history to understand what happened and prevent unsafe downstream use. Exact takedown behavior, retention of derived metadata, and contract effects are deferred to Stages 04 and 12.

### 6.12 Evidence is too weak to classify responsibly

Keep the material in a review/quarantine state or limit its influence. “Unknown” is preferable to false precision. A source does not earn analytical influence merely because ingestion succeeded technically.

### 6.13 App asks for material that is analytically useful but not reusable

Corpus should return the intelligence/pattern metadata allowed by the rights model and make the restriction visible. App should generate or select an original equivalent rather than expose restricted source content.

### 6.14 Future request for a public API or Corpus UI

Treat it as a new product expansion. Reuse the internal conceptual contract where possible, but do not assume internal trust, rights, operational, security, or SLA rules automatically satisfy an external product.

## 7. Relationship to Other Bestehen Stages

Stage 01 is the boundary and decision filter for all later Corpus shaping:

- **Stage 02 — Source Strategy:** must collect broadly enough to satisfy the A2/B1 and provider scope without drifting into generic scraping.
- **Stage 03 — Authenticity and Confidence:** must make unofficial evidence usable without equating all sources or erasing uncertainty.
- **Stage 04 — Rights and Usage Metadata:** must independently control reuse/surfacing regardless of confidence.
- **Stage 05 — Canonical Exam Model:** must support the broad provider set without a TELC-only schema.
- **Stage 06 — Exam and Skill Taxonomy:** must create the shared conceptual bridge to App's learner model.
- **Stage 07 — Difficulty and TELC Relevance:** must explicitly distinguish generic A2/B1 importance from TELC B1 importance.
- **Stage 08 — Ingestion Pipeline:** must preserve provenance, uncertainty, partial data, review states, and traceability from raw source to published intelligence.
- **Stage 09 — Deduplication:** must protect frequency and corroboration from mirror inflation.
- **Stage 10 — Validation and QA:** must define measurable quality rather than assuming successful extraction equals correct data.
- **Stage 11 — Corpus Analytics:** must produce actionable coaching intelligence, not just searchable records.
- **Stage 12 — Corpus → App Contract:** must formalize the boundary locked here, including rights-aware/reference-aware consumption.
- **Stage 13 — Corpus Operations:** must make the internal-first product maintainable without direct database surgery.
- **Stage 14 — Cost, Scale, and Automation:** must establish sustainable processing targets consistent with a personal-project budget.
- **Stage 15 — Security and Abuse:** must harden broad source intake and confirm learner/personal data remains outside Corpus ownership unless a later privacy-safe aggregate feedback path is deliberately added.
- **Stage 16 — Initial Benchmark Corpus:** must prove the product can represent the agreed provider/level/format range and measure extraction/taxonomy/dedup/confidence/rights quality.
- **Stage 17 — Final Product Specification:** must reconcile all later detailed decisions back to this mission and scope.

### Relationship to Bestehen / App

The App's TELC B1 launch focus and Corpus's broader evidence scope are complementary rather than contradictory:

- Corpus gathers enough cross-provider evidence to understand generic A2/B1 exam patterns and progression.
- Corpus separately models TELC relevance so generic breadth does not dilute target specificity.
- App uses TELC B1 as the learner-facing target and turns Corpus intelligence into recommendations, original practice, evaluation context, and readiness evidence.
- Corpus does not determine an individual learner's readiness or own their personal learning history.

## 8. Cost Notes

Stage 01 creates an important cost boundary even though exact budgets belong to Stage 14.

### Preferred low-cost default

Corpus should be designed around **offline/incremental preprocessing and reusable intelligence**, not expensive model calls during each learner session.

Preferred product principles:

- deterministic extraction/validation where it is sufficiently reliable;
- hash/fingerprint/similarity techniques before semantic-model dedup where practical;
- cheap or local/open-source processing for broad first-pass classification where quality is adequate;
- cached and versioned enrichment so unchanged material is not repeatedly reprocessed;
- batching of model work instead of one premium call per item;
- human review for high-impact ambiguity rather than blanket manual review;
- higher-quality model calls only when uncertainty materially affects trust, rights-adjacent review support, difficult extraction, taxonomy quality, or high-value TELC evidence.

### What would justify higher recurring spend

More expensive processing is justified when benchmark evidence shows that the cheaper path causes meaningful errors in conclusions the App relies on—for example, mis-parsed answer keys, incorrect task structure, poor skill classification, or false duplicate independence that changes frequency signals.

The upgrade rule is therefore **measured quality improvement on high-value corpus decisions**, not “use the best model everywhere.”

Exact source volumes, item volumes, per-1,000-item cost targets, retry limits, and model tiers are explicitly deferred to Stage 14.

## 9. Decisions Made

1. Bestehen / Corpus is an **exam-data and intelligence product**, not a learner product or generic scraper.
2. Its one-sentence mission is to turn broad German A2/B1 exam material into trustworthy, rights-aware, deduplicated intelligence for Bestehen / App.
3. The **primary customer is Bestehen / App**; the owner/operator is the secondary internal user.
4. The initial domain is **German A2, B1, and mixed A2–B1 exam material**.
5. **TELC B1 is the strongest target signal**, while cross-provider breadth is deliberately preserved.
6. Initial in-scope families are TELC B1, TELC A2–B1, Goethe B1, Goethe A2, ÖSD B1, ÖSD A2, DTZ A2–B1, and other credible A2/B1 exam-style material.
7. A1 is not an initial acquisition target; App owns adapting exam-led learning to an A1-starting learner.
8. Corpus is **internal-first but intentionally reusable**. A public API/UI is future optionality, not launch scope.
9. Corpus success is defined by representative coverage, structural quality, trust/provenance, deduplication integrity, actionable intelligence, App usefulness, and sustainable maintenance—not raw document count.
10. Corpus must eventually cover the complete conceptual capability set from source intake through benchmarked QA, analytics, App contract, operations, cost controls, and security boundaries.
11. Corpus does not own learner profiles, coaching decisions, or individual readiness.
12. Stable exam intelligence should normally be precomputed/reused so Corpus does not impose per-learner AI processing cost.

## 10. Open Questions / Deferred Decisions

### Owner questions

**None.** The available context is sufficient to make Stage 01 product decisions without an owner preference blocking completion.

### Deliberately deferred product-detail decisions

These are not Stage 01 blockers because later dedicated stages exist for them:

- exact source categories, discovery methods, supported input formats, freshness, and mirror/dead-URL behavior — **Stage 02**;
- confidence dimensions, source tiers, granularity, and influence thresholds — **Stage 03**;
- concrete rights statuses, takedown rules, and derived-metadata retention — **Stage 04**;
- canonical entity hierarchy and task/asset/scoring representation — **Stage 05**;
- taxonomy contents, curated-vs-discovered boundaries, and taxonomy versioning — **Stage 06**;
- numerical difficulty/TELC relevance models and provider weighting — **Stage 07**;
- ingestion states, review thresholds, OCR/transcription/alignment, and reprocessing — **Stage 08**;
- duplicate/derivative thresholds and canonical-record selection — **Stage 09**;
- QA metrics, production-ready thresholds, and gold-standard accuracy requirements — **Stage 10**;
- analytical outputs and low-quality-source protections — **Stage 11**;
- exact Corpus → App request/response contract and versioning — **Stage 12**;
- internal operations UI requirements — **Stage 13**;
- volume targets, processing budgets, model tiers, and cost per 1,000 items — **Stage 14**;
- detailed file/URL security and retention controls — **Stage 15**;
- exact seed benchmark and accuracy targets — **Stage 16**.

### Architecture/implementation decisions intentionally not made here

Storage technology, schema implementation, services, queues, crawlers, vector databases, embedding models, model vendors, hosting, API protocol, dashboard framework, job orchestration, and deployment architecture remain explicitly open. Later architecture should implement the product requirements rather than reinterpret them.

## 11. Definition of Done Check

- [x] A concise one-sentence mission for Bestehen / Corpus is locked.
- [x] The primary customer is explicitly Bestehen / App, not end learners.
- [x] The initial domain is German A2–B1 exam material, including mixed A2–B1 sources.
- [x] TELC B1 is explicitly the strongest target signal while Corpus remains broader than TELC.
- [x] TELC B1 is explicitly in scope initially.
- [x] TELC A2–B1 is explicitly in scope initially.
- [x] Goethe B1 is explicitly in scope initially.
- [x] Goethe A2 is explicitly in scope initially.
- [x] ÖSD B1 is explicitly in scope initially.
- [x] ÖSD A2 is explicitly in scope initially.
- [x] DTZ A2–B1 is explicitly in scope initially.
- [x] Other credible A2/B1 exam-style material is explicitly in scope initially.
- [x] Initial non-goals and out-of-scope areas are explicit.
- [x] Corpus is locked as internal-first with reusable product boundaries and future API/UI optionality.
- [x] Useful-corpus success criteria are defined beyond raw document count.
- [x] Minimum conceptual capabilities required for a complete Corpus are listed.
- [x] Cost-sensitive product principles and cheaper defaults are documented.
- [x] No Stage 01 owner question remains unresolved.

**Stage 01 is product-complete when the live Corpus checklist matches the decisions above.**
