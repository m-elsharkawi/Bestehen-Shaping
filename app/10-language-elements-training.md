# Bestehen / App — Stage 10: Language Elements / Sprachbausteine Training

> **Status:** Authoritative Stage 10 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Training promise:** Teach only the grammar, connectors, word order, case/preposition patterns, and vocabulary-in-context that help the learner make better TELC decisions — then prove those patterns on fresh exam-shaped content.

## 1. Purpose and Scope

This document defines the complete learner-facing **Language Elements / Sprachbausteine** coaching experience for Bestehen / App.

Sprachbausteine is not treated as a miniature grammar course inserted into an exam-preparation product. It is treated as an exam area where the learner must choose the form or word that makes a connected text work. The coach therefore teaches grammar and vocabulary because they recover likely exam points, unlock other exam skills, or repair a demonstrated recurring weakness — not because a textbook syllabus says the next chapter is the dative case or subordinate clauses.

Stage 10 applies the common product loop — **Observe → Attempt → Diagnose → Repair → Retry → Remember** — to contextual language choices and makes the Stage 08 A1 → B1 progression concrete for the two TELC Sprachbausteine task families.

The product outcome is not merely “the learner knows more grammar rules.” It is that Bestehen can explain:

- which contextual language decision failed;
- whether the failure is primarily grammar, vocabulary, meaning, task execution, or still uncertain;
- which short repair is most likely to recover future points;
- whether the repair transfers to fresh content;
- whether the pattern recurs across independent opportunities;
- how strong the resulting evidence is for Language Elements and broader German capability.

This is product shaping, not implementation architecture. It defines learner behavior, content priorities, adaptive difficulty, feedback, evidence, scoring boundaries, Corpus inputs, and cost constraints. It does not choose a database, UI framework, model vendor, tagging algorithm, or final readiness formula.

### In scope

- current TELC B1 Sprachbausteine task patterns;
- P0–P4 lower-difficulty and target-condition variants;
- exam-relevance and Corpus-informed prioritization;
- conjunction/connector training;
- preposition/case training;
- word-order training;
- vocabulary-in-context and lexical-cohesion training;
- short exam-driven explanations and repair flows;
- adaptive cloze difficulty;
- recurring-weakness review behavior;
- deterministic scoring and diagnosis rules for objective items;
- evidence emitted to the learner model and later readiness model;
- low-confidence, ambiguous, stale-blueprint, and insufficient-Corpus handling;
- low-cost content/evaluation defaults.

### Out of scope

- final review scheduling across every skill — Stage 14;
- final TELC readiness coefficients and pass prediction — Stage 15;
- complete Reading + Sprachbausteine block simulation and mock cadence — Stage 16;
- final screen structure and copy hierarchy — Stages 18–19;
- generalized cross-skill content-generation QA — Stage 21;
- exact Corpus → App payload/API — Stage 22;
- accessibility equivalence for target-condition timing — Stage 25;
- calibrated thresholds and causal-validation analytics — Stage 26;
- technical content-generation, caching, storage, or model architecture.

---

## 2. Inputs / Existing Decisions

Stage 10 preserves the project overview, identity, and App Stages 01–09:

- Bestehen is a calm, direct, evidence-based **personal German exam coach**.
- TELC B1 is the launch target; the learner may begin around A1.
- German is learned through exam-shaped activity rather than a conventional A1 → A2 → B1 syllabus.
- Readiness is primary; lesson completion, grammar-topic completion, streaks, and raw exercise volume are not readiness.
- Written and oral pass risk remain separate.
- Language Elements is a distinct section-level evidence stream inside the written component.
- The Stage 03 diagnostic samples Language Elements with a short contextual cloze/sentence-choice cluster and gives only provisional evidence.
- The learner model separates contextual selection from spontaneous production. Correctly choosing a connector in a cloze does not prove the learner can use it spontaneously in Writing or Speaking.
- Mastery, confidence, freshness, assistance dependence, timing, and readiness contribution remain separate.
- Mistake Memory requires a defensible cause and independent recurrence before a fine-grained known weakness is created.
- Same-item repetition and immediate post-explanation success are weak learning evidence. Fresh delayed transfer is required for retained repair.
- The Daily Coaching Engine prioritizes pass risk, due repair, active weaknesses, evidence gaps, freshness, reachability, and coverage. Corpus frequency may raise relevance but never creates a learner weakness by itself.
- The core loop requires narrow repair, normally 2–6 minutes and ordinarily under eight minutes, followed by fresh equivalent content when a retry is useful.
- Stage 08 progression uses **P0 Supported Foundation → P1 Guided A2 → P2 A2/B1 Bridge → P3 Independent B1 Training → P4 Target Conditions**, by task family rather than one global CEFR level.
- Assistance offered but unused does not weaken evidence. Assistance used before submission remains attached to the attempt.
- Stage 09 established that Reading and Sprachbausteine share the official 90-minute block; internal practice budgets must not be presented as official standalone TELC time limits.
- Corpus supplies target/task intelligence, frequency, difficulty, source confidence, and skill relationships. The App owns learner evidence, personalization, explanations, and priority.
- Objective scoring, learner-state updates, and common feedback should be deterministic and inexpensive when reviewed metadata is sufficient.

No earlier App decision is materially changed by Stage 10.

### 2.1 Target-format verification note

The target format was rechecked on **19 August 2026** against the current official telc Deutsch B1 product page and the official downloadable `Zertifikat Deutsch / telc Deutsch B1 — Übungstest 1`.

The current official structure is:

| Family | Official target intent | Current model-test mechanism | Current model-test size |
|---|---|---|---:|
| **SB1 — Sprachbausteine Teil 1** | Grammatik | Connected-text cloze; each gap has three alternatives and one is selected | 10 gaps |
| **SB2 — Sprachbausteine Teil 2** | Lexik | Connected-text cloze; choose from a shared word bank; each candidate is used at most once | 10 gaps from 15 candidates |

The official model test assigns **15 points to each part, 30 points total**, and reports Sprachbausteine as **10% of the total 300-point examination**. Reading and Sprachbausteine share **90 minutes** with no official standalone time allocation for either Sprachbausteine part.

Official references used for this verification:

- [telc — Zertifikat Deutsch / telc Deutsch B1](https://www.telc.net/sprachpruefungen/deutsch/zertifikat-deutsch-telc-deutsch-b1/)
- [telc — Zertifikat Deutsch B1, Übungstest Version 1](https://shop.telc.net/media/catalog/product/file/2/0/20201225_5061-b00-010301_web.pdf)

**Product rule:** this is versioned target knowledge, not an eternal constant. Before content is labelled **P4**, a mock is called TELC-realistic, or official point conversion is shown, Bestehen must use a currently verified target blueprint. Older content can remain useful capability evidence when the underlying skill still transfers, but it must not silently retain current-target status after a material blueprint change.

### 2.2 Current Corpus-evidence availability

At the time of Stage 10 shaping, the repository contains no completed `corpus/` shaping-output folder and therefore no authoritative Corpus grammar-frequency table to consume yet.

That does **not** block this stage. Stage 10 defines:

1. the target-language concepts that the App must be able to prioritize;
2. the Corpus signals required to replace provisional ordering with evidence;
3. a conservative launch seed based on the verified TELC task mechanism and already-shaped learner model;
4. explicit fallback behavior when Corpus evidence is sparse, low-confidence, duplicated, or contradictory.

The provisional seed must be re-ranked when Corpus analytics become available. Stage 10 does not invent percentages or claim that an unmeasured grammar topic is empirically frequent.

---

## 3. Decisions and Rationale

### 3.1 Model Sprachbausteine as two distinct but related task families

**Decision:** Bestehen maintains separate SB1 and SB2 task-family evidence because they differ in target intent and solving mechanism.

- **SB1 — grammatical contextual choice:** the learner must decide which form makes the local and wider sentence/text structure grammatical and meaningful.
- **SB2 — lexical contextual choice:** the learner must decide which word or phrase makes the local and wider text lexically, semantically, and functionally coherent while managing a shared candidate bank.

They remain related because real cloze decisions are rarely “pure grammar” or “pure vocabulary.” A connector can require both semantic relation and word-order knowledge; a preposition can be a lexical chunk and a case-governance problem; a word-bank item can depend on syntax. The official part label is the **task intent**, not permission to shotgun-tag every error as grammar or vocabulary.

### 3.2 Teach contextual decisions, not chapter completion

**Decision:** A grammar concept enters active coaching when at least one of these is true:

1. it occurs materially in the verified TELC target or Corpus evidence;
2. the learner has a candidate/known weakness in it;
3. it is a prerequisite for a current high-value exam behavior;
4. it transfers to a pass-relevant Writing, Speaking, Reading, or Listening behavior worth verifying;
5. it is needed to make the next reachable Sprachbausteine rung meaningful.

A concept does **not** receive training merely because it is traditionally taught at A2 or B1.

This gives Bestehen a practical rule for scope control: **teach the smallest language distinction that changes an exam decision.**

### 3.3 Use Corpus frequency as a prior, not as learner truth

**Decision:** Corpus evidence influences **what is worth covering and how strongly it competes for practice time**, while learner evidence controls **what this learner is currently weak at**.

A common connector may deserve early coverage even before the learner has failed it. It cannot be labelled a weakness until the learner provides evidence. Conversely, a rare but repeatedly failed target-relevant pattern may become a high-priority personal weakness despite lower global frequency.

### 3.4 Keep explanations short enough to return to the exam task

**Decision:** The normal grammar explanation is a **micro-explanation**, not a lesson.

Default shape:

1. name what changed the answer;
2. show the decisive contextual cue;
3. give one practical rule or contrast;
4. optionally name the formal grammar term;
5. return to one or two controlled checks only if needed;
6. test a fresh equivalent cloze.

The learner should normally be back in an exam-shaped decision within **2–6 minutes**, preserving Stage 07's repair boundary.

### 3.5 Diagnose only what the item can actually isolate

**Decision:** A wrong cloze answer creates precise grammar/vocabulary evidence only when reviewed item metadata and the distractor design support that cause.

If two plausible causes remain — for example, unknown noun gender versus weak case knowledge, or connector meaning versus word order — the event stays broad or receives one short clarifying contrast. Bestehen prefers **“cause not yet clear”** to false precision.

### 3.6 Objective Language Elements should be zero-runtime-AI by default

**Decision:** Reviewed answer keys determine correctness. Reviewed item metadata, distractor rationale, learner history, and compact deterministic contrasts should handle normal diagnosis and repair selection.

AI is valuable mainly **offline** for generating and reviewing natural connected texts, plausible distractors, lexical banks, controlled-difficulty variants, and metadata. A routine learner cloze attempt should not trigger a premium model call.

### 3.7 Full target-condition timing exists only in the shared written block

**Decision:** Because TELC gives Reading + Sprachbausteine one shared 90-minute block, an isolated Sprachbausteine task can be target-format and target-difficulty but cannot by itself prove the complete official time-allocation condition.

Therefore:

- isolated P3 exercises can be practice-timed or target-pace probes;
- an isolated full-format SB1/SB2 set may supply strong pace evidence;
- **P4 timing evidence for the official allocation strategy is earned inside the combined Reading + Sprachbausteine block or a valid mock**, not from an invented official “Sprachbausteine = X minutes” rule.

This preserves Stage 09 and prevents the App from teaching a made-up exam constraint.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 TELC task-family model

### SB1 — Grammar in connected text

The learner reads a connected functional/personal text with gaps and selects one of three alternatives for each gap.

The task tests whether the learner can make local choices while maintaining sentence and text coherence. The official model-test examples demonstrate that the family can draw from multiple grammar domains within one text rather than isolate a single chapter.

Primary capability families include:

- conjunctions and connectors;
- main/subordinate-clause relationships and verb placement;
- articles, pronouns, and case marking;
- preposition choice and governed case;
- verb form, auxiliary/modal choice, tense, infinitive/separable constructions where relevant;
- adjective/nominal agreement where target evidence supports it;
- relative/reference forms;
- functional formality/person reference;
- other B1-relevant morphology/syntax supported by Corpus evidence.

**SB1 does not prove spontaneous grammar production.** It supplies direct contextual-selection evidence. A shared grammar node may later be verified in Writing or Speaking when productive transfer matters.

### SB2 — Lexis and cohesion in connected text

The learner reads a connected text and fills ten gaps from a larger shared bank. Some candidate words are unused.

Primary capability families include:

- contextual meaning and semantic fit;
- functional language and register;
- collocations and common chunks;
- connector/discourse relation choice;
- prepositional or governed lexical chunks;
- adverbial and temporal/logical cohesion;
- modal/functional phrasing;
- synonym and near-synonym discrimination;
- text-level coherence across more than one sentence;
- efficient candidate-bank elimination without losing semantic verification.

SB2 is **not** an isolated vocabulary-definition test. Knowing the dictionary meaning of a word is insufficient when the wrong candidate does not fit the text's function, collocation, syntax, or register.

### Shared task rules

1. Every scored gap must have one reviewed defensible answer under the intended target conditions.
2. A gap can map to one primary node and, when genuinely useful, one secondary/contributing node.
3. The surrounding text matters. Do not reduce every gap to a decontextualized sentence when wider context decides the answer.
4. A complete set mixes concepts only at the learner's reachable rung; targeted repair sets may isolate one concept temporarily.
5. Target-format practice uses **original reviewed texts** by default. Exact source material is displayed only when usage rights permit it.
6. Correct-answer positions/candidate order are varied; the learner should not learn bank or answer-position patterns.
7. Near-duplicate texts or the same gap with reordered options do not count as fresh transfer.

---

## 4.2 Exam-relevance and Corpus-priority model

### Core priority decision

Language Elements priority is determined by **target value × learner need × evidence quality × reachability**, with Corpus frequency acting as an evidence-backed target-value prior.

The App does not need one opaque numerical score. The first product uses an ordered decision model.

### Priority order

1. **Due/known learner weakness with meaningful TELC impact** — recurring connector, case, word-order, or lexical pattern due for repair/retention.
2. **Pass-relevant evidence gap or target-format weakness** — one of SB1/SB2 is under-evidenced, stale, or failing under B1/pace conditions.
3. **High-confidence Corpus core pattern** — frequent across independent target-relevant sources and useful across exam contexts.
4. **Prerequisite/reachability pattern** — a smaller language distinction that unlocks the next exam-shaped task.
5. **Coverage/maintenance** — avoid leaving important high-frequency families unknown while repeatedly practising a strength.
6. **Low-frequency enrichment** — only after stronger exam value and personal needs are covered.

### Corpus signals required by the App

Once Corpus analytics exist, each grammar/lexical node should conceptually be able to supply:

| Corpus signal | Why Stage 10 needs it |
|---|---|
| Target/provider task association | Separates TELC-target evidence from generic B1 occurrence |
| Independent occurrence frequency | Estimates how often a concept appears after deduplication |
| Source breadth | Distinguishes one repeated source family from a pattern seen across independent materials |
| Authenticity/confidence | Reduces influence of uncertain unofficial material without conflating rights |
| Blueprint/version relevance | Prevents obsolete target forms from dominating current priorities |
| SB1/SB2 association | Shows whether the concept tends to appear in grammar-choice, lexical-choice, or both |
| Distractor/confusion pattern | Identifies distinctions that actually create plausible wrong choices |
| Co-occurring grammar/lexical nodes | Helps build natural mixed sets and diagnostic contrasts |
| Topic/register context | Avoids teaching a form only in one memorized context |
| Difficulty distribution | Helps place the node at P0–P4 without a traditional chapter sequence |
| Rights/display status | Determines whether source text may be shown; does not change authenticity or frequency evidence |

### Frequency guardrails

Corpus frequency must be **deduplicated and confidence-aware**.

- Ten mirrors of one mock count as one underlying occurrence source, not ten independent exam signals.
- Current/relevant TELC evidence has more target-priority value than a large unrelated generic-B1 pool.
- Broader Goethe/ÖSD/DTZ/educational evidence can support transfer/general frequency but does not silently become TELC-format evidence.
- Low-confidence unofficial evidence may suggest a candidate priority but cannot by itself establish a “core TELC pattern.”
- Raw token frequency is insufficient. The product cares whether a form is **tested or decision-relevant**, not merely whether the word `und` appears often.
- Corpus priority changes what gets practised; it never changes demonstrated learner mastery without learner evidence.

### Provisional launch seed before Corpus analytics

Until a trustworthy Corpus ranking exists, Bestehen uses the following **coverage seed**, not a claim of measured frequency:

| Seed band | Language family | Reason for provisional inclusion |
|---|---|---|
| **Core seed** | Connectors/conjunctions + clause relationship + resulting verb position | Directly changes contextual meaning and structure; transfers broadly |
| **Core seed** | Prepositions + governed case + common contractions/chunks | Frequent functional relationship in connected text; grammar and lexicon interact |
| **Core seed** | Article/pronoun/case choices and basic agreement | Common contextual-form distinction and prerequisite for functional accuracy |
| **Core seed** | Main-clause/subordinate-clause word order, sentence bracket, modal/infinitive/separable patterns | High transfer value and directly coachable contextual choices |
| **Core seed** | Functional vocabulary, common collocations/chunks, discourse adverbs, register-sensitive choices | Central to SB2 lexical cohesion and productive exam language |
| **Supporting seed** | Relative/reference forms, adjective inflection/comparison, less-common verb/governance patterns | Train when target/Corpus evidence or learner recurrence justifies them |
| **Deprioritized by default** | Rare exceptions, literary/advanced structures, low-transfer rules beyond B1 | Poor expected exam return unless evidence says otherwise |

As soon as Corpus evidence is available, it may move concepts between bands. The App should preserve the reason for the move: **target frequency, learner recurrence, transfer value, or coverage**, not “because the algorithm says so.”

---

## 4.3 Conjunction and connector training

### Product decision

Bestehen trains connectors as a combination of **meaning relationship + syntactic consequence + contextual use**. It does not teach disconnected connector lists.

### Required relation families

The initial product must support Corpus-prioritized examples from at least these functional families:

- addition;
- contrast;
- cause/reason;
- result/consequence;
- concession;
- condition;
- time/sequence;
- alternative/choice;
- purpose where B1-relevant.

The exact connector inventory is Corpus-driven. Example families such as `weil/denn/deshalb`, `obwohl/trotzdem`, `wenn`, `aber/sondern`, or `damit` are useful pedagogically, but the product must not freeze a textbook list as the priority source.

### Three connector decisions

A learner can fail a connector item in three different ways:

1. **Relation:** Does the context need cause, contrast, consequence, condition, etc.?
2. **Lexical choice:** Which connector expresses that relation here?
3. **Structure:** What happens to clause/verb order with that connector family?

These should be separate diagnostic nodes when the item can isolate them.

### Connector repair flow

1. Ask/establish the semantic relation in plain language: “Is the second idea a reason, a result, or a contrast?”
2. Contrast the learner's choice with the correct relation.
3. Give the minimum word-order consequence when relevant.
4. Use one compact contrast where two connectors express related meaning with different structure.
5. Serve a fresh contextual cloze with different surface content.
6. Later embed the same relation in a mixed set; productive verification can be added in Writing/Speaking when useful.

### Word-order coupling

Connector coaching must preserve syntactic family differences:

- coordinating connectors that preserve ordinary main-clause verb position;
- subordinating connectors that create a subordinate-clause verb-final pattern;
- connector/adverbial elements that occupy a clause position while the finite verb remains second.

The learner-facing explanation starts with the usable behavior, e.g. **“After this word, the finite verb moves to the end”**, before formal labels such as *subordinating conjunction*.

### Near-confusion training

When Corpus or learner history shows recurring confusion, the repair should use **contrast pairs/sets** rather than reteach each item separately. Examples include:

- cause versus consequence;
- concession versus contrast;
- condition versus time;
- addition versus opposition;
- connector with normal V2 versus connector with verb-final clause.

The pair is treated as one repair family only when the semantic/syntactic relation is genuinely shared. Similar-looking words are not automatically grouped.

---

## 4.4 Preposition and case training

### Product decision

Bestehen teaches **meaningful preposition + case/chunk decisions in context**, not declension tables as the primary experience.

The diagnostic sequence is:

1. what relationship is being expressed — place, direction, time, recipient, reason, dependency, etc.;
2. which preposition/chunk fits that relationship;
3. which case/form follows in this use;
4. whether the remaining error is article/pronoun/adjective realization rather than preposition choice.

### Training families

The product must support Corpus-prioritized practice for:

- fixed/common preposition + case combinations;
- local/temporal functional prepositions;
- two-way preposition distinctions where B1-target evidence justifies them;
- verb + preposition chunks;
- adjective/noun + preposition chunks when target-relevant;
- common contractions and fixed functional expressions;
- case realization in articles/pronouns/adjectives after the governing choice.

### Cause-separation rules

- If the learner chooses the wrong preposition but the case would be correct for that preposition, diagnose **preposition/meaning or lexical governance** first, not “case weakness.”
- If the preposition is correct but the article ending is wrong, diagnose **case/form realization**.
- If the noun's gender is unknown and that alone causes the article choice, keep the cause as **lexical gender/word knowledge** or unresolved rather than pretending the case rule is weak.
- If a verb-preposition combination is conventional rather than predictable, teach it as a **chunk** and test it in context.
- If multiple forms are grammatically possible but change meaning, the item must make the intended meaning decisive or be invalidated.

### Repair format

Preferred repair:

1. show the functional relation or governing chunk;
2. show the required case only when it matters;
3. contrast one wrong/right context;
4. use one fresh cloze;
5. later change the noun/topic so the learner cannot memorize the surface phrase.

Declension tables may be available on demand as reference, but the default repair should not expand into a full case chapter.

---

## 4.5 Word-order training

### Product decision

Bestehen trains word order as **verb anchors and movable meaning blocks**, then adds terminology only when useful.

Initial target families include, subject to Corpus evidence:

- finite verb in second position in a main clause;
- verb-final subordinate clauses;
- inversion after a fronted time/place/connective element while preserving V2;
- modal/infinitive and auxiliary/participle sentence brackets;
- separable verbs;
- placement required by common B1 connector/clause patterns;
- pronoun/object/adverb ordering only when target evidence or recurring learner errors make it valuable.

### Word-order repair flow

1. Identify the finite verb or verbal bracket.
2. Identify the clause type/connector cue.
3. Mark the position the finite verb must occupy.
4. Move only the necessary blocks; do not rewrite the whole sentence.
5. Give one fresh rearrangement or cloze.
6. Return to a connected-text item where the same pattern is no longer visually scaffolded.

### Evidence boundary

A rearrangement exercise is controlled construction evidence. A three-option cloze is contextual-selection evidence. Neither alone proves spontaneous Writing/Speaking word order. If the same grammar node matters productively, the Daily Coaching Engine may later schedule a compact fresh Writing or Speaking verification without lowering those modalities in advance.

---

## 4.6 Vocabulary-in-context training

### Product decision

SB2 vocabulary is taught as **availability of the right word/chunk for this communicative context**, not isolated translation recall.

### Lexical capability families

- semantic fit;
- collocation;
- fixed/function phrase;
- register and recipient appropriateness;
- discourse connector/adverbial;
- governed preposition/chunk;
- synonym/near-synonym discrimination;
- temporal/logical cohesion;
- word-family/form distinction where the target mechanism requires it;
- candidate-bank elimination followed by positive context verification.

### Vocabulary repair sequence

1. Identify what role the gap needs: meaning, function, relation, register, or chunk.
2. Explain the decisive context in one sentence.
3. Contrast the chosen word with the correct candidate on the **one feature that matters here**.
4. If it is a collocation/chunk, show it as a unit rather than separate dictionary entries.
5. Test a fresh context with different nouns/topic where possible.
6. Schedule later retrieval only if the pattern is recurring/high-value; do not turn every encountered word into review.

### Candidate-bank strategy for SB2

At higher rungs, the learner practises a two-pass approach:

1. determine the likely grammatical/semantic role of the gap;
2. shortlist plausible bank candidates;
3. verify the best candidate against local **and** wider text meaning;
4. use already-filled choices to reduce the bank without assuming elimination proves understanding;
5. return to uncertain gaps rather than forcing a weak first guess.

Strategy evidence is recorded only when the behavior can be observed or defensibly inferred. The App does not claim “good elimination strategy” simply because the final answer is correct.

### Translation boundary

At P0/P1, selected word help may keep the text reachable. A translated/tested word does not become independent lexical mastery in that attempt. At P2/P3, on-request help creates assisted evidence for affected gaps. P4 measured attempts expose no answer-bearing vocabulary help.

---

## 4.7 Short exam-driven explanations and repair rules

### Default explanation contract

For a normal wrong gap, show at most:

1. **Outcome:** the chosen answer and the correct choice;
2. **Decisive clue:** the few words or relation that determine the gap;
3. **Practical rule:** one sentence;
4. **Contrast:** why the learner's option fails here;
5. **Next action:** one micro-check or fresh retry.

Deep grammar reference is available on demand, but it is not inserted into every loop.

### Working explanation templates

**Connector / word order**

> This sentence gives the **reason**. The connector used here sends the finite verb to the end. Check the relation first, then the verb position.

**Preposition / case**

> The preposition is correct; the remaining problem is the case form after it. Keep the same preposition and change only the article ending.

**Lexical chunk**

> Both words are possible German words, but only one forms the normal expression in this context. Learn the phrase as a chunk, then test it in a new sentence.

**Uncertain cause**

> The answer is wrong, but this item cannot tell whether the blocker was the word meaning or the case form. I’ll keep the result broad and use one short contrast before choosing a repair.

### Repair-size rules

- One primary concept per repair; at most one material contributor.
- Normal repair is **2–6 minutes**; eight minutes remains the normal ceiling from Stage 07.
- One or two controlled actions are enough when they make a fresh retry meaningful.
- Do not explain all three options when only one distractor matters to the learner's error.
- Do not teach every grammar rule present in the surrounding text.
- If the learner already demonstrates the rule during diagnosis, compress repair and move to a fresh check.
- If the issue is a prerequisite below the current task, repair that narrow prerequisite and keep the original target open.
- A model/solution exposure is repair evidence, not mastery.

---

## 4.8 Adaptive cloze difficulty

### Core decision

Cloze difficulty is multidimensional. Bestehen adjusts the **smallest causal axis** rather than using only “A2 item” versus “B1 item.”

### Difficulty axes

1. vocabulary frequency/familiarity;
2. sentence and text length;
3. grammar density;
4. number of gaps in one text;
5. local cue versus cross-sentence/context dependency;
6. number of choices/candidate-bank size;
7. distractor grammatical/semantic closeness;
8. single-concept versus mixed-concept set;
9. explicit lexical overlap versus paraphrase;
10. number of plausible candidates before wider-context verification;
11. assistance availability;
12. timing/pace pressure;
13. text register/topic familiarity;
14. target-format sequencing and deferred feedback.

### Progression by rung

| Rung | SB1 grammar-cloze variant | SB2 lexical-cloze variant | Assistance / evidence claim |
|---|---|---|---|
| **P0 — Supported Foundation** | 1–3 gaps in short connected text; usually 2 clearly contrasted choices; one high-value rule | 1–3 gaps with a small bank and strong contextual separation | Small preview/hint may be visible; open time; supported contextual-choice evidence |
| **P1 — Guided A2** | 3–5 gaps; three choices increasingly normal; genuine A2 forms and simple mixed concepts | 3–5 gaps; bank larger than gaps; common chunks/functions; mild distractors | Help moves to request; pace awareness appears; A2 working evidence |
| **P2 — A2/B1 Bridge** | 5–8 gaps using target-like three-choice mechanism; controlled B1 grammar density and closer distractors | 5–8 gaps with a target-like surplus bank; wider context and lexical cohesion matter | Most help on request; practice timing; B1-shaped transfer evidence |
| **P3 — Independent B1 Training** | Full/near-full original B1-equivalent 10-gap sets with target-like distractors | Full/near-full original B1-equivalent 10-gap sets with 15-candidate target-like bank | No default answer-bearing help; unassisted and target-pace probes; strong B1 task-family evidence |
| **P4 — Target Conditions** | Current verified SB1 mechanism inside valid combined written-block conditions | Current verified SB2 mechanism inside valid combined written-block conditions | Exact current target rules; no coaching during measured block; strongest readiness anchor |

P0 may use two choices only as a learning scaffold; it must never be mislabeled target-format evidence. P3 may use the exact surface mechanism, but full P4 timing/sequence realism still requires the shared written-block condition.

### Adaptation behavior

After enough comparable evidence, change **one axis at a time** where possible:

- reduce a hint before simultaneously increasing text length and distractor closeness;
- move a connector from isolated targeted gaps into a mixed set before adding hard timing;
- increase SB2 bank ambiguity while keeping vocabulary load stable when elimination/semantic discrimination is the target;
- add target pace only after the learner understands the task mechanism.

Use Stage 08's promotion, provisional-promotion, difficulty-wall, and fallback rules rather than inventing a second unrelated progression algorithm.

### Difficulty-wall examples

- **Grammar correct with hint, blank without hint:** restore on-request cue and re-test one fresh item later; do not lower every grammar node.
- **SB2 meaning correct when bank is small, collapses with 15 candidates:** keep lexical knowledge visible and train candidate management/semantic discrimination.
- **Untimed set accurate, timed set weak:** preserve language capability and diagnose pace/execution before reteaching grammar.
- **B1 mixed set fails because one prerequisite repeats:** isolate and repair that concept briefly, then return to mixed context.

---

## 4.9 Timed, untimed, and exam-realistic modes

### Language Elements timing ladder

| Mode | Typical rung | Evidence meaning |
|---|---|---|
| **Open learning** | P0–P1 | Language/context learning without exam-pace claim |
| **Pace awareness** | P1–P2 | Elapsed time or soft pace guidance; no forced finish |
| **Practice timed** | P2–P3 | Generous/realistic internal pace target; over-target completion remains valid learning evidence |
| **Target-pace probe** | P3 | Full/near-full B1 set without learning help; useful pace evidence, but not the official shared-allocation claim alone |
| **P4 combined block** | P4 | Reading + Sprachbausteine use the verified shared 90-minute rules with feedback deferred |

### No invented official minute split

Bestehen must not say “TELC gives you 10 minutes for Part 1” or “20 minutes for Sprachbausteine” unless a future official blueprint actually specifies such a rule.

The coach may recommend a **personal working budget** based on the learner's own valid practice/mock evidence. That recommendation is labelled strategy, e.g. “Your current plan is to finish both Sprachbausteine parts with enough time left for Reading review.” It can change as accuracy and pace change.

Until the learner has enough combined-block evidence, isolated Language Elements practice uses pace awareness or a clearly labelled **Bestehen practice target**, not a fabricated official limit.

### Timing diagnosis

- accurate but slow → positive language evidence, weaker timing/execution evidence;
- weak only under time pressure after reliable untimed performance → test pace/strategy before lowering grammar/vocabulary mastery;
- weak both timed and untimed → language/context cause remains more plausible;
- interrupted/technical timeout → invalid, not learner weakness;
- one slow set does not create a persistent timing weakness.

---

## 4.10 Recurring weakness review

### Core decision

Language Elements weaknesses feed Mistake Memory and the Daily Coaching Engine; Stage 10 does not create a parallel grammar-review system.

A recurring grammar/lexical pattern follows the Stage 05 lifecycle:

- same-session fresh retry after repair;
- first delayed transfer normally 1–3 days later;
- retention check around 7 days;
- broader transfer around 21 days;
- later stability/resolution check around 30–60 days or a natural suitable opportunity.

Stage 14 may recalibrate these intervals.

### Preferred review formats

| Weakness type | Compact return format | Broader transfer |
|---|---|---|
| Connector relation | One contextual contrast or micro-cloze | Mixed SB1/SB2 text; later Writing/Speaking verification if useful |
| Connector + word order | Choose relation, then place/select verb form | Fresh connected-text cloze with no scaffold |
| Preposition/case | One short governed-context choice | Different noun/topic and later mixed set |
| Word order | Verb-anchor reorder or targeted gap | Fresh mixed B1 text; productive check when relevant |
| Lexical chunk/collocation | Contextual pair/choice | SB2 bank item in a new text/register |
| Register/functional phrase | Choose phrase for recipient/function | Writing prompt verification where valuable |
| Mixed/uncertain | One clarifying contrast | Broader fresh set only after cause becomes defensible |

### Review guardrails

- Same underlying errors within one 10-gap text are one mistake episode for recurrence when they share a root cause; raw wrong clicks do not inflate recurrence.
- A successful same-session retry means responsive to repair, not “repaired.”
- Review uses fresh contexts and changing nouns/topics, not the original solved sentence.
- A natural occurrence in Reading/Writing/Speaking can satisfy a due check only when it directly tests the relevant capability and condition.
- Productive evidence may strengthen a shared grammar node but does not retroactively turn a Language Elements cloze into productive evidence.
- Do not create a flashcard backlog. The daily coach selects the highest-value due patterns that fit the session.

---

## 4.11 Evidence and scoring contribution

### Objective scoring

Every valid gap has an objective outcome from a reviewed key:

- correct;
- incorrect;
- blank/incomplete;
- invalid/excluded.

Normal practice may show **raw task accuracy** and coaching interpretation. It should not convert a 3-gap P1 micro-cloze into pseudo-official TELC points.

For a current verified P4/mock task, the product may use the official scoring conversion associated with that blueprint. The current model test gives SB1 and SB2 equal 15-point value, 30 points total. **Stage 15 remains authoritative for readiness weighting, score prediction, confidence, and written-pass calculations.**

### Evidence emitted per gap/task

| Evidence group | Required meaning |
|---|---|
| Target | Language Elements section, SB1/SB2 family, target blueprint/version |
| Content | Text/set/gap identity, original/reference status, novelty, quality confidence |
| Context | Topic, register, sentence/text span needed to decide the gap |
| Difficulty | Progression rung and relevant difficulty axes |
| Response | Choice, correctness, blank/incomplete, task accuracy |
| Assistance | Help offered/used and whether answer-bearing |
| Timing | Open/practice/target mode, elapsed pace, interruption/over-target status |
| Skill mapping | Primary grammar/lexical node, optional contributor, mapping confidence |
| Distractor | Chosen distractor type and intended distinction when reviewed |
| Diagnosis | Manifestation, primary cause, optional contributor, confidence/unresolved state |
| Repair | Explanation/contrast/support/model exposure |
| Retry | Freshness/equivalence, conditions, result, same-session transfer |
| Corpus relevance | Target relevance/frequency band and confidence used for priority, not mastery |
| Validity/provenance | Content/evaluator validity, diagnostic/practice/review/mock context, source rights/provenance as needed |

### Attribution rules

1. **Correct SB1 gap:** directly supports the contextual-choice node(s) the item was designed to test. It does not automatically support every grammar concept appearing in the sentence.
2. **Wrong SB1 gap:** lowers a fine node only when the distractors/context isolate the cause; otherwise use broad Language Elements evidence and a clarifier.
3. **Correct SB2 gap:** supports contextual lexical/cohesion selection. It does not automatically prove isolated recall or productive availability.
4. **Assisted result:** remains useful working evidence at the assisted condition; it is weaker for independence/readiness.
5. **Same-item repeat:** low/zero independence contribution depending on exposure; never counts as fresh transfer.
6. **One 10-gap set:** provides multiple objective observations, but breadth/confidence must still consider shared text, session, and repeated-node dependence. Ten gaps in one text are not ten independent occasions.
7. **Cross-modal transfer:** a Language Elements grammar result may influence what Writing/Speaking should test next, not those modalities' mastery before direct evidence.

### Section coverage for later readiness

A Language Elements readiness rollup must preserve:

- SB1 and SB2 coverage separately;
- current B1/target-difficulty coverage;
- assisted versus unassisted evidence;
- untimed/practice-timed versus combined P4/mock evidence;
- concept breadth rather than one memorized grammar family;
- confidence, freshness, and contradiction;
- recurring high-impact bottlenecks;
- target blueprint/version context.

Strong SB1 grammar-choice evidence cannot hide missing SB2 lexical evidence, and vice versa.

### Readiness boundary

Stage 10 deliberately does **not** decide:

- the final Language Elements weight inside written readiness;
- the minimum sample count for “safe” readiness;
- a pass probability;
- the exact written-pass threshold model;
- how a combined Reading + Sprachbausteine pace profile is converted to booking confidence.

Those decisions belong to Stages 15–17. Stage 10 supplies trustworthy, condition-aware evidence so they do not need to invent what a Language Elements attempt means.

---

## 4.12 Representative coaching flows

### Flow A — P0 connector repair

1. **Observe:** short connected text; two connector choices; meaning of one non-tested word previewed.
2. **Attempt:** learner chooses the wrong connector.
3. **Diagnose:** both connectors are known, but the learner chose contrast where the context needs a reason.
4. **Repair:** one-sentence relation contrast; if relevant, show the verb-position consequence.
5. **Retry:** new topic, same cause relation, different answer words.
6. **Remember:** record supported immediate transfer only; schedule a later fresh check if the issue recurs.

### Flow B — P2 preposition/case diagnosis

1. **Observe:** five-gap B1-shaped cloze with on-request hints.
2. **Attempt:** learner chooses the correct preposition family but wrong article form.
3. **Diagnose:** isolate case realization rather than treating the whole preposition as unknown.
4. **Repair:** one governing cue + one contrast.
5. **Retry:** different noun/gender in a fresh context.
6. **Remember:** update contextual case evidence; do not infer productive Writing mastery.

### Flow C — P3 SB2 lexical bank

1. **Observe:** full target-like 10-gap/15-candidate original text; no default language help; target-pace probe.
2. **Attempt:** learner fills the bank.
3. **Diagnose:** deterministic key; one miss is a collocation, another is a broad unresolved lexical/meaning issue.
4. **Repair:** teach the collocation only; use one clarifier for the unresolved item rather than inventing a second weakness.
5. **Retry:** fresh compact bank/context for the collocation.
6. **Remember:** preserve pace, contextual lexical evidence, and any due delayed transfer.

### Flow D — P4 combined written block

1. Run the current verified Reading + SB1 + SB2 structure under the shared 90-minute condition.
2. Do not provide grammar hints, translations, answer explanations, or repair during the measured block.
3. Preserve how the learner allocates time across Reading and Language Elements.
4. Score objective items against reviewed current keys.
5. After the block, diagnose the highest-value Language Elements losses.
6. Repair on separate fresh content; never rewrite the original measured result after coaching.

---

## 4.13 Learner-facing feedback examples

### Correct with assistance

> **Correct with a hint.** You used the rule successfully after the cue. That is useful learning evidence; I’ll check the same pattern later without the hint before calling it independent.

### Connector meaning versus structure

> You chose a connector that expresses a **result**, but this sentence needs the **reason**. The meaning is the first decision; then check what that connector does to the verb position.

### Case versus gender uncertainty

> The article is wrong, but this item alone cannot tell whether the blocker is the case rule or the noun's gender. I saved the result broadly and will separate those with one short fresh contrast.

### SB2 bank distractor

> Your word fits the general topic, but it does not form the normal phrase in this sentence. The correct choice works as a chunk here. I’ll test the chunk in a different context next.

### Correct but slow

> **Accurate, but slower than your current practice target.** The language choice is fine here. The next improvement is making these decisions faster without losing accuracy.

### Immediate repair success

> You solved a **new** item with the same pattern and no hint. The repair worked now. It returns later to check whether it stayed.

### Recurring weakness

> This connector/word-order pattern has now caused misses in more than one fresh session. It is an active weakness, so it will return in short review and later in a mixed B1 text.

---

## 5. Edge Cases / Failure or Uncertainty Handling

| Situation | Stage 10 behavior | What must not happen |
|---|---|---|
| More than one answer is defensible | Invalidate/quarantine the gap; exclude learner impact; replace when feasible | Penalize the learner or pay a premium model to force one answer |
| Grammar cause and vocabulary cause both plausible | Keep broader Language Elements evidence or use one clarifying contrast | Create two fine weaknesses from one ambiguous gap |
| Preposition correct, case form wrong | Diagnose case/form realization | Label the entire preposition unknown |
| Wrong article may be noun-gender knowledge | Test/retain lexical gender uncertainty | Assume case weakness automatically |
| Connector meaning correct but verb position wrong | Separate relation knowledge from syntactic control | Mark the connector itself unknown |
| Correct by elimination in SB2 | Keep positive task evidence; fine lexical confidence may remain limited if relevant | Interrogate every correct answer or claim productive mastery |
| Learner knows rule but is too slow | Preserve language evidence; diagnose pace/execution separately | Reteach the grammar automatically |
| Same pattern fails multiple times in one text | Retain severity/frequency inside the response; one episode for recurrence | Count each gap as an independent weakness episode |
| Same solved text is repeated | Reduce/exclude independence and transfer value | Treat memorization as fresh evidence |
| Learner requests translation/hint | Provide it in ordinary practice when useful; record assisted condition | Shame the learner or pretend the result was unassisted |
| Learner is far below B1 | Reduce one causal axis, use P0/P1 exam-shaped cloze, and keep the target visible | Force repeated full B1 failure or start a generic grammar course |
| P3 full set accurate but SB1 weak in P4 combined block | Diagnose timing/sequence/pressure as well as language | Erase strong untimed capability without comparison |
| Corpus says pattern is frequent but learner is strong | Use occasional maintenance/coverage only | Manufacture a weakness from population frequency |
| Learner repeatedly fails a low-frequency pattern | Raise personal priority if target-relevant | Suppress it solely because corpus frequency is low |
| Corpus sources are duplicated/mirrored | Deduplicate before frequency affects priority | Let one leaked/mock source dominate ranking |
| Corpus confidence is low | Use provisional/supporting priority and broader coverage | Claim “TELC often tests this” without evidence |
| Current blueprint changes | Preserve transferable historical capability; update target relevance/P4 content | Erase all history or keep obsolete content labelled current |
| Exact reference item cannot be reused | Learn from its pattern; serve original reviewed equivalent content | Treat public availability as redistribution permission |
| AI/content service unavailable | Use reviewed cached bank and deterministic feedback | Block objective practice or invent a diagnosis |
| Accessibility support changes interaction/timing | Preserve condition; wait for Stage 25 equivalence rules before strong P4 claim | Treat access support as cheating or generic slowness |

### Ambiguous natural-language grammar

German often permits multiple word orders or lexical choices with different emphasis. A good generated gap must make the intended choice decisively better under the task's meaning and register. If the explanation requires “the test probably wanted this,” the item is not trustworthy enough for learner evidence.

### Too many grammar errors

A mixed set may reveal several weak nodes. Diagnose all supported evidence internally, but the learner-facing repair should normally focus on **one dominant recoverable pattern** and at most one secondary issue. The Daily Coaching Engine can schedule others later. Sprachbausteine must not become a 20-minute post-mortem after every set.

### Grammar that is acceptable at B1 but not ideal

For objective target-format items, the reviewed key determines the intended answer. For broader productive transfer, Stage 12/13's B1 sufficiency rules matter more than native-like perfection. A cloze preference must not cause Bestehen to overcorrect acceptable Writing/Speaking language later.

---

## 6. Relationship to Other Bestehen Stages

### Stage 03 — Initial Diagnostic

The short diagnostic Language Elements cluster remains a provisional routing signal. Stage 10 supplies the full SB1/SB2 task families, node mapping, adaptive cloze behavior, and follow-up evidence needed after diagnosis.

### Stage 04 — Learner Model

Stage 10 writes contextual-selection evidence to grammar/vocabulary nodes while preserving assistance, timing, confidence, freshness, and direct-lane boundaries. Contextual cloze success never becomes spontaneous production automatically.

### Stage 05 — Mistake Memory

Language Elements errors become known weaknesses only through the existing cause-confidence, independent-recurrence, opportunity, repair, and delayed-transfer gates. Stage 10 supplies skill-specific manifestations, clarifiers, and repair formats.

### Stage 06 — Daily Coaching Engine

Corpus frequency, due review, personal recurrence, section coverage, reachability, and exam date compete under the existing session-priority hierarchy. Cheap Language Elements practice must not crowd out missing Writing/Speaking/Listening evidence merely because it is easy to score.

### Stage 07 — Core Learning Loop

Sprachbausteine uses the objective-question loop: deterministic scoring, narrow diagnosis, short repair, fresh equivalent retry, and Remember. Same-session success is responsiveness, not retained repair.

### Stage 08 — A1 → B1 Progression

SB1 and SB2 progress independently across P0–P4. Assistance, text complexity, gap count, distractor closeness, bank size, mixing, and timing are separate axes. One support is restored before globally demoting the task family.

### Stage 09 — Reading Coaching

Reading and Sprachbausteine share the official 90-minute block. Stage 10 preserves that constraint and makes a stronger cross-stage decision: **isolated Language Elements tasks may be target-like and practice-timed, but complete P4 time-allocation realism requires the combined block.**

### Stage 12 — Writing / Stage 13 — Speaking

Language Elements may trigger productive verification of a shared grammar/functional-language node. Direct Writing/Speaking evidence remains required before those modalities change. Productive sufficiency must not be reduced to perfect cloze grammar.

### Stage 14 — Review and Spaced Repetition

Stage 14 integrates connector, preposition/case, word-order, lexical-chunk, and functional-language weaknesses into the full review scheduler. It should preserve contextual review and natural embedding rather than create a separate generic grammar-flashcard product.

### Stage 15 — TELC Readiness

Stage 15 receives SB1/SB2 coverage, target relevance, assistance, timing, freshness, confidence, B1/P4 evidence, task accuracy, and recurring bottlenecks. It owns final weights, pass prediction, and written-component aggregation.

### Stage 16 — Mock Exams

Stage 16 owns the exact combined Reading + Sprachbausteine block experience, full response-sheet behavior, pace strategy, pause rules, and post-mock analysis. It must preserve target-version verification and defer feedback until the measured block ends.

### Stage 21 — Content Strategy

Stage 21 must preserve Stage 10's requirements for natural connected German, one defensible answer, reviewed distractor rationale, node/mapping confidence, fresh-equivalent variants, anti-duplication, source rights, and batch/pre-generated content.

### Stage 22 — Corpus → App Contract

Stage 22 must expose the conceptual Corpus signals listed in Section 4.2, including deduplicated frequency, source breadth/confidence, target/task association, difficulty, grammar/lexical nodes, distractor patterns, topic/register context, rights, and version relevance.

### Stage 25 — Accessibility

Stage 25 decides which interaction/timing accommodations preserve target-condition equivalence. Stage 10 records the condition and avoids overstating comparability in the meantime.

### Stage 26 — Product Analytics

Stage 26 should validate:

- SB1/SB2 accuracy by rung;
- concept-level diagnosis precision;
- false-positive grammar weaknesses;
- support-use reduction;
- repair → fresh-retry transfer;
- delayed retention;
- contextual selection → productive transfer where tested;
- untimed → timed/combined-block degradation;
- Corpus-frequency priority versus actual learner point recovery;
- generated-gap ambiguity/invalidation rate;
- content reuse/near-duplicate effects;
- readiness calibration against mocks and eventual real exam outcomes.

### Cross-stage guardrails

Later stages may tune thresholds, intervals, exact concept bands, and UI copy, but they must preserve:

- grammar/vocabulary taught for exam value and learner need, not chapter completion;
- separate SB1 grammar-choice and SB2 lexical-choice evidence;
- contextual selection distinct from spontaneous production;
- Corpus frequency as a priority prior, never mastery evidence;
- deduplicated/confidence-aware Corpus signals;
- short practical repairs and fresh transfer;
- precise cause only when item design supports it;
- adaptive cloze difficulty by multiple axes;
- no invented official standalone Sprachbausteine time limit;
- combined Reading + Sprachbausteine P4 timing realism;
- deterministic routine scoring and negligible per-attempt AI cost.

---

## 7. Cost Notes

Language Elements should be one of Bestehen's lowest recurring-cost skill experiences.

### Preferred low-cost default

- deterministic scoring from reviewed answer keys;
- reviewed per-gap node, distractor, rationale, and cause metadata;
- template-driven explanations and Remember copy;
- deterministic recurrence, priority, progression, and review-state updates;
- Corpus frequency/relevance precomputed and cached;
- original cloze texts and variants authored or generated **in batches**, reviewed once, then reused;
- fresh-equivalent pools selected from metadata rather than generated live for every retry;
- no runtime premium model for ordinary SB1/SB2 answers or common explanations.

### Where AI can justify cost

AI may materially help offline with:

- drafting natural connected texts at controlled difficulty;
- generating plausible but uniquely wrong distractors;
- constructing SB2 surplus word banks;
- creating fresh equivalents that preserve a node while changing surface context;
- proposing grammar/lexical tags and distractor rationales;
- checking whether multiple answers might be defensible;
- batch-expanding thin high-priority Corpus-derived content families.

A stronger/more expensive model is justified only when cheaper generation plus review produces unacceptable ambiguity, unnatural German, poor distractors, or insufficient coverage in a high-priority family.

### Cheapest fallback

If content generation quality is unreliable, launch with a **smaller manually reviewed original Sprachbausteine bank** and rotate it intelligently. A small trustworthy bank is better than unlimited ambiguous live cloze generation.

If an unusual learner error has no reviewed repair, use a broader safe explanation or schedule a fresh clarifying task. Do not buy a premium classification merely to make the diagnosis look precise.

### Explicit anti-patterns

Do not require:

- one LLM call per cloze answer;
- live generation of every retry;
- runtime AI to restate a deterministic grammar rule;
- premium classification of an ambiguous item that should instead be invalidated;
- repeated generation of content already available in a reviewed equivalent pool;
- an always-on grammar tutor conversation detached from exam-shaped work.

The first product should upgrade spend only when measured content quality/diversity or diagnosis quality is demonstrably blocking transfer or readiness calibration.

---

## 8. Decisions Made

1. Mapped current target Sprachbausteine into **SB1 grammar contextual choice** and **SB2 lexical contextual choice**, with separate evidence and a versioned target blueprint.
2. Preserved the official shared Reading + Sprachbausteine 90-minute block and rejected invented official standalone Sprachbausteine time limits.
3. Defined grammar scope by exam value, learner evidence, prerequisites, transfer, and reachability rather than traditional chapter order.
4. Defined Corpus frequency as a deduplicated, confidence-aware priority prior — never a learner mastery signal.
5. Defined the required Corpus signals and a conservative provisional launch seed until Corpus analytics exist.
6. Defined conjunction/connector coaching through semantic relation, lexical choice, and syntactic consequence, with contrastive repair.
7. Defined preposition/case coaching through functional relation, governed chunk, case realization, and cause separation rather than declension-table-first teaching.
8. Defined word-order coaching through verb anchors, clause type, controlled movement, and later contextual/productive transfer.
9. Defined SB2 vocabulary as lexical/functional choice in context, including collocation, register, cohesion, chunks, and candidate-bank strategy.
10. Defined short exam-driven explanations, 2–6-minute repairs, one primary concept, and fresh equivalent retries.
11. Defined adaptive cloze difficulty across fourteen explicit axes and P0–P4 variants for both SB1 and SB2.
12. Fed recurring grammar/lexical weaknesses into existing Mistake Memory and daily review rather than creating a parallel grammar scheduler.
13. Defined gap/task evidence, attribution, assistance/timing boundaries, section coverage, and the handoff to Stage 15 readiness.
14. Defined ambiguous-item, mixed-cause, timing, sparse-Corpus, blueprint-change, rights, accessibility, and difficulty-wall behavior.
15. Chose deterministic runtime scoring/feedback and reviewed batch content as the low-cost default, with AI mainly for offline content creation/QA.

---

## 9. Open Questions / Deferred Decisions

### Owner questions

**None.** No Stage 10 product decision requires an owner preference to proceed.

### Deferred to later shaping stages

- final adaptive review intervals and competition among all due review types — Stage 14;
- final Language Elements weight in written readiness, evidence minimums, pass probability, and score prediction — Stage 15;
- exact learner-specific Reading + Sprachbausteine time-allocation coaching and full-block mock mechanics — Stage 16, informed by combined-block evidence rather than invented official limits;
- final learner-facing grammar terminology depth and bilingual explanation policy — Stage 18;
- exact screen layout for gap feedback, deep grammar reference, and weakness history — Stage 19;
- cross-skill generated-content QA thresholds and final author/review workflow — Stage 21;
- exact Corpus payload/interface, normalization, and taxonomy/version governance — Stage 22;
- accessibility accommodations that qualify as equivalent target conditions — Stage 25;
- empirical calibration of difficulty, Corpus-priority bands, review effectiveness, item ambiguity thresholds, and timing targets — Stage 26;
- storage schema, algorithms, services, model providers, and generation infrastructure — post-shaping architecture work.

The absence of current Corpus frequency outputs is **not a blocker**. Stage 10 defines an implementable provisional seed and the exact evidence behavior required when the Corpus becomes available. No empirical frequency claim is fabricated in the meantime.

---

## 10. Definition of Done Check

Stage 10 is complete when all of the following are true:

- [x] Map TELC task types.
- [x] Prioritize grammar concepts by exam relevance.
- [x] Define conjunction/connector training.
- [x] Define preposition/case training.
- [x] Define word-order training.
- [x] Define vocabulary-in-context training.
- [x] Keep grammar explanations short and exam-driven.
- [x] Feed recurring grammar weaknesses into daily review.
- [x] Define adaptive cloze difficulty.
- [x] Use Corpus frequency data to influence priority.
- [x] Define evidence and scoring contribution without pre-empting Stage 15 readiness.
- [x] Preserve the Reading + Sprachbausteine shared-time constraint and target-version verification.
- [x] Define low-confidence, ambiguity, insufficient-Corpus, rights, timing, and difficulty-wall behavior.
- [x] Keep routine learner interaction deterministic and financially sustainable.

**Done outcome:** Grammar and vocabulary are taught because they recover likely TELC points, repair demonstrated weaknesses, and unlock target performance — never because the learner reached the next chapter in a generic course.
