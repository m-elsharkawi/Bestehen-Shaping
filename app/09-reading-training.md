# Bestehen / App — Stage 09: Reading Training

> **Status:** Stage 09 product shaping in progress — first decision set captured
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Reading promise:** Train the learner to understand the German that TELC B1 requires **and** to solve each reading task with the right reading behavior, while progressively removing support until performance is independent and exam-realistic.

## 1. Purpose and Scope

This document defines the learner-facing Reading coaching experience for Bestehen / App. Reading is not treated as a generic collection of texts followed by comprehension questions. It is a set of exam-relevant task families that require different combinations of language comprehension, gist, selective scanning, detailed evidence retrieval, paraphrase recognition, inference, constraint checking, distractor rejection, and pacing.

Stage 09 applies the common product loop — **Observe → Attempt → Diagnose → Repair → Retry → Remember** — to Reading and makes the Stage 08 A1 → B1 progression concrete for the TELC B1 reading task families.

This is product shaping rather than implementation architecture. It defines what must happen, what evidence must be preserved, and what the learner should experience. It does not choose storage, UI frameworks, model providers, or final readiness coefficients.

### In scope

- the current TELC B1 Reading task families and their solving demands;
- lower-difficulty exam-shaped variants for learners below B1;
- reading skill and strategy mapping;
- vocabulary and paraphrase/synonym assistance and training;
- Reading-specific exercise behavior that later sections of this document will complete with scanning/detail practice, distractor feedback, timing, diagnosis/repair, content-source policy, and readiness evidence.

### Out of scope

- Sprachbausteine task design — Stage 10;
- full combined Reading + Sprachbausteine time allocation — Stage 10 and Stage 16;
- the calibrated TELC readiness formula and official-weight translation — Stage 15;
- full mock-exam sequencing — Stage 16;
- final screen architecture — Stage 19;
- corpus rights ingestion or source-classification mechanics — Bestehen / Corpus shaping;
- implementation details for content generation, validation, caching, or storage.

## 2. Inputs / Existing Decisions

Stage 09 preserves the project overview, identity, and App Stages 01–08:

- Bestehen is a calm, direct, evidence-based **personal German exam coach**.
- TELC B1 is the launch target; the learner may begin around A1.
- German is learned through exam-shaped activity rather than a conventional course sequence.
- Readiness is the primary progress concept, with evidence quality and uncertainty kept explicit.
- Reading is a direct-evidence lane; competence in another modality cannot substitute for Reading evidence.
- Mastery, confidence, freshness, assistance dependence, timing, and readiness contribution remain separate.
- The learner model already includes Reading nodes for gist/purpose, scanning, detailed comprehension, synonym/paraphrase recognition, inference, intention/stance where relevant, matching, restriction/negation handling, distractor rejection, unknown-word management, and time allocation/checking.
- Mistake Memory requires a defensible cause. One wrong choice does not automatically become a permanent weakness.
- The Daily Coaching Engine chooses the highest-value reachable work and protects both due repair and evidence gaps.
- The core learning loop requires narrow repair and a **fresh equivalent retry**, not the revealed original answer.
- Stage 08 progression uses P0 Supported Foundation → P1 Guided A2 → P2 A2/B1 Bridge → P3 Independent B1 Training → P4 Target Conditions, by task family rather than one global level.
- Assistance offered but unused does not weaken evidence. Assistance used before submission remains attached to the attempt.
- Answer-bearing help, direct solution exposure, and same-item repetition cannot masquerade as independent mastery.
- Corpus is the evidence/intelligence source. The learner receives coaching, not a raw Corpus browser.
- Real/reference material defines task shape and what is tested; the App should normally practice through original content unless exact reuse is permitted.
- The project begins as a personal project, so deterministic scoring, reviewed reusable content, precomputation, caching, and batch generation are preferred to per-attempt premium AI calls.

No earlier App decision is changed by this stage.

## 3. Current TELC B1 Reading Blueprint

### 3.1 Reference basis

The current general **Zertifikat Deutsch / telc Deutsch B1** product page continues to define Reading as **three parts**. In the official mock format, Reading and Sprachbausteine share a **90-minute** written block rather than giving Reading its own official standalone time allocation.

The three Reading parts are:

