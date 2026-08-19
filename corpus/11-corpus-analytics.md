# Bestehen / Corpus — Stage 11: Corpus Analytics

> **Status:** Authoritative Stage 11 product-shaping decision  
> **Product:** Bestehen / Corpus  
> **Initial domain:** German A2–B1 exam and exam-style material  
> **Primary downstream customer:** Bestehen / App  
> **Core principle:** Corpus analytics must convert independent, quality-weighted exam evidence into explainable signals about what is tested, how patterns differ by level/provider, and what the App should treat as important—without turning raw repetition, mirrors, prolific publishers, or weak metadata into false prevalence.

## 1. Purpose and Scope

Stage 11 defines the intelligence Bestehen / Corpus must produce so it becomes more than a searchable archive. The stage answers questions such as:

- Which vocabulary, grammar, topics, task forms, skills, reasoning patterns, and distractor patterns recur in credible A2/B1 exam evidence?
- Which patterns are genuinely common versus merely repeated inside one long document, publisher collection, mirror family, or shared stimulus?
- How does the evidence change from A2 toward B1?
- Which patterns are broadly B1-relevant and which disproportionately characterize TELC B1?
- Which combinations of skill, task, topic, language feature, reasoning, and distractor are common enough to ground original exercise generation?
- Which Corpus outputs should influence App coaching priority, content generation, and readiness evidence design?
- How strong is the evidence behind each conclusion, and what should happen when evidence is sparse, duplicated, low-confidence, historically stale, or concentrated in one source family?

This is **product shaping, not analytics architecture**. It defines analytical questions, counting units, weighting rules, output semantics, safeguards, and initial dashboard/report concepts. It does not choose a warehouse, SQL engine, BI product, graph database, notebook stack, scheduled-job framework, vector store, visualization library, or statistical package.

### 1.1 Stage objective

**Corpus should be able to say not merely “this tag appears 180 times,” but “this pattern appears across six independent, mostly A/B-quality B1 materials, is strongly represented in TELC, usually occurs in this task/skill context, and is therefore safe to use as an App priority/generation signal.”**

### 1.2 Product invariants

1. **Independent evidence, not URL/file count, is the default basis for prevalence.**
2. **Frequency and importance are different.** A rare pass-critical productive competency can matter more than a common low-value lexical detail.
3. **Presence and tested role are different.** Grammar/vocabulary merely present in a passage must not be treated as deliberately tested.
4. **Different analytics require different canonical scopes.** A shared passage is one lexical stimulus even when five Items reference it; five Items can still be five real item observations for item-level reasoning analysis.
5. **A standalone exercise is not evidence of whole-exam balance.** Scope fit is mandatory.
6. **Provider volume must not become provider authority.** One publisher producing thousands of exercises cannot dominate a cross-provider conclusion by volume alone.
7. **TELC-specific and generic-B1 analytics remain separate.** Cross-provider recurrence does not prove target-format prevalence.
8. **Low-confidence material may broaden context but cannot manufacture a decision-grade priority.**
9. **Uncertainty is output.** Sparse support, unresolved dependency, missing denominator coverage, taxonomy uncertainty, and source concentration must remain visible.
10. **Analytics are precomputed/recomputed as Corpus intelligence.** Bestehen / App should not need paid AI calls to rediscover corpus frequencies during learner sessions.
11. **Rights do not decide whether abstract analytics are true.** Rights govern downstream use of source expression; non-reconstructive analytics remain separately governed by Stage 04.
12. **Corpus analytics inform App decisions but do not own learner state or readiness.**

---

## 2. Inputs / Existing Decisions

Stage 11 preserves the shared Product Overview, Identity, both live shaping checklists, and Corpus Stages 01–10.

### 2.1 Mission and source breadth — Stages 01–02

Earlier stages established that Corpus is an **exam-data and intelligence product** whose primary customer is Bestehen / App; its initial acquisition domain is German A2, B1, and mixed A2–B1 exam material; TELC B1 is the strongest target signal while the source universe remains broader than TELC; official and unofficial sources may both contribute useful evidence; and success is measured by actionable intelligence rather than raw document count.

Stage 02 also established that Source Observations, underlying material, and mirrors are separate concepts; standalone exercises and fragments are valid evidence but have narrower scope; and coverage-driven discovery matters more than indiscriminate crawling.

### 2.2 Trust and analytical influence — Stage 03

Stage 03 established the A/B/C/D confidence model and the default eligible analytical weights:

| Evidence tier | Default weight in eligible aggregate analytics |
|---|---:|
| **A** | **1.00** |
| **B** | **0.70** |
| **C** | **0.25** |
| **D** | **0.00** |
| **Quarantined** | **0.00** |

It also established that decision-grade analytics may include C only as bounded support, while App learning-priority changes should normally have at least **two independent A/B underlying materials**. One verified official TELC source can establish that a format/requirement exists; it cannot establish prevalence by itself.

Stage 11 adopts this system rather than creating a second confidence score.

### 2.3 Rights — Stage 04

Stage 04 established that confidence/authenticity and usage rights are independent. `REFERENCE_ONLY` or `UNKNOWN_REVIEW_REQUIRED` material can still contribute non-reconstructive analytics when trust and policy permit, while exact source content remains blocked from learner reuse unless the rights gate allows it.

Therefore a frequency conclusion may be usable even when the source text that supported it may not be displayed to a learner.

### 2.4 Canonical evidence units — Stage 05

Stage 05 established Source Observation → Document → Exam/Test Set → Section → optional Part → Task → Item, with Instructions, Stimuli, Response Options, Answers, Explanations, Scoring Rules, and Assets separately addressable.

Critical Stage 11 consequences are:

- Instructions are excluded from ordinary tested-language frequency by default.
- Shared Stimuli are represented once and must not be multiplied merely because several Items reference them.
- An Item is the smallest response/scoring-addressable unit.
- Incomplete exams remain incomplete rather than being forced into a whole-exam denominator.

### 2.5 Taxonomy — Stage 06

Stage 06 established the multi-axis taxonomy families used by this stage: provider/exam, CEFR, section, task shape, topic, grammar, vocabulary/domain/functional language, Reading skills, Listening skills, Writing competencies, Speaking competencies, strategy, reasoning patterns, and distractor patterns.

Assignments retain a role such as `primary_tested`, `secondary_tested`, `prerequisite_supporting`, `context`, `incidental_present`, or `distractor`, plus assignment confidence/origin/version.

Stage 11 therefore never equates “tag attached” with “skill deliberately tested.”

### 2.6 Difficulty and relevance — Stage 07

Stage 07 established:

- multidimensional L/R/T/A/P difficulty;
- separate Generic-B1 (`GB1`) and TELC-B1 (`TELC`) relevance;
- a conceptual evidence-contribution model: **Independence × Stage03ConfidenceWeight × TargetAlignment × Currentness × ScopeFit**;
- TELC-specific target-alignment priors by source/evidence family;
- a **15% maximum effective C-tier contribution** to published relevance/priority evidence mass;
- when eligible official TELC evidence exists, unofficial/third-party evidence should normally contribute no more than **35% of effective support for a high-confidence TELC-specific conclusion**;
- source volume must not dominate aggregate results;
- weighted distributions and support strength are preferable to raw means/counts.

