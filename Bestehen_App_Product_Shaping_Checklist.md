# Bestehen / App — Product Shaping Checklist

> **Purpose:** Fully shape **Bestehen / App** before architecture and implementation planning.
>
> **End state:** The complete learner journey, coaching model, learning engine, TELC-readiness model, exam experiences, content strategy, UX structure, and success metrics are defined well enough to design and build incrementally without leaving major product decisions to implementation.

---

## 1. Lock the Product Thesis

- [ ] Finalize the one-sentence product definition.
- [ ] Confirm the identity: **personal German exam coach**.
- [ ] Confirm the objective: **maximize the learner's probability of passing TELC B1**.
- [ ] Confirm that German is learned **through exam preparation**, not a traditional course curriculum.
- [ ] Confirm the initial learner profile:
  - [ ] may start around A1,
  - [ ] intends to reach/pass B1,
  - [ ] prioritizes certification over broad language mastery.
- [ ] Decide whether TELC B1 is the only initial target or the first target in an expandable exam framework.
- [ ] Define what Bestehen intentionally does *not* try to be.
- [ ] Define product success beyond engagement and streaks.

**Done when:** Every major feature can be judged against “Does this improve exam readiness?”

---

## 2. Define the Complete Learner Journey

- [ ] Map first visit → “book your exam.”
- [ ] Define onboarding.
- [ ] Define target/exam-date setup.
- [ ] Define initial diagnostic.
- [ ] Define first readiness result.
- [ ] Define the first recommended session.
- [ ] Define daily training.
- [ ] Define weekly/monthly progress moments.
- [ ] Define transition into realistic exam conditions.
- [ ] Define mock-exam cadence.
- [ ] Define “you are ready” state.
- [ ] Define what happens after readiness is reached.
- [ ] Define recovery after a weak mock exam.
- [ ] Define return flow after missed days or long absence.

**Done when:** The full learner journey can be storyboarded without inventing new major states.

---

## 3. Design the Initial Diagnostic

- [ ] Decide target duration.
- [ ] Decide A1/A2/B1 content mix.
- [ ] Collect initial evidence for:
  - [ ] Reading
  - [ ] Language Elements
  - [ ] Listening
  - [ ] Writing
  - [ ] Speaking
- [ ] Define a lightweight speaking sample.
- [ ] Define a lightweight writing sample.
- [ ] Represent uncertainty where evidence is weak.
- [ ] Decide whether estimated CEFR level is shown.
- [ ] Define how results initialize the learner model.
- [ ] Define behavior when the learner is far below real B1 difficulty.

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
- [ ] Define where human-curated gold content is required.
- [ ] Define content-error reporting and correction.

**Done when:** Practice can scale without becoming low-quality AI exercise soup.

---

## 22. Define User Control vs Coach Autonomy

- [ ] Decide what the coach controls automatically.
- [ ] Decide what learners can manually choose:
  - [ ] section,
  - [ ] skill,
  - [ ] duration,
  - [ ] difficulty,
  - [ ] mock exam,
  - [ ] review,
  - [ ] assistance.
- [ ] Define how overrides interact with personalization.
- [ ] Explain deviations from the recommended plan.
- [ ] Provide a “just practice X” path.
- [ ] Keep “coach me” as the default.

**Done when:** Advanced users have control while the default experience remains strongly coached.

---

## 23. Define Exam-Date and Urgency Behavior

- [ ] Define no-exam-date behavior.
- [ ] Define target-month behavior.
- [ ] Define exact-date behavior.
- [ ] Define recommended daily workload.
- [ ] Define behavior when the learner is behind schedule.
- [ ] Define handling of unrealistic deadlines.
- [ ] Define 60-day, 30-day, 21-day, and 7-day modes.
- [ ] Define final-day guidance.
- [ ] Define post-exam state.

**Done when:** The same learner model supports casual preparation and fixed-deadline preparation.

---

## 24. Define Analytics and Product Success Metrics