| TELC Reading part | Official target | Current task form | Scored decisions | Core solving behavior |
|---|---|---|---:|---|
| **Teil 1** | Globalverstehen | Match **5 short texts** to **10 headings**; each heading is used at most once | 5 | Identify the main point/purpose and recognize a paraphrased heading rather than matching isolated keywords |
| **Teil 2** | Detailverstehen | Read **one longer text** and answer **5 three-option multiple-choice questions** | 5 | Locate and integrate precise evidence, interpret relationships and qualifiers, and reject plausible but unsupported alternatives |
| **Teil 3** | Selektives Verstehen | Match **10 situations/needs** to a set of **advertisements/notices**; an explicit **x / no suitable ad** outcome is possible | 10 | Extract constraints from the need, scan selectively across many short texts, verify all required conditions, and reject partial matches |

This blueprint is the launch target for Reading coaching. Corpus may contain other A2/B1 providers and task forms, but those are supporting evidence. They must not silently replace the target TELC mechanism.

### 3.2 Product interpretation of the three parts

The official labels describe the dominant comprehension target, but Bestehen trains the actual solving behaviors underneath them.

#### Teil 1 — Global understanding through heading matching

The learner must usually resist a common trap: a heading and text may share vocabulary while expressing different main ideas. The decisive skill is selecting the heading that best compresses the **whole text's main point**.

Bestehen therefore treats Teil 1 as primarily:

- gist and main-point extraction;
- text-purpose recognition;
- synonym/paraphrase recognition;
- semantic discrimination between nearby headings;
- distractor rejection;
- efficient reading that avoids over-investing in minor details.

#### Teil 2 — Detailed evidence in a longer text

The learner must connect each question to evidence in the passage and choose one defensible answer. Depending on the item, the answer may require an explicit detail, combining nearby information, following a relation such as cause/result, or making a limited inference supported by the text.

Bestehen treats Teil 2 as primarily:

- question-led evidence search;
- detailed comprehension;
- local/cross-sentence integration;
- qualifier, restriction, contrast, and negation handling;
- inference when supported by the item;
- rejecting answers that sound reasonable but are not supported by the passage.

#### Teil 3 — Selective reading across functional notices

The learner first needs to understand the situation/need, convert it into decisive constraints, and then scan candidate notices. Topic overlap is not enough. A notice about flights is still wrong if it fails the age, destination, date, price, location, service, or other required condition.

Bestehen treats Teil 3 as primarily:

- extracting one or more constraints from a stated need;
- selective scanning rather than full linear reading;
- functional vocabulary and abbreviations;
- exact condition/restriction checking;
- multi-constraint matching;
- recognizing when **no candidate fully satisfies the need**;
- avoiding attractive partial matches.

## 4. Lower-Difficulty Variants

### 4.1 Principle: preserve the reasoning mechanism

A lower-difficulty Reading exercise is valid only when it preserves the target task's underlying reading behavior. Simplification may reduce vocabulary load, sentence complexity, text length, number/similarity of distractors, number of constraints, and time pressure. It must not turn the exercise into unrelated vocabulary flashcards or a different comprehension mechanism.

Lower-difficulty tasks are **training variants**, never representations of the official exam format. P4 is the only rung where a measured attempt must reproduce the applicable target task constraints.

### 4.2 Teil 1 progression — heading matching

| Rung | Training variant | What changes | What stays exam-shaped |
|---|---|---|---|
| **P0 Supported Foundation** | 2–3 very short texts, 3–5 headings | Concrete A1/early-A2 language; headings differ clearly; one main idea per text; selective vocabulary preview may be visible | Learner still chooses the heading expressing the whole text's main point |
| **P1 Guided A2** | 3–4 short texts, roughly twice as many headings as texts | Genuine A2 language; one or two headings share topic vocabulary; support moves on request | Gist before detail; one heading per text; unused alternatives create distractor pressure |
| **P2 A2/B1 Bridge** | 4–5 texts with controlled B1-like paraphrase | Longer texts, more synonymy, closer headline alternatives, fewer direct lexical matches | Target matching logic and main-point discrimination |
| **P3 Independent B1** | Full or near-full task family with original B1 content | Authentic B1 language and distractor closeness; no default answer-bearing help | Same reasoning, comparable scale, independent attempt |
| **P4 Target Conditions** | Target-form set | Exact target-form scale/constraints and no learning help during measured attempt | Strong readiness evidence |

### 4.3 Teil 2 progression — detailed multiple choice