Stage 11 uses these rules as hard analytical safeguards.

### 2.7 Pipeline, independence, and QA — Stages 08–10

Stage 08 requires offline/incremental enrichment and partial publication by use. Stage 09 requires three distinct counts where relevant: **observation count, canonical content occurrence count, and independent evidence count**. It requires deduplication/independence treatment **before** confidence/relevance weights are summed and allows an independence range when dependency is unresolved.

Stage 10 requires capability-scoped production readiness and a quality vector rather than a single validity flag. Analytics must therefore respect local extraction quality, correctness readiness, taxonomy confidence, asset linkage, and unresolved duplicate state rather than assuming every published record is equally usable for every metric.

No earlier shaping decision is changed by Stage 11.

---

## 3. Decisions and Rationale

## 3.1 Use an evidence-aware analytic result, not a naked frequency number

**Decision:** Every decision-grade Corpus analytic must expose enough context to explain the result. Conceptually an analytical output should carry:

- **subject** — taxonomy node/pattern/provider/task/etc.;
- **metric family** — vocabulary frequency, task prevalence, provider comparison, co-occurrence, progression, etc.;
- **scope/filter** — CEFR, provider family, section, task type, currentness window, source class, or other relevant slice;
- **counting unit** — Stimulus, Task, Item, Exam/Test Set, independent content family, or another explicitly named unit;
- **raw/observation count where useful**;
- **canonical content occurrence count where useful**;
- **independent evidence count or conservative range**;
- **eligible denominator** and denominator coverage;
- **effective evidence mass** after Stage 03/07/09 weighting;
- **distribution/prevalence value** rather than only a count;
- **A/B/C contribution mix** and source/provider concentration where material;
- **sufficiency/confidence label**;
- **method/taxonomy/model version** and last recomputation time;
- **allowed downstream uses** when a result is restricted to exploratory rather than decision-grade consumption.

The exact storage/serialization is a Stage 12/architecture decision. The product requirement is that a later App or operator can distinguish “40 occurrences from one publisher” from “40 occurrences across independent established evidence.”

## 3.2 Maintain exploratory and decision-grade analytical lanes

**Decision:** Corpus supports two analytical postures.

| Lane | Purpose | Evidence posture | Downstream use |
|---|---|---|---|
| **Exploratory** | Discover candidate patterns, coverage gaps, anomalies, and review targets | C+ may contribute with Stage 03 weights; unresolved dependency may be shown with ranges; sparse results allowed | Operator/research use; must not directly change learner priority/readiness |
| **Decision-grade** | Produce stable signals App and final shaping decisions may rely on | A/B must materially support conclusion; C remains capped; D/quarantine zero; independence/scope/currentness/QA gates apply | App priority priors, generation grounding, target profile, readiness evidence design |

A candidate can move from exploratory to decision-grade when supporting evidence and QA improve. The distinction prevents a useful but uncertain pattern-discovery capability from silently becoming learner-facing truth.

## 3.3 Use denominator-aware prevalence as the main frequency language

**Decision:** Raw counts are retained, but the default comparison metric is **prevalence over an explicit eligible denominator**.

Examples:

- “Housing vocabulary occurs in 42% of eligible independent B1 reading Stimuli.”
- “Constraint-filtering is a primary reasoning pattern in 31% of eligible TELC B1 reading Items of this task family.”
- “Matching tasks represent 24% of eligible Reading Tasks across complete/representative TELC B1 test sets.”

This is preferable to “housing appears 387 times” because raw count is highly sensitive to passage length, repeated tokens, number of items per passage, publisher volume, and corpus composition.

Raw token/occurrence density remains useful as a secondary measure where the analytical question is genuinely about exposure density.

## 3.4 Keep three frequency concepts separate

**Decision:** Stage 11 distinguishes:

1. **Exposure frequency** — how often a learner is likely to encounter a language/topic feature in tested source material.
2. **Tested-dependency frequency** — how often success appears to depend materially on that feature/skill/reasoning pattern.
3. **Exam-structure prevalence** — how often a task/section/response pattern occurs in representative exam structures.

A grammar form can be common exposure but rarely the decisive tested feature. A task type can be structurally common even if its vocabulary changes every time. The App uses these signals differently.

## 3.5 Balance evidence at the scope appropriate to the question

**Decision:** There is no universal “one row = one vote.” The correct evidence unit depends on the analytical question.

| Question | Default counting scope | Key guardrail |
|---|---|---|
| Lexical/grammar exposure | Stimulus or tested text unit | Shared Stimulus counted once per occurrence, not once per linked Item |
| Task-form prevalence | Task within representative Exam/Test Set | Standalone exercise cannot infer whole-exam balance |
| Response-mechanic prevalence | Item/Task as defined by source semantics | Multi-part/composite structure preserved |
| Skill/reasoning prevalence | Item/Task based on assignment role | Primary/secondary tested kept separate from supporting/incidental |
| Distractor prevalence | Eligible objective Item and its wrong options | Requires correctness-ready answer context |
| Provider whole-exam comparison | Exam/Test Set and provider-section distribution | Long exams/item-heavy publishers do not gain automatic dominance |
| Difficulty distribution | Item/Task/Stimulus according to Stage 07 dimension | Preserve distribution/spread, not just average |
| Topic prevalence | Task/Stimulus with role | Repeated item references do not multiply one context |

Stage 09 duplicate/derivative treatment is applied before any of these units gain evidence influence.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Vocabulary analytics

### Product question

**Which words, lexical concepts, domains, functional phrases, and paraphrase relationships are common enough in credible A2/B1 exam evidence to deserve recognition/review priority, generation coverage, or explicit learner support?**

### Required outputs

Vocabulary analytics should distinguish at least:

1. **Lemma/concept exposure prevalence** — share of eligible independent text-bearing units containing the lexical concept at least once.
2. **Token density** — occurrences per normalized amount of tested text, useful for exposure intensity but secondary to prevalence for priority.
3. **Exam/material spread** — number/share of independent Exam/Test Set or source families in which the concept occurs.
4. **Section/task distribution** — where the vocabulary appears.
5. **CEFR progression distribution** — A2 vs mixed A2–B1 vs B1 evidence.
6. **TELC vs generic-B1 distribution** — target-specific versus broad recurrence.
7. **Role/context** — whether the lexical concept is answer-critical/tested, prerequisite-supporting, or merely contextual where this can be determined.
8. **Phrase/function frequency** — useful multi-word chunks and communicative functions should be analyzable separately from individual word tokens.
9. **Lexical relation evidence** — recurring synonym/paraphrase relations when they are part of the tested reasoning pattern.

### Counting rules

