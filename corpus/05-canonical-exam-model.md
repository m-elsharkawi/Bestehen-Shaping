# Bestehen / Corpus — Stage 05: Canonical Exam Model

> **Status:** Authoritative Stage 05 product-shaping decision  
> **Product:** Bestehen / Corpus  
> **Initial domain:** German A2–B1 exam and exam-style material  
> **Primary downstream customer:** Bestehen / App  
> **Core principle:** Represent what the source actually contains and how the exam actually behaves, without forcing provider-specific structure into a TELC-shaped schema or inventing missing material.

## 1. Purpose and Scope

This stage defines the **canonical conceptual exam model** for Bestehen / Corpus: the common language Corpus uses to describe exam evidence gathered from TELC, Goethe, ÖSD, DTZ, publishers, teachers, unofficial collections, archives, and standalone exam-style material.

The model must be broad enough to represent:

- a complete official model exam distributed as a booklet, answer key, audio tracks, and scoring guide;
- a modular exam whose reading, listening, writing, and speaking components behave differently from TELC;
- a teacher-created mock with several sections in one document;
- one standalone reading task on a web page;
- a fragment consisting only of an audio file and three questions;
- a scan with a missing page;
- a detached answer key that is discovered later;
- matching, cloze, multiple-choice, multiple-correct-answer, short-answer, writing, and speaking tasks;
- tasks that share one passage, image, table, form, advertisement, or audio track;
- mixed-rights and mixed-confidence components within the same exam package.

This is a **product model, not a database schema**. It defines the concepts and relationships the product requires. It deliberately does not choose tables, collections, graph edges, IDs, storage engines, serialization formats, APIs, ORM classes, extraction models, or indexing technology.

### 1.1 Stage objective

**Bestehen / Corpus should be able to represent any supported A2/B1 exam as faithful, composable evidence: source observations lead to concrete documents and assets; documents contribute to exams or fragments; exams contain optional structural layers down to answerable items; shared tested content, instructions, answers, explanations, media, and scoring remain separately addressable and traceable.**

### 1.2 Why a canonical model is necessary

Without a canonical model, each provider or source format would leak its own vocabulary and layout into downstream analytics. TELC might call a unit a `Teil`, another provider might call it an `Aufgabe` or a module, a publisher might use only numbered exercises, and an unofficial PDF might omit section labels entirely. If Corpus treated those literal labels as the data model, later stages would have to write provider-specific logic for every analysis.

The canonical model therefore separates three things:

1. **generic exam semantics** — concepts that apply across providers, such as exam, section, task, item, stimulus, answer, and scoring rule;
2. **provider-native presentation** — the source's original labels, numbering, grouping, timing, and provider-specific rules;
3. **normalized taxonomy** — later Stage 06 classifications such as Reading, Listening, task type, skill, topic, grammar, and strategy.

The source wording is preserved; the generic model makes it comparable; the taxonomy makes it analyzable.

### 1.3 What this stage does not decide

This stage does not decide:

- the Stage 06 taxonomy vocabulary or exact task-type list;
- numerical difficulty or TELC relevance;
- ingestion/extraction algorithms;
- duplicate thresholds;
- validation accuracy targets;
- physical persistence or API shape;
- current provider-format verification for every provider/version;
- final scoring calculators for the App;
- learner attempts, learner answers, coaching feedback, or learner readiness.

Those later decisions must use this model rather than replacing it with provider-specific structures.

---

## 2. Inputs / Existing Decisions

This stage preserves the product overview, identity, App checklist, live Corpus checklist, and Corpus Stages 01–04.

### 2.1 Stage 01 — mission and boundaries

`corpus/01-product-mission-and-boundaries.md` established that:

- Corpus is an exam-data and intelligence product whose primary customer is Bestehen / App;
- its initial acquisition domain is German A2, B1, and mixed A2–B1 material;
- TELC B1 is the strongest target signal, while the corpus remains intentionally cross-provider;
- canonical representation must preserve source, exam, section, task, item, answer, instruction, shared passage, scoring information, and media relationships;
- incomplete material may remain useful but must not be made artificially complete;
- Corpus evidence and learner-facing practice are separate products.

### 2.2 Stage 02 — source strategy and provenance

`corpus/02-source-strategy.md` established that:

- **candidate leads, observed source locations, and underlying material are distinct concepts**;
- one source page or ZIP may distribute a booklet, answer key, audio, transcripts, image prompts, and scoring material together;
- multiple source observations may point to the same underlying work;
- one exam may be assembled from related material observed at different locations;
- source versions and materially changed documents must remain distinguishable;
- partial material and standalone exercises are valid Corpus evidence;
- downstream structured records must retain lineage to the source observations from which they were derived.

The canonical model therefore cannot treat `URL = document = exam`.

### 2.3 Stage 03 — authenticity and confidence

`corpus/03-trust-authenticity-confidence.md` requires confidence at **source, document, exam/test-set, task, and item/question** levels. Local evidence may diverge from parent confidence. A trusted exam may contain one disputed item; an incomplete exam may contain intact trusted tasks.

The canonical model must therefore let uncertainty and review state attach at the smallest relevant unit. Answer-key conflicts must be localizable rather than forcing the whole exam into one trusted/untrusted state.

### 2.4 Stage 04 — rights and usage

`corpus/04-rights-and-usage-metadata.md` requires rights metadata to attach to source/material/component scopes and supports inheritance only where license scope justifies it. Text, audio, images, answers, and other components may have different rights. Takedown must be able to remove the smallest defensible affected component while preserving non-reconstructive intelligence where permitted.

The canonical model therefore must keep material components separately addressable rather than embedding every source expression inside one indivisible exam object.

### 2.5 App boundary

Bestehen / App owns learner attempts, responses, coaching, generated practice, learner evaluation, and readiness. Corpus owns the **reference exam model and evidence**.

An `Answer` in this document means a source/reference answer, accepted response, answer-key assertion, or scoring-relevant reference associated with corpus evidence. It does **not** mean a learner's answer. Learner-response modeling belongs in the App.

---

## 3. Decisions and Rationale

## 3.1 Use a stable generic hierarchy plus reusable supporting entities

**Decision:** The canonical hierarchy is:

**Source Observation → Document → Exam / Test Set → Section → Part (optional) → Task → Item / Question → Answer / Scoring**

with **Instruction, Stimulus, Response Option, Explanation, Scoring Rule/Rubric, and Asset** as separately addressable supporting concepts that may be shared or attached at the level where they actually apply.

This is intentionally not a strict tree from top to bottom. The **structural exam hierarchy** is tree-like where useful, but source/document/assets have many-to-many relationships with exams and tasks because real material is distributed across files and reused across questions.

### Why not use one rigid tree?

A rigid tree fails common cases:

- one PDF contains the booklet while another contains the key;
- one MP3 track serves ten listening items;
- one passage is shared by five reading items;
- one answer key covers the entire exam;
- one document contains two separate mock tests;
- one scan contains only pages 7–10 of a larger exam;
- one task uses a text plus a separate image asset;
- the same official document is observed from an original URL and several mirrors.

