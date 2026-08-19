# Bestehen / App — Stage 21: Content Strategy

> **Status:** Authoritative Stage 21 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Content promise:** Use Corpus to learn what the exam rewards, then serve original, rights-safe, validated practice that is natural enough to feel real and controlled enough to support trustworthy learner evidence.

## 1. Purpose and Scope

This document defines how Bestehen / App obtains enough high-quality exam-shaped material to coach an A1→B1 learner without becoming a library of copied exams or a stream of unreviewed AI exercises.

The content strategy has to satisfy several requirements that pull in different directions:

- **exam fidelity:** practice must preserve the task mechanisms, language demands, distractor behavior, timing, playback, productive obligations, and interaction patterns that matter for TELC B1;
- **learning breadth:** the learner needs enough fresh equivalent content for repair, delayed transfer, daily training, mocks, and repeated readiness evidence;
- **rights safety:** public availability and authenticity do not imply permission to redistribute source material;
- **evidence validity:** ambiguous answers, unnatural language, broken audio, copied variants, or invalid prompts must not become learner mistakes or readiness evidence;
- **natural German:** generated material must read and sound like plausible German communication rather than content assembled to contain target vocabulary or grammar;
- **cost control:** Bestehen is initially a personal project, so content should normally be created, validated, and cached before use rather than generated expensively for every learner attempt.

### Core decision

**Corpus is the evidence and calibration layer; the App content bank is a separately governed learner-practice layer.**

Corpus may contain material that is highly informative but cannot be shown to the learner. The App should normally transform **abstract exam intelligence**—task patterns, topic distributions, grammar/vocabulary signals, difficulty characteristics, distractor archetypes, discourse structures, audio characteristics, and skill relationships—into **original content** that passes an App-specific quality gate.

Exact source material is learner-playable only when its usage status explicitly permits the intended display and any attribution/license obligations are satisfied.

### Content-quality principle

**A content item is part of the measurement instrument.**

If the item is ambiguous, unnaturally written, technically broken, too close to something already exposed, wrongly keyed, or mismatched to the claimed difficulty/target condition, the product must lower or remove the evidence claim rather than blame the learner.

### In scope

- relationship between Corpus/reference material and App-served content;
- direct reuse versus original generation;
- content classes and approval levels;
- Corpus-grounded generation briefs and task templates;
- generated-content QA and answer validation;
- difficulty controls;
- anti-copy, anti-repetition, and freshness rules;
- natural-language requirements for Reading, Language Elements, Listening, Writing, and Speaking;
- generated-audio requirements;
- curated gold content and readiness-grade content;
- content refresh and rotation;
- source attribution;
- content-error reporting, quarantine, correction, and evidence repair;
- low-cost generation, batching, caching, and selective premium/human review;
- acceptance criteria for learner-facing content.

### Out of scope

- the final technical Corpus → App payload/API and compatibility mechanism — Stage 22;
- notification delivery — Stage 23;
- learner-data/content retention, export, deletion, and legal retention behavior — Stage 24;
- accessibility equivalence for target-condition evidence — Stage 25;
- final analytics instrumentation and empirical quality calibration — Stage 26;
- databases, queues, model vendors, embedding systems, storage formats, TTS vendors, or deployment architecture.

---

## 2. Inputs / Existing Decisions

Stage 21 preserves the shared Product Overview, shared Identity, and App Stages 01–20.

### 2.1 Corpus and App already have different jobs

The foundational project documents establish that:

- Corpus gathers broad A2/B1 exam evidence from official and unofficial sources;
- source **authenticity/confidence** and **usage rights** are independent dimensions;
- public accessibility is not redistribution permission;
- Corpus is evidence, while the learner-facing exercise bank is what the learner practices;
- real/reference exams define what gets tested; original exercises normally provide how it is practised;
- Corpus should remain intelligence behind the coach rather than become a learner-facing archive.

Stage 21 makes that boundary operational for content creation and serving.

### 2.2 Content validity already affects learner evidence

Stages 03–07 establish that broken media, ambiguous content, unsupported answer keys, or evaluator failures are **non-learner invalidations**. They do not become mistakes, mastery loss, or readiness penalties.

The learner model also preserves content/evaluation quality as part of evidence quality. Stage 21 therefore treats pre-publication content QA and post-publication correction as part of the evidence system, not merely editorial polish.

### 2.3 Fresh content is required throughout the product

Stages 05, 07, and 14 require repair and review to use fresh equivalent tasks. Same-item repetition, solution exposure, and superficial variants cannot establish independent transfer or retention.

Stages 15–17 require recent independent target-condition evidence and fresh mock forms for defensible readiness and Ready-to-Book decisions. Content freshness therefore has a stronger meaning than “the learner has not clicked this database row before.”

### 2.4 Difficulty is multidimensional

Stage 08 defines P0 Supported Foundation → P1 Guided A2 → P2 A2/B1 Bridge → P3 Independent B1 Training → P4 Target Conditions. Difficulty is controlled through separable dimensions such as:

- linguistic load;
- task/reasoning load;
- task length and breadth;
- distractor closeness;
- assistance;
- timing;
- replay/reference constraints;
- production independence;
- realism/sequencing;
- evaluation standard.

Stage 21 must create content to those profiles rather than ask a generator for a vague “easy A2 exercise” or “hard B1 question.”

### 2.5 Skill stages have already defined modality-specific constraints

Stages 09–13 establish that:

- Reading and Sprachbausteine are normally objectively scored from reviewed keys;
- ambiguous objective items are invalidated/quarantined rather than adjudicated against the learner after the fact;
- learner-facing Reading and Language Elements practice defaults to original reviewed content;
- Listening normally uses original reviewed scripts, batch-generated/cached audio at lower rungs, and stronger audited assets for readiness anchors;
- Writing prompts contain explicit communicative context and separately assessable content obligations;
- Writing has many valid B1 responses rather than one “correct answer”;
- Speaking must rehearse actual production and interaction, not generic chatbot conversation;
- S2 requires meaningful information/viewpoint difference and S3 permits multiple valid joint plans;
- target-format details are **versioned exam knowledge** and must be revalidated before P4/target-condition claims.

Stage 21 generalizes those constraints into one content-governance model.

### 2.6 Mocks and readiness require stronger content than ordinary practice

Stages 15–17 already require target-mappable, current, independent, valid evidence. Stage 16 specifically states that learner-facing mocks default to **original, reviewed, target-calibrated forms** unless a source asset has confirmed reuse rights.

Stage 21 therefore creates approval levels: not every useful training item is automatically suitable for a clean P4 mock or Ready-to-Book evidence.

### 2.7 Cost is already a product constraint

Earlier stages consistently prefer:

- deterministic scoring;
- reviewed reusable content;
- precomputation;
- batching;
- caching;
- fixed/prerecorded interaction where sufficient;
- selective AI for productive evaluation or genuinely adaptive interaction;
- stronger models only when uncertainty or evidence stakes justify them.

