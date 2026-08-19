# Bestehen / App — Stage 09: Reading Training

> **Status:** Authoritative Stage 09 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Reading promise:** Train the learner to understand the German that TELC B1 requires **and** to solve each Reading task with the right reading behavior, while progressively removing support until performance is independent and exam-realistic.

## 1. Purpose and Scope

This document defines the complete learner-facing Reading coaching experience for Bestehen / App.

Reading is not treated as a generic collection of texts followed by questions. It is a set of exam-relevant task families that require different combinations of:

- global understanding and text-purpose recognition;
- selective scanning;
- detailed comprehension;
- synonym and paraphrase recognition;
- local and cross-sentence inference;
- restriction, negation, exception, and qualifier handling;
- multi-constraint matching;
- distractor rejection;
- handling unknown vocabulary without abandoning the task;
- time allocation, checking, and moving on.

Stage 09 applies the common product loop — **Observe → Attempt → Diagnose → Repair → Retry → Remember** — to Reading and makes the Stage 08 A1 → B1 progression concrete for TELC B1 Reading.

The product outcome is not merely “the learner got more Reading questions right.” It is that Bestehen can explain **what kind of Reading decision failed, why it failed, how to repair the smallest blocker, whether the repair transferred to fresh content, and how strong that evidence is for eventual TELC readiness**.

This is product shaping rather than implementation architecture. It defines learner behavior, coaching rules, evidence requirements, content policy, and uncertainty handling. It does not choose UI frameworks, storage technology, model providers, or final readiness coefficients.

### In scope

- TELC B1 Reading task patterns used as the launch target;
- lower-difficulty exam-shaped variants from P0 through P4;
- task-to-skill mapping;
- Reading assistance states and evidence consequences;
- vocabulary, synonym/paraphrase, scanning, detailed-reading, and inference training;
- distractor explanations;
- timed and untimed practice;
- Reading-specific diagnosis, repair, retry, and delayed return;
- reference/source material versus original/generated practice;
- exercise flows and feedback examples;
- evidence emitted to the learner model and later readiness model;
- content-quality, uncertainty, and low-cost operating rules.

### Out of scope

- Sprachbausteine task design — Stage 10;
- calibrated TELC scoring/readiness weights — Stage 15;
- full mock sequencing and final mock timing policy — Stage 16;
- final screen information architecture — Stage 19;
- generalized App content-generation QA across every modality — Stage 21;
- final Corpus → App interface and versioning — Stage 22;
- accessibility accommodation policy for target-condition evidence — Stage 25;
- technical content-generation, caching, model, storage, or instrumentation architecture.

---

## 2. Inputs / Existing Decisions

Stage 09 preserves the project overview, identity, and App Stages 01–08:

- Bestehen is a calm, direct, evidence-based **personal German exam coach**.
- TELC B1 is the launch target; the learner may begin around A1.
- German is learned through exam-shaped activity rather than a conventional chapter sequence.
- Readiness is the primary progress concept, with evidence quality and uncertainty kept explicit.
- Reading is a direct-evidence lane; another modality cannot substitute for Reading evidence.
- Mastery, confidence, freshness, assistance dependence, timing, and readiness contribution remain separate.
- The learner model already contains Reading nodes for gist/purpose, scanning, detailed comprehension, synonym/paraphrase recognition, inference, matching, restriction/negation handling, distractor rejection, unknown-word management, and time allocation/checking.
- Mistake Memory requires a defensible cause. One wrong choice does not automatically become a permanent weakness.
- A fine-grained known weakness normally requires independent recurrence rather than repeated clicks inside one repair loop.
- The Daily Coaching Engine chooses the highest-value reachable work and protects due repair, pass-risk evidence gaps, freshness, and section coverage.
- The core loop requires narrow repair and a **fresh equivalent retry**, not repetition of exposed content.
- Stage 07 expects normal repair to take roughly 2–6 minutes and ordinarily remain under eight minutes.
- Stage 08 progression uses **P0 Supported Foundation → P1 Guided A2 → P2 A2/B1 Bridge → P3 Independent B1 Training → P4 Target Conditions**, by task family rather than one global learner level.
- Assistance offered but unused does not weaken evidence. Assistance used before submission stays attached to the attempt.
- Answer-bearing help, direct solution exposure, and same-item repetition cannot masquerade as independent mastery.
- Corpus is the evidence/intelligence source. The learner receives coaching, not a raw Corpus browser.
- Real/reference material defines what is tested. The App should usually practice with original content unless exact reuse is permitted.
- The project begins as a personal project, so deterministic scoring, reviewed reusable content, precomputation, caching, and batch generation are preferred to per-attempt premium AI calls.

No earlier App decision is materially changed by Stage 09.

### 2.1 Target-format verification note

As verified against the official TELC product information on **19 August 2026**, the current general `Zertifikat Deutsch / telc Deutsch B1` written examination still contains **three Reading parts**, and Reading plus Sprachbausteine share a **90-minute** written block.

Bestehen must treat the exact target blueprint as **versioned exam knowledge**, not an eternal constant. Before content is labeled P4/target-condition or a mock is called TELC-realistic, the task structure must be checked against the currently approved target blueprint.

This stage therefore locks the **Reading mechanisms and coaching behavior** while requiring exact item counts, option mechanics, and exam-layout details used for target-condition content to remain verifiable rather than silently hard-coded forever.

---

## 3. Decisions and Rationale

### 3.1 Model Reading as three target task families

**Decision:** The launch Reading experience uses three target task families corresponding to the long-running TELC B1 model:

| Reading family | Target mechanism | Dominant learner problem |
|---|---|---|
| **R1 — Global / heading matching** | Match short texts to a larger bank of headings | Identify the whole text's main point despite lexical overlap and paraphrase |
| **R2 — Detailed comprehension** | Read a longer text and select the best supported answer from alternatives | Find precise evidence, integrate meaning, and reject plausible but unsupported claims |
| **R3 — Selective / situation-to-notice matching** | Match needs/situations to functional notices, offers, or advertisements | Convert a need into constraints, scan efficiently, and reject partial matches |

