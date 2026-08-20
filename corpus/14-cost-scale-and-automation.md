# Bestehen / Corpus — Stage 14: Cost, Scale, and Automation Principles

> **Status:** Authoritative Stage 14 product-shaping decision  
> **Product:** Bestehen / Corpus  
> **Primary operator:** One owner in the personal-project phase  
> **Primary downstream customer:** Bestehen / App  
> **Core principle:** Corpus grows by information value, not by crawl volume. Cheap deterministic/local processing is the default; paid AI, expensive media processing, and human review are selective escalations whose cost must be measurable, bounded, cached, and justified by a material product outcome.

---

## 1. Purpose and Scope

Stage 14 defines the economic and scale envelope within which Bestehen / Corpus should grow. Earlier stages deliberately established a rich product model—broad source discovery, multi-format extraction, confidence and rights handling, deduplication, semantic taxonomy, difficulty/relevance, QA, analytics, an App contract, and owner review—but repeatedly deferred the concrete questions of **how much material is plausible, how much automated processing is justified, how retries are bounded, how crawling behaves, what raw media is worth retaining, and what spend should stop further processing**.

This stage resolves those questions for the personal-project phase.

The objective is not to make Corpus free at all costs and not to optimize prematurely for millions of documents. The objective is to make a useful A2/B1 evidence product that can reach tens of thousands of canonical exam Items at a predictable personal-project cost, while preserving a path to a larger corpus if measured product value justifies it.

### 1.1 Stage objective

**Bestehen / Corpus should be able to grow from a benchmark-sized seed to a useful tens-of-thousands-of-items evidence base while keeping routine Corpus-specific cash spend around a small personal-project budget, owner review bounded, and every expensive operation attributable to a clear coverage, quality, correctness, or TELC-intelligence benefit.**

### 1.2 What this stage decides

This stage decides:

- low/base/high planning volumes for source families, observations, documents, Tasks, Items, audio, and storage;
- which source types normally need deterministic processing, OCR/ASR, semantic models, stronger models, or human review;
- the cheap-first processing ladder and escalation rules;
- batching, caching, reuse, deferred-processing, and reprocessing principles;
- concrete retry/failure limits;
- respectful crawl/rate-limit guardrails;
- raw/media storage expectations and capacity triggers;
- a provider-independent cost-accounting model;
- a target paid processing cost per 1,000 canonical Items;
- monthly budget alerts/caps and one-off backfill limits;
- when higher-quality models, more infrastructure, or more automation are justified;
- where human review is worth its time cost.

### 1.3 What this stage does not decide

This stage does **not** choose:

- a cloud, OCR, ASR, embedding, or LLM vendor;
- model names or hardware;
- crawler, queue, scheduler, database, object store, workflow engine, or cache implementation;
- exact physical data layout;
- legal raw-retention periods or deletion obligations—Stage 15 owns the final security/retention policy;
- the exact Stage 16 benchmark source set;
- how Bestehen / App pays for its own learner-facing generation/evaluation. Stage 14 concerns Corpus costs.

The numerical thresholds below are **initial product guardrails**, not claims that future empirical cost will match them exactly. They must be recalibrated from real Corpus cost logs without weakening the cheap-first and impact-based principles.

---

## 2. Inputs / Existing Decisions

Stage 14 preserves the shared Product Overview, Identity, both live shaping checklists, and Corpus Stages 01–13.

### 2.1 Mission, source strategy, and scope

Stages 01–02 established that Corpus is an internal-first A2/B1 exam-data and intelligence product, that TELC B1 is the strongest target signal while acquisition remains cross-provider, that official and unofficial evidence may both contribute, and that discovery is **coverage-driven rather than URL-count-driven**.

Stage 02 already requires:

- automated discovery plus manual URL/file intake;
- bounded targeted crawling rather than web-wide recursion;
- monthly revisits for the most important official target pages, quarterly revisits for other active high-value sources, and semiannual revisits for stable/lower-value sources by default;
- HTML, PDF, DOC/DOCX, scans/images, audio, video, and archives;
- permanent provenance even when mirrors or URLs disappear;
- no access circumvention.

Stage 14 assigns concrete capacity and crawl budgets to that strategy; it does not widen it.

### 2.2 Trust, rights, and economic consequences

Stages 03–04 established that confidence and rights are separate, that weak material may remain useful only for bounded purposes, and that unknown/reference-only source expression must not automatically be sent to an external model.

This has a direct cost implication: **a paid model is not merely an expense decision; it can also be an invalid processing route for some source material.** Local/deterministic processing and derived abstractions are therefore required fallbacks, not optional optimizations.

### 2.3 Canonical structure and shared-content reuse

Stage 05 represents shared Stimuli, option banks, audio, and Assets once and links them to the Items that depend on them. This prevents the cost model from paying to reprocess the same passage or recording per question.

The unit used for the primary Stage 14 cost target is the **canonical Item**, not the Source Observation. Observation counts are still tracked because crawling and storage are driven by observations, while exam intelligence is driven by canonical independent content.

### 2.4 Semantic enrichment and model-quality gates

Stages 06–07 established deterministic normalization first, offline semantic enrichment, approximate **95% measured precision** before high-impact fine taxonomy mappings auto-publish, multidimensional difficulty/relevance, and an explicit preference for broader/unknown/provisional output over expensive fabricated precision.

### 2.5 Pipeline, reprocessing, and QA

Stage 08 established four conceptual cost tiers:

1. deterministic/local baseline;
2. cheap/local/batched extraction and enrichment;
3. selective stronger model/analysis;
4. human/legal/gold-standard review.

It also established selective OCR/ASR, shared-content reuse, dependency-scoped reprocessing, and no per-learner Corpus inference.

Stage 10 adds the main quality constraints that spending must protect:

- roughly **99% precision** for correctness-critical machine answer/key/scoring links;
- roughly **95% precision** for high-impact taxonomy mapping;
- risk-stratified QA sampling: initially 10% for a new/changed slice and 3% for a stable qualified slice, with gold records fully reviewed;
- last-known-good output survives a cheaper/newer method that regresses quality.

Stage 14 therefore budgets manual QA sampling separately from exception review and does not attempt to automate away the benchmark contract merely to reduce cost.

### 2.6 Deduplication, analytics, and App contract

Stages 09–12 require deterministic deduplication before expensive semantic comparison, offline/cached analytics, precomputed target profiles and generation blueprints, and no per-learner Corpus inference. The App sends desired pattern requirements rather than personal learner state, which keeps Corpus outputs highly cacheable.

### 2.7 Operations

Stage 13 defines one-owner operations, impact-prioritized queues, scoped reprocessing, source allow/block controls, and an actionable health vector. It deliberately deferred concrete retry limits, batch sizes, automation budgets, and cost caps to this stage.

