# Bestehen / App — Product Shaping Checklist

> **Purpose:** Fully shape **Bestehen / App** before architecture and implementation planning.
>
> **End state:** The complete learner journey, coaching model, learning engine, TELC-readiness model, exam experiences, content strategy, UX structure, and success metrics are defined well enough to design and build incrementally without leaving major product decisions to implementation.

---

## 1. Lock the Product Thesis

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

**Done when:** Every major feature can be judged against “Does this improve exam readiness?”

---

## 2. Define the Complete Learner Journey

- [x] Map first visit → “book your exam.”
- [x] Define onboarding.
- [x] Define target/exam-date setup.
- [x] Define initial diagnostic.
- [x] Define first readiness result.
- [x] Define the first recommended session.
- [x] Define daily training.
- [x] Define weekly/monthly progress moments.
- [x] Define transition into realistic exam conditions.
- [x] Define mock-exam cadence.
- [x] Define “you are ready” state.
- [x] Define what happens after readiness is reached.
- [x] Define recovery after a weak mock exam.
- [x] Define return flow after missed days or long absence.

**Done when:** The full learner journey can be storyboarded without inventing new major states.

---

## 3. Design the Initial Diagnostic

- [x] Decide target duration.
- [x] Decide A1/A2/B1 content mix.
- [x] Collect initial evidence for:
  - [x] Reading
  - [x] Language Elements
  - [x] Listening
  - [x] Writing
  - [x] Speaking
- [x] Define a lightweight speaking sample.
- [x] Define a lightweight writing sample.
- [x] Represent uncertainty where evidence is weak.
- [x] Decide whether estimated CEFR level is shown.
- [x] Define how results initialize the learner model.
- [x] Define behavior when the learner is far below real B1 difficulty.

**Done when:** Personalization starts on Day 1 without forcing a long traditional placement test.

---

## 4. Define the Learner Model

- [x] Define grammar mastery.
- [x] Define vocabulary/domain mastery.
- [x] Define reading skills.
- [x] Define listening skills.
- [x] Define writing competencies.
- [x] Define speaking competencies.
- [x] Define exam-strategy skills.
- [x] Define topic familiarity.
- [x] Define mistake history.
- [x] Define recurrence frequency.
- [x] Define recency/decay.
- [x] Define confidence in each estimate.
- [x] Separate assisted vs unassisted performance.
- [x] Separate timed vs untimed performance.
- [x] Separate passive understanding from productive ability.
- [x] Connect learner skills to the Corpus skill graph.

**Done when:** “Weak at listening” becomes a useful set of specific, measurable skill states.

---

## 5. Define Mistake Memory

- [x] Define a mistake event.
- [x] Classify mistakes:
  - [x] vocabulary gap,
  - [x] grammar gap,
  - [x] listening-recognition failure,
  - [x] misunderstanding,
  - [x] exam-strategy error,
  - [x] attention/careless error,
  - [x] production error.
- [x] Define how repeated mistakes gain priority.
- [x] Define how resolved weaknesses lose priority.
- [x] Allow mistakes in one modality to influence another when relevant.
- [x] Define recurring-mistake explanations.
- [x] Define when a mistake becomes a known weakness.
- [x] Define when a weakness is repaired.
- [x] Define spaced return of old mistakes.

**Done when:** Every wrong answer improves future coaching.

---

## 6. Define the Daily Coaching Engine

- [x] Choose default daily session duration.
- [x] Support configurable session lengths.
- [x] Define the optimization objective for session assembly.
- [x] Balance:
  - [x] exam weighting,
  - [x] weakest areas,
  - [x] spaced review,
  - [x] skill freshness,
  - [x] learner fatigue,
  - [x] exam-date urgency,
  - [x] section coverage.
- [x] Define focused vs mixed-session logic.
- [x] Define how mock exams affect upcoming sessions.
- [x] Define how a fixed exam date changes priorities.
- [x] Allow learner override without destroying personalization.
- [x] Explain “why this today?”
- [x] Define partial-session completion behavior.

**Done when:** Given a learner state and 25 minutes, Bestehen can explain exactly why it chose today's work.

---

## 7. Lock the Core Learning Loop

- [x] Finalize: **Observe → Attempt → Diagnose → Repair → Retry → Remember**.
- [x] Define each step in the UI.
- [x] Define when steps may be skipped.
- [x] Define expected repair duration.
- [x] Ensure retry uses fresh equivalent content.
- [x] Define success criteria for a repaired weakness.
- [x] Define the loop for:
  - [x] objective questions,
  - [x] listening,
  - [x] writing,
  - [x] speaking.