The canonical model therefore keeps **structural containment** separate from **evidence/provenance relationships**.

## 3.2 Define the hierarchy by semantic responsibility, not visual layout

A PDF heading, page break, box, or number does not automatically determine an entity. Entities are created because the unit has a stable exam meaning.

For example:

- a page heading may denote a Section, a Part, or merely presentation;
- a numbered question containing three separately scored subquestions may become one composite Item with three child items;
- five numbered statements responding to one shared passage are five Items under one Task;
- a writing prompt may be one Task with one productive Item even if the page contains several bullet points;
- a listening track is an Asset/Stimulus, not a Section merely because it is stored separately.

**Rule:** preserve source numbering and labels, but normalize by function.

## 3.3 Keep provider-native structure without making it canonical structure

Every structural entity may preserve its original provider/source label and order, for example `Leseverstehen`, `Lesen`, `Teil 1`, `Aufgabe 2`, `Hören`, `Modul Schreiben`, or a publisher's own terminology.

The generic entity remains `Section`, `Part`, `Task`, or `Item`. Provider labels are evidence, not schema names.

This lets Corpus compare providers without pretending they have identical exam designs.

## 3.4 Treat shared tested material as a first-class Stimulus

**Decision:** Tested material that one or more items depend on is represented through a first-class **Stimulus** concept rather than copied into every question.

A stimulus can be:

- a reading passage;
- several short texts;
- an audio segment or whole track;
- a video segment;
- an image;
- a table;
- a form;
- a notice/sign;
- an advertisement;
- a chart/diagram;
- a composite of text plus visual/media elements;
- a speaking prompt card or situation description.

A stimulus may be used by one task, many tasks, one item, or many items.

This prevents shared passage/audio duplication from distorting text frequency, rights lineage, confidence, or removal behavior.

## 3.5 Separate instructions from tested content

**Decision:** Instructions are a distinct functional concept from tested content.

The distinction is based on **what the candidate must do with the text**, not typography.

- **Instruction:** tells the candidate how to perform, select, write, listen, speak, use time, or record an answer.
- **Stimulus/tested content:** contains information the candidate must comprehend, infer from, transform, respond to, or use to earn points.
- **Prompt/stem:** can combine both roles. The model must be able to mark the tested semantic portion separately when the distinction matters.

Instructions should not normally influence vocabulary/grammar/topic frequency as though they were tested language. They may still inform exam-format, strategy, timing, and task-shape analytics.

## 3.6 Define an Item as the smallest response/scoring-addressable unit

**Decision:** An Item/Question is the smallest unit to which a candidate response and scoring outcome can be meaningfully attached.

That definition is more durable than “whatever has a printed number.”

Examples:

- one multiple-choice question = one Item;
- one true/false statement = one Item;
- one cloze blank scored independently = one Item;
- one matching target requiring one match = one Item;
- one question asking “select two correct answers” = one Item with response cardinality two, unless the source explicitly scores each selection independently;
- one writing assignment can be one productive Item even if it has four required content points;
- one speaking interaction task can be one productive/interactive Item with rubric dimensions rather than one objective answer.

## 3.7 Support composite and multi-part items without over-fragmenting

**Decision:** Items may have **parent/child composition** when a visually single question contains independently answerable/scorable subparts.

Use a composite parent when it preserves source structure or shared wording. Child items represent the independently response/scoring-addressable parts.

Do **not** split a multiple-correct-answer question into several fake true/false questions merely to simplify storage. Preserve the source's actual response rule and scoring behavior.

## 3.8 Treat scoring as evidence, not a property hidden inside answers

**Decision:** Scoring rules/rubrics are first-class supporting concepts attachable at Exam, Section, Part, Task, or Item scope.

This is necessary because scoring can include:

- point values;
- all-or-nothing rules;
- partial credit;
- penalties or no-penalty rules;
- selection cardinality;
- section totals;
- rubric dimensions;
- performance bands;
- pass-related constraints;
- rounding/conversion rules;
- provider-specific scoring notes.

Stage 05 preserves the source rule and its scope. Later App/readiness stages decide how to use verified scoring evidence for learner simulation.

## 3.9 Model incompleteness explicitly rather than as extraction failure alone

**Decision:** Every relevant structural level can represent whether it is complete, partial, or of unknown completeness.

A partial exam is not necessarily a bad record. It may be high-value evidence for the material that exists.

The model distinguishes:

- `complete` — evidence supports that the represented unit is complete for its claimed scope;
- `intentional_excerpt` — the source intentionally provides only part of a larger exam or sample;
- `incomplete_known_missing` — evidence shows expected components are missing;
- `completeness_unknown` — Corpus cannot responsibly determine whether more material should exist.

Missing dependencies are recorded explicitly, such as missing page, missing answer key, missing audio, missing transcript, missing scoring guide, missing instruction, or detached/unlinked component.

Corpus must never generate a missing page, key, score, task, or audio relationship merely to make the exam look complete.

## 3.10 Use provider-specific extensions only for irreducible provider semantics

**Decision:** The model has a **generic core** and allows provider-specific extensions at the exam/section/part/task/item/scoring level only when the generic model cannot faithfully express a meaningful provider-specific rule.

Provider extensions must follow these rules:

1. preserve provider-native semantics without changing the generic hierarchy;
2. never duplicate data already expressible generically merely for convenience;
3. remain namespaced/conceptually isolated from the generic model;
4. not become a dependency for generic cross-provider analytics;
5. be promotable into the generic model later if the concept proves broadly useful across providers;
6. preserve the original source/provider terminology that justified the extension;
7. carry provenance, confidence, and rights context like any other source-derived claim.

Examples of appropriate extension candidates include provider-specific module-certification behavior, special scoring conversions, or delivery rules that do not generalize. Exact extension storage syntax is an architecture decision.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Source Observation

### Definition

A **Source Observation** records a place/context where Corpus observed or received material. It is the provenance entry point, not the exam itself.

Typical examples:

- an official provider resource page;
- a direct PDF URL;
- a repository path;
- an archive snapshot;
- a mirror URL;
- a public shared document;
- a manually submitted file;
- a purchased/authorized owner copy submitted manually.

### Required conceptual behavior

A Source Observation can:

- point to one or many Documents/Assets;
- have its own observed availability, discovery route, source claims, rights evidence, and source-level confidence;
- be related to another observation as original, mirror, archive, redirect, alternate, version lead, or unknown relationship;
- remain as provenance even if the underlying raw material is later removed, subject to Stage 04's stronger takedown rules.

### Important distinction

**Different URLs are not different exams by default.** Source Observation answers “where/how was this seen?”, while Document/Exam answer “what material was seen?”

## 4.2 Document

### Definition

A **Document** is a concrete, versioned content-bearing artifact or coherent artifact unit from which structured exam evidence can be extracted.

Examples:

- exam booklet PDF;
- answer-key PDF;
- scoring guide;
- HTML exercise page;
- DOCX mock exam;
- transcript document;
- scanned page set;
- an extracted member of a ZIP whose content is independently meaningful.

Audio/image/video bytes are normally modeled as **Assets** rather than Documents unless they themselves function as the primary coherent source artifact and need document-level provenance/version behavior. The physical implementation may store them similarly; the conceptual distinction is about role.

### Relationships

A Document may:

- contain one complete exam;
- contain multiple exams/test sets;
- contain only one Section, Task, or fragment;
- contain only an answer key or scoring material;
- contribute to an Exam together with other Documents/Assets;
- have multiple Source Observations;
- have material versions/editions that must remain distinguishable.

### Document completeness

Document completeness describes the artifact itself: pages missing, scan cropped, file truncated, etc. It is separate from Exam completeness. A complete answer-key PDF can belong to an incomplete exam package.

## 4.3 Exam / Test Set

### Definition

An **Exam / Test Set** is the coherent assessment package or exam-shaped set that the source presents as belonging together for a provider, level, edition/version, mock, module set, or standalone assessment context.

It is the main unit for whole-test structure analysis.

### It may be

- a complete model exam;
- a complete mock exam;
- a set of independently deliverable modules presented as one provider practice set;
- a mixed A2–B1 test set;
- an intentionally partial provider sample;
- an incomplete reconstructed package whose missing components are known;
- an unofficial exam claiming a provider style, with authenticity/confidence handled separately.

### Relationships

An Exam may span:

- several Documents;
- multiple Assets;
- one or more Sections;
- exam-level Instructions;
- exam-level Scoring Rules;
- provider-specific extension metadata.

One Document may contribute to several Exams if, for example, a workbook contains multiple mock tests.

### Full-exam inference rule

A collection of tasks does not become a full Exam merely because it appears in one PDF. Corpus should only claim whole-exam/test-set structure when the source evidence supports that grouping.

## 4.4 Section

### Definition

A **Section** is a top-level functional division of an Exam/Test Set.

Examples include provider-native divisions corresponding conceptually to reading, language elements, listening, writing, or speaking. Stage 06 will define the normalized section taxonomy.

### Section rules

- Preserve the provider's native section/module name.
- Allow a section to be independently deliverable or scorable when the provider's exam design requires it.
- Do not require every provider to have every section.
- Do not invent a `Language Elements` section for providers that integrate grammar/vocabulary differently.
- Allow section-level instructions, timing, scoring, assets, and completeness.
- Section order is source/provider metadata, not a universal canonical order.

## 4.5 Part

### Definition

A **Part** is an **optional** structural subdivision within a Section that groups one or more Tasks according to the source/provider's exam organization.

It commonly corresponds to native labels such as `Teil`, `Aufgabegruppe`, or a named subpart, but it is not mandatory.

### Why Part is optional

Some providers and standalone exercises have no useful layer between Section and Task. Requiring a Part would manufacture meaningless `Part 1` containers.

### Part rules

- Preserve provider/source label and order when present.
- A Part can own shared instructions, shared stimuli, time/scoring context, or provider-specific metadata.
- A Task may belong directly to a Section when no meaningful Part exists.

## 4.6 Task

### Definition

A **Task** is a coherent candidate activity with a shared instruction/response pattern, usually containing one or more Items and often one or more shared Stimuli.

Examples:

- match five texts to a set of headings;
- answer five questions about one passage;
- listen to one announcement and judge several statements;
- fill ten gaps in one text;
- write an email responding to four required content points;
- plan an activity with a speaking partner;
- choose several correct statements from a list.

### Task owns or links to

- task-level Instructions;
- one or more Stimuli;
- Items;
- shared Response Options where applicable;
- task-level Scoring Rules;
- time/playback/response-mode facts when source-defined;
- provider-native label/number;
- completeness and confidence/review state.

### Task boundary rule

Create a new Task when the candidate's instruction, response mode, shared stimulus context, or scoring logic materially changes. A page break alone does not create a new Task.

## 4.7 Item / Question

### Definition

An **Item** is the smallest response/scoring-addressable unit within a Task.

### Common item forms

- single-select choice;
- true/false or yes/no decision;
- cloze blank;
- matching target;
- short response;
- multiple-select response;
- ordered response;
- productive written response;
- productive spoken response;
- interactive spoken response;
- composite item with child items.

The exact normalized task/item taxonomy is Stage 06.

### Item relationships

An Item may reference:

- all Task stimuli by default;
- a specific Stimulus or stimulus segment;
- item-specific prompt/stem;
- item-specific Response Options;
- one or more Answers/reference answers;
- item-level Scoring Rule;
- an Explanation;
- child Items if composite;
- local confidence/rights/review overrides where appropriate.

## 4.8 Multi-part and composite questions

Multi-part behavior is represented according to scoring semantics.

### Pattern A — independently scored subparts

Example source shape:

> 12. Read the notice.  
> a) Where?  
> b) When?  
> c) How much?

If a/b/c are separately answerable/scored, represent:

- one composite parent Item preserving printed question `12` and shared prompt context;
- three child Items `12a`, `12b`, `12c`, each with its own answer/scoring relationship.

### Pattern B — one response requires several selections

Example:

> Choose **two** statements that are correct.

Represent **one Item** with:

- a choice set;
- required/allowed selection cardinality;
- an accepted correct set;
- scoring rule defining all-or-nothing or partial credit.

Do not create fake independent items unless the source actually scores each choice separately.

### Pattern C — productive task with required content points

A writing task saying “address these four points” remains one productive Item if the provider scores one integrated response. The four points are **task requirements/rubric criteria**, not four objective Items unless the source scoring truly treats them as independently answered units.

## 4.9 Instruction

### Definition

An **Instruction** is source content whose primary function is to tell the candidate how to perform the assessment.

Instruction scopes may include:

- exam-wide;
- section;
- part;
- task;
- item;
- audio/playback;
- administration/proctoring;
- answer-sheet/response-format guidance.

### Instruction roles

Corpus should be able to distinguish at least conceptually:

- candidate instruction;
- example/demonstration instruction;
- timing instruction;
- playback/repetition rule;
- response-format instruction;
- scoring-relevant constraint;
- administrative/proctor note.

### Tested-content boundary

The same sentence cannot be classified solely from style. For example:

- “Lesen Sie den Text und wählen Sie die richtige Antwort.” is an instruction.
- “Sie dürfen die Wohnung nur werktags besichtigen.” inside an advertisement is tested stimulus content.
- “Nennen Sie zwei Gründe, warum Sie nicht kommen können.” is part instruction and part response requirement; its requirement must remain scoring-visible even if the wording is stored as an instruction/prompt.

### Analytics rule

Instruction text is excluded from normal tested vocabulary/topic/grammar frequency by default. It may contribute to task-format, exam-strategy, timing, and instruction-language analysis.

## 4.10 Stimulus

### Definition

A **Stimulus** is the tested source material or situation that a candidate must interpret or respond to.

### Stimulus forms