Stage 21 applies the same rule to content creation.

### 2.8 No earlier document requires amendment

No Stage 21 decision reverses an earlier App decision. This stage formalizes the content system that Stages 09–17 deliberately assumed would exist.

---

## 3. Decisions and Rationale

## 3.1 Separate reference intelligence from learner-playable content

**Decision:** A Corpus item and an App exercise are different product objects even when one informed the other.

Corpus may preserve exact source text/audio/images/questions for analysis subject to its own rights rules. The App receives or derives only what it is permitted to use and gives every learner-playable item its own approval state, content identity, answer/rubric contract, difficulty profile, target-blueprint relationship, freshness family, and rights/attribution state.

The App must be able to continue serving already approved practice even if a particular reference source later becomes unavailable. Corpus is a source of intelligence and approved assets, not a requirement that the learner fetch or inspect raw source material during a session.

### Why this boundary matters

Treating Corpus as the exercise bank would create four failures:

1. rights-uncertain material could leak into the learner experience;
2. repeated real/reference items would be memorized and lose evidence value;
3. low-confidence unofficial items could accidentally be treated as target truth;
4. content generation would become paraphrased cloning instead of skill-equivalent practice.

---

## 3.2 Use five content classes

**Decision:** Every learner-relevant content candidate belongs conceptually to one of five classes.

| Class | Meaning | Normal learner use | Readiness role |
|---|---|---|---|
| **C0 — Reference only** | Source/reference material useful for Corpus intelligence but not approved for learner display | Never served verbatim | May inform abstract patterns/calibration only |
| **C1 — Reusable source content** | Exact source content whose rights/status explicitly permit the intended learner use | Occasional direct practice, examples, or calibration when quality is sufficient | Can contribute only if target/current/evidence requirements also pass; rights alone never make it readiness-grade |
| **C2 — Curated gold original** | Original or legally reusable content that has received the strongest review/calibration required for its role | Diagnostic anchors, benchmark tasks, P4/readiness forms, gold QA examples | Preferred readiness/mocks anchor class |
| **C3 — Validated original practice** | Original human-authored or model-assisted content that passed normal App QA | Main P0–P3 training, repairs, reviews, focused B1 practice | May create E3-style evidence when the applicable Stage 15 conditions are met; not automatically P4 |
| **C4 — Adaptive/ephemeral interaction** | Content whose value depends on the learner’s current response, especially partner turns or a narrowly tailored repair | Selected Speaking interaction and rare personalized learning moments | Normally learning/evidence support only; readiness-grade use requires the stronger interaction/evaluation validity already defined by Stages 13–16 |

“Original” means the learner-facing wording, scenario, information configuration, answer path, and media are newly created for Bestehen rather than a close paraphrase of one identifiable reference item.

A model may help create C2 or C3; **gold describes review/calibration status, not whether a human typed every sentence.**

---

## 3.3 Default to original generation; use verbatim content conservatively

**Decision:** Exact/verbatim source content may be shown only when all applicable conditions are true:

1. usage metadata explicitly permits the intended redistribution/display;
2. any derivative-use limitation is respected if the item is modified;
3. required attribution/license notices can be satisfied;
4. the source/content is not prohibited, withdrawn, quarantined, or pending rights review;
5. content quality and answer/media validity meet the App approval level required for the intended use;
6. current target-blueprint relevance is verified if the item is used as P4/readiness evidence;
7. learner freshness has not been destroyed by prior exposure.

The following are **not** sufficient reasons to reuse material:

- it is downloadable without login;
- it is an official practice test;
- it appears on many websites;
- it looks authentic;
- it has a correct answer key;
- it is “for educational use” without a clear license granting the App’s intended use.

### Conservative fallback

When rights are unknown, analysis/reference only, or unclear, the App does **not** show the source item or produce a line-by-line paraphrase of it. It uses the source only through abstract, aggregated, rights-permitted intelligence such as:

- task mechanism;
- topic/domain;
- discourse/genre type;
- target skill;
- grammar/vocabulary pattern;
- answer/distractor archetype;
- difficulty characteristics;
- audio characteristics;
- structural counts and relationships;
- source-breadth/frequency signals.

Precise legal interpretation remains part of Corpus rights review. The App’s product default is intentionally stricter: **uncertain reuse becomes original practice, not legal guesswork.**

---

## 3.4 Generate from a structured content brief, not from raw source imitation

**Decision:** Original generation begins from a **content brief** derived from approved target knowledge and Corpus intelligence.

A content brief specifies the exam behavior to create without supplying distinctive source wording as the thing to imitate.

At product level, the brief contains:

| Brief dimension | Required meaning |
|---|---|
| Target/task family | R1/R2/R3, SB1/SB2, H1/H2/H3, Writing, S1/S2/S3, repair/review variant, etc. |
| Target blueprint/version | Which current target format/constraints this content is intended to support |
| Progression rung | P0–P4 and the evidence claim allowed at that rung |
| Skill/capability targets | Primary node(s), with at most the necessary secondary relationships |
| Communicative domain/genre | Housing, work, course, appointments, travel, services, social planning, etc.; notice/email/interview/conversation/etc. |
| Corpus support | Aggregate frequency/relevance/source-breadth/confidence signals that justify the pattern |
| Linguistic profile | Vocabulary familiarity, grammar density, sentence complexity, abstraction, paraphrase level |
| Reasoning profile | Gist/detail/inference, constraint count, distractor closeness, correction behavior, matching burden, etc. |
| Media/interaction profile | Speaker count, speed, playback, turn structure, private/shared information, partner role |
| Answer/rubric contract | What makes the answer defensible or what semantic obligations/rubric behaviors must be judgeable |
| Freshness/diversity requirements | Topic/genre/semantic frame that must differ from recent content while preserving the target capability |
| Source-separation constraints | Reference families/phrases/configurations that must not be copied or closely reconstructed |

The content generator may use several high-confidence Corpus observations to learn a pattern. It must not be asked to “rewrite this copyrighted exam question so it looks different.”

### Corpus-confidence rule

High-confidence, current TELC evidence should dominate target-format generation. Broader A2/B1 sources can enrich language, topics, variants, and progression, but they may not override current verified TELC behavior for P4.

Low-confidence unofficial evidence can suggest a hypothesis or diversity opportunity. It cannot by itself define an official task requirement, answer rule, or target-condition difficulty.

---

## 3.5 Pre-generate normal practice; generate at runtime only when adaptation itself adds value

**Decision:** The default content lifecycle is **generate/author → validate → approve → cache → serve many times**, while still enforcing per-learner freshness.

Original exercises are generated when:

- a task-family × rung × capability combination lacks enough approved fresh content;
- a review/repair pattern needs variants that are equivalent but not memorized;
- topic/genre diversity is too narrow;
- a target-blueprint update invalidates or reclassifies existing forms;
- exposure saturation would prevent fresh independent evidence;
- content-error/quality data retires too much of a bank;
- Corpus evidence reveals a newly important pattern worth covering.

### Runtime generation boundary

Unreviewed runtime generation is **not** the normal source of objective questions, Reading passages, Language Elements items, Listening scripts/audio, Writing prompts, diagnostic anchors, mocks, or P4 readiness forms.

Runtime generation is justified when the learner’s live response must materially shape the content, primarily:

- adaptive S2/S3 partner turns;
- a narrowly tailored productive repair when a reviewed template cannot express the needed contrast;
- rare low-stakes fresh-transfer content when the approved bank is temporarily exhausted and the result is explicitly treated as lower-confidence learning evidence until validated.

A first-seen runtime-generated objective item must never become a clean readiness anchor merely because a model supplied an answer key.

---

## 3.6 Use approval levels, not one binary “generated content is good” flag

**Decision:** Content progresses through product approval levels according to the evidence stakes.

| Approval level | Allowed use | Minimum product expectation |
|---|---|---|
| **Draft / quarantine** | No learner scoring | Candidate exists but one or more rights, answer, naturalness, difficulty, duplication, media, or metadata checks remain unresolved |
| **Training-approved** | P0–P2 and ordinary repair/review; selected P3 when target mapping permits | Rights-safe; structurally valid; natural enough; answer/rubric defensible; difficulty plausible; no material duplicate/copy; media valid |
| **Independent-B1 approved** | Clean P3 B1 evidence and higher-stakes practice | Strong naturalness; reviewed answer/rubric rationale; target mapping verified; difficulty/distractor behavior independently validated; low ambiguity |
| **Readiness/P4 approved** | P4, target-condition mocks, Stage 15/17 anchors | Current blueprint; strongest review; human sign-off for the complete form/asset; target-calibrated difficulty/format; content-family independence; stable version; no known material defect |
| **Gold benchmark** | QA regression, diagnostic anchor, evaluator calibration, canonical examples; often also P4 | Curated representative example with explicit expected properties and documented review rationale |

A C2 gold item may be P0, P3, or P4 depending on what it benchmarks. Gold describes confidence and curation, not difficulty.

### Initial launch rule

Until automated QA is proven against the gold set and real content-error data, **every new generation batch receives human review before learner publication**. Later automation may reduce routine human review for low-stakes Training-approved material, but it may not reduce the P4/gold human-signoff requirement without Stage 26 evidence showing the replacement is equally reliable.

This costs owner time but avoids recurring model cost and protects the early product from “AI exercise soup.”

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Generation and QA pipeline concept

Every learner-facing content item follows this conceptual pipeline. The implementation may combine steps, but none of the product gates may disappear.

### Gate 1 — eligibility and brief

Confirm:

- intended task family/rung/evidence role;
- target blueprint version where relevant;
- Corpus support and confidence;
- rights-safe inputs;
- freshness/diversity need;
- expected approval level.

If the required source rights are unclear, switch to an abstract Corpus-derived brief rather than carrying source wording into the candidate.

### Gate 2 — semantic/task design

Define the **information structure and answer/rubric logic before polishing the German**.

Examples:

- Reading: facts, relationships, decisive evidence, question intent, and distractor failure reasons;
- SB: connected-text intent, each gap’s required function, and distractor rationale;
- Listening: scenario, speakers, information timeline, correction/negation events, decisive details, and questions;
- Writing: recipient, purpose, source context, content-point obligations, and acceptable interpretation space;
- Speaking: shared goal, private/different inputs, partner roles, useful constraints, and multiple valid interaction paths.

This reduces the chance that a fluent paragraph is later forced into an ambiguous question.

### Gate 3 — language/media creation

Create the natural German stimulus, options, prompt wording, script, or partner material at the intended linguistic profile.

Audio is produced only after the script itself passes semantic and language review.

### Gate 4 — deterministic structural validation

Validate all properties that should not need judgment, for example:

- required item/option/content-point counts;
- unique IDs and complete metadata;
- no missing stimulus/asset;
- no duplicated answer options;
- answer-position/candidate-use constraints;
- shared-bank constraints in SB2;
- task-instruction and response-format consistency;
- audio duration/playback metadata;
- Writing content-point presence;
- Speaking role/input completeness;
- target-version presence for P4;
- rights and attribution status.

Failure returns the candidate to Draft; it is not repaired dynamically during a learner attempt.

### Gate 5 — independent answer/rubric validation

Validate the candidate **without relying on the generator’s confidence in its own answer**.

Objective content requires an independent solve/reasoning pass plus reviewed evidence for the key. Productive prompts require rubric/semantic validation rather than a single expected response.

Disagreement sends content to human review or quarantine. The learner is never used as the ambiguity detector by default.

### Gate 6 — naturalness and register review

Judge whether the content sounds like plausible German for its genre, relationship, and modality. This is separate from grammatical correctness.

A grammatically correct but obviously machine-assembled passage fails this gate.

### Gate 7 — difficulty and target-fit review

Check the intended difficulty axes independently. A candidate is not accepted as P2/P3/P4 merely because a model labels it “B1.”

For P4, compare the complete form against current approved target characteristics and curated reference/gold anchors.

### Gate 8 — anti-copy and anti-repetition review

Check:

- exact duplication;
- near duplication;
- distinctive source-phrase/configuration overlap;
- same semantic frame with cosmetic noun/date changes;
- repeated answer-position patterns;
- excessive reuse of names, topics, settings, or prompt skeletons.

Assign the final content-family identity used for learner freshness.

### Gate 9 — media/render/interaction validation

For audio and interactive content, validate what the learner actually receives, not only the source script.

This includes pronunciation of names/numbers/dates, voice/speaker mapping, clipping, silence, speed, turn order, private-information boundaries, playback behavior, and question alignment.

### Gate 10 — publish with a fixed approval/version state

Published content receives an explicit approval level and version. Material edits create a new version so prior learner evidence remains explainable.

### Gate 11 — post-publication quality loop

Learner reports, observed answer disputes, evaluator disagreement, unusual failure patterns, naturalness complaints, and target-blueprint changes can quarantine or downgrade an item after publication.

Content quality is therefore maintained over time rather than assumed permanent.

---

## 4.2 Answer validation

### Objective questions

**Decision:** Every scored objective item must have a defensible answer contract before publication.

Required rules:

1. Exactly one keyed answer exists unless the verified task type explicitly permits another structure.
2. The correct answer is supported by the stimulus/task alone; no external cultural or factual knowledge is required unless that knowledge is intentionally part of a valid target pattern.
3. The item stores a concise **answer rationale** identifying the decisive evidence or language relationship.
4. Every distractor has a **distractor rationale** explaining why it is plausible and why it is wrong.
5. Distractors should fail for exam-relevant reasons—partial match, wrong qualifier, corrected detail, wrong main idea, semantic/grammar mismatch—not arbitrary trick wording.
6. An independent validator must be able to solve the item from the learner-visible content without seeing the generator’s intended key first.
7. Generator/validator disagreement, multiple defensible answers, or a rationale that depends on “what the author probably meant” causes quarantine.
8. Reordering the same answers or changing only names/numbers does not create a fresh item family.
9. Answer positions and candidate-bank use vary enough that position patterns cannot become a solving strategy.
10. If a published item is later found ambiguous, the learner’s affected result is invalidated rather than retroactively forcing one answer to remain “correct.”

### Writing prompts

Writing has **no single gold response**.

Prompt validation must establish:

- recipient relationship and register are clear;
- communicative purpose is plausible;
- required content points are distinct enough to judge independently;
- each point has a defined semantic obligation and acceptable interpretation space;
- two content points do not accidentally demand the same sentence/idea;
- several materially different B1-sufficient responses could succeed;
- prompt wording does not secretly require advanced cultural knowledge;
- the task can be completed within the intended rung/time without hidden requirements;
- sample responses at clearly weak, B1-sufficient, and stronger levels can be scored consistently enough against the shaped rubric.

A model answer is optional teaching/calibration material. It is never the answer key against which the learner’s wording is compared literally.

### Speaking prompts and partner content

Speaking validation must establish:

- there is a real communicative reason to speak;
- the learner has enough information to participate but is not given the partner’s private input when the task depends on information difference;
- the partner has a clear role, goal, and boundaries;
- S1 requires reciprocal behavior rather than only a memorized self-introduction;
- S2 paired inputs contain meaningfully different viewpoints/information and permit authentic response;
- S3 contains a shared goal plus negotiable choices/constraints and **no single correct plan**;
- partner branches do not lead the learner toward a hidden answer;
- several valid interaction paths can satisfy the task;
- fixed/prerecorded branches remain internally coherent;
- adaptive partner turns preserve the scenario and do not become coaching during the clean attempt.

---

## 4.3 Difficulty controls

**Decision:** Content difficulty is a profile of explicit axes, not a single CEFR label or model-generated “difficulty score.”

### Shared axes

Every content brief may control:

1. vocabulary frequency/domain familiarity;
2. sentence length and grammatical density;
3. concreteness versus abstraction;
4. explicit wording versus paraphrase;
5. stimulus length per decision;
6. number of decisions/candidates;
7. number of simultaneous constraints;
8. distractor semantic closeness;
9. inference/cross-sentence or cross-turn burden;
10. negation/restriction/correction density;
11. information density and memory burden;
12. assistance availability;
13. time pressure;
14. sequencing/endurance;
15. production openness;
16. interaction unpredictability;
17. audio speed, speaker count, pronunciation variability, and playback rule where applicable.

### Progression rule

When producing a lower-difficulty equivalent, change only the axes necessary to make the target mechanism reachable.

Examples:

- a P0 Reading matching task may use shorter texts and clearer constraints while still requiring need-to-notice matching;
- a P1 Listening task may reduce information density or speech speed without turning into transcript reading;
- a P2 Writing task may retain the full communicative mechanism but offer fewer/clearer content obligations and on-request support;
- a P3 Speaking task may keep B1 language and open responses while using a more controlled partner than P4.

A candidate that becomes a generic vocabulary/grammar drill is no longer a lower-difficulty variant of that exam task; it is repair content and must be labelled accordingly.

### Calibration rule

Initial difficulty comes from target/reference characteristics, Corpus evidence, expert review, and gold comparisons. Later learner performance may recalibrate it. Stage 21 does **not** invent precise numeric thresholds before data exists.

A generator’s self-assigned “B1” label is never sufficient for P4 approval.

---

## 4.4 Anti-copy, anti-repetition, and freshness

### Content family is the unit of independence

**Decision:** Every item belongs to a **content family** representing the underlying scenario/information configuration and answer path.

A new database ID is not fresh when the learner has effectively seen the same task before.

The following normally belong to the same family:

- exact duplicates;
- a source item and a close paraphrase of it;
- the same Reading passage with reordered questions;
- the same cloze with shuffled options;
- the same Listening script spoken by a different voice;
- the same decisive facts with changed names/dates only;
- the same Writing prompt with cosmetic nouns replaced;
- the same Speaking planning scenario with only superficial object/place substitutions;
- an item whose answer path is obvious because the learner has already seen the explanation/model.

### Fresh-equivalent rule

A valid fresh retry preserves the **capability and approximate difficulty** while changing enough of the semantic surface that the learner must solve the capability again.

Normally vary at least the scenario/information configuration and decisive language realization, and when appropriate also topic/genre/distractor instantiation. Do not vary so much that a different skill becomes the main challenge.

### Per-learner serving rules

- Once an answer/model has been exposed, that family cannot count as a clean independent retry/readiness attempt for that learner.
- Explicit review of an old item is allowed as teaching, but it is labelled repetition and cannot masquerade as fresh transfer.
- Delayed review should normally introduce broader topic/genre variation than the same-session retry.
- Mocks and target-condition forms use unseen independent families for that learner.
- A compromised/abandoned mock form is considered exposed for any parts whose answers/stimuli were materially revealed, even if it did not produce valid evidence.
- The serving strategy avoids excessive repetition of the same names, cities, household situations, professions, recipient relationships, partner constraints, and answer positions across a short run of practice.

### Bank-level diversity rules

A large item count is not enough. Content coverage should be assessed across:

- task families;
- progression rungs;
- target capabilities;
- topic/domain;
- text/audio genre;
- communicative function;
- register;
- distractor archetypes;
- difficulty-axis combinations;
- speaker/voice patterns;
- Writing recipient/purpose combinations;
- Speaking interaction paths.

This prevents 500 cosmetic variants of one exercise from being treated as content scale.

---

## 4.5 Natural German quality requirements

### Shared standard

**Decision:** Learner stimuli must sound like language a plausible German speaker, writer, business, institution, or exam author could reasonably produce for that genre.

Correct grammar is necessary but insufficient.

Reject content that exhibits patterns such as:

- vocabulary or grammar visibly stuffed into the text to satisfy tags;
- English-like translated syntax or discourse;
- generic AI openings/conclusions repeated across items;
- implausibly complete explanations in short notices/ads;
- over-symmetric paragraphs or dialogue turns;
- repeated use of the same placeholder names, cities, prices, dates, or professions;
- distractors created through awkward wording that no real speaker would use;
- contradictions introduced only to make a question difficult;
- excessive explicitness that removes the intended inference;
- obscure real-world trivia or current-events facts that become accidental knowledge tests;
- culturally narrow assumptions unrelated to the target skill;
- unnatural formality/informality for the relationship;
- prose written to be read silently used unchanged as spoken dialogue.