No earlier product decision is replaced by Stage 14.

---

## 3. Decisions and Rationale

## 3.1 Plan for three scale scenarios, but optimize the product for the base scenario

**Decision:** Corpus uses three **planning envelopes**, not growth KPIs. The base scenario is the design center for the initial personal project; the high scenario is an upgrade trigger, not a target to fill.

| Planning envelope | Distinct source families / collections | Source observations / candidate URLs | Unique Documents / source Assets | Tasks | Canonical Items / questions | Listening audio | Raw + retained derived storage | Product interpretation |
|---|---:|---:|---:|---:|---:|---:|---:|---|
| **Low — benchmark / useful seed** | **25–50** | **500–1,500** | **250–500** | **800–2,000** | **3,000–8,000** | **10–30 h** | **≤25 GB** | Enough to exercise all stages, instantiate the Stage 16 benchmark, and start useful pattern analysis; not expected to settle many prevalence questions. |
| **Base — useful personal Corpus** | **75–150** | **5,000–15,000** | **1,500–3,000** | **5,000–12,000** | **20,000–50,000** | **75–200 h** | **50–150 GB** | Target planning range for a broad A2/B1 evidence product with meaningful cross-provider/TELC analytics. |
| **High — stretch / upgrade envelope** | **300–500** | **30,000–80,000** | **8,000–12,000** | **30,000–60,000** | **120,000–200,000** | **500–1,000 h** | **300–750 GB** | Large enough that owner time, storage lifecycle, batch throughput, and paid processing deserve explicit infrastructure review before further growth. |

### Interpretation rules

- These are **unique/canonical planning volumes after obvious duplicate handling**, except `Source observations`, which intentionally includes mirrors/alternate locations and rejected/deferred candidates.
- One Document can contain many Items; one Item can depend on shared Stimuli or Assets. The columns are not expected to scale linearly.
- Video minutes are not a target volume because full-video acquisition/analysis is not a default Corpus requirement. Relevant video may contribute audio, captions, or selected visual prompts.
- If the corpus reaches only half the base volume but already has strong coverage and decision-grade analytics, **do not crawl merely to hit a number**.
- If a strategically important provider/section remains weak at the high overall volume, acquisition should still target that gap rather than celebrate the total count.

### Why these ranges

The low range is materially larger than Stage 10's 300–500-Item gold set but still small enough to inspect and iterate on methods. The base range is large enough for repeated task/skill/topic patterns to emerge without implying enterprise-scale infrastructure. The high range represents a plausible long-term personal corpus where hundreds of gigabytes and six-figure Item counts change operational economics, but still does not justify architecture optimized for internet-scale crawling.

## 3.2 Growth is controlled by marginal information value

**Decision:** A new source earns processing budget by improving one or more of:

- TELC B1 target fidelity/currentness;
- provider × CEFR × Section coverage;
- underrepresented task/format/media coverage;
- A2→B1 progression evidence;
- independent corroboration;
- correctness/scoring evidence;
- duplicate/lineage resolution;
- benchmark/regression coverage;
- a high-value App generation/target-profile gap.

A source that mainly adds another mirror, another large exercise collection from an already dominant publisher, or low-confidence near-duplicates should normally stop after cheap intake/dedup checks.

**Product rule:** once marginal information gain becomes low, **defer processing before paying for OCR, ASR, embeddings, or semantic AI**.

## 3.3 Use a seven-step cheap-first processing ladder

**Decision:** Every eligible source follows the cheapest applicable path first. Higher steps are conditional; the ladder is not a requirement that every record reach every step.

| Step | Cost posture | Typical work | Default decision |
|---|---|---|---|
| **0 — Reject / defer before deep processing** | near-zero | relevance, source allow/block, coverage-gap value, obvious mirror/known-work hints, size/type sanity | Stop low-value candidates before expensive download/enrichment. |
| **1 — Deterministic intake** | very low | fetch/change metadata, hashes, file/container facts, native text presence, explicit provider/level/source labels, archive manifest, source relationship clues | Always preferred where applicable. |
| **2 — Deterministic structure + exact dedup** | very low | native parse, source numbering, explicit relationships, canonical skeleton, response cardinality, exact/content fingerprints, known key links, basic validators | Reuse an existing derivation when content identity allows it. |
| **3 — Local/cheap extraction** | low | selective OCR, selective ASR, layout recovery, local fuzzy matching, deterministic/NLP features | Only the pages/segments needed for a downstream job. |
| **4 — Cheap batched semantic enrichment** | low paid or local | topic/grammar/skill suggestions, broad reasoning/distractor candidates, semantic relation candidates, difficulty/relevance estimates | Offline, cacheable, benchmark-qualified for auto-use or provisional otherwise. |
| **5 — Selective stronger-model analysis** | materially higher | difficult OCR/ASR, ambiguous high-impact segmentation/linking, primary-skill/reasoning/distractor adjudication, productive-rubric mapping, high-value TELC ambiguity | Invoke only when cheaper results are insufficient **and** resolving the ambiguity changes a meaningful product outcome. |
| **6 — Human / legal / gold review** | scarce owner/expert time | conflicting keys, rights/legal ambiguity, likely fake/tamper, benchmark truth, unique target evidence, unresolved correctness-critical cases | Highest-impact only; preserve an unresolved/held state when review is not worth the cost. |

The ladder extends the Stage 08 tiers without changing their meaning. The important new decision is the **economic stop rule**: a lower tier may be the final state when the unresolved precision is not worth paying to obtain.

## 3.4 Higher-quality models are risk-triggered, not source-type-triggered

**Decision:** No source automatically “deserves the best model” merely because it is official or TELC. A stronger model is required only when all of these are true:

1. a required production capability cannot meet its Stage 10 quality gate with the cheaper qualified path;
2. leaving the field unknown/provisional would materially block a high-value Corpus/App use; and
3. the stronger method has benchmark evidence or a narrowly inspectable output that makes the extra spend defensible.

Typical stronger-model cases are:

- answer-critical OCR/ASR containing numbers, dates, prices, negation, corrections, or response options;
- ambiguous answer/scoring or cross-document linkage after deterministic evidence is exhausted;
- ambiguous canonical segmentation that changes what is scored or counted;
- primary skill, reasoning, distractor, or productive-rubric classification that materially affects learner diagnosis/generation and a cheaper method misses the Stage 10 gate;
- high-impact derivative/independence ambiguity that materially changes decision-grade prevalence;
- a unique/current TELC source whose unresolved interpretation changes the target profile;
- benchmark/regression adjudication where the lower tier is known to be weak.

A stronger model is **not** justified simply to replace a broad but adequate tag with a cosmetically more precise leaf label.

## 3.5 Human review is treated as a cost, even when it has no invoice

**Decision:** Owner time is a first-class scarce resource and is measured separately from cash spend.

