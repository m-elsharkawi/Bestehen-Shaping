# Bestehen / App — Stage 24: Analytics and Product Success Metrics

> **Status:** Authoritative Stage 24 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Success promise:** Measure whether Bestehen creates stronger, more trustworthy evidence of TELC B1 pass readiness — and eventually whether that evidence predicts the real exam — without turning usage, retention, or analytics volume into the product goal.

## 1. Purpose and Scope

This document defines how Bestehen / App decides whether the product is actually working.

The central product question is not **“Are learners spending time in the App?”** It is:

> **Does Bestehen help a learner become demonstrably more capable of passing TELC B1, and are its readiness claims becoming trustworthy enough to act on?**

Earlier stages already define a rich evidence model: direct attempts, task-family results, assistance, timing, playback, content quality, evaluator confidence, mistake recurrence, delayed transfer, progression toward target conditions, separate Written/Oral readiness, mocks, and Ready-to-Book gates. Stage 24 therefore does not need a second analytics universe. It defines the smallest outcome-oriented measurement layer needed to aggregate those existing facts, detect product-quality failures, calibrate the readiness model, and control cost.

This stage defines:

- the launch north-star metric;
- learner-outcome metrics;
- readiness-accuracy and calibration metrics before and after real exam outcomes exist;
- skill-improvement, repair, delayed-transfer, and independence metrics;
- session-value metrics that do not reward time-on-screen;
- content-quality and evaluation-consistency metrics;
- mock-to-real-exam comparison;
- optional real-exam result collection and how those outcomes may be used for calibration;
- a lean initial analytics set suitable for a personal project;
- which engagement/growth analytics can wait;
- cost and privacy guardrails;
- the account, retention, export, deletion, sync, offline, and AI-data expectations required by the current live Stage 24 checklist.

This is product shaping, not analytics architecture. It does **not** choose an analytics vendor, event bus, warehouse, dashboard product, statistical library, auth provider, database, storage format, model vendor, or observability stack.

### Core decision

**Bestehen launches with an outcome hierarchy, not an engagement hierarchy.**

1. The **north star** is reaching **decision-grade Safe Readiness** in both pass components.
2. The strongest eventual validation is **real TELC outcome accuracy**, especially whether learners whom Bestehen considered Ready to Book actually pass both components.
3. Learning metrics explain *how* readiness improves: fresh transfer, delayed retention, decreasing assistance, stronger target-condition performance, and repaired weaknesses.
4. Session, retention, and usage metrics are diagnostic support metrics only.
5. Analytics may evaluate the readiness model, but analytics never create a second learner-facing readiness score.

---

## 2. Inputs / Existing Decisions

Stage 24 preserves the shared Product Overview, shared Identity, and App Stages 01–23.

### 2.1 Product-success hierarchy already exists

Stage 01 already establishes that product success should be judged in this order:

- real exam outcome when available;
- readiness calibration;
- written/oral pass safety;
- repair transfer;
- retention/stability;
- increasing realism and independence;
- efficient use of study time;
- adequate evidence coverage.

Streaks, session completion, DAU, time in app, and content consumption are explicitly secondary.

Stage 24 turns that hierarchy into named metrics and measurement rules.

### 2.2 The learner model is the primary measurement source

Stage 04 already requires an evidence ledger that preserves:

- task/skill and direct-evidence lane;
- served difficulty and target mapping;
- result/rubric dimensions;
- assistance and reference use;
- open, practice-timed, or exam-timed conditions;
- playback conditions where relevant;
- evaluator method, version, confidence, and quality;
- content quality and technical validity;
- timestamps, distinct attempts/occasions, and provenance.

Stage 24 should aggregate these facts rather than add click-by-click surveillance merely because an analytics SDK makes that easy.

### 2.3 Learning evidence and readiness evidence remain different

Stages 04, 08, 14, and 15 establish that:

- assisted or lower-difficulty success can show real learning while contributing less or nothing to the target-performance estimate;
- immediate retry success is weaker than delayed fresh transfer;
- direct evidence is lane-specific;
- P3/P4 evidence is stronger for current TELC readiness than supported Foundation/Bridge activity;
- missing evidence is unknown, not zero;
- technical/content/evaluator invalidation is not learner failure.

Metrics must preserve those distinctions instead of averaging everything into “accuracy” or “completion.”

### 2.4 Readiness has one existing definition

Stage 15 is authoritative:

- Written and Oral are estimated separately;
- each current TELC B1 pass gate is 60%;
- the launch **Readiness Index = min(Written target %, Oral target %)**;
- the index is **not a pass probability**;
- Safe pass range requires an estimated component performance of at least 65/100, the planning-range lower bound at or above 60, decision-grade evidence, at least Medium confidence, and no unresolved pass-critical blocker;
- pass probability is deliberately withheld until matched real-exam outcomes can support empirical calibration.

Stage 24 evaluates that model. It does not replace it.

### 2.5 Ready to Book is a consequential action gate

Stage 17 requires both components to be Safe plus current decision-grade evidence, a clean passing full mock within 14 days, independent component confirmation within 30 days, at least Medium confidence, and no pass-critical contradiction.

Ready-to-Book therefore becomes an important **lagging product outcome and future real-world validation cohort**, but it is not a second readiness score.

### 2.6 Repair and review already define retained-learning evidence

Stages 05, 07, and 14 distinguish:

- same-session fresh Retry;
- early delayed transfer in 1–3 days;
- consolidation around 7 days;
- broader transfer around 21 days;
- later stability around 60 days;
- re-diagnosis after repeated failure;
- natural valid practice satisfying review when it directly tests the capability.

Analytics must not report same-session Retry as though it proved durable learning.

### 2.7 Content and productive evaluation are measurement instruments

Stages 12, 13, and 21 establish that:

- Writing and Speaking evaluation are TELC-aligned estimates, not official grades;
- evaluator version and confidence matter;
- content errors, ambiguity, broken media, poor transcription, or evaluator failure invalidate learner conclusions;
- content has approval levels, with readiness/P4 forms requiring the strongest review;
- objective Reading, Language Elements, and Listening scoring should normally be deterministic;
- stronger AI or human review is reserved for higher-stakes uncertainty.

Quality analytics therefore belong to the product-outcome system rather than being merely operational logs.

### 2.8 Stage-numbering reconciliation

The live `Bestehen_App_Product_Shaping_Checklist.md` currently names Stage 24 **“Define Account, Data, and Portability Expectations”**, while the Stage 24 agent prompt governing this document is **“Define Analytics and Product Success Metrics.”** The live checklist currently places Product Analytics and Evaluation at Stage 26.

This is the same kind of continuity mismatch already resolved in Stages 22 and 23. Stage 24 therefore covers **both**:

1. Analytics and Product Success Metrics — the primary objective of this stage prompt; and
2. Account, Data, and Portability Expectations — every checkbox in the current live Stage 24 checklist.

This document does not create a second analytics model for a later stage. Any later analytics/evaluation checklist work should treat this document as the Stage 24 product baseline and refine measurement implementation or empirical thresholds without inventing conflicting success definitions.

---

## 3. Decisions and Rationale

## 3.1 North Star: Decision-Grade Safe Readiness Attainment

**Decision:** Bestehen's launch north-star metric is **Decision-Grade Safe Readiness Attainment (DSRA)**.

### Definition

For a learner who has established a usable baseline, DSRA is achieved when:

- **Written = Safe pass range** under Stage 15;
- **Oral = Safe pass range** under Stage 15;
- both components still satisfy Stage 15 decision-grade evidence requirements;
- the target blueprint is current;
- the state is supported by valid direct evidence rather than inferred from activity volume.

For a multi-learner product, the north-star rate is:

> **Learners reaching DSRA during a preparation episode ÷ learners who established a baseline and began below DSRA during that episode.**

For the initial personal-project phase, a cohort percentage is not useful. The same north star is observed as:

- DSRA **not yet reached / reached**;
- date first reached;
- time and useful study effort from baseline to first attainment;
- whether the state remains supported by fresh evidence afterward.

### Why DSRA instead of Ready to Book

Ready to Book adds deliberate consistency and whole-exam rehearsal requirements appropriate to a consequential booking recommendation. Those requirements are important, but they partly measure **decision confidence and rehearsal logistics** after the learner is already safely performing in both components.

DSRA is the cleaner learning outcome: **has the product moved both pass components into an evidence-defensible safe range?** Ready-to-Book attainment remains a major secondary outcome.

### Why DSRA instead of real-exam pass rate at launch

Real TELC pass outcomes are the strongest validation, but they are delayed, sparse, optional, and selection-biased. A learner may study for months without taking the exam, may take it without reporting the result, or may book outside Bestehen's recommendation.

Real outcomes therefore become the ultimate validation layer as data accumulates; they are not a practical launch north star.

### North-star guardrail

DSRA may never be optimized by loosening the readiness model merely to make the number rise. Changes to readiness thresholds, evidence requirements, evaluator behavior, or planning ranges require independent calibration evidence and versioned review.

---

## 3.2 Ultimate validation: real TELC outcomes

**Decision:** Once enough voluntary real-exam outcomes exist, the strongest product validation is whether **pre-exam Bestehen states predict the real written and oral outcomes**.

The most important future safety metric is:

> **Real-exam pass rate among learners whose last valid pre-exam state was Ready to Book.**

This metric is always accompanied by:

- Written pass rate;
- Oral pass rate;
- count of matched outcomes;
- source confidence of the outcome data;
- the readiness/evaluator/blueprint version used before the exam.

A high overall pass rate that hides repeated Oral failures is not acceptable because the target has independent pass gates.

A reported failure after a Ready-to-Book recommendation is a **high-severity calibration case** that should be reviewed even when the aggregate rate still looks healthy. It may reveal score bias, weak content calibration, an evaluator problem, insufficient realism, a recency issue, or ordinary real-exam variance.

---

## 3.3 Use a metric hierarchy, not one dashboard score

The product uses five measurement layers:

| Layer | Main question | Examples | Optimization status |
|---|---|---|---|
| **1 — Outcome** | Did the learner become safely more likely to pass? | DSRA, Ready-to-Book attainment, real pass result | Primary |
| **2 — Readiness validity** | Are Bestehen's readiness claims trustworthy? | forward mock error, planning-range coverage, pass-gate agreement | Primary quality guardrail |
| **3 — Learning mechanism** | Are repairs and practice creating transferable, retained capability? | fresh transfer, delayed retention, independence gain, target-condition progression | Primary explanatory metrics |
| **4 — Delivery quality** | Are sessions, content, and evaluators producing valid useful evidence? | useful-session outcome, invalidation, content defects, evaluator consistency | Supporting quality metrics |
| **5 — Engagement/operations** | Can the learner access and continue preparation reliably and affordably? | return rate, session start/completion, notification response, cost | Diagnostic only |

A metric from a lower layer may explain a higher-layer problem. It may not silently replace the higher-layer objective.

---

## 4. Measurement Rules That Apply to Every Metric

## 4.1 Use independent evidence episodes, not clicks

One response can contain many scored decisions or rubric dimensions. One mock can contain many items. Repeated clicks inside one repair chain are correlated.

For learning and confidence metrics, Bestehen therefore uses the same independent-attempt/episode semantics already defined by Stages 04, 05, and 15. It must not create an apparent sample of 100 independent observations from ten items inside one repeated task.

## 4.2 Exclude invalid learner evidence

Technical failure, ambiguous content, broken audio, unsupported answer keys, evaluator failure, or other non-learner invalidation has **zero learner-outcome effect**.

Those events still matter as **delivery-quality incidents**. They must appear in content/evaluator/technical quality metrics rather than lowering the learner's skill result.

## 4.3 Compare like with like

Skill improvement is meaningful only when the compared evidence is similar enough in:

- task family;
- progression rung / difficulty;
- direct-evidence lane;
- assistance;
- timing/playback/reference condition;
- content approval/quality;
- evaluator version and reliability.

If conditions materially strengthen — for example, assisted → unassisted or open → target-timed — stable performance may itself be improvement even when raw percentage is unchanged.

## 4.4 Preserve Written and Oral separately

Every readiness and real-outcome metric is reported separately for Written and Oral before any combined view.

The weaker component is not allowed to disappear inside a total-score average.

## 4.5 Freeze prediction snapshots for validation

When Bestehen later validates a readiness prediction against a future mock or real exam, the prediction snapshot must be the state **before** that validating result entered the learner model.

The validating result may update readiness afterward, but it cannot be used both to produce and to validate the same prediction.

## 4.6 Always show raw counts with small samples

At personal-project and early-user scale, percentages can be misleading. Internal reports should pair any rate with the number of learners, attempts, forms, or matched outcomes behind it.

No learner-facing claim such as “90% of Ready learners pass” is allowed from a tiny or convenience-selected sample.

## 4.7 Version the interpretation, not just the data

Outcome analysis must preserve the relevant:

- TELC target blueprint version;
- readiness model version;
- content/form version;
- Writing/Speaking evaluator version;
- material scoring/calibration version.

A later calibration change should not rewrite history so that old predictions look better than what the learner actually saw at the time.

---

## 5. Metric Catalog

## 5.1 Learner-outcome metrics