| Rung | Training variant | What changes | What stays exam-shaped |
|---|---|---|---|
| **P0 Supported Foundation** | One short functional/narrative text with 2 questions | Answers usually rest on one explicit sentence; language is concrete; question wording initially close to text | Learner must find evidence in a passage and choose one supported option |
| **P1 Guided A2** | Short-to-medium text with 3 questions | Some paraphrase between question and evidence; simple contrast/negation; distractors are plausible but clearly contradicted | Question-led detailed reading and evidence-based selection |
| **P2 A2/B1 Bridge** | Medium text with 3–5 questions | Cross-sentence links, closer distractors, more implicit relationships, controlled inference | Same MCQ reasoning and evidence requirement |
| **P3 Independent B1** | Full-length or equivalent original B1 passage with 5 items | Authentic B1 density and distractor quality; no default support | Independent detailed comprehension at target difficulty |
| **P4 Target Conditions** | Target-form set inside realistic written conditions | Exact target constraints and deferred feedback | Readiness-grade target-condition evidence |

### 4.4 Teil 3 progression — situation-to-notice matching

| Rung | Training variant | What changes | What stays exam-shaped |
|---|---|---|---|
| **P0 Supported Foundation** | 2–3 situations and 3–5 short notices | One decisive constraint per situation; high-frequency functional vocabulary; abbreviations expanded where needed | Learner extracts a need and finds the one notice that satisfies it |
| **P1 Guided A2** | 3–5 situations and 5–7 notices | Two conditions begin to matter; one partial-match distractor appears; simple abbreviations/time ranges are natural | Need → constraints → selective scan → verification |
| **P2 A2/B1 Bridge** | 5–8 situations with a larger candidate set | Multi-constraint needs, closer partial matches, more paraphrase, occasional no-match outcome | Authentic selective-reading strategy and rejection of incomplete matches |
| **P3 Independent B1** | Full or near-full original B1-equivalent set | Authentic density, variety, abbreviations, distractors and no-match logic | Independent target mechanism |
| **P4 Target Conditions** | Target-form set | Exact target-form scale/constraints and no coaching during attempt | Strong readiness evidence |

### 4.5 Difficulty controls shared across Reading

Reading difficulty is adjusted through observable dimensions rather than a vague “A2/B1” label:

1. vocabulary frequency and domain familiarity;
2. sentence length and grammar density;
3. explicit versus paraphrased correspondence;
4. amount of text per scored decision;
5. number of candidate answers/texts;
6. distractor semantic closeness;
7. number of simultaneous constraints;
8. explicit detail versus cross-sentence/inference demand;
9. frequency of negation, exception, restriction, or contrast cues;
10. functional compression such as ads, abbreviations, prices, schedules, and conditions;
11. assistance availability;
12. time pressure and sequencing.

When a learner hits a wall, the coach should normally restore **one causal support axis** or reduce one difficulty dimension rather than collapse the whole task to a much easier level.

## 5. Task → Reading Skill Map

### 5.1 Skill families

Stage 09 uses the Reading skill nodes already established in the learner model and makes their task relevance explicit.

| Reading capability | Teil 1 Global | Teil 2 Detail | Teil 3 Selective | Coaching interpretation |
|---|:---:|:---:|:---:|---|
| Gist / main point | **Primary** | Supporting | Supporting | What is this text mainly saying or doing? |
| Text purpose/function | **Primary** | Supporting | Supporting | Inform, offer, explain, report, advise, invite, restrict, etc. |
| Scanning for target details | Supporting | **Primary** | **Primary** | Locate only the information needed for the current decision |
| Detailed comprehension | Supporting | **Primary** | Important | Interpret exact meaning after locating a candidate segment |
| Synonym/paraphrase recognition | **Primary** | **Primary** | **Primary** | Recognize the same idea when the wording changes |
| Local/cross-sentence inference | Occasional | **Important** | Occasional | Derive only what the text supports, not outside knowledge |
| Restriction/negation/exception handling | Important | **Primary when present** | **Primary** | Notice words such as `nur`, `nicht`, `außer`, conditions, dates, ranges and exclusions |
| Matching / constraint satisfaction | **Primary** | Low | **Primary** | Compare the target meaning/need with candidate options |
| Distractor rejection | **Primary** | **Primary** | **Primary** | State the decisive reason a tempting candidate fails |
| Unknown-word management | Important | Important | **Primary** | Continue using context/task evidence instead of stopping for every unknown word |
| Time allocation / moving on | Important | Important | Important | Avoid losing the shared written-block budget on one item |
| Checking / evidence confirmation | Important | **Primary** | **Primary** | Verify the chosen answer against the decisive text evidence |

