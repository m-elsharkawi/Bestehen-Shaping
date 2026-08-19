# Bestehen / Corpus — Product Shaping Checklist

> **Purpose:** Fully shape **Bestehen / Corpus** before architecture and implementation planning.
>
> **End state:** We know exactly what the Corpus gathers, how sources are evaluated, how exam material becomes structured intelligence, how quality is measured, and what Bestehen / App can reliably consume.

---

## 1. Lock the Product Mission and Boundaries

- [x] Finalize the one-sentence mission for Bestehen / Corpus.
- [x] Confirm that its primary customer is **Bestehen / App**, not end learners.
- [x] Confirm the initial domain: German **A2–B1 exam material**.
- [x] Confirm that TELC B1 is the strongest target signal, while the corpus is broader than TELC.
- [x] Decide which exam families are explicitly in scope at launch:
  - [x] TELC B1
  - [x] TELC A2–B1
  - [x] Goethe B1
  - [x] Goethe A2
  - [x] ÖSD B1
  - [x] ÖSD A2
  - [x] DTZ A2–B1
  - [x] Other credible A2/B1 exam-style material
- [x] Define what is explicitly out of scope initially.
- [x] Decide whether Corpus is internal-only or intentionally designed as a reusable platform/API later.
- [x] Define success criteria for a **useful corpus**, not merely a large corpus.

**Done when:** The scope is clear enough that an architecture agent does not need to decide what the product is.

---

## 2. Define the Source Strategy

- [x] Define source categories:
  - [x] official exam providers,
  - [x] established educational publishers,
  - [x] language schools and teachers,
  - [x] public repositories and archives,
  - [x] unofficial exam collections,
  - [x] forums/shared documents,
  - [x] individual exam-style exercises.
- [x] Define how sources are discovered for each category.
- [x] Decide which input formats are supported:
  - [x] HTML
  - [x] PDF
  - [x] DOC/DOCX
  - [x] images/scans
  - [x] audio
  - [x] video
  - [x] ZIP/archive files
- [x] Support both automated discovery/crawling and manual URL/file submission.
- [x] Define source revisit/freshness rules.
- [x] Define handling for mirrors and alternate URLs.
- [x] Define handling for dead or removed URLs.
- [x] Preserve source provenance permanently.

**Done when:** We can explain where content comes from, how it enters the system, and how its origin remains traceable.

---

## 3. Define Authenticity and Confidence

- [x] Create a confidence model independent of usage rights.
- [x] Define confidence dimensions:
  - [x] provider reputation,
  - [x] similarity to known exam structure,
  - [x] language quality,
  - [x] answer-key presence,
  - [x] answer-key consistency,
  - [x] similarity to trusted material,
  - [x] internal structural consistency,
  - [x] corroboration across independent sources.
- [x] Define source tiers, e.g. A/B/C/D.
- [x] Decide whether confidence exists at source, document, exam, task, and/or item level.
- [x] Define thresholds for:
  - [x] inclusion in corpus analytics,
  - [x] influence on difficulty models,
  - [x] influence on learning priorities,
  - [x] direct surfacing in Bestehen / App.
- [x] Define manual-review flow for uncertain but valuable material.
- [x] Define handling of conflicting answer keys.
- [x] Define quarantine behavior for likely fake or malformed exams.

**Done when:** Unofficial material can add breadth without being treated as equally trustworthy as official material.

---

## 4. Define Rights and Usage Metadata

- [x] Create a rights/usage classification separate from authenticity.
- [x] Track:
  - [x] public accessibility,
  - [x] known license,
  - [x] redistribution permission,
  - [x] derivative-use permission,
  - [x] attribution requirements,
  - [x] commercial-use restrictions,
  - [x] review status,
  - [x] source terms/notes.
- [x] Define operational statuses such as:
  - [x] reusable,
  - [x] analysis/reference only,
  - [x] unknown/review required,
  - [x] prohibited.
- [x] Define what downstream systems may do with each status.
- [x] Define takedown/removal behavior.
- [x] Decide what happens to already-derived metadata when a source is removed.

**Done when:** The system can learn from broad material without assuming that publicly accessible means freely redistributable.

---

## 5. Define the Canonical Exam Model

- [x] Define the hierarchy from source to item, e.g.:
  - [x] Source
  - [x] Document
  - [x] Exam/Test Set
  - [x] Section
  - [x] Part
  - [x] Task
  - [x] Question/Item
  - [x] Answer
  - [x] Explanation
  - [x] Asset
- [x] Define multi-part questions.
- [x] Define shared reading/listening passages.
- [x] Define audio-to-question mapping.
- [x] Define images, tables, forms, notices, and advertisements.
- [x] Define matching and multiple-correct-answer tasks.
- [x] Separate instructions from tested content.
- [x] Represent answer keys and scoring rules.
- [x] Represent incomplete exams honestly.