The current practice blueprint commonly represents these as approximately **5 + 5 + 10 scored decisions**. That is a useful launch-content baseline, but P4/mock content must use the exact currently verified blueprint rather than treating those counts as permanently immutable.

This mapping is intentionally target-specific. Other Reading formats from Goethe, ÖSD, DTZ, educational sources, or Corpus-derived practice may supply useful skill evidence, but they must not silently replace TELC-specific evidence when the product claims target-condition realism.

### 3.2 Preserve the task mechanism at every difficulty

**Decision:** A lower-difficulty Reading task may simplify language, length, candidate count, distractor closeness, number of simultaneous constraints, or time pressure, but it must preserve the target reasoning behavior.

A P0 heading task is still about choosing the best main-point heading. A P0 selective task is still about matching a need to a notice. A simplified task that becomes ordinary vocabulary recall is not a valid lower-difficulty Reading variant.

### 3.3 Train strategy as observable behavior, not generic tips

**Decision:** Reading strategy becomes learner-model evidence only when the behavior can be observed or defensibly inferred from the task interaction and result.

Examples of legitimate strategy evidence include:

- extracting decisive constraints before scanning a notice set;
- identifying the evidence span supporting a detailed answer;
- rejecting a heading because it reflects one detail rather than the main point;
- moving on after a reasonable time instead of over-reading one item;
- noticing a restriction such as `nur`, `nicht`, `außer`, a date range, age condition, or location constraint.

Simply showing the learner a “scanning tip” does not improve scanning mastery.

### 3.4 Separate language failure from solving failure

**Decision:** A wrong answer does not automatically mean weak German comprehension. Reading diagnosis must distinguish at least:

- vocabulary gap;
- synonym/paraphrase failure;
- gist/main-point misunderstanding;
- scanning/target-location failure;
- detailed-comprehension failure;
- restriction/negation/qualifier miss;
- inference failure;
- distractor/partial-match failure;
- instruction/format misunderstanding;
- timing/execution pressure;
- attention slip;
- unresolved/mixed cause.

This matters because the repairs are different. Re-teaching vocabulary to a learner who understood the text but selected a partial-match advertisement wastes time and corrupts Mistake Memory.

### 3.5 Use deterministic evaluation by default

**Decision:** Standard Reading answers are objective and should normally be scored from a reviewed answer key without a runtime AI call.

AI may be useful during **content creation, ambiguity review, distractor generation, paraphrase annotation, or difficult offline QA**, but it is not required to decide whether a reviewed multiple-choice/matching response is correct.

If an item is ambiguous, the product should invalidate or quarantine the item rather than pay for a premium model to “decide” the learner's answer after the fact.

### 3.6 Timing is a separate capability dimension

**Decision:** Slow-but-accurate Reading is not the same weakness as inaccurate Reading. Untimed capability, practice-timed capability, and target-condition execution remain distinct evidence.

The product progressively introduces pace while preserving the learner's underlying comprehension signal. A learner who understands a passage accurately but needs too long receives pacing/strategy coaching, not an automatic language downgrade.

### 3.7 Generated/original practice is the default learner content

**Decision:** Real/reference exams define the target mechanism, difficulty, topics, distractor patterns, and language characteristics. Everyday learner practice should primarily use **original, reviewed content** generated or authored from those patterns unless the exact reference item has reuse rights that permit learner display.

Public accessibility alone is never treated as permission to redistribute exact source text.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Reading task model

### R1 — Global understanding / heading matching

The learner must select the heading that best captures the **whole text**, not the heading that merely shares a word with one sentence.

Primary skills:

- gist and main-point extraction;
- text purpose/function;
- synonym and paraphrase recognition;
- semantic discrimination among related headings;
- distractor rejection;
- unknown-word tolerance;
- efficient time allocation.

Common failure patterns:

- chooses a heading with an exact keyword but wrong main idea;
- focuses on one interesting detail rather than the whole text;
- misses a paraphrased heading because wording differs;
- over-reads every sentence before making a gist decision;
- confuses broad topic with specific communicative point.

### R2 — Detailed comprehension

The learner must connect the question to defensible evidence in the text and distinguish the correct claim from plausible alternatives.

Primary skills:

- locating the relevant segment;
- detailed comprehension;
- local and cross-sentence integration;
- reference tracking;
- cause/result, contrast, condition, and sequence interpretation;
- negation/restriction/qualifier handling;
- paraphrase recognition;
- limited text-supported inference;
- distractor rejection.

Common failure patterns:

- selects something true in the passage that does not answer the question;
- overlooks one qualifier or exception;
- chooses a plausible real-world answer unsupported by the text;
- finds the correct paragraph but misreads the relationship inside it;
- treats a partial truth as the full answer;
- reads the entire passage repeatedly instead of returning to the decisive segment.

### R3 — Selective reading / situation-to-notice matching

The learner must convert each stated need into one or more **must-have constraints**, scan a large candidate set, and verify the candidate rather than stopping at topic overlap.

Primary skills:

- need/constraint extraction;
- selective scanning;
- functional vocabulary and abbreviations;
- date, time, price, place, age, audience, service, and restriction handling;
- multi-constraint satisfaction;
- synonym/paraphrase recognition;
- partial-match rejection;
- no-match recognition when the verified target format uses it;
- pace and move-on behavior.

Common failure patterns:

- selects the first notice with the right topic;
- checks one requirement but misses another;
- misses a restriction in small functional text;
- reads every notice in full instead of scanning for decisive cues;
- refuses “no suitable match” because one option seems close enough.

---

## 4.2 Lower-difficulty variants by progression rung

### R1 progression

| Rung | Training variant | Main simplification | Evidence claim |
|---|---|---|---|
| **P0 Supported Foundation** | 2–3 very short texts with 3–5 clearly separated headings | Concrete A1/early-A2 language, one clear main idea, targeted preview | Main-point matching with substantial support |
| **P1 Guided A2** | 3–4 short texts with extra headings | Genuine A2 language, some topic-overlap distractors | Functional gist with selective/on-request help |
| **P2 A2/B1 Bridge** | 4–5 texts with controlled B1-like paraphrase | Longer text, closer headings, fewer lexical matches | B1-shaped global reading with limited support |
| **P3 Independent B1** | Full or near-full original B1-equivalent set | Authentic density/distractors; no default help | Independent B1 task-family evidence |
| **P4 Target Conditions** | Current verified target-form set | No simplification | Strong target-condition evidence |

