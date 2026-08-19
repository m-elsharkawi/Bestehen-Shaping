# Bestehen / Corpus — Stage 09: Duplicate and Near-Duplicate Detection

> **Status:** Authoritative Stage 09 product-shaping decision  
> **Product:** Bestehen / Corpus  
> **Initial domain:** German A2–B1 exam and exam-style material  
> **Primary downstream customer:** Bestehen / App  
> **Core principle:** Preserve every provenance observation, but let each underlying exam contribution count only according to its real independence; mirrors, reformatting, excerpts, and light derivatives must never manufacture frequency or corroboration.

## 1. Purpose and Scope

Stage 09 defines how Bestehen / Corpus recognizes exact copies, reformatted copies, excerpts, copied questions, shared assets, near-duplicates, and derivative variants across documents, tasks, items, images/scans, and audio. It also defines how those relationships affect canonical records and aggregate evidence counting.

The problem is not merely storage duplication. The product risk is analytical distortion. One mock exam can be downloaded, renamed, scanned, converted to DOCX, reposted on several domains, copied into a forum, split into individual exercises, and accompanied by a retyped answer key. If Corpus treats every observation as independent evidence, a single underlying work can look like a widespread exam pattern and can incorrectly increase authenticity corroboration, frequency, TELC relevance, difficulty confidence, or App learning priority.

The opposite error also matters. Two genuinely independent exam items may share boilerplate, common task wording, a topic, or even a public stimulus. Over-aggressive deduplication would hide real evidence. Stage 09 therefore favors **conservative automatic collapse, non-destructive relationships, and selective review** rather than irreversible merging.

This is product shaping, not implementation architecture. It defines identity concepts, comparison normalization, relationship classes, initial decision thresholds, canonicalization behavior, analytical counting rules, review policy, cost tiers, and edge-case treatment. It does not choose a hash algorithm, vector database, perceptual-hash library, acoustic fingerprinting library, embedding model, ANN index, OCR engine, storage schema, or batch scheduler.

### 1.1 Stage objective

**“Seen 20 times online” must never be interpreted as “seen in 20 independent exams” unless Corpus has evidence that those observations are actually independent.**

At the same time, Corpus must be able to say that the material was observed at 20 locations, because observation breadth can be useful provenance/history even when it is not independent exam evidence.

### 1.2 Product invariants

1. **Source observation count is not evidence count.** URLs, files, archive snapshots, and mirrors are observations first.
2. **Deduplication is non-destructive.** No duplicate decision erases provenance, rights, confidence, version history, or source-specific claims.
3. **Exact copies and derivatives are different.** A reformatted copy contributes no new underlying content; a derivative may contain new material or claims even though its lineage is dependent.
4. **Duplicate status is local.** A document can be derivative while some of its items are exact copies and other items are genuinely new.
5. **Shared assets do not make whole exams duplicates.** One repeated photo, instruction, passage, or audio clip is insufficient to collapse unrelated surrounding items.
6. **Independence is use-specific.** The same re-recorded listening script is dependent evidence for script/content frequency but can be distinct evidence about acoustic difficulty.
7. **Answer disagreement does not create a new item.** Exact item content with conflicting keys remains one item-content family with multiple answer assertions and a dispute.
8. **Rights and authenticity remain separate.** Canonicalization never transfers rights, officiality, or confidence from one observation to another.
9. **Unknown dependency is not treated as full independence.** Production analytics must remain conservative until an important ambiguous relationship is resolved.
10. **Cheap deterministic evidence comes first.** Semantic/AI review is an escalation path, never the default comparison mechanism.
11. **Thresholds are starting policy, not permanent truth.** Stage 16 benchmark data must validate and recalibrate them.

---

## 2. Inputs / Existing Decisions

Stage 09 preserves the Product Overview, Identity, both live shaping checklists, and Corpus Stages 01–08.

### 2.1 Stage 01 — mission and success

`corpus/01-product-mission-and-boundaries.md` established that Corpus succeeds only when frequency analysis reflects **independent evidence rather than mirrors**. Deduplication integrity is a core corpus-quality dimension, not a storage optimization.

### 2.2 Stage 02 — source strategy and provenance

`corpus/02-source-strategy.md` established the distinction among candidate leads, Source Observations, and underlying material; permanent provenance; mirror/alternate/archive relationships; dead-source history; and the rule that an archive or mirror is an observation location rather than a second exam by default.

Stage 09 must preserve every Source Observation even when many observations resolve to one underlying work.

### 2.3 Stage 03 — trust and independent corroboration

`corpus/03-trust-authenticity-confidence.md` established that independent corroboration can increase confidence but mirrors cannot manufacture corroboration. It also established A/B/C/D confidence tiers and the default eligible aggregate weights A/B/C/D = **1.00 / 0.70 / 0.25 / 0.00**.

Stage 09 supplies the missing independence decision that must be applied **before** repeated observations are allowed to contribute those weights.

### 2.4 Stage 04 — rights

`corpus/04-rights-and-usage-metadata.md` established component-level rights, conservative unknown-rights handling, and takedown/removal behavior. A reusable mirror does not make a reference-only original reusable, and a restricted original does not automatically impose the mirror's observed rights state on every related observation.

Deduplication therefore links content identity while preserving rights per source/material component.

### 2.5 Stage 05 — canonical exam model

`corpus/05-canonical-exam-model.md` established Source Observation → Document → Exam/Test Set → Section → optional Part → Task → Item, with Instructions, Stimuli, Response Options, Answers, Scoring Rules, and Assets separately addressable.