**Done when:** Any supported A2/B1 exam can be represented without forcing it into a TELC-only schema.

---

## 6. Build the Exam and Skill Taxonomy

- [x] Define exam-provider metadata.
- [x] Define CEFR and mixed-level handling.
- [x] Define section taxonomy:
  - [x] Reading
  - [x] Language Elements / Sprachbausteine
  - [x] Listening
  - [x] Writing
  - [x] Speaking
- [x] Define task-type taxonomy.
- [x] Define topic taxonomy.
- [x] Define grammar taxonomy.
- [x] Define vocabulary/domain taxonomy.
- [x] Define reading skill taxonomy.
- [x] Define listening skill taxonomy.
- [x] Define writing competency taxonomy.
- [x] Define speaking competency taxonomy.
- [x] Define exam-strategy/reasoning-pattern taxonomy.
- [x] Define distractor-pattern taxonomy.
- [x] Define relationships between taxonomy nodes.
- [x] Decide what is curated vs AI-discovered.
- [x] Define taxonomy versioning.

**Done when:** Corpus items can connect to the same skill graph Bestehen / App will use for learner modeling.

---

## 7. Define Difficulty and TELC Relevance

- [x] Define linguistic difficulty.
- [x] Define task/reasoning difficulty.
- [x] Define time-pressure difficulty.
- [x] Define audio difficulty.
- [x] Define production difficulty for writing/speaking.
- [x] Separate CEFR level from numerical difficulty.
- [x] Define TELC relevance separately from generic B1 relevance.
- [x] Define provider/source weighting principles.
- [x] Limit how strongly low-confidence material affects aggregate insights.
- [x] Represent uncertainty in AI-estimated difficulty.
- [x] Plan for future recalibration using real learner performance.

**Done when:** The corpus can say not only “this is B1,” but how hard it is, why, and how relevant it is to TELC B1.

---

## 8. Define the Ingestion Pipeline

- [ ] Define the conceptual pipeline:
  - [ ] discover,
  - [ ] fetch,
  - [ ] normalize,
  - [ ] parse,
  - [ ] segment,
  - [ ] classify,
  - [ ] extract answers,
  - [ ] extract assets,
  - [ ] enrich,
  - [ ] validate,
  - [ ] deduplicate,
  - [ ] review,
  - [ ] publish.
- [ ] Define partial-failure handling.
- [ ] Define human-review checkpoints.
- [ ] Define auto-accept vs review thresholds.
- [ ] Define scanned-document handling.
- [ ] Define audio transcription/alignment.
- [ ] Define answer-key linking.
- [ ] Make AI-generated metadata traceable.
- [ ] Define reprocessing when models improve.

**Done when:** Every source has a predictable path from raw material to trusted structured data.

---

## 9. Define Duplicate and Near-Duplicate Detection

- [ ] Define document fingerprinting.
- [ ] Define question/item similarity detection.
- [ ] Define text normalization before comparison.
- [ ] Define duplicate image/scan handling.
- [ ] Define duplicate audio handling.
- [ ] Detect reformatted/mirrored copies.
- [ ] Define canonical-record selection.
- [ ] Preserve all known source references after deduplication.
- [ ] Ensure frequency analytics count independent evidence, not mirrors.
- [ ] Define exact-duplicate vs derivative thresholds.

**Done when:** “Seen 20 times online” cannot be mistaken for “seen in 20 independent exams.”

---

## 10. Define Validation and QA

- [ ] Define exam-structure validation.
- [ ] Define answer-key validation.
- [ ] Define language-quality checks.
- [ ] Define metadata completeness checks.
- [ ] Define broken-asset checks.
- [ ] Define audio-question alignment checks.
- [ ] Define cross-checking for AI extraction.
- [ ] Define manual QA sampling.
- [ ] Define corpus quality metrics.
- [ ] Define “production-ready corpus data.”
- [ ] Build a manually annotated gold-standard dataset.
- [ ] Define regression tests against it.

**Done when:** Corpus growth is measured by both quantity and quality.

---

## 11. Define Corpus Analytics

- [ ] Define vocabulary-frequency analysis.
- [ ] Define grammar-frequency analysis.
- [ ] Define topic-frequency analysis.
- [ ] Define task-type frequency.
- [ ] Define skill-frequency analysis.
- [ ] Define provider comparisons.
- [ ] Define A2 → B1 progression analysis.
- [ ] Define TELC-vs-generic-B1 comparisons.
- [ ] Define distractor/reasoning-pattern analysis.
- [ ] Define co-occurrence analysis across skills, topics, grammar, and tasks.
- [ ] Decide which outputs directly influence Bestehen / App.
- [ ] Protect aggregate results from low-quality-source distortion.