### R2 progression

| Rung | Training variant | Main simplification | Evidence claim |
|---|---|---|---|
| **P0** | Short text, 2 questions, evidence usually in one explicit sentence | Concrete language, clearly distinguishable options | Supported detailed comprehension |
| **P1** | Short-medium text, 2–3 questions | A2 language, mild paraphrase/contrast | Functional evidence-based Reading |
| **P2** | Medium text, 3–5 questions | Controlled cross-sentence links and closer distractors | B1-shaped detailed comprehension |
| **P3** | Full-length/equivalent original B1 passage | Authentic B1 language and distractor quality | Independent B1 evidence |
| **P4** | Current verified target-form task | Exact target constraints | Readiness-grade target evidence |

### R3 progression

| Rung | Training variant | Main simplification | Evidence claim |
|---|---|---|---|
| **P0** | 2–3 situations, 3–5 short notices | One decisive condition; high-frequency functional vocabulary | Supported need-to-notice matching |
| **P1** | 3–5 situations, 5–7 notices | Two conditions begin to matter; one partial-match distractor | Functional selective Reading |
| **P2** | 5–8 situations, larger candidate set | Multi-constraint needs, more paraphrase, closer partial matches | B1-shaped scanning/verification |
| **P3** | Full or near-full original B1-equivalent set | Authentic density, abbreviations, restrictions, distractors | Independent B1 evidence |
| **P4** | Current verified target-form task | Exact target constraints | Readiness-grade target evidence |

### Shared difficulty axes

Reading difficulty is adjusted along explicit axes:

1. vocabulary frequency and domain familiarity;
2. sentence length and grammar density;
3. explicit wording versus paraphrase;
4. text length per scored decision;
5. number of candidate answers/texts;
6. distractor semantic closeness;
7. number of simultaneous constraints;
8. explicit detail versus cross-sentence/inference demand;
9. frequency of negation, exception, restriction, contrast, or correction cues;
10. functional compression such as abbreviations, prices, schedules, and conditions;
11. assistance availability;
12. time pressure and task sequencing.

When the learner hits a wall, the coach should normally adjust **one causal axis** rather than collapse every dimension at once.

---

## 4.3 Task-to-skill map

| Reading capability | R1 Global | R2 Detail | R3 Selective | Coaching interpretation |
|---|:---:|:---:|:---:|---|
| Gist/main point | **Primary** | Supporting | Supporting | What is this text mainly saying or doing? |
| Text purpose/function | **Primary** | Supporting | Supporting | Inform, offer, explain, report, advise, invite, restrict, etc. |
| Scanning for target detail | Supporting | **Primary** | **Primary** | Locate only information relevant to the current decision |
| Detailed comprehension | Supporting | **Primary** | Important | Interpret the decisive segment correctly |
| Synonym/paraphrase recognition | **Primary** | **Primary** | **Primary** | Recognize the same meaning with different wording |
| Local/cross-sentence inference | Occasional | **Important** | Occasional | Derive only what the text supports |
| Restriction/negation/exception | Important | **Primary when present** | **Primary** | Detect conditions, exclusions, and limiting words |
| Matching/constraint satisfaction | **Primary** | Low | **Primary** | Compare target meaning/need to candidates |
| Distractor rejection | **Primary** | **Primary** | **Primary** | Identify the decisive reason a tempting option fails |
| Unknown-word management | Important | Important | **Primary** | Continue without resolving non-decisive vocabulary |
| Time allocation/moving on | Important | Important | Important | Protect the shared written-block time budget |
| Evidence checking | Important | **Primary** | **Primary** | Verify a choice against decisive text evidence |

A correct answer does **not** automatically raise every skill tagged to the item. Fine-grained evidence is applied only where task metadata and/or diagnosis supports attribution.

Where fine attribution matters, reviewed item metadata should conceptually include:

- primary intended Reading skill;
- optional secondary skills;
- decisive evidence span/cue;
- paraphrase relationship where relevant;
- distractor rationale/type;
- restriction/constraint pattern;
- linguistic difficulty;
- reasoning difficulty;
- task-family relevance;
- mapping confidence.

If mapping confidence is low, retain broader task-family evidence rather than inventing skill precision.

---

## 4.4 Vocabulary assistance

### Assistance goal

Vocabulary help keeps an exam-shaped task reachable **without removing the Reading behavior being measured**. Full translation is not the default response to difficult text.

### Assistance states

| Support | P0 | P1 | P2 | P3 ordinary practice | P4/target probe |
|---|---|---|---|---|---|
| Small vocabulary preview | Default when needed | Default only for a new/high-load domain, otherwise request | Rare default/request | Request makes affected evidence assisted | Unavailable during measured attempt |
| Selected word/short-phrase translation | Visible/request | Request | Request | Request makes affected evidence assisted | Post-attempt only |
| Sentence explanation | Default/request only if task otherwise inaccessible | Request | Request | Post by default; request makes evidence assisted | Post-attempt only |
| Strategy cue | Default for new behavior | Default/request | Request | Request in ordinary practice; post in target probe | Post-attempt only |
| Evidence-location / answer-narrowing hint | After meaningful attempt or clear wall | Request after attempt | Request after attempt | Repair only by default | Post-attempt only |
| Full translation/model solution | Repair exposure only | Repair only | Repair only | Repair only | After measured block only |

### Vocabulary-preview rules

- Preview only words/phrases whose absence would otherwise make a meaningful attempt unlikely.
- Do not preview the exact synonym/paraphrase relation the item is designed to test.
- Do not translate every unknown word.
- A previewed word does not prove independent vocabulary recognition in that attempt.
- If a preview reveals the decisive answer, the affected answer is weak assisted evidence rather than clean comprehension evidence.
- Initial operating guardrail: a **small handful** of preview items per lower-rung task, typically around 3–6 when needed, decreasing as independence grows. This is tunable rather than a scientific cutoff.

### On-demand word help

Selecting a word can show:

1. concise context-relevant meaning;
2. base form where useful;
3. at most one brief disambiguating example.