Routine human effort has two categories:

1. **QA sampling** required by Stage 10; and
2. **exception/adjudication review** caused by ambiguous records.

The initial personal-project target is:

- **routine owner review should normally fit within about 1 hour/week at base-scale steady state**;
- **exception review should average no more than ~30 minutes per 1,000 newly processed canonical Items**, excluding Stage 16 gold annotation and deliberate one-off investigations;
- gold/benchmark work is explicitly allowed to exceed the routine target because it buys reusable automation confidence.

These are workload guardrails rather than personal-time commitments. If the corpus cannot stay inside them for four consecutive weeks, growth pauses long enough to improve automation, sampling, source selection, or queue prioritization.

Human review is worth the cost when it protects or unlocks:

- learner correctness/scoring;
- current TELC target facts;
- rights/takedown/legal disposition;
- a unique coverage gap;
- benchmark truth;
- a repeated failure class whose one correction unlocks many records;
- a decision-grade duplicate/independence question;
- a high-impact taxonomy/generation blueprint.

Human review is **not** routinely worth the cost for:

- D-tier or duplicate noise with strong alternative coverage;
- optional metadata;
- cosmetic formatting/OCR differences that do not alter meaning;
- fine semantic distinctions whose broader parent is sufficient;
- old low-relevance sources whose resolution does not affect current analytics;
- proving that a large low-value backlog is indeed low value.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 AI / automation needs by source type

“AI need” means semantic or probabilistic processing beyond straightforward deterministic parsing. It does not imply a paid third-party API.

| Source / format | Cheap/default path | AI / probabilistic processing normally needed | Stronger-model / human escalation |
|---|---|---|---|
| **Clean HTML** | fetch, DOM/text extraction, explicit metadata, deterministic segmentation clues, hashes/dedup | semantic taxonomy/difficulty/relevance for accepted unique content; often batchable | only ambiguous task boundaries, answer semantics, or high-impact target interpretation |
| **Text-native PDF** | native text/layout, numbering, table-of-contents/source relations, fingerprints | semantic enrichment; layout model only where native structure is insufficient | answer-critical layout corruption, difficult tables/forms, cross-file edition/link ambiguity |
| **DOC/DOCX** | native structure, paragraphs/tables/media relations, explicit metadata | semantic enrichment similar to native PDF | malformed complex layout, ambiguous answer/key relations |
| **Scanned PDF / image** | scan detection, region/page triage, local OCR only where needed | OCR/layout recovery for relevant pages; semantic enrichment after extraction | poor answer-critical regions, tables/forms, unique TELC evidence, benchmark pages |
| **Audio** | metadata, duration, existing source transcript/captions, file/script fingerprints | ASR only when semantic content is required; acoustic features when needed; semantic enrichment from reliable transcript | answer-critical uncertain segments, difficult alignment, benchmark Listening evidence |
| **Video** | metadata; use source captions/audio/selected visual prompts when sufficient | extract only the modality necessary for the exam evidence; avoid full video understanding by default | full visual/temporal analysis only for uniquely valuable tasks whose tested content cannot be recovered more cheaply |
| **ZIP / archive** | deterministic inventory/unpack, hash/dedup members, preserve bundle relationships | none at container level; process accepted members by their own type | only for ambiguous bundle/member relationship affecting exam identity |
| **Official/current TELC** | same cheap ladder as every source, but high acquisition/enrichment priority | enrich enough to support current target profile and benchmark gaps | stronger model/human only when lower-tier uncertainty would materially affect target facts/correctness |
| **Unofficial collection / forum / shared document** | provenance/relevance/dedup gate first; often defer before semantic work | semantic processing only after evidence value and independence justify it | rare—only unique/high-value evidence or a dispute that materially affects analytics |

### Base-scenario processing mix

For capacity planning—not as a quality shortcut—the base corpus should be economically viable if approximately:

- **100%** of accepted content receives Steps 1–2 deterministic processing;
- **40–60%** of unique Tasks/Items receive some Step 3–4 semantic/media enrichment because the rest can be source-explicit, duplicated/reused, deferred, or structurally useful without every semantic field;
- **≤10%** of newly accepted unique records require Step 5 stronger-model escalation in a mature pipeline;
- **≤2%** require exception/adjudication human review, **in addition to** the Stage 10 risk-stratified QA sample;
- the Stage 16 gold set remains 100% manually adjudicated for its required truth fields.

If mature operations substantially exceed the 10% stronger-model or 2% exception-review assumptions, this is a signal that either the cheap method, source mix, or requested granularity is economically wrong. It is not a reason to normalize premium processing everywhere.

## 4.2 Deterministic / cheap processing requirements

The following should use deterministic/local processing before any paid semantic model whenever the source supports it:

- allow/block and acquisition-policy checks;
- URL/source normalization and change detection;
- HTTP/file metadata and redirects;
- raw/content fingerprints and known duplicate lookup;
- archive/container inventory;
- native text extraction;
- page, paragraph, heading, numbering, and option boundaries where source-explicit;
- provider/exam/CEFR labels explicitly declared by the source;
- response mechanics/cardinality and source numbering;
- explicit answer/key/scoring links;
- asset inventory, media duration/dimensions, source transcript presence;
- structural invariants and Q0/Q1 deterministic validators;
- exact/reformatted duplicate detection and local candidate fingerprinting;
- obvious rights/license statement extraction as **evidence**, not legal interpretation;
- cache lookup and prior derivation reuse;
- aggregate analytics from published structured data;
- Corpus → App eligibility decisions from already-computed trust/rights/QA/version states.

**Rule:** do not call a model to rediscover a fact that the source or canonical structure already states unambiguously.

## 4.3 OCR principles

- Never OCR a clean text-native page merely for uniformity.
- Detect which pages/regions actually require OCR.
- Prefer local/cheap OCR for first pass when benchmark quality is adequate.
- Run stronger OCR only on failed/low-confidence regions whose meaning affects structure, answer truth, rights evidence, benchmark quality, or high-value TELC intelligence.
- Do not pay for whole-document re-OCR because one answer-critical region needs escalation.
- Cache OCR by source-region identity and OCR method/version.
- A failed OCR region can remain extraction-incomplete indefinitely when its expected product value is low.

## 4.4 Transcription / audio principles

- Reuse a reliable source transcript before ASR.
- Do not transcribe audio merely to know that the Asset exists, its duration, or its file identity.
- When semantics are required, prefer the coarsest useful scope: required track/segment rather than word-level alignment.
- Batch/local ASR is the default where benchmark quality is adequate.
- Stronger ASR/manual correction is selective for answer-critical tokens, benchmark Listening records, difficult alignment, and unique/current TELC evidence.
- Cache transcript and alignment by audio/script identity and method version.
- Re-recordings of the same script reuse semantic/script analysis while preserving distinct acoustic evidence when Stage 09 says it matters.