- [x] Define how assistance is offered without turning every activity into a full lesson.

**Done when:** Every activity follows one consistent coaching philosophy.

---

## 8. Design the A1 → B1 Progression Model

- [x] Define difficulty stages without traditional course chapters.
- [x] Define the assisted A1/early-A2 experience.
- [x] Decide assistance types:
  - [x] word translation,
  - [x] sentence explanation,
  - [x] grammar hints,
  - [x] vocabulary preview,
  - [x] slowed audio,
  - [x] replay,
  - [x] answer hints.
- [x] Define how assistance is gradually removed.
- [x] Define transition into genuine A2 complexity.
- [x] Define transition into A2/B1 material.
- [x] Define transition into genuine B1 complexity.
- [x] Define when timing is introduced.
- [x] Define when replays/retries become exam-realistic.
- [x] Make progression skill-specific rather than one global level.
- [x] Define fallback behavior when a learner hits a difficulty wall.

**Done when:** An A1 learner can start immediately while the destination remains authentic B1 exam performance.

---

## 9. Define Reading Coaching

- [x] Map TELC B1 reading task types.
- [x] Define lower-difficulty variants.
- [x] Map each task to specific reading skills.
- [x] Define vocabulary assistance.
- [x] Define synonym-recognition training.
- [x] Define scanning vs detailed-comprehension practice.
- [x] Define distractor explanations.
- [x] Define timed and untimed modes.
- [x] Define repair after reading mistakes.
- [x] Define reference-material vs generated-content use.

**Done when:** Reading develops both German comprehension and TELC solving strategy.

---

## 10. Define Language Elements / Sprachbausteine Coaching

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

**Done when:** Grammar is taught because it wins exam points, not because it belongs to a chapter.

---

## 11. Define Listening Coaching

- [x] Map TELC B1 listening task types.
- [x] Define audio source strategy.
- [x] Decide generated vs human/native-recorded audio policy.
- [x] Define speech-speed progression.
- [x] Define replay rules by stage.
- [x] Define transcript availability.
- [x] Define pre-listening vocabulary assistance.
- [x] Diagnose:
  - [x] unknown vocabulary,
  - [x] numbers/dates/times,
  - [x] speed,
  - [x] distractors,
  - [x] missed negation,
  - [x] inference.
- [x] Define targeted listening repair.
- [x] Define audio difficulty scoring.
- [x] Define exam-realistic listening mode.

**Done when:** Bestehen can diagnose *why* the learner failed to understand audio.

---

## 12. Define Writing Coaching

- [x] Map current TELC B1 writing format and scoring dimensions.
- [x] Define prompt categories.
- [x] Represent required content points explicitly.
- [x] Define evaluation dimensions:
  - [x] task completion,
  - [x] communicative success,
  - [x] structure,
  - [x] vocabulary,
  - [x] grammar,
  - [x] register,
  - [x] greeting/closing where relevant.
- [x] Evaluate against **B1 sufficiency**, not ideal/native German.
- [x] Decide correction presentation.
- [x] Limit the number of corrections emphasized at once.
- [x] Define repair-and-rewrite flow.
- [x] Define reusable patterns/templates responsibly.
- [x] Define timed writing mode.
- [x] Define how writing affects readiness.

**Done when:** The coach can answer: “Would this likely be good enough for B1?”

---

## 13. Define Speaking Coaching

- [x] Map all TELC B1 speaking parts.
- [x] Define solo practice for each part.
- [x] Define AI partner behavior for interactive tasks.
- [x] Define voice input requirements.
- [x] Define transcript behavior.
- [x] Define evaluation dimensions:
  - [x] task completion,
  - [x] interaction,
  - [x] fluency,
  - [x] vocabulary,
  - [x] grammar,
  - [x] intelligibility/pronunciation.
- [x] Avoid over-penalizing accent.
- [x] Define useful phrase/structure recommendations.
- [x] Define turn-taking behavior.
- [x] Define planning-together scenarios.
- [x] Define exam-like preparation time.
- [x] Define timed speaking simulation.
- [x] Feed speaking into the independent oral pass model.

**Done when:** Speaking feels like rehearsal with an exam coach and partner, not generic chatbot conversation.

---

## 14. Define Review and Spaced Repetition