A word lookup does not automatically become a known weakness. It becomes a repair/review candidate only when evidence shows that it materially blocked exam-relevant performance or recurs.

### Unknown-word strategy

Bestehen trains three decisions:

- **Decisive:** the answer depends on this word/phrase.
- **Useful but inferable:** context or paraphrase may be sufficient.
- **Incidental:** keep reading.

At P2/P3 the learner should sometimes be encouraged to continue past a non-decisive unknown word, with feedback confirming that the answer remained obtainable. The goal is target-condition resilience, not translation dependence.

---

## 4.5 Synonym and paraphrase training

### Product decision

Synonym/paraphrase recognition is a first-class Reading capability. Training includes more than dictionary-style synonym pairs:

- word-level synonymy;
- phrase equivalence;
- grammatical reformulation;
- more general/specific expressions;
- cause/result or condition rewording;
- functional equivalents;
- sentence-level paraphrase.

### Progression

| Step | Exercise | Purpose |
|---|---|---|
| 1. Simple equivalence | Which phrase means the same thing? | Establish semantic equivalence |
| 2. Contextual equivalence | Which phrase in the text supports this differently worded heading/question? | Bind meaning to context |
| 3. Contrastive paraphrase | Pick the true equivalent among a near synonym and a misleading topic-related phrase | Reject lexical-overlap traps |
| 4. Transformation | Rephrase a short cue in another B1-suitable way | Deepen flexible representation |
| 5. Exam transfer | Solve a fresh R1/R2/R3 item with intentionally low lexical overlap | Test independent Reading transfer |

A productive rephrase can support learning, but it does not replace direct Reading evidence.

### “Same idea, different words” micro-repair

When a miss is confidently diagnosed as paraphrase failure:

1. show the target wording and decisive source wording side by side;
2. explain the semantic connection in one sentence;
3. ask one or two new equivalence judgments;
4. serve a fresh Reading item requiring the same paraphrase capability.

Normal duration: **2–5 minutes**, inside the Stage 07 repair boundary.

Do not teach context-dependent paraphrases as universal one-to-one synonyms.

---

## 4.6 Scanning versus detailed-comprehension practice

### Core decision

**Bestehen explicitly teaches the learner to choose the cheapest reading behavior that can answer the task correctly.**

The learner should not read every text in the same way. Reading strategy is task-dependent:

| Task need | Default behavior | When to switch |
|---|---|---|
| R1 main point | Quick whole-text gist pass | Close-read only when two headings remain genuinely plausible |
| R2 exact answer | Locate relevant question evidence, then read the decisive local context carefully | Broaden to nearby sentences when relation/reference/inference requires it |
| R3 functional match | Extract the situation's must-have constraints, scan notices for candidate cues | Close-read only candidate notices that satisfy the first decisive conditions |

### Scanning training

Scanning exercises train the learner to search for **criteria**, not merely identical words.

Examples:

- “Find the notice that is available on Sunday and accepts children.”
- “Find where the author states a reason, not merely where the topic is mentioned.”
- “Which two candidate notices survive the first constraint?”

Early practice may visually separate texts or let the learner mark constraints before scanning. At higher rungs the support disappears.

### Detailed-reading training

Detailed practice teaches a consistent evidence sequence:

1. understand the question/claim;
2. identify the likely text region;
3. read the decisive sentence plus enough local context;
4. check modifiers, negation, reference, condition, and contrast;
5. compare the exact claim against the options;
6. answer from the text rather than from general plausibility.

### Mixed strategy-selection drills

Some sessions deliberately mix microtasks and ask the learner to choose **scan**, **gist**, or **read closely** before answering. This is useful when the learner's problem is not comprehension itself but inefficient strategy selection.

The learner is not penalized for using a different reading route if the task is completed accurately and efficiently. The coach teaches effective behavior, not one rigid ritual.

### Diagnosis boundaries

- Accurate but consistently too slow → primarily timing/strategy evidence.
- Fast but misses qualifiers → restriction/checking or attention/strategy evidence.
- Finds the correct paragraph but misinterprets it → detailed-comprehension evidence.
- Cannot locate the relevant segment despite knowing the vocabulary → scanning evidence.
- Needs a translation to understand the decisive word → vocabulary evidence.

When cause is uncertain, keep the mistake broad or use one small clarifying probe.

---

## 4.7 Distractor explanations

### Product decision

A useful Reading explanation does not merely state the correct answer. It explains **why the learner's chosen option was tempting and the decisive reason it fails**.

Default feedback order:

1. **Your choice**;
2. **decisive source evidence**;
3. **why your choice looked plausible**;
4. **the exact mismatch**;
5. **the solving behavior to use next time**;
6. fresh retry when repair is needed.

The learner normally sees a deep explanation for the chosen distractor and the correct answer—not a lecture on every unused option.

### Initial distractor taxonomy

| Distractor type | Why it is tempting | Decisive failure | Typical repair |
|---|---|---|---|
| **Keyword overlap** | Same word/topic appears in text and option | Relationship/main point differs | Gist/paraphrase contrast |
| **Partial match** | One requirement is satisfied | Another required condition fails | Constraint checklist |
| **Opposite / negation** | Vocabulary looks familiar | `nicht`, `kein`, `nur`, contrast, or reversal changes meaning | Restriction/negation repair |
| **True but irrelevant** | Statement is genuinely in the text | It does not answer this question | Question-to-evidence mapping |
| **Too broad** | Fits general topic | Claims more than the text supports | Evidence-bound inference |
| **Too narrow / detail trap** | Reflects one sentence/detail | Misses the whole text's main point | Global-reading repair |
| **Wrong person/time/place/number** | Nearby fact is similar | Attribute belongs to another entity/condition | Detail tracking |
| **Plausible outside knowledge** | Sounds reasonable in real life | Passage does not support it | “Answer from the text” repair |
| **Near paraphrase** | Most words seem equivalent | One semantic element changes the claim | Contrastive paraphrase training |
| **No-match avoidance** | One notice is almost suitable | Mandatory condition still fails | Multi-constraint verification |

Corpus may later refine frequency and provider relevance of these patterns. The App needs the taxonomy now so it can diagnose and explain them consistently.

### Feedback examples