- Exclude ordinary Instructions, answer keys, explanations, copyright/footer text, navigation, and OCR noise from tested-language frequency.
- A shared reading/listening Stimulus is counted once for lexical exposure even when many Items reference it.
- Repetition inside a Stimulus is real token exposure and remains visible in token density, but **unit prevalence counts the concept once per eligible unit** so a repeated word cannot manufacture cross-material recurrence.
- Surface forms should be normalized to a lexical concept/lemma for aggregate analysis while preserving source form for examples and morphology-specific questions.
- Named entities and one-off strings do not automatically become learner-priority vocabulary nodes merely because they are frequent in one source.
- Exact/derivative copies do not add independent lexical evidence for inherited text.
- A re-recording of the same listening script does not add another lexical occurrence, even if it may add acoustic evidence under Stage 09.

### App use

- **Priority:** increase review/training emphasis for lexical concepts that combine strong TELC/GB1 relevance, broad independent prevalence, and learner weakness; raw token frequency alone does not decide priority.
- **Exercise generation:** select realistic vocabulary domains and paraphrase relations for a task/skill/difficulty profile without copying source wording.
- **Readiness:** vocabulary analytics define expected evidence coverage and skill context, but do not directly increase/decrease an individual learner’s readiness score.

## 4.2 Grammar analytics

### Product question

**Which grammar patterns are commonly encountered, deliberately tested, or productively demanded in A2/B1 exam evidence, and how does that differ by section/task/provider/level?**

### Required outputs

Grammar analytics separate:

- **exposure prevalence** — pattern occurs in tested input;
- **tested-dependency prevalence** — correct performance materially depends on recognizing/producing the grammar pattern;
- **productive-demand prevalence** — Writing/Speaking tasks/rubrics strongly invite or require the structure/function to perform well enough at B1;
- **section/task distribution**;
- **A2→B1 shift**;
- **TELC vs generic-B1 distribution**;
- **difficulty association** where Stage 07 evidence supports it;
- **common co-occurring vocabulary/functions/skills**.

### Counting rules

- A grammar construction merely present in a passage is **not** automatically a tested grammar event.
- Stage 06 assignment role is authoritative: `primary_tested` and `secondary_tested` support tested-frequency analytics; `prerequisite_supporting`/`incidental_present` belong to exposure/co-occurrence views unless evidence shows answer dependency.
- Grammar analytics should normally aggregate canonical grammar concepts rather than every inflected surface form.
- Productive tasks can show grammar demand without a unique correct structure; do not convert rubric/task affordances into fake answer-key frequency.
- Language Elements may contain concentrated explicit grammar evidence and must not be allowed to make a grammar concept look equally dominant in Reading/Listening/Writing/Speaking. Section-conditioned results are mandatory.

### App use

- **Priority:** supports exam-driven grammar repair/review when the learner is weak on a grammar node that is materially tested/relevant.
- **Exercise generation:** grounds which grammar relationships naturally belong in cloze, reading, writing, or speaking scenarios and at what difficulty band.
- **Readiness:** informs which grammar competencies should be represented in evidence coverage; learner mastery still comes from App attempts/evaluation.

## 4.3 Topic analytics

### Product question

**Which practical contexts repeatedly frame A2/B1 exam tasks, and which topics are disproportionately relevant to TELC or particular skills/task forms?**

### Required outputs

- primary-topic prevalence by Task/Stimulus;
- secondary/context topic prevalence separately;
- section/task/provider/level distribution;
- topic × skill and topic × task co-occurrence;
- topic × vocabulary-domain association;
- TELC-vs-generic over/under-representation;
- concentration/diversity measures sufficient to detect a corpus or generated-bank topic imbalance.

### Counting rules

- Count a primary topic once per eligible Task/Stimulus occurrence rather than once per Item that shares the context.
- A long passage can have one primary topic and several secondary contexts without those contexts receiving equal analytical weight.
- Topic is **context**, not mastery. “Health appears often” does not mean the learner should study health facts; it means language/exam practice should expose the learner to that context.
- A prolific publisher cannot make its favorite topic look universally common without independent/provider-balanced support.

### App use

- **Priority:** topic familiarity may break ties or support a learner-specific gap, but topic frequency should not outrank pass-critical skills merely because it is common.
- **Exercise generation:** maintain realistic topic mix, choose plausible contexts for target grammar/vocabulary/skills, and prevent repetitive generation.
- **Readiness:** use only for coverage diagnostics (for example, all Reading evidence came from one narrow topic), not as a direct pass-readiness competency.

## 4.4 Task-type analytics

### Product question

**Which activity families, response mechanics, stimulus forms, and interaction shapes actually occur, how often do they appear within representative exams, and which are target-specific versus generic?**

### Required outputs

- Task activity-family prevalence;
- response-mechanic prevalence;
- stimulus-form prevalence;
- Speaking interaction-shape prevalence;
- section-conditioned distributions;
- provider/CEFR distributions;
- task share within complete/representative Exam/Test Sets;
- standalone-practice volume as a **separate** measure;
- difficulty distributions by task type;
- skill/reasoning/distractor associations by task type.

### Counting rules

- **Whole-exam task balance uses only complete or sufficiently representative Exam/Test Sets for the claimed scope.** Intentional excerpts and standalone exercises can establish existence/variation but not section proportions.
- The Task is the main counting unit for activity family; Item is used when response mechanics are item-level.
- One Exam/Test Set should contribute bounded structural evidence to a provider-section distribution rather than gaining arbitrary extra authority because it contains many short Items.
- Provider-native labels remain available, but comparisons use normalized Stage 06 facets.
- Reused official items/publications may be reported as provider reuse, but exact underlying content remains one independent-origin family according to Stage 09.

### App use

- **Priority:** tells the coach which target task forms need routine coverage and which are minor/rare.
- **Exercise generation:** provides the shape that original tasks should reproduce: response mechanic, stimulus form, interaction mode, typical skill/reasoning combinations, and difficulty envelope.
- **Readiness:** helps define whether learner evidence covers the task forms expected for TELC B1; task prevalence itself is not learner performance.

## 4.5 Skill-frequency analytics

### Product question

**Which receptive skills, productive competencies, strategies, and reasoning patterns are actually being tested, and where do they matter most?**

### Required outputs

For every skill/competency/reasoning node, analytics should expose separately:

- `primary_tested` prevalence;
- `secondary_tested` prevalence;
- supporting/prerequisite association;
- section/task/provider/level distribution;
- difficulty distribution;
- TELC and GB1 relevance/support;
- A2→B1 progression behavior;
- frequent co-occurring grammar/vocabulary/topic/task/distractor nodes;
- evidence sufficiency/concentration.

### Role rule

**Do not collapse primary, secondary, supporting, and incidental roles into one unqualified “skill frequency.”** If a later consumer needs a combined score, Stage 12/App may define a transparent use-specific combination. Stage 11 keeps the evidence roles visible rather than introducing an arbitrary hidden multiplier.

### App use

- **Priority:** this is one of the strongest Corpus inputs to the daily coaching engine. The App combines the Corpus evidence with learner weakness, recency, assistance conditions, exam-date urgency, section coverage, and pass constraints.
- **Exercise generation:** choose a primary skill and realistic supporting skills/contexts without overloading every exercise with all tags that happen to co-occur.
- **Readiness:** expected skill/task coverage helps determine whether the App has enough representative learner evidence. Corpus does not decide learner mastery.

