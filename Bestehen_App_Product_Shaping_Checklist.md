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

- [ ] Define grammar mastery.
- [ ] Define vocabulary/domain mastery.
- [ ] Define reading skills.
- [ ] Define listening skills.
- [ ] Define writing competencies.
- [ ] Define speaking competencies.
- [ ] Define exam-strategy skills.
- [ ] Define topic familiarity.
- [ ] Define mistake history.
- [ ] Define recurrence frequency.
- [ ] Define recency/decay.
- [ ] Define confidence in each estimate.
- [ ] Separate assisted vs unassisted performance.
- [ ] Separate timed vs untimed performance.
- [ ] Separate passive understanding from productive ability.
- [ ] Connect learner skills to the Corpus skill graph.

**Done when:** “Weak at listening” becomes a useful set of specific, measurable skill states.

---

## 5. Define Mistake Memory

- [ ] Define a mistake event.
- [ ] Classify mistakes:
  - [ ] vocabulary gap,
  - [ ] grammar gap,
  - [ ] listening-recognition failure,
  - [ ] misunderstanding,
  - [ ] exam-strategy error,
  - [ ] attention/careless error,
  - [ ] production error.
- [ ] Define how repeated mistakes gain priority.
- [ ] Define how resolved weaknesses lose priority.
- [ ] Allow mistakes in one modality to influence another when relevant.
- [ ] Define recurring-mistake explanations.
- [ ] Define when a mistake becomes a known weakness.
- [ ] Define when a weakness is repaired.
- [ ] Define spaced return of old mistakes.

**Done when:** Every wrong answer improves future coaching.

---

## 6. Define the Daily Coaching Engine

- [ ] Choose default daily session duration.
- [ ] Support configurable session lengths.
- [ ] Define the optimization objective for session assembly.
- [ ] Balance:
  - [ ] exam weighting,
  - [ ] weakest areas,
  - [ ] spaced review,
  - [ ] skill freshness,
  - [ ] learner fatigue,
  - [ ] exam-date urgency,
  - [ ] section coverage.
- [ ] Define focused vs mixed-session logic.
- [ ] Define how mock exams affect upcoming sessions.
- [ ] Define how a fixed exam date changes priorities.
- [ ] Allow learner override without destroying personalization.
- [ ] Explain “why this today?”
- [ ] Define partial-session completion behavior.

**Done when:** Given a learner state and 25 minutes, Bestehen can explain exactly why it chose today's work.

---

## 7. Lock the Core Learning Loop

- [ ] Finalize: **Observe → Attempt → Diagnose → Repair → Retry → Remember**.
- [ ] Define each step in the UI.
- [ ] Define when steps may be skipped.
- [ ] Define expected repair duration.
- [ ] Ensure retry uses fresh equivalent content.
- [ ] Define success criteria for a repaired weakness.
- [ ] Define the loop for:
  - [ ] objective questions,
  - [ ] listening,
  - [ ] writing,
  - [ ] speaking.
- [ ] Define how assistance is offered without turning every activity into a full lesson.

**Done when:** Every activity follows one consistent coaching philosophy.

---

## 8. Design the A1 → B1 Progression Model

- [ ] Define difficulty stages without traditional course chapters.
- [ ] Define the assisted A1/early-A2 experience.
- [ ] Decide assistance types:
  - [ ] word translation,
  - [ ] sentence explanation,
  - [ ] grammar hints,
  - [ ] vocabulary preview,
  - [ ] slowed audio,
  - [ ] replay,
  - [ ] answer hints.
- [ ] Define how assistance is gradually removed.
- [ ] Define transition into genuine A2 complexity.
- [ ] Define transition into A2/B1 material.
- [ ] Define transition into genuine B1 complexity.
- [ ] Define when timing is introduced.
- [ ] Define when replays/retries become exam-realistic.
- [ ] Make progression skill-specific rather than one global level.
- [ ] Define fallback behavior when a learner hits a difficulty wall.

**Done when:** An A1 learner can start immediately while the destination remains authentic B1 exam performance.

---

## 9. Define Reading Coaching

- [ ] Map TELC B1 reading task types.
- [ ] Define lower-difficulty variants.
- [ ] Map each task to specific reading skills.
- [ ] Define vocabulary assistance.
- [ ] Define synonym-recognition training.
- [ ] Define scanning vs detailed-comprehension practice.
- [ ] Define distractor explanations.
- [ ] Define timed and untimed modes.
- [ ] Define repair after reading mistakes.
- [ ] Define reference-material vs generated-content use.

**Done when:** Reading develops both German comprehension and TELC solving strategy.

---

## 10. Define Language Elements / Sprachbausteine Coaching

- [ ] Map TELC task types.
- [ ] Prioritize grammar concepts by exam relevance.
- [ ] Define conjunction/connector training.
- [ ] Define preposition/case training.
- [ ] Define word-order training.
- [ ] Define vocabulary-in-context training.
- [ ] Keep grammar explanations short and exam-driven.
- [ ] Feed recurring grammar weaknesses into daily review.
- [ ] Define adaptive cloze difficulty.
- [ ] Use Corpus frequency data to influence priority.