**R1 — keyword trap**

> You picked the heading because both mention **Reisen**. The text is mainly about a **discount for families**, not travel in general. The correct heading expresses the whole point, even though it uses different words.

**R2 — missed restriction**

> You found the right sentence, but missed **nur werktags**. Your answer would be true every day; the text limits it to Monday–Friday. This is a restriction-checking error, not a general vocabulary gap.

**R3 — partial match**

> This course matches the topic and price, but it starts in October. The situation requires a course **before September**. One missing condition makes the whole match wrong.

**True-but-irrelevant distractor**

> That statement appears in the article, but the question asks **why** the change happened. The sentence you chose describes what happened afterward.

---

## 4.8 Timed and untimed modes

### Timing ladder

| Mode | Typical rung | Learner experience | Evidence meaning |
|---|---|---|---|
| **Open training** | P0–P1 | No countdown pressure; learner can focus on task mechanism | Comprehension/strategy learning evidence, not target pace |
| **Pace awareness** | P1–P2 | Soft expected range or post-task pace feedback; no forced stop | Early timing evidence without sacrificing learning |
| **Practice timed** | P2–P3 | Visible timer with a realistic but initially generous target; learner may finish after time | Timed practice evidence; over-target completion remains valid but marked slow |
| **Target-time probe** | P3 | No learning help; task-family timer derived from verified exam block strategy | Stronger task-family timing evidence |
| **P4 target conditions** | P4 | Reading operates inside the verified current written-block constraints with feedback deferred | Highest Reading readiness contribution |

### Shared 90-minute block rule

The official target gives **Reading + Sprachbausteine a shared 90-minute block**, so Bestehen must not present an internal per-part minute allocation as an official TELC rule.

The coach may teach a **recommended working budget** for R1/R2/R3 and Sprachbausteine, but that budget is strategy, not scoring law. It should evolve from:

- the currently verified blueprint;
- learner pace evidence;
- task-family accuracy under pressure;
- later mock performance;
- Stage 10 Sprachbausteine demands;
- Stage 16 full-block rehearsal.

Stage 09 therefore owns Reading pace evidence and task-family timing behavior; Stage 10/16 own final combined-block strategy and full simulation.

### Timing diagnosis rules

- Correct and comfortably within target → positive timing evidence.
- Correct but over target → comprehension remains positive; timing/strategy is weaker.
- Incorrect only under time pressure after reliable untimed success → test timing/execution before lowering language mastery.
- Incorrect both timed and untimed → language/comprehension cause remains likely.
- Timeout/incomplete because of app interruption or technical failure → invalid, not learner weakness.
- One slow task does not create a persistent timing weakness.

### Timer behavior

In normal practice, crossing a timer does not forcibly erase or terminate the response. The learner may finish, and the evidence is recorded as **over target**. Hard stopping belongs only where the verified exam simulation itself requires it.

---

## 4.9 Diagnosis and repair after Reading mistakes

### Reading diagnosis sequence

After a wrong or partial Reading decision:

1. **Validate the item** — answer key, content, layout, and task must be unambiguous.
2. **State the outcome** — correct, incorrect, incomplete, skipped, invalid.
3. **Identify decisive evidence** — the sentence, relation, constraint, or whole-text gist that determines the answer.
4. **Compare the learner's choice** — identify the first material mismatch.
5. **Assign the narrowest defensible cause**, or leave it unresolved.
6. **Choose the smallest useful repair**.
7. **Retry on fresh equivalent content**.
8. **Remember** support, timing, transfer, and any due delayed check.

### Reading cause taxonomy

| Cause | Diagnostic clue | Repair |
|---|---|---|
| Vocabulary gap | Meaning remains unknown when decisive word/phrase is isolated | Brief context meaning + contrast + fresh item |
| Paraphrase/synonym failure | Learner understands both expressions independently but misses equivalence | Side-by-side equivalence + contrast + fresh transfer |
| Gist/main-point failure | Learner focuses on one detail rather than whole text | “What is the whole text doing?” compression exercise |
| Scanning failure | Learner understands evidence once location is shown | Constraint/cue extraction + locate in fresh short text |
| Detailed-comprehension failure | Learner finds the region but misreads relation/meaning | Reconstruct decisive sentence/context + new item |
| Restriction/negation miss | Correct region found; limiting cue overlooked/misinterpreted | Contrast two claims differing only by condition/negation |
| Inference failure | Literal facts understood but conclusion exceeds/misses text evidence | Evidence-bound inference comparison |
| Distractor/partial-match failure | Chosen option matches some but not all evidence | Chosen-vs-correct contrast with decisive disqualifier |
| Instruction/format | Learner solved a different task than asked | One format clarification/example, then fresh item |
| Timing/strategy | Untimed ability stronger; paced execution degrades | Pacing/move-on strategy + fresh timed attempt |
| Attention slip | Strong contrary evidence and quick self-correction; isolated event | Short checking cue; monitor rather than over-teach |
| Unresolved/mixed | Multiple causes remain plausible | One small clarifying probe or broad task evidence only |

### Clarifying probes

When the distinction changes the repair materially, Bestehen may use one brief diagnostic contrast.

Examples:

- show the decisive word meaning, then ask the same semantic question: success raises vocabulary-gap likelihood;
- highlight the relevant sentence **without explaining it**: success raises scanning-failure likelihood but remains assisted evidence;
- ask which phrase supports the chosen answer: useful for separating unsupported distractor selection from comprehension failure;
- remove time pressure on a fresh comparable item: useful for timing versus comprehension.

Do not force a probe after every mistake. Use it when the cause is high-impact and genuinely uncertain.

### Repair limits

- Normal Reading repair: **1–6 minutes**, usually inside Stage 07's 2–6 minute range.
- One primary cause and at most one material contributor by default.
- Do not teach every unknown word in the passage.
- Do not reuse the original item as proof of repair after exposing its solution.
- If the learner still fails the fresh retry, allow one useful re-diagnosis; then stop the loop, save the evidence, and schedule a better future intervention instead of drilling indefinitely.

### Repair is not resolution

A successful same-session retry means **the repair transferred immediately**. It does not resolve a known weakness.