## 4.6 Provider comparisons

### Product question

**How do TELC, Goethe, ÖSD, DTZ, and credible third-party material differ after controlling for level, section, task scope, confidence, and corpus imbalance?**

### Comparison dimensions

Provider comparison should support matched views of:

- task-type distribution;
- skill/reasoning distribution;
- topic distribution;
- vocabulary/grammar profile;
- distractor behavior where correctness-ready evidence exists;
- L/R/T/A/P difficulty distributions;
- scoring/section exposure where source evidence supports it;
- A2/B1 progression within provider families where coverage exists;
- source/evidence quality and coverage so apparent differences can be interpreted responsibly.

### Balancing rules

1. Compare like with like: B1 Reading against B1 Reading, not one provider’s whole B1 exam against another provider’s A2 standalone exercises.
2. Whole-exam distribution comparisons require representative Exam/Test Set scope; standalone material remains in a separate practice-material view.
3. Use independent evidence and effective evidence mass after Stage 03/07/09 rules.
4. Preserve provider-level distributions and support rather than pooling every Item into one giant item-weighted corpus.
5. A source family/publisher with many items may add precision within its own distribution but must not automatically dominate a cross-provider conclusion.
6. When one third-party family supplies most of the evidence, mark **source concentration** explicitly and avoid language implying broad provider consensus.
7. Difficulty comparisons preserve medians/spread/upper challenge or equivalent distributions rather than one average.
8. Provider differences are descriptive evidence, not judgments that one exam is “better.”

### App use

- **Priority:** provider comparisons matter mainly for distinguishing **TELC-specific priorities from broadly transferable B1 skills**.
- **Exercise generation:** broad provider evidence can supply diverse contexts/variants, while TELC evidence controls target task shape and final realism.
- **Readiness:** TELC remains the target distribution; non-TELC evidence can strengthen generic skill understanding but must not redefine the target exam.

## 4.7 A2 → B1 progression analytics

### Product question

**For the same underlying skill, language concept, task family, or productive demand, what changes as credible exam evidence moves from A2 through mixed A2–B1 toward B1?**

### Progression dimensions

Progression analysis should compare matched taxonomy nodes/patterns across levels on:

- prevalence/exposure shift;
- primary-tested versus supporting-role shift;
- L/R/T/A/P difficulty change;
- lexical abstraction/paraphrase demand;
- grammar/syntax demand;
- number and interaction of constraints;
- distractor/reasoning complexity;
- productive content-point, organization, register, spontaneity, and interaction demand;
- task/response mechanic change where providers alter format with level;
- provider consistency versus provider-specific progression behavior.

### Progression classifications

A pattern may be described as:

| Classification | Meaning |
|---|---|
| **Foundational / stable** | Present at A2 and B1 with similar underlying role; B1 may increase difficulty without changing the core skill |
| **Intensifying** | Exists at A2 but becomes more frequent, more central, less assisted, or more demanding at B1 |
| **B1-emergent / B1-dominant** | Rare or supporting at A2, materially more central in B1 evidence |
| **De-emphasized** | More prominent at A2 than B1 in the available matched evidence |
| **Provider-specific progression** | Shift is strong within one provider family but not supported as a generic A2→B1 pattern |
| **Inconclusive** | Evidence is too sparse, unbalanced, or dependent to claim a progression pattern |

### Counting and comparison rules

- Compare the **same canonical taxonomy node/pattern** across level slices rather than comparing unrelated “typical A2” and “typical B1” content.
- Mixed A2–B1 material is a bridge slice, not automatically counted once as A2 and once as B1. Local Task/Item classification can narrow the level when evidence supports it.
- Provider-balanced results should be preferred for generic progression. A provider changing its own format is not automatically a CEFR-wide progression fact.
- Difficulty increase is not itself CEFR proof; Stage 06 level classification and Stage 07 difficulty remain separate.
- Frequency does not define pedagogical prerequisite order. A low-frequency prerequisite can still be important to learn first.
- Corpus has no launch requirement to build an A1 acquisition corpus. The App may create A1-accessible scaffolds for A2/B1-derived nodes.

### App use

- **Priority:** helps distinguish foundation repair from true B1 target work. An A1/A2 learner can practice a B1-relevant skill first in its lower-demand form rather than being sent through a generic course chapter.
- **Exercise generation:** select a progression-consistent version of the same skill: simpler language/fewer constraints first, then B1-equivalent reasoning and realistic conditions.
- **Readiness:** only B1-/target-condition learner evidence can establish B1 readiness; success on an A2 precursor can support mastery history but must not be treated as equivalent target evidence.

## 4.8 TELC-vs-generic-B1 analytics

### Product question

**Which patterns are shared B1 exam competence, which are disproportionately important for TELC B1, and which are generic B1 evidence that should not control target-exam emphasis?**

### Use two baselines, not one circular comparison

**Decision:** Corpus maintains two complementary B1 profiles:

1. **TELC B1 target profile** — eligible TELC B1 and explicitly weighted TELC-family/target-relevant evidence using Stage 07 target alignment/currentness.
2. **Generic B1 profile** — provider-balanced eligible B1 evidence across established provider families, with confidence/independence treatment and no assumption that any one provider defines “generic B1.”

For an explicit **TELC over/under-index comparison**, the comparator should be the eligible **non-TELC established-B1 profile**. This avoids diluting the contrast by placing TELC evidence on both sides of the comparison.

### Comparison outputs

A node/pattern can be classified as:

| Result | Meaning | App implication |
|---|---|---|
| **Shared B1 core** | Strong generic-B1 support and clear TELC relevance | High transfer value; teach as both language competence and target preparation |
| **TELC-over-indexed** | Materially more prevalent/central in TELC than the balanced non-TELC B1 comparator | Increase target-specific practice/realism once learner can handle the underlying skill |
| **TELC format/requirement specific** | Verified target evidence establishes a TELC-specific structure/constraint even if generic recurrence is low | Must be represented in target mocks/readiness coverage; prevalence language remains conservative if support is sparse |
| **Generic-B1 transferable** | Strong cross-provider B1 signal but limited target-specific prevalence | Useful foundation/repair/generation diversity; lower target-format priority |
| **Provider-specific non-TELC** | Concentrated in another provider without meaningful TELC support | Do not let broad-corpus volume become TELC priority |
| **Inconclusive** | Coverage/support/currentness too weak for a directional comparison | Fall back to curated target facts and broader node definitions |

### Rules

- **Absence is not evidence of absence** when TELC coverage is sparse. Use “not observed in the current eligible TELC evidence” rather than “not tested by TELC” unless an authoritative specification supports the stronger statement.
- One official TELC example can establish existence/requirement, not frequency.
- TELC-specific priority claims normally require at least two independent A/B materials, consistent with Stage 03/07.
- Current official/provider evidence overrides contradictory third-party claims about current format/requirements, with review where needed.
- Generic-B1 pooling should remain provider-balanced; a large publisher practice bank cannot define the generic baseline alone.

### App use

