# Bestehen / Corpus — Stage 02: Source Strategy

> **Status:** Authoritative Stage 02 product-shaping decision  
> **Product:** Bestehen / Corpus  
> **Initial domain:** German A2–B1 exam and exam-style material  
> **Primary downstream customer:** Bestehen / App  
> **Target signal:** TELC B1 is strongest, while source discovery remains deliberately broader than TELC

## 1. Purpose and Scope

This stage defines **where Bestehen / Corpus looks for evidence, which source classes are strategically valuable, which content formats may enter the product, how automated discovery and manual submission coexist, and how sources remain traceable when URLs move, disappear, or appear in multiple places**.

The source strategy exists to make Stage 01's broad A2/B1 mission operational without turning Corpus into an uncontrolled web crawler or a public archive. Corpus should search broadly enough to discover useful official and unofficial exam evidence, but ingest selectively according to exam relevance, provenance quality, expected analytical value, and maintenance cost.

This is a product strategy, not a crawler or storage architecture. It does not choose a search provider, crawling framework, queue, database, file store, OCR engine, browser automation stack, or hosting model. Later architecture should implement the rules below without weakening the source breadth, provenance, cost, or access boundaries established here.

### 1.1 Source-strategy objective

**Bestehen / Corpus should maintain a curated, coverage-driven source universe that combines authoritative originals with useful secondary and unofficial evidence, accepts both automated and manual intake, and permanently preserves the lineage of every observation even when the live source later changes or disappears.**

### 1.2 What this stage does not decide

This stage deliberately does not assign final authenticity/confidence scores, rights statuses, deduplication thresholds, parsing accuracy requirements, retention periods for raw bytes, or crawler implementation details. Those belong to later Corpus stages.

However, source strategy must capture enough information that those later decisions are possible. In particular, discovering a source must never erase whether it was official, mirrored, manually supplied, archived, incomplete, or no longer live.

## 2. Inputs / Existing Decisions

Stage 02 preserves the following established decisions from the product overview, identity, App shaping context, Corpus checklist, and `corpus/01-product-mission-and-boundaries.md`:

- Corpus is an **exam-data and intelligence product**, not a learner-facing content library or generic scraper.
- Its initial acquisition domain is **German A2, B1, and mixed A2–B1 exam material**. A1 is not an initial acquisition target.
- TELC B1 is the strongest target signal, but Corpus intentionally includes TELC A2–B1, Goethe A2/B1, ÖSD A2/B1, DTZ A2–B1, and other credible A2/B1 exam-style material.
- Official and unofficial sources are both potentially useful.
- **Authenticity/confidence and usage rights are independent.** Source category is evidence about provenance; it is not itself a rights decision or a complete confidence score.
- Corpus material is evidence first. Presence in Corpus does not mean source content is safe or desirable to surface directly in Bestehen / App.
- Independent evidence matters more than repeated mirrors. Alternate URLs must be preserved without inflating frequency analysis.
- Unknowns remain explicit. A source may be incomplete, unattributed, unavailable, or ambiguous and still be worth preserving for later review.
- Corpus is internal-first and should remain financially sustainable as a personal project. Stable source intelligence should be gathered and processed incrementally rather than requiring expensive work per learner interaction.

No contradiction with Stage 01 is introduced by this stage. Stage 02 makes its source-discovery boundary concrete.

## 3. Decisions and Rationale

### 3.1 Source categories and strategic priority

**Decision:** Corpus uses seven required source categories. They are ranked by **default acquisition priority and expected analytical value**, not by an assumed final authenticity score.

A source category answers “where did this candidate come from and what kind of evidence might it provide?” Stage 03 will answer “how strongly should we trust this material?” Stage 04 will answer “what may we do with it?” Those questions must not be collapsed.

