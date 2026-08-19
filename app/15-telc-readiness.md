# Bestehen / App — Stage 15: TELC Readiness

> **Status:** Authoritative Stage 15 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Readiness promise:** Estimate how safely the learner could meet **both** current TELC B1 pass gates if they sat the exam now, using recent direct evidence under increasingly realistic conditions, while showing uncertainty and refusing to turn sparse practice into a fake pass probability.

## 1. Purpose and Scope

This document defines the central readiness model for Bestehen / App.

Readiness is the product's primary progress concept, but it is not a lesson-completion percentage, a CEFR placement label, a generic mastery average, a streak, or an AI opinion. It is a current evidence-based estimate of **target-exam performance under the conditions the claim requires**.

The model must answer four learner questions:

1. **If I sat TELC B1 now, which pass component is most at risk?**
2. **What performance does the current evidence support for the written and oral components?**
3. **How trustworthy is that estimate, and what evidence is still missing?**
4. **What changed the estimate, and what would most improve or clarify it next?**

Stage 15 defines:

- exactly what Readiness means;
- the learner-facing representation;
- separate written and oral readiness and their combination;
- current target section/task weights;
- the role of fine-grained skills without double-counting them;
- recency, assistance, timing, realism, evaluation quality, breadth, and evidence minimums;
- mock influence;
- an initial pre-calibration score/range model;
- conservative learner-facing readiness bands;
- score-change explanations;
- the path from the initial deterministic model to empirical calibration from real exam outcomes;
- cost boundaries and failure/uncertainty handling.

This is product shaping, not implementation architecture. It does not select a database, service topology, statistical library, model vendor, event pipeline, or UI framework. Later architecture may implement these decisions in different ways, but it must preserve the evidence boundaries and learner contract defined here.

### Core decision

**Bestehen launches with a readiness index and predicted component-score ranges, not a claimed pass probability.**

The primary numeric model estimates the learner's current percentage of available points in the **written** and **oral** components separately. Because the current TELC B1 pass boundary is 60% in each component, the overall **Readiness Index** is the lower of the written and oral target-performance estimates.

A value such as **62/100** therefore means approximately **“the weaker pass component is currently estimated around 62% of its available points”**. It does **not** mean “62% chance of passing.”

Pass probability is a future calibrated output. It is not displayed until matched real-exam outcomes are sufficient to validate it.

---

## 2. Inputs / Existing Decisions

Stage 15 preserves the product overview, identity, and App Stages 01–14.

### 2.1 Product identity and journey constraints

- Bestehen is a calm, direct, evidence-based **exam coach**.
- Readiness, rather than course completion, is the primary progress concept.
- The learner may begin around A1. Early supported learning is useful, but it is not automatically target-exam evidence.
- The learner should be able to see **what is known, what is weak, and what is still unknown**.
- Readiness is reversible. New contradictory evidence, stale evidence, a target-blueprint change, or a corrected evaluation may lower or qualify a previous estimate.
- A booked exam date changes priority and urgency; it never raises demonstrated ability or readiness.
- The learner may book before the App considers them ready. Stage 17 owns the booking recommendation and final ready-to-book policy.

### 2.2 Learner-model constraints

Stage 04 already defines the evidence ledger and the semantics Stage 15 must consume:

- direct evidence flows upward from response/rubric → task pattern → section → written/oral component;
- missing evidence is **unknown**, never silently imputed as zero or inferred from another modality;
- mastery, confidence, freshness, assistance dependence, timing, and readiness contribution are separate;
- Reading, Listening, Writing production, Speaking production, and interactive Speaking require direct evidence in their own lanes;
- assistance and timing are preserved on every observation;
- evidence strength is already classified from **E0 excluded** through **E4 target-condition anchor**;
- one repair chain is one evidence episode; repeated clicks/items do not become independent evidence;
- the model must avoid counting one response several times merely because it maps to several fine-grained skills.

Stage 15 therefore does **not** create a second mastery model. It defines how the existing evidence is interpreted for the current target exam.

### 2.3 Progression and realism constraints

Stage 08 defines:

- **P0 Supported Foundation**;
- **P1 Guided A2**;
- **P2 A2/B1 Bridge**;
- **P3 Independent B1 Training**;
- **P4 Target Conditions**.

P0–P2 are primarily learning/progression evidence. P3 can create strong B1 target-mappable readiness evidence when it is fresh, direct, unassisted, and valid. P4 creates the strongest target-condition evidence when the current blueprint, timing/playback/reference rules, content, and evaluation are valid.

### 2.4 Skill-stage constraints

Stages 09–13 define the scoring units and evidence boundaries Stage 15 aggregates:

- Reading has three target task families and target timing is ultimately meaningful inside the shared Reading + Sprachbausteine block.
- Sprachbausteine has two target parts and shares a 90-minute official block with Reading; an invented standalone official time limit must not be used.
- Listening has three target parts with part-specific playback rules; transcript-assisted or extra-replay work is not equivalent to clean target Listening.
- Writing uses the official three-criterion TELC-aligned estimate. One good email is not enough for strong Writing readiness.
- Speaking is the entire oral pass component. S1/S2/S3 remain separate, and S2/S3 require genuine interaction evidence. A solo monologue cannot prove oral interaction readiness.
- Writing/Speaking model outputs are evaluator estimates, not official telc grades. Evaluator confidence and version must travel with the evidence.

### 2.5 Review and mistake constraints

Stages 05 and 14 establish that:

- one target-condition failure can be a high-priority provisional blocker without becoming a permanent fine-grained weakness;
- repeated coherent realistic failure should eventually dominate old supported success;
- successful immediate retry is learning responsiveness, not retained readiness;
- fresh delayed transfer and retention matter;
- valid natural practice or mock evidence may satisfy review;
- no review scheduler or weakness rule may create a second readiness score.

---

## 3. Current TELC B1 Target Anchor

### 3.1 Verification and versioning

The target scoring anchor was rechecked on **19 August 2026** against the current official telc product page and the official `Zertifikat Deutsch B1, Übungstest Version 1`.

Current launch blueprint:

| Component / section | Maximum points | Share of total exam | Current pass implication |
|---|---:|---:|---|
| Reading / Leseverstehen | 75 | 25% | Part of written component |
| Language Elements / Sprachbausteine | 30 | 10% | Part of written component |
| Listening / Hörverstehen | 75 | 25% | Part of written component |
| Writing / Schriftlicher Ausdruck | 45 | 15% | Part of written component |
| **Written component total** | **225** | **75%** | **Must reach at least 135 / 225 (60%)** |
| Speaking / Mündlicher Ausdruck | 75 | 25% | **Must reach at least 45 / 75 (60%)** |
| **Exam total** | **300** | **100%** | Overall points do not override either component gate |

The official weighting table further divides the target into:

- Reading R1/R2/R3: **25 points each**;
- Sprachbausteine SB1/SB2: **15 points each**;
- Listening H1/H2/H3: **25 points each**;
- Writing: **45 points**, with the three official criteria contributing equal maximum raw value before the current multiplier;
- Speaking S1/S2/S3: **15 / 30 / 30 points**.

Official references used for this Stage 15 check:

- `https://www.telc.net/sprachpruefungen/deutsch/zertifikat-deutsch-telc-deutsch-b1/`
- `https://shop.telc.net/media/catalog/product/file/2/0/20201225_5061-b00-010301_web.pdf`

### 3.2 Product rule: never collapse the pass condition to 180/300

The total maximum is 300 and 60% of 300 is 180, but **180/300 is not a sufficient pass model** because the written and oral components must each independently cross their own 60% threshold.

Examples:

- Written 150/225 + Oral 35/75 = 185/300 overall, but oral is below its pass gate. Bestehen must show **Not ready — oral component**.
- Written 130/225 + Oral 60/75 = 190/300 overall, but written is below its pass gate. Bestehen must show **Not ready — written component**.
- A strong written result must never hide missing or weak oral evidence, and vice versa.

All target weights and pass rules are versioned. If telc changes the blueprint, historical evidence may remain useful capability evidence, but current readiness must be recomputed against the approved current target definition.

---

## 4. Learner-Facing Readiness Representation

### 4.1 Recommended primary representation: a combination

Bestehen uses a **combination** rather than choosing one isolated number:

1. **Readiness band** — Not ready, Borderline, or Safe pass range; when evidence is too sparse, show Evidence building / Not enough evidence instead of inventing a band.
2. **Readiness Index, 0–100** — available only after the minimum evidence needed for a defensible numeric estimate is met.
3. **Written readiness** — estimated current written percentage and equivalent point range versus the 135/225 pass line.
4. **Oral readiness** — estimated current oral percentage and equivalent point range versus the 45/75 pass line.
5. **Evidence confidence** — Low, Medium, or High, with concrete missing/weak evidence named.
6. **Primary blocker / evidence gap** — the section, part, timing condition, assistance dependency, or uncertainty currently limiting the claim.
7. **Pass probability** — deliberately absent at launch; may be added later only after empirical outcome calibration.

### 4.2 Readiness Index definition

Let:

- **W** = estimated written target performance as a percentage of the 225 available written points;
- **O** = estimated oral target performance as a percentage of the 75 available oral points.

Then:

**Readiness Index = min(W, O)**

This is intentionally a bottleneck measure. It mirrors the independent pass gates and keeps the weaker component visible.

The pass line is **60/100** under the current blueprint because both component pass requirements are 60%.

The index is not a probability and should normally be rendered as **`62 / 100`**, not `62% chance`.

### 4.3 When the overall number is withheld

Do not show an overall 0–100 Readiness Index merely because some practice exists.

The overall number is withheld when:

- either written or oral has no defensible numeric target estimate;
- an official scoring unit required for the component estimate has no usable current direct evidence;
- Speaking lacks actual oral evidence;
- S2/S3 evidence is only solo/typed when interaction is required;
- productive evaluation is pending or too unreliable to support the section;
- the target blueprint is stale/unverified for evidence being treated as current target evidence.

In those cases the Home/Progress experience says **Evidence building** or **Not enough evidence**, names the gap, and still shows useful skill/progression information.

This preserves Stage 03's rule that the initial diagnostic does not manufacture a precise readiness percentage.

### 4.4 Secondary predicted-score view

When evidence is sufficient, Bestehen may show:

- `Written: 144 / 225 estimated · planning range 134–154 · pass line 135`
- `Oral: 47 / 75 estimated · planning range 41–53 · pass line 45`

The range is explicitly a **Bestehen planning range**, not an official telc result, not a 95% confidence interval, and not a psychometric guarantee.

The learner can drill down to sections/parts, but the default screen should stay coach-like rather than expose every coefficient.

---

## 5. What Counts Toward the Numeric Target Estimate

### 5.1 Core rule: only target-mappable direct B1 evidence can set the score

The numeric target-performance estimate is deliberately narrower than the full learner model.

**Direct score-setting evidence** must be:

- mapped to a current official scoring unit or rubric;
- at B1-equivalent difficulty;
- based on a fresh learner response;
- direct in the required modality;
- evaluated reliably enough to support the mapped outcome;
- unassisted except for non-answer-bearing accessibility/access support;
- classified as Stage 04 **E3 strong direct evidence** or **E4 target-condition anchor**.

This normally means P3/P4 evidence.

### 5.2 What does not directly set the target score

The following remains useful learner/coaching evidence but does **not** directly raise the numeric target-performance estimate:

- P0/P1 supported Foundation/A2 work;
- P2 bridge success whose easier language/task conditions are not target-equivalent;
- initial diagnostic evidence that is too sparse or assisted;
- answer-bearing hints;
- phrase-bank/model-answer dependence;
- same-item retries after solution exposure;
- transcript-based success for a Listening claim;
- typed rehearsal for a Speaking claim;
- unsupported fine-grained skill inference;
- content/evaluator results too uncertain for the scoring unit.

This is intentionally conservative. The learner can make real progress before the App has enough evidence to publish a target score.

### 5.3 Assisted evidence can lower confidence or expose a blocker

Assisted evidence is not ignored. It can show:

- that the skill is reachable with support;
- what support unlocks performance;
- whether assistance dependence is narrowing;
- that even supported performance remains below the working target;
- which prerequisite should be repaired next.

But supported success cannot make a pass-critical section look target-ready before equivalent unassisted evidence exists.

### 5.4 Access support is not answer assistance

Accessibility or interaction support that does not change the tested linguistic capability does not reduce the ability estimate merely because support exists. The exact target-condition equivalence of accommodations belongs to Stage 25.

Until then, the condition is preserved and the App avoids claiming exact target equivalence when that has not been shaped yet.

---

## 6. Initial Pre-Calibration Calculation Model