## 4.5 Embeddings and semantic similarity

**Decision:** Paid embeddings are **not a mandatory all-content ingestion step**.

Use this order:

1. raw/content fingerprints and deterministic normalization;
2. cheap/local lexical/fuzzy candidate generation;
3. local/open semantic embeddings or equivalent only where they materially improve unresolved candidate discovery/search;
4. stronger semantic comparison only for high-impact unresolved pairs.

Embedding/similarity outputs are cached/versioned. Exact duplicates do not need repeated embeddings. When Stage 04 does not permit external processing of raw source expression, use local processing or allowed derived abstractions.

Embeddings must not become a hidden per-model-upgrade backfill obligation. A new embedding model is re-run only when measured search/dedup/product value justifies the affected reindexing cost.

## 4.6 Batching principles

**Decision:** Tier 1/Step 4 semantic enrichment must be **batchable by design**; item-by-item paid calls are reserved for exceptional Step 5 adjudication.

Batch together work that shares:

- modality/source type;
- requested output schema;
- taxonomy/rubric/model version;
- rights-compatible processing route;
- provider/task family when context materially improves accuracy;
- the same source bundle or shared Stimulus when this reduces repeated context.

Batching should reduce request overhead and allow cheap offline processing, but **large batch size is never allowed to weaken failure isolation or traceability**. Every output remains attributable to its Item/Task/Stimulus and derivation version.

The product does not mandate one numeric batch size because optimal size depends on the chosen provider/local runtime. The economic rule is:

- Step 4 work waits for a homogeneous cohort/source bundle unless it is a high-impact freshness blocker;
- Step 5 work may run as a small targeted request because its purpose is exception resolution, not throughput;
- App sessions never wait for a Corpus enrichment batch.

## 4.7 Caching and reuse principles

**Decision:** If inputs and governing versions have not materially changed, Corpus should not pay to recompute the same fact.

A reusable derivation is conceptually keyed by enough identity to distinguish:

- source/content fingerprint or canonical content identity;
- relevant source region/Asset/Stimulus scope;
- method/model/rule version;
- prompt/template/schema version when applicable;
- taxonomy/rubric version when applicable;
- rights-compatible processing mode where external-versus-local processing matters.

Required reuse behaviors:

- exact/reformatted duplicates reuse compatible extraction/enrichment rather than re-running paid processing;
- shared Stimuli, option banks, and audio are processed once for shared properties;
- source-level provenance/rights evidence is reused where its scope legitimately covers descendants;
- deterministic failures are **negative-cached** so unchanged input/method does not loop forever;
- model disagreements and human decisions are cached as review state, not repeatedly re-billed;
- analytics and App-facing blueprints are recomputed only when a contributing dependency changes;
- a new model version creates a candidate reprocessing opportunity, **not an automatic corpus-wide backfill**.

### Reuse safety rule

Reuse only properties that are truly invariant. A derivative Item may inherit source/script identity evidence but must not automatically inherit its answer, distractor semantics, difficulty, rights, or independence if those changed.

## 4.8 Deferred processing

**Decision:** “Known but not processed yet” is a first-class economical state.

Normally defer expensive work for:

- low-confidence material with strong alternative coverage;
- likely duplicates pending cheap identity resolution;
- large unofficial collections that do not fill a coverage gap;
- missing-dependency records whose semantic work would be unusable without the dependency;
- full-video analysis when audio/captions/selected images are sufficient;
- fine-grained taxonomy when a broad trusted parent is adequate;
- word-level audio alignment when Task-level mapping is sufficient;
- semantic embeddings when deterministic/fuzzy retrieval is adequate;
- historical sources whose current target relevance is low and whose metadata is already sufficient;
- corpus-wide reprocessing after a model release until benchmark evidence proves a useful gain.

Deferred records remain discoverable in operations and can be promoted when their expected information value changes.

## 4.9 Retry and failure limits

**Decision:** Retry is bounded by failure class. The product must not create an uncontrolled background loop that repeatedly bills the same operation or hammers a source.

| Failure / operation | Initial product limit | After limit |
|---|---|---|
| **Transient network/server fetch** | **3 total attempts** for the unchanged fetch action (initial + up to 2 retries), honoring server retry guidance | `retry_exhausted` / deferred until a later scheduled revisit or operator action |
| **HTTP 404/410 / clear permanent absence** | **No immediate retry loop** | mark unavailable; follow Stage 02 freshness/alternate/archive rules |
| **HTTP 429 / explicit Retry-After** | honor the specified wait; do not bypass it; maximum 3 attempts in the active fetch cycle | defer to later crawl/revisit if still rate-limited |
| **Deterministic parser failure** | one normal attempt plus **one materially different applicable fallback method** | extraction-incomplete / review/defer; do not repeat the same method |
| **OCR / ASR failure** | one baseline pass plus **one targeted escalation pass** only when value justifies it | hold/unknown/manual review; no open-ended paid retries |
| **Paid semantic model derivation** | **2 paid attempts maximum** per unchanged input + method/prompt/schema version (normal + one structured corrective retry) | broader/provisional/unknown or Step 5/6 review if impact justifies it |
| **Strong-model adjudication** | **1 primary strong pass**, optionally one independent check only for a correctness/benchmark gate | human review or hold; no model-voting loop |
| **Reprocessing job with unchanged deterministic failure** | do not retry until an input, dependency, method version, or explicit operator decision changes | negative-cache failure and surface in operations |

### Retry accounting rule

A rate-limit wait or infrastructure interruption may be retried without pretending the record itself failed semantically, but **every paid attempt still counts toward the cost ledger**. A retry that would breach the monthly budget gate is deferred unless it protects a Q0/current-target/benchmark-critical outcome.

## 4.10 Crawling etiquette and rate-limit principles

**Decision:** Corpus uses conservative crawling suitable for a personal project and a finite curated source universe.

Default per-host posture:

- **1 concurrent request per host**;
- at least **2 seconds between requests** to the same host (default ceiling **0.5 requests/second**);
- honor `Retry-After`, robots directives, published rate limits, source terms, and any stricter source-specific policy;
- use provider/resource indexes, known URLs, conditional/change checks, and targeted links before broad traversal;
- do not bypass login, paywalls, bot protections, CAPTCHAs, private groups, or access controls;
- do not use multiple identities/proxies to evade a source limit;
- prefer a manual submission/recheck over fragile high-volume automation for a small number of awkward high-value sources.

### Discovery-run ceiling

A previously unreviewed host may fetch at most **200 new candidate URLs in one discovery run** by default. Crossing that threshold requires a coverage/value reason in the source registry or an explicit owner-approved expansion. The intent is to prevent one noisy site or accidental link graph from manufacturing thousands of downstream OCR/AI jobs.