| Priority | Source category | Examples of source role | Primary Corpus value | Default acquisition posture |
|---|---|---|---|---|
| **P0** | **Official exam providers** | TELC, Goethe, ÖSD and official DTZ-related provider/authority material | Best evidence for real format, instructions, scoring context, official model tests and provider-specific behavior | Exhaustively discover relevant public A2/B1 resource areas within the bounded provider scope; revisit most actively |
| **P1** | **Established educational publishers** | Reputable exam-prep publishers, textbook companion material, public samples | High-quality authored practice, broader task variants, explanations and progression evidence | Targeted discovery of public A2/B1 exam-prep material; prioritize samples and resources with clear provenance |
| **P1** | **Language schools and teachers** | Established schools, recognized teachers, course resource pages, teacher-authored mocks | Useful realistic practice, common learner-facing task patterns, alternative explanations and local exam-prep material | Curated discovery; favor sources with identifiable authorship/institution and coherent exam structure |
| **P1/P2** | **Public repositories and archives** | Public code/document repositories, institutional archives, web archives, openly indexed collections | Historical material, vanished sources, alternate formats, rare assets, provenance corroboration | Search deliberately for known exam/provider terms; treat repository/archival hosting separately from claimed original authorship |
| **P2** | **Unofficial exam collections** | Public mock-test collections, exam-prep sites, compiled PDFs, community collections | Breadth where official supply is sparse; potentially strong structural evidence despite weaker origin | Include when materially relevant; require provenance/confidence handling and deduplication awareness rather than blanket exclusion |
| **P3** | **Forums and shared documents** | Public forum posts, public shared documents, public community links | Leads to rare material, answer discussions, fragments, corroboration, historical availability | Discovery-heavy but ingestion-selective; treat claims and embedded files as candidates, not automatically as independent evidence |
| **P2** | **Individual exam-style exercises** | Standalone reading, listening, cloze, writing or speaking tasks | Useful evidence for task patterns, vocabulary, grammar, distractors, skills and difficulty even without a full exam | Accept when genuinely exam-shaped and A2/B1 relevant; do not treat isolated exercises as full-exam structure evidence |

#### Priority interpretation

- **P0/P1 means “look here first,” not “automatically trust or reuse.”**
- A P2 unofficial mock can later receive high confidence if Stage 03 evidence supports it.
- A P0 official PDF can still be restricted/reference-only under Stage 04.
- A public archive may host an exact copy of an official file; the archive is an observation location, not a second independent exam.
- An individual exercise can be strategically valuable for skill intelligence while being weak evidence for whole-exam frequency or provider format.

### 3.2 Value is multidimensional, not a single source ranking

**Decision:** Acquisition priority is driven by the source's likely contribution to one or more evidence goals:

1. **Target fidelity** — does it directly reveal TELC B1 behavior?
2. **Cross-provider comparison** — does it help distinguish TELC-specific patterns from generic A2/B1 behavior?
3. **Progression evidence** — does it help explain A2→B1 development?
4. **Structural coverage** — does it cover underrepresented sections, task types, answer keys, scoring rules, or media relationships?
5. **Skill/content breadth** — does it add useful vocabulary, grammar, topic, distractor, reasoning, writing, or speaking evidence?
6. **Historical/resilience value** — does it preserve evidence no longer available at its original location?
7. **Corroboration value** — does it independently support or challenge a claim found elsewhere?

This prevents a simplistic policy in which full official model tests are considered the only valuable material. Official material remains the anchor, but the broader corpus exists because the App needs more evidence than the small official sample set alone can provide.

## 4. Detailed Product Model / Rules for this Stage

### 4.1 Discovery principles applying to every category

Corpus discovery follows these rules regardless of source class:

1. **Prefer origins over copies.** When an official/original publisher location can be identified, it is the preferred provenance anchor even if a mirror is easier to fetch.
2. **Search broadly; ingest selectively.** Discovery may produce many candidates. A candidate only enters meaningful Corpus processing when it appears relevant enough to the A2/B1 exam domain to justify cost and review burden.
3. **Coverage drives exploration.** Discovery effort should target weak cells in the coverage matrix rather than maximizing URLs visited.
4. **Source class does not equal confidence.** Category and claimed provider are recorded inputs to later confidence evaluation, not final trust labels.
5. **Public reachability does not equal reuse permission.** Discovery and rights evaluation are independent.
6. **No access circumvention.** The initial product does not require bypassing authentication, paywalls, bot protections, access controls, or private-group boundaries in order to meet coverage goals.
7. **Manual evidence is first-class.** Material supplied directly by the owner can enter the same provenance and review model as web-discovered material.
8. **Partial material is allowed.** A fragment, audio file, answer key, scanned page, or single task may be useful even when the full exam is absent.
9. **Mirrors are observations, not extra evidence by default.** Multiple URLs may point to one underlying document/exam and must remain linkable.
10. **Discovery is reproducible enough to audit.** Corpus should retain how a candidate was found: seeded source, targeted query, link traversal, archive lookup, manual URL, or manual file submission.

### 4.2 Discovery approach by source category

#### A. Official exam providers — P0

Corpus should maintain an explicit registry of the in-scope official provider families and their known public exam/resource areas. Discovery should use:

- provider resource/download pages;
- model-test and exam-preparation sections;
- provider search results and site navigation;
- public sitemaps or equivalent resource indexes where available;
- links from official exam descriptions to PDFs, audio, answer keys, scoring material and supporting assets;
- targeted web search queries for provider + exam + level + section/resource terms when provider navigation is incomplete;
- archived copies only as a resilience/historical supplement when an original page/file is gone or changed.

**TELC-specific rule:** TELC B1 receives the most active and complete discovery treatment because it defines the learner-facing target. Corpus should still retain separate TELC A2–B1 and cross-provider discovery so target fidelity is not confused with generic B1 evidence.