- [ ] Define learner-outcome metrics.
- [ ] Define readiness-model accuracy metrics.
- [ ] Define mock-to-real-exam correlation once outcome data exists.
- [ ] Define skill-improvement metrics.
- [ ] Define session completion metrics.
- [ ] Define recommendation-following metrics.
- [ ] Define retention metrics without making retention the goal.
- [ ] Define content-quality metrics.
- [ ] Define writing/speaking evaluation consistency metrics.
- [ ] Define a north-star metric centered on exam readiness.
- [ ] Define optional learner reporting of real exam results for calibration.

**Done when:** Product success is measured by improved pass readiness, not just screen time.

---

## 25. Decide Business Model and Product Boundaries

- [ ] Decide whether the initial personal project is private/free.
- [ ] If public later, define free vs paid principles.
- [ ] Identify costly AI capabilities:
  - [ ] speaking,
  - [ ] writing evaluation,
  - [ ] generated audio,
  - [ ] full mocks.
- [ ] Avoid monetization that damages the core coaching loop.
- [ ] Define account/data portability expectations.
- [ ] Define learner data retention/deletion expectations.

**Done when:** The product model supports the intended experience without creating architecture surprises.

---

## 26. Define Platform and Non-Functional Expectations

- [ ] Confirm responsive web as the initial platform.
- [ ] Define mobile-browser priority.
- [ ] Define microphone/browser requirements.
- [ ] Define accessibility expectations.
- [ ] Define keyboard-only behavior.
- [ ] Define audio controls.
- [ ] Define supported browsers/devices.
- [ ] Define acceptable latency for AI feedback.
- [ ] Define offline expectations, if any.
- [ ] Define privacy expectations for voice/audio.
- [ ] Define reliability expectations during timed mocks.

**Done when:** Design and architecture can make informed platform decisions.

---

## 27. Validate with End-to-End Scenarios

- [ ] Write an A1 Day-1 scenario.
- [ ] Write an A2 midpoint scenario.
- [ ] Write a strong-reading / weak-speaking scenario.
- [ ] Write an exam-in-30-days scenario.
- [ ] Write a return-after-3-weeks scenario.
- [ ] Write a failed-mock → repair → retry scenario.
- [ ] Write a speaking-practice scenario.
- [ ] Write a writing-repair scenario.
- [ ] Write a “ready to book” scenario.
- [ ] Verify learner model, readiness model, daily engine, and coach behavior are coherent in every scenario.

**Done when:** The product works as one system rather than a set of individually appealing features.

---

## 28. Produce the Final Product Specification

- [ ] Write the final Bestehen / App PRD.
- [ ] Document the complete learner journey.
- [ ] Document the learner model.
- [ ] Document Mistake Memory.
- [ ] Document the Daily Coaching Engine.
- [ ] Document A1 → B1 progression.
- [ ] Document every exam-section coaching flow.
- [ ] Document Readiness calculation and uncertainty.
- [ ] Document mock exams.
- [ ] Document “ready to book” logic.
- [ ] Document content-generation strategy.
- [ ] Document coach behavior.
- [ ] Document information architecture.
- [ ] Document analytics and success metrics.
- [ ] Document explicit non-goals.
- [ ] Document deferred ideas.
- [ ] Separate remaining architecture questions from unresolved product questions.

### Bestehen / App is fully shaped when:

- [ ] We know **who the learner is and what success means**.
- [ ] We can describe the complete **A1 → B1 → exam-ready journey**.
- [ ] We know **what the learner model stores**.
- [ ] We know **how today's session is chosen**.
- [ ] We know **how mistakes alter future training**.
- [ ] We know **how assistance disappears as ability improves**.
- [ ] Reading, Language Elements, Listening, Writing, and Speaking all have complete coaching flows.
- [ ] We have a defensible **TELC Readiness model**.
- [ ] We know when the coach can say **“you are ready to book the exam.”**
- [ ] The product has a clear **exam-coach voice and UX hierarchy**.
- [ ] The content strategy scales without depending on copying source exams.
- [ ] Representative end-to-end scenarios are internally consistent.
- [ ] No major product decision needs to be invented by the design or architecture agent.