That model makes Stage 09 deliberately multi-level:

- Source Observations can be mirrors without being deleted;
- Documents can be exact/reformatted/derivative;
- Exams can be equivalent even when packaged differently;
- Tasks/Items can be copied across otherwise different documents;
- Stimuli and Assets can be shared without making surrounding Items duplicates.

### 2.6 Stage 06 — taxonomy

`corpus/06-exam-and-skill-taxonomy.md` separates task mechanics, skills, topics, grammar, vocabulary, reasoning, and distractor patterns. Similar taxonomy assignments are **not duplicate evidence by themselves**. Two independent items may test the same skill or use the same task template; that is exactly what frequency analytics are meant to observe.

### 2.7 Stage 07 — difficulty and relevance

`corpus/07-difficulty-and-relevance-models.md` separates estimated value, estimate uncertainty, evidence confidence, and aggregate influence. Stage 07 already requires independence/deduplication to constrain evidence influence. Stage 09 defines how that independence signal is obtained and when it remains unresolved.

### 2.8 Stage 08 — ingestion lifecycle

`corpus/08-ingestion-and-extraction-pipeline.md` places **Deduplicate** after Validate and before Review/Publish and requires publication never to assume independence merely because two sources have different URLs. Stage 08 also requires unresolved independence to receive conservative influence.

Stage 09 completes that product contract without changing the Stage 08 lifecycle.

No earlier shaping decision needs to be changed.

---

## 3. Decisions and Rationale

## 3.1 Model observations, content identity, derivative lineage, and analytical independence separately

**Decision:** Corpus must not use one `duplicate=true/false` flag to answer every deduplication question. It needs four separate product concepts:

1. **Observation identity** — where/when/how concrete material was seen or submitted.
2. **Content identity** — whether two units contain the same substantive exam content.
3. **Derivative/lineage relationship** — whether one unit appears to be copied, reformatted, excerpted, lightly edited, re-recorded, annotated, or otherwise derived from another/common ancestor.
4. **Analytical independence** — whether the relationship contributes a new independent unit for a particular metric or claim.

This separation allows Corpus to preserve valuable facts such as “the same exam was mirrored by 12 domains,” while ensuring those 12 observations contribute only one independent exam occurrence to ordinary frequency analytics.

## 3.2 Use explicit relationship classes instead of destructive merges

**Decision:** At Document, Exam, Task, Item, Stimulus, and Asset scope where applicable, Corpus can classify a relationship using the following conceptual classes.

| Relationship class | Meaning | Default evidence treatment |
|---|---|---|
| **BYTE_EXACT_COPY** | Raw payload bytes are identical | Same content; zero additional independent evidence |
| **CONTENT_EXACT_COPY** | Substantive content is identical after allowed non-semantic normalization, despite container/metadata differences | Same content; zero additional independent evidence |
| **REFORMATTED_COPY** | Same substantive content, but layout/container/pagination/scan/OCR/branding/format differs | Same underlying evidence; zero additional independent evidence |
| **DERIVATIVE_COPY** | Clearly common-origin material with small/moderate edits, annotations, omissions, option reorder, copied excerpts, re-recording, or other dependent transformation | Preserve separately; no new full independent evidence for the inherited content |
| **FRAGMENT_OF / CONTAINS_FRAGMENT** | One unit is an excerpt/subset of another or shares a substantial exact region without representing the whole work | Shared region counts once; non-shared content evaluated separately |
| **RELATED_VARIANT** | Common template/lineage is plausible, but substantive changes create a meaningfully new solve/listen/write/speak instance | May be a separate content occurrence, but provenance dependence remains visible and can limit corroboration claims |
| **INDEPENDENT** | No evidence of common content origin beyond ordinary exam conventions/common public material | Full independent evidence subject to trust/relevance rules |
| **UNRESOLVED_DEPENDENCY** | Similarity suggests possible dependence but evidence is insufficient for a safe decision | Conservative production counting; review only when impact justifies it |

These are product meanings, not required enum names.

### Why `RELATED_VARIANT` is not a duplicate

A teacher may copy a task template but replace the passage, constraints, distractors, and correct response with genuinely new content. That is related authorship/style, not duplicate evidence of the specific item. Conversely, changing only names, dates, formatting, or one distractor while preserving the tested proposition and answer logic is a derivative copy.

Corpus should preserve the difference rather than treating all high semantic similarity as duplication.

## 3.3 Exact identity is stricter than near-duplicate similarity

**Decision:** An **exact duplicate** means that all meaning-bearing content relevant to the compared unit is the same after explicitly permitted normalization. It does not mean “very similar.”

At document/exam scope, exact-content identity requires all substantive represented exam content for the claimed scope to align. Different cover metadata, pagination, file container, fonts, or lossless transcoding can still be exact-content copies.

At Item scope, exact-content identity requires the same:

- tested stem/prompt content;
- referenced/shared stimulus identity or equivalent substantive stimulus content;
- response mechanic/cardinality;
- response options or answerable slots, after only semantics-preserving reordering where the source response rule makes order irrelevant;
- scoring-addressable structure.

**Answer-key assertions are deliberately not part of exact Item identity.** If two copies contain the same item but different claimed correct answers, Corpus must detect one item family and preserve a conflicting-answer dispute instead of incorrectly treating them as two independent questions.

Instructions are included in duplicate identity only when they alter response semantics, timing, cardinality, or what the candidate must do. Routine provider boilerplate is not sufficient to create or prevent an item match.

## 3.4 Near-duplicate means dependent content, not merely semantic resemblance