| Metric | Definition | Why it matters | Guardrail |
|---|---|---|---|
| **Decision-Grade Safe Readiness Attainment (DSRA)** | Both Written and Oral reach current Stage 15 Safe pass range with decision-grade evidence | Launch north star; closest available proxy for “prepared to pass” before real outcomes are abundant | Never loosen readiness to increase attainment |
| **Ready-to-Book attainment** | Learner satisfies all Stage 17 gates | Measures whether safe performance becomes current and consistent enough for a consequential booking recommendation | Not a separate score; requires Stage 17 evidence exactly |
| **Time to DSRA** | Calendar time from usable baseline to first DSRA | Helps understand preparation pace and scheduling | Descriptive; influenced by learner availability |
| **Useful study effort to DSRA** | Approximate purposeful session/attempt time from baseline to DSRA | Measures efficiency better than raw app time | Do not optimize by skipping necessary evidence or difficult skills |
| **Sustained Safe Readiness** | DSRA remains supported when new current evidence arrives rather than immediately collapsing | Distinguishes a stable state from one favorable measurement | Aging alone is reported as evidence staleness, not ability loss |
| **Written bottleneck resolution** | Previously limiting Written component/section moves into Safe current evidence | Shows whether the coach repairs pass-critical written risk | Oral still required independently |
| **Oral bottleneck resolution** | Previously limiting Oral component moves into Safe current evidence | Protects the independent oral gate | Cannot be inferred from typed/monologue-only evidence |
| **Real exam pass outcome** | Voluntarily reported real TELC overall, Written, and Oral result | Ultimate outcome validation | Self-report confidence and selection bias remain visible |

### Interpretation rule

A learner can make meaningful progress without immediately moving DSRA. Capability/evidence metrics below explain that progress. The App must not create a second motivational score merely because the north star is intentionally slow-moving.

---

## 5.2 Readiness-accuracy and calibration metrics

Before enough real exam outcomes exist, Bestehen uses **forward validation against future independent clean P4 evidence**.

### Pre-real-outcome metrics

| Metric | Definition | Why it matters |
|---|---|---|
| **Forward component error** | Absolute difference between a frozen Written/Oral target-performance estimate and the next independent clean P4 component/full-mock result | Tests whether the estimate predicts genuinely new target-condition evidence rather than merely summarizes history |
| **Signed component bias** | Future clean P4 result minus frozen estimate | Detects systematic optimism or pessimism |
| **Planning-range coverage** | Share of future clean P4 component results that fall inside the previously shown planning range | Tests whether uncertainty ranges are honest |
| **Safe-range forward pass rate** | Among frozen component states labelled Safe, share of next independent clean P4 results that clear that component's 60% gate | Early safety check for the Safe label |
| **Band-to-future-result agreement** | Distribution of future clean P4 results for Not ready, Borderline, and Safe states | Checks whether bands order risk meaningfully |
| **Confidence validity** | Prediction error and contradiction rate by Low/Medium/High evidence confidence | High confidence should be more stable and accurate than low confidence |
| **Bottleneck agreement** | Whether the component predicted as weaker is also the weaker component in the next clean whole-exam measurement | Validates the product's bottleneck framing |
| **Readiness reversal reason rate** | Material readiness reversals categorized as new weaker evidence, aging, evaluator correction, blueprint change, or unexplained | Detects model instability and makes unexplained volatility visible |

### No circular validation

A full mock already included in the current readiness estimate may not be used to claim that the estimate accurately predicted that same mock. Forward validation requires a later independent form/occasion.

### Real-outcome calibration metrics

Once real outcomes exist, add:

- predicted Written estimate/range versus real Written score or pass status;
- predicted Oral estimate/range versus real Oral score or pass status;
- Ready-to-Book versus real overall pass/fail;
- false-ready cases: Ready to Book before exam, but at least one real component fails;
- opportunistic false-not-ready cases: learner took and passed despite not being Ready to Book;
- planning-range coverage against real component scores when numeric scores are supplied;
- signed bias and absolute error by component;
- calibration by readiness band and confidence;
- later, only after adequate matched outcomes, calibration of any proposed pass-probability output.

### Pass probability remains deferred

Stage 15's decision remains unchanged: Bestehen does not show a pass probability merely because a regression/model can produce one. A pass-probability feature becomes eligible only after out-of-sample matched real outcomes show sufficiently stable calibration across both Written and Oral risk ranges. The exact statistical sample threshold should be set from the eventual validation design and uncertainty, not guessed now.

---

## 5.3 Skill-improvement and repair-success metrics

Raw task accuracy alone is insufficient because the product intentionally changes difficulty and assistance.

| Metric | Definition | Why it matters |
|---|---|---|
| **Fresh-transfer success** | After a repair, learner succeeds on fresh equivalent content in the same direct-evidence lane without seeing the answer | Shows the repair changed behavior beyond the exposed item |
| **Early delayed-transfer rate** | R1 checks passed 1–3 days after repair | First retained-learning signal |
| **Consolidation retention rate** | R2 checks passed around 7 days | Distinguishes durable learning from same-session responsiveness |
| **Broader-transfer rate** | R3 checks passed around 21 days across new context/task variation | Tests generalization |
| **Stability/resolution rate** | R4 checks passed around 60 days when applicable | Tests longer retention for high-value weaknesses |
| **Reopen rate** | Previously repaired/resolved weakness reappears under valid fresh evidence | Reveals fragile repair or insufficient transfer |
| **Assistance-reduction success** | Performance stays functional/reliable when answer-bearing support is reduced | Core A1→B1 progression signal |
| **Target-condition conversion** | Task family moves from useful P3 evidence to valid P4 success without support/timing violations | Measures transition from learning to exam-relevant execution |
| **Comparable performance change** | Change across fresh comparable attempts at similar condition/difficulty | Direct skill gain when comparison is fair |
| **Condition-strength gain** | Same or better performance under materially stronger condition | Captures improvement hidden by flat raw score |
| **Repeated-failure re-diagnosis yield** | After review failure triggers re-diagnosis, a changed intervention produces later fresh improvement | Tests whether the coach adapts rather than drilling blindly |

### Immediate retry is reported separately

Same-session fresh Retry can be tracked as **repair responsiveness**, but it must never be combined with delayed-transfer rates as though they are equivalent.

A product that drives 95% immediate Retry success but poor 7-day retention is not succeeding at learning.

---

## 5.4 Session metrics

Sessions are judged by the coaching outcome they create, not how long the learner stays in the App.

### Primary session metric: Useful Session Outcome Rate

A session has a **useful outcome** when it reaches a meaningful boundary and accomplishes at least one planned coaching purpose, such as:

- obtains valid decision-relevant evidence;
- completes a due delayed-transfer/retention check;
- completes a narrow repair plus fresh transfer;
- resolves a high-impact diagnosis uncertainty;
- moves a task family to less assistance or stronger realism;
- completes a valid maintenance/coverage check that was actually due;
- completes a measured mock scope whose result answers the intended readiness question.

A partial session can count when it completed such a boundary. A long session that only produced invalid evidence does not.

### Supporting session metrics

| Metric | Use |
|---|---|
| **Dominant commitment completion** | Did the planned main coaching commitment reach its meaningful stop boundary? |
| **Planned-vs-actual duration fit** | Detects whether 10/25/45-minute plans are consistently unrealistic; not a performance score |
| **Invalid-session evidence rate** | Share of sessions materially affected by technical/content/evaluator failure |
| **Interruption/resume success** | Whether resumable ordinary work preserves completed evidence without duplicate counting |
| **Override rate** | Descriptive signal of how often learners choose another useful path; high/low is not inherently good |
| **Recommendation acceptance** | Helps detect whether recommendations are understandable/relevant; not a product north star |
| **Early-stop reason mix** | Time constraint, fatigue, technical failure, task difficulty, learner choice, etc.; used to fix delivery problems |

### Engagement anti-patterns

Do not optimize:

- session length;
- number of questions answered;
- screen count;
- daily opens;
- completion at any cost;
- easy-task acceptance.

If a harder 20-minute Speaking session is more useful than 40 minutes of comfortable Reading, the analytics system must not reward the opposite product choice.

---

## 5.5 Retention and habit metrics are separate from learning metrics

Retention can help identify whether the experience is usable and whether reminders support preparation, but it does not prove learning.

Allowed operational metrics include:

- learner returns for another useful preparation opportunity within 7/30 days;
- learner resumes after a long absence;
- scheduled study commitment attempted/completed;
- reminder opened/actioned/ignored;
- notification opt-out/mute rate;
- weekly preparation days or useful commitments.

These metrics must live in a separate reporting group from DSRA, readiness accuracy, and learning transfer.

A retention experiment is invalid if it improves return rate by shifting the learner toward easier, lower-value work or manipulative notification pressure.

---

## 5.6 Content-quality metrics

Content is part of the measurement instrument, so quality failures are first-class product failures.

| Metric | Definition / use |
|---|---|
| **Serve-time validity rate** | Share of served content that remains valid for its declared approval/evidence role |
| **Content invalidation rate** | Served attempts later invalidated because of ambiguity, wrong key, broken media, rights state, target mismatch, or material content defect |
| **Quarantine/rejection rate** | Draft/generated candidates rejected before learner use; useful for improving generation/QA without penalizing learners |
| **Answer/rubric correction rate** | Approved content whose answer key, content-point contract, or rubric interpretation required later correction |
| **Difficulty residual** | Intended rung/difficulty versus observed comparable learner performance after enough data; used to detect systematically miscalibrated forms |
| **Target-form health** | P4/readiness forms with current blueprint, valid calibration/review, no known defect, and adequate independent form supply |
| **Freshness collision rate** | Attempts that accidentally reuse exposed/near-duplicate content where fresh evidence was required |
| **Content-family concentration** | Detects overuse of one topic, form, voice, scenario, or template that can inflate familiarity |
| **Learner-reported content issue rate** | Direct quality feedback; high-impact reports trigger review/quarantine rather than automatic learner penalty |
| **Audio validity rate** | Listening/Speaking assets with working playback/recording and expected voice/speed/quality conditions |

### Difficulty analytics guardrail

Observed performance may help calibrate difficulty only after controlling for learner state and evidence condition. A low score from weak learners does not prove an item is too hard; a high score from already-strong learners does not prove it is too easy.

### Quality response rule

A confirmed content defect must:

1. quarantine/retire the affected content for the relevant use;
2. repair or exclude affected learner evidence where material;
3. recompute readiness if that evidence influenced a current claim;
4. explain any material learner-facing change through the normal evidence-change language.

---

## 5.7 Writing and Speaking evaluation-consistency metrics

Productive evaluation is the largest measurement-quality risk because it cannot rely on one fixed answer key.

### Required evaluator QA dimensions

| Metric | Definition / use |
|---|---|
| **Same-response repeatability** | A fixed response evaluated repeatedly by the same evaluator version should produce materially stable official-aligned bands/points and coaching diagnosis |
| **Benchmark agreement** | Evaluator output compared with a curated human-reviewed benchmark set across TELC criteria/parts |
| **Pass-gate flip rate** | Frequency with which evaluator disagreement would change whether a component/attempt is above or below a consequential pass boundary; highest-severity disagreement |
| **Criterion/part agreement** | Writing Criteria I/II/III and Speaking parts/official criteria tracked separately so one strong dimension cannot hide a weak evaluator area |
| **Evaluator-version drift** | Fixed benchmark responses compared before/after an evaluator change |
| **Escalation rate** | Share of productive responses whose uncertainty/contradiction triggers the stronger evaluation path |
| **Correction/reversal rate** | Standard evaluator result later materially changed by stronger/human review |
| **Confidence validity** | High-confidence evaluations should disagree/reverse less often than low-confidence evaluations |
| **Speaking technical invalidation** | Audio/transcription/partner failures that prevent responsible scoring rather than becoming poor learner performance |

### Benchmark-set decision

Bestehen should maintain a small, deliberately varied **gold benchmark set** of Writing and Speaking responses spanning likely rubric bands, common error patterns, stronger/weaker accents and intelligibility conditions, and technically challenging but valid samples.

The benchmark is run when an evaluator materially changes, not on every learner response.

### Fairness without unnecessary demographic collection

The personal-project launch does not collect race, ethnicity, nationality, gender, or other sensitive demographics merely to build evaluator dashboards. Speaking fairness should first be tested with intentionally varied benchmark voices/accents and intelligibility levels.

If the product later has enough users to support responsible group-level bias analysis, the legal/privacy basis and collection design must be shaped explicitly before collecting sensitive attributes.

---

## 5.8 Cost metrics

Cost is a product constraint because unnecessary premium calls can distort what the coach chooses to practice.

Track at minimum:

- **cost per active learner / preparation episode**;
- **cost per completed session**;
- **cost per valid Writing evaluation**;
- **cost per valid Speaking evaluation/interactive session**;
- **cost per full mock**;
- **cost per decision-grade productive evidence occasion**;
- premium escalation rate and cost;
- generated-audio/content generation cost as amortized/batch cost where useful rather than pretending every playback is a fresh generation.

The product should prefer a cheaper design when learning/evaluation quality is equivalent. It must not avoid necessary productive practice merely because objective Reading is cheaper.

---

## 6. Mock-to-Real-Exam Correlation

## 6.1 Primary matched comparison