- passage;
- collection of short texts;
- dialogue/transcript concept;
- audio segment;
- image/photo;
- table;
- form;
- notice/sign;
- advertisement;
- chart/diagram;
- map/layout;
- message/email/letter;
- scenario card;
- composite multimedia stimulus.

Stage 06 may later normalize these into content/task taxonomies.

### Shared stimulus rule

A Stimulus is created once for the represented material and linked to all Tasks/Items that depend on it. Do not duplicate the passage or transcript per Item.

### Stimulus segmentation

When only part of a stimulus applies to an item, the relationship may identify a **segment/range** conceptually:

- paragraph/line span;
- one of several short texts;
- audio time range;
- video time range;
- image region;
- table row/column or form field group.

Exact coordinate/timecode storage is an implementation choice. The product requirement is that local mapping can be represented when needed.

## 4.11 Shared reading passages

Shared reading material follows these rules:

1. store the passage/text collection once as a Stimulus;
2. link all dependent Tasks/Items to it;
3. preserve the source order and grouping of subtexts where meaningful;
4. allow one item to target one subtext while another targets the whole passage;
5. keep passage confidence/rights/provenance independently addressable if local evidence requires it;
6. do not count the same shared passage once per question in corpus text-frequency analysis.

### Example

One newspaper-style article followed by five questions becomes:

- one Task;
- one shared passage Stimulus;
- five Items;
- each Item's choices/answers;
- optionally item-to-paragraph relationships where extraction can support them.

## 4.12 Audio-to-question mapping

**Decision:** Audio is represented as an Asset used by one or more Stimuli, with explicit relationships to the Tasks/Items that depend on it.

The model supports:

- one audio track → one task;
- one audio track → many items;
- one long track → several logical stimulus segments/tasks;
- several audio tracks → one section or task set;
- one item → a specific time segment within a track;
- shared introductory audio/instructions distinct from tested audio;
- replay/count/timing rules attached as instructions/scoring/delivery facts rather than encoded in the audio itself.

### Mapping rule

If an item depends on the whole recording, link it to the whole Stimulus. If it depends on a segment and that relationship is known, preserve the segment mapping. If alignment is uncertain, mark the relationship uncertain rather than inventing timestamps.

### Transcript rule

A transcript, when available or produced later, is not the same thing as the audio asset. It is a textual representation/derived component with its own provenance, extraction status, confidence, and rights implications. Stage 08 defines transcription production; Stage 05 requires that it can be separately represented and linked.

## 4.13 Asset

### Definition

An **Asset** is a separately addressable media or source component used by a Document, Exam, Section, Part, Task, Item, Instruction, or Stimulus.

Examples:

- audio file;
- video file;
- image/photo;
- scan/page image;
- diagram;
- visual prompt card;
- source PDF page crop when preserved as evidence;
- answer sheet template;
- externally distributed supporting file.

### Asset rules

- One Asset may be shared by many Items.
- One Task may use many Assets.
- Assets preserve their own provenance, rights, confidence/extraction quality where needed.
- A restricted asset can be removed/replaced while reusable text remains active.
- Asset identity and duplicate handling are distinct from the logical Stimulus that the asset conveys.

**Example:** two differently encoded MP3 files may later be deduplicated as the same underlying audio Asset, while the logical listening Stimulus remains one exam content unit.

## 4.14 Images, tables, forms, notices, and advertisements

**Decision:** Visual or layout-dependent material is represented as a Stimulus with an appropriate semantic role and one or more Assets/structured representations as needed. Corpus must not flatten away exam-relevant layout.

### Images/photos

Preserve the image Asset and its Stimulus role. OCR/captioning may enrich it later, but machine description does not replace the original visual evidence.

### Tables

Where structure matters, preserve row/column semantics or an equivalent structured representation in addition to source appearance. A plain text dump that loses which value belongs to which heading is insufficient.

### Forms

Preserve field labels, grouping, filled/unfilled state, and layout relationships needed to answer the task. Treat the form as tested content when the learner must interpret or complete it.

### Notices/signs

Treat the notice as a Stimulus. Preserve short text and visual context when the design/location contributes meaning.

### Advertisements

Treat each advertisement as one Stimulus or as a member of a Stimulus collection, depending on the task. Preserve price, conditions, dates, contact details, headings, and visual grouping that may create distractors.

### Layout preservation rule

If answering correctly depends on spatial/layout information, the canonical representation must retain enough structure to reconstruct the semantic relationship even if the implementation later stores both raw and normalized forms.

## 4.15 Response Option

### Definition

A **Response Option** is a candidate-selectable option or member of a response set. It is not automatically a correct Answer.

Examples:

- A/B/C options;
- true/false choices;
- a heading in a matching bank;
- a person/place/advertisement to match;
- a word supplied for a cloze bank;
- an ordered list element.

### Why separate Option from Answer?

Calling every choice an `Answer` confuses **what the learner may select** with **what the key says is correct**. The distinction is essential for distractor analytics and conflicting answer keys.

A Response Option may be:

- correct;
- incorrect/distractor;
- partially correct;
- unused in the key;
- correct for one Item and incorrect for another in a shared option bank.

Correctness belongs to Answer/Scoring relationships, not to the option globally.

## 4.16 Matching tasks

**Decision:** Matching is represented as a relationship problem between two or more task-defined sets rather than flattened into repeated multiple-choice text.

A matching Task can define:

- **targets/prompts** — the members that need a match;
- **candidate match options** — headings, people, ads, statements, etc.;
- cardinality/reuse constraints — one-to-one, options reusable, one option unused, several distractors, etc.;
- one Item per independently scored target, unless the source scores the whole matching set as one unit;
- Answer relationships linking target Items to the correct option(s).

### Example

Five short texts matched to ten headings:

- one Task;
- a Stimulus collection containing five texts;
- one shared Response Option bank containing ten headings;
- five Items, one per text/target;
- five Answer relationships identifying the correct heading for each Item;
- scoring rule preserving whether each match earns a point independently.

This representation supports distractor analysis without duplicating all ten headings inside every Item.

## 4.17 Multiple-correct-answer tasks

For an Item with several correct selections, preserve:

- the complete Response Option set;
- minimum/maximum/exact selection count if instructed;
- the accepted correct option set(s);
- whether order matters;
- whether partial credit is possible;
- penalties, if any;
- alternative accepted sets if the source permits them;
- confidence/dispute at the answer-key assertion level where relevant.

The canonical model must not assume every objective item has exactly one correct answer.

## 4.18 Answer

### Definition

An **Answer** represents source/reference evidence about what response is accepted, expected, exemplary, or correct for an Item/Task.

Answer forms may include:

- keyed choice/option relation;
- set of correct options;
- short accepted text/value;
- several equivalent accepted responses;
- ordered sequence;
- match relationship;
- reference/model response;
- source-provided sample answer;
- explicit statement that no single answer exists and scoring is rubric-based.

### Answer-key provenance rule