**Decision:** A near-duplicate/derivative relationship requires evidence of **common content origin**, not just similar meaning.

Examples that normally qualify:

- identical exam text retyped into HTML;
- PDF converted to DOCX with new branding;
- scan/OCR copy with minor OCR differences;
- copied task with names/dates lightly changed;
- copied question with distractor order changed;
- full exam with one page omitted;
- one task extracted from a larger exam;
- same listening recording transcoded or trimmed;
- same listening script re-recorded by another voice;
- copied prompt with annotations/explanations added.

Examples that do **not** qualify by similarity alone:

- two B1 appointment emails with independently written content;
- two reading tasks both testing a time restriction;
- two items using common TELC-like instruction wording;
- two questions on the same topic or skill;
- two independently authored passages with high-level semantic similarity;
- two speaking tasks asking the learner to plan an event but with materially different constraints.

Semantic similarity can generate a review candidate; it cannot by itself auto-collapse independent evidence.

## 3.5 Canonicalization has three different “preferred” concepts

**Decision:** Corpus must distinguish:

1. **Canonical provenance anchor** — the best-supported origin/identity of the underlying work or content family.
2. **Preferred processing representation** — the version that is most complete and extractable for parsing/analysis.
3. **Preferred downstream reusable representation** — if direct source use is ever allowed, the representation whose rights/product constraints permit that use.

These may be different observations.

Example: an official provider scan can be the canonical provenance anchor, while a clean text-native mirror is the preferred processing representation. If the mirror has unclear redistribution rights, it is still not automatically the preferred learner-facing representation.

This prevents deduplication from accidentally transferring provenance, rights, confidence, or usability across copies.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Comparison representations: preserve source truth and derive separate fingerprints

Every supported modality should conceptually keep two things separate:

- **preservation representation** — the raw/versioned source evidence and faithful extraction defined by earlier stages;
- **comparison representation(s)** — derived, explicitly versioned forms used only for fingerprinting/similarity.

A comparison-normalization change must never rewrite the source text/audio/image. Reprocessing can produce a new comparison fingerprint version while historical source evidence remains unchanged.

## 4.2 Text normalization before comparison

**Decision:** Text comparison uses conservative, meaning-preserving normalization first. The default comparison representation should normalize presentation noise while preserving German language features that can change exam meaning.

### Normalize by default

- Unicode normalization to a consistent canonical form;
- normalize line endings and collapse repeated insignificant whitespace;
- remove soft hyphens and confidently repair line-break hyphenation caused by page layout;
- normalize typographic quote/dash variants when they do not carry task semantics;
- case-fold for a secondary layout-insensitive fingerprint while retaining an original-case fingerprint;
- strip page numbers, repeated headers/footers, watermarks, navigation chrome, and download-site boilerplate **only when confidently identified as presentation noise**;
- normalize predictable OCR spacing artifacts;
- preserve source block/paragraph/item boundaries separately even if a flat comparison string is also produced;
- preserve both content order and an order-insensitive variant only where the task semantics allow reordering.

### Do not remove by default

- numbers, dates, prices, times, percentages, or units;
- negation (`nicht`, `kein`, etc.);
- modal verbs or particles that alter obligation/possibility;
- umlauts/ß or other German orthographic distinctions;
- punctuation that changes question/answer semantics;
- answer options, blank positions, labels, or content-point constraints;
- meaningful headings inside the tested material;
- spelling/grammar differences merely because a model considers them “equivalent.”

Stop-word removal, stemming, lemmatization, synonym replacement, and semantic paraphrase are **candidate-generation aids only**, not exact-identity normalization.

### OCR correction rule

Obvious OCR confusions may support a secondary fuzzy fingerprint, but uncertain OCR correction must not turn two different source strings into an automatic exact match. Visual/page evidence should corroborate an OCR-based duplicate decision.

## 4.3 Recommended document fingerprint layers

**Decision:** Document detection begins with cheap layered evidence, from strongest/cheapest to more interpretive.

1. **Raw payload fingerprint** — identifies byte-identical files immediately.
2. **Container-insensitive content fingerprint** — normalized extracted substantive text/content blocks, excluding presentation noise.
3. **Structural fingerprint** — sequence of normalized Sections/Tasks/Items, numbering patterns, block lengths, response mechanics, and stable content anchors.
4. **Local block/item fingerprints** — detects copied subsets when whole-document similarity is low.
5. **Fuzzy lexical fingerprint** — shingle/token overlap or equivalent cheap locality-sensitive comparison for candidate generation.
6. **Cross-format media evidence** — page-image/OCR fingerprints for scans; audio fingerprints/transcripts for listening components.
7. **Semantic escalation** — only for unresolved suspected paraphrases/derivatives whose decision matters.

The product does not require these exact algorithms; it requires an equivalent cheap-to-expensive layering.

## 4.4 Initial text similarity decision bands

The following are **starting product thresholds for long-enough text/document candidates**, to be validated against Stage 16. They are not universal algorithm constants and must not be reused blindly for short items.

| Candidate evidence | Starting decision posture |
|---|---|
| **100% substantive normalized match** plus compatible structure | `CONTENT_EXACT_COPY` unless contradictory source evidence shows otherwise |
| **≥98% substantive overlap** plus **≥95% structural/item alignment**, with no changed tested proposition, option meaning, response rule, or scoring structure | May auto-classify as `REFORMATTED_COPY` when comparison/extraction quality is high |
| **80–<98% substantive overlap**, or one artifact contains **≥90% of the smaller artifact's substantive content** in aligned order/context | `DERIVATIVE_COPY` / `FRAGMENT_OF` candidate; auto-link only when provenance or multiple cheap signals make common origin clear, otherwise review/unresolved |
| **60–<80% overlap** | Do not collapse whole documents automatically; review only with strong provenance/title/sequence/item-match evidence; continue item-level matching |
| **<60% whole-document overlap** | No whole-document duplicate action by similarity alone; exact copied tasks/items/assets may still be detected locally |