The product should not crawl unrelated sections of an official provider's site simply because the domain is trusted.

#### B. Established educational publishers — P1

Discovery should target publishers with identifiable German A2/B1 exam-prep offerings using:

- public catalog/product pages that link to companion materials;
- downloadable public sample chapters, worksheets, mock exams, audio samples and answer material;
- publisher resource portals and teacher/student companion pages;
- targeted search queries combining publisher name, exam family, CEFR level, “Modelltest”, “Prüfung”, “Übung”, “Hörverstehen”, “Leseverstehen”, “Schreiben”, “Sprechen”, and related terms;
- manual seeding when a useful title or resource is found outside automated discovery.

Paid or account-gated products may be recorded as known candidates or manually supplied when the owner lawfully possesses them, but Corpus does not require automated paywall/account circumvention.

#### C. Language schools and teachers — P1

Discovery should favor identifiable institutions/authors over anonymous exercise farms. Methods include:

- targeted searches for school/teacher resources tied to TELC, Goethe, ÖSD, DTZ, A2 or B1;
- public lesson-resource, exam-preparation and blog pages;
- linked PDFs, worksheets, audio and video on the same public site;
- public teacher-resource hubs and public profiles that clearly identify authorship;
- manual submission of high-value teacher materials discovered through normal browsing.

The value of this category is breadth and realism, not assumed officiality. Claims such as “original exam” or “real TELC questions” are captured as claims and assessed later rather than accepted at face value.

#### D. Public repositories and archives — P1/P2

Discovery should use repositories and archives for **finding and preserving evidence**, not for treating hosting location as proof of authorship. Methods include:

- repository search for exam/provider/level terms and recognizable file names;
- archive search for known original URLs that are dead or materially changed;
- public institutional libraries/document archives;
- collections linked from reputable exam-prep or teaching resources;
- manual lookup of historic versions when current official resources have been replaced.

Each archived or repository-hosted copy should retain both its immediate host and any claimed/original source relationship that can be established. An archive snapshot is a historical observation of a URL, not automatically a new source work.

#### E. Unofficial exam collections — P2

Discovery should use targeted queries and curated link expansion rather than unrestricted crawling. Useful approaches include:

- searches for exam family + level + model test/mock/sample terms;
- searches for section-specific material where coverage is weak;
- links from already accepted unofficial sources to closely related public resources;
- known public exam-prep collection sites;
- manual submission of credible collections found by the owner.

A collection may be valuable even when its rights are unclear or its claim of authenticity cannot yet be verified. Such material can enter a candidate/review path without gaining strong analytical influence automatically.

#### F. Forums and shared documents — P3

This category is useful primarily for **lead generation, fragments, historical clues and corroboration**. Discovery should include:

- public, search-indexed forum threads relevant to in-scope exams;
- public shared documents reachable without requesting access;
- public links from discussions to files or original sources;
- targeted searches for rare resource names, missing answer keys, historic model tests or disputed materials.

Corpus should not depend on private groups, closed communities, credential sharing or access-request automation. A forum post that points to a file should preserve the forum post as discovery provenance while separately identifying the file's host/origin where possible.

#### G. Individual exam-style exercises — P2

Standalone exercises are discoverable through:

- targeted section/task searches;
- publisher, teacher and school resource pages;
- public exercise portals with clearly exam-shaped A2/B1 tasks;
- links from broader exam-prep articles;
- manual submission.

They are usable when they reveal a recognizable exam skill/task/content pattern. They should be labeled as standalone material so later analytics do not infer that they represent the full balance of a real exam.

### 4.3 Automated discovery and manual submission are both required

**Decision:** Bestehen / Corpus requires **both automated discovery and manual URL/file submission** from the beginning of the product concept.

They solve different problems:

| Intake path | Purpose | Why it is required |
|---|---|---|
| **Automated discovery** | Repeatedly find candidates from known domains, targeted searches, resource indexes and bounded link neighborhoods | Prevents the corpus from becoming a one-time hand-curated set and makes freshness/coverage maintainable |
| **Manual URL submission** | Let the owner add a public page/file immediately | Captures discoveries from normal browsing, recommendations, search results, communities and sources not worth automating |
| **Manual file submission** | Let the owner supply a file already lawfully obtained | Supports scans, downloaded documents, email/teacher materials, local archives, renamed files, gated material the automated system should not access, and assets with no durable public URL |

All three paths must converge on the same conceptual provenance model. Manual material is not “untracked trusted content”; its submission origin, filename, supplied context and any claimed source URL/provider must be recorded.

Manual submission should permit optional operator notes such as claimed exam/provider, level, source page, why the material seems valuable, and whether it is known to be incomplete. Missing optional notes do not make a file unusable; they increase uncertainty for later review.

