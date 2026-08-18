# Bestehen / App — Stage 01: Product Thesis

> **Status:** Authoritative Stage 01 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** TELC B1
>
> **Decision filter:** Does this materially improve the learner's evidence-backed readiness to pass TELC B1?

## 1. Purpose and Scope

This document locks the product thesis for Bestehen / App. It defines who the first product is for, the outcome it optimizes, what it deliberately does not become, how TELC B1 focus should constrain future extensibility, what success means beyond engagement, and how the "personal German exam coach" identity translates into product behavior.

This is a product-shaping document, not an architecture specification. Later stages may decide implementation mechanisms, scoring formulas, model providers, storage, UI composition, or infrastructure, but they should not need to reinvent the product objective captured here.

### Authoritative one-sentence product definition

**Bestehen / App is a personal German exam coach that teaches learners from around A1 through exam-shaped practice, diagnoses and repairs the weaknesses costing them points, and uses evidence to guide them toward a defensible TELC B1 pass-ready state.**

### Value proposition

**Stop guessing what to study: Bestehen shows where you are losing exam points, chooses the highest-value work to do next, and tells you when the evidence supports treating yourself as ready for TELC B1.**

The product does not promise a pass. It improves preparation quality and estimates readiness from evidence while making uncertainty visible.

## 2. Inputs / Existing Decisions

Stage 01 preserves the following established decisions from the project overview and identity documents:

- Bestehen teaches German backwards from the exam: **Observe → Attempt → Diagnose → Repair → Retry → Remember**.
- The learner-facing product is an **exam coach**, not a generic language-learning app, textbook, flashcard product, AI tutor, or mock-exam library.
- The initial learner may start around A1, while the destination remains authentic B1 exam performance.
- Readiness is the primary progress concept. XP, streaks, lesson completion, and similar engagement signals must not replace it.
- The product must eventually cover the complete target experience across reading, language elements, listening, writing, speaking, review, mock exams, and readiness.
- Written and oral evidence must remain separately visible where a weakness in either can block a pass.
- Bestehen / Corpus is the evidence and intelligence system behind the learner experience; Corpus is not itself the learner UX.
- Real/reference exam material defines what is tested. The App should usually practice the same patterns using original content where direct reuse is not appropriate.
- The project is personal initially, so recurring cost and maintainability are explicit constraints.

No prior `app/` Stage outputs existed when this stage began, so there were no earlier App shaping decisions to reconcile.

## 3. Decisions and Rationale

### 3.1 Product identity: personal German exam coach

**Decision:** Bestehen / App is a **personal German exam coach**.

"Personal" means the product uses the learner's evidence, weaknesses, history, target, and available time to choose priorities. "Exam coach" means the product takes responsibility for diagnosis, prioritization, practice selection, feedback, reassessment, and readiness interpretation.

This identity is stronger than alternatives such as "language course," "AI German tutor," or "TELC practice bank" because those labels encourage the learner to browse content or accumulate activity. Bestehen instead owns the question: **What is the highest-value next move for improving pass readiness?**

### 3.2 Optimization objective

**Decision:** The product objective is to **maximize the learner's probability of passing TELC B1, subject to honest evidence, efficient use of study time, and financially sustainable operation**.

This objective has several consequences:

1. A feature is valuable only if it can plausibly improve diagnosis, learning, exam performance, strategy, confidence in the readiness estimate, or execution under exam conditions.
2. Improving engagement is useful only when it supports preparation. Engagement is not an end in itself.
3. Strong performance in one area must not hide a pass-critical weakness in another.
4. Assisted practice is valuable for learning, but it must not be treated as equally strong readiness evidence as realistic unassisted performance.
5. The system should sometimes recommend uncomfortable weak-area practice instead of the activity most likely to maximize short-term enjoyment.

### 3.3 Initial learner profile

**Decision:** The primary initial learner is a German learner who:

- may begin at approximately **A1**, including uneven A1/A2 ability across skills;
- has a concrete goal to **reach and pass B1**, specifically TELC B1 at launch;
- values certification and exam efficiency more than broad, curriculum-complete language mastery;
- may or may not already have an exam date booked;
- may have limited study time and benefits from being told what matters most today;
- is willing to learn grammar, vocabulary, comprehension, writing, speaking, and exam strategy when those capabilities improve exam performance.