“Primary” does not mean every item updates that node. Evidence is attributed only when the item and diagnosis genuinely isolate or support the capability.

### 5.2 Correct answers do not automatically prove every tagged skill

An item may require multiple skills to solve, but one correct choice normally supplies direct evidence only for the task result and the skills the item was deliberately designed/annotated to probe. Bestehen must not raise gist, synonym, inference, scanning, and distractor mastery together merely because one answer was correct.

Where fine attribution matters, the item should include reviewed metadata such as:

- primary intended reading skill;
- secondary skills;
- decisive evidence span or cue;
- expected paraphrase relation;
- distractor rationale/type;
- relevant restriction/constraint;
- linguistic and reasoning difficulty;
- mapping confidence.

If those mappings are uncertain, preserve broader task-family evidence rather than inventing precise skill mastery.

## 6. Vocabulary Assistance

### 6.1 Assistance goal

Vocabulary help exists to keep an exam-shaped attempt reachable **without removing the reading work that the task is meant to measure**. The default response to difficult text is not full translation.

### 6.2 Assistance ladder

Reading uses the Stage 08 availability states:

| Support | P0 | P1 | P2 | P3 ordinary practice | P4 / target probe |
|---|---|---|---|---|---|
| Small vocabulary preview | Default when needed | Default only for new/high-load domain, otherwise request | Rare default / request | Request makes attempt assisted | Unavailable during measured attempt |
| Selected word/short-phrase translation | Visible/request | Request | Request | Request makes affected evidence assisted | Post-attempt only |
| Sentence explanation | Default/request only when text is otherwise inaccessible | Request | Request | Post by default; request makes attempt assisted | Post-attempt only |
| Evidence-location / answer-narrowing hint | Only after meaningful attempt or clear wall | Request after attempt | Request after attempt | Repair only by default | Post-attempt only |
| Full translation/model solution | Repair exposure only | Repair only | Repair only | Repair only | After measured block only |

### 6.3 Vocabulary-preview rules

A preview is deliberately small and targeted.

- Preview only words/phrases whose absence would make a useful attempt unlikely at the learner's current rung.
- Do not preview the exact lexical/paraphrase relation the item is designed to test.
- Do not translate every unknown word in a text.
- Prefer a short German explanation, image, or simple synonym only when it is actually clearer for the learner; the learner's explanation language remains available where needed.
- A previewed item cannot later be treated as independently recognized vocabulary in that attempt.
- If a preview reveals a decisive answer, the item is no longer clean evidence for the affected comprehension decision.

Initial product default: **roughly 3–6 preview items for a P0/P1 task set when necessary, fewer as independence grows**. This is an operating guardrail rather than a scientific threshold and should later be tuned from completion and transfer data.

### 6.4 On-demand word help

Selecting a word may show:

1. a concise meaning relevant to the current context;
2. the base form where useful;
3. at most one short example if ambiguity remains.

The interaction must not expand into an unsolicited dictionary lesson. After the attempt, a word that caused a point loss may enter a targeted repair and later review. A word the learner merely looked up does not automatically become a known weakness.

### 6.5 Unknown-word strategy is itself trained

Bestehen teaches the learner to classify an unknown word before opening help:

- **Decisive:** the answer depends on it — use help in learning mode or mark it for repair.
- **Useful but inferable:** try context/paraphrase first.
- **Incidental:** continue without resolving it.

At P2/P3 the coach sometimes asks the learner to continue without a non-decisive translation and then confirms that the item was solvable. This builds target-condition resilience rather than creating translation dependence.

## 7. Synonym and Paraphrase Recognition Training

### 7.1 Product decision

Synonym/paraphrase recognition is a first-class Reading capability because TELC-style answers frequently express the same meaning with different wording. Training must go beyond memorizing word-pair synonyms: it includes phrases, changes of grammatical form, more general/specific wording, functional equivalence, and short sentence paraphrases.

### 7.2 Training progression