A source with an explicit public API/download mechanism may use its documented higher allowance. The product requirement is to respect the provider's rules rather than enforce the 0.5 req/s default when the provider intentionally supports another access pattern.

### Crawl budgeting rule

Crawl volume is not free merely because bandwidth is cheap: every new payload can create storage, extraction, review, and AI cost. The operations view should therefore distinguish **URLs discovered**, **payloads fetched**, **unique content accepted**, and **canonical Items published**.

## 4.11 Raw-file and media storage expectations

**Decision:** Corpus expects to retain enough raw/source evidence for provenance, reprocessing, QA, and rights operations **when Stage 04 and Stage 15 permit retention**, while avoiding redundant physical copies and unnecessary media derivatives.

### Storage principles

- One byte-identical raw object is stored once conceptually even when many Source Observations point to it.
- Preserve source/version identity and provenance even when physical duplicate bytes are shared.
- Keep raw/source-quality evidence where it is needed to defend extraction, answer, asset, or provenance claims.
- Keep retained derived data that is costly or necessary to reproduce: validated OCR, transcripts, alignment, normalized structure, fingerprints, benchmark annotations, and current/superseded derivations according to the owning-stage audit rules.
- Temporary intermediates that are safely regenerable and not needed for audit/debug may be discarded after successful validation.
- Avoid keeping many equivalent media transcodes merely because a tool produced them.
- Full video bytes are **not** a default archival requirement when the relevant evidence can be preserved through an allowed source reference plus needed audio/caption/visual components; Stage 15 may impose stricter retention or deletion rules.
- A single file larger than **250 MB** should require an explicit value/retention decision before long-term local/paid storage; this mainly protects against accidental video/archive growth.

### Storage guardrails

- **≤150 GB raw + retained derivatives:** normal base-envelope operation.
- **>150 GB:** storage-growth alert; identify duplicate/transcode/cache waste and large-media sources.
- **>250 GB or >€10/month Corpus-specific storage cost:** trigger a storage/tiering/retention architecture review before continuing unconstrained growth.
- **>500 GB:** treat as high-scale operation; new large-media ingestion requires explicit coverage value until Stage 15/architecture has a deliberate lifecycle policy.

These thresholds are capacity guardrails, not deletion commands. Rights, legal, security, benchmark, and provenance requirements can justify retaining data beyond them; the response is to choose a more economical storage/lifecycle design, not to silently delete source evidence.

## 4.12 Cost accounting model

**Decision:** Corpus maintains a small **cost ledger** so “cheap” is measurable rather than aspirational.

Every paid or materially metered processing run should be attributable conceptually to:

- source/source family and canonical scope;
- first-pass ingestion versus retry versus reprocessing/backfill;
- modality: text, scan/OCR, audio/ASR, video/visual, semantic AI, embedding/similarity, storage;
- processing tier/step;
- model/service/method and version where applicable;
- number of source pages/audio minutes/Tasks/Items processed;
- cache hit/reuse versus fresh work;
- actual paid cost where available, or measured internal compute unit when running locally;
- outcome: published, provisional, rejected, duplicate-reused, failed, or review-required.

### Primary cost denominator

The Stage 14 primary variable-cost metric is:

> **Paid variable processing cost per 1,000 newly processed canonical Items.**

For this metric:

- count Items that reach validated structured publication or a stable limited/provisional state after the batch;
- allocate shared document/audio/model costs across the linked canonical Items for the batch;
- include paid OCR/ASR/semantic/embedding/extra compute directly attributable to processing;
- exclude durable baseline storage and generic project hosting from the denominator—they are tracked as monthly fixed/semifixed cost;
- exclude human time from cash cost but report it alongside the metric;
- exclude App learner-facing generation/evaluation costs.

Because modality mix can distort a single denominator, also track:

- paid cost per 1,000 candidates triaged/fetched;
- cost per 1,000 pages requiring OCR;
- cost per audio hour requiring ASR;
- cost per 1,000 semantic enrichments;
- cost per 1,000 reprocessed Items;
- owner review minutes per 1,000 Items.

## 4.13 Target processing cost per 1,000 Items

**Decision:** For the **base mixed-modality Corpus**, the initial target is:

- **target:** **≤€3 paid variable processing cost per 1,000 canonical Items**;
- **warning band:** **>€3 to €4 / 1,000 Items**;
- **optimization/escalation threshold:** **>€4 to €5 / 1,000 Items**;
- **stop-and-review threshold:** **>€5 / 1,000 Items** over a rolling cohort of at least 5,000 Items, unless the cohort is intentionally media-heavy/benchmark-critical and the exception is documented.

This is a **budget target, not a vendor-price claim**. It assumes the product follows the cheap-first ladder, shares Stimulus/media analysis, avoids paid processing for duplicates/low-value candidates, and uses premium calls on a small minority of records.

A media-heavy Listening or scan benchmark batch may legitimately cost more per Item. Such a batch should expose its OCR-page/audio-hour cost separately rather than causing the entire product to normalize a higher baseline.

### Why €3 / 1,000 is the design target

At base volume, 20,000–50,000 Items would correspond to roughly **€60–€150 of cumulative paid variable processing** if the full corpus were processed at the target, typically spread across months and reduced further where local processing/caching is effective. That is material enough to measure but small enough for a personal project. If real implementation cannot approach this range without compromising Stage 10 quality, Stage 14 prefers a smaller/high-value corpus or more local/batched processing over silently accepting enterprise-style per-item spend.

The threshold should be recalibrated after the first 5,000–10,000 real Items, using actual modality mix and QA outcomes.

## 4.14 Monthly personal-project budget guardrails

**Decision:** Initial Corpus-specific recurring cash spend should normally fit inside **€25/month**, with a hard exception boundary at **€50/month**.

This includes Corpus-specific paid processing and storage that would not otherwise be paid for by the project. Existing shared/general project infrastructure may be accounted separately but should still be visible so the project does not hide true marginal cost.

| Monthly state | Trigger | Product behavior |
|---|---|---|
| **Green** | **≤€15 actual and forecast remains ≤€25** | Normal bounded ingestion/enrichment under priority rules. |
| **Amber** | **>€15 actual**, forecast **>€25**, or rolling processing cost **>€4/1k Items** | Defer low-priority paid enrichment, inspect cache/dedup/media/reprocessing waste, keep Tier 0/1 local work running. |
| **Red** | **>€25 actual** or rolling processing cost **>€5/1k Items** without a documented high-value cohort reason | Pause nonessential paid bulk processing; only deterministic/local work and explicitly high-impact Tier 2/3 cases continue. |
| **Hard ceiling** | **€50 in a calendar month** | No further paid Corpus job without an explicit owner override identifying purpose and expected cost. |

### One-off benchmark/backfill allowance