Prefer timeless or slowly changing functional scenarios unless current facts themselves are important to the task. This reduces maintenance and accidental factual errors.

### Reading

Reading passages/notices should:

- have a clear genre and communicative purpose;
- contain a coherent information structure independent of the question set;
- distribute answer evidence naturally rather than placing each answer in formulaic order;
- use paraphrase as normal communication, not a thesaurus substitution exercise;
- make distractors plausible from the text while still defensibly wrong;
- preserve realistic compression in ads/notices where appropriate;
- avoid making the correct option uniquely longer, more grammatical, or more detailed by accident;
- preserve B1-suitable imperfections/ordinary style where genre-realistic rather than making every text polished corporate German.

### Language Elements

Connected cloze texts should:

- read as coherent texts before gaps are removed;
- use each gap because the language relationship is meaningful in context;
- avoid sentences written solely to force a grammar phenomenon;
- make distractors plausible enough to diagnose a real distinction but not ambiguous;
- preserve discourse coherence across the full text, especially SB2;
- vary answer positions and candidate-bank roles.

### Listening scripts

Listening scripts must be written **for speech**.

They should:

- use plausible spoken turn length and discourse markers;
- allow natural contractions, reformulation, hesitation, or correction only when appropriate for the target/rung;
- avoid dense written syntax that sounds unnatural when read aloud;
- use numbers, dates, names, addresses, and corrections in a way a speaker would naturally say them;
- preserve the intended target cue without exaggerated emphasis;
- avoid making the correct answer obvious through unnatural pauses or stress;
- keep speaker roles and information consistent;
- use target-appropriate conversational speed rather than making “hard” mean merely fast.

### Writing prompts

Writing scenarios should:

- give the learner a believable reason to write;
- make the recipient relationship/register unambiguous;
- provide enough context to answer without requiring hidden facts;
- create content points that are distinct, actionable, and semantically judgeable;
- avoid four repetitive variants of the same communicative function;
- leave room for the learner’s own details/opinion where appropriate;
- allow several B1-sufficient solutions;
- avoid ornate source messages that are harder to decode than the intended Writing task.

### Speaking prompts

Speaking scenarios should:

- invite genuine exchange rather than recitation;
- create opportunities to ask, react, justify, agree/disagree, propose, negotiate, and repair;
- keep topics familiar enough that world knowledge does not dominate language ability;
- make partner constraints plausible rather than adversarial for its own sake;
- support several coherent paths and outcomes;
- avoid scripted sequences in which every learner is expected to say the same sentence;
- ensure S2 private/different inputs and S3 shared planning constraints are internally consistent.

---

## 4.6 Generated-audio requirements

**Decision:** Audio approval applies to the final rendered asset, not only the script.

### Source strategy preserved from Stage 11

- **P0–P2:** reviewed original scripts with batch-generated, cached TTS are the normal low-cost default.
- **P3:** high-naturalness reviewed TTS remains acceptable for much routine work, with deliberate voice diversity and some independently validated/human assets.
- **P4/readiness:** prefer native-human recordings or premium-generated audio that has been human-audited and calibrated against current target characteristics.
- Maintain a small reusable human/native **audio benchmark bank** for calibration and learner exposure.

### Audio acceptance rules

Before publication, verify:

- script-to-audio fidelity;
- natural pronunciation and prosody;
- correct pronunciation of names, places, numbers, dates, times, prices, abbreviations, and spelled information;
- speaker identity consistency;
- no clipping, missing words, accidental silence, duplicated segments, or volume discontinuity that changes intelligibility;
- intended speech rate and connectedness;
- intended correction/negation/restriction cues are audible but not artificially emphasized;
- target playback metadata and question alignment;
- no synthetic artifact that supplies an unintended clue or makes a key word uniquely hard to understand;
- voice diversity across the bank so readiness is not learned against one voice/style.

Changing only the TTS voice does not create a fresh content family.

If the final audio is bad, the learner result is invalid even if the script and answer key were correct.

---

## 4.7 Curated gold content

**Decision:** Bestehen requires a deliberately small but high-quality gold bank. Bulk generated content cannot validate itself.

Gold content is necessary in the following roles:

### 1. Diagnostic anchors

The initial diagnostic needs reviewed examples across all five areas so routing quality is not dominated by content defects.

### 2. Task-family benchmarks

Maintain representative gold examples for every TELC task family and major progression rung used to calibrate structure, naturalness, difficulty, distractor quality, media behavior, and generation prompts/briefs.

### 3. P4/readiness and mock forms

Maintain enough independent gold/readiness-approved forms that a learner can satisfy Stage 15–17 freshness and consistency requirements without seeing near-duplicate content.

**Launch constraint:** Bestehen must not expose a Ready-to-Book path unless the approved content inventory can support the required clean full mock plus independent written/oral confirmations on genuinely fresh families. Exact inventory volume is a launch-planning decision based on pilot exposure, but independence is non-negotiable.

### 4. Writing/Speaking evaluator calibration

Maintain curated prompts and response/interaction examples spanning clearly weak, B1-sufficient, and stronger behavior, including acceptable alternative answers and edge cases. These are used to check evaluator consistency and prevent the evaluator from learning one preferred model response.

### 5. Audio calibration

Maintain native-human or strongly audited target-style audio across representative task families, voices, numbers/details, and conversational conditions.

### 6. QA regression

Gold items include intentionally difficult edge cases—close distractors, valid alternative wording, ambiguous-looking-but-resolved examples, register differences, corrections, negation, multiple valid S3 plans—so changes to generation/validation can be tested against known expectations.

Gold content may be original, licensed/reusable reference material, or AI-assisted; its defining property is **documented high-confidence review and representative calibration value**.

---

## 4.8 Content refresh and rotation

**Decision:** Content refresh is **coverage- and evidence-driven**, not a fixed “rewrite everything every month” cycle.

Generate, review, rotate, or retire content when one of these occurs:

- target blueprint changes;
- a task family/rung/capability lacks fresh eligible inventory;
- learner exposure is saturating a family or scenario pattern;
- a topic/genre/register/voice group is materially overrepresented;
- Corpus provides stronger/new evidence that changes priority or target characteristics;
- difficulty calibration shows a bank is systematically too easy/hard;
- content reports or QA metrics expose a quality cluster;
- a rights/source status changes;
- an evaluator/generation change reveals a previous class of weak prompts/items.

### Rotation rules

- Stable high-quality content does not need regeneration merely for novelty.
- Rotation chooses a fresh eligible family that still matches the coach’s capability/difficulty goal.
- Diversity never overrides validity or makes two attempts incomparable when the coach needs a controlled transfer check.
- Gold/P4 forms rotate more conservatively and remain version-locked once used for a measured attempt.
- Retired content is not silently deleted from historical evidence references; it receives a status explaining whether prior evidence remains valid, becomes weaker, or is invalidated.

### Favor low-maintenance scenario facts