### 4.4 Supported source/content formats

**Decision:** All formats listed in the Stage 02 checklist are supported as **accepted Corpus inputs**. “Supported” at product level means Corpus may register, preserve provenance for, and attempt to derive evidence from the format. It does not require identical automation quality across every format in the first implementation.

| Format | Initial product support | Typical evidence | Product rules |
|---|---|---|---|
| **HTML** | Required | Instructions, exercises, answer pages, provider descriptions, embedded assets, metadata | Preserve page URL and observation time; linked assets may become separate related observations |
| **PDF** | Required | Model tests, worksheets, answer keys, scoring guides, scans, full exams | Both text-native and scanned PDFs are valid inputs; extraction quality may differ and must remain visible later |
| **DOC/DOCX** | Required | Teacher materials, shared mocks, worksheets, answer keys | Preserve original document provenance and structure where possible; do not assume author metadata is trustworthy without review |
| **Images/scans** | Required | Scanned pages, photographed exercises, notices, forms, advertisements, answer sheets | A single image may be a usable fragment; OCR/extraction mechanics belong to Stage 08 |
| **Audio** | Required | Listening passages, announcements, conversations, prompts | Preserve relationship to source page/document and any linked question set; transcription/alignment is Stage 08 |
| **Video** | Required | Listening/speaking practice, recorded model tasks, embedded exam-prep material | Video may contribute audio, transcript, visual prompt or instructional evidence; automated extraction depth can be phased |
| **ZIP/archive files** | Required | Bundled tests, audio sets, documents, answer keys, image collections | Treat the archive as a container observation while preserving provenance for extracted members; archives do not erase member-level lineage |

Plain text/Markdown and common metadata sidecars may also be accepted as low-complexity ancillary inputs if convenient, but they are not required to define Stage 02 completion.

### 4.5 What constitutes a usable source

A source is **usable for Corpus intake** when all of the following product conditions hold:

1. **Relevance:** It contains or plausibly leads to German A2/B1 exam or exam-style evidence.
2. **Traceability:** Corpus can record at least a submission origin or discovery location. Perfect original attribution is not required at intake, but “came from nowhere” is not acceptable.
3. **Accessible acquisition:** It can be obtained through normal public access or manual owner submission without requiring the product to defeat access controls.
4. **Recognizable content:** The retrieved material is a supported format and is not merely an unrelated placeholder/error payload.
5. **Potential evidence value:** It contains at least one useful exam signal—structure, instructions, task/item content, answer material, scoring guidance, media, topic/skill patterns, or credible provenance/corroboration information.
6. **Safe enough to quarantine/process:** Suspect or malformed files may be retained in a non-published state for review, but unsafe content must not be treated as successfully ingested simply because it downloaded.

A source **does not need** to be complete, official, unique, redistributable, or high-confidence in order to be usable for intake. Those properties determine later treatment, not whether the evidence can be recorded at all.

### 4.6 Candidate, observed source, and underlying material are distinct concepts

**Decision:** The source strategy distinguishes three conceptual layers before the canonical exam model is defined:

- **Candidate:** a URL/file lead that may contain relevant material but has not yet been accepted as a useful observation.
- **Source observation:** a particular public URL, archive snapshot, repository object, or manual submission observed at a particular time.
- **Underlying material:** the document/exam/task/asset that one or more observations may represent.

This distinction is essential for mirror handling and freshness. Two URLs can be separate observations of the same PDF. One URL can change over time and expose different versions. A manually uploaded file can match an official source found later.

Stage 05 will define canonical exam entities; Stage 09 will define duplicate and derivative relationships. Stage 02 only requires that discovery not collapse these distinctions prematurely.

### 4.7 Initial source breadth without uncontrolled crawler scope

**Decision:** Initial breadth is defined by **representative coverage across the agreed domain**, not by crawling the open web exhaustively.

Corpus should maintain a coverage view across at least:

- exam/provider family: TELC B1, TELC A2–B1, Goethe B1, Goethe A2, ÖSD B1, ÖSD A2, DTZ A2–B1, other credible exam-style material;
- level: A2, B1, mixed A2–B1;
- major section/skill: reading, language elements where applicable, listening, writing, speaking;
- source class: authoritative, established educational, and selected unofficial/community evidence;
- media/formats where materially relevant: document/web, image/scan, audio and video.

The initial personal-project acquisition strategy is therefore **seeded and bounded**:

1. Start with known official providers and high-value reputable sources.
2. Expand through targeted searches for under-covered provider/level/section cells.
3. Follow relevant links from accepted source neighborhoods, not every link on the host domain.
4. Add public repository/archive searches for missing/historical evidence.
5. Use unofficial collections and public forums/shared documents selectively when they fill a real coverage or corroboration gap.
6. Accept manual URLs/files at any time.
7. Reduce discovery effort in cells where additional sources mostly produce duplicates or low-value variants, and redirect effort toward under-covered cells.