The first model is intentionally deterministic and auditable. It should be easy to calculate from stored evidence and easy to replace or recalibrate later.

### 6.1 Step 1 — aggregate independent attempts, not raw clicks

For each official scoring unit, first collapse responses into an **independent attempt/episode result**.

Examples:

- a 10-item Reading part inside one set is one task-family observation plus its supported item details, not ten independent confidence occasions;
- all rubric dimensions from one Writing email belong to one Writing occasion;
- all turns from one S3 planning exchange belong to one S3 occasion;
- one mock counts as one occasion for consistency/confidence even though it contains many scored decisions.

This prevents confidence from exploding because one long test contains many items.

### 6.2 Step 2 — normalize the official scoring-unit result

Each eligible E3/E4 observation has a normalized target result from 0 to 100 for the official scoring unit it measures.

Examples:

- objective target-equivalent tasks use the reviewed target-aligned point result;
- Writing uses the official-criterion-aligned point estimate defined in Stage 12;
- Speaking uses the official-part-aligned estimate defined in Stage 13;
- a generic fine-grained grammar or vocabulary score does not become an invented telc point score.

### 6.3 Step 3 — weight eligible observations

For the initial model, an eligible observation's influence uses:

**effective weight = Stage 04 evidence strength × readiness recency × evaluation quality**

#### Stage 04 evidence-strength input

| Evidence tier | Existing relative weight | Stage 15 use |
|---|---:|---|
| E0 — excluded | 0 | No readiness effect |
| E1 — weak learning signal | 0.25 | No direct numeric target-score effect |
| E2 — standard observation | 0.5 | Training/support/confidence context; normally not direct score-setting evidence |
| E3 — strong direct evidence | 1.0 | Eligible target-mappable score evidence |
| E4 — target-condition anchor | 1.5 | Highest normal score evidence and realism anchor |

The initial model therefore avoids inventing a second assistance/timing multiplier on top of Stage 04. The evidence tier already reflects assistance, directness, difficulty, independence, and realism.

#### Readiness-specific recency multiplier

Stage 15 deliberately uses stricter current-readiness windows than ordinary daily coaching:

| Age of relevant evidence | Initial readiness multiplier | Interpretation |
|---|---:|---|
| 0–14 days | 1.00 | Fully current |
| 15–30 days | 0.90 | Strongly current |
| 31–60 days | 0.65 | Useful but aging |
| 61–90 days | 0.35 | Weak current anchor; recheck due for high-stakes claims |
| >90 days | 0 | Historical capability only for current readiness |

Historical evidence is retained in progress history and may guide rechecks. It simply stops pretending to answer **“could you do this now?”** after it is too old.

#### Evaluation-quality multiplier

| Evaluation quality | Initial multiplier |
|---|---:|
| High / reviewed deterministic / readiness-grade validated evaluator | 1.00 |
| Medium | 0.75 |
| Low but still usable | 0.40 |
| Unsupported / invalid | 0 |

For objective tasks, reviewed answer-key scoring can normally be high confidence. For Writing/Speaking, evaluator confidence/version and the quality gates from Stages 12–13 remain authoritative.

### 6.4 Step 4 — estimate each official scoring unit

For each scoring unit, calculate the weighted mean of current eligible E3/E4 normalized outcomes.

Rules:

1. Fresh target evidence should dominate old P3 evidence naturally through E4 + recency weight.
2. One repeated/near-duplicate task is not a new independent occasion.
3. A technically compromised attempt is excluded rather than scored low.
4. A major contradiction lowers confidence and widens the range before the model concludes that a stable capability suddenly disappeared.
5. Repeated coherent E4 failure must eventually dominate older supported/untimed success.
6. A single independent episode may move a sparse estimate materially, but it cannot create high confidence by itself.

### 6.5 Step 5 — apply official task/section weights

#### Reading

| Unit | Weight inside Reading | Official max |
|---|---:|---:|
| R1 Global | 1/3 | 25 |
| R2 Detailed | 1/3 | 25 |
| R3 Selective | 1/3 | 25 |

#### Language Elements

| Unit | Weight inside Sprachbausteine | Official max |
|---|---:|---:|
| SB1 Grammar/context | 1/2 | 15 |
| SB2 Lexis/context | 1/2 | 15 |

#### Listening

| Unit | Weight inside Listening | Official max |
|---|---:|---:|
| H1 Global | 1/3 | 25 |
| H2 Detailed | 1/3 | 25 |
| H3 Selective | 1/3 | 25 |

#### Writing

The initial target estimate follows the **official three criteria**, each with equal maximum raw value in the current rubric:

- Aufgabenbewältigung;
- Kommunikative Gestaltung;
- Formale Richtigkeit.

The Stage 12 coaching sub-dimensions explain these estimates but do not create extra TELC points.

#### Speaking

| Unit | Weight inside Oral | Official max |
|---|---:|---:|
| S1 Einander kennenlernen | 20% | 15 |
| S2 Über ein Thema sprechen | 40% | 30 |
| S3 Gemeinsam etwas planen | 40% | 30 |

### 6.6 Step 6 — calculate component estimates

Let section estimates be expressed from 0 to 1.

**Written predicted points** =

`75 × Reading + 30 × Sprachbausteine + 75 × Listening + 45 × Writing`

**Written target percentage (W)** = Written predicted points / 225 × 100.

**Oral predicted points** =

`15 × S1 + 30 × S2 + 30 × S3`

**Oral target percentage (O)** = Oral predicted points / 75 × 100.

**Readiness Index** = min(W, O).

The component formulas intentionally mirror the target blueprint rather than a generic equal average of five App skill cards.

### 6.7 Fine-grained skill weights: inherited, not additive

**Decision:** Fine-grained learner-model skills do **not** receive a second independent percentage that is added to readiness.

Their readiness influence is **inherited through the official scoring units they affect**.

Examples:

- restriction handling may affect R2/R3 outcomes;
- connector control may affect SB1 and Writing;
- number recognition may affect Listening;
- interaction repair may affect S2/S3.

But after the task/rubric outcome has already changed the target score, the same fine-grained node is not counted again as bonus/penalty points.

Fine skills are used to:

- explain the estimate;
- identify bottlenecks;
- choose coaching priorities;
- decide which evidence gap to close;
- widen confidence when a known pass-relevant weakness conflicts with a flattering average;
- later improve prediction if empirical outcome data proves a reliable additional effect.