Prefer everyday functional situations whose facts can be internally defined by the task. Avoid unnecessary dependence on current prices, laws, train timetables, famous people, live events, or changing public facts. If a task needs real current information, it requires a specific freshness/source check and should be treated as higher-maintenance content.

---

## 4.9 Source attribution

**Decision:** Attribution follows the content actually shown, not the hidden intelligence that informed it.

### Exact reused source content

When C1 source content is displayed:

- satisfy the license/source’s required attribution;
- preserve required author/provider/license notice where applicable;
- do not imply official endorsement or affiliation with TELC or another provider;
- place attribution where it does not reveal an answer or undermine a measured attempt; pre-task, post-task, or content-detail placement may vary by requirement.

### Original App content

Original C2/C3 content is labelled as Bestehen practice. It does **not** cite a reference exam as though the displayed wording came from that source.

The product may state that a task is **“based on the current TELC B1 task format”** or equivalent factual target language where appropriate, while preserving the shared identity rule that Bestehen is not an official TELC product.

### Internal provenance

Original content still keeps internal provenance to:

- the target blueprint/version;
- Corpus intelligence/version;
- contributing aggregate pattern evidence;
- generator/author and validation versions where useful;
- approval/reviewer state.

This provenance supports audit and regeneration without turning the learner UI into a Corpus browser.

---

## 4.10 Content-error reporting and correction

**Decision:** Every learner-facing task/result has a low-friction **Report a content problem** path.

Suggested report reasons:

- answer seems wrong;
- more than one answer seems valid / ambiguous;
- German sounds unnatural;
- audio problem;
- prompt/instruction is unclear;
- speaking partner/scenario problem;
- source/attribution concern;
- other content issue.

The report should automatically attach the content identity/version and relevant attempt context so the learner does not need to describe the whole task manually.

### Learner trust rule

Reporting an item does not itself mark the learner correct or incorrect. It opens a content-quality review. The product should avoid defensive copy such as “the official answer is…” when the item has not yet been revalidated.

### Quarantine and severity

An item is removed from future scored serving immediately when there is credible evidence of a material defect such as:

- multiple defensible answers;
- wrong key;
- missing/contradictory stimulus;
- materially unnatural language that changes interpretation;
- broken/misaligned audio;
- wrong prompt obligations;
- partner behavior that violates the scenario;
- invalid rights/source status;
- current-target mismatch for a claimed P4 form.

Lower-severity style reports may wait for normal review without blocking all use when they do not affect validity.

### Evidence correction

If a published content defect makes a learner attempt unfair or unsupported:

1. mark the affected observation **invalid/excluded** for the relevant capability/readiness claim;
2. remove any mistake event or weakness evidence that depended on it;
3. recompute derived mastery, confidence, review obligations, and readiness from the remaining valid evidence;
4. reopen a needed fresh check if the removed item created an evidence gap;
5. explain any learner-visible change neutrally.

Example learner-facing behavior:

> “We corrected a problem in that Listening task. Your attempt no longer counts against your Listening evidence, and I’ll replace it with a fresh check.”

A content correction therefore cannot leave a false weakness behind.

### Versioning rule

A material correction creates a new content version. Historical attempts remain linked to the version actually seen. Do not silently mutate an old stimulus/key and pretend prior evidence came from the corrected form.

Precise raw-content retention after takedown and learner-data deletion behavior remains Stage 24 territory.

---

## 5. Edge Cases / Failure or Uncertainty Handling

## 5.1 Rights are unknown but the source is extremely useful

Keep the source C0/reference-only. Extract only approved abstract intelligence and create an original candidate from the content brief. Do not unblock exact display because the pedagogical value is high.

If later rights review confirms reuse, the source may become C1 without changing the status of already original App exercises.

## 5.2 A generated item is fluent but answer validation disagrees

Quarantine it. Fluency cannot compensate for ambiguity.

If the item is pedagogically valuable, revise the information structure or distractors and re-run the full relevant QA. Do not let a stronger model simply “vote” the learner wrong after publication.

## 5.3 The item is valid but difficulty is uncertain

Do not call it P4/readiness-grade. It may remain Draft or receive a lower Training-approved role after review if the task is still useful and the uncertainty does not undermine that claim.

Use learner data later to calibrate the difficulty; do not invent a precise level to fill metadata.

## 5.4 Corpus evidence is sparse or contradictory

Use the currently verified TELC blueprint and curated gold material as the target anchor. Broader Corpus evidence can expand variants, but weak/duplicated/unofficial observations cannot create a new target rule.

Record that the content brief has weaker Corpus support so Stage 22/26 can revisit it when evidence improves.

## 5.5 The learner exhausts fresh variants for a due repair

Prefer one of:

1. a fresh variant from another compatible topic/genre family;
2. a broader natural task that contains the same capability and can satisfy the obligation;
3. postponing the independent evidence claim until validated content exists.

Do not serve a near-duplicate and call it fresh merely to complete the loop.

Low-stakes runtime generation may provide learning practice, but it is not upgraded automatically to readiness evidence.

## 5.6 A target blueprint changes

Immediately stop calling affected old content current P4/target-condition until revalidated.

Historical learner capability may remain useful where the underlying behavior still transfers. Current readiness must follow Stage 15’s versioned-target rule and may require new approved forms.

Refresh priorities become:

1. gold/P4 and mock forms;
2. target-format P3 practice;
3. lower-rung variants whose mechanism materially changed;
4. low-risk generic repair content.

## 5.7 A reused source loses permission or receives a takedown request

Stop future learner display immediately and remove the asset from eligible serving. Keep attribution/status history needed to understand prior use subject to Stage 24’s retention/deletion contract.

If the issue is purely rights availability rather than content correctness, learner performance is not automatically “wrong”; Stage 22/24 must define what derived evidence may remain. Do not keep serving the source while that decision is pending.

## 5.8 A report challenges an official/reusable reference answer

Reference status does not make an answer immune to review. Quarantine the App-served item if the challenge is credible, validate the source/version and task logic, then either restore, correct with a new App version where permitted, or retire it.

The learner is never penalized merely because Bestehen trusted a reference source too strongly.

## 5.9 AI-generated German repeatedly passes grammar checks but feels unnatural

Treat this as a failed generation strategy, not a learner problem. Pause publication from that template/generator configuration, compare against gold/native material, and change the brief/model/review process before producing more volume.

Do not solve a systemic naturalness defect by manually patching thousands of near-identical items.

## 5.10 P4 inventory is too small for independent evidence

Do not weaken the Stage 15–17 freshness rules. The product must say that another clean readiness measurement is not currently available and prioritize creation/review of more independent P4 forms.

Content scarcity is a product limitation; it must not be hidden by reusing exposed forms as “fresh mocks.”

---

## 6. Relationship to Other Bestehen Stages

### Stage 03 — Initial Diagnostic