The learner does **not** need to be close to B1 before Bestehen becomes useful. Difficulty and assistance adapt; the exam-led organizing principle does not.

### 3.4 Primary learner success outcome

**Decision:** The primary learner outcome is to reach a state where **recent, sufficiently broad, increasingly realistic evidence supports treating both written and oral TELC B1 performance as pass-ready with an explicitly stated level of confidence**.

When a learner later reports a real exam result, the strongest validation outcome is straightforward: they pass TELC B1 after the product had evidence to support a pass-ready recommendation. Before enough real-exam outcomes exist, realistic mock performance, held-out transfer tasks, and stable unassisted/timed evidence serve as validation signals.

The exact readiness formula, evidence minimums, pass-range bands, and calibration procedure are intentionally deferred to Stage 15 (TELC Readiness) and Stage 17 (Ready to Book Logic). Stage 01 locks the meaning and product role of readiness, not a decorative percentage or premature formula.

### 3.5 Learn German through exam preparation

**Decision:** Bestehen does **not** place a conventional A1 → A2 → B1 course in front of exam preparation. German is learned through exam-shaped activity from the beginning.

At lower proficiency, the learner may receive simplified language, vocabulary previews, translations, hints, slowed/replayable audio, scaffolding, or guided production. Those supports exist to make exam-shaped learning accessible; they are not a parallel course curriculum.

A grammar or vocabulary topic earns product attention because it solves recurring exam problems, repairs observed weaknesses, or unlocks exam-relevant performance—not simply because a CEFR syllabus says it belongs in the next chapter.

### 3.6 TELC B1 launch focus and future extensibility

**Decision:** **TELC B1 is the only product target at launch, but it is the first target in a conceptually expandable exam framework.**

Future extensibility should influence shaping only at the boundaries where a TELC-only assumption would create an obvious product dead end. Later stages should therefore distinguish:

- generic learner evidence and skills from target-exam-specific interpretation;
- reusable practice concepts from TELC-specific task patterns;
- generic readiness evidence from TELC-specific section/pass rules;
- Corpus intelligence from the target exam weighting applied by the App.

However, Stage 01 explicitly rejects "build multi-exam now" scope. There is no requirement for multi-exam onboarding, switching exams, provider comparison, cross-exam readiness, generalized scoring UI, or parity with Goethe/ÖSD/DTZ. Those would add shaping, content, QA, and implementation cost before the first target is validated.

**Rule:** If making a choice generic is cheap and does not dilute TELC B1 quality, preserve the seam. If generalization adds meaningful complexity, optimize for TELC B1 and document the assumption for later replacement.

### 3.7 Explicit non-goals

Bestehen / App intentionally does **not** try to be:

| Non-goal | Product boundary |
|---|---|
| A complete conventional German course | No textbook-like chapter progression whose primary purpose is CEFR coverage. |
| A general conversational German tutor | Free conversation may be used when it repairs or rehearses exam-relevant speaking skills; open-ended tutoring is not the organizing product. |
| A flashcard/SRS product | Review is embedded in coaching and mistake repair. A standalone card-collection loop must not become the center of the experience. |
| A giant exercise catalog | Browsing may exist secondarily, but the default experience recommends what to do next. |
| A mock-exam-only product | Mocks are measurement and rehearsal tools inside a larger diagnosis/repair system. |
| An official TELC product | TELC is the target exam. Bestehen must not imply endorsement, certification, affiliation, or official scoring authority. |
| A perfect German / native-level coach | Feedback optimizes for B1 sufficiency and exam usefulness rather than rewriting every answer into advanced German. |
| A gamified engagement product | Streaks, achievements, or similar mechanics may support consistency but cannot outrank readiness. |
| A learner-facing Corpus browser | Corpus provenance and evidence can inform the product, but the learner should not need to navigate raw corpus internals. |
| An expensive always-on AI companion | AI is a capability used where it materially improves exam coaching, not the product identity or a requirement for every interaction. |

### 3.8 Product success beyond engagement and streaks

**Decision:** Product success is measured by **readiness quality, learning transfer, pass-critical evidence, and eventual real-exam outcomes**, not by activity volume alone.

The following hierarchy should guide later metric design:

| Success dimension | What success means | Example evidence |
|---|---|---|
| Real exam outcome | Learners classified as ready ultimately pass the target exam at an acceptable rate once enough outcomes exist. | Self-reported/verified exam result when available. |
| Readiness calibration | Readiness statements become more trustworthy as evidence grows and correspond to realistic mock/real outcomes. | Calibration by readiness band; confidence vs observed outcomes. |
| Written/oral safety | The product does not allow a strong area to conceal a pass-critical weak area. | Separate evidence sufficiency and performance trends for written and oral components. |
| Repair transfer | Diagnosis and repair improve performance on a **fresh equivalent task**, not only the task just explained. | Immediate retry plus later spaced evidence on the same underlying skill. |
| Retention/stability | Improvement persists rather than disappearing after one successful attempt. | Recurring evidence over time with reduced assistance. |
| Increasing realism | Learners progressively succeed with less help and under more exam-like constraints. | Assisted → unassisted and untimed → timed evidence progression. |
| Study efficiency | Available study time is concentrated on weaknesses and patterns that matter for the target exam. | Priority coverage, time-to-improvement, avoided low-value repetition. |
| Evidence coverage | The product accumulates enough relevant evidence to make its coaching claims responsibly. | Coverage, recency, confidence, and realistic attempts across pass-critical areas. |

Streaks, session completion, daily active use, time in app, and content consumption may be operational or diagnostic metrics. They must never become the primary product success definition.

No numeric success thresholds are locked in Stage 01 because they require later readiness design, real learner data, and calibration. Later stages must establish initial thresholds explicitly and define how they will be recalibrated.

## 4. Detailed Product Model / Rules for This Stage

The exam-coach identity is not just copy. It imposes the following product rules.

### Rule 1 — The default product action is a recommendation

The learner should normally arrive to a clear recommended next session or next action. A content library can exist, but "choose something from a catalog" is not the primary daily experience.

### Rule 2 — Every recommendation must have an exam-readiness reason

The product should be able to explain why an activity is prioritized, such as a recurring weakness, high TELC relevance, due review, insufficient evidence, upcoming exam date, or weak mock result.

### Rule 3 — Diagnose before broad teaching

A wrong answer or weak response is evidence to interpret. The product should distinguish likely causes such as vocabulary, grammar, comprehension, production, exam strategy, listening recognition, or attention before selecting repair.

### Rule 4 — Repair narrowly, then test transfer

Prefer the smallest intervention that fixes the blocker. A repair is not complete merely because the learner saw an explanation; a fresh equivalent retry should test whether the capability transferred.

### Rule 5 — Adapt assistance, not the destination

A learner around A1 may need substantial help. The task can be simplified or scaffolded, but the learning remains connected to an exam-relevant skill or pattern. Assistance should reduce as competence grows.

### Rule 6 — Learning evidence and readiness evidence are not interchangeable

Assisted, repeated, untimed, or highly scaffolded success can demonstrate learning progress, but later readiness decisions must give stronger weight to recent, unassisted, timed, exam-like evidence.

### Rule 7 — Written and oral pass risk stays visible

An aggregate readiness view may exist, but it must not conceal separate written/oral constraints. Later readiness design must preserve pass-critical weak areas instead of averaging them away.

### Rule 8 — Feedback is B1-sufficient, not perfectionist

Writing and speaking feedback should prioritize whether the learner communicates successfully enough for the target and what correction would earn or protect exam points. Advanced stylistic rewrites are secondary unless they repair a relevant weakness.

### Rule 9 — The coach is calm, direct, specific, and uncertainty-aware

The product may say an area is below the current pass range. It should pair difficult feedback with the reason and next action. It must not manufacture confidence, overpromise a pass, or use vague encouragement as a substitute for evidence.

### Rule 10 — Corpus informs priorities; learners experience coaching

Corpus may influence task patterns, topic frequency, grammar/vocabulary relevance, difficulty, distractors, and content generation. The learner-facing product should translate that intelligence into useful practice and explanations rather than expose raw corpus complexity by default.

### Rule 11 — Engagement mechanics are subordinate

If a streak, achievement, milestone, notification, or reward causes the product to favor easy repeatable activity over the highest-value exam preparation, the mechanic is working against the thesis and should be changed or removed.

### Rule 12 — Future exam support must not weaken TELC B1