A deliberate Stage 16 benchmark build, regression investigation, or high-value backfill may spend up to **three normal monthly envelopes (≤€75)** as an explicitly initiated one-off campaign. It must be costed separately from recurring operations and should not become the new normal monthly run rate.

### Storage sub-budget

At base scale, storage should normally remain **≤€5/month** of the €25 envelope. Sustained storage above **€10/month** triggers the >250 GB/storage-review posture even if total cash spend is otherwise acceptable.

## 4.15 Budget alerts and paid-job gating

Before a paid bulk job/reprocessing campaign starts, the product must conceptually know:

- why the work is needed;
- estimated unit count/modalities;
- whether cached/duplicate/shared outputs can be reused;
- estimated cost range based on recent effective rates;
- remaining monthly budget;
- which lower-cost fallback exists if the job is deferred.

After the job, the cost ledger records actual cost and outcome. The product does **not** need a complex billing platform; a stored estimate/actual and simple budget status are sufficient.

Budget alerts should surface in Stage 13 Corpus Health/Operations when:

- monthly green/amber/red thresholds are crossed;
- a batch exceeds the €3/1k target or €5/1k stop threshold;
- retry/reprocessing cost becomes more than **20% of the month’s paid processing spend**;
- cache/reuse rates materially fall after a method/version change;
- storage crosses 150/250/500 GB guardrails;
- stronger-model escalation exceeds 10% of newly accepted unique records for a mature slice;
- exception review exceeds the owner-time guardrail.

## 4.16 Upgrade triggers

**Decision:** Corpus upgrades infrastructure, models, or automation in response to a measured bottleneck—not because a larger option exists.

### A. Trigger for a stronger paid model/service

Upgrade a field/slice only when:

- the current cheap method fails a Stage 10 production-quality gate or creates repeated Q0/Q1 review work;
- a benchmarked stronger option materially improves the relevant metric; and
- the cost per successfully resolved high-impact record is better than keeping the field provisional or reviewing it manually.

A stronger model that improves style while not changing product eligibility is not an upgrade justification.

### B. Trigger for more local/managed compute

Review compute capacity when a **high-value** processing backlog remains more than **14 days** behind for two consecutive cycles despite batching/caching, and the bottleneck is compute throughput rather than review, source access, or deliberate deferral.

The product requirement is timely completion of high-value offline work, not real-time Corpus processing.

### C. Trigger for more storage/lifecycle capability

Review storage design at **>250 GB** or **>€10/month** storage cost. Treat **>500 GB** as high-scale and require explicit large-media intake policy.

### D. Trigger for more review automation

Improve review tooling/automation when routine owner burden exceeds **~1 hour/week for four consecutive weeks** or when the same failure class repeatedly consumes manual time. Automate the repeated evidence-gathering/check, not the final high-risk legal/correctness judgment unless benchmark gates support it.

### E. Trigger for broader crawler infrastructure

Do not upgrade crawling merely because a site is large. Upgrade discovery throughput only when the conservative host/run limits repeatedly prevent coverage of P0/P1/high-value gaps and the source explicitly permits the higher access rate.

### F. Trigger for analytics/contract recomputation infrastructure

Upgrade when decision-grade analytics/App bundles for a material change cannot be recomputed within **24 hours** at the base envelope or when a 14-day backlog would make current TELC target information operationally stale. The exact mechanism remains architecture.

### G. Trigger when the corpus approaches the high envelope

Crossing roughly **100,000 canonical Items, 8,000 unique Documents, or 250 GB** is a formal scale review point. The result may be “continue with the current simple architecture”; the review is required so a personal-project design is not accidentally stretched beyond its measured operating envelope.

## 4.17 Vendor-pricing policy

**Decision:** Stage 14 does **not** embed a current OCR/ASR/LLM/storage vendor price table because no vendor is a product requirement and the budget guardrails above are deliberately provider-independent.

Current vendor prices are therefore **not needed to make this product decision**. When architecture selects or compares an external provider, it must:

1. use that vendor’s current official pricing at the time of selection;
2. record the date/source of the pricing snapshot;
3. model the expected source/modalities against the Stage 14 €3/1k and €25/month targets;
4. include batch/cached/local alternatives;
5. avoid a provider whose economics require normalizing premium calls across the corpus merely to fit the pipeline.

This keeps the product specification stable even when vendor pricing changes.

---

## 5. Edge Cases / Failure or Uncertainty Handling

### 5.1 One official TELC source is expensive to process

Do not reject it because its per-Item cost exceeds the normal average. Current/unique target evidence can justify a documented cohort exception. Process only the pages/segments needed, reuse the result, and keep the exception from redefining the corpus-wide baseline.

### 5.2 Large unofficial collection contains thousands of exercises

Run relevance/provenance/dedup/coverage checks first. Sample or ingest only the material that adds independent coverage. Do not OCR/enrich the whole collection simply because it is available.

### 5.3 A clean mirror is cheaper to parse than the official scan

Use the mirror as the preferred processing representation when Stage 09 evidence supports identity, while keeping the official source as provenance anchor. Rights and processing permissions remain separately evaluated.

### 5.4 Paid model produces a failure and retry would exceed the budget

Defer the retry unless the output is Q0/current-target/benchmark-critical. Keep the record provisional/unknown/held rather than spending past the guardrail automatically.

### 5.5 A new model is cheaper and better on average

Run the Stage 10 benchmark/incident regression first. Reprocess only affected high-value records after qualification. Do not corpus-wide backfill merely because the unit price fell.

### 5.6 A new model is more expensive but fixes one important slice

Use it only for that slice. A field-specific upgrade does not imply switching every semantic task to the stronger model.

### 5.7 Local processing is “free” but takes days

Local compute is not economically free if it blocks owner work or creates a high-value backlog. Track runtime/queue age. Upgrade only when the 14-day high-value backlog trigger is met and a paid/managed alternative is cheaper than the operational burden.

### 5.8 Storage is cheap but video volume explodes

Apply the 250 MB per-file value check and 150/250/500 GB storage guardrails. Preserve only the source evidence/derived modalities required by product, rights, QA, and Stage 15 retention policy; do not archive large video merely because storage pennies are low today.

### 5.9 Duplicate decision changes after expensive enrichment already ran

Keep the derivation if useful/auditable, but cluster it correctly and reuse the result going forward. Do not allow historical sunk cost to justify counting a mirror as independent evidence.

### 5.10 Rights prohibit external model processing

Use deterministic/local processing or allowed derived abstractions. If the field cannot be resolved locally and direct product value does not justify a legal/rights review, keep it unknown/provisional.

### 5.11 Low-confidence material would exceed human-review budget

Do not review it merely to empty the queue. Keep it bounded/held, prioritize high-impact unique evidence, or reject/defer the source family if its maintenance burden is consistently poor.

### 5.12 Stable method has a sudden Q0 escape