| Level | Exercise | Example behavior |
|---|---|---|
| Recognition | Choose which simple phrase means the same thing | `billiger` ↔ `kostet weniger` |
| Contextual equivalence | Identify the text phrase that supports a differently worded heading/question | heading says `Angebot für Familien`; text describes reduced fares for parents and children |
| Contrastive paraphrase | Choose the **true equivalent** among a near synonym and a misleading topic-related phrase | distinguish “available for students” from “available for all young people” |
| Transformation | Rewrite a short cue into another B1-appropriate expression | `nur am Wochenende` → `samstags und sonntags, nicht werktags` |
| Exam transfer | Solve a fresh Teil 1/2/3 item where lexical overlap is deliberately low | infer meaning from semantic equivalence rather than keyword matching |

Examples are illustrative and must not become a fixed phrase curriculum.

### 7.3 The “same idea, different words” micro-repair

When a miss is confidently diagnosed as paraphrase failure:

1. show the question/heading wording and the decisive text phrase side by side;
2. state the semantic link in one sentence;
3. ask for one or two quick equivalence judgments using new phrases;
4. serve a **fresh Reading item** that requires the same paraphrase skill.

Normal duration: **2–5 minutes**, within the Stage 07 repair boundary.

### 7.4 Avoid turning paraphrase training into keyword replacement

The learner should learn that equivalence depends on context. Bestehen therefore avoids presenting every paraphrase as a permanent one-to-one synonym pair. Where two expressions overlap only in a particular context, feedback says so.

A learner who succeeds only after the App highlights the relevant phrase has shown repair responsiveness, not independent scanning or paraphrase mastery.

## 8. Initial Exercise Flows

These flows establish the Reading-specific use of the common loop. Detailed diagnosis, distractor, timing, content, and evidence rules are completed later in this stage document.

### 8.1 Teil 1 training flow

1. **Goal:** “Find the heading that expresses each text's main point. Topic words alone are not enough.”
2. **Attempt:** read headings and texts; support is available according to the current rung.
3. **Result check:** deterministic answer key.
4. **If wrong:** compare the chosen and correct heading against the text's main point; identify whether the issue is gist, paraphrase, or a tempting topic-keyword distractor when evidence supports that diagnosis.
5. **Repair:** one narrow gist/paraphrase contrast.
6. **Fresh check:** a new short text and new heading set testing the same reading behavior.
7. **Remember:** save support use and whether the fresh check transferred.

### 8.2 Teil 2 training flow

1. **Goal:** “Answer from the passage, not from what seems generally true.”
2. **Attempt:** question-led reading with no feedback until submission.
3. **Result check:** deterministic answer key.
4. **If wrong:** reveal the decisive evidence span only after submission and compare it with the chosen option.
5. **Repair:** narrow work on the diagnosed detail, qualifier, inference, or paraphrase issue.
6. **Fresh check:** a new passage/item requiring the same capability.
7. **Remember:** record whether the learner could find and use evidence independently.

### 8.3 Teil 3 training flow

1. **Goal:** turn each situation into its decisive constraints before scanning the notices.
2. **Attempt:** scan candidates; full linear reading is not required.
3. **Result check:** deterministic answer/no-match key.
4. **If wrong:** compare the situation constraints with the selected notice and identify the first decisive mismatch.
5. **Repair:** short constraint-extraction or scanning exercise.
6. **Fresh check:** a new situation with new notices and the same constraint pattern.
7. **Remember:** store the strategy/constraint evidence and support used.

## 9. Decisions Made — First Decision Set

1. The launch Reading blueprint is the current three-part telc Deutsch B1 model: global heading matching, detailed MCQ reading, and selective situation-to-notice matching.
2. Every target task has P0–P4 lower-difficulty variants that preserve its reasoning mechanism while varying language, length, distractors, constraints, assistance, and timing.
3. Reading task performance is mapped to explicit skills; one correct answer does not automatically update every possible skill tag.
4. Vocabulary assistance is targeted and progressively faded; blanket translation and answer-bearing help cannot count as independent Reading evidence.
5. Synonym/paraphrase recognition is trained explicitly through equivalence, contrast, transformation, and fresh exam-shaped transfer rather than rote synonym pairs.

## 10. Open Questions / Deferred Decisions — Work in Progress

No owner question blocks the first decision set.

The remaining Stage 09 product decisions still to be captured in this document are:

- scanning versus detailed-comprehension coaching behavior;
- distractor explanation taxonomy and examples;
- timed versus untimed Reading modes and how the shared 90-minute written block affects target-condition claims;
- Reading-specific diagnosis and repair rules;
- reference/reusable versus original/generated content policy;
- Reading evidence emitted to the learner/readiness model;
- edge cases, cost notes, stage relationships, and final Definition of Done reconciliation.