**Material semantic difference overrides numeric similarity.** A 99% match can still be a derivative/variant rather than exact if the changed 1% changes a correct answer, content point, restriction, score rule, or tested proposition.

## 4.5 Question/item similarity detection

**Decision:** Item matching is stricter than document matching because short exam text produces accidental similarity easily.

### Item identity components

Comparison should consider:

- normalized tested stem/prompt;
- canonical referenced Stimulus/content fingerprint;
- response mechanic/cardinality;
- options/slots/blank positions/matching targets;
- composite parent/child structure;
- local Task/Section context when useful;
- content-point constraints for Writing/Speaking prompts.

### Initial item decision bands

| Item evidence | Starting posture |
|---|---|
| All identity components exact after allowed normalization | `CONTENT_EXACT_COPY` |
| **≥95% substantive overlap** plus same stimulus/response mechanic/answerable structure and no changed tested proposition | May be `DERIVATIVE_COPY`; for short items auto-link only when exact anchors or parent/provenance evidence also match |
| **80–<95% overlap** with compatible structure | Near-duplicate candidate; review/semantic escalation only when impact matters |
| Semantic equivalence without strong lexical/structural/provenance evidence | Never auto-collapse; at most `UNRESOLVED_DEPENDENCY` or `RELATED_VARIANT` candidate |

For very short items, fixed percentages are unreliable. **Exact anchors, shared Stimulus identity, neighboring-item sequence, parent-document lineage, and response structure are required for automatic decisions.**

### Task-form-specific rules

- **Multiple choice:** option order may be normalized only if order has no source semantic/scoring meaning. Different option wording is derivative/variant evidence, not exact.
- **Matching:** label/order permutations may be superficial; the underlying target-option relationships and content must align.
- **Cloze:** same passage with same blank positions is a strong duplicate signal. Same passage with different blanks is a derivative/related variant, not the same Item set.
- **Shared passage, different questions:** duplicate the Stimulus only; the Items remain distinct.
- **Writing:** same scenario, recipient/register, and required content points with only surface/layout edits can be duplicate/derivative. Same topic alone is not enough.
- **Speaking:** same situation, roles, communicative goal, and constraints can indicate derivation; generic task form (“plan something together”) does not.
- **Conflicting answer keys:** preserve one Item-content family with multiple Answer assertions; do not split the Item to avoid the conflict.

## 4.6 Images and scans

**Decision:** Image/scan deduplication uses both visual and extracted-content evidence because file hashes fail after resizing, compression, rotation, cropping, screenshots, or rescanning.

Recommended low-cost layers:

1. raw byte fingerprint;
2. normalized visual/perceptual fingerprint tolerant of ordinary compression/resizing;
3. orientation/crop-aware page comparison;
4. OCR/text fingerprint when text is present;
5. layout/block-position evidence;
6. neighboring-page/Document sequence context.

### Classification rules

- Same page image with only compression/resolution/container change → `REFORMATTED_COPY` / exact-content copy.
- Same page photographed/scanned again with layout/content unchanged → reformatted copy when visual/OCR evidence supports it.
- Same page with handwritten answers, highlighting, watermark, added logo, or explanation overlay → `DERIVATIVE_COPY`; preserve the annotation as source-specific content.
- Cropped region from a larger page → `FRAGMENT_OF`, not whole-page exact duplicate.
- Same advertisement/photo/diagram reused in two otherwise independent tasks → Asset duplicate only. Do not collapse the Tasks/Exams without additional evidence.
- OCR differences alone do not establish independent content.

## 4.7 Audio duplicates and re-recordings

**Decision:** Audio identity separates **recording identity**, **spoken-script identity**, and **acoustic-condition evidence**.

Recommended low-cost layers:

1. raw byte fingerprint;
2. decoded/acoustic fingerprint robust to codec/bitrate/container/loudness changes and ordinary leading/trailing silence;
3. duration and segment alignment;
4. transcript fingerprint when a transcript/ASR is available;
5. Task/Item linkage and neighboring-track sequence.

### Classification rules

- Same recording transcoded MP3↔AAC, normalized for volume, or with harmless silence trimmed → `REFORMATTED_COPY`; one recording-content evidence unit.
- Same recording with intro/outro added → derivative or contained-fragment relationship for the shared speech region.
- Same script re-recorded by a different speaker → `DERIVATIVE_COPY`/shared-script relationship, **not** exact audio.
- Different audio using only common stock chime/music/noise → shared Asset fragment, not duplicate listening task.
- A clipped excerpt from a longer recording → `FRAGMENT_OF`.

### Metric-specific independence for re-recordings

A re-recorded script contributes:

- **no new independent script/content occurrence** for vocabulary/topic/task-content frequency by default;
- potentially **new acoustic evidence** for speech rate, speaker characteristics, clarity, noise, and listening difficulty when the recording is genuinely distinct;
- no extra corroboration of the original exam's provenance merely because somebody re-recorded it.

This is the clearest example of why independence cannot be one global duplicate flag.

## 4.8 Detecting reformatted and mirrored copies across formats

**Decision:** File type and URL/domain are weak evidence of independence. Cross-format comparison must operate on normalized substantive units.

A single underlying work can appear as:

- official PDF;
- mirrored PDF with changed metadata;
- scan of a printout;
- OCR-derived text PDF;
- DOC/DOCX retype;
- HTML transcription;
- screenshots/page images;
- forum/shared-document copy;
- ZIP member;
- individual-task excerpt.

Cross-format detection should therefore prioritize stable text/item sequence, shared Stimuli, response structures, visual fingerprints, audio fingerprints, distinctive phrase anchors, and provenance hints over filenames or MIME types.

**Filename/title similarity is candidate evidence only.** Renaming a file does not create independence; similar filenames do not prove duplication.

## 4.9 Canonical-record selection

**Decision:** Each exact-content family should have a stable canonical content identity plus preserved member records/observations. Canonical selection is reversible and must not break source references when a better origin is discovered later.

### Canonical provenance-anchor priority

Choose the best-supported origin using this order of preference:

1. verified original/provider/publisher observation for the exact work/version;
2. strongest established provenance to the original work when the original is unavailable;
3. complete, coherent, unmodified representation with the clearest authorship/edition evidence;
4. best-known representation when origin remains uncertain, explicitly marked provisional.

Do **not** choose canonical provenance solely because a copy is easier to parse, has broader usage rights, ranks higher in search, was discovered first, or has a cleaner filename.

### Preferred processing representation

For extraction/comparison, Corpus may separately prefer the member with:

- the most complete content;
- highest extraction quality;
- text-native structure over poor OCR where equivalent;
- intact assets and answer relationships;
- least annotation/tampering;
- easiest reliable segmentation.

A mirror can therefore be the best processing representation while the official/original observation remains the provenance anchor.

### Canonical Item/Task selection

Within an exact Item/Task family, prefer the version with the strongest provenance and most faithful/complete source content. Source-specific Answer assertions, explanations, annotations, rights, and confidence remain attached to their own evidence and are never silently imported into the canonical item as universal truth.

### Re-canonicalization rule

Discovering a better original may change the preferred anchor/representation, but:

- the content-family identity remains stable where possible;
- all previous observations remain linked;
- prior canonical-selection history remains auditable;
- analytics are recomputed only where the relationship/independence conclusion changed.

## 4.10 Preserve every source reference after deduplication

**Decision:** Deduplication never deletes or replaces Source Observations merely because they are duplicates.

For every known observation/member, Corpus must preserve conceptually:

- location/submission context and discovery path;
- first/last observation and availability history where available;
- raw/content fingerprints and comparison-method version;
- relationship to the canonical family/member;
- relationship confidence and review state;
- claimed provider/title/edition as observed;
- source-specific authenticity/confidence evidence;
- source-specific rights/terms evidence;
- source-specific annotations, answer assertions, or modifications;
- current/superseded/takedown state according to earlier stages.

A duplicate relationship can be corrected later without rewriting provenance history.

## 4.11 Derivatives and near-duplicates remain separate records

**Decision:** Exact/reformatted copies can share one underlying content identity; **derivatives are never destructively merged into that content record**.

A derivative should preserve, when discoverable:

- parent/common-ancestor relation and direction, or `direction_unknown`;
- which scope is shared: Document/Exam/Task/Item/Stimulus/Asset;
- change type: added, removed, reordered, substituted, translated, re-recorded, annotated, rebranded, reformatted, answer-modified, or unknown;
- affected tested propositions/options/content points;
- whether the derivative introduces genuinely new Items/Stimuli/claims;
- independence treatment for relevant analytics.

### Substantive-change rule

A derivative becomes a `RELATED_VARIANT` rather than “same item evidence” when the modifications require a materially new solve/response—for example a new passage proposition, changed constraint, changed blank, different distractor logic, different communicative content points, or distinct recording conditions.

It may then count as a separate **content occurrence** for some metrics while still remaining lineage-dependent for provenance/corroboration metrics.

## 4.12 Independent-evidence counting rules

**Decision:** Production analytics must expose and distinguish at least three conceptual counts when relevant:

1. **Observation count** — how many URLs/files/submissions/archive snapshots were seen.
2. **Canonical content occurrence count** — how many distinct Item/Task/Exam content occurrences remain after exact/reformatted copies are collapsed.
3. **Independent evidence count** — how many provenance/content families can responsibly be treated as independent for the metric/claim.

The default frequency/prevalence and corroboration logic uses **independent evidence**, not observation count.

### Core counting rules

| Situation | Default production counting |
|---|---|
| Same file mirrored on 10 URLs | Observation count = 10; underlying content/evidence contribution = 1 |
| Same exam converted PDF → DOCX → HTML | One underlying exam/content family |
| Full exam plus individual task excerpts | Excerpt adds no new occurrence for inherited task content; unique added material counts separately |
| Same item copied into several unofficial collections | One inherited content/evidence family unless independent authorship of new claims is established |
| Same shared passage used by five Items in one canonical exam | Stimulus content counted once at Stimulus scope; Item multiplicity remains real and Stage 11 decides the metric |
| Same passage reused in a second deliberately published exam edition | Separate publication/reuse can be reported, but exact underlying content is still one content family for independent-origin analysis |
| Lightly edited derivative preserving tested proposition | No new full independent evidence for that proposition |
| Materially new related variant | May be separate content occurrence; lineage-dependence remains available for corroboration/provenance metrics |
| Same script, new voice recording | One script/content family; potentially separate acoustic-difficulty evidence |
| Exact item with independently authored answer explanation | One item occurrence; explanation/answer claim may be independently corroborating **only if** its authorship/reasoning is genuinely independent |

### Confidence and relevance weighting order