Diagnostic core content should come from curated gold or equivalent high-confidence reviewed assets. Routing must not depend on experimental generated items whose difficulty or answer key is uncertain.

### Stages 04–05 — Learner Model and Mistake Memory

Every evidence observation must retain the content/version/quality context needed to invalidate a defective item later. Content errors can remove mistake/weakness evidence; they cannot leave derived learner penalties behind.

### Stage 06 — Daily Coaching Engine

The content bank must expose enough eligibility information for the coach to choose a valid activity by task family, difficulty, freshness, evidence role, and quality. The coach should use a reviewed fallback rather than a lower-quality fine-grained item.

### Stage 07 — Core Learning Loop

“Fresh equivalent retry” now means a different content family with preserved capability/difficulty, not a cosmetic rewrite.

### Stage 08 — A1→B1 Progression

Content briefs use the explicit progression axes. Generation must preserve the exam mechanism while changing only the difficulty/support dimensions needed for reachability.

### Stages 09–10 — Reading and Language Elements

Objective content remains deterministic after review. Answer/distractor rationale, natural connected text, and ambiguity quarantine are mandatory. Runtime AI is unnecessary for scoring.

### Stage 11 — Listening

Stage 21 preserves batch-generated/cached TTS as the broad low-cost default and adds final-asset QA, content-family rules, and gold/native audio calibration.

### Stages 12–13 — Writing and Speaking

Productive prompts use semantic/rubric contracts and multiple valid responses, not one answer key. Speaking partner content must preserve role/interaction constraints. Adaptive runtime generation is justified only where response-dependent interaction adds value.

### Stage 14 — Review

Review obligations are satisfied with fresh content families. The bank must provide enough variants to test delayed transfer without answer memorization.

### Stage 15 — TELC Readiness

Only sufficiently approved, current, direct, target-mappable content/evaluation may set readiness. Content-quality uncertainty can lower confidence or exclude evidence.

### Stages 16–17 — Mocks and Ready to Book

Mocks use independent readiness/P4-approved forms. The content inventory must be sufficient to support fresh full and component confirmations; repeated exposed forms do not satisfy consistency.

### Stage 18 — Coach Personality

Content instructions and scenarios should use clear, practical language consistent with Bestehen’s calm exam-coach identity. No extra model call is justified merely to make fixed content “sound more AI-personal.”

### Stage 19 — Information Architecture

Raw Corpus provenance stays secondary. Source/attribution details may appear where required, but the learner’s main experience remains the task and coaching consequence.

### Stage 20 — Progress and Motivation

Content volume is not progress. “500 new exercises” does not become a learner achievement; progress remains evidence-backed readiness and capability movement.

### Stage 22 — Corpus → App Product Contract

Stage 22 should preserve this Stage 21 product requirement: the App needs enough information to distinguish raw/reference content, approved reusable assets, abstract generation intelligence, confidence/source breadth, target-version relevance, difficulty characteristics, rights/attribution requirements, and source/content-family similarity constraints.

The App does **not** need raw source access merely to serve normal daily practice.

### Stage 24 — Account, Data, and Portability

Stage 24 must define retention/deletion behavior for generated content, learner responses, content-version references, and removed/takedown assets without breaking the evidence-audit requirement.

### Stage 26 — Product Analytics and Evaluation

Stage 26 should measure at least:

- content-report rate by class/template/task family;
- confirmed defect rate and severity;
- answer-validator disagreement;
- human QA rejection rate;
- post-publication quarantine rate;
- naturalness failure themes;
- generated difficulty versus observed learner performance;
- exposure/family saturation;
- gold/regression pass rate when generation/evaluation changes;
- cost and human-review effort per accepted item/batch;
- whether content defects disproportionately affect readiness or productive skills.

Those measures are for calibration and operations, not learner progress.

---

## 7. Cost Notes

### 7.1 Preferred low-cost default

Bestehen should spend content-generation cost **once per accepted item/batch**, not once per learner attempt.

Preferred launch pattern:

1. derive reusable content briefs from Corpus/target knowledge;
2. batch-generate or author candidates offline;
3. run deterministic structural/duplicate checks;
4. use a cheap capable model for normal generation/semantic QA where AI is useful;
5. use an independent validator rather than repeated self-check loops;
6. human-review each launch batch while the system is uncalibrated;
7. batch-generate audio and cache the final approved asset;
8. serve/scoring from the approved bank deterministically;
9. generate more only when coverage, freshness, target change, or quality data justifies it.

This keeps normal Reading, Language Elements, Listening playback, Writing prompts, and mock serving close to zero marginal AI cost after approval.

### 7.2 When a higher-quality model is justified

A stronger model is justified **offline and selectively** when:

- a long/nuanced Reading passage or distractor set needs better semantic control;
- Language Elements naturalness or uniqueness is hard to validate cheaply;
- a Writing/Speaking prompt has overlapping obligations or subtle register/interaction constraints;
- an independent validator disagrees with the proposed key/rubric;
- a candidate is being promoted to high-stakes P3/P4/gold use and a stronger semantic review materially reduces risk;
- a new generation strategy/template is being benchmarked against gold content.

A stronger model is **not** justified merely because the item is “B1,” because a learner opened it, or because a cheaper model already produced a reviewed deterministic answer.

### 7.3 When human review is worth the cost

Human review is required for:

- launch generation batches until automated QA is empirically trustworthy;
- all Readiness/P4-approved complete forms;
- gold benchmark content;
- high-stakes audio calibration/audit;
- disputed or validator-conflicting objective answers;
- repeatedly reported unnatural/ambiguous content;
- new task templates before they can generate scale.

The personal-project trade-off is intentional: owner review time is cheaper and safer than paying a premium model on every learner interaction while the quality system is immature.

### 7.4 Runtime premium cost remains bounded by earlier stages

Stage 21 adds **no** requirement for always-on premium content generation.

Runtime premium use remains limited to capabilities already justified elsewhere, chiefly:

- productive Writing/Speaking evaluation when cheaper evaluation is insufficient;
- adaptive S2/S3 partner interaction where learner meaning must affect the next turn;
- rare high-impact uncertainty escalation.

Readiness recomputation, item scoring, review scheduling, content rotation, and ordinary coach copy do not need another premium model call.

### 7.5 Upgrade trigger

Increase model/human spend only when measured quality data shows the cheaper path is failing at a rate that threatens learner trust, evidence validity, target calibration, or the time needed to maintain the bank.

Do not degrade core exam fidelity merely to make generation free; pay selectively for the small number of high-stakes assets that protect the readiness promise.

---

## 8. Acceptance Criteria

### 8.1 Global learner-playable acceptance criteria

A content item may be served as scored practice only when all applicable statements are true:

- its intended learner use is rights-permitted;
- required attribution can be satisfied;
- its task family and progression role are explicit;
- its target blueprint/version is known where relevant;
- its learner-visible German is natural and genre/register appropriate;
- its semantic/task structure is internally coherent;
- its answer/rubric contract is defensible;
- objective keys have independent validation;
- distractors are plausible but uniquely wrong for documented reasons;
- productive prompts permit multiple valid B1 solutions where appropriate;
- difficulty is plausible for the claimed profile and uncertainty is not hidden;
- it is not a prohibited close copy of a reference source;
- it has a content-family identity suitable for freshness checks;
- final audio/media/interaction output is valid, not only the source script;
- required metadata for learner evidence and later invalidation exists;
- it has passed the approval level required for its intended evidence role.

Any material failure keeps the item out of scored learner use.

### 8.2 Readiness/P4 acceptance criteria

In addition to the global criteria, P4/readiness content must:

- use the currently approved target blueprint;
- reproduce the applicable format, timing, playback, preparation, interaction, and no-help rules;
- have human sign-off on the complete form/assets;
- be calibrated against curated target/reference/gold characteristics;
- use an independent content family unseen by the learner for a clean evidence claim;
- have no unresolved key/rubric/media/rights uncertainty;
- be version-locked for the measured attempt;
- support the exact evidence scope claimed by Stages 15–17.

### 8.3 “AI exercise soup” rejection test

A generated bank is not acceptable merely because individual items are grammatically correct.

Reject or redesign the generation strategy if the bank shows systematic:

- repetitive scenarios/names/structures;
- generic or translated-sounding German;
- grammar/vocabulary stuffing;
- shallow lexical-overlap distractors;
- cosmetic variations presented as fresh transfer;
- prompts with one obvious/model-like answer;
- difficulty created only through longer text or faster audio;
- inconsistent answer rationales;
- weak genre/register authenticity;
- target patterns unsupported by current Corpus/blueprint evidence.

Content scale is measured by **validated independent practice coverage**, not raw item count.

---

## 9. Decisions Made

- Corpus/reference content is evidence and calibration; App content is a separately governed learner-practice bank.
- Exact source material is shown only when explicit usage rights permit the intended use and all quality/attribution conditions are met.
- Unknown/reference-only rights default to original generation from abstract pattern intelligence rather than close paraphrase.
- Five content classes are used conceptually: C0 reference only, C1 reusable source, C2 curated gold original, C3 validated original practice, C4 adaptive/ephemeral interaction.
- Normal learner content is pre-generated/authored, validated, cached, and reused; runtime generation is exceptional and adaptation-driven.
- Generation begins from a structured Corpus/target-grounded content brief rather than raw source imitation.
- Content has approval levels from Draft/quarantine through Training, Independent-B1, Readiness/P4, and Gold.
- Launch batches receive human review until automated QA has been validated empirically; P4/gold retains human sign-off.
- Objective items require independent answer validation and documented distractor rationale; ambiguity causes quarantine, not learner penalty.
- Writing/Speaking prompts are validated against semantic/rubric obligations and multiple valid solutions rather than one model answer.
- Difficulty is controlled across explicit linguistic, reasoning, media, support, timing, production, and interaction axes.
- Freshness is enforced at the content-family level; cosmetic variants cannot create independent transfer or readiness evidence.
- Generated Reading, Language Elements, audio scripts, Writing prompts, and Speaking scenarios must satisfy modality-specific natural-German requirements.
- Listening uses reviewed original scripts and cached audio broadly, with stronger human-audited/native benchmark assets for P4/readiness.
- A curated gold bank is required for diagnostic anchors, task-family calibration, P4/mocks, productive evaluator calibration, audio calibration, and QA regression.
- Content refresh is triggered by coverage, exposure, blueprint, quality, rights, or calibration changes rather than arbitrary calendar churn.
- Source attribution follows the content actually displayed; original App content does not misleadingly cite reference items as its source.
- Learners can report content defects; material defects quarantine content and invalidate/recompute dependent learner evidence.
- Content creation spend is concentrated offline per accepted item/batch; stronger models and human review are reserved for disagreement, complex generation, P4/gold, and systemic quality issues.

---

## 10. Open Questions / Deferred Decisions

### No owner-blocking product question remains for Stage 21

The conservative rights default, quality tiers, gold-content requirement, and low-cost generation strategy can all be chosen responsibly from the current product constraints.

### Deferred to Stage 22 — Corpus → App contract

Define the exact product contract/version behavior by which the App obtains:

- target/task patterns;
- aggregate frequency and source breadth;
- difficulty characteristics;
- TELC relevance;
- rights/attribution status for reusable assets;
- provenance/confidence;
- content/source similarity or family constraints;
- current target-blueprint/version information.

Stage 21 defines **what must be possible**, not the payload or service architecture.

### Deferred to Stage 24 — retention/deletion

Define retention and deletion behavior for:

- learner-generated productive responses;
- raw audio;
- generated content assets;
- historical content-version references;
- takedown/source removal cases.

### Deferred to Stage 26 — empirical calibration and automation thresholds

Calibrate:

- how much human sampling can safely replace launch-time 100% batch review for low-stakes training content;
- acceptable content defect/report rates;
- difficulty models from real learner performance;
- diversity/exposure thresholds that trigger regeneration;
- QA model disagreement thresholds;
- cost/human-time per accepted item;
- whether any P4 QA step can later be automated without weakening evidence reliability.

### Architecture intentionally deferred

No decision is made here about model vendor, vector search, embeddings, storage, job queues, similarity algorithms, TTS provider, generation orchestration, caching implementation, or moderation infrastructure. Architecture must implement the product guarantees above without changing them.

---

## 11. Definition of Done Check

- [x] Relationship between Corpus/reference material and App-served content is defined.
- [x] Verbatim/direct-reuse rules are defined independently from authenticity.
- [x] Original-generation triggers and runtime-generation boundaries are defined.
- [x] Corpus-grounded generation briefs/templates are defined.
- [x] Generated-content QA and approval levels are defined.
- [x] Objective and productive answer-validation rules are defined.
- [x] Multidimensional difficulty controls are defined.
- [x] Anti-copy, anti-repetition, content-family freshness, and diversity rules are defined.
- [x] Natural German requirements for Reading and Language Elements are defined.
- [x] Generated-audio strategy and final-asset QA are defined.
- [x] Writing and Speaking prompt-generation requirements are defined.
- [x] Curated gold-content roles and readiness-grade requirements are defined.
- [x] Content refresh/rotation rules are defined.
- [x] Source attribution behavior is defined.
- [x] Content-error reporting, quarantine, correction, and learner-evidence repair are defined.
- [x] Low-cost generation/caching and selective premium/human-review rules are defined.
- [x] Acceptance criteria distinguish ordinary training from Readiness/P4 content.
- [x] No earlier App shaping decision was silently replaced.

**Stage 21 is complete when the live App checklist is reconciled with these decisions and the repository contains this document as the authoritative content-strategy artifact.**