Delayed fresh checks return through Mistake Memory / Stage 14 review. Repeated independent success under progressively realistic conditions is what can move the capability toward reliable/target-evidenced.

---

## 4.10 Canonical Reading exercise flows

### Flow A — Supported Reading learning, P0/P1

1. **Observe:** task goal, format demonstration if new, small targeted vocabulary preview.
2. **Attempt:** learner answers with permitted on-request word help.
3. **Diagnose:** deterministic answer check plus one likely cause if supported.
4. **Repair:** short explanation/contrast.
5. **Retry:** simpler or equivalent fresh item with less answer-bearing help where feasible.
6. **Remember:** “You solved a new task after support; this is learning evidence, not yet independent B1 evidence.”

### Flow B — Guided/independent coaching, P2/P3

1. **Observe:** task-family goal and current pace condition.
2. **Attempt:** no default answer-bearing help.
3. **Diagnose:** show decisive evidence and chosen-distractor rationale after submission.
4. **Repair:** only if a coachable blocker exists.
5. **Retry:** fresh equivalent item, same lane, same underlying capability.
6. **Remember:** update task-family capability, assistance dependence, timing, and Mistake Memory.

### Flow C — Target-time probe, P3

1. **Observe:** explain timer and no-help measurement condition.
2. **Attempt:** B1-equivalent original task under target-like pace.
3. **No coaching during attempt.**
4. **Diagnose after task block:** accuracy + pace + cause analysis.
5. **Repair later** for the highest-value misses.
6. **Remember:** stronger readiness evidence than ordinary untimed practice, but still distinguish it from a full P4/mock context.

### Flow D — P4 / mock Reading block

1. Run the verified target Reading structure inside the current exam-realistic written conditions.
2. Defer all feedback, translations, explanations, hints, and repair until the measured block ends.
3. Preserve task-family accuracy, timing, skipped items, and any technical invalidation.
4. Post-block diagnosis selects only the highest-value misses for repair.
5. Same-session repair and fresh retries become learning evidence; they do not alter the original mock result.

### Flow E — Post-mock Reading recovery

1. Group errors by supported cause, not by item count alone.
2. Separate isolated misses from recurring/known weaknesses.
3. Prioritize high-impact recurring patterns and timing bottlenecks.
4. Run one or two narrow repairs rather than replaying the whole mock.
5. Schedule fresh transfer checks.
6. Later re-test the relevant task family under realistic conditions.

---

## 4.11 Evidence emitted to the learner/readiness model

Every valid Reading attempt must be capable of emitting the following conceptual evidence.

### Attempt evidence

| Evidence group | Required meaning |
|---|---|
| Target | Reading section, task family R1/R2/R3, target exam/version context |
| Content | Item/set identity, source/original status, freshness/novelty, content-quality confidence |
| Difficulty | Linguistic load, reasoning load, task scale, progression rung |
| Response | Choice/match/skip/incomplete, correctness, item/set score |
| Assistance | Which support was offered, which was used, whether it was answer-bearing |
| Timing | Open/practice/target mode, elapsed time, within/over target, interruption flags |
| Skills | Primary/secondary Reading skills and mapping confidence |
| Decisive evidence | Reviewed source span/cue/constraint where available |
| Distractor | Chosen distractor type/rationale where relevant |
| Diagnosis | Manifestation, primary cause, optional contributor, diagnosis confidence |
| Repair | Repair type/exposure, model/solution exposure, controlled practice completion |
| Retry | Freshness/equivalence, conditions, result, same-session transfer outcome |
| Validity | Technical/content/evaluator validity and exclusion reason when invalid |
| Provenance | Diagnostic/daily/review/target-probe/mock context and target blueprint version |

### Evidence-strength ordering for Reading

The following order guides later readiness weighting without locking Stage 15's formula:

1. **Invalid/excluded** — ambiguous item, technical failure, broken task: zero learner impact.
2. **Supported working evidence** — P0/P1 or answer-bearing assistance: useful for routing/learning, weak for readiness.
3. **Unassisted untimed evidence** — stronger capability evidence, still incomplete for exam execution.
4. **Unassisted B1 practice-timed evidence** — strong task-family evidence.
5. **Verified P4/mock target-condition evidence** — strongest Reading readiness anchor.

Same-item repetition and performance after direct answer exposure do not move up this ladder merely because accuracy improved.

### Coverage rules

A Reading readiness rollup later must know whether evidence exists across **all target task families**. Strong R1 performance cannot hide missing R2 or R3 evidence.

It must also preserve meaningful subskill bottlenecks. A high average must not hide a recurring restriction/negation weakness if that pattern repeatedly loses target-condition points.

### Readiness boundary

Stage 09 does **not** decide:

- the final Reading weight within written readiness;
- the minimum sample count for a strong readiness claim;
- official score prediction or pass probability;
- written/oral pass thresholds.

Those belong to Stage 15. Stage 09 supplies the evidence quality and coverage needed so Stage 15 can make those decisions defensibly.

---

## 4.12 Learner-facing feedback examples

### Correct but slow

> **Correct — but over target pace.** You found the right evidence without help. Comprehension is fine here; the next improvement is finding the decisive sentence faster.

### Vocabulary assistance used

> You solved the item after checking **vereinbaren**. That is useful learning evidence, but it does not yet prove you recognize the word independently. It will return later without the translation.

### Scanning failure

> You understood the sentence once it was highlighted. The blocker was finding the right place in the text, not understanding the German. We’ll do one short scanning check before the retry.

### Detailed-comprehension failure

> You found the correct paragraph, but read **obwohl** as if the second point supported the first. The text is contrasting them. We’ll repair that relation, then test it in a new passage.

### Distractor failure

> Your choice matches **two** conditions, but fails the required date. This is a partial-match trap. For the retry, check every must-have condition before choosing.

### Immediate repair success

> You solved a **new** restriction item without a hint. The repair helped. I’ll check the same skill again later before calling it reliable.

### Uncertain diagnosis

> The answer was wrong, but I can’t tell yet whether the problem was the word **Gebühr** or the price condition. I saved the result without labeling a weakness. One short comparison later will separate them.

---

## 5. Edge Cases / Failure or Uncertainty Handling

### 5.1 Correct by guessing or keyword matching