- **Priority:** TELC-over-index and target-specific requirements strengthen the exam-priority prior; shared-core skills remain important even when not uniquely TELC.
- **Exercise generation:** generic B1 sources can diversify language/context while TELC evidence controls target-facing task mechanics, reasoning shape, delivery constraints, and final realism.
- **Readiness:** the target profile defines what representative learner evidence should cover. Generic B1 success cannot substitute for missing target-format evidence where format/conditions matter.

## 4.9 Distractor and reasoning-pattern analytics

### Product question

**How do eligible objective exam items make wrong answers plausible, what reasoning operation is needed to reject them, and which patterns matter most for TELC B1?**

### Eligibility

Distractor analytics require:

- an objective Item with a valid response mechanic;
- correctness-ready answer/key context under Stage 10;
- sufficient source/extraction/taxonomy confidence for the specific reasoning/distractor assignment;
- no unresolved answer dispute that changes which option is correct;
- duplicate/independence treatment applied first.

A task without a verified answer can still contribute task/skill/topic evidence, but it must not contribute decision-grade “this wrong option is a distractor of type X” analytics.

### Required outputs

- reasoning-pattern prevalence by Section/Task/provider/level;
- distractor-pattern **Item prevalence** — share of eligible Items containing at least one distractor of that pattern;
- distractor **option share** — secondary measure showing how wrong-option inventory is composed;
- reasoning × distractor pairing prevalence;
- difficulty association (especially Stage 07 `R` and relevant `A/L` effects);
- TELC-vs-generic distribution;
- common failure-sensitive lexical/grammar cues where justified by evidence.

### Counting rules

- Item prevalence is the primary priority measure so an Item with three similar distractors does not look like three independent tested occurrences.
- Option share remains useful for generation design and QA.
- Similar distractor wording in copied/derivative Items adds no independent prevalence.
- A distractor can use a vocabulary cue without making that vocabulary node the primary tested skill.
- Writing/Speaking do not receive fake distractor labels; their equivalent challenges are productive/interaction/rubric demands.

### App use

- **Priority:** repeated learner mistakes can be mapped to Corpus-supported reasoning/distractor families, allowing repair to target “missed restriction,” “keyword trap,” “speaker correction,” etc. rather than only the content topic.
- **Exercise generation:** generate fresh wrong options that reproduce the **reasoning trap**, not copied wording from source material.
- **Readiness:** distractor analytics influence which reasoning failures should be represented in objective-task evidence; they do not independently score readiness.

## 4.10 Co-occurrence analytics

### Product question

**Which combinations of task, skill, reasoning, topic, vocabulary, grammar, and distractor naturally occur together often enough to guide realistic practice and explain exam patterns?**

### Allowed relationship scopes

Co-occurrence strength must be scope-aware:

| Scope | Interpretation |
|---|---|
| **Same Item** | Strongest evidence that two concepts participate in one answerable decision |
| **Same Task** | Strong evidence that concepts belong to one coherent exam activity |
| **Same shared Stimulus** | Strong context/exposure relationship, but not proof each linked Item tests every concept |
| **Same Section/Exam** | Broad co-presence only; useful for coverage/planning, weak for claiming a direct semantic relationship |

The output must state its scope. “Grammar X co-occurs with Skill Y in the same exam” must not be used as though they interact in the same Item.

### High-value co-occurrence families

Initial analytics should prioritize combinations with clear product value rather than computing every possible graph pair:

- Task type ↔ primary/secondary skill;
- Task type ↔ reasoning pattern;
- Task type ↔ distractor pattern;
- Reasoning ↔ distractor;
- Skill ↔ grammar tested dependency;
- Skill ↔ vocabulary/domain or functional language;
- Topic ↔ vocabulary/domain;
- Topic ↔ task/skill;
- Writing/Speaking competency ↔ functional language/register demand;
- difficulty dimension/band ↔ task/skill/reasoning pattern;
- Task + Skill + Topic or Task + Reasoning + Distractor **triples** only when support is sufficient for generation/diagnosis value.

### Metrics

For an eligible pair/combination, Corpus should support:

- independent support count/evidence mass;
- joint prevalence;
- conditional prevalence, e.g. “when Task A occurs, how often Skill B is primary-tested”;
- base prevalence of each member;
- **lift/over-representation** versus base rates when denominator/support quality is adequate;
- level/provider/TELC slices;
- evidence sufficiency and concentration.

Lift is useful because two very common tags can co-occur often by chance. However, it must be suppressed/qualified on sparse denominators rather than displayed as a dramatic ratio from one or two examples.

### Sufficiency rule

A co-occurrence may be shown exploratorily from C+ evidence, but it cannot become a decision-grade App priority/generation rule unless it is materially supported by the same A/B corroboration rules used for learning-priority conclusions. A single official source can establish that a combination exists; it cannot establish that the combination is typical.

### Cost/complexity guardrail

Do not turn the taxonomy into an unrestricted all-pairs/all-triples mining exercise. Start with the product-useful family pairs above, cache the results, and only promote additional relationships when they answer a specific coaching/generation question or repeatedly appear as useful exploratory candidates.

### App use

- **Priority:** co-occurrence helps explain where a weakness tends to cost points, but learner evidence remains the primary personalized signal.
- **Exercise generation:** this is a major grounding input. It enables “a TELC-like Reading matching task testing paraphrase recognition in a housing context with restriction distractors” without copying an underlying source item.
- **Readiness:** co-occurrence helps design representative evidence coverage and prevent a learner from appearing well-tested when all evidence comes from one narrow task/context combination.

## 4.11 Which analytics directly influence Bestehen / App

**Decision:** Corpus outputs have three distinct downstream roles: **exam-priority priors, generation grounding, and readiness evidence design**. They must not be collapsed into one opaque “importance score.”

### A. App coaching priority

Corpus may directly provide or support these **exam-side priors**:

- TELC relevance and currentness;
- task/skill/reasoning prevalence in eligible target evidence;
- generic-B1 relevance/transfer value;
- scoring/section exposure from Stage 07 where source evidence supports it;
- A2→B1 progression classification;
- high-value vocabulary/grammar tested-dependency prevalence;
- distractor/reasoning prevalence;
- difficulty profile/distribution;
- evidence sufficiency/confidence/concentration.

The App then combines those priors with **learner-specific evidence**: mastery/weakness, recurrence of mistakes, recency/decay, assistance, timing, review due state, learner fatigue, section pass risk, exam date, and available session time.

**Boundary:** Corpus can say “this is important for TELC B1.” Only App can say “this learner should practice it today.”

### B. Exercise generation

Decision-grade Corpus analytics may directly ground:

- target Task/response/stimulus/interaction shape;
- primary skill/reasoning pattern;
- typical supporting skill/language combinations;
- realistic topic/domain distribution;
- vocabulary/grammar demand by level/difficulty;
- distractor families and wrong-option composition;
- difficulty envelope and relevant L/R/T/A/P dimensions;
- target-vs-generic pattern distinction;
- anti-repetition/content-diversity targets.

Generation should consume **abstract pattern intelligence**, not require verbatim source expression. Any direct source content remains separately confidence/rights gated by Stages 03–04 and App content strategy.