This is the Stage 15 answer to “skill weights within sections”: **the first model weights official scoring units; diagnostic skills inherit their importance from those mappings rather than receiving a flat parallel score.**

---

## 7. Uncertainty and Confidence

### 7.1 Confidence is evidence confidence, not probability confidence

The learner sees **Low / Medium / High evidence confidence** for Written, Oral, and overall Readiness.

Stage 04's confidence dimensions remain the foundation:

- effective volume;
- breadth;
- independence;
- consistency;
- quality;
- recency.

Stage 15 adds **target coverage and realism** because the claim is specifically TELC B1 readiness.

### 7.2 Planning-range calculation

The initial model produces a practical score range rather than a statistical confidence interval.

For each sufficiently evidenced scoring unit:

1. take the weighted mean;
2. calculate observed recent variation when multiple comparable occasions exist;
3. impose a minimum uncertainty floor based on confidence;
4. widen for material contradiction or missing target-condition realism.

Initial minimum half-widths:

| Unit evidence confidence | Minimum planning-range half-width |
|---|---:|
| Low | ±12 percentage points |
| Medium | ±8 percentage points |
| High | ±5 percentage points |

Add **3 percentage points** when either of these applies:

- no recent E4 target-condition anchor exists for the unit; or
- a major unresolved contradiction exists.

Cap the initial half-width at **±20 percentage points**. If uncertainty is worse than that, the correct state is normally **Not enough evidence**, not a huge pseudo-precise range.

Component lower/upper ranges are produced by applying the official point weights to the section/unit lower and upper estimates.

These widths are provisional product heuristics. Stage 26 must recalibrate them against real mock/exam error.

### 7.3 Component confidence rules

**Low** when the number is technically calculable but evidence is narrow, mostly one occasion, missing realistic confirmation, or contains meaningful contradiction.

**Medium** normally requires:

- every official scoring unit in the component to have direct current score-setting evidence;
- at least two independent recent observations for the major task families/parts where feasible;
- an unassisted signal in every required lane;
- productive evidence across more than one prompt/occasion;
- no major unresolved evaluation/content contradiction.

**High** additionally requires:

- Stage 04 High-confidence characteristics: at least five effective evidence units across at least three occasions/fresh variants for the relevant component claims;
- broad target-task coverage;
- recent E4 target-condition evidence in every major section/part;
- multiple-day productive/interactive evidence;
- no pass-critical section depending on one fragile evaluator result;
- no major unresolved contradiction.

Overall confidence is the **lower** of Written and Oral confidence.

### 7.4 Decision-grade evidence for strong readiness language

A component may have a numeric estimate before it has decision-grade evidence. **Safe pass range** requires more.

#### Written decision-grade minimum

All of the following:

1. R1/R2/R3, SB1/SB2, H1/H2/H3, and Writing have current direct E3/E4 score-setting evidence.
2. Reading, Sprachbausteine, Listening, and Writing each have at least one **recent E4 target-condition anchor within 30 days**.
3. Reading + Sprachbausteine include at least one valid target-condition shared-block timing/allocation observation; isolated invented part timers do not qualify.
4. Listening target evidence uses the current part-specific playback rules.
5. Writing includes a current clean target-time response and at least one other fresh independent B1 Writing response on another occasion.
6. Evidence spans at least two days/occasions rather than one single marathon.
7. Each written section has at least Medium confidence and no unresolved pass-critical contradiction.

#### Oral decision-grade minimum

All of the following:

1. S1/S2/S3 all have current direct oral E3/E4 score-setting evidence.
2. S2 and S3 include genuine partner interaction, not only solo/fixed monologue behavior that cannot test the claim.
3. At least two fresh S2/S3 contexts across at least two occasions exist so one memorized scenario cannot dominate.
4. At least one current full target-condition three-part oral simulation or equivalent P4 oral sequence exists within 30 days.
5. A second independent recent P3/P4 oral occasion confirms that the full simulation is not the only evidence.
6. Intelligibility is validly judgeable.
7. Each oral part has at least Medium confidence and no unresolved pass-critical contradiction.

These are **readiness evidence minimums**, not the final “book your exam” rule. Stage 17 may add mock-count, consistency, date, maintenance, and practical booking requirements.

---

## 8. Assistance and Timing Rules

### 8.1 Assistance treatment

Assistance changes the claim, not the learner's worth.

| Evidence condition | Readiness treatment |
|---|---|
| Non-answer-bearing access support | May remain fully eligible when it does not change the tested capability; preserve condition |
| Unassisted fresh B1 task | Eligible E3 score evidence when target-mappable and valid |
| Light language/strategy assistance | Useful training/support evidence; normally E2 and not direct score-setting evidence |
| Answer-narrowing hint / supplied structure | Weak learning evidence; no direct target score-setting effect |
| Model/solution exposure before retry | Immediate response is repair evidence, not readiness evidence |
| Same-item repetition after feedback | Does not create independent readiness evidence |

If assisted performance is strong while unassisted performance is weak or missing, learner-facing wording should say **“This skill is working with support; independent exam evidence is still missing.”**

### 8.2 Timing treatment

Timing is a distinct exam capability.

- **Open/untimed E3** may contribute to the target score estimate if the task is B1-equivalent and otherwise eligible, but it cannot by itself produce Safe pass range.
- **Practice-timed E3** is stronger execution evidence but remains distinct from exact target conditions.
- **P4/current-target timed evidence** can be E4 and is required for decision-grade safe language.
- A timed failure after stable untimed success should diagnose execution/timing before automatically lowering the underlying language node.
- A learner who can perform only after extra time may have strong training capability and still have target-condition uncertainty; Stage 25 decides accommodation equivalence.

### 8.3 Section-specific timing realism

- Reading + Sprachbausteine: true target allocation evidence is earned in the current shared **90-minute block**, not by claiming an official standalone time for each part.
- Listening: exact playback opportunity is part of target realism.
- Writing: clean target evidence uses the current **30-minute** condition.
- Speaking: target evidence preserves the current preparation and part timing/sequence rules plus actual interaction behavior.

---

## 9. Minimum Evidence Before Any Numeric Readiness Estimate

### 9.1 Written numeric estimate eligibility

A written point estimate is shown only when each of these has at least one current direct target-mappable E3/E4 observation:

- R1, R2, R3;
- SB1, SB2;
- H1, H2, H3;
- one complete enough Writing response with trustworthy official-criterion estimate.

