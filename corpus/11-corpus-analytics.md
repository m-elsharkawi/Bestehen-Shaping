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

---

## 5. Edge Cases / Failure or Uncertainty Handling — Part I

### 5.1 One word repeated 20 times in one passage

Token density should show the repetition. Unit prevalence records one Stimulus occurrence. It does not become 20 independent examples of exam importance.

### 5.2 One passage shared by five Items

Vocabulary/topic/grammar exposure at Stimulus scope counts the passage once. The five Items remain real item-level evidence for their separate response/reasoning patterns.

### 5.3 One publisher contributes thousands of standalone exercises

Those exercises may enrich pattern examples and within-publisher analytics, but they cannot determine provider whole-exam task shares or generic-B1 consensus by volume alone.

### 5.4 A pattern appears once in a verified official TELC source

Corpus may state that the pattern/requirement **exists in trusted TELC evidence**. It must not state that it is frequent or high-priority based on that one occurrence alone.

### 5.5 A source is high confidence but its taxonomy assignment is uncertain

Use the source for structural/provenance conclusions that pass QA, but back off the semantic analytic to a broader confident parent node or withhold the fine-grained result. Strong source confidence does not repair a weak classification.

---

## 6. Relationship to Other Bestehen Stages — Part I

- **Stages 03/07/09/10 are hard prerequisites.** Stage 11 does not redefine trust, relevance, independence, or QA.
- **Stage 12 (Corpus → App contract)** must expose the Stage 11 result semantics and downstream eligibility without forcing App to reconstruct weighting logic.
- **Stage 13 (Corpus Operations)** should surface evidence concentration, sparse slices, analytic freshness, and review/recompute needs.
- **Stage 14 (Cost/Scale)** should preserve offline/batched aggregation and avoid per-learner recomputation.
- **Stage 16 (Benchmark Corpus)** must validate thresholds, deduplication effects, semantic tagging accuracy, and whether starting safety caps produce sensible aggregate behavior.
- **App daily coaching, content strategy, and readiness stages** consume these analytics as priors/evidence-design inputs; learner personalization remains in App.

The remaining Stage 11 decisions—A2→B1 progression, TELC-vs-generic comparison semantics, distractor/reasoning analysis, co-occurrence, App influence boundaries, aggregate safeguards, dashboards/reports, cost notes, and Definition of Done—are completed in the next section of this same document.