Deduplication/independence is applied **before repeated evidence weights are summed**.

A cluster of ten mirrors does not get ten Stage 03 A/B/C weights. The underlying independent evidence unit receives the appropriate confidence/relevance treatment once. If a verified original is later found, it may improve the underlying work's provenance/confidence, but the mirrors still do not become independent corroboration.

Stage 11 owns final analytical formulas; it may not violate this invariant.

### Do not destroy real within-exam frequency

Deduplication prevents repeated **copies of the same exam** from multiplying analytics. It does not automatically collapse legitimate repeated occurrences inside one canonical exam. If a canonical exam independently contains the same vocabulary item six times, that is a real within-exam observation; Stage 11 decides how vocabulary frequency uses it.

## 4.13 Unknown independence and analytical uncertainty

**Decision:** When a candidate relationship is unresolved, production analytics should not pretend either full independence or certain duplication.

Corpus should be able to preserve an **independence range** conceptually:

- **minimum independent count** — assume unresolved candidate links are dependent;
- **maximum independent count** — assume they are independent.

For decision-grade claims, use the conservative side of the range or withhold/range-label the conclusion when the difference is material. Exploratory/operator views may show raw observations, likely clusters, and the range.

This approach is preferable to inventing fractional weights before benchmark calibration.

## 4.14 Review thresholds and escalation policy

**Decision:** Review effort is driven by both **similarity uncertainty** and **potential product impact**.

### Auto-accept duplicate relationships

Automatic exact/reformatted classification is appropriate when:

- byte/content identity is deterministic; or
- multiple high-quality cheap signals agree strongly (for example normalized text + structure, or perceptual page match + OCR),
- there is no conflicting evidence of material semantic change,
- extraction quality is sufficient for the comparison,
- the rule has met Stage 16 benchmark precision for auto-publication.

### Review / unresolved band

Route to review or keep unresolved when:

- similarity falls in the Stage 09 middle bands;
- short items lack enough lexical evidence;
- OCR/ASR uncertainty could explain the difference;
- provider/title/version claims conflict;
- an answer/scoring/content-point difference may be material;
- a candidate copy crosses formats in a way cheap signals cannot resolve;
- semantic paraphrase/common-origin is plausible but not textually obvious;
- a derivative direction or parent is unclear and the direction matters.

### Impact triggers for escalation

Prefer human/stronger-model review when an unresolved decision could:

- change a production frequency/prevalence ranking or learning-priority conclusion;
- create/remove independent A/B evidence for a TELC-specific claim;
- change authenticity corroboration materially;
- affect a high-TELC-relevance source family;
- collapse or split a cluster with several observations/domains;
- hide a disputed answer key or material content change;
- affect a benchmark/gold-standard record.

Low-impact C/D or exploratory material may remain `UNRESOLVED_DEPENDENCY` indefinitely with conservative influence rather than consuming expensive review.

## 4.15 False-positive and false-negative trade-off

**Decision:** For **automatic evidence collapse**, false positives are more damaging than false negatives, so auto-merge precision is prioritized.

Why:

- A false positive can hide genuinely independent exam evidence and distort provider/task prevalence downward.
- A false negative mirror can inflate frequency upward, but suspicious unresolved clusters can be conservatively bounded and revisited.
- Because relationships are non-destructive, both errors are correctable, but automatic collapse should still be strict.

### Product posture

- **Exact/strong reformatted copies:** aggressive cheap detection; very high precision expected.
- **Near-duplicates/derivatives:** conservative automatic classification; review/high-confidence evidence required for collapse into one evidence family.
- **Semantic similarity:** candidate generation only unless common-origin evidence is strong.
- **Unresolved high-impact candidates:** do not allow them to contribute several full independent units while waiting for resolution.

Stage 16 will set measurable target precision/recall using the annotated benchmark corpus. Stage 09 deliberately does not claim an unvalidated universal accuracy percentage.

## 4.16 Recommended low-cost detection stack

**Decision:** The default deduplication stack should be offline, cached, deterministic/local where practical, and progressively expensive.

| Layer | Purpose | Cost posture |
|---|---|---|
| **0. Provenance hints** | redirects, original/mirror links, archive ancestry, known source URLs, file names/sizes, package relationships | essentially free; hints only |
| **1. Exact payload fingerprints** | byte-identical file/asset detection | extremely cheap; always run |
| **2. Normalized content/structure fingerprints** | layout/container-insensitive exact copies | cheap; always run when extraction exists |
| **3. Fuzzy lexical/block/item candidate generation** | retypes, OCR drift, excerpts, partial overlap | cheap/local/batched |
| **4. Perceptual image + acoustic fingerprints** | scans/images/transcodes/crops/audio copies | local/batched; run only for relevant assets |
| **5. Cross-level alignment** | match document sections/tasks/items and detect copied subsets/variants | moderate local compute; run on candidates, not all pairs |
| **6. Local/open semantic similarity** | suspected paraphrases or common-origin variants missed lexically | optional, batched/cached, candidate-only |
| **7. Premium model or human review** | high-impact ambiguous lineage/semantic-change decisions | rare exception path |

The architecture may choose different techniques, but it should preserve this **cheap narrowing funnel** rather than comparing every pair with a paid model.

---

## 5. Edge Cases / Failure or Uncertainty Handling

### 5.1 Official provider reuses the same item in multiple publications

Do not treat the publications as mirrors if each is a genuine provider publication. Preserve both publication occurrences. The exact Item content still belongs to one content family for independent-origin analysis, while a separate “provider reuse/publication occurrence” measure can capture the fact that the provider deliberately reused it.