One observation per unit is enough to calculate a **Low-confidence provisional number**, not to call the learner safe.

### 9.2 Oral numeric estimate eligibility

An oral point estimate is shown only when:

- S1 has direct oral evidence;
- S2 has direct oral evidence including response to a partner/input;
- S3 has direct oral evidence including actual negotiation/planning interaction;
- each part is target-mappable at B1 difficulty and evaluation is trustworthy enough to estimate the official-aligned part result.

Solo Speaking may build production capability but cannot fill an interactive scoring unit that requires interaction.

### 9.3 Overall index eligibility

The overall Readiness Index is shown only when **both** component numeric estimates are eligible.

Before then, the learner gets:

- Evidence building / Not enough evidence;
- what has been measured;
- what is missing;
- which next task would close the highest-value gap.

This is a deliberate trust choice, not a missing feature.

---

## 10. Readiness Bands

The official pass boundary is 60% in each component. Bestehen adds conservative **pre-calibration guard bands** around that line.

### 10.1 Component bands

#### Not enough evidence

Use instead of a pass-risk band when the component lacks the minimum direct coverage for a numeric estimate and existing evidence does not already make a below-target conclusion clear.

#### Not ready

A component is initially **Not ready** when at least one of these is true:

- target estimate is below **55/100** with sufficient direct evidence to support the conclusion;
- repeated recent E4 target-condition evidence is below the 60 pass line;
- a pass-critical target condition remains consistently unsuccessful even when the average is superficially higher;
- a supported/bridge learner is clearly not yet able to produce meaningful P3/P4 evidence.

A learner can therefore be responsibly “Not ready” before a precise index exists when strong lower-rung evidence shows the target is currently unreachable. The App should still avoid fake point precision.

#### Borderline

A component is **Borderline** when any of these applies:

- target estimate is **55–64.9/100**;
- the planning range crosses the official 60 line;
- point estimate is ≥65 but decision-grade target evidence is missing;
- recent realistic evidence materially contradicts prior results;
- one pass-critical section/part is unstable enough that the average is not trustworthy.

#### Safe pass range

A component is in **Safe pass range** only when all of these are true:

1. target estimate is at least **65/100**;
2. the **lower end of the planning range is at or above 60/100**;
3. the component meets the decision-grade evidence minimum in Section 7.4;
4. evidence confidence is at least Medium;
5. no unresolved pass-critical bottleneck or evaluator/content problem undermines the component;
6. the current target blueprint is valid for the claim.

`65` is a Bestehen launch safety margin, not an official telc grade boundary. It exists because a point estimate sitting one or two points above 60 is not a defensible “safe” claim before empirical calibration.

### 10.2 Overall band

Because both components must pass:

- **Overall Safe pass range** only when **both Written and Oral are Safe pass range**.
- **Overall Not ready** when either component is responsibly Not ready.
- **Overall Borderline** when neither component is Not ready, both are sufficiently evidenced, and at least one is Borderline.
- **Overall Evidence building / Not enough evidence** when no component is established Not ready but at least one cannot yet be judged responsibly.

The overall band is therefore bottleneck-driven, not an average.

### 10.3 “Safe” is not “guaranteed”

Learner-facing copy must never say that Safe pass range guarantees a pass. It means current recent evidence has a conservative margin above the pass line and enough realistic breadth to make that claim useful.

Stage 17 decides when that evidence becomes a **Ready to book** recommendation.

---

## 11. How Mock Exams Affect Readiness

### 11.1 Mock evidence is strong because of conditions, not because the label says “mock”

A mock affects readiness only to the extent that it is valid for the claim:

- current blueprint;
- correct task/part structure;
- appropriate timing/playback/preparation constraints;
- no coaching during the measured block;
- fresh content;
- technically valid capture;
- trustworthy evaluation.

A valid target-condition mock normally produces E4 evidence for the scoring units it actually measures.

### 11.2 One mock is one correlated occasion

Do not let one full mock create artificial certainty.

- Item/criterion results update the relevant scoring units.
- For confidence/independence, the mock counts as **one occasion**, not dozens of independent samples.
- A full mock additionally supplies valuable sequencing, endurance, allocation, and realism evidence that isolated tasks cannot provide.
- The score receives normal E4 influence through the Stage 04 evidence weight; there is **no extra secret “mock bonus.”**

### 11.3 Passing mock behavior

One valid passing mock:

- can move the component estimate materially;
- narrows uncertainty if it agrees with prior evidence;
- raises realism coverage;
- may resolve an earlier timing/sequence question;
- **does not by itself create Safe pass range or High confidence** when breadth/independence is otherwise weak.

Repeated independent target-condition results that agree with broader evidence are what make the estimate stable.

### 11.4 Failed mock behavior

One failed mock against stable contrary evidence:

- updates the score as strong E4 evidence;
- lowers confidence / widens the range if the result is contradictory;
- triggers cause analysis before broad regression;
- does not shotgun-create every fine-grained weakness visible in the mock.

Repeated coherent failed mocks or target-condition sections should eventually dominate old assisted/untimed success and can move the component to Not ready.

### 11.5 Partial, paused, or technically compromised mocks

Use only the valid evidence actually obtained.

- A completed valid section may update that section.
- An interrupted mock cannot claim full sequencing/endurance realism.
- Technical failure is not learner failure.
- A learner continuing after an invalid pause may receive useful practice evidence, but the result is no longer unchanged full target-condition evidence.

Stage 16 owns exact mock formats, cadence, pause rules, and post-mock UX. It must preserve these Stage 15 evidence semantics.

---

## 12. Explaining Readiness Changes

### 12.1 Every movement must be traceable

A readiness change explanation is generated from structured evidence differences, not from a free-form model story.

For each recalculation, preserve:

- prior and current Written estimate/range/confidence;
- prior and current Oral estimate/range/confidence;
- prior and current Readiness Index/band;
- the new/aged/reclassified observations that caused the change;
- section/part affected;
- assistance/timing/evaluation condition;
- whether the main change was performance, confidence, freshness, blueprint, or calibration.

### 12.2 Learner-facing explanation order

Show at most three reasons by default:

1. **What changed:** Written, Oral, overall index, confidence, or band.
2. **Why:** the highest-impact new or aging evidence.
3. **What it means next:** blocker, confirmation needed, or strongest next evidence task.

### 12.3 Do not celebrate noise

The default UI should not announce tiny daily numerical movement as progress.