Every correctness claim must remain attributable to its source evidence when material. An answer from an official key, a teacher explanation, and an automated semantic inference are not silently collapsed into the same unquestioned fact.

Stage 03 conflict behavior applies: competing plausible keys remain separate candidate assertions while the item is marked disputed.

### Productive-task rule

Writing and speaking tasks do not require a fake canonical “correct answer.” A source-provided sample response can be represented as an Answer/reference example, but scoring truth primarily belongs to the rubric/scoring rule.

## 4.19 Explanation

### Definition

An **Explanation** is rationale or interpretive content explaining a task, answer, scoring decision, language point, or source claim.

It may be:

- source-authored;
- publisher/teacher-authored;
- official commentary;
- manually curated by the owner;
- generated by Corpus later;
- generated by App for learner coaching.

### Separation rule

Explanations must carry an origin/type so generated or secondary rationale is never mistaken for source exam content or official provider guidance.

An Explanation may attach to:

- Item;
- Answer;
- Task;
- Scoring Rule;
- review/conflict resolution.

Learner-specific explanations remain an App concern; Corpus may expose reusable source/reference explanations where confidence and rights permit.

## 4.20 Scoring Rule / Rubric

### Definition

A **Scoring Rule** expresses how a response or collection of responses receives points, ratings, bands, or pass-relevant treatment according to the source evidence.

### Scope

A scoring rule may apply to:

- an Item;
- a Task;
- a Part;
- a Section;
- an Exam/Test Set.

### Objective examples

- 1 point for correct choice, 0 otherwise;
- one point per correct match;
- exactly two selections required, all-or-nothing;
- partial credit for each correct selected response;
- no penalty for wrong responses.

### Productive examples

- writing rubric dimensions;
- speaking interaction/fluency/language dimensions;
- task-fulfilment criteria;
- content-point requirements;
- performance descriptors.

### Rule conflict behavior

Conflicting scoring evidence is preserved as a dispute at the smallest applicable scope, just like conflicting answer keys. The model does not silently pick a scoring rule because it is convenient for the App.

## 4.21 Shared option banks and reusable content within a task

Matching, cloze, and classification tasks often share a bank of options. The model must allow one Response Option collection to serve multiple Items without copying the options into each Item.

The same applies to:

- shared list of headings;
- shared word bank;
- shared people/descriptions;
- shared advertisements;
- shared statements;
- shared images.

A shared bank may have task-level rules such as “each option used once,” “one option unused,” or “options may be reused.” These belong to task/response/scoring constraints.

## 4.22 Examples, demos, and unscored sample items

Provider materials often include example questions (`Beispiel`, `0`, demo answer) that teach the response format but do not count toward scoring.

**Decision:** Preserve them as Tasks/Items when they materially explain exam behavior, but mark their assessment role as **example/unscored** rather than treating them as scored evidence.

This prevents example items from inflating frequency/count analytics or exam point totals while retaining their structural value.

## 4.23 Detached answer keys, transcripts, and scoring guides

A related document may be discovered before its parent exam, or vice versa.

The model supports **unresolved/detached components**:

- an Answer/Answer Key document can exist with a tentative or unknown link to Items;
- a transcript can exist without verified audio alignment;
- an audio Asset can exist without verified task mapping;
- a scoring guide can exist without a verified exact edition link.

Corpus should preserve the candidate relationship and uncertainty until evidence supports linking. It must not force association solely from filename similarity.

## 4.24 Completeness and missing-material model

Completeness is represented independently at Document, Exam, Section, Part, Task, and where useful Item scope.

### Required completeness questions

For a represented unit, Corpus should be able to answer:

1. Does the source claim this is complete or an excerpt?
2. What expected components are present?
3. What components are known missing?
4. Are required dependencies linked?
5. Is completeness itself uncertain?
6. Is the incompleteness caused by the source material, acquisition, or extraction?

### Missing-component examples

- booklet page 9 missing;
- Section Hören present but audio missing;
- audio present but answer key missing;
- Task 3 references an image not supplied;
- scoring guide missing;
- answer key present only for items 1–20;
- document begins at `Teil 2`, so earlier material is likely absent;
- standalone exercise intentionally contains only one Task and is therefore complete **for its claimed scope**, not an incomplete exam.

### No synthetic completion

A missing entity may be represented as an expected/missing reference, but not populated with guessed content. AI may later suggest possible relationships for review; it cannot convert speculation into source truth.

## 4.25 Partial extraction versus partial source

**Decision:** Distinguish **source incompleteness** from **extraction incompleteness**.

- **Source incomplete:** the obtained material itself lacks expected content.
- **Extraction incomplete:** the source contains content but Corpus failed or has not yet extracted it.
- **Linking incomplete:** components exist but their relationship is not yet verified.

This distinction is essential for Stage 08 and Stage 10. A failed parser must not cause Corpus to conclude that the official exam itself lacks a section.

## 4.26 Structural order and numbering

Every structural entity should preserve:

- provider/source-native label;
- source-native identifier/number when present;
- order within its parent scope;
- normalized canonical role separately.

Order can matter for exam realism and provider analysis. However, order is not identity: a reordered mirror does not automatically become a new independent exam.

## 4.27 Confidence/authenticity attachment

Stage 03's mandatory confidence levels map directly to the canonical model:

- Source Observation → source confidence/authenticity evidence;
- Document → document confidence;
- Exam/Test Set → exam confidence;
- Task → task confidence;
- Item → item confidence.

The model also permits finer local confidence on Answers, Scoring Rules, Stimuli, Assets, transcripts, or extracted relationships when later stages need it.

**Most-specific-evidence rule:** local defects override parent assumptions for the affected use.

## 4.28 Rights attachment and inheritance

Stage 04 rights metadata may attach at:

- Source Observation;
- Document;
- Exam/Test Set;
- Section/Part/Task/Item where distinct rights are evidenced;
- Instruction/Stimulus/Answer/Explanation/Scoring Rule where source expression needs separate control;
- Asset.

Rights may inherit from a broader scope only when the license/permission evidence clearly covers descendants. A narrower statement overrides the broader one.

### Composite-use rule

If a Task combines reusable text with a restricted image/audio Asset, the complete unchanged Task is not learner-reusable unless every included component passes the intended-use rights gate. The reusable parts may remain separable if the experience still makes sense.

## 4.29 Provenance and lineage attachment

Every content-bearing or source-derived unit must be traceable back to the Document/Asset and Source Observation(s) that support it.

This includes:

- structural claims such as “this is Part 2”;
- instruction text;
- stimulus content;
- answer keys;
- scoring rules;
- transcripts;
- explanations when source-derived;
- provider-specific extension facts.

Derived non-reconstructive metadata can later point to these units rather than embedding the source expression.

## 4.30 Generic core versus provider-specific extensions

### Generic core must be sufficient for

- whole-exam structure;
- sections/parts/tasks/items;
- shared stimuli;
- instructions;
- response options;
- answers;
- scoring/rubrics;
- assets/media mapping;
- completeness;
- provenance;
- confidence/review state;
- rights state;
- source-native labels/order.