**Explicit non-goal:** Corpus does not require a recursive web-wide crawler, exhaustive crawling of every trusted domain, or continuous indexing of all German-learning content.

A later Stage 14 may assign numerical source/document targets and crawl budgets. Stage 02 locks the optimization target: **coverage gain per unit of processing/review effort**, not URL count.

### 4.8 Source revisit and freshness model

**Decision:** Corpus revisits sources according to **source importance, expected volatility, and current availability**, not one global crawl cadence.

The product-level default cadence is:

| Source state/class | Default revisit target | Rationale |
|---|---|---|
| **High-value official TELC/provider resource indexes and current model-test pages** | About every **30 days** | Target format/resources can change and these sources have high strategic importance |
| **Other active official sources and established publisher/school resource hubs** | About every **90 days** | Useful freshness without constant polling |
| **Stable direct documents/assets whose parent source is unchanged** | About every **180 days**, or sooner when the parent page changes | Binary assets are usually less volatile than indexes/pages |
| **Unofficial collections, repositories, archives, forums/shared documents** | About every **180 days** when still useful; more often only if high-value/volatile | Controls personal-project cost and avoids repeatedly crawling noisy sources |
| **Known unavailable/dead observations** | Retry on a short decay path, then about every **180 days** or when a new lead appears | Allows recovery from temporary failures without wasting ongoing requests |

These are **product defaults, not scheduling architecture**. A later implementation may use change signals, cache validators, manual triggers, source-specific overrides, or more efficient mechanisms.

Revisiting should answer:

- is the source still reachable?
- did the URL redirect or move?
- did the content materially change?
- did linked assets/answer keys appear or disappear?
- is a newer version/edition now available?
- did source metadata relevant to confidence or rights change?

A revisit that sees no material change should not trigger expensive full reprocessing by default. Stage 14 will refine batching/caching economics; Stage 08 will define reprocessing behavior.

### 4.9 Version/change behavior

**Decision:** Corpus does not silently overwrite history when a source changes materially.

- Minor transport/presentation changes that do not change the underlying evidence may update the current observation status.
- Materially changed content should create or preserve a distinguishable observation/version relationship so earlier derived intelligence remains explainable.
- When an official provider replaces an old model test with a newer one at the same URL, Corpus should be able to know that both versions were observed.
- A “latest” source may be preferred for current exam-format analysis while older material remains useful as historical evidence with appropriate relevance weighting later.

The exact version-detection mechanism is an architecture/deduplication decision. The product requirement is non-destructive lineage.

### 4.10 Mirrors and alternate URLs

**Decision:** Corpus preserves **all known meaningful observation URLs** while preferring an identifiable original/provider URL as the provenance anchor when available.

For mirrors/alternates:

1. Record each observed URL/location independently.
2. Record relationships such as **original/provider location**, **mirror/repost**, **archive snapshot**, **alternate official URL**, **redirected/moved URL**, or **relationship unknown** when supportable.
3. Never treat the count of mirrors as independent corroboration by default.
4. Prefer the official/original location for current-source identity when it exists, but retain mirrors for resilience and historical traceability.
5. A mirror may become the only currently fetchable copy after the original disappears; this does not erase the original provenance.
6. If two locations contain modified variants, preserve the uncertainty until Stage 09 decides whether they are exact duplicates, near-duplicates/derivatives, or independent material.
7. Alternate URLs may be used as acquisition fallbacks where allowed, but downstream analytics should reason over underlying evidence rather than raw URL count.

### 4.11 Redirects and moved resources

Permanent or stable redirects should create a **moved/alias relationship**, not a brand-new independent source. Corpus should retain:

- the originally discovered URL;
- the resolved destination;
- when the move was first observed;
- whether the destination appears to be the same underlying material.

Redirect chains that lead to an unrelated page, login wall, generic homepage, or error page should not be accepted as successful freshness checks.

### 4.12 Dead, removed, or inaccessible URLs

**Decision:** A dead URL is a provenance state, not a deletion instruction.

When a previously useful URL becomes unavailable:

- keep its source observation and lineage permanently unless a later legal/rights/security rule requires stronger deletion;
- record that it is currently unavailable, moved, access-restricted, or failed for another reason rather than collapsing every failure into “deleted”;
- retain the last successful observation metadata and relationships needed to explain already-derived intelligence;
- look for a new official location, known alternate URL, or public archive snapshot when the source is strategically valuable;
- do not make repeated dead-link retries a high-cost background workload;
- do not automatically delete structured metadata merely because the public URL disappeared.