Design seams may preserve future target-exam substitution, but TELC B1 correctness, realism, content quality, and readiness defensibility win whenever abstraction conflicts with launch quality.

### Rule 13 — Expensive intelligence must earn its cost

The product must not require a premium model call merely to preserve the feeling of an "AI coach." Deterministic logic, cached explanations, precomputed Corpus intelligence, templates, local/open-source processing, batching, and cheaper models should be preferred whenever quality is sufficient.

### Rule 14 — Readiness must be explainable

A readiness change should eventually be attributable to evidence: e.g. stronger recent unassisted listening, a weak timed writing sample, insufficient oral evidence, or a passing mock. The product should not expose a number that cannot explain why it moved.

## 5. Edge Cases / Failure or Uncertainty Handling

### Learner is far below B1

Do not block them behind a generic beginner course and do not throw them into unassisted B1 mocks. Keep exam-shaped tasks but reduce linguistic difficulty and increase scaffolding. Readiness should show limited/low-confidence evidence rather than pretending early assisted tasks predict a pass.

### Learner is already close to B1

Avoid forcing unnecessary beginner progression. The diagnostic and early evidence should allow the coach to move quickly toward realistic practice, weak-area repair, and mocks.

### Learner has uneven skills

Do not assign one global language level that suppresses useful variation. A learner may need A2-style support in listening while handling B1 reading well. Later stages should support skill-specific difficulty and evidence.

### Learner has no exam date

The product still coaches toward pass readiness. A date changes urgency and scheduling, not the product thesis. Recommending when to book becomes a later evidence-based state.

### Learner books an exam before being ready

The coach should not hide the risk. Later journey/coaching stages should adapt priorities to the fixed date while communicating remaining pass-critical weaknesses and uncertainty clearly.

### Evidence is sparse or contradictory

Show uncertainty and collect better evidence. Do not fill missing sections with inferred confidence merely to produce a complete dashboard.

### A learner wants broad German learning

Bestehen may still improve broad German as a side effect, but the product should not expand into unrelated curriculum unless the capability can be justified against the exam goal. The product thesis deliberately favors certification efficiency.

### Generated or AI evaluation is uncertain

The product should lower confidence, request another sample, use deterministic checks where possible, or defer stronger claims. Premium evaluation can be reserved for cases where quality materially affects readiness or repair.

## 6. Relationship to Other Bestehen Stages

Stage 01 is the decision filter for later App shaping:

- **Stage 02 — Learner Journey:** must make the coach-led route from first visit to ready-to-book concrete.
- **Stage 03 — Diagnostic:** must gather useful evidence without requiring a full B1 exam from an A1 learner.
- **Stage 04 — Learner Model:** must represent specific weaknesses, evidence quality, assistance, timing, recency, and uncertainty.
- **Stage 05 — Mistake Memory:** must convert errors into persistent coaching signals.
- **Stage 06 — Daily Coaching Engine:** must optimize the learner's limited time against exam-readiness priorities.
- **Stage 07 — Core Learning Loop:** must operationalize Attempt → Diagnose → Repair → Retry → Remember consistently.
- **Stage 08 — A1→B1 Progression:** must adapt scaffolding while preserving exam-shaped learning.
- **Stages 09–13 — Skill Coaching:** must optimize each skill for target-exam performance and B1 sufficiency.
- **Stage 14 — Review:** must support retained exam-relevant capability rather than become a standalone flashcard product.
- **Stage 15 — TELC Readiness:** must turn the readiness concept into a defensible, calibrated evidence model with separate written/oral constraints.
- **Stage 16 — Mock Exams:** must provide realistic measurement and rehearsal evidence.
- **Stage 17 — Ready to Book:** must define the evidence threshold and confidence language for recommending an exam date.
- **Stage 18 — Coach Personality:** must refine the already-locked calm, direct, diagnostic, evidence-based behavior.
- **Stage 19 — Information Architecture:** must keep "What should I do today?" and readiness central rather than turning the product into an LMS/catalog.
- **Stage 20 — Progress and Motivation:** must keep engagement mechanics secondary to meaningful capability and readiness movement.
- **Stage 21 — Content Strategy:** must turn Corpus evidence into safe, original, high-quality practice without assuming public material can be reused verbatim.
- **Later measurement/final-spec stages:** must use exam outcomes, transfer, calibration, and evidence quality as the ultimate product measures.