When real outcome data exists, the primary mock-to-real comparison uses the **latest clean full target-condition mock before the real exam**, provided that:

- it used the same applicable TELC blueprint;
- it used fresh content and valid target conditions;
- productive evaluation was trustworthy;
- it occurred close enough to the exam to be relevant; the initial reporting window is **within 30 days**;
- the real result belongs to the same learner and exam attempt.

Older/full mocks may still support secondary analysis, but the latest clean current mock is the most actionable comparison.

## 6.2 Report more than correlation

Correlation alone can look good while scores are systematically biased. Report:

1. **Written score error** — normalized mock Written versus real Written when numeric result exists;
2. **Oral score error** — normalized mock Oral versus real Oral;
3. **signed bias** — does Bestehen systematically over- or under-predict?;
4. **mean/median absolute error**;
5. **rank correlation** — whether stronger mock performers tend to be stronger real performers once sample size makes this meaningful;
6. **component pass/fail agreement**;
7. **overall gate agreement** — whether both mock and real exam pass/fail states agree after respecting separate components;
8. **planning-range coverage** — whether the real component score falls inside the pre-exam range shown by Bestehen;
9. **Ready-to-Book agreement** — whether a Ready recommendation is followed by real pass.

### Stratification when sample size permits

Inspect by:

- days between mock and exam;
- readiness/evidence confidence;
- evaluator version;
- content form/approval class;
- Writing/Speaking evaluation confidence;
- whether the learner was already booked/under deadline pressure;
- material accessibility/condition differences where known.

Do not slice tiny samples into dozens of misleading segments.

## 6.3 Calibration consequence

Mock-to-real evidence may later adjust:

- planning-range width;
- readiness confidence mapping;
- evaluator calibration;
- the relative interpretation of specific P4 evidence;
- future pass-probability calibration if ever enabled.

It does **not** justify changing official TELC point weights or independent pass gates.

---

## 7. Optional Real Exam Result Collection

## 7.1 Collection is voluntary and skippable

After the learner marks the exam completed and later returns to the result-pending state, Bestehen may ask:

> **Want to add your result? It helps calibrate how well Bestehen predicts the real exam.**

The learner can skip, dismiss permanently, or return later. Result entry is not required to retain progress history or close the goal.

## 7.2 Minimum result fields

Recommended launch collection:

- exam date;
- overall pass / not pass / result not known;
- Written pass/fail if known;
- Oral pass/fail if known;
- optional numeric Written score/points if available;
- optional numeric Oral score/points if available;
- optional note that the score format differs or only partial information is known.

The App derives the learner's last pre-exam readiness/Ready-to-Book state from its own frozen history; it should not ask the learner to remember that state.

### Do not collect by default

The launch flow does not need:

- candidate/registration number;
- date of birth;
- home address;
- passport/ID data;
- examiner names;
- certificate serial number;
- exam-center details unless a later calibration question genuinely requires them;
- certificate upload.

Avoiding certificate upload removes a large privacy/storage burden for little early calibration value.

## 7.3 Outcome confidence

At launch, outcomes are **self-reported** and must be labelled as such internally. Self-report is still useful, especially for pass/fail and component results, but selection/reporting bias must remain visible.

A future verified-result tier is optional, not required for the personal-project phase. If verification is ever introduced, it needs separate privacy/legal shaping before collecting documents.

## 7.4 Use of real outcomes

A reported result may be used to:

- validate past readiness predictions;
- evaluate Ready-to-Book precision;
- evaluate mock-to-real bias;
- calibrate future planning ranges/confidence;
- compare evaluator versions offline;
- identify recurring false-ready root causes.

It must **not**:

- retroactively change what the learner actually demonstrated in old attempts;
- silently rewrite historical predictions;
- become training data for a third-party general-purpose model without separate explicit consent;
- be required for core coaching.

The learner can delete the reported result under the same personal-data deletion contract as other learner data.

---

## 8. Lean Initial Analytics Set for a Personal Project

## 8.1 What must exist from the first usable product

Bestehen can start with a very small analytics layer because most required data is already product evidence.

### A. Evidence observations

Keep the Stage 04 evidence contract:

- task family/skill/lane;
- progression/difficulty and target blueprint;
- result/rubric;
- assistance/timing/playback/reference condition;
- validity/content quality;
- evaluator method/version/confidence;
- independent attempt/session/date provenance.

This is core product state, not optional analytics telemetry.

### B. Material readiness snapshots

Record a versioned snapshot when readiness is first established or materially changes:

- Written estimate/range/band/confidence;
- Oral estimate/range/band/confidence;
- overall Readiness Index/band when allowed;
- evidence sufficiency/coverage;
- primary blocker;
- Ready-to-Book gate state when relevant;
- model/blueprint versions.

There is no need to persist every render or every tiny recomputation if the state did not materially change.

### C. Repair/review lifecycle summaries

Record:

- candidate/known weakness;
- repair occurred;
- immediate fresh Retry result;
- delayed R1/R2/R3/R4 outcomes when applicable;
- resolved/reopened state;
- cause/evaluation confidence.

### D. Session summary

At one session-level boundary, record:

- planned purpose and dominant commitment;
- planned duration bucket;
- meaningful completion state;
- useful outcome type;
- override/early-stop reason when known;
- technical/content/evaluation invalidation if present.

No full clickstream is required.

### E. Mock summary

Record scope, target validity, component scores/ranges, pass-gate results where applicable, form/blueprint/evaluator versions, and whether the measured block remained clean.

### F. Content/evaluator quality incidents

Record quarantine/invalidation/correction and productive-evaluator escalations/reversals.

### G. Cost summary

Record aggregated model/speech/audio-generation spend by session or high-cost product action so cost can be compared with evidence value.

### H. Optional real exam outcome

Use the voluntary result contract in Section 7.

## 8.2 What can wait

The personal-project launch does **not** need:

- a commercial product-analytics suite;
- a real-time analytics warehouse;
- raw screen/session replay;
- heatmaps;
- every button click;
- elaborate acquisition funnels;
- referral/virality metrics;
- feature-adoption scorecards for dozens of screens;
- sophisticated retention cohorting;
- experimentation infrastructure for growth A/B tests;
- automated causal inference;
- item-response-theory/psychometric infrastructure;
- always-on AI judging analytics anomalies;
- per-user LLM-generated analytics summaries;
- pass probability;
- demographic segmentation collected without a clear product need.

A simple local/low-cost reporting process over structured product data is sufficient until usage volume creates a real need for more infrastructure.

---

## 9. Account, Data, and Portability Expectations

This section resolves every requirement in the current live Stage 24 checklist.

## 9.1 Sign-in is not required initially

**Decision:** Core first-use coaching must not require sign-in.