### Extension use is justified when

A provider has a meaningful rule that cannot be represented without losing semantics, for example:

- independently certifiable module behavior;
- provider-specific score conversion;
- unusual delivery/combination rule;
- provider-native classification with no generic equivalent yet.

### Promotion rule

If an extension concept becomes relevant across multiple providers or becomes necessary for generic App/analytics behavior, later product shaping should promote it into the canonical core through a versioned model decision rather than proliferating duplicated provider extensions.

## 4.31 Provider extension anti-contamination rule

Generic analytics should not need code such as “if TELC then inspect special field X; if Goethe then special field Y” merely to answer generic questions like task count, number of items, shared stimuli, response mode, or scoring points. Those belong in the canonical core.

Provider-specific extensions are for **provider-specific semantics**, not basic modeling shortcuts.

---

## 5. Representative Examples

These examples demonstrate how the canonical model handles different structures. They are **representative modeling examples**, not a substitute for Stage 16 benchmark verification of the current official provider formats and editions.

## 5.1 TELC-style example — reading matching task with separate answer material

### Source evidence

Imagine an official/provider practice resource area exposes:

- a test booklet PDF;
- a separate answer-key PDF;
- other exam assets.

The same booklet is also mirrored elsewhere.

### Canonical representation

**Source Observations**

- official provider page/download observation;
- official booklet URL observation;
- official answer-key URL observation;
- mirror observation linked as a mirror, not independent evidence.

**Documents**

- `Test booklet — version A`;
- `Answer key — version A`.

**Exam/Test Set**

- one TELC-style B1 model/practice exam, linked to both documents.

**Section**

- provider-native `Leseverstehen`, normalized later by Stage 06 as Reading.

**Part**

- provider-native `Teil 1`.

**Task**

- candidate reads several short texts and matches each to a heading from a larger heading bank.

**Instructions**

- task instruction describing the matching rule and any unused headings.

**Stimuli**

- five short text stimuli, grouped as one task stimulus collection.

**Response Option bank**

- ten heading options shared by all Items.

**Items**

- five matching Items, one per target text if each match is scored independently.

**Answers**

- five key relationships from target Item → correct heading option, sourced from the answer-key document.

**Scoring**

- one point per correct match if that is what the source specifies; the rule is linked at Task/Item scope rather than guessed.

### Why this example matters

A TELC-only flat schema might copy all ten headings into each of five questions and embed the answer key inside the booklet record. The canonical model instead recognizes shared content, separate evidence documents, and mirror provenance. That is cheaper to analyze, easier to deduplicate, and safer for rights/removal.

## 5.2 TELC-style listening example — one audio track shared by several items

**Section:** provider-native Listening/Hörverstehen section.  
**Part:** provider-native part label where present.  
**Task:** listen to a recording and evaluate several statements/questions.  
**Asset:** one MP3/audio file.  
**Stimulus:** one logical listening segment backed by the audio Asset.  
**Items:** several objective Items sharing that Stimulus.  
**Answers:** keyed responses from the answer material.  
**Instruction:** playback/response rule, distinct from the tested audio.  
**Mapping:** each Item points to the whole listening Stimulus or to a known segment if the source/alignment supports that precision.

The track is stored/modeled once. It is not duplicated once per question.

## 5.3 Non-TELC example — Goethe-style modular practice set

A non-TELC provider may organize B1 practice around modules such as reading, listening, writing, and speaking rather than TELC's exact section composition.

### Source evidence

Suppose a provider practice set contains:

- one reading-module PDF with several `Aufgaben`;
- a separate answer material document;
- separate listening material/audio for another module;
- writing/speaking prompt material.

### Canonical representation

**Exam/Test Set**

- one provider practice set representing the B1 assessment family.

**Section / Module**

- provider-native `Lesen` module represented generically as a Section;
- provider-native `Hören`, `Schreiben`, and `Sprechen` likewise become Sections when present.

The generic model does **not** invent a TELC-specific `Sprachbausteine` section.

**Part / Aufgabe grouping**

- where the source's `Aufgabe` acts as a structural grouping, it may map to Part;
- where `Aufgabe` is itself the coherent candidate activity, it maps directly to Task.

The mapping is decided by semantic function, not by translating one provider word to one fixed entity globally.

**Reading Task example**

- one shared passage Stimulus;
- several Items asking for decisions/choices about the passage;
- shared or item-specific Response Options;
- Answers sourced from the separate key.

**Provider-specific extension**

- if the provider's modules have a certification/delivery property that matters and cannot be represented generically, preserve it as a provider-specific module extension on the Section/Exam relationship.

### Why this example matters

The model represents a modular non-TELC exam naturally without pretending it has TELC's section names, part hierarchy, or scoring behavior. The same App-facing analytics can still ask generic questions such as “how many reading tasks?”, “what response types occur?”, “which stimuli are shared?”, or “which skills appear?”

## 5.4 Standalone teacher exercise — no fake exam wrapper

A teacher web page contains one B1 listening exercise and one audio file, with five questions but no claim that it is a complete exam.

Represent:

- Source Observation: teacher page;
- Document: HTML exercise page;
- Exam/Test Set: **optional** — use a standalone assessment/test-set wrapper only if grouping is useful and label it as standalone, never as a full provider exam;
- Section: Listening if needed for canonical organization;
- Task: one listening activity;
- Asset/Stimulus: one audio track;
- Items: five questions;
- Answers: only if supplied/validated;
- Completeness: complete for its claimed standalone scope, not “missing Reading/Writing/Speaking.”

This prevents standalone material from falsely influencing full-exam composition analytics.

## 5.5 Incomplete scanned exam with missing answer key

Observed material contains pages 1–8 and 11–14 of a mock exam; pages 9–10 are missing and no answer key is available.

Represent:

- Document completeness: `incomplete_known_missing`, with missing page range;
- Exam completeness: likely `incomplete_known_missing` if the absent pages affect exam structure;
- intact Sections/Tasks/Items normally where extractable;
- expected/missing relationship for the absent page range;
- answer state as missing/unknown for objective Items rather than invented;
- lower document/exam structural confidence as Stage 03 requires;
- intact Tasks/Items allowed to retain stronger local confidence where independently supportable.

The fragment may still contribute topic, vocabulary, task-shape, and other non-correctness evidence.

## 5.6 Mixed-rights visual task

A reusable teacher-authored task text embeds a third-party photo whose rights are unknown.

Represent separately:

- Task text / Instruction / Item content with reusable rights if supported;
- image Asset/Stimulus component with `UNKNOWN_REVIEW_REQUIRED` rights;
- composite Task effective direct-reuse decision blocked while the image is included;
- option to replace the image with an independently created Asset if the task semantics allow it.

No whole-document rights label is allowed to erase the image-specific restriction.

---

## 6. Edge Cases / Failure or Uncertainty Handling

### 6.1 One document contains two exams

Create two Exam/Test Sets linked to the same Document. Do not split source provenance artificially just to preserve a one-document/one-exam assumption.