**Done when:** Grammar is taught because it wins exam points, not because it belongs to a chapter.

---

## 11. Define Listening Coaching

- [ ] Map TELC B1 listening task types.
- [ ] Define audio source strategy.
- [ ] Decide generated vs human/native-recorded audio policy.
- [ ] Define speech-speed progression.
- [ ] Define replay rules by stage.
- [ ] Define transcript availability.
- [ ] Define pre-listening vocabulary assistance.
- [ ] Diagnose:
  - [ ] unknown vocabulary,
  - [ ] numbers/dates/times,
  - [ ] speed,
  - [ ] distractors,
  - [ ] missed negation,
  - [ ] inference.
- [ ] Define targeted listening repair.
- [ ] Define audio difficulty scoring.
- [ ] Define exam-realistic listening mode.

**Done when:** Bestehen can diagnose *why* the learner failed to understand audio.

---

## 12. Define Writing Coaching

- [ ] Map current TELC B1 writing format and scoring dimensions.
- [ ] Define prompt categories.
- [ ] Represent required content points explicitly.
- [ ] Define evaluation dimensions:
  - [ ] task completion,
  - [ ] communicative success,
  - [ ] structure,
  - [ ] vocabulary,
  - [ ] grammar,
  - [ ] register,
  - [ ] greeting/closing where relevant.
- [ ] Evaluate against **B1 sufficiency**, not ideal/native German.
- [ ] Decide correction presentation.
- [ ] Limit the number of corrections emphasized at once.
- [ ] Define repair-and-rewrite flow.
- [ ] Define reusable patterns/templates responsibly.
- [ ] Define timed writing mode.
- [ ] Define how writing affects readiness.

**Done when:** The coach can answer: “Would this likely be good enough for B1?”

---

## 13. Define Speaking Coaching

- [ ] Map all TELC B1 speaking parts.
- [ ] Define solo practice for each part.
- [ ] Define AI partner behavior for interactive tasks.
- [ ] Define voice input requirements.
- [ ] Define transcript behavior.
- [ ] Define evaluation dimensions:
  - [ ] task completion,
  - [ ] interaction,
  - [ ] fluency,
  - [ ] vocabulary,
  - [ ] grammar,
  - [ ] intelligibility/pronunciation.
- [ ] Avoid over-penalizing accent.
- [ ] Define useful phrase/structure recommendations.
- [ ] Define turn-taking behavior.
- [ ] Define planning-together scenarios.
- [ ] Define exam-like preparation time.
- [ ] Define timed speaking simulation.
- [ ] Feed speaking into the independent oral pass model.

**Done when:** Speaking feels like rehearsal with an exam coach and partner, not generic chatbot conversation.

---

## 14. Define Review and Spaced Repetition

- [ ] Decide what enters review:
  - [ ] vocabulary,
  - [ ] grammar patterns,
  - [ ] useful phrases,
  - [ ] listening distinctions,
  - [ ] writing mistakes,
  - [ ] speaking corrections,
  - [ ] exam strategies.
- [ ] Define scheduling principles.
- [ ] Weight review priority by TELC relevance.
- [ ] Define behavior after repeated failure.
- [ ] Let successful productive use improve mastery more strongly where appropriate.
- [ ] Define quick-review formats.
- [ ] Blend review into daily coaching rather than building a separate flashcard product.

**Done when:** Important mistakes reliably return until they are retained.

---

## 15. Design TELC Readiness

- [ ] Define exactly what **Readiness** means.
- [ ] Decide primary representation:
  - [ ] pass probability,
  - [ ] readiness index,
  - [ ] predicted score,
  - [ ] or a combination.
- [ ] Define written readiness.
- [ ] Define oral readiness separately.
- [ ] Reflect TELC's separate written/oral pass constraints.
- [ ] Define section weights.
- [ ] Define skill weights within sections.
- [ ] Define recency effects.
- [ ] Distinguish assisted from unassisted evidence.
- [ ] Distinguish timed from untimed evidence.
- [ ] Represent uncertainty/confidence.
- [ ] Set minimum evidence before strong predictions.
- [ ] Define how mocks affect readiness.
- [ ] Define initial calibration before real-user outcome data exists.
- [ ] Define future recalibration using actual exam outcomes.
- [ ] Define “not ready,” “borderline,” and “safe pass range.”
- [ ] Explain score changes to the learner.

**Done when:** Readiness is defensible, not a decorative progress bar.

---

## 16. Define Mock Exams

- [ ] Define full mocks.
- [ ] Define section-only mocks.
- [ ] Define mini-mocks.
- [ ] Define exam-realistic timing.
- [ ] Define pause/resume behavior.
- [ ] Define listening playback restrictions.
- [ ] Define speaking simulation.
- [ ] Define scoring.
- [ ] Define post-exam analysis.
- [ ] Feed mock mistakes into the learner model.
- [ ] Define when the coach recommends another mock.
- [ ] Define how many passing mocks contribute to readiness.
- [ ] Distinguish source/reference exams from generated simulations.
- [ ] Ensure mocks respect content-usage restrictions.

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