- [x] Decide what enters review:
  - [x] vocabulary,
  - [x] grammar patterns,
  - [x] useful phrases,
  - [x] listening distinctions,
  - [x] writing mistakes,
  - [x] speaking corrections,
  - [x] exam strategies.
- [x] Define scheduling principles.
- [x] Weight review priority by TELC relevance.
- [x] Define behavior after repeated failure.
- [x] Let successful productive use improve mastery more strongly where appropriate.
- [x] Define quick-review formats.
- [x] Blend review into daily coaching rather than building a separate flashcard product.

**Done when:** Important mistakes reliably return until they are retained.

---

## 15. Design TELC Readiness

- [x] Define exactly what **Readiness** means.
- [x] Decide primary representation:
  - [x] pass probability — future calibrated secondary output; intentionally withheld pre-calibration,
  - [x] readiness index — launch primary numeric representation,
  - [x] predicted score — launch written/oral supporting estimate and range,
  - [x] or a combination — **selected launch approach**.
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

**Done when:** Readiness is defensible, not a decorative progress bar.

---

## 16. Define Mock Exams

- [x] Define full mocks.
- [x] Define section-only mocks.
- [x] Define mini-mocks.
- [x] Define exam-realistic timing.
- [x] Define pause/resume behavior.
- [x] Define listening playback restrictions.
- [x] Define speaking simulation.
- [x] Define scoring.
- [x] Define post-exam analysis.
- [x] Feed mock mistakes into the learner model.
- [x] Define when the coach recommends another mock.
- [x] Define how many passing mocks contribute to readiness.
- [x] Distinguish source/reference exams from generated simulations.
- [x] Ensure mocks respect content-usage restrictions.

**Done when:** Learners can rehearse actual exam structure and pressure before booking.

---

## 17. Define “Ready to Book” Logic

- [x] Define the readiness threshold.
- [x] Require adequate written evidence.
- [x] Require adequate oral evidence.
- [x] Require recent performance.
- [x] Require enough unassisted/timed evidence.
- [x] Decide whether consistency across several mocks is required.
- [x] Define confidence language.
- [x] Define coaching when the learner is close but not ready.
- [x] Define final preparation once the exam is booked.
- [x] Define 21-day and 7-day preparation modes.

**Done when:** “Book your exam” is earned from evidence, not motivational copy.

---

## 18. Define the Coach Personality and Behavior

- [x] Apply the Bestehen identity consistently.
- [x] Define how the coach recommends, corrects, warns, encourages, and explains uncertainty.
- [x] Define phrases and styles to avoid.
- [x] Decide German vs English usage by learner stage.
- [x] Define gradual increase of German in explanations.
- [x] Define tone after poor performance.
- [x] Define tone after improvement.
- [x] Define tone when the learner is ready.
- [x] Define how personalized the coach feels.
- [x] Decide whether the coach has a separate character/name or remains “Bestehen.”

**Done when:** UI copy and AI behavior feel like one coherent exam coach.

---

## 19. Define Information Architecture and Core Screens

- [x] Define primary navigation.
- [x] Define Home / Coach screen.
- [x] Define Readiness dashboard.
- [x] Define Today's Session.
- [x] Define Attempt experience.
- [x] Define Diagnosis/Repair experience.
- [x] Define Review area.
- [x] Define Skill/Weakness detail.
- [x] Define Mock Exam area.
- [x] Define Exam Date/Goal.
- [x] Define Progress/history.
- [x] Define Settings.
- [x] Decide how much source/Corpus information learners see.
- [x] Keep “What should I do today?” as the dominant journey.

**Done when:** Every core capability has a clear home without becoming a dense LMS.

---

## 20. Define Progress and Motivation

- [x] Confirm Readiness as the primary progress concept.
- [x] Decide whether streaks are needed.
- [x] Decide whether XP is needed.
- [x] Decide whether achievements are needed.
- [x] Ensure any gamification stays secondary to exam readiness.
- [x] Define meaningful milestones:
  - [x] initial diagnostic,
  - [x] first section in pass range,
  - [x] oral pass range,
  - [x] written pass range,
  - [x] first passing mock,
  - [x] consistent passing mocks,
  - [x] ready to book.
- [x] Define weekly progress summaries.
- [x] Define how regressions are communicated.

**Done when:** Motivation reinforces preparation rather than replacing it with arbitrary game mechanics.

---

## 21. Define the Content Strategy