A correct answer remains positive task evidence, but the App should not routinely force an explanation after every correct choice.

When a high-value claim appears fragile—e.g. repeated very-fast keyword matches or a target-condition task near a readiness decision—the coach may occasionally ask for the decisive evidence/cue. If the learner cannot identify it, confidence in the fine-grained skill remains limited. Do not turn this into constant interrogation.

### 5.2 Unknown word that is not decisive

Do not create a vocabulary repair merely because the learner tapped an unknown word. If the task is solved independently despite that word, reinforce the useful exam behavior: not every word needs to be understood.

### 5.3 Learner overuses translation

Translation use is not punished. It becomes **assistance-dependence evidence** when comparable tasks repeatedly require it.

The coach should fade help gradually:

1. translation visible/requestable;
2. request only;
3. suggest trying context first;
4. remove during clean target probes;
5. restore one support if the task becomes unreachable.

### 5.4 Very slow but accurate

Keep comprehension positive. Diagnose pacing only after comparable evidence shows a pattern. Repair time allocation, scanning, or move-on behavior rather than reteaching language by default.

### 5.5 Very fast with careless misses

One fast error is not enough to label the learner careless. Repeated missed qualifiers/conditions with otherwise strong comprehension may become a checking/strategy pattern.

### 5.6 Ambiguous generated item

If two answers are defensible or the rationale depends on an unreasonable interpretation:

- invalidate the item;
- create no learner mistake event;
- remove its mastery/readiness impact;
- replace with a reviewed task when possible;
- quarantine it for content QA.

The learner-facing message should be neutral: **“This item was unclear, so it won’t affect your progress.”**

### 5.7 Reference source changes or disappears

Derived task intelligence may remain useful subject to Corpus rights/removal policy, but direct learner display must follow the current rights classification. If the source is no longer permitted for surfacing, switch practice to original content without losing the learner's unrelated historical performance evidence.

### 5.8 Current TELC blueprint changes

If target-format verification detects a material change:

- old practice remains historical Reading evidence where the skill is still relevant;
- it loses or reduces **target-format** relevance as appropriate;
- P4/mock templates must update before being labeled current TELC-realistic;
- the App should not retroactively erase demonstrated general Reading capability;
- later readiness interpretation must use the target-version context.

### 5.9 Corpus lacks enough evidence for a fine-grained pattern

Use a broader reviewed task pattern or manually authored baseline rather than fabricate a high-confidence Corpus conclusion. Low-confidence Corpus metadata cannot create a precise learner weakness.

### 5.10 Accessibility affects timing or interaction

Accessibility support that does not change the Reading capability being tested should not be treated as cheating or assistance dependence. Stage 25 owns the final target-condition accommodation contract. Until then, preserve the condition and avoid overclaiming comparability.

### 5.11 Learner hits a B1 difficulty wall

Do not repeat full B1 failures. Reduce one relevant axis:

- language complexity;
- text length;
- distractor closeness;
- number of constraints;
- support availability;
- timing.

Then return to the same target reasoning mechanism and later re-probe the harder condition.

### 5.12 Fresh retry content unavailable

Do not reuse the exposed answer just to complete the loop. Mark fresh transfer as pending and let the Daily Coaching Engine return when a valid equivalent item exists.

---

## 6. Relationship to Other Bestehen Stages

### Stage 04 — Learner Model

Stage 09 refines the already-defined Reading skill family into target task patterns and concrete evidence. Stage 04's separation of mastery, confidence, freshness, assistance, timing, and readiness contribution remains authoritative.

### Stage 05 — Mistake Memory

Reading diagnosis feeds mistake episodes and known weaknesses only when cause confidence and independent recurrence rules are satisfied. A wrong answer by itself does not create “weak synonym recognition” or “weak scanning.”

### Stage 06 — Daily Coaching Engine

Reading work competes with other pass-critical needs using the existing priority hierarchy. Cheap objective Reading must never crowd out missing oral or Writing evidence merely because it is easier to serve and score.

### Stage 07 — Core Learning Loop

Reading uses the same Observe → Attempt → Diagnose → Repair → Retry → Remember semantics. Objective scoring is deterministic; repair stays narrow; retries are fresh.

### Stage 08 — A1 → B1 Progression

R1/R2/R3 each maintain task-family progression profiles. A learner can be P4 in R1 while still P2 in R3. Assistance and timing fade independently.

### Stage 10 — Sprachbausteine

Reading and Sprachbausteine share the target written 90-minute block. Stage 10 must preserve this shared-budget constraint. Neither stage should pretend its internal pace recommendation is an official standalone time allocation.

### Stage 14 — Review and Spaced Repetition

Reading-derived review candidates include:

- exam-relevant vocabulary gaps;
- paraphrase relations;
- restriction/negation patterns;
- distractor patterns;
- scanning/checking strategies.

Stage 14 owns scheduling calibration and quick-review formats. Reading review should remain embedded in coaching rather than become a separate flashcard product.

### Stage 15 — TELC Readiness

Stage 15 receives:

- R1/R2/R3 coverage;
- difficulty and target relevance;
- assisted versus unassisted split;
- timed versus untimed split;
- evidence freshness/confidence;
- mock/P4 anchors;
- repeated bottlenecks;
- source/original content context.

Stage 15 decides weights, thresholds, evidence minimums, and pass-probability/readiness representation.

### Stage 16 — Mock Exams

Mocks must use a currently verified TELC Reading blueprint and defer feedback until the measured block ends. Post-mock repair creates new learning evidence without rewriting the original mock result.

### Stage 21 — Content Strategy

Stage 21 generalizes the original/generated/reference policy across every modality and locks final QA requirements. It must preserve Stage 09's Reading-specific requirements for natural German, answer unambiguity, distractor rationale, paraphrase quality, and target-pattern grounding.

### Stage 22 — Corpus → App Contract

Reading requires Corpus to be able to provide or support conceptually:

- target/provider/task-pattern classification;
- target blueprint version;
- topic/domain;
- vocabulary/grammar signals;
- linguistic and reasoning difficulty;
- TELC relevance;
- Reading skill mapping;
- paraphrase/synonym relationships;
- distractor patterns;
- source confidence;
- rights/usage status;
- provenance and source-version context.