A learner should be able to:

- configure the TELC B1 goal;
- begin/complete the diagnostic;
- receive a first plan;
- use the initial single-device product

without creating an account.

Sign-in becomes justified when the learner explicitly wants capabilities that require identity continuity, primarily **cross-device sync and recovery**.

For the personal-project MVP, a single-device/local-first experience is acceptable. If local data can be lost because the learner has not enabled recovery/sync, the product should state that plainly rather than surprise them later.

An account wall before the learner experiences the coach would conflict with the Stage 02 journey.

## 9.2 Learner profile data

The minimum useful learner profile contains only information with a clear coaching purpose:

### Learner-provided

- TELC B1 target at launch;
- exam status: no date, target month, planned date, or booked date;
- date/window when supplied;
- normal available study time/session preference;
- preferred explanation language;
- relevant accessibility/equipment preferences;
- notification/study-schedule preferences if habit support is enabled;
- optional display name.

### Product-derived

- evidence history and learner-model state;
- capability/mastery/confidence/freshness summaries;
- mistake/repair/review state;
- progression/assistance dependence;
- readiness history;
- mock history;
- current coach priority;
- reported real-exam result if voluntarily supplied.

### Not collected merely for profiling

Do not require age, gender, nationality, precise location, occupation, income, or other demographic attributes unless a future feature has a defined product/legal reason.

Self-reported proficiency can route initial content but remains context, not performance evidence.

## 9.3 Progress/evidence history retention

**Decision:** Structured learner progress and evidence history is retained for the lifetime of the active TELC B1 goal and afterward as history until the learner deletes it or explicitly starts over in a way that removes the history.

Why retain it:

- Readiness must remain explainable;
- old evidence may become historical-only without disappearing;
- weakness recurrence and repair require history;
- evaluator/calibration corrections may require reinterpreting earlier evidence;
- progress/milestones depend on historical state.

Time changes **freshness and readiness contribution**, not whether history existed.

The App should not retain duplicate raw telemetry that adds no learner/coaching value merely because storage is cheap.

## 9.4 Raw Writing and Speaking data

### Writing

Learner-authored Writing text may be retained with the evidence history because it supports:

- learner review of past work;
- explanation of evaluator results;
- re-evaluation after a correction/model change when needed;
- proof of what the learner actually produced.

It is deleted under the learner-data deletion contract.

### Speaking raw audio

**Decision:** Raw microphone audio is **ephemeral by default**.

Normal behavior:

1. capture only what is required for the speaking attempt;
2. use it for transcription/evaluation and any immediate justified escalation;
3. preserve structured evaluation, condition, transcript where useful, and evidence metadata;
4. delete the raw recording after evaluation is finalized.

If evaluation is pending because of a technical/evaluator problem, raw audio may be retained temporarily to resolve that attempt, with an initial product ceiling of **7 days** before it is deleted or the attempt is marked unresolved/invalid.

A future “keep my recordings” feature may be an explicit learner opt-in. Permanent raw-audio retention is not required at launch and would add privacy/storage cost without improving the core coaching loop enough to justify it.

## 9.5 Generated-content retention

**Decision:** Reusable App content is retained/versioned according to its content role, not regenerated for every attempt.

- approved generated/original practice can be cached and reused across learners while per-learner freshness rules prevent memorization;
- readiness/P4 forms keep stable versions and QA provenance;
- if a learner evidence record depends on a particular prompt/form, the exact content/version needed to reproduce the evidence interpretation remains referenceable;
- adaptive ephemeral partner turns/repairs may be retained only to the extent necessary to explain the learner attempt;
- generated content should not embed unnecessary personal profile information.

Rights-restricted Corpus/reference assets keep their separate rights rules and are not automatically included in learner exports.

## 9.6 Export needs

**Decision:** Learners should ultimately be able to take their personal learning record out of Bestehen.

The export contract should include, in a common human-readable and/or structured form:

- goal/date context;
- readiness history and confidence;
- Written/Oral/section summaries;
- capability/weakness/review state;
- evidence/attempt history at a useful level;
- mock results;
- learner-authored Writing retained in history;
- retained transcripts/evaluations;
- voluntarily reported real-exam outcome;
- profile/preferences that belong to the learner.

Raw audio can only be exported if it still exists because the learner explicitly chose to retain it.

The export must not redistribute rights-restricted Corpus/reference material merely because an evidence record points to it. A stable identifier/description can preserve provenance without copying prohibited source content.

A polished export UI is not required to prove the first personal-project learning loop, but the product contract requires that architecture not trap learner data in an intentionally non-portable form.

## 9.7 Deletion expectations

**Decision:** The learner can delete their personal Bestehen data.

Full deletion covers, where applicable:

- profile/account identity;
- goal/date context;
- evidence and learner-model history;
- mistakes/review states;
- Writing responses;
- saved/raw audio still present;
- transcripts/evaluations linked to the learner;
- readiness/mock history;
- notification/schedule preferences;
- voluntarily reported real-exam outcome;
- synced copies controlled by Bestehen.

The product should warn clearly that deletion may make progress/readiness unrecoverable.

Aggregated calibration/product metrics may be retained only when they have been irreversibly de-linked from the learner such that they are no longer personal learner records. Legal retention requirements, if any, are a later legal/architecture matter; they must not be invented by analytics design.

## 9.8 Device sync expectations

**Decision:** Cross-device sync is desirable but **not required for the first personal-project version**.

When sync is offered, the user contract is:

- the same learner goal, evidence history, readiness, review obligations, settings, and current plan are available across signed-in devices;
- completed evidence must not be duplicated merely because devices sync the same attempt twice;
- conflicts preserve evidence truth rather than choosing whichever device shows the higher score;
- offline/queued attempts, if supported, retain their actual condition/timestamp and merge once;
- raw audio does not need to sync when it is ephemeral.

Sign-in may be required for this future sync capability even though core first use remains account-optional.

## 9.9 Offline expectations

**Decision:** Full offline parity is **not a launch requirement**.

The product should degrade honestly:

- already-loaded objective practice/review may continue offline where practical;
- locally available progress/history may remain viewable;
- Writing/Speaking evaluation, adaptive AI partner behavior, uncached audio/content, sync, and some mocks may require connectivity;
- a measured attempt that cannot complete required media/evaluation because connectivity failed is partial/pending/invalid as appropriate — never silently target-condition;
- reconnecting should not create duplicate evidence.

Stage 25 owns the broader low-connectivity/accessibility experience. Stage 24 only requires that offline limitations never corrupt evidence semantics.

## 9.10 Privacy-sensitive AI data handling

**Decision:** AI receives the minimum learner data necessary for the specific coaching/evaluation job.

Product requirements:

1. **Purpose limitation:** send the response/task/context needed for the current Writing, Speaking, generation, or partner action — not the learner's entire history by default.
2. **Data minimization:** do not include name, exact exam date, profile fields, or unrelated past mistakes when they are unnecessary to judge the current response.
3. **Pseudonymous processing:** use non-identifying learner references where an external service needs correlation.
4. **Modal separation:** raw audio is sent only where speech processing/evaluation requires it; Writing text is sent only where Writing evaluation/coaching requires it.
5. **No analytics-by-LLM default:** deterministic aggregation of structured evidence is preferred to sending learner histories to a premium model for analytics summaries.
6. **No general-model training by default:** learner responses, audio, and real exam outcomes must not intentionally be contributed to third-party/general model training without separate explicit opt-in.
7. **Confidence-preserving failure:** if the required evaluator cannot be used safely/reliably, keep evaluation pending/lower-confidence rather than manufacture a readiness update.
8. **Outcome-data separation:** voluntary real-exam outcomes can support Bestehen calibration, but that purpose is explained and deletion remains available.
9. **No advertising/session-replay requirement:** the personal-project analytics plan has no need for ad tracking or invasive full-session replay.

Exact provider contracts, regional processing, encryption, legal bases, and retention mechanisms are architecture/legal decisions. The product requirement is minimization, explicit purpose, and no hidden expansion of learner-data use merely for analytics convenience.

---

## 10. Edge Cases / Failure or Uncertainty Handling

### Sparse data / one learner

Do not report impressive percentages from one or two cases. Use raw trajectories, matched attempt comparisons, and qualitative calibration findings until the sample supports aggregation.

### Learner never establishes a usable baseline

Do not count them as “failed to improve.” Report onboarding/diagnostic abandonment separately. DSRA cohorts begin only after a baseline exists.

### Learner starts already Safe

Exclude them from **attainment-rate** denominator because the product did not move them from below Safe to Safe. Track **maintenance, Ready-to-Book, calibration, and real outcome** instead.

### Learner changes exam date

Time-to-readiness and preparation-episode context may change, but historical evidence remains. Date changes never alter capability metrics retrospectively.

### Learner takes the exam while Not ready

If they voluntarily report the outcome, it is valuable calibration evidence. Passing does not prove the prior readiness model was useless; failing does not prove it was perfect. Record the exact frozen state and conditions, then analyze with the larger matched set.

### Learner is Ready to Book but fails the real exam

Treat it as a high-priority calibration case. Inspect separately:

- which component failed;
- latest readiness ranges/confidence;
- mock-to-real gap;
- evaluator version;
- content/form validity;
- days between last clean evidence and exam;
- technical/accommodation/condition differences if known.

Do not retroactively blame the learner or rewrite the historical prediction.

### Real result is partial

Use whatever is known. Written-only or Oral-only outcomes can calibrate that component without inventing the missing one.

### Self-report may be wrong

Keep outcome source confidence. Do not discard all self-report, but do not mix it with future verified outcomes without preserving the distinction.

### Evaluator version changes

Run the fixed benchmark before promotion. If historical re-evaluation would materially change a current readiness state, update current evidence interpretation transparently while preserving the old prediction snapshot for calibration history.

### Content defect discovered after use

Invalidate affected learner evidence where material, recalculate current state, and classify the event as a content-quality incident rather than learner decline.

### Offline or sync duplicate

Duplicate the record operationally if needed for recovery, but it must resolve to one independent learner attempt for mastery/confidence metrics.

### Raw audio already deleted

The App can preserve the structured score/transcript/evaluator confidence. It simply cannot perform a later raw-audio re-evaluation; that privacy/cost trade-off is accepted by the launch policy.

---

## 11. Relationship to Other Bestehen Stages

- **Stage 01 — Product Thesis:** Stage 24 operationalizes its outcome hierarchy and anti-engagement optimization rule.
- **Stage 02 — Learner Journey:** baseline, post-exam, Passed/Not passed, and optional result-entry states define the analytics cohort boundaries.
- **Stage 03 — Diagnostic:** diagnostic completion and evidence validity initialize a baseline; the diagnostic itself is not a pass prediction.
- **Stage 04 — Learner Model:** the evidence ledger is the primary source for analytics; no duplicate clickstream learner model is created.
- **Stage 05 — Mistake Memory:** candidate/known/repaired/resolved/reopened states supply repair-success metrics.
- **Stage 06 — Daily Coaching Engine:** session-value metrics should eventually help validate prioritization, but may not bypass the existing pass-risk hierarchy.
- **Stage 07 — Core Learning Loop:** Attempt/Diagnose/Repair/Retry/Remember boundaries define useful session and transfer events.
- **Stage 08 — Progression:** assistance reduction and P0→P4 condition strengthening are learning outcomes.
- **Stages 09–13 — Skill Coaching:** metrics remain task-family/lane-specific; productive evaluator QA uses the official-aligned rubric contracts shaped there.
- **Stage 14 — Review:** delayed transfer and stability metrics can later recalibrate review intervals without turning cards cleared into success.
- **Stage 15 — TELC Readiness:** remains the only readiness model; Stage 24 measures its forward and real-world accuracy.
- **Stage 16 — Mock Exams:** supplies clean independent validation occasions and the primary future mock-to-real comparison.
- **Stage 17 — Ready to Book:** supplies the high-consequence future real-pass validation cohort.
- **Stage 18 — Coach Personality:** learner-facing analytics stay evidence-based and uncertainty-aware; raw product metrics should not leak into motivational copy.
- **Stage 19 — Information Architecture:** internal analytics do not turn Home/Progress into a dense product dashboard.
- **Stage 20 — Progress and Motivation:** Readiness remains the only primary learner-facing progress concept; analytics engagement metrics remain internal/secondary.
- **Stage 21 — Content Strategy:** content approval, quarantine, freshness, and defect repair feed quality metrics.
- **Stage 22 — User Controls / Corpus Contract:** self-selected and coach-selected evidence are interpreted identically when conditions are equivalent; selection source is not a readiness weight.
- **Stage 23 — Exam Date / Habit Support:** reminder/continuation metrics stay diagnostic and never justify shame or inflated readiness.
- **Stage 25 — Accessibility / Device Experience:** must preserve accessibility-equivalent evidence conditions and may refine low-connectivity/offline expectations.
- **Later analytics/evaluation work:** should treat the metric definitions in this document as authoritative product semantics and focus on implementation, empirical thresholds, and calibration rather than creating a competing north star.
- **Stage 27 — Business / Cost Boundaries:** can use the cost metrics here to set operational budgets and escalation policy.
- **Stage 28 — Final Specification:** should carry forward DSRA, readiness calibration, real-outcome collection, data/privacy, and low-cost analytics boundaries.