- [x] Define the relationship between Corpus and App content.
- [x] Define what can be shown verbatim.
- [x] Define when original exercises are generated.
- [x] Define generation patterns grounded in Corpus evidence.
- [x] Define generated-content QA.
- [x] Define answer validation.
- [x] Define difficulty controls.
- [x] Define anti-repetition rules.
- [x] Ensure generated reading passages remain natural German.
- [x] Define generated-audio requirements.
- [x] Define writing/speaking prompt generation requirements.
- [x] Define content refresh/rotation.
- [x] Define source attribution rules where needed.

**Done when:** Bestehen has enough high-quality practice without depending on redistributing copyrighted exam material.

---

## 22. Define User Controls vs Coach Autonomy + Corpus → App Product Contract

> **Stage continuity note:** The Stage 22 agent prompt defines **User Controls vs Coach Autonomy**, while this checklist previously named Stage 22 **Corpus → App Product Contract**. Stage 22 now covers both; decisions are documented in `app/22-user-controls-vs-coach-autonomy.md`.

### User controls vs coach autonomy

- [x] List what the coach controls automatically.
- [x] List what learners can override.
- [x] Define learner controls for:
  - [x] section / skill,
  - [x] duration,
  - [x] difficulty / realism,
  - [x] mocks,
  - [x] review,
  - [x] assistance.
- [x] Define **Coach me** versus **Just practice X** paths.
- [x] Define how overrides affect personalization.
- [x] Define how overrides affect evidence and Readiness.
- [x] Define how the App explains deviations from its recommendation.
- [x] Prevent excessive settings from weakening the coach identity.

### Corpus → App product contract

- [x] Define what the App requests from Corpus.
- [x] Define what Corpus returns.
- [x] Define how the App uses:
  - [x] task patterns,
  - [x] topic frequency,
  - [x] vocabulary frequency,
  - [x] grammar frequency,
  - [x] difficulty,
  - [x] TELC relevance,
  - [x] distractor patterns,
  - [x] skill relationships.
- [x] Decide whether App needs raw/reference source access.
- [x] Define behavior if Corpus lacks enough evidence.
- [x] Define version compatibility expectations.

**Done when:** The coach owns the strong default without trapping the learner, learner overrides preserve evidence truth, and Corpus/App responsibilities remain unambiguous.

---

## 23. Define Exam-Date and Urgency Behavior + Notifications, Scheduling, and Habit Support

> **Stage continuity note:** The Stage 23 agent prompt defines **Exam-Date and Urgency Behavior**, while this checklist previously named Stage 23 **Notifications, Scheduling, and Habit Support**. Stage 23 now covers both; decisions are documented in `app/23-exam-date-and-urgency.md`.

- [x] Define reminder types.
- [x] Define configurable study schedule.
- [x] Define due-review reminders.
- [x] Define mock-exam reminders.
- [x] Define exam-date urgency reminders.
- [x] Avoid shame-based missed-day messaging.
- [x] Define quiet hours.
- [x] Define notification frequency caps.
- [x] Define behavior when the learner ignores reminders.
- [x] Keep reminders tied to preparation value, not generic engagement.

**Done when:** Urgency changes the coaching plan without changing readiness truth, and habit support helps the learner prepare without becoming noisy or manipulative.

---

## 24. Define Analytics and Product Success Metrics + Account, Data, and Portability Expectations

> **Stage continuity note:** The Stage 24 agent prompt defines **Analytics and Product Success Metrics**, while this checklist previously named Stage 24 **Account, Data, and Portability Expectations**. Stage 24 now covers both; decisions are documented in `app/24-analytics-and-success-metrics.md`.

### Analytics and product success metrics

- [x] Define the north-star metric.
- [x] Define learner-outcome metrics.
- [x] Define readiness-accuracy and calibration metrics.
- [x] Define skill-improvement and repair/retention metrics.
- [x] Define session-value metrics without optimizing time-on-screen.
- [x] Define content-quality metrics.
- [x] Define Writing/Speaking evaluation-consistency monitoring.
- [x] Define future mock-to-real-exam comparison.
- [x] Define optional actual exam-result collection and calibration use.
- [x] Separate retention/engagement metrics from learning metrics.
- [x] Define minimum analytics suitable for a personal project and what can wait.
- [x] Define cost-per-active-learner / cost-per-session monitoring.
- [x] Keep observability/privacy/cost proportional and avoid optimizing only for engagement.

### Account, data, and portability expectations