Stage 10 immediately holds the affected slice. Budget limits do not override the quality hold. Spend may temporarily shift to benchmark/review under the one-off allowance, while unrelated low-priority paid work is deferred.

### 5.13 Corpus exceeds the high planning envelope but costs stay low

Do not force an architecture rewrite. Perform the formal scale review, inspect owner burden, storage, QA, batch latency, and App freshness. Continue simply if the measured constraints remain healthy.

### 5.14 Corpus remains small but high-quality and analytically sufficient

This is success. The planning volumes are not a collection quota. Stop or slow acquisition when marginal information value is low.

---

## 6. Relationship to Other Bestehen Stages

### Stage 02 — Source Strategy

Stage 14 operationalizes Stage 02’s coverage-driven discovery with a conservative 0.5 requests/second per-host default, one concurrent host request, a 200-new-URL discovery-run ceiling, and explicit stop/defer behavior before expensive processing.

### Stage 03 — Trust / Stage 04 — Rights

Confidence and rights continue to gate expensive processing. Low-confidence volume is not entitled to review spend, and unknown/reference-only material may require local rather than external models.

### Stage 05 — Canonical Exam Model

Shared Stimuli/Assets are cost-sharing units. One passage/audio analysis is reused across dependent Items. Exact physical schema remains open.

### Stage 06 — Taxonomy

Fine semantic taxonomy remains batch/cached and premium escalation is justified only when the cheaper path cannot meet the roughly 95% high-impact precision requirement and the fine distinction changes product behavior.

### Stage 07 — Difficulty / Relevance

Difficulty/relevance stays offline, incremental, and cacheable. High-value current TELC ambiguity can receive premium processing; broad/low-impact estimates may remain provisional.

### Stage 08 — Pipeline

Stage 14 makes Stage 08’s cost tiers concrete: paid attempts are bounded, deferred processing is first-class, retries are limited, and one model release never triggers automatic full reprocessing.

### Stage 09 — Deduplication

Cheap fingerprints run before paid semantic comparison. Confirmed duplicates reuse extraction/enrichment. Semantic duplicate adjudication is impact-triggered rather than all-pairs.

### Stage 10 — QA

Cost caps never weaken correctness/QA gates. Stage 10’s risk-stratified sampling remains mandatory; Stage 14 budgets it separately from exception review and permits a one-off benchmark/regression allowance.

### Stage 11 — Analytics

Analytics should remain nearly free incremental computation over structured data. Paid AI is not used to repeatedly explain or recompute ordinary frequencies.

### Stage 12 — Corpus → App Contract

Precomputed/cacheable capabilities are a major cost boundary. Corpus does not add per-learner inference; App personalization remains in App.

### Stage 13 — Operations

Corpus Health must expose budget state, per-1,000 cost, storage thresholds, retry/reprocessing share, escalation share, and owner-time burden alongside the existing quality/backlog/coverage vector.

### Stage 15 — Security and Abuse

Stage 15 owns final raw-file retention/deletion/security policy. It must preserve Stage 14’s economic expectation of deduplicated raw storage and deliberate large-media retention while overriding it where legal/security obligations require stronger retention or deletion.

### Stage 16 — Initial Benchmark Corpus

Stage 16 may use the explicit one-off ≤€75 campaign allowance and is exempt from routine human-review-time targets for gold annotation. It should produce the measurements needed to recalibrate OCR/ASR/model quality and the initial €3/1,000 economics.

### Stage 17 — Final Product Specification

The final PRD should preserve the base planning envelope, cheap-first ladder, cost ledger, budget caps, retry/crawl/storage guardrails, and upgrade triggers without turning any current vendor into a product dependency.

---

## 7. Cost Notes

## 7.1 Major cost drivers, ranked by likely personal-project impact

| Cost driver | Why it can grow | Cheap-first control | Upgrade only when |
|---|---|---|---|
| **Owner review time** | Ambiguous keys, rights, provenance, taxonomy, QA sampling | impact-prioritized queue, benchmark-qualified automation, broader/provisional fallback | >1 h/week sustained or repeated class can be automated safely |
| **OCR / layout processing** | scans, photos, tables/forms, poor PDFs | native text first; page/region selective; local first | answer-critical/high-value regions miss QA gate |
| **ASR / alignment** | Listening/video assets | source transcript first; segment-selective; local/batch | answer-critical/current TELC/benchmark needs higher fidelity |
| **Semantic extraction/classification** | tags, difficulty, relevance, reasoning/distractors | deterministic features + cheap batch + cache | high-impact field misses benchmark gate |
| **Reprocessing/backfills** | model/taxonomy/rule changes | dependency-scoped; last-known-good; no automatic whole-corpus rerun | measured quality/value gain exceeds cost |
| **Raw media/storage** | audio/video/scans and duplicate formats | one physical exact copy; no redundant transcodes; large-media check | >250 GB / >€10 month or provenance/security need |
| **Embeddings/semantic dedup** | all-content reindexing can become habitual | fingerprints/fuzzy/local first; cache pair results | unresolved similarity materially changes evidence counting/search |
| **Crawling/network** | cheap requests can create expensive downstream work | conservative host/run limits; change checks; coverage gating | high-value coverage is demonstrably blocked by throughput |
| **Analytics** | naïve full recomputation | incremental/cached deterministic aggregates | recompute cannot meet target-currentness needs |

## 7.2 Low/base/high economic interpretation

| Scenario | Expected economic posture |
|---|---|
| **Low** | Mostly local/deterministic; paid processing can plausibly stay below one normal monthly envelope for many batches. Owner time is dominated by benchmark/gold setup rather than routine operations. |
| **Base** | Design center: cumulative paid ingestion roughly tens to low hundreds of euros if the €3/1k target is met, with recurring spend normally ≤€25/month and storage ≤€5/month. |
| **High** | Paid processing may accumulate into several hundred euros and storage/owner throughput become material. Growth should be staged and should trigger the formal scale review rather than one uncontrolled backfill. |

## 7.3 What must never be optimized away

Cost control may reduce enrichment depth or defer low-value work, but it must not weaken:

- provenance and auditability;
- rights/takedown enforcement;
- local correctness/scoring gates;
- Stage 10 hard QA/regression gates;
- duplicate neutrality for decision-grade analytics;
- preservation of uncertainty;
- benchmark/gold truth;
- App/Corpus product boundary.

The economically correct fallback is often **less data or less precision**, not lower trustworthiness.

---

## 8. Decisions Made