A score-change callout is normally shown only when one of these happens:

- Readiness Index changes by at least **2 points**;
- Written or Oral changes by at least 2 points;
- readiness band changes;
- confidence changes;
- a pass-critical bottleneck changes;
- a major target-condition mock/result arrives;
- a blueprint/calibration change materially reinterprets evidence.

Smaller changes may remain visible in history without a celebratory/punitive message.

### 12.4 Example explanations

**Strong new evidence**

> Written readiness rose from 61 to 65. Your new target-playback Listening result was strong and replaced older replay-assisted evidence. Writing is unchanged.

**Non-bottleneck improvement**

> Written improved, but overall readiness stayed at 58 because Oral is still the limiting pass component.

**Confidence improved without score movement**

> The estimate stayed at 66, but confidence moved from Low to Medium. A second fresh Writing task confirmed the same level under target time.

**Evidence aged**

> Oral confidence fell because the last target-condition S3 planning exchange is now over 30 days old. Your historical result still counts as progress; we need one fresh interaction before using strong readiness language again.

**Contradictory mock**

> Oral readiness moved from 67 to 63 after a target-condition simulation. The result conflicts with your recent practice, so the range is wider until one fresh S2/S3 check clarifies whether this was a one-off or a real change.

**Model recalibration**

> Your German performance did not change. We recalibrated how older evidence predicts real exam results, so the readiness estimate changed by 3 points. Your underlying attempt history is unchanged.

---

## 13. Initial Calibration Before Real Outcome Data

### 13.1 Launch model is blueprint-aligned, not empirically probabilistic

Before Bestehen has enough matched learner → real-exam outcome data:

- the Readiness Index is a **target-performance index**;
- written/oral predicted points are weighted from current target-mappable E3/E4 evidence;
- uncertainty uses conservative heuristic planning ranges;
- Safe pass range uses a +5-point guard margin plus decision-grade evidence;
- **no pass probability is displayed**.

The product must explicitly label these values as **Bestehen estimates**.

### 13.2 Why no initial pass probability

A probability such as “72% chance of passing” would require evidence about how App performance, assistance history, mocks, evaluator behavior, test-day variability, and the TELC blueprint translate into real outcomes.

Before that data exists, a percentage probability would be decorative precision. A target-performance estimate with a transparent pass line and uncertainty is more defensible.

### 13.3 Pre-launch sanity validation

Before the readiness model is used for consequential learner language, manually test it against synthetic/human-reviewed learner histories covering at least:

- clearly below-B1 learner;
- strong written / weak oral;
- weak written / strong oral;
- one excellent mock but sparse history;
- consistent P3 strength but no P4 timing;
- strong assisted / weak unassisted performance;
- recent borderline results;
- old formerly strong evidence;
- contradictory mock;
- Writing/Speaking evaluator uncertainty;
- missing S2/S3 interaction;
- invalid/technical attempts;
- target-blueprint change.

The expected product behavior should match the rules in this document before numerical tuning begins.

---

## 14. Future Empirical Recalibration from Real Exam Outcomes

### 14.1 Outcome data to request/store when appropriate

Subject to Stage 24 privacy/consent decisions, the most useful real-outcome record is:

- target exam + blueprint/version;
- exam date;
- overall pass/fail;
- written pass/fail and score when available;
- oral pass/fail and score when available;
- section/subtest scores when the learner has them;
- whether the outcome is self-reported or document-verified;
- App readiness snapshot and evidence state immediately before the exam.

The App should not require proof of results merely to continue using the product.

### 14.2 First recalibration priorities

Use real outcomes to test, in this order:

1. Do predicted Written points align with actual Written points?
2. Do predicted Oral points align with actual Oral points?
3. Are Safe pass range learners actually passing both components at an acceptably high rate?
4. Are Borderline learners distributed around the pass line rather than systematically over-scored?
5. Which evidence types over- or under-predict real performance?
6. Are recency windows too aggressive or too forgiving?
7. Do E3→E4 differences predict exam results as intended?
8. Are Writing/Speaking evaluator slices causing systematic optimism/pessimism?
9. Do full mocks add predictive value beyond section-level target evidence?

### 14.3 What may be recalibrated

Real outcomes may change:

- recency multipliers/windows;
- the relative influence of E3 versus E4 evidence;
- planning-range widths;
- the +5 Safe pass guard margin;
- minimum evidence thresholds;
- how contradictory evidence widens uncertainty;
- evaluator-quality weighting;
- whether particular target-condition evidence deserves more/less predictive influence.

Real outcomes do **not** justify removing the separate written/oral pass gates or treating missing oral evidence as written-inferable.

### 14.4 Pass probability activation gate

Pass probability remains disabled until there is enough outcome data to validate it separately from the raw readiness index.

Initial product activation gate:

- at least **100 matched real-exam outcomes** for the same materially compatible target blueprint;
- at least **20 written non-pass/boundary outcomes** and **20 oral non-pass/boundary outcomes**, or an equivalent amount of evidence concentrated near each 60% component boundary;
- enough cases around the pass boundary to detect systematic false-safe behavior;
- held-out or later-in-time validation showing the probability mapping is reasonably calibrated rather than merely fitting the training data.

These numbers are conservative starting gates, not universal statistical truths. Stage 26 may raise or refine them based on the actual outcome distribution. If the personal project never reaches this evidence level, **the readiness-index + score-range model remains the permanent honest fallback.**

### 14.5 Probability representation after calibration

If probability becomes valid later:

- keep the Readiness Index and written/oral score ranges;
- show Written and Oral pass probabilities separately when each is calibrated;
- show overall pass probability only when the **joint event “passes both components”** is empirically calibrated;
- do **not** multiply written and oral probabilities by assumption;
- preserve confidence and data-quality caveats;
- recalibrate or withdraw probability after a material target-blueprint/evaluator change until validation is restored.

A calibrated probability is a later evidence layer, not a replacement for the causal exam-coach view.

---

## 15. Edge Cases / Failure or Uncertainty Handling