- [x] Decide whether sign-in is required initially.
- [x] Define learner profile data.
- [x] Define progress/evidence history retention.
- [x] Define audio retention expectations.
- [x] Define generated-content retention.
- [x] Define export needs.
- [x] Define deletion expectations.
- [x] Define device sync expectations.
- [x] Define offline expectations.
- [x] Define privacy-sensitive AI data handling requirements at product level.

**Done when:** Bestehen can be measured against learner readiness and eventual exam outcomes, while architecture can later make analytics/storage/auth choices without inventing the success model or user-data contract.

---

## 25. Define Business Model and Product Boundaries + Accessibility and Device Experience

> **Stage continuity note:** The Stage 25 agent prompt defines **Business Model and Product Boundaries**, while this checklist previously named Stage 25 **Accessibility and Device Experience** and placed overlapping business/cost work at Stage 27. Stage 25 now covers both; decisions are documented in `app/25-business-model-and-product-boundaries.md`.

### Business model and product boundaries

- [x] Confirm the private/free initial state.
- [x] Define optional future free/paid principles without prematurely choosing a subscription model.
- [x] Identify expensive AI capabilities that may require quotas/limits later.
- [x] Define non-negotiable core coaching features that monetization must not cripple.
- [x] Define future quota/fallback behavior without changing evidence truth.
- [x] Preserve account/data portability and learner-data retention/deletion expectations across commercial states.
- [x] Define product boundaries and explicitly deferred commercial features.

### Accessibility and device experience

- [x] Define launch platforms.
- [x] Define phone-first vs tablet/desktop expectations.
- [x] Define keyboard navigation expectations where relevant.
- [x] Define screen-reader expectations.
- [x] Define color/contrast requirements.
- [x] Define text scaling.
- [x] Define caption/transcript expectations.
- [x] Define microphone-permission fallback.
- [x] Define accessibility for timed experiences.
- [x] Define low-connectivity behavior.

**Done when:** Core exam preparation is accessible across the launch device model, and public monetization could be added without changing readiness truth or crippling pass-critical coaching.

---

## 26. Define Accessibility, Platform, and Non-Functional Expectations

> **Stage continuity note:** The current Stage 26 agent prompt defines **Accessibility, Platform, and Non-Functional Expectations**, while this checklist previously named Stage 26 **Product Analytics and Evaluation**. The analytics/evaluation decisions were already completed by Stage 24 and remain authoritative in `app/24-analytics-and-success-metrics.md`. The deeper platform/non-functional decisions are documented in `app/26-platform-accessibility-nonfunctional.md`.

### Accessibility, platform, and non-functional expectations

- [x] Confirm responsive web as the launch platform and define mobile-browser priorities.
- [x] Define phone, tablet, and desktop/laptop experience expectations.
- [x] Define supported modern browser families and unsupported-browser degradation.
- [x] Define microphone permission, recording, audio-output, preflight, and fallback behavior.
- [x] Define keyboard navigation and screen-reader behavior.
- [x] Preserve WCAG 2.2 AA contrast, text-scaling/reflow, reduced-motion, caption/transcript, and timed-accessibility expectations.
- [x] Define acceptable deterministic-feedback latency.
- [x] Define acceptable AI-evaluation and adaptive-speaking latency plus pending/fallback behavior.
- [x] Define offline and low-connectivity expectations.
- [x] Define voice/audio privacy and raw-recording retention behavior.
- [x] Define reliability expectations for ordinary practice and timed P4/mock work.
- [x] Define measured-block preflight, response checkpointing, timer, crash/reload, media, network, partner, and evaluator failure behavior.
- [x] Separate launch requirements, acceptable degradations, and later enhancements.
- [x] Balance quality/reliability against personal-project cost and implementation complexity.

### Legacy Product Analytics and Evaluation continuity — resolved by Stage 24

- [x] Define core product metrics — `app/24-analytics-and-success-metrics.md`.
- [x] Define readiness-calibration metrics — `app/24-analytics-and-success-metrics.md`.
- [x] Define learning-outcome metrics — `app/24-analytics-and-success-metrics.md`.
- [x] Define repair-success metrics — `app/24-analytics-and-success-metrics.md`.
- [x] Define retention metrics separately from learning metrics — `app/24-analytics-and-success-metrics.md`.
- [x] Define mock-to-real-exam comparison when outcome data exists — `app/24-analytics-and-success-metrics.md`.
- [x] Define feedback/quality sampling — learner reports, benchmark QA, and selective stronger/human review are defined in `app/24-analytics-and-success-metrics.md`.
- [x] Define AI evaluation quality monitoring — `app/24-analytics-and-success-metrics.md`.
- [x] Define content-quality metrics — `app/24-analytics-and-success-metrics.md`.
- [x] Define cost-per-active-learner / cost-per-session monitoring — `app/24-analytics-and-success-metrics.md`.
- [x] Avoid optimizing only for engagement — `app/24-analytics-and-success-metrics.md`.

**Done when:** Architecture can later choose technical mechanisms without inventing browser, accessibility, microphone/audio, latency, offline, voice-privacy, or timed-mock reliability behavior, and the repository retains one authoritative analytics model rather than duplicating Stage 24.

---

## 27. Validate with End-to-End Scenarios + Legacy Business / Cost Boundaries

> **Stage continuity note:** The current Stage 27 agent prompt defines **Validate with End-to-End Scenarios**, while this checklist previously named Stage 27 **Business / Cost Boundaries**. Stage 25 already resolved the business/cost requirements in `app/25-business-model-and-product-boundaries.md`. Stage 27 now preserves that completed continuity section and adds the prompt-defined system validation documented in `app/27-end-to-end-scenario-validation.md`.

### End-to-end scenario validation

- [x] Validate the A1 Day-1 scenario.
- [x] Validate the A2 midpoint scenario.
- [x] Validate the strong-Reading / weak-Speaking scenario.
- [x] Validate the 30-day deadline scenario.
- [x] Validate the return-after-break scenario.
- [x] Validate the failed-mock scenario.
- [x] Validate the Speaking coaching scenario.
- [x] Validate the Writing-repair scenario.
- [x] Validate the Ready-to-Book scenario.
- [x] For every scenario, document learner state, coach decision, selected activities, evidence updates, readiness changes, and messaging.
- [x] Identify contradictions, missing rules, and cross-stage composition issues.
- [x] Define cross-stage precedence rules for validity, direct evidence, pass risk, uncertainty, repair/review, deadline urgency, progression, and learner preference.
- [x] Assess whether earlier shaping documents require amendment; validation found no contradictory or missing single-stage rule requiring a reversal/amendment.
- [x] Keep a cross-stage correction/change log.
- [x] Validate technical/content/evaluator failure handling and pending evidence.
- [x] Validate learner overrides without corrupting evidence semantics.
- [x] Validate return-after-break behavior when deadline urgency also applies.
- [x] Validate that all scenarios preserve the personal-project low-cost model and bounded premium-AI use.

### Legacy business/cost continuity — resolved early by Stage 25

- [x] Confirm personal-project assumptions.
- [x] Define acceptable recurring-cost philosophy.
- [x] Decide where premium AI is justified.
- [x] Define cheap/deterministic fallbacks.
- [x] Define caching/batching expectations.
- [x] Define acceptable generated-audio cost strategy.
- [x] Define storage-cost expectations.
- [x] Define whether free/paid product tiers matter initially.
- [x] Avoid design choices that require enterprise-scale infrastructure.

**Done when:** The complete shaped App survives representative journeys from A1 Day-1 through Ready to Book without inventing contradictory behavior, and it remains affordable before scale.

---

## 28. Produce the Final Bestehen / App Product Specification

- [x] Consolidate all shaping documents into a final PRD/spec.
- [x] Document the complete learner journey.
- [x] Document the learner model.
- [x] Document the coaching engine.
- [x] Document mistake memory.
- [x] Document A1→B1 progression.
- [x] Document every exam-skill experience.
- [x] Document review/spaced repetition.
- [x] Document TELC readiness.
- [x] Document mock exams and ready-to-book logic.
- [x] Document coach personality.
- [x] Document information architecture.
- [x] Document content strategy.
- [x] Document Corpus contract.
- [x] Document notifications/habit support.
- [x] Document account/data expectations.
- [x] Document accessibility/device expectations.
- [x] Document analytics and cost constraints.
- [x] Document explicitly deferred features.
- [x] Separate unresolved architecture questions from unresolved product questions.

### Bestehen / App is fully shaped when:

- [x] An A1 learner can be described from first launch to exam booking without inventing new major product behavior.
- [x] Every major skill has a defined coaching experience.
- [x] Every mistake has a path into future coaching.
- [x] Readiness is defensible and respects TELC's pass constraints.
- [x] The coach can explain what to do today and why.
- [x] Corpus intelligence has a clear role without becoming the learner product.
- [x] Product success is measurable beyond engagement.
- [x] Recurring-cost assumptions are explicit and sustainable.
- [x] No major product decision needs to be invented by the architecture agent.