This prevents both extremes: claiming two independently authored items, or losing the fact that repeated official reuse may itself be strategically informative.

### 5.2 One mirror contains a cleaner or more complete copy than the original observation

Keep the original as provenance anchor when established. Use the cleaner mirror as preferred processing representation if it is demonstrably the same work and more extractable. Do not inherit the mirror's rights or claims into the original.

### 5.3 Mirror adds an answer key or explanation

The inherited question content still counts once. The added key/explanation is a new source-specific claim. It counts as independent answer corroboration only when evidence supports genuinely independent authorship/reasoning, not when it is simply copied from the same ancestor.

### 5.4 Same question, different claimed correct answer

Treat the question as duplicate/exact content and route the answer assertions into Stage 03's conflict model. Never split the question to make the conflict disappear.

### 5.5 Same passage, different questions

Deduplicate/share the Stimulus. Keep Items distinct. Vocabulary/topic analytics at Stimulus scope must not multiply the passage merely because several Items reference it.

### 5.6 Same item with option order shuffled

If option order has no semantic/scoring role, treat order-only change as reformatting/derivative rather than new evidence. If labels/order matter to matching/scoring, preserve the distinction.

### 5.7 Same text but changed number/date/negation

These are meaning-bearing changes and can change the correct response. The unit is not exact-content identical. It is at most a derivative/related variant depending on whether the tested proposition remains effectively the same.

### 5.8 Common boilerplate creates false similarity

Provider instructions, copyright lines, standard exam directions, “Lesen Sie den Text…”, answer-sheet labels, and recurring headers are downweighted/excluded from substantive similarity. Boilerplate alone can never collapse two Items/Exams.

### 5.9 Two independent authors use the same public-domain/source passage

Shared Stimulus identity does not imply the Items are duplicates. Preserve one/shared source passage relationship if appropriate, but compare the independently authored questions/tasks separately. Independence of the task claims remains possible.

### 5.10 One exam is a composite assembled from several sources

Do not collapse the entire composite into one parent. Match copied Tasks/Items locally, preserve new/unique content, and represent multiple lineage relationships. Analytics count each inherited unit according to its originating family.

### 5.11 OCR/ASR method improves later

Recompute comparison representations/fingerprints and revisit affected relationships. A changed extraction fingerprint does not mean the source version changed. Relation decisions remain versioned/auditable.

### 5.12 Source removed or takedown requested

Apply Stage 04. Deduplication metadata and non-reconstructive prevention fingerprints may remain only to the extent Stage 04 permits. If a canonical provenance anchor is removed from active content retention, another member may become the preferred processing representation without fabricating a new origin.

### 5.13 A duplicate candidate is never worth resolving

Keep it unresolved and conservative. Bestehen is a personal project; not every ambiguous pair deserves semantic-model or human cost. Resolution effort is reserved for material that affects production intelligence.

---

## 6. Relationship to Other Bestehen Stages

### Stage 02 — Source Strategy

Stage 02 discovers and preserves observations. Stage 09 determines when those observations refer to the same or dependent underlying content. Discovery breadth must therefore never become frequency breadth automatically.

### Stage 03 — Trust, Authenticity, and Confidence

Stage 09 provides the independence prerequisite for corroboration and aggregate weighting. Mirrors/derivatives cannot raise confidence by repetition. Independent source-specific claims may still corroborate locally when their authorship is genuinely independent.

### Stage 04 — Rights and Usage

Rights stay attached to each source/material component. Deduplication never transfers permission. Canonical provenance, preferred processing copy, and reusable copy are separate choices.

### Stage 05 — Canonical Exam Model

Deduplication operates at Document, Exam, Task, Item, Stimulus, Answer-claim, and Asset scope rather than only whole-file scope. This prevents one copied Task from forcing two otherwise different exams into one record.

### Stage 06 — Taxonomy

Similar tags do not imply duplicate content. The taxonomy helps characterize related variants but cannot be used alone to collapse evidence.

### Stage 07 — Difficulty and Relevance

Difficulty/TELC relevance may be estimated for every record, but aggregate influence must first respect Stage 09 independence. Re-recorded audio is the key example where script independence and acoustic-difficulty independence differ.

### Stage 08 — Ingestion and Extraction

Stage 09 supplies the detailed Deduplicate state between Validate and Review/Publish. The pipeline should publish relationship/independence status with enough lineage for downstream analytics.

### Stage 10 — Validation and QA

Stage 10 should validate broken/circular cluster relationships, canonical-member integrity, benchmark precision/recall, and regression behavior for deduplication decisions.

### Stage 11 — Corpus Analytics

Stage 11 must define each metric's denominator/evidence unit explicitly and use independent/canonical evidence rather than URL count. It may report raw observation count separately, but it cannot let mirrors multiply production prevalence.

### Stage 12 — Corpus → App Contract

The App normally needs corpus patterns and aggregate intelligence, not raw duplicate graphs. Where source/reference material is exposed internally or debugging/provenance is relevant, the contract should expose canonical identity, provenance, rights, and confidence without requiring App to redo deduplication.

### Stage 13 — Operations

Duplicate review needs an operator view for candidate pairs/clusters, side-by-side differences, provenance, canonical selection, relation confidence, unresolved-impact priority, and reversible corrections.

### Stage 14 — Cost and Automation

Stage 14 should budget mostly local/deterministic dedup processing. Paid semantic review is an exception path and should be measurable/capped.

### Stage 16 — Benchmark Corpus