| Situation | Readiness behavior | What must not happen |
|---|---|---|
| Initial diagnostic only | Show starting skill/phase evidence; no overall numeric readiness unless later minimums are met | Fake pass percentage from sparse samples |
| Entire oral component missing | Overall = Not enough evidence unless other evidence already establishes Not ready | Infer Speaking from Writing/Reading |
| Strong total points but oral below gate | Overall Not ready — Oral | Use 180/300 as passing logic |
| Strong total points but written below gate | Overall Not ready — Written | Let oral strength compensate |
| Strong assisted, weak unassisted | Target estimate follows clean evidence; show support dependence | Average both as equivalent |
| Strong untimed, weak timed | Preserve language capability; target estimate/band remains limited by timing evidence | Re-teach language automatically |
| One passing mock with little history | Score can rise; confidence remains limited; Safe requires broader evidence | Declare ready from one event |
| One failed mock contradicts stable history | Strong negative update + wider range + clarifier | Erase stable history instantly |
| Repeated failed target evidence | Let recent realistic evidence dominate and lower band | Protect old flattering score indefinitely |
| Same task repeated | Reduce/exclude independence | Grow confidence from memorization |
| Writing evaluator low confidence | Lower/withhold Writing readiness effect; collect fresh/stronger evidence if decision-relevant | Force an exact TELC estimate |
| Speaking transcript unreliable | Preserve oral evidence only for dimensions still judgeable | Treat ASR failure as poor German |
| Content item ambiguous | Exclude it | Penalize learner or pay a model to rationalize ambiguity |
| Recent high performance, old pass-critical weakness | Current success can lower risk when repair/retention criteria are met; history remains | Permanently penalize repaired history |
| Evidence ages past readiness window | Lower current influence/confidence; retain historical mastery | Delete progress or claim regression from silence |
| Blueprint changes | Re-map/recompute current target relevance; preserve transferable history | Keep obsolete P4 status silently |
| Evaluator/model calibration changes | Recalculate interpretation from immutable evidence; explain calibration-caused movement | Rewrite original learner response/history |
| Exam date is tomorrow | Increase coaching urgency only | Inflate readiness because time is short |
| Learner stops a mock | Use valid partial evidence only | Score unanswered/invalid remainder as certain inability |
| Accessibility changes timing conditions | Preserve condition; wait for Stage 25 equivalence rule | Call accommodated work cheating or automatically target-equivalent |
| No AI available | Objective readiness continues; unsupported productive evidence stays pending | Fabricate productive scores |

---

## 16. Relationship to Other Bestehen Stages

- **Stage 01 — Product Thesis:** Stage 15 makes the previously deferred primary success metric concrete while preserving “probability of passing” as the strategic objective, not an uncalibrated learner-facing number.
- **Stage 02 — Learner Journey:** supplies Evidence building, Readiness under review, Ready-to-book, booked, and post-exam states. Stage 15 supplies the measurement behind them; Stage 17 owns the booking action.
- **Stage 03 — Initial Diagnostic:** remains a provisional starting baseline and must not surface a fake readiness percentage.
- **Stage 04 — Learner Model:** is the source of evidence tiers, confidence, recency, assistance/timing conditions, task/section rollups, and immutable provenance used here.
- **Stage 05 — Mistake Memory:** pass-critical known weaknesses are explanation/bottleneck signals; they do not receive a second hidden numerical penalty after the underlying task outcomes are already scored.
- **Stage 06 — Daily Coaching Engine:** consumes the readiness bottleneck, evidence gaps, confidence, and likely recoverable exam points; it must not reverse-engineer a different readiness formula.
- **Stage 07 — Core Learning Loop:** immediate Retry remains repair evidence; only later clean fresh observations can become readiness evidence.
- **Stage 08 — A1→B1 Progression:** P3/P4 define the normal readiness score-setting evidence boundary; P0–P2 remain valid learning progress without fake target-score projection.
- **Stages 09–13 — Skill Coaching:** provide the target-mappable scoring units, rubric estimates, timing/playback rules, direct-lane semantics, and evaluator confidence aggregated here.
- **Stage 14 — Review:** feeds fresh condition-qualified evidence and can restore current confidence; review completion itself does not add readiness points.
- **Stage 16 — Mock Exams:** must implement the mock evidence rules in Section 11, including one-correlated-occasion semantics, partial-mock validity, and no secret mock bonus.
- **Stage 17 — Ready to Book:** must use these bands, component gates, confidence, target-condition evidence, and unresolved blockers, then add its own booking/consistency/date policy. Safe pass range is not automatically identical to Ready to book.
- **Stage 18 — Coach Personality:** should use `Readiness Index` / `estimated target performance` language and must never paraphrase it as pass probability before calibration.
- **Stage 19 — Information Architecture:** decides exact screens/visual hierarchy; the default experience must keep Written, Oral, pass lines, confidence, blocker, and explanation discoverable.
- **Stage 20 — Progress and Motivation:** should emphasize earned evidence, stronger conditions, confidence, and repaired blockers rather than rewarding tiny index movement.
- **Stage 21 — Content Strategy:** must provide target-mappable, fresh, reviewed P3/P4 content and avoid near-duplicate evidence inflation.
- **Stage 22 — Corpus → App:** supplies current target blueprint, task mappings, difficulty/relevance, and confidence; Corpus does not calculate learner readiness.
- **Stage 24 — Account/Data:** owns consent, result upload/self-report, retention, deletion, and verification status for real-exam outcome calibration.
- **Stage 25 — Accessibility/Devices:** decides which accommodations preserve target-condition equivalence; Stage 15 preserves conditions until that decision exists.
- **Stage 26 — Analytics:** validates calibration error, false-safe rate, range coverage, recency, evidence weights, probability activation, and real-exam predictive usefulness.
- **Stage 27 — Cost Boundaries:** may impose portfolio budgets but must preserve the deterministic readiness computation and honest productive-evidence fallback.

### Cross-stage decision later agents must preserve

**The launch readiness number is a target-performance index, not pass probability. Written and oral are calculated independently against their current TELC point systems, and the overall index is the weaker component. Safe language requires both pass components, conservative score range, sufficient recent target-condition evidence, and no unresolved pass-critical uncertainty.**

---

## 17. Cost Notes

Stage 15 should have **negligible recurring compute cost beyond evaluation already required by the learner's tasks**.

### Preferred low-cost default

- Calculate section, component, range, confidence, band, and change attribution deterministically from stored structured evidence.
- Reuse Stage 04 evidence tiers rather than buying an AI model to reinterpret conditions.
- Reuse the Writing/Speaking structured evaluation already produced by the task. Do not make a second model call just to update readiness.
- Objective Reading/Language Elements/Listening results use reviewed deterministic answer keys.
- Recompute readiness only from changed/aged evidence and the current blueprint; the arithmetic itself is trivial.
- Generate learner-facing explanations from structured templates populated with the actual changed evidence.
- Cache/version the last readiness snapshot for history and explanation.