### 6.2 One exam spans several documents

Link all contributing Documents/Assets to one Exam. Preserve which component supplies booklet text, answer key, scoring, transcript, or media.

### 6.3 Provider label is ambiguous between Part and Task

Use semantic behavior: if it groups several coherent candidate activities, prefer Part; if it is the coherent activity itself, use Task. Preserve the native label regardless. Mark uncertain mapping for review if it materially affects analytics.

### 6.4 A question stem includes essential tested information

Do not classify the entire stem as “instruction” merely because it starts with an imperative. Preserve the tested prompt content as Item prompt/Stimulus and the operational directive as Instruction where useful.

### 6.5 One passage is printed twice in a source

Stage 09 will decide duplicate identity. Stage 05 permits both observed placements to point to the same logical Stimulus when evidence supports reuse, or to separate candidate stimuli until deduplication resolves it.

### 6.6 One audio file includes several tasks with pauses and spoken instructions

Represent one Asset, several logical Stimuli/segments, and separate Instruction segments when known. If segmentation is uncertain, preserve whole-track mapping and uncertainty rather than fabricating exact boundaries.

### 6.7 Answer key refers to wrong numbering because of edition mismatch

Do not force-link by position. Preserve answer-key Document and candidate relationship, mark affected Items/Answers disputed or unlinked, and allow later edition/version resolution.

### 6.8 Matching options can be reused

Task-level matching constraints explicitly allow reuse. Correctness is Item→Option relationship, so one Option can be correct for more than one Item.

### 6.9 Matching has one unused distractor

Keep the unused option in the shared bank. It remains valuable distractor evidence and should not be discarded merely because no correct Answer points to it.

### 6.10 Multiple accepted short answers

One Item can have several accepted Answer variants, with equivalence/normalization rules where source evidence supports them. Do not choose one textual form as the only truth if several are explicitly accepted.

### 6.11 Writing source provides a sample answer

Store the sample as a reference/model Answer or Explanation with source provenance. Do not treat it as the unique correct response. Scoring comes from the rubric/criteria.

### 6.12 Speaking prompt references a picture card

The picture is an Asset backing a Stimulus; the spoken task instruction is separate; the productive Item links to both. Rights can differ between prompt text and image.

### 6.13 Table OCR loses column structure

Keep extraction marked incomplete/low-quality. Do not publish a flattened text representation as faithful tested content if the table relationships are needed to answer correctly.

### 6.14 Source is intentionally an excerpt

Mark `intentional_excerpt`. Do not penalize it as though pages are accidentally missing, and do not use it to infer whole-exam balance.

### 6.15 Full source exists but parser extracted only half

Mark extraction incomplete, not source incomplete. Stage 08/10 should reprocess; Stage 05's completeness semantics must preserve the distinction.

### 6.16 Question has no answer key but semantic answer seems obvious

Do not silently create a source Answer. A derived/inferred candidate answer may later be stored as generated/analytical evidence with explicit origin and confidence, but correctness-dependent App use remains subject to Stage 03 gates.

### 6.17 An explanation contradicts the key

Preserve both source claims and mark the affected Item/Answer disputed. Explanations do not automatically override answer keys; Stage 03/10 review resolves evidence conflicts.

### 6.18 Provider-specific concept appears in several providers

Promote it to a future generic model revision if it becomes broadly meaningful. Do not maintain multiple near-identical provider extensions indefinitely.

### 6.19 Asset removed after takedown

Retain the Task/Item structure and non-reconstructive metadata when Stage 04 permits, mark the Asset unavailable/prohibited, and ensure composite direct use is blocked. The canonical structure should survive without pretending the removed expression still exists.

### 6.20 Orphan audio/answer file discovered first

Preserve it as a Document/Asset with candidate relationships and provenance. Linking can occur later. Ingestion success does not require immediate exam attachment.

---

## 7. Relationship to Other Bestehen Stages

### Stage 06 — Exam and Skill Taxonomy

Stage 06 should classify the canonical entities rather than define provider-specific data structures. Section, task, item, stimulus, response type, provider labels, and scoring behavior provide the substrate for task-type, skill, topic, grammar, vocabulary, strategy, and distractor taxonomies.

### Stage 07 — Difficulty and TELC Relevance

Difficulty and relevance can attach at Exam/Section/Task/Item/Stimulus/Asset scopes as appropriate, while remaining separate from confidence. Audio-specific difficulty can use Asset/Stimulus properties without duplicating Items.

### Stage 08 — Ingestion Pipeline

Ingestion must create/link these concepts progressively and support partial extraction. It should distinguish missing source material from failed extraction and allow orphan/detached components to be linked later.

### Stage 09 — Duplicate and Near-Duplicate Detection

Deduplication operates at multiple model levels: Source Observations can be mirrors; Documents can be byte/near duplicates; Exams can be same/derivative editions; Stimuli, Items, and Assets can repeat or be adapted. The canonical model preserves enough identity and lineage to neutralize mirror inflation without deleting provenance.

### Stage 10 — Validation and QA

Validation should verify structural containment, answer mapping, stimulus/item relationships, asset presence, audio alignment, response cardinality, scoring, completeness, and instruction/tested-content classification.

### Stage 11 — Corpus Analytics

Analytics should count the right evidence units. Shared passages/options/assets must not be multiplied by item count. Full-exam composition analytics must exclude standalone/partial material unless the analytical question explicitly supports it.

### Stage 12 — Corpus → App Contract

The App should receive normalized task/exam patterns, allowed source/reference content, scoring information, stimuli/assets where rights permit, and abstract pattern metadata otherwise. The App should not need to understand source URLs or provider-specific document layouts to request suitable practice patterns.

### Stage 13 — Operations

Operations must be able to inspect and correct links among source/document/exam/task/item/answer/stimulus/assets, review incomplete/detached material, and resolve provider-specific mapping without direct database surgery.

### Stage 14 — Cost, Scale, and Automation

The canonical model is designed to reduce redundant processing: shared passages, option banks, and audio are represented once and reused by relationship. Stage 14 can measure processing at meaningful units rather than repeatedly analyzing duplicated content.

### Stage 15 — Security and Abuse

Raw untrusted Documents/Assets remain separate from normalized structured data, allowing later security/retention rules without collapsing provenance or exam structure.

### Stage 16 — Benchmark Corpus

The benchmark must include examples that exercise this model: TELC and non-TELC structure, shared passages/audio, matching, multiple-correct-answer items, productive tasks, visual material, partial/incomplete material, detached keys/assets, and mixed-confidence/rights cases.

### Stage 17 — Final Product Specification

The final Corpus specification should preserve this hierarchy and the distinction among structural containment, shared material, provenance, confidence, rights, and provider extensions.

---

## 8. Cost Notes

The canonical model itself has **no meaningful recurring runtime cost requirement**. Its main cost effect is on ingestion/enrichment complexity.

### Preferred low-cost default