---

## 12. Cost Notes

### Preferred low-cost default

The analytics design has **low incremental recurring cost** because it reuses structured product evidence that must exist for coaching anyway.

Use:

- deterministic aggregation;
- local/simple reporting at personal-project scale;
- material state snapshots rather than every click;
- sampled evaluator benchmarks rather than double-evaluating every Writing/Speaking response;
- batch/offline content QA;
- cached generated content/audio;
- ephemeral raw audio;
- cost summaries from existing model/speech calls.

### Premium capability is justified only when

- a high-impact Writing/Speaking evaluation is low-confidence or contradictory;
- an evaluator version is being benchmarked against a difficult gold sample;
- content intended for P4/readiness use needs stronger quality review;
- enough real outcomes exist that a more rigorous calibration study will materially improve learner-facing readiness truth.

### Cheaper fallback

If premium evaluation/analytics is unavailable:

- keep productive evidence lower-confidence or pending;
- use deterministic objective sections normally;
- use the existing reviewed benchmark/content bank;
- aggregate outcomes with ordinary scripts/reports;
- do not invent precision to preserve a dashboard.

### What would justify more analytics infrastructure later

Upgrade only when user volume or calibration work makes manual/simple reporting a real bottleneck: many active learners, enough matched exam outcomes for repeated model evaluation, frequent content/evaluator releases, or a need for reliable scheduled cohort reports.

---

## 13. Decisions Made

1. Chose **Decision-Grade Safe Readiness Attainment (DSRA)** as the launch north star.
2. Kept real TELC pass outcomes as the ultimate validation layer rather than a launch metric that would be too sparse and delayed.
3. Defined Ready-to-Book real-pass rate and false-ready cases as the most consequential future safety validation.
4. Defined forward-validation readiness metrics using future independent clean P4 evidence rather than circularly validating against evidence already used in the estimate.
5. Defined Written and Oral calibration separately and preserved independent pass-gate truth.
6. Defined fresh-transfer, delayed-retention, independence, target-condition, and stability metrics as the core learning mechanism measures.
7. Defined **Useful Session Outcome Rate** so sessions are judged by valid coaching value rather than time-on-screen or question count.
8. Kept retention, reminder response, session completion, and similar engagement metrics explicitly separate from learning/outcome success.
9. Defined content validity, difficulty, freshness, defect, and form-health metrics.
10. Defined Writing/Speaking evaluator repeatability, benchmark agreement, pass-gate disagreement, confidence validity, version drift, and escalation/correction metrics.
11. Defined a future mock-to-real model using the latest clean full mock within 30 days and requiring error/bias/pass-agreement measures in addition to correlation.
12. Made real exam-result collection optional, minimal, self-reported at launch, and calibration-focused; certificate/document upload is not required.
13. Preserved Stage 15's rule that pass probability remains hidden until real matched outcomes support out-of-sample calibration.
14. Defined the lean launch analytics set as evidence observations, material readiness snapshots, repair/review lifecycle, session summary, mock summary, quality incidents, cost summary, and optional real outcome.
15. Rejected full clickstream, session replay, advanced growth analytics, heavy warehouse infrastructure, and always-on AI analytics for the personal-project phase.
16. Defined cost-per-active-learner/session and productive-evidence costs so expense can be compared with learning value without biasing the coach toward cheap objective work.
17. Reconciled the live Stage 24 checklist by also defining Account, Data, and Portability expectations.
18. Made sign-in optional for first use and required only for future identity-dependent capabilities such as sync/recovery.
19. Defined a minimal learner profile and rejected unnecessary demographic collection.
20. Retained structured progress/evidence history for explainability while making raw Speaking audio ephemeral by default.
21. Defined generated-content version retention, learner export expectations, complete personal-data deletion, future sync semantics, and honest partial offline support.
22. Defined privacy-sensitive AI handling around purpose limitation, minimum payloads, pseudonymous processing, no general-model training without separate opt-in, and no need for advertising/session-replay telemetry.

---

## 14. Open Questions / Deferred Decisions

There are **no owner decisions blocking Stage 24**.

The following are intentionally deferred because they require implementation scale, empirical data, legal review, or later architecture rather than more product intent:

- analytics storage/query technology;
- analytics vendor versus local/self-hosted reporting;
- auth provider and exact account/recovery mechanism;
- exact structured export file format;
- sync protocol/conflict implementation;
- exact offline cache boundaries by platform;
- model/provider data-processing terms and regional infrastructure;
- statistical method/sample threshold for exposing a learner-facing pass probability;
- exact numeric evaluator-release acceptance thresholds before a real gold benchmark baseline exists;
- sophisticated psychometrics/IRT;
- verified real-exam result/document collection, if it is ever worth the privacy cost;
- sensitive-demographic fairness analysis unless a future product/legal need justifies collecting that data.

These deferrals do not leave an undefined learner contract: outcome priority, evidence meaning, minimum analytics, data ownership, retention behavior, and privacy boundaries are already decided.

---

## 15. Definition of Done Check

- [x] North-star metric is defined and tied to decision-grade pass readiness rather than engagement.
- [x] Learner-outcome metrics are defined.
- [x] Readiness-accuracy and calibration metrics are defined before and after real outcome data.
- [x] Written and Oral remain independently measurable.
- [x] Skill-improvement and condition-strengthening metrics are defined.
- [x] Repair success distinguishes immediate Retry from delayed retained transfer.
- [x] Session success is defined without optimizing time-on-screen.
- [x] Retention/engagement metrics are explicitly secondary to learning metrics.
- [x] Content-quality metrics are defined.
- [x] AI/productive-evaluation consistency metrics are defined.
- [x] Mock-to-real-exam correlation/comparison is defined.
- [x] Optional real exam-result collection and calibration use are defined.
- [x] Cost-per-active-learner/session and expensive-capability monitoring are defined.
- [x] Lean personal-project analytics are separated from later analytics infrastructure.
- [x] Privacy/observability are proportional and do not require invasive clickstream/session replay.
- [x] Sign-in expectation is defined.
- [x] Learner profile data is defined.
- [x] Progress/evidence history retention is defined.
- [x] Raw audio retention is defined.
- [x] Generated-content retention is defined.
- [x] Export needs are defined.
- [x] Deletion expectations are defined.
- [x] Device-sync expectations are defined.
- [x] Offline expectations are defined.
- [x] Privacy-sensitive AI data handling is defined.
- [x] No unresolved owner question blocks later design/architecture work.

**Stage 24 is product-shaped when later teams can tell whether Bestehen improves and predicts pass readiness, can collect the smallest data needed to learn from real outcomes, and can implement account/storage choices without inventing a conflicting learner-data contract.**