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

- [ ] Define the readiness threshold.
- [ ] Require adequate written evidence.
- [ ] Require adequate oral evidence.
- [ ] Require recent performance.
- [ ] Require enough unassisted/timed evidence.
- [ ] Decide whether consistency across several mocks is required.
- [ ] Define confidence language.
- [ ] Define coaching when the learner is close but not ready.
- [ ] Define final preparation once the exam is booked.
- [ ] Define 21-day and 7-day preparation modes.

**Done when:** “Book your exam” is earned from evidence, not motivational copy.

---

## 18. Define the Coach Personality and Behavior

- [ ] Apply the Bestehen identity consistently.
- [ ] Define how the coach recommends, corrects, warns, encourages, and explains uncertainty.
- [ ] Define phrases and styles to avoid.
- [ ] Decide German vs English usage by learner stage.
- [ ] Define gradual increase of German in explanations.
- [ ] Define tone after poor performance.
- [ ] Define tone after improvement.
- [ ] Define tone when the learner is ready.
- [ ] Define how personalized the coach feels.
- [ ] Decide whether the coach has a separate character/name or remains “Bestehen.”

**Done when:** UI copy and AI behavior feel like one coherent exam coach.

---

## 19. Define Information Architecture and Core Screens

- [ ] Define primary navigation.
- [ ] Define Home / Coach screen.
- [ ] Define Readiness dashboard.
- [ ] Define Today's Session.
- [ ] Define Attempt experience.
- [ ] Define Diagnosis/Repair experience.
- [ ] Define Review area.
- [ ] Define Skill/Weakness detail.
- [ ] Define Mock Exam area.
- [ ] Define Exam Date/Goal.
- [ ] Define Progress/history.
- [ ] Define Settings.
- [ ] Decide how much source/Corpus information learners see.
- [ ] Keep “What should I do today?” as the dominant journey.

**Done when:** Every core capability has a clear home without becoming a dense LMS.

---

## 20. Define Progress and Motivation

- [ ] Confirm Readiness as the primary progress concept.
- [ ] Decide whether streaks are needed.
- [ ] Decide whether XP is needed.
- [ ] Decide whether achievements are needed.
- [ ] Ensure any gamification stays secondary to exam readiness.
- [ ] Define meaningful milestones:
  - [ ] initial diagnostic,
  - [ ] first section in pass range,
  - [ ] oral pass range,
  - [ ] written pass range,
  - [ ] first passing mock,
  - [ ] consistent passing mocks,
  - [ ] ready to book.
- [ ] Define weekly progress summaries.
- [ ] Define how regressions are communicated.

**Done when:** Motivation reinforces preparation rather than replacing it with arbitrary game mechanics.

---

## 21. Define the Content Strategy

- [ ] Define the relationship between Corpus and App content.
- [ ] Define what can be shown verbatim.
- [ ] Define when original exercises are generated.
- [ ] Define generation patterns grounded in Corpus evidence.
- [ ] Define generated-content QA.
- [ ] Define answer validation.
- [ ] Define difficulty controls.
- [ ] Define anti-repetition rules.
- [ ] Ensure generated reading passages remain natural German.
- [ ] Define generated-audio requirements.
- [ ] Define writing/speaking prompt generation requirements.
- [ ] Define content refresh/rotation.
- [ ] Define source attribution rules where needed.

**Done when:** Bestehen has enough high-quality practice without depending on redistributing copyrighted exam material.

---

## 22. Define Corpus → App Product Contract

- [ ] Define what the App requests from Corpus.
- [ ] Define what Corpus returns.
- [ ] Define how the App uses:
  - [ ] task patterns,
  - [ ] topic frequency,
  - [ ] vocabulary frequency,
  - [ ] grammar frequency,
  - [ ] difficulty,
  - [ ] TELC relevance,
  - [ ] distractor patterns,
  - [ ] skill relationships.
- [ ] Decide whether App needs raw/reference source access.
- [ ] Define behavior if Corpus lacks enough evidence.
- [ ] Define version compatibility expectations.

**Done when:** The two products can evolve independently without ambiguity about their responsibilities.

---

## 23. Define Notifications, Scheduling, and Habit Support

- [ ] Define reminder types.
- [ ] Define configurable study schedule.
- [ ] Define due-review reminders.
- [ ] Define mock-exam reminders.
- [ ] Define exam-date urgency reminders.
- [ ] Avoid shame-based missed-day messaging.
- [ ] Define quiet hours.
- [ ] Define notification frequency caps.
- [ ] Define behavior when the learner ignores reminders.
- [ ] Keep reminders tied to preparation value, not generic engagement.

**Done when:** Habit support helps the learner prepare without becoming noisy or manipulative.

---

## 24. Define Account, Data, and Portability Expectations

- [ ] Decide whether sign-in is required initially.
- [ ] Define learner profile data.
- [ ] Define progress/evidence history retention.
- [ ] Define audio retention expectations.
- [ ] Define generated-content retention.
- [ ] Define export needs.
- [ ] Define deletion expectations.
- [ ] Define device sync expectations.
- [ ] Define offline expectations.
- [ ] Define privacy-sensitive AI data handling requirements at product level.

**Done when:** Architecture can later make storage/auth choices without inventing the user contract.

---

## 25. Define Accessibility and Device Experience

- [ ] Define launch platforms.
- [ ] Define phone-first vs tablet/desktop expectations.
- [ ] Define keyboard navigation expectations where relevant.
- [ ] Define screen-reader expectations.
- [ ] Define color/contrast requirements.
- [ ] Define text scaling.
- [ ] Define caption/transcript expectations.
- [ ] Define microphone-permission fallback.
- [ ] Define accessibility for timed experiences.
- [ ] Define low-connectivity behavior.

**Done when:** Core exam preparation is usable without architecture later deciding whether accessibility matters.

---

## 26. Define Product Analytics and Evaluation

- [ ] Define core product metrics.
- [ ] Define readiness-calibration metrics.
- [ ] Define learning-outcome metrics.
- [ ] Define repair-success metrics.
- [ ] Define retention metrics separately from learning metrics.
- [ ] Define mock-to-real-exam comparison when outcome data exists.
- [ ] Define feedback/quality sampling.
- [ ] Define AI evaluation quality monitoring.
- [ ] Define content-quality metrics.
- [ ] Define cost-per-active-learner / cost-per-session monitoring.
- [ ] Avoid optimizing only for engagement.

**Done when:** We can later tell whether Bestehen works, not merely whether people use it.

---

## 27. Define Business / Cost Boundaries

- [ ] Confirm personal-project assumptions.
- [ ] Define acceptable recurring-cost philosophy.
- [ ] Decide where premium AI is justified.
- [ ] Define cheap/deterministic fallbacks.
- [ ] Define caching/batching expectations.
- [ ] Define acceptable generated-audio cost strategy.
- [ ] Define storage-cost expectations.
- [ ] Define whether free/paid product tiers matter initially.
- [ ] Avoid design choices that require enterprise-scale infrastructure.

**Done when:** The shaped product can be operated affordably before scale.

---

## 28. Produce the Final Bestehen / App Product Specification

- [ ] Consolidate all shaping documents into a final PRD/spec.
- [ ] Document the complete learner journey.
- [ ] Document the learner model.
- [ ] Document the coaching engine.
- [ ] Document mistake memory.
- [ ] Document A1→B1 progression.
- [ ] Document every exam-skill experience.
- [ ] Document review/spaced repetition.
- [ ] Document TELC readiness.
- [ ] Document mock exams and ready-to-book logic.
- [ ] Document coach personality.
- [ ] Document information architecture.
- [ ] Document content strategy.
- [ ] Document Corpus contract.
- [ ] Document notifications/habit support.
- [ ] Document account/data expectations.
- [ ] Document accessibility/device expectations.
- [ ] Document analytics and cost constraints.
- [ ] Document explicitly deferred features.
- [ ] Separate unresolved architecture questions from unresolved product questions.

### Bestehen / App is fully shaped when:

- [ ] An A1 learner can be described from first launch to exam booking without inventing new major product behavior.
- [ ] Every major skill has a defined coaching experience.
- [ ] Every mistake has a path into future coaching.
- [ ] Readiness is defensible and respects TELC's pass constraints.
- [ ] The coach can explain what to do today and why.
- [ ] Corpus intelligence has a clear role without becoming the learner product.
- [ ] Product success is measurable beyond engagement.
- [ ] Recurring-cost assumptions are explicit and sustainable.
- [ ] No major product decision needs to be invented by the architecture agent.