1. The base design envelope is **75–150 source families, 1,500–3,000 unique Documents/Assets, 5,000–12,000 Tasks, 20,000–50,000 canonical Items, 75–200 Listening hours, and 50–150 GB** raw/retained derived data.
2. The high envelope—roughly **120,000–200,000 Items, 8,000–12,000 Documents, and 300–750 GB**—is an upgrade/review point, not a growth target.
3. Corpus growth is driven by marginal information value and coverage gaps rather than crawl/document count.
4. Processing follows a seven-step cheap-first ladder from reject/defer through deterministic/local/batched work to selective strong models and human/legal review.
5. No source type automatically receives a premium model; higher-quality models are invoked only when cheaper processing misses a required quality gate and resolving the result has meaningful product value.
6. Base mature operations should aim for **≤10% stronger-model escalation** and **≤2% exception human review** of new accepted unique records, in addition to Stage 10 QA sampling.
7. Deterministic/source-explicit facts must be extracted deterministically before semantic AI is considered.
8. Native text is preferred to OCR; OCR is page/region selective. Source transcripts are preferred to ASR; ASR/alignment is scope-selective.
9. Paid embeddings are not a mandatory all-content step; deterministic/fuzzy/local semantic methods come first.
10. Tier-1 semantic enrichment must be batchable/offline. Paid item-by-item calls are reserved for exception adjudication, never App sessions.
11. Derivations are cached/reused by content/scope/method/governing versions; exact duplicates and shared Stimuli/Assets must not be repeatedly billed.
12. Deferred processing is a first-class economical state. Low-value ambiguity may remain unresolved indefinitely.
13. Retries are bounded: three transient fetch attempts, two paid semantic attempts per unchanged derivation, one baseline + one targeted OCR/ASR escalation, and no repeated unchanged deterministic-failure loop.
14. Default crawling is **1 concurrent request per host, at least 2 seconds between requests**, with a **200-new-URL per unreviewed-host/run** ceiling, while honoring stricter source rules and documented APIs.
15. Raw/source evidence is retained when rights/security allow, exact bytes are deduplicated physically, unnecessary media derivatives are avoided, and files >250 MB require explicit value/retention review.
16. Storage is normal up to **150 GB**, reviewed at **>250 GB or >€10/month**, and treated as high-scale above **500 GB**.
17. Corpus keeps a simple cost ledger covering source/modality/tier/first-pass-vs-reprocess/unit counts/cache reuse/cash cost/outcome.
18. The initial target paid variable processing cost is **≤€3 per 1,000 canonical Items**, warning above €3–4, optimize above €4–5, and stop/review above €5/1k on a rolling ≥5k-Item cohort absent a documented high-value exception.
19. Normal Corpus-specific recurring cash spend should stay **≤€25/month**, with a **€50 hard ceiling** without owner override; one-off benchmark/backfill campaigns may use **≤€75** when explicitly initiated.
20. Owner review is treated as a cost; steady-state routine review should normally fit around **1 hour/week**, and exception review should average **≤30 minutes per 1,000 Items** outside gold/benchmark work.
21. Infrastructure/model/automation upgrades are triggered by measured quality, cost, backlog, storage, or owner-time bottlenecks rather than hypothetical scale.
22. Stage 14 embeds no vendor price table because no vendor is a product requirement; implementation must use dated official pricing when a provider is selected and prove it fits these provider-independent guardrails.

---

## 9. Open Questions / Deferred Decisions

### 9.1 Owner questions

**None.** The product can adopt conservative initial personal-project caps without requiring the owner to choose a vendor or commit to a permanent monthly budget. The €25/€50/€75 values are default product guardrails and can be deliberately changed later if the project’s economics change; they are not inferred statements about the owner’s personal finances.

### 9.2 Empirical recalibration required later

The following should be recalibrated from Stage 16 and the first 5,000–10,000 real processed Items rather than treated as eternal constants:

- low/base/high source-to-Item ratios;
- proportion of scans/audio/video in the actual corpus;
- percentage of records needing Step 4/5/6 processing;
- real cache/dedup reuse rate;
- OCR cost per 1,000 pages and ASR cost per audio hour;
- paid semantic cost per 1,000 enrichments;
- €3/1,000 blended processing target if benchmark-quality evidence proves it unrealistically strict or unnecessarily loose;
- owner review minutes by queue/failure class;
- whether 150/250/500 GB storage thresholds remain useful;
- whether the 14-day backlog and 24-hour recomputation triggers are appropriate after real operation.

Any recalibration must preserve Stage 10 quality gates and Stage 03/04 trust/rights rules. “The cheap model is cheaper” is not by itself evidence to lower quality.

### 9.3 Architecture / implementation decisions intentionally deferred

- cloud/local/hybrid compute topology;
- model/OCR/ASR/embedding vendors and versions;
- cache technology and physical cache keys;
- object-store/database choice and storage tiers;
- scheduler, batch engine, queue, concurrency implementation, and retry backoff algorithm;
- exact crawler identity/user-agent and network stack;
- exact cost-ledger schema and alert delivery mechanism;
- hardware purchase versus cloud compute;
- compression/transcoding strategy;
- raw-retention/deletion periods and malware/sandbox policy — Stage 15;
- exact Stage 16 benchmark acquisition and annotation workflow.

These choices may change without changing the product economics shaped here.

---

## 10. Definition of Done Check

| Stage 14 requirement | Decision captured | Where |
|---|---|---|
| Estimate source/document/question volume targets | **Yes** | §3.1 |
| Include low/base/high usage scenarios | **Yes** | §3.1, §7.2 |
| Estimate AI processing needs by source type | **Yes** | §4.1 |
| Decide which steps require higher-quality models | **Yes** | §3.4, §4.1 |
| Decide which steps should use deterministic/cheap processing | **Yes** | §3.3, §4.2–4.5 |
| Define batching principles | **Yes** | §4.6 |
| Define caching/reuse/deferred-processing principles | **Yes** | §4.7–4.8 |
| Define retry/failure limits | **Yes** | §4.9 |
| Define crawling etiquette and rate limits | **Yes** | §4.10 |
| Define raw-file/media storage expectations | **Yes** | §4.11 |
| Define target cost model and cost per 1,000 Items | **Yes** | §4.12–4.13 |
| Define monthly budget alerts/limits | **Yes** | §4.14–4.15 |
| Define infrastructure/model upgrade triggers | **Yes** | §4.16 |
| Define where human review is worth the cost | **Yes** | §3.5 |
| Identify major cost drivers | **Yes** | §7.1 |
| Address crawling, storage, OCR, transcription, embeddings, AI extraction/classification, review, and reprocessing | **Yes** | §4, §7.1 |
| Preserve no-per-learner Corpus AI cost | **Yes** | §3.3, §4.6, relationship to Stage 12 |
| Current vendor pricing handled without lock-in | **Yes — no vendor needed at shaping stage; dated official pricing required when implementation selects a provider** | §4.17 |
| Owner blocker remains | **No** | §9.1 |

**Stage 14 product-shaping status: complete once the live Corpus checklist is reconciled with these decisions.**