Corpus owns source intelligence; App owns learner evidence and coaching.

### Stage 25 — Accessibility

Stage 25 must define which accommodations preserve target-condition evidence, particularly timer behavior, text presentation, navigation, and screen-reader interaction.

### Stage 26 — Product Analytics

Reading analytics should later validate:

- task-family accuracy by rung;
- support-use reduction;
- repair → fresh-retry transfer;
- delayed retention;
- untimed → timed performance gap;
- distractor patterns causing losses;
- generated-item invalidation/ambiguity rate;
- readiness calibration against mocks and eventually real outcomes.

---

## 7. Cost Notes

Reading can be one of the lowest recurring-cost exam skills if shaped carefully.

### Preferred low-cost default

- reviewed answer keys score attempts deterministically;
- reviewed explanation/rationale metadata is reused;
- task selection and learner-state updates are deterministic;
- common repair explanations are templated/cached;
- original exercises are authored or generated **in batches**, reviewed once, and reused;
- Corpus-derived frequency/difficulty/distractor intelligence is precomputed;
- no premium model call is required for a normal learner Reading attempt.

### Where AI may be worth paying for

AI can materially help **offline** with:

- drafting natural original passages/notices;
- producing controlled-difficulty variants;
- generating plausible distractors;
- detecting paraphrase relationships;
- explaining why distractors fail;
- proposing metadata and skill tags;
- ambiguity review as one signal among QA checks.

Higher-quality models are justified only for batches where cheaper generation or deterministic QA cannot achieve acceptable naturalness and answer certainty.

### Cheapest fallback

If generation quality/cost is poor, start with a **smaller manually reviewed original Reading bank** and rotate it intelligently. A smaller trustworthy bank is better than endless ambiguous live generation.

### Explicit anti-patterns

Do not require:

- one LLM call per objective answer;
- one LLM call per distractor explanation at runtime;
- live generation of every learner item;
- premium-model classification of obvious deterministic mistakes;
- repeated generation of equivalent content that could be cached/reused safely.

The product should upgrade spending only when measured content diversity or quality becomes the actual bottleneck.

---

## 8. Decisions Made

1. Reading is shaped around three TELC-target task families: **R1 global/heading matching, R2 detailed comprehension, and R3 selective situation-to-notice matching**.
2. Target blueprint details are versioned and must be reverified before P4/mock content is called current TELC-realistic.
3. Every task family has P0–P4 variants that preserve the exam reasoning mechanism while varying language, length, distractors, constraints, assistance, and timing.
4. Reading skill mapping is explicit; one correct answer does not automatically update every tagged skill.
5. Vocabulary assistance is targeted and progressively faded. Blanket translation and answer-bearing help cannot count as independent Reading evidence.
6. Synonym/paraphrase recognition is explicitly trained through semantic equivalence, contrast, transformation, and fresh exam-shaped transfer.
7. Bestehen explicitly teaches **when to scan, when to read for gist, and when to close-read**, rather than treating all text the same way.
8. Distractor feedback explains the learner's chosen trap and the decisive disqualifying evidence, not only the correct option.
9. Reading uses open, pace-awareness, practice-timed, target-probe, and P4 target-condition modes. Slow-but-correct evidence is separated from comprehension failure.
10. Reading mistakes follow a narrow diagnosis/repair taxonomy and fresh equivalent retry; immediate success is not permanent repair.
11. Everyday practice defaults to original reviewed content grounded in Corpus intelligence. Exact source material is surfaced only when rights permit it.
12. Standard Reading scoring and coaching state updates should be deterministic and low-cost; AI belongs mainly in offline content creation/QA.
13. Reading emits task-family coverage, assistance, timing, skill mapping, cause, distractor, repair, retry, validity, and provenance evidence for the learner/readiness model.
14. Strong Reading evidence later contributes to **written** readiness, but Stage 09 does not invent final weights or pass probabilities.

---

## 9. Open Questions / Deferred Decisions

### Owner questions

**None.** No product decision in Stage 09 requires an owner preference to proceed.

### Deferred to later shaping stages

- **Exact final readiness weights, score prediction, and evidence minimums:** Stage 15.
- **Final combined Reading + Sprachbausteine time-allocation strategy and full mock behavior:** Stages 10 and 16.
- **Cross-modality generated-content QA thresholds and final naturalness review policy:** Stage 21.
- **Exact Corpus payload/interface/versioning mechanics:** Stage 22.
- **Accessibility accommodations that qualify as target-condition equivalent:** Stage 25.
- **Empirical recalibration of pace targets, repair thresholds, content difficulty, and evidence weighting:** Stage 26 and future learner data.

These are not blockers for Reading product shaping. This document defines the learner-facing behavior and evidence contract they must preserve.

---

## 10. Definition of Done Check

Stage 09 is complete when all of the following are true:

- [x] TELC B1 Reading task patterns are mapped.
- [x] Lower-difficulty exam-shaped variants are defined.
- [x] Each task family is mapped to specific Reading skills.
- [x] Vocabulary assistance and its evidence consequences are defined.
- [x] Synonym/paraphrase recognition training is defined.
- [x] Scanning versus detailed-comprehension practice is defined.
- [x] Distractor explanations and trap taxonomy are defined.
- [x] Timed and untimed Reading modes are defined without inventing a false official per-part time rule.
- [x] Reading-specific diagnosis, repair, fresh retry, and delayed-return behavior are defined.
- [x] Reference material versus original/generated content use is defined.
- [x] Exercise flows and assistance states are concrete enough for later UX design.
- [x] Feedback examples demonstrate the exam-coach voice and causal diagnosis.
- [x] Reading evidence emitted to the learner/readiness model is defined.
- [x] Low-confidence, ambiguous, stale-blueprint, technical, and accessibility cases preserve uncertainty rather than inventing performance conclusions.
- [x] Cost-sensitive defaults avoid per-attempt premium AI.
- [x] Cross-stage dependencies and deferred decisions are explicit.

**Done outcome:** Reading develops both German comprehension and TELC-solving strategy from supported A1-level entry work through independently timed B1 target conditions, and every meaningful Reading attempt can improve future coaching without overstating readiness.