**Done when:** The corpus produces actionable learning intelligence, not merely a searchable archive.

---

## 12. Define the Contract with Bestehen / App

- [ ] List every type of information the App needs from Corpus.
- [ ] Separate:
  - [ ] raw/reference content,
  - [ ] structured metadata,
  - [ ] aggregate statistics,
  - [ ] skill relationships,
  - [ ] exercise-generation patterns,
  - [ ] difficulty/relevance signals.
- [ ] Define how the App requests suitable exam patterns.
- [ ] Define how Corpus distinguishes A1-assisted, A2, A2/B1, and B1 use cases.
- [ ] Define how generated exercises remain grounded in corpus patterns without copying source material.
- [ ] Return provenance/attribution metadata where required.
- [ ] Define versioning of the Corpus → App contract.
- [ ] Define behavior when a source is reclassified or removed.

**Done when:** Bestehen / App can be designed against a stable conceptual interface.

---

## 13. Define Corpus Operations

- [ ] Decide whether an internal operations dashboard is required.
- [ ] Define views for:
  - [ ] discovery queue,
  - [ ] ingestion status,
  - [ ] extraction failures,
  - [ ] duplicate review,
  - [ ] authenticity review,
  - [ ] rights review,
  - [ ] low-confidence items,
  - [ ] taxonomy corrections.
- [ ] Define manual-edit capabilities.
- [ ] Define audit history.
- [ ] Define source allow/block lists.
- [ ] Define reprocessing controls.
- [ ] Define corpus health metrics.

**Done when:** The corpus can be maintained without direct database surgery.

---

## 14. Define Cost, Scale, and Automation Principles

- [ ] Estimate source/document/question volume targets.
- [ ] Estimate AI processing needs by source type.
- [ ] Decide which steps require higher-quality models.
- [ ] Decide which steps should use deterministic/cheap processing.
- [ ] Define batching and caching principles.
- [ ] Define retry/failure limits.
- [ ] Define crawling etiquette and rate-limit principles.
- [ ] Define raw-file/media storage expectations.
- [ ] Set a target processing cost per 1,000 items.
- [ ] Define where human review is worth the cost.

**Done when:** The concept is economically viable at the desired corpus size.

---

## 15. Define Security and Abuse Boundaries

- [ ] Confirm whether Corpus stores any learner/personal data.
- [ ] Define safe handling of untrusted files.
- [ ] Define URL/content sanitization.
- [ ] Define domain blocking rules.
- [ ] Define secret/access requirements.
- [ ] Define permissions for internal tooling.
- [ ] Define raw-file retention rules.
- [ ] Define abuse handling for manually submitted sources.

**Done when:** Non-functional boundaries are clear before architecture begins.

---

## 16. Establish the Initial Benchmark Corpus

- [ ] Select a representative seed set across providers and source tiers.
- [ ] Include both A2 and B1.
- [ ] Include all major exam sections.
- [ ] Include HTML, PDF, audio, and at least one imperfect unofficial source.
- [ ] Manually annotate a benchmark subset.
- [ ] Define target extraction accuracy.
- [ ] Define target taxonomy accuracy.
- [ ] Define target deduplication accuracy.
- [ ] Define expected authenticity classification.
- [ ] Define expected rights classification.

**Done when:** Architecture and implementation can later be tested against a concrete gold-standard dataset.

---

## 17. Produce the Final Product Specification

- [ ] Write the final Bestehen / Corpus PRD.
- [ ] Document the canonical data model conceptually.
- [ ] Document source tiers and confidence rules.
- [ ] Document rights/usage classifications.
- [ ] Document taxonomy and versioning.
- [ ] Document ingestion and review states.
- [ ] Document deduplication behavior.
- [ ] Document Corpus → App responsibilities.
- [ ] Document analytics outputs.
- [ ] Document quality metrics.
- [ ] Document explicitly deferred features.
- [ ] Separate unresolved architecture questions from unresolved product questions.

### Bestehen / Corpus is fully shaped when:

- [ ] We know **what to collect**.
- [ ] We know **where to collect it from**.
- [ ] We know **how to judge trustworthiness**.
- [ ] We treat **usage rights independently from authenticity**.
- [ ] We know **how every exam becomes structured data**.
- [ ] We have a stable **exam/skill taxonomy**.
- [ ] We know **how duplicates are neutralized**.
- [ ] We know **how difficulty and TELC relevance are estimated**.
- [ ] We know **what analytics the corpus must produce**.
- [ ] We know **exactly what Bestehen / App consumes**.
- [ ] We have a **gold-standard benchmark dataset**.
- [ ] No major product decision needs to be invented by the architecture agent.