A high-frequency pattern with weak evidence does not become a generation template. B+ grounding rules and correctness/structure QA continue to apply.

### C. Readiness evidence design

Corpus analytics may influence readiness **indirectly** by defining what representative target evidence should contain:

- expected TELC section/task coverage;
- high-relevance skill/competency coverage;
- target difficulty/delivery-condition distribution;
- important reasoning/distractor coverage;
- target-specific requirements that must appear in mocks/evidence;
- warnings that evidence is concentrated in one task, topic, assistance state, or non-target provider shape.

Corpus analytics must **not**:

- award learner readiness points;
- convert corpus frequency into learner mastery;
- change TELC pass thresholds;
- let success on many common low-value patterns compensate for a missing pass-critical written/oral requirement;
- let A2 precursor success substitute for B1 target-condition evidence;
- let generic-B1 evidence replace TELC-specific evidence where target format/conditions matter.

**Boundary:** Corpus defines the target evidence distribution; App evaluates the learner against it while preserving the independent written/oral pass constraints already shaped in the App.

### D. Fallback when Corpus evidence is weak

When a result is not decision-grade, the App should receive one of:

- a broader parent-node/pattern result with stronger support;
- an anchor-only target fact without prevalence language;
- an explicit `insufficient evidence`/low-confidence status;
- a curated target-exam default established from verified specification/model evidence.

The App must not infer a precise priority from missing analytics.

## 4.12 Aggregate weighting and distortion safeguards

**Decision:** Every decision-grade aggregate follows this order:

1. **Choose the correct canonical scope and eligible denominator.**
2. **Apply Stage 10 use-specific QA gates.**
3. **Apply Stage 09 duplicate/derivative/independence treatment.**
4. **Use conservative independence bounds when dependency is unresolved.**
5. **Apply Stage 03 confidence eligibility and A/B/C weights.**
6. **Apply Stage 07 TargetAlignment, Currentness, and ScopeFit for the analytical question.**
7. **Apply existing C-tier and third-party caps where relevant.**
8. **Check provider/source-family concentration and coverage balance.**
9. **Compute prevalence/distribution/co-occurrence.**
10. **Attach evidence sufficiency/confidence, concentration, denominator coverage, and version metadata.**

### 4.12.1 Confidence and low-quality safeguards

- A = `1.00`, B = `0.70`, C = `0.25`, D/Quarantine = `0.00` where the use permits those tiers.
- For published relevance/priority analytics, **C-tier contribution is capped at 15% of effective evidence mass**.
- C-only results are exploratory/insufficient, not decision-grade priorities.
- Difficulty calibration remains A/B only according to Stage 07.
- If eligible official TELC evidence exists, third-party/unofficial evidence should normally contribute no more than **35% of effective support for a high-confidence TELC-specific conclusion**.
- One verified official TELC source can establish existence/requirement but not prevalence.
- Relative learning-priority/frequency conclusions normally require at least **two independent A/B underlying materials**.

### 4.12.2 Duplicate and dependency safeguards

- Ten mirrors contribute ten Source Observations but one underlying independent evidence unit.
- Exact/reformatted/fragment copies add no independent inherited-content prevalence.
- Light derivatives preserving the same tested proposition do not create new full independent support.
- Related variants may add a content occurrence when the solve/response is materially new, while lineage dependence remains visible for corroboration claims.
- For unresolved dependencies, use the conservative/minimum independent count for decision-grade conclusions or withhold the conclusion when the range would materially change the result. Do **not** invent fractional independence weights before benchmark calibration.

### 4.12.3 Source/provider-volume safeguards

- Whole-exam prevalence is calculated from representative Exam/Test Sets, not from all standalone Tasks in the corpus.
- Provider comparison first preserves provider-level distributions; it does not let the provider with the most Items become the generic baseline by default.
- Cross-provider claims require actual support across provider families. “Cross-provider” must not mean several third-party websites copying the same source family.
- A single non-target publisher/source family supplying most of the effective evidence is flagged as **concentrated**. The result can remain useful within that source family but must not be described as broad generic-B1 consensus.
- Stage 11 deliberately introduces no new universal numeric source-family cap beyond the Stage 07 15%/35% safeguards. Stage 16 should calibrate whether an additional cap is warranted rather than inventing precision now.

### 4.12.4 Scope and denominator safeguards

- Standalone/fragment material cannot infer full-exam section/task proportions.
- Unknown completeness is excluded from denominators that require complete structure.
- Missing/unknown metadata is not treated as absence or zero.
- Instructions do not enter tested-language frequency by default.
- Shared Stimuli do not multiply lexical/topic exposure across linked Items.
- Productive Writing/Speaking requirements are represented through competencies/affordances, not fake objective-answer counts.

### 4.12.5 Semantic-quality safeguards

- Fine-grained taxonomy analytics require assignment quality adequate for the use; otherwise back off to a broader node.
- Source confidence and taxonomy confidence are independent.
- Distractor analytics require correctness-ready items.
- AI/model self-confidence is not a substitute for Stage 10 benchmark quality.
- A taxonomy version change, merge, split, or corrected mapping must trigger affected analytical recomputation; historical analytics remain version-identifiable.

### 4.12.6 Currentness safeguards

- Old evidence does not lose authenticity merely because it is old.
- Currentness affects target-specific analytical contribution only when format currency matters.
- When evidence shows a target format changed, historical and current profiles remain distinguishable; they are not silently averaged.
- If currentness is unknown, preserve uncertainty rather than applying an arbitrary date-decay penalty.

## 4.13 Evidence sufficiency labels

**Decision:** Corpus results should communicate sufficiency without inventing a fake statistical confidence percentage before Stage 16 calibration.

Recommended product labels:

| Label | Meaning |
|---|---|
| **Insufficient / sparse** | Not enough eligible independent support for the intended claim |
| **Anchor-only** | Strong evidence establishes existence/requirement but not recurrence/prevalence |
| **Corroborated** | At least the existing two-independent-A/B rule for priority/relative-frequency conclusions is satisfied and no major concentration/QA issue dominates |
| **Cross-provider supported** | Corroborated across at least two genuinely distinct established provider families for a generic-B1 claim |
| **Concentrated** | Result is supported but one provider/source family supplies a material majority of the usable evidence, limiting generality |
| **Decision-grade** | Use-specific gates, support, independence, currentness, concentration, and QA are strong enough for the documented App/operator use |

These can coexist: for example, “corroborated but concentrated” or “decision-grade TELC target profile, not cross-provider.” Stage 16 may later replace/augment the labels with empirically calibrated intervals.

## 4.14 Analytical recomputation and versioning

Analytics are derived intelligence, not immutable source facts.

Recompute affected outputs when:

- a source confidence tier changes;
- a duplicate/derivative/independence relationship changes;
- a source moves into/out of quarantine;
- a target-currentness conclusion changes;
- a taxonomy assignment is corrected or a taxonomy version migrates nodes;
- extraction/QA improvement changes usable text, answers, assets, or structure;
- a rights takedown requires derived-data purge/recompute under Stage 04;
- new independent evidence materially changes a distribution;
- Stage 16 recalibrates analytical thresholds/weights.