A **takedown/rightsholder removal request** is different from an ordinary 404/410 or website redesign. Stage 04 will define whether raw content and/or derived metadata must be removed in such cases.

### 4.13 Permanent provenance expectations

**Decision:** Source provenance is permanent even when raw files are later removed, URLs die, rights statuses change, or records are deduplicated.

At minimum, Corpus must preserve enough lineage to answer:

- **Where was this found?** Original submitted/discovered location, including URL/repository/archive/manual-file origin.
- **How was it found?** Official seed, targeted discovery, link traversal, archive lookup, manual URL, or manual file submission.
- **When was it observed?** First discovery and later successful/failed checks relevant to source history.
- **Who/what claimed authorship or provider?** Site/publisher/author/provider claims as observed, without silently upgrading claims to verified facts.
- **What was observed?** Resource name/title, media/content type, filename when applicable, and enough stable identity to relate later observations.
- **What did it resolve to?** Redirected/canonical/alternate location relationships.
- **How does it relate to other observations?** Potential original, mirror, archive copy, version, bundle member, related answer key/audio, or unknown relationship.
- **Which downstream data came from it?** Later structured exams/tasks/items/assets and derived intelligence must retain lineage back to source observation(s).
- **What happened later?** Availability changes, reclassification, removal, replacement, or provenance corrections must not erase the historical trail.

“Permanent provenance” does **not** require keeping every raw copyrighted byte forever. Raw-content retention, takedown deletion, and security retention rules belong to Stages 04 and 15. The invariant is that Corpus should not lose the historical fact that a piece of evidence existed, where it came from, and what downstream records depended on it, except where law/policy explicitly requires removal of that metadata too.

### 4.14 Provenance corrections do not rewrite history

If the operator later learns that a source previously attributed to “TELC” was actually a teacher-created mock, Corpus should correct the current attribution while preserving an audit/history trail that the prior claim existed and was changed. Later analytics should use the corrected current interpretation, but historical explainability remains intact.

### 4.15 Bundles and related assets

A single source page or ZIP may contain a test booklet, answer key, audio tracks, transcripts, image prompts and scoring material. Corpus should preserve both:

- the **container/source relationship** that explains how the assets were distributed together; and
- the **individual asset provenance** needed to link each derived task/item to the correct source evidence.

An audio file found on a mirror and a booklet found on the provider site may later be linked as a set, but that relationship should be evidence-based rather than assumed solely from similar filenames.

## 5. Edge Cases / Failure or Uncertainty Handling

### 5.1 Official file found only through a mirror

Accept the mirror as a source observation and preserve any credible claimed original/provider reference. Do not label the mirror itself as official hosting. Search for the provider origin when worthwhile; confidence remains a Stage 03 decision.

### 5.2 Public shared document with no clear author

It may enter as a low-provenance candidate/observation if the content is relevant. Record the sharing URL and discovery context; do not invent authorship. Its analytical influence will be bounded later by confidence and deduplication rules.

### 5.3 File manually uploaded with no source URL

Accept it when the owner has a legitimate copy and it is relevant. Record manual submission, filename, submission time, owner notes/claimed provider if supplied, and mark original location as unknown. A later discovered public/original copy can be linked without losing the manual observation.

### 5.4 Password-protected or account-gated file

Automated discovery may record that the candidate exists, but the initial product does not require bypassing the gate. If the owner lawfully acquires and manually submits the file, it can enter through manual intake with that acquisition context.

### 5.5 Paywalled publisher resource

The catalog/page may be useful provenance, but Corpus does not need automated access to the paid content. Free sample material is discovered normally. Purchased material may be manually submitted if appropriate; reuse rights remain separately assessed.

### 5.6 Video with useful listening content but no downloadable audio

Treat the video itself as supported evidence. It can remain partially processed until Stage 08 defines extraction/transcription. Lack of an audio-only asset does not make it unusable.

### 5.7 ZIP contains mixed relevant and irrelevant material

Preserve the bundle provenance. Relevant members may proceed; irrelevant members need not contribute to the corpus. The archive is not evidence that every contained file is independently authored or independently sourced.

### 5.8 Same URL serves a new document later

Preserve separate observation/version history when the underlying evidence materially changes. Do not overwrite the old record and make old analytics inexplicable.

### 5.9 Source changes only styling or download wrapper

Do not treat cosmetic page changes as new exam evidence. Re-fetch/reprocessing depth should reflect meaningful content change, not HTML churn.

### 5.10 Mirror has a clearer scan than the original copy

The mirror may be preferred as an extraction asset while the original remains the preferred provenance anchor. “Best bytes for processing” and “best source-of-origin evidence” are allowed to differ.

### 5.11 Dead official URL with archived snapshot

Keep the official URL as the historical origin and the archive snapshot as a separate observation/resilience location. The archive does not become the author/provider.