### Corpus relationship

Corpus is broader than TELC and may learn from multiple A2/B1 exam families. The App applies that broad intelligence through a **TELC B1 target lens**. Broad Corpus evidence must not cause the App to train generic B1 patterns at the expense of TELC-relevant behavior near the target exam.

## 7. Cost Notes

Stage 01 itself creates **no required recurring AI or infrastructure cost**. The thesis deliberately avoids defining the coach as a permanently open generative conversation, which would turn product identity into an always-on cost obligation.

Preferred low-cost defaults for later shaping are:

- deterministic recommendation/scoring logic where it is reliable;
- precomputed and cached Corpus intelligence;
- reusable explanations/templates for common repair patterns;
- batching and caching of generated content/evaluations;
- local/open-source or cheaper models for low-risk classification/transcription where quality is sufficient;
- premium model calls only for cases such as difficult writing/speaking evaluation or generation where cheaper approaches fail quality requirements.

A more expensive capability is justified only when it materially improves diagnosis, practice quality, readiness reliability, or learner outcome. Later stages must define invocation conditions and fallback behavior rather than assuming premium AI for every task.

## 8. Decisions Made

1. Locked the one-sentence product definition and value proposition.
2. Confirmed the learner-facing identity as **personal German exam coach**.
3. Locked the optimization objective: improve the probability of passing **TELC B1** using honest evidence and efficient study time.
4. Confirmed exam-led German learning rather than traditional course progression.
5. Defined the primary learner as someone who may start around A1, intends to reach/pass B1, and prioritizes certification efficiency over broad curriculum mastery.
6. Set **TELC B1 as the only launch target**, while preserving cheap conceptual seams for future exam targets without building multi-exam scope now.
7. Defined explicit non-goals that prevent drift into a course, generic tutor, flashcard app, catalog, mock-only app, gamified engagement product, or always-on AI companion.
8. Defined product success around real exam outcomes, readiness calibration, written/oral safety, transfer, retention, increasing realism, study efficiency, and evidence coverage—not streaks or activity volume.
9. Converted the exam-coach identity into concrete product rules for recommendation, diagnosis, repair, evidence, feedback, uncertainty, Corpus usage, cost, and extensibility.

## 9. Open Questions / Deferred Decisions

### Open owner questions

**None.** Stage 01 can be responsibly decided from the existing product context.

### Deferred product decisions

The following are intentionally deferred to their dedicated shaping stages rather than left ambiguous:

- exact diagnostic composition and duration — Stage 03;
- learner-model schema and mastery mechanics — Stage 04;
- daily session duration and prioritization formula — Stage 06;
- assistance ladder and removal rules — Stage 08;
- skill-specific TELC task mapping and coaching behavior — Stages 09–13;
- exact readiness representation, weighting, minimum evidence, bands, and calibration — Stage 15;
- mock cadence and scoring — Stage 16;
- exact ready-to-book threshold and exam-date preparation modes — Stage 17;
- detailed bilingual coach language policy — Stage 18;
- navigation and screen structure — Stage 19;
- exact gamification choices — Stage 20;
- generated-content and AI evaluation policies — Stage 21 and related later stages.

These deferrals do not block Stage 01 because the governing product principles are now fixed.

## 10. Definition of Done Check

- [x] Finalize the one-sentence product definition.
- [x] Confirm the identity: **personal German exam coach**.
- [x] Confirm the objective: **maximize the learner's probability of passing TELC B1**.
- [x] Confirm that German is learned **through exam preparation**, not a traditional course curriculum.
- [x] Confirm the initial learner profile:
  - [x] may start around A1,
  - [x] intends to reach/pass B1,
  - [x] prioritizes certification over broad language mastery.
- [x] Decide whether TELC B1 is the only initial target or the first target in an expandable exam framework.
- [x] Define what Bestehen intentionally does *not* try to be.
- [x] Define product success beyond engagement and streaks.
- [x] Translate the exam-coach identity into concrete product rules.
- [x] Identify recurring-cost implications and preserve a low-cost default.

**Stage 01 is complete when every major feature can be challenged with one question: _Does this improve evidence-backed TELC B1 exam readiness?_**