- Represent shared passages, option banks, and media **once**, then link them to dependent Tasks/Items rather than duplicating content.
- Use deterministic structural rules and source numbering/layout where they are reliable.
- Allow partial/unlinked records rather than spending premium-model calls to force uncertain relationships during first ingestion.
- Perform expensive semantic segmentation/alignment only where the relationship materially affects downstream value.
- Batch enrichment and reuse extracted structure; do not re-analyze the same shared passage/audio separately for every Item.
- Preserve source-native labels so later provider mapping can be corrected without re-fetching source material.

### Where premium processing may later be justified

A stronger model or selective manual review may be useful for:

- ambiguous Part/Task boundaries;
- scanned/layout-heavy tables/forms;
- uncertain shared-passage segmentation;
- audio-to-item alignment that cannot be derived deterministically;
- mixed-document answer-key linking;
- provider-specific structure that materially affects App behavior.

The fallback is to keep the relationship **unknown/review-required** and use stronger independent evidence elsewhere. There is no product requirement to spend money resolving every low-value ambiguity immediately.

### Cost guardrail

No per-learner or per-App-session model call should be required merely to reconstruct canonical exam structure. Corpus should resolve and cache structure during ingestion/reprocessing.

---

## 9. Decisions Made

1. The canonical structural hierarchy is **Source Observation → Document → Exam/Test Set → Section → optional Part → Task → Item**, with Answer/Scoring attached at the appropriate response scope.
2. The hierarchy is not a rigid source tree: Documents, Exams, Assets, Stimuli, and source observations may have many-to-many relationships where real exam distribution requires it.
3. Source Observation represents provenance/location; Document represents a concrete versioned artifact; Exam/Test Set represents a coherent assessment package. They must never be collapsed into one concept.
4. Section is a generic top-level exam division; provider-native labels are preserved and normalized later.
5. Part is optional and used only when the provider/source has a meaningful intermediate grouping.
6. Task is the coherent candidate activity; Item is the smallest response/scoring-addressable unit.
7. Composite Items with child Items represent independently scored subparts while preserving source grouping.
8. Multi-select questions remain one Item when they form one response/scoring unit; the model does not assume exactly one correct answer.
9. **Instruction** and **Stimulus/tested content** are distinct functional concepts.
10. **Stimulus** is first-class and reusable across Items/Tasks, covering passages, audio, visual material, tables, forms, notices, ads, scenarios, and composite media.
11. Audio is an Asset backing one or more Stimuli, with explicit Task/Item mapping and optional segment relationships.
12. Visual/layout-dependent material must preserve semantic structure when layout affects the answer.
13. Response Options are separate from Answers so distractors and shared option banks can be modeled faithfully.
14. Matching tasks use shared target/option sets plus Item→Option answer relationships and explicit reuse/cardinality constraints.
15. Answers preserve accepted/correct/reference responses and provenance; writing/speaking do not require a fake unique correct answer.
16. Explanations are separately typed/provenanced so official/source rationale, secondary commentary, and generated explanation are never conflated.
17. Scoring Rules/Rubrics are first-class and can attach at Exam, Section, Part, Task, or Item scope.
18. Completeness is explicit: `complete`, `intentional_excerpt`, `incomplete_known_missing`, or `completeness_unknown`, with missing dependencies recorded.
19. Source incompleteness, extraction incompleteness, and linking incompleteness are separate states.
20. Detached answer keys, transcripts, scoring guides, and media may exist before their exact relationships are verified.
21. Confidence/authenticity attaches at the Stage 03 mandatory levels and may be refined locally for answers/assets/scoring/relationships.
22. Rights metadata attaches at the smallest evidenced scope and inherits only when license scope supports it.
23. Provider-specific extensions are isolated from the generic core and used only for semantics that cannot be represented generically; broadly useful concepts should later be promoted into the core.
24. Standalone exercises are complete for their claimed scope and must not be falsely treated as incomplete full exams.
25. The model supports representative TELC-style and non-TELC modular structures without requiring a TELC-only schema.

---

## 10. Open Questions / Deferred Decisions

### Owner questions

**None.** The available product context is sufficient to make the Stage 05 product decisions without an owner preference or legal-risk decision.

### Deferred architecture/implementation decisions

The following are intentionally deferred because they do not change the product semantics defined here:

- relational versus document versus graph persistence;
- entity IDs, keys, and physical versioning strategy;
- exact serialization/API representation;
- whether shared relationships are implemented as join records, edges, references, or embedded structures;
- exact provider-extension namespace/storage syntax;
- text-range, image-region, and media-timecode representation;
- extraction algorithms for structure, OCR, tables, forms, and audio segmentation;
- automatic confidence for extracted relationships;
- physical representation of missing/expected placeholders;
- scoring engine implementation and score conversion code;
- current-edition provider-format verification, which belongs in benchmark/reference work rather than being hardcoded from this conceptual example.

These decisions may vary later without changing the canonical product model.

---

## 11. Definition of Done Check

| Stage 05 requirement | Decision captured | Where |
|---|---|---|
| Define hierarchy from source to item | **Yes** | Sections 3.1, 4.1–4.7 |
| Source | **Yes** | 4.1 Source Observation |
| Document | **Yes** | 4.2 |
| Exam/Test Set | **Yes** | 4.3 |
| Section | **Yes** | 4.4 |
| Part | **Yes — optional by design** | 4.5 |
| Task | **Yes** | 4.6 |
| Question/Item | **Yes** | 4.7 |
| Answer | **Yes** | 4.18 |
| Explanation | **Yes** | 4.19 |
| Asset | **Yes** | 4.13 |
| Define multi-part questions | **Yes** | 3.7, 4.8 |
| Define shared reading/listening passages | **Yes** | 3.4, 4.10–4.12 |
| Define audio-to-question mapping | **Yes** | 4.12 |
| Define images, tables, forms, notices, advertisements | **Yes** | 4.14 |
| Define matching tasks | **Yes** | 4.16 |
| Define multiple-correct-answer tasks | **Yes** | 4.17 |
| Separate instructions from tested content | **Yes** | 3.5, 4.9 |
| Represent answer keys | **Yes** | 4.18, 4.23 |
| Represent scoring rules | **Yes** | 3.8, 4.20 |
| Represent incomplete exams honestly | **Yes** | 3.9, 4.24–4.25 |
| Define provider-specific extensions without contaminating generic model | **Yes** | 3.10, 4.30–4.31 |
| Include TELC-style example | **Yes** | 5.1–5.2 |
| Include non-TELC-style example | **Yes** | 5.3 |
| Preserve Stage 02 provenance/mirrors/version behavior | **Yes** | 4.1–4.3, 4.29 |
| Preserve Stage 03 confidence locality | **Yes** | 4.27 |
| Preserve Stage 04 granular rights/removal behavior | **Yes** | 4.28 |
| Address personal-project cost constraint | **Yes** | Section 8 |

**Stage 05 product-shaping status: complete.** The remaining choices are architecture, extraction, taxonomy, validation, benchmark, or provider-currentness decisions assigned to later stages.