### 5.12 Forum thread contains answer-key disagreement

Preserve the thread as contextual/corroborative evidence if useful, but do not silently replace the source answer key. Conflicting-answer handling is a Stage 03/10 concern.

### 5.13 Search result leads to unrelated generic German content

Reject it as a candidate once relevance is clear. Corpus is not a general German-learning index.

### 5.14 High-volume exercise site produces thousands of near-identical items

Do not ingest volume merely because it is available. Sample/ingest according to coverage value and marginal information gain until Stage 14 sets concrete volume targets and Stage 09 handles similarity.

### 5.15 Source contains both A2/B1 and B2 material

Preserve the source context, but only A2/B1-relevant material should count toward initial coverage/analytics. Do not expand automated discovery into the provider's B2 ecosystem by default.

## 6. Relationship to Other Bestehen Stages

Stage 02 establishes inputs and lineage; later stages decide how those inputs are judged, transformed and consumed.

- **Stage 03 — Authenticity and Confidence:** uses source category, origin claims, officiality, corroboration and structural evidence captured here, but must not equate category with final confidence.
- **Stage 04 — Rights and Usage Metadata:** decides whether discovered/observed content may be stored, transformed, redistributed or surfaced. Public discovery alone grants no rights.
- **Stage 05 — Canonical Exam Model:** formalizes source/document/exam/task/item/asset entities and must support multiple observations and partial materials.
- **Stage 06 — Taxonomy:** classifies the evidence discovered here across provider, level, section, task, topic, grammar, vocabulary and skills.
- **Stage 07 — Difficulty and TELC Relevance:** weights broad source evidence toward the TELC B1 learner target without discarding useful cross-provider signals.
- **Stage 08 — Ingestion Pipeline:** implements the candidate → fetch → normalize/parse/enrich/review lifecycle and defines OCR, transcription, partial failures and reprocessing.
- **Stage 09 — Deduplication:** determines whether mirrors/versions/derivatives represent the same underlying evidence and prevents URL multiplicity from becoming false frequency.
- **Stage 10 — Validation and QA:** determines whether accepted observations were extracted correctly and remain structurally usable.
- **Stage 11 — Analytics:** uses independent, quality-bounded evidence rather than source URL counts.
- **Stage 12 — Corpus → App Contract:** exposes source/rights/provenance only where needed while primarily serving structured intelligence and original-practice grounding.
- **Stage 13 — Operations:** should provide source registry, candidate/review visibility, manual URL/file intake, freshness status, source controls and provenance correction workflows.
- **Stage 14 — Cost, Scale and Automation:** assigns concrete source/document volume targets, crawl budgets, batching, caching and rate-limit rules to the bounded strategy defined here.
- **Stage 15 — Security and Abuse:** hardens untrusted URLs/files and decides raw-file retention/security behavior.
- **Stage 16 — Benchmark Corpus:** should intentionally include the format and source diversity required here, including official and imperfect unofficial evidence.
- **Stage 17 — Final Specification:** must preserve the source categories, dual automated/manual intake, bounded breadth and permanent lineage defined in this stage.

### Relationship to Bestehen / App

The App should not need to discover or scrape exam material. Corpus absorbs the complexity of fragmented sources, provenance, mirrors and freshness, then exposes stable intelligence. This supports the App's exam-coach identity: learner interactions can be based on evidence without depending on live third-party pages or repeated source processing during a session.

## 7. Cost Notes

Source discovery has meaningful cost risk because an unconstrained crawler can create network, storage, extraction and AI-processing work much faster than it creates useful evidence.

### Preferred low-cost default

The initial personal-project default is:

- a curated registry of official/high-value source families;
- targeted searches and bounded link expansion rather than web-wide recursion;
- coverage-gap-driven acquisition rather than URL-volume goals;
- manual URL/file intake for rare or inconvenient sources;
- slow revisits for stable/low-value sources and more frequent revisits only for strategically important current official resources;
- change detection/caching before expensive reprocessing wherever implementation allows;
- no premium AI requirement for source discovery itself;
- no automatic processing of every discovered candidate before basic relevance/provenance gating;
- no recurring per-learner source fetches.

### Cheaper fallback when automation is not worth it

For a small number of high-value or awkward sites, **manual seeding/rechecking is an acceptable product fallback**. Automating a fragile source is not mandatory if the corpus can achieve representative coverage more cheaply and reliably through manual intake.

### What would justify higher spend later

Higher discovery/processing spend is justified only when measured coverage or freshness gaps materially weaken Corpus intelligence—for example, missing current TELC assets, underrepresented listening/speaking material, or repeated manual work across many similarly structured high-value sources.

Concrete monthly budgets, volume targets, crawl-rate limits, storage expectations and processing cost per 1,000 items belong to Stage 14.