The benchmark must contain known exact copies, cross-format reformats, scans/OCR variants, excerpts, short-item collisions, derivative variants, shared stimuli, audio transcodes, re-recordings, and genuinely independent look-alikes. Stage 16 calibrates thresholds and establishes target precision/recall.

---

## 7. Cost Notes

Stage 09 has **low recurring cost** if implemented according to the product policy above. Deduplication is offline Corpus processing and does not require any per-learner call.

### Preferred low-cost default

- cryptographic/content hashes for exact copies;
- normalized deterministic text/structure fingerprints;
- local fuzzy candidate generation rather than all-pairs semantic comparison;
- local perceptual image/acoustic fingerprints;
- cached item/block fingerprints reused across reprocessing;
- batch candidate alignment;
- optional local/open embeddings only for unresolved candidate pairs;
- human or premium-model review only for high-impact ambiguity.

### What would justify higher spend later

A stronger semantic model is justified only when the unresolved candidate could materially change production analytics, TELC-specific conclusions, confidence corroboration, or benchmark quality and cheaper signals cannot resolve it.

Even then, the result should be cached/versioned so the same pair is not repeatedly billed. No Stage 09 decision requires always-on AI, per-item paid embeddings, or per-user inference.

---

## 8. Decisions Made

1. Deduplication is non-destructive and operates on relationships/clusters rather than deleting provenance records.
2. Observation identity, content identity, derivative lineage, and analytical independence are separate product concepts.
3. Exact duplicates are stricter than similarity: meaning-bearing content must match after conservative normalization.
4. Reformatted copies count as one underlying evidence unit even when format, layout, scan quality, or hosting changes.
5. Near-duplicates/derivatives remain separate records and preserve their deltas/lineage.
6. Document fingerprinting uses a cheap layered approach: raw hash → normalized content/structure → fuzzy/block/item/media comparison → semantic escalation only when needed.
7. Item matching includes tested prompt/stimulus/response structure but deliberately excludes claimed correct-answer assertions from identity so key conflicts remain visible.
8. Text normalization removes presentation noise but preserves German meaning-bearing features such as negation, numbers, dates, umlauts/ß, options, blank positions, and constraints.
9. Images/scans use visual + OCR/layout evidence; audio separates recording identity from script identity and acoustic evidence.
10. Cross-format retypes, scans, OCR copies, HTML copies, and excerpts can be linked despite different file types/URLs.
11. Canonical provenance anchor, preferred processing representation, and preferred reusable representation are separate selections.
12. Every known source reference survives deduplication with its own provenance, trust, rights, claims, and observation history.
13. Production analytics use independent evidence rather than source-observation count and apply confidence/relevance weighting only after deduplication.
14. Independence is metric-specific; derivative material can be dependent for one metric and legitimately distinct for another.
15. Unresolved dependency is bounded conservatively rather than granted full independent weight.
16. Automatic collapse prioritizes precision; ambiguous near-duplicates are reviewed only when product impact justifies the cost.
17. Initial text similarity bands are provisional and must be calibrated against Stage 16's annotated benchmark.
18. No paid/always-on AI is required for normal deduplication.

---

## 9. Open Questions / Deferred Decisions

### Owner questions

**None.** The Stage 09 product decisions can be made responsibly from the established project principles.

### Deferred to architecture/implementation

The following are intentionally not product decisions:

- exact cryptographic, MinHash/SimHash/shingle, perceptual-image, or acoustic-fingerprint algorithms/libraries;
- physical cluster/edge/index schema;
- ANN/search technology;
- exact OCR/ASR normalization implementation;
- batch/queue scheduling and parallelization;
- local embedding model choice;
- premium-model/provider choice if semantic escalation is ever used;
- storage/retention representation for fingerprints.

### Deferred to later shaping stages

- **Stage 10:** production QA metrics and regression checks for dedup decisions.
- **Stage 11:** final formulas/denominators for each aggregate analytic, within the independence invariants defined here.
- **Stage 13:** duplicate-review operations UX.
- **Stage 14:** concrete scale/cost targets and processing budget.
- **Stage 16:** benchmark examples, target dedup precision/recall, and recalibration of the provisional similarity bands.

These deferrals do not block any Stage 09 checklist item.

---

## 10. Definition of Done Check

- [x] Document fingerprinting is defined conceptually with low-cost layered fingerprints and provisional decision bands.
- [x] Question/item similarity detection is defined, including short-item safeguards and task-form-specific rules.
- [x] Text normalization rules distinguish presentation cleanup from meaning-changing transformations.
- [x] Duplicate image/scan handling is defined using visual, OCR, layout, crop, and annotation relationships.
- [x] Duplicate audio handling distinguishes exact recording copies, transcodes, excerpts, re-recordings, and script/acoustic independence.
- [x] Reformatted/mirrored copies are detectable across format/host boundaries and cannot manufacture independence.
- [x] Canonical-record selection distinguishes provenance anchor, processing representation, and reusable representation.
- [x] All known source references and source-specific trust/rights/claims remain preserved after deduplication.
- [x] Aggregate analytics count independent evidence rather than mirrors, with observation/content/independent counts kept distinct.
- [x] Exact-copy, reformatted-copy, derivative, fragment, related-variant, independent, and unresolved concepts have starting thresholds/rules.
- [x] Review thresholds and false-positive/false-negative trade-offs are explicit.
- [x] Cheap deterministic/local processing is the default; semantic AI/human review is impact-triggered.

**Stage 09 is product-complete when later architecture can implement duplicate detection without inventing what counts as the same evidence, what survives canonicalization, how derivatives behave, or how mirrors are prevented from distorting analytics.**