The App should be able to consume a versioned current snapshot while later Stage 12 defines exact compatibility behavior.

---

## 5. Initial Dashboards / Reports Concept

The product needs **internal intelligence views**, not a BI-stack commitment. A static/generated report, simple internal page, notebook, or later dashboard can satisfy the same product need if it presents the required information.

## 5.1 Corpus Intelligence & Evidence Health

### Product question

**Do we have enough trustworthy, independent, well-classified evidence for the conclusions we are publishing?**

Conceptual contents:

- eligible evidence by level/provider/section/task/source tier;
- observation vs canonical occurrence vs independent count;
- A/B/C evidence mix;
- unresolved-dependency ranges;
- source/provider concentration;
- completeness/QA coverage;
- stale/currentness-uncertain target slices;
- taxonomy/analytic version;
- sparse cells worth sourcing/reviewing next.

This view prevents attractive frequency charts from hiding a weak evidence base.

## 5.2 TELC B1 Target Intelligence Profile

### Product question

**What does current eligible evidence say the App should expect and emphasize for TELC B1?**

Conceptual contents:

- section/task distribution;
- primary skill/reasoning profile;
- vocabulary/grammar tested-dependency and exposure profiles;
- topic mix;
- distractor/reasoning distribution;
- L/R/T/A/P difficulty distributions;
- TELC-vs-generic classification;
- source support/sufficiency and currentness for every prominent conclusion.

This is the main Corpus report feeding target-aware App shaping.

## 5.3 A2 → B1 Progression Map

### Product question

**Which exam-relevant capabilities stay stable, intensify, or emerge as the evidence moves toward B1?**

Conceptual contents:

- matched node/pattern progression classifications;
- prevalence and difficulty changes;
- provider-consistent vs provider-specific changes;
- bridge evidence from mixed A2–B1 material;
- weak/inconclusive cells;
- generation/scaffolding implications.

## 5.4 Provider Comparison Report

### Product question

**What is genuinely TELC-specific versus common across established B1 exams?**

Conceptual contents:

- matched provider distributions by section/task/skill/topic/language/difficulty;
- provider-balanced generic baseline;
- TELC over/under-index patterns;
- coverage/evidence quality per provider;
- explicit source concentration and historical/current target distinctions.

## 5.5 Pattern Relationships / Generation Grounding Report

### Product question

**Which combinations are realistic enough to use as original exercise templates without copying source material?**

Conceptual contents:

- high-support Task ↔ Skill/Reasoning relationships;
- Reasoning ↔ Distractor pairs;
- Topic ↔ Vocabulary/Skill relationships;
- Grammar ↔ Skill tested-dependency relationships;
- supported Task + Skill + Topic or Task + Reasoning + Distractor combinations;
- difficulty envelopes;
- support/concentration/currentness;
- “decision-grade for generation” versus exploratory candidates.

## 5.6 Dashboard/report guardrail

No dashboard may default to a raw “top 20 tags by count” ranking without showing or applying independence, denominator, confidence, scope, and concentration. The report exists to support decisions, not to reward corpus size.

---

## 6. Edge Cases / Failure or Uncertainty Handling

### 6.1 One word repeated 20 times in one passage

Token density shows the repetition. Unit prevalence records one Stimulus occurrence. It does not become 20 independent examples of exam importance.

### 6.2 One passage shared by five Items

Vocabulary/topic/grammar exposure at Stimulus scope counts the passage once. The five Items remain real item-level evidence for their separate response/reasoning patterns.

### 6.3 One publisher contributes thousands of standalone exercises

Those exercises may enrich pattern examples and within-publisher analytics, but they cannot determine provider whole-exam task shares or generic-B1 consensus by volume alone.

### 6.4 A pattern appears once in a verified official TELC source

Corpus may state that the pattern/requirement **exists in trusted TELC evidence**. It must not state that it is frequent or high-priority based on that one occurrence alone.

### 6.5 A source is high confidence but its taxonomy assignment is uncertain

Use the source for structural/provenance conclusions that pass QA, but back off the semantic analytic to a broader confident parent node or withhold the fine-grained result. Strong source confidence does not repair a weak classification.

### 6.6 Many third-party TELC-style mocks agree, but official evidence is sparse

Surface the pattern as a useful target-relevance candidate with bounded confidence. Third-party consensus cannot manufacture an official requirement or a high-confidence target-prevalence claim, and the Stage 07 high-confidence support cap remains active.

### 6.7 Official TELC material is old but no replacement evidence exists

Do not decay authenticity by age. Preserve currentness as unknown/uncertain unless evidence indicates the format changed. Avoid both claiming it is current and automatically discarding it.

### 6.8 A grammar pattern is common but rarely answer-critical

Report high exposure and low tested-dependency prevalence. The App may still ensure recognition, but it should not allocate the same repair priority as a similarly common pattern that repeatedly determines points.

### 6.9 A rare pattern is pass-critical

Frequency does not override scoring/requirement importance. An official target requirement or productive competency can remain mandatory for readiness coverage even if it is encountered only once per full exam.

### 6.10 Same listening script, different voice recordings

Lexical/topic/script frequency counts one inherited script/content family. Acoustic difficulty analytics may count genuinely distinct recording evidence according to Stage 09.

### 6.11 Conflicting answer key

Exclude the disputed Item from distractor/correctness-dependent reasoning analytics. It may still contribute language/topic/task-shape evidence if those aspects independently pass QA.

### 6.12 Mixed A2–B1 exam without item-level level labels

Keep the exam in the mixed slice. Do not force every Item into A2 or B1 merely to make the progression chart complete. Local level estimates can be exploratory until sufficiently validated.

### 6.13 Pattern not observed in TELC slice

Say “not observed in current eligible TELC evidence” and show coverage. Do not infer “TELC does not test this” from corpus absence.

### 6.14 Source removed/taken down

Follow Stage 04’s derived-data disposition. Non-reconstructive aggregate metadata may remain where allowed; if a takedown/legal decision requires purge/recompute, remove the source’s contribution and version/recompute affected analytics.

---

## 7. Relationship to Other Bestehen Stages

### 7.1 Corpus Stage 12 — Contract with Bestehen / App

Stage 12 must define the conceptual interface for retrieving:

- Stage 11 prevalence/distribution results;
- support/sufficiency/confidence/concentration metadata;
- target-vs-generic classifications;
- progression classifications;
- co-occurrence/generation-grounding patterns;
- difficulty/relevance distributions;
- version/currentness information;
- fallback behavior when evidence is insufficient.

Stage 12 should not make App reconstruct confidence, duplicate, or provider-balancing logic from raw Corpus rows.

### 7.2 Corpus Stage 13 — Operations

Operations should expose:

- stale analytics;
- high-impact sparse cells;
- concentrated results;
- unresolved duplicate candidates that materially widen an analytic range;
- taxonomy corrections affecting App-used analytics;
- review targets where resolving uncertainty could change a priority/provider/progression conclusion.

### 7.3 Corpus Stage 14 — Cost, Scale, Automation

Stage 14 should preserve the low-cost assumption that analytics are incremental/offline, cached, and recomputed only when relevant inputs/versions change.