## 8. Decisions Made

1. Corpus uses seven explicit source categories: official exam providers; established educational publishers; language schools/teachers; public repositories/archives; unofficial exam collections; forums/shared documents; individual exam-style exercises.
2. Official exam providers are the highest acquisition priority; TELC B1 receives the strongest discovery attention while cross-provider breadth remains intentional.
3. Source category/acquisition priority is **not** a confidence score and never implies reuse rights.
4. Every source category has an explicit discovery approach; discovery is targeted, coverage-driven and bounded rather than web-wide.
5. Corpus requires **automated discovery, manual URL submission, and manual file submission** as complementary first-class intake paths.
6. HTML, PDF, DOC/DOCX, images/scans, audio, video and ZIP/archive files are all required supported input formats.
7. Partial/incomplete material is usable when it contributes real exam evidence and retains uncertainty.
8. A usable source must be relevant, traceable at least to discovery/submission origin, acquired without access circumvention, recognizable, and potentially valuable as exam evidence.
9. Candidate leads, observed source locations and underlying material are distinct concepts so mirrors and changing URLs do not erase lineage.
10. Initial breadth is measured by representative provider/level/section/source/format coverage, not URL count or exhaustive crawling.
11. Source revisits are importance/volatility-based: roughly monthly for the most important official target pages, quarterly for other active high-value sources, and semiannually for stable/lower-value sources by default.
12. Material source changes preserve version/observation history rather than silently overwriting prior evidence.
13. Mirrors, redirects, alternates and archive snapshots remain distinct provenance observations and do not count as independent evidence by default.
14. Dead/removed URLs remain permanently traceable; disappearance alone does not delete their derived structured intelligence.
15. Provenance must permanently connect downstream records back to where/how/when source evidence was observed, while raw-byte retention remains a later rights/security decision.
16. The preferred personal-project strategy is curated seeding + targeted automated discovery + manual intake + selective revisits, with expensive processing only after relevance gating.

## 9. Open Questions / Deferred Decisions

### Owner questions

**None.** The available product context is sufficient to define the Stage 02 source strategy without requiring an owner preference or legal-risk decision.

### Deliberately deferred product-detail decisions

The following are intentionally left to their dedicated stages and do not block Stage 02:

- final confidence dimensions, source tiers and influence thresholds — **Stage 03**;
- exact rights/usage statuses, takedown behavior and derived-metadata deletion rules — **Stage 04**;
- canonical data hierarchy and exact representation of source observations/documents/exams/assets — **Stage 05**;
- duplicate/near-duplicate thresholds and canonical-record selection — **Stage 09**;
- extraction QA and production-ready criteria — **Stage 10**;
- numerical source/document/item targets and processing budgets — **Stage 14**;
- safe file sandboxing, URL sanitization and raw-file retention periods — **Stage 15**.

### Architecture/implementation decisions intentionally not made here

Search engine/provider choice, crawler framework, browser automation, robots/rate-limit implementation, scheduling technology, queues, storage, HTTP cache strategy, file hashing method, archive extraction library, OCR/transcription tools, embeddings, model vendors and databases remain open.

The product does require respectful bounded acquisition and no access circumvention; Stage 14/15 and architecture must turn those principles into concrete technical controls.

## 10. Definition of Done Check

- [x] Official exam providers are defined as a source category and prioritized.
- [x] Established educational publishers are defined as a source category and prioritized.
- [x] Language schools and teachers are defined as a source category and prioritized.
- [x] Public repositories and archives are defined as a source category and prioritized.
- [x] Unofficial exam collections are defined as a source category and prioritized.
- [x] Forums and shared documents are defined as a source category and prioritized.
- [x] Individual exam-style exercises are defined as a source category and prioritized.
- [x] Discovery methods are defined for every source category.
- [x] HTML is a supported input format.
- [x] PDF is a supported input format, including scanned PDFs.
- [x] DOC/DOCX is a supported input format.
- [x] Images/scans are supported input formats.
- [x] Audio is a supported input format.
- [x] Video is a supported input format.
- [x] ZIP/archive files are supported input formats.
- [x] Automated discovery/crawling is required within a bounded, coverage-driven scope.
- [x] Manual URL submission is required.
- [x] Manual file submission is required.
- [x] Source revisit/freshness behavior is defined.
- [x] Mirror and alternate-URL handling is defined.
- [x] Dead/removed URL handling is defined.
- [x] Permanent provenance expectations are defined.
- [x] Initial personal-project breadth is defined without requiring an uncontrolled crawler.
- [x] Cost-sensitive source-discovery defaults and cheaper manual fallbacks are documented.
- [x] No Stage 02 owner question remains unresolved.

**Stage 02 is product-complete when the live Corpus checklist matches the decisions above.**