### When paid AI may affect readiness indirectly

A stronger evaluator can be justified only when an **underlying new productive observation** is high-value and too uncertain for the normal evaluator—for example, a P4/mock Writing or Speaking sample near the pass boundary. This follows Stages 12–13.

The stronger evaluator produces better **evidence**. It still does not calculate the readiness formula.

### Cheap fallback

If productive evaluation is unavailable:

- leave the relevant evidence pending/unsupported;
- lower or withhold the component estimate if minimum evidence is no longer met;
- continue calculating unaffected objective sections;
- schedule a later valid productive sample/evaluation;
- never buy an expensive model merely to avoid showing “Not enough evidence.”

There is no product justification for always-on premium AI to compute readiness, confidence, decay, bands, or explanation copy.

---

## 18. Decisions Made

1. Defined Readiness as the current evidence-based estimate of meeting **both** TELC B1 pass components under the conditions claimed.
2. Chose a **combination representation**: readiness band + 0–100 Readiness Index + written/oral predicted point ranges + evidence confidence; pass probability is deferred until empirically calibrated.
3. Defined Written and Oral independently and set the overall Readiness Index to the weaker component.
4. Locked the current blueprint weights: Reading 75, Sprachbausteine 30, Listening 75, Writing 45, Speaking 75; written 225 and oral 75.
5. Preserved the independent 60% gates: 135/225 written and 45/75 oral.
6. Defined official task/part weights within Reading, Sprachbausteine, Listening, Writing, and Speaking.
7. Defined fine-grained skill influence as inherited through official scoring units, not an additive second score.
8. Limited direct numeric target-score evidence to current, target-mappable, direct, valid E3/E4 B1 observations; supported/lower-rung work remains useful coaching evidence without manufacturing target points.
9. Defined stricter readiness recency: 0–14 full, 15–30 strong, 31–60 aging, 61–90 weak, >90 historical-only for current readiness.
10. Defined assistance and timing treatment without double-penalizing Stage 04 evidence tiers.
11. Defined deterministic pre-calibration weighting from Stage 04 strength × recency × evaluation quality.
12. Defined Low/Medium/High confidence, score planning ranges, numeric-estimate minimums, and stronger decision-grade evidence gates.
13. Defined conservative initial bands: Not ready, Borderline, Safe pass range, plus Not enough evidence when the claim cannot responsibly be made.
14. Defined mock influence as strong E4 evidence and one correlated occasion, with no secret mock bonus and no one-mock ready state.
15. Defined deterministic score-change explanations and a 2-point/material-state threshold for surfacing movement.
16. Defined a future real-exam calibration path and a conservative initial activation gate before pass probability may be shown.
17. Kept readiness arithmetic and explanations deterministic/cheap; expensive AI may improve an underlying high-value productive evaluation but never calculates the score itself.

---

## 19. Open Questions / Deferred Decisions

### No owner question blocks Stage 15

The readiness product model can be responsibly defined from the existing target, learner-model, skill, and cost decisions. No owner preference is required to complete this stage.

### Deferred to later shaping / validation

- Exact full/section/mini-mock formats, cadence, pause behavior, and mock result screen — **Stage 16**.
- Final **Ready to book** eligibility, required mock consistency, maintenance after readiness, and 21-/7-day booked-exam programs — **Stage 17**.
- Exact learner-facing wording and whether the UI renders `62/100`, an equivalent gauge, or another visual form while preserving the semantic meaning — **Stages 18–19**.
- Final data/consent flow for collecting real exam outcomes — **Stage 24**.
- Accessibility accommodation equivalence for target-condition evidence — **Stage 25**.
- Empirical tuning of recency, E3/E4 predictive influence, range widths, guard bands, probability model, activation thresholds, and calibration quality gates — **Stage 26**.
- Portfolio-wide paid-model budget caps — **Stage 27**.
- Technical storage, recalculation mechanisms, statistics libraries, event pipelines, model providers, and system architecture — post-shaping architecture work.

The numerical multipliers, ±12/8/5 planning-range floors, 65 Safe margin, 2-point movement threshold, and 100-outcome probability activation target are **initial product defaults**. They are deliberately measurable and replaceable rather than claims of psychometric truth.

---

## 20. Definition of Done Check

### Stage 15 checklist coverage

- [x] Define exactly what **Readiness** means.
- [x] Decide primary representation:
  - [x] pass probability — **future calibrated secondary output; intentionally not shown pre-calibration**;
  - [x] readiness index — **launch primary numeric representation**;
  - [x] predicted score — **launch written/oral point estimate + planning range**;
  - [x] combination — **selected product approach**.
- [x] Define written readiness.
- [x] Define oral readiness separately.
- [x] Reflect TELC's separate written/oral pass constraints.
- [x] Define section weights.
- [x] Define skill weights within sections.
- [x] Define recency effects.
- [x] Distinguish assisted from unassisted evidence.
- [x] Distinguish timed from untimed evidence.
- [x] Represent uncertainty/confidence.
- [x] Set minimum evidence before strong predictions.
- [x] Define how mocks affect readiness.
- [x] Define initial calibration before real-user outcome data exists.
- [x] Define future recalibration using actual exam outcomes.
- [x] Define “not ready,” “borderline,” and “safe pass range.”
- [x] Explain score changes to the learner.

### Deliverable checks

- [x] Current target points and pass gates are explicit and versioned.
- [x] Initial calculation model is deterministic, explainable, and cheap.
- [x] Missing evidence remains unknown rather than zero or cross-modally imputed.
- [x] Fine skills cannot double-count task/rubric evidence.
- [x] Assisted and non-target work remains useful learning evidence without inflating target readiness.
- [x] Strong readiness requires recent target-condition evidence and sufficient breadth.
- [x] One mock cannot create artificial confidence.
- [x] Pass probability is withheld until real-outcome calibration justifies it.
- [x] Calibration-caused score changes are distinguishable from learner-performance changes.
- [x] No routine premium AI call is required to calculate readiness.
- [x] No owner question blocks completion.

**Stage 15 is product-shaped when every readiness claim can answer: what target points it represents, which written/oral gate limits it, which recent direct evidence supports it, how uncertain it is, why it changed, and what evidence would change the conclusion next.**