### 7.4 Corpus Stage 16 — Benchmark Corpus

Stage 16 must validate/recalibrate:

- A/B/C aggregate behavior and the Stage 07 caps;
- whether duplicate/derivative treatment produces the intended independent counts;
- semantic taxonomy precision for high-impact analytics;
- provider balancing and scope-fit behavior;
- co-occurrence false discoveries in sparse slices;
- initial sufficiency labels/thresholds;
- comparison/progression stability under representative source sampling.

### 7.5 Bestehen / App

Stage 11 supplies **exam-side evidence priors and target-distribution intelligence**. App remains authoritative for learner mastery, mistakes, session selection, generated exercise delivery/evaluation, mock scoring, readiness, exam-date urgency, and final “what should this learner do now?” decisions.

---

## 8. Cost Notes

### 8.1 Preferred low-cost default

Stage 11 should add **very little recurring cost beyond ingestion/enrichment already required by Stages 06–10**.

Preferred posture:

- compute frequencies, distributions, concentration, conditional prevalence, and co-occurrence deterministically from published structured data;
- reuse existing normalized vocabulary/grammar/taxonomy/difficulty/relevance outputs rather than calling an AI model again for analytics;
- batch and cache analytical snapshots;
- recompute incrementally when source confidence, taxonomy, deduplication, currentness, QA, or source set changes;
- calculate dashboards/reports from the cached analytics rather than from paid model calls;
- use local/open-source/statistical processing where semantic interpretation is not required;
- reserve stronger models/human review for **high-impact ambiguity**: unresolved lineage that changes a priority, disputed semantic mapping, difficult provider-specific comparison, or benchmark review.

### 8.2 What would justify more spend later

Higher-cost analytical modeling is justified only if it demonstrably improves one of:

- high-impact taxonomy/distractor/reasoning precision;
- provider/currentness interpretation that changes target preparation;
- robust co-occurrence/generalization beyond deterministic tags;
- future predictive validation against real learner/exam outcomes.

Even then, the result should be precomputed/batched. There is no product requirement for always-on paid AI inference when a learner opens the App.

### 8.3 Dashboard cost boundary

Stage 11 requires the **information**, not a dedicated BI subscription. A generated Markdown/HTML report, simple internal page, database query view, or notebook can satisfy the personal-project phase. Stage 13/architecture may upgrade the presentation only when maintenance or decision speed justifies it.

---

## 9. Decisions Made

1. Corpus frequency analytics are **denominator-aware prevalence/distribution analytics**, with raw counts retained only as supporting context.
2. Exposure frequency, tested-dependency frequency, and exam-structure prevalence are separate concepts.
3. Vocabulary frequency uses lexical prevalence + token density + independent material spread, excludes ordinary instructions, and counts shared Stimuli once.
4. Grammar analytics separate exposure, tested dependency, and productive demand.
5. Topic frequency is context/task prevalence, not a learner mastery score.
6. Task-type frequency uses representative Exam/Test Set structure for whole-exam proportions; standalone practice remains a separate slice.
7. Skill-frequency analytics keep primary/secondary/supporting roles separate rather than inventing one hidden role multiplier.
8. Provider comparisons are matched, provider-balanced, scope-aware, and show support/concentration.
9. A2→B1 progression compares the same canonical nodes across levels and classifies stable/intensifying/emergent/de-emphasized/provider-specific/inconclusive patterns.
10. TELC-vs-generic B1 uses a TELC target profile plus provider-balanced generic B1 profile; explicit over-index comparisons use a non-TELC established-B1 comparator.
11. Distractor analytics require correctness-ready objective Items and expose both Item prevalence and wrong-option share.
12. Co-occurrence analytics are scope-aware and limited initially to product-useful family combinations; support, conditional prevalence, and lift are retained where meaningful.
13. Corpus outputs influence App through exam-priority priors, generation grounding, and readiness evidence design—not through one opaque “importance” score.
14. Decision-grade aggregate weighting inherits Stage 03/07/09/10 rules, including A/B/C weights, the 15% C-tier cap, the TELC-specific 35% third-party high-confidence support guardrail, duplicate-first counting, currentness, scope fit, and QA.
15. Sparse/concentrated evidence remains visible; absence in Corpus is not treated as proof of absence from the exam.
16. Initial internal views are Corpus Intelligence & Evidence Health, TELC Target Profile, A2→B1 Progression, Provider Comparison, and Pattern Relationships/Generation Grounding.
17. Analytics should be deterministic/offline/cached by default and should not create a per-learner paid-AI cost.

---

## 10. Open Questions / Deferred Decisions

### 10.1 Owner questions

**None.** No Stage 11 product decision requires owner preference or legal-risk input to proceed.

### 10.2 Intentionally deferred architecture/implementation decisions

The following are intentionally left to later architecture/implementation stages because the product behavior above is already defined:

- physical analytics storage/model, query engine, data warehouse, OLAP, graph, or relational representation;
- exact scheduling/incremental-computation mechanism;
- dashboard/BI framework and chart library;
- statistical implementation for uncertainty intervals/significance tests;
- exact lexical normalization library or NLP stack;
- materialized-view/cache layout;
- App API payload/endpoint shape, finalized in Corpus Stage 12.

### 10.3 Deferred empirical calibration

Stage 16/real evidence should calibrate rather than guess:

- additional minimum sample thresholds beyond the inherited two-independent-A/B priority rule;
- whether a numeric source-family dominance cap is useful in addition to concentration labels;
- confidence intervals/error bars for prevalence and provider differences;
- stability thresholds for co-occurrence lift;
- whether Stage 07’s 15% C-tier and 35% third-party TELC-specific support caps should change;
- future empirical relation between Corpus pattern importance and real exam outcomes.

Until calibrated, the conservative rules and qualitative sufficiency labels in this document remain the default.

---

## 11. Definition of Done Check

| Stage 11 checklist requirement | Where resolved | Status |
|---|---|---|
| Define vocabulary-frequency analysis | §4.1 | Done |
| Define grammar-frequency analysis | §4.2 | Done |
| Define topic-frequency analysis | §4.3 | Done |
| Define task-type frequency | §4.4 | Done |
| Define skill-frequency analysis | §4.5 | Done |
| Define provider comparisons | §4.6 | Done |
| Define A2 → B1 progression analysis | §4.7 | Done |
| Define TELC-vs-generic-B1 comparisons | §4.8 | Done |
| Define distractor/reasoning-pattern analysis | §4.9 | Done |
| Define co-occurrence across skills/topics/grammar/tasks | §4.10 | Done |
| Decide which outputs directly influence Bestehen / App | §4.11 | Done |
| Protect aggregate results from low-quality-source distortion | §4.12–4.14 | Done |
| Identify dashboards/reports conceptually | §5 | Done |
| Address recurring-cost impact and cheap default | §8 | Done |

**Stage 11 product-shaping status: Complete.**

The next Corpus stage can define the stable conceptual contract by which Bestehen / App consumes these results without reimplementing trust, deduplication, provider-balancing, or analytical-sufficiency logic.