# Bestehen / App — Stage 19: Information Architecture and Core Screens

> **Status:** Authoritative Stage 19 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **IA promise:** The learner can always find the evidence behind their readiness, but the default product experience remains one clear answer to **“What should I do today?”** rather than a dashboard, course catalog, or dense LMS.

## 1. Purpose and Scope

This document defines the learner-facing information architecture, primary navigation, screen inventory, responsibilities, hierarchy, and primary actions for Bestehen / App.

Earlier stages already define what the product must do: diagnose, coach, remember mistakes, assemble daily work, progress from supported practice to target conditions, evaluate all relevant TELC skills, schedule review, estimate readiness, run mocks, decide when evidence supports booking, and communicate as one calm exam coach. Stage 19 decides **where those capabilities live and how the learner moves among them** without forcing later design or architecture work to invent the product structure.

The stage has one governing product constraint:

**The learner should normally open Bestehen, understand the most important current state in seconds, and have one obvious recommended action.**

The product may expose depth for a learner who wants to inspect evidence, weaknesses, review obligations, mock history, or progress. That depth is secondary to the coach-led daily journey.

This is information architecture and UX structure, not visual design or implementation architecture. It does not lock component libraries, colors, typography, routing technology, state-management patterns, responsive breakpoints, storage, model providers, or notification mechanisms.

### In scope

- primary navigation and route responsibilities;
- Home / Coach;
- Readiness;
- Today’s Session;
- Attempt;
- Diagnosis / Repair;
- Review;
- Skill / Weakness detail;
- Mock Exam;
- Goal / Exam Date;
- Progress / History;
- Settings;
- how Corpus/source information appears to learners;
- responsive/mobile hierarchy priorities;
- cross-screen state and failure behavior;
- cost implications of the learner-facing IA.

### Out of scope

- final visual design system and interaction polish;
- gamification and motivation mechanics beyond preserving Readiness as primary — Stage 20;
- generalized content-generation and attribution rules — Stage 21;
- final Corpus → App payload/API — Stage 22;
- reminder/notification settings and scheduling policy — Stage 23;
- account, retention, sync, export, deletion, and privacy contract — Stage 24;
- launch-platform and accessibility policy — Stage 25;
- analytics instrumentation and experiment design — Stage 26;
- architecture and implementation routing details.

---

## 2. Inputs / Existing Decisions

Stage 19 preserves the shared Product Overview, shared Identity, and App Stages 01–18.

### 2.1 The default journey is coach-led

Stages 01, 02, and 06 establish that Bestehen is not a content catalog. The coach owns prioritization and should answer:

1. **Where am I?**
2. **What is holding me back?**
3. **What should I do next?**

The default daily session is 25 minutes, usually has one dominant priority, and must explain “why this today?”. The learner can override the recommendation without destroying personalization.

### 2.2 The core loop is semantic, not six mandatory screens

Stage 07 establishes **Observe → Attempt → Diagnose → Repair → Retry → Remember**, while explicitly allowing UI compression. Stage 19 therefore does not create six top-level routes or force every loop state onto a separate page. Attempt is visually focused; diagnosis, repair, fresh check, and remember may form one continuous post-attempt coaching flow.

### 2.3 Readiness is central but must not swallow the product

Stage 15 defines the launch representation:

- Readiness band;
- Readiness Index when evidence permits it;
- separate Written and Oral target-performance estimates;
- predicted component score ranges;
- evidence confidence;
- blocker/evidence gap;
- no pass probability before empirical calibration.

The overall index is the weaker of Written and Oral performance estimates. Missing evidence remains unknown rather than zero. Stage 17 further distinguishes **Safe pass range** from **Ready to Book**.

### 2.4 Review is an obligation, not a deck product

Stage 14 defines review as due coaching obligations that are normally blended into daily training and may be satisfied by natural practice. Stage 19 must therefore make review inspectable and directly startable without presenting “clear your cards” as a competing primary product loop.

### 2.5 Mocks are measurement commitments

Stage 16 defines mini, section/component, and full mocks with explicit scope, duration, rules, validity, and result claims. During a clean target-condition measured block, Bestehen behaves like an exam environment and defers coaching until the block ends.

### 2.6 The coach is Bestehen

Stage 18 rejects a separate mascot or named AI persona. Copy and generated messages follow a **fact → meaning → next action** structure and must preserve distinctions such as not enough evidence, not ready, borderline, safe pass range, and Ready to Book.

### 2.7 Corpus is intelligence behind the learner experience

Corpus provides source, task, difficulty, relevance, and pattern intelligence. Earlier stages explicitly reject a learner-facing Corpus browser. Real/reference material may define what is tested, while learner practice usually uses original reviewed material where direct reuse is not appropriate.

No earlier product decision needs amendment as a result of Stage 19.

---

## 3. Decisions and Rationale

## 3.1 Primary navigation: four destinations plus utilities

**Decision:** The primary learner shell has four destinations:

1. **Coach** — the default Home and answer to “What should I do today?”
2. **Readiness** — the evidence-backed current pass picture and booking status
3. **Train** — a secondary, curated way to deliberately choose Review, Weakness work, a Mock, or another useful skill activity
4. **Progress** — history and meaningful change over time

**Goal / Exam Date** and **Settings** are persistent utility destinations rather than equal members of the main daily navigation.

### Why this shape

A larger primary navigation such as Home / Learn / Reading / Listening / Writing / Speaking / Review / Mocks / Progress / Settings would make Bestehen feel like an LMS and force the learner to self-diagnose every day. A minimal two-item navigation would protect simplicity but make mocks, review, and evidence exploration unnecessarily hidden.

The four-destination model keeps the hierarchy understandable:

- **Coach tells me what to do.**
- **Readiness tells me where I stand.**
- **Train lets me deliberately choose something else.**
- **Progress tells me what changed.**

Goal and Settings support those jobs but are not daily study destinations.

### Navigation map

~~~text
Bestehen
├── Coach  ← default entry
│   ├── Today's Session
│   │   ├── Attempt
│   │   └── Diagnosis → Repair → Fresh Check → Remember
│   ├── Recommended weakness
│   ├── Recommended mock
│   └── Goal / Exam Date shortcut
├── Readiness
│   ├── Written readiness
│   ├── Oral readiness
│   ├── Section evidence
│   ├── Skill / Weakness detail
│   └── Ready-to-Book evidence status
├── Train
│   ├── Coach alternatives
│   ├── Review
│   ├── Weaknesses
│   ├── Mock Exams
│   └── Skill practice  ← lowest-priority browsing path
├── Progress
│   ├── Readiness history
│   ├── Evidence / attempt history
│   ├── Mock history
│   └── Repaired / reopened weaknesses
└── Utilities
    ├── Goal / Exam Date
    └── Settings
~~~

### Primary-navigation rules

- **Coach is always the default return destination** after launch, session completion, or a long absence unless the learner explicitly deep-linked into another task.
- Primary navigation does not disappear during ordinary browsing, but it is minimized or suppressed during measured attempts where distraction would undermine the evidence claim.
- Train may never become an unranked giant exercise library. Its first content is the coach’s current alternatives and obligations, not subject categories.
- Review and Mocks are discoverable from Train and contextually linked from Coach/Readiness/Progress; they do not become primary tabs.
- A learner may reach the same weakness from Readiness, Train, Progress, or post-attempt diagnosis. Those routes open the **same weakness state**, not separate copies.

---

## 3.2 Screen inventory and responsibility boundaries

| Screen / surface | Responsibility | Primary action | Explicitly not responsible for |
|---|---|---|---|
| **Coach / Home** | Orient today: current state, top blocker, recommended session/action | **Start / Continue today’s plan** | Full analytics, full history, content browsing |
| **Readiness** | Explain current Written/Oral pass picture, confidence, evidence gaps, and booking status | **Do the action that most improves/clarifies readiness** | Daily-plan assembly, raw learner-model inspection |
| **Train** | Secondary deliberate choice among coach-approved alternatives | **Start selected useful work** | Becoming the default learner journey |
| **Today’s Session** | Show today’s coherent coaching commitment and progress through it | **Start / Continue next block** | Long-term analytics or broad browsing |
| **Attempt** | Provide a clean, fair task environment and capture valid learner evidence | **Submit / Finish measured block** | Coaching before the attempt is over |
| **Diagnosis / Repair** | Explain what happened, repair the narrow blocker, and test fresh transfer | **Do quick repair / Fresh check** | Dumping every possible correction |
| **Review** | Expose due and upcoming review obligations without creating a card-deck identity | **Start due review** | Permanent deck maintenance, vanity card counts |
| **Weakness detail** | Explain one actionable weakness/pattern, evidence, lifecycle, and next check | **Work on this weakness** | Raw graph/database browsing |
| **Mock Exam** | Choose, prepare, run, and review mini/section/full mocks with honest scope | **Start recommended mock / Review result** | Pretending every mock is equally valuable or valid |
| **Goal / Exam Date** | Set target/date state and explain planning consequences | **Set / change / mark booked** | Inflating readiness because a date exists |
| **Progress / History** | Show meaningful evidence-backed change and past work | **Inspect a meaningful change / resume consequence** | Replacing Readiness with engagement metrics |
| **Settings** | Configure stable product preferences and equipment/support defaults within shaped boundaries | **Save preference / test setup** | Overriding exam-validity rules or becoming a learner-model editor |

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Coach / Home

### Job

Home is not a dashboard of everything Bestehen knows. It is the **daily coaching decision surface**.

The learner should be able to answer, without scrolling through analytics:

- What is my most important current state?
- What are we doing today?
- Why this?
- How long will it take?
- What should I press now?

### Information hierarchy

Home uses this order:

1. **Today’s primary coaching action**
   - task/session name in plain language;
   - expected duration;
   - dominant skill or goal;
   - one-sentence learner-specific “why this today?”;
   - **Start** or **Continue**.
2. **Compact readiness state**
   - overall band/index only when Stage 15 evidence permits it;
   - separate Written / Oral status;
   - evidence-confidence cue when material;
   - contextual link to full Readiness.
3. **Current blocker or evidence gap**
   - one primary blocker by default, optionally one secondary;
   - direct link to the relevant weakness/evidence detail.
4. **Today’s plan preview**
   - coherent blocks and estimated time, not a long lesson queue;
   - due review may appear as one short block;
   - mock appears only when actually recommended.
5. **Goal/date context when it changes action**
   - exam not booked: light planning status;
   - booked: days remaining and current preparation mode;
   - Ready to Book: recommendation with evidence language.
6. **Recent meaningful change**
   - one concise item such as “Oral evidence moved from low to medium confidence” or “Writing content coverage repeated cleanly.”

### Home primary action rules

- There is normally **one visually and semantically dominant CTA**: Start/Continue Today’s Session.
- If the correct next action is not a normal session—e.g. resume the diagnostic, complete missing oral evidence, run a recommended mock, or review a pending mock result—the main CTA becomes that action.
- Home does not show five equal skill buttons above the recommended action.
- “Choose something else” is allowed but secondary and routes to Train.
- After a long absence, Home first presents the return/recheck plan rather than pretending the old schedule is still current.
- When evaluation is pending, Home can continue with work that remains valid rather than blocking the whole product.

### Sparse-evidence Home

Before a defensible readiness number exists, Home shows:

- **Evidence building** / **Not enough evidence**;
- what has been observed;
- the most important missing evidence;
- the next evidence-building action.

It must not render a greyed 0% readiness gauge.

---

## 4.2 Readiness dashboard

### Job

Readiness answers: **“If I sat TELC B1 now, what does the current evidence support, how sure are we, and what is limiting the conclusion?”**

It is the deepest learner-facing evidence summary, but still translates analytics into coaching decisions.

### Information hierarchy

1. **Readiness state**
   - band: Evidence building / Not enough evidence, Not ready, Borderline, or Safe pass range;
   - Readiness Index when allowed by Stage 15;
   - explicit statement that it is an estimated target-performance index, not pass probability.
2. **Written and Oral side by side conceptually**
   - target-performance estimate and range;
   - current pass line;
   - confidence;
   - strongest blocker/evidence gap;
   - neither component can be hidden by the other.
3. **Ready-to-Book status**
   - separate from Safe pass range;
   - show which Stage 17 gates are satisfied/missing in plain language;
   - when satisfied, state the booking recommendation without guaranteeing a pass.
4. **Section/task evidence**
   - Reading, Language Elements, Listening, Writing, Speaking;
   - concise state, confidence, realism/condition signal, freshness;
   - deeper task-family information on demand.
5. **What is holding the score/state down**
   - prioritized blocker, evidence gap, stale area, or contradictory result;
   - one recommended action.
6. **Why it changed**
   - latest material evidence changes, not every tiny internal movement.
7. **Evidence quality explanation**
   - short explainer for assisted/unassisted, timed/target-condition, recency, and uncertainty.

### Readiness interaction rules

- A learner can drill from component → section → weakness/evidence detail.
- Fine-grained detail is progressively disclosed; the default dashboard does not expose dozens of internal skill nodes.
- Predictions and ranges are shown only when the underlying Stage 15 evidence gate permits them.
- If evidence becomes stale, the screen explains the recheck needed rather than showing a mysterious score drop.
- A booked date adds urgency/context but never raises the score.
- The dominant CTA is the action that most improves or clarifies readiness, normally the same priority the Coach uses.

---

## 4.3 Train: secondary deliberate-practice hub

### Job

Train is the learner’s controlled escape hatch from the default recommendation. It exists because a coach-led product still needs learner agency and direct access to review, weaknesses, and mocks.

### Information hierarchy

1. **Coach’s alternatives** — 2–4 useful options the engine considers worthwhile now, with time and reason.
2. **Due Review** — only current obligations requiring deliberate attention.
3. **Weaknesses** — active or repairing patterns, ordered by coaching priority rather than alphabetically.
4. **Mock Exams** — recommendation and access to mini/section/full modes.
5. **Practice by skill** — Reading, Language Elements, Listening, Writing, Speaking as a secondary browse route.

### Guardrails against LMS drift

- No giant unit tree, chapter map, or “complete all B1 topics” syllabus.
- No global catalog sorted primarily by content quantity.
- No XP/lock system that forces sequence.
- Skill browsing remains useful, but the product keeps the current recommendation visible and marks whether chosen work is high-value, neutral, or mainly exploratory.
- Learner-selected work still generates valid evidence according to its actual conditions and can influence future recommendations.

---

## 4.4 Today’s Session

### Job

Today’s Session is a **coaching commitment**, not a playlist.

Before starting, it should explain the coherent plan. During the session, it should keep the learner focused on the next useful block and preserve meaningful resume boundaries.

### Pre-session hierarchy

1. session goal / dominant priority;
2. expected duration and selected time budget;
3. short reason;
4. block preview with approximate time and evidence/repair purpose;
5. relevant environment needs, e.g. audio or microphone;
6. **Start Session**;
7. secondary controls: change today’s available time, replace/skip a block, choose another useful option.

### In-session hierarchy

- current block and task goal;
- lightweight session progress such as “2 of 3 blocks” rather than XP;
- remaining estimated time when useful;
- ability to stop at a meaningful boundary;
- next block only after the current loop is complete or explicitly deferred.

### Partial completion

If the learner stops:

- completed valid evidence remains recorded;
- an unfinished measured attempt follows that attempt’s validity rules;
- Home becomes **Continue today’s session** when resumption remains useful;
- stale low-value leftovers are not carried forever merely because they were originally planned;
- the coaching engine may replan later when new evidence or time changes the best action.

---

## 4.5 Attempt experience

### Job

Attempt is the cleanest and most focused learner surface. It must preserve the conditions needed to interpret the response fairly.

### Common hierarchy

1. task family / goal in compact form;
2. instructions and target material;
3. allowed support / timer / playback / preparation rules;
4. learner response controls;
5. progress within the measured unit when relevant;
6. submit/finish action.

### Rules

- No diagnosis, answer reveal, correctness feedback, or coach interruption before submission unless the configured learning mode explicitly allows a help action that changes the evidence claim.
- Assistance actually used is visible enough that the learner understands the attempt is assisted; it is not framed as punishment.
- Technical failure has a clear report/retry path and is not converted into learner failure.
- Writing separates preparation/response/submission.
- Speaking separates preparation, recording/interaction, and finish.
- Listening playback behavior follows the active progression/mock condition.
- During clean P4/mock measurement, global navigation is suppressed/minimized and coaching waits until the measured block ends.
- Leaving a target-condition measured block triggers the already-defined stop/pause validity semantics rather than silently saving a “clean” result.

### Objective vs productive attempts

Objective attempts can normally transition directly into deterministic diagnosis. Writing/Speaking may enter **Evaluation pending**. The UI keeps the original response immutable and can let the learner continue elsewhere while evaluation completes when that does not compromise the planned loop.

---

## 4.6 Diagnosis / Repair experience

### Job

The post-attempt experience turns a result into a useful next move without becoming a wall of corrections.

### Information hierarchy

1. **What happened** — correct / partial / incorrect / incomplete / invalid / pending.
2. **Decisive evidence** — answer cue, missed content point, observable speaking behavior, or rubric dimension.
3. **Likely cause and confidence** — one primary cause, optionally one contributor; unresolved remains allowed.
4. **Why it matters** — skill/exam consequence in plain language.
5. **Quick repair** — the smallest useful explanation, contrast, phrase, strategy, or micro-practice.
6. **Fresh check** — new equivalent content when transfer should be tested now.
7. **What changed / Remember** — current weakness/capability consequence and when it will return.

### Rules

- A correct/simple outcome may compress diagnosis to one line and skip repair.
- Writing and Speaking emphasize at most one or two high-impact corrections by default.
- A model answer or correction is clearly teaching material and never shown as though it were the learner’s improved evidence.
- Detailed linguistic explanation is available on demand; it does not push the next action below a long lecture.
- Mock diagnosis is deferred until the relevant measured block ends and starts from the mock-level summary before drilling into items/weaknesses.
- When diagnosis confidence is low, the next action may be a clarifying probe rather than a speculative repair.

---

## 4.7 Review area

### Job

Review exposes the obligations already defined by Stage 14 while keeping review subordinate to coaching.

### Information hierarchy

1. **Due now** — small set of obligations that actually benefit from explicit review;
2. **Why these are due** — repair transfer, aging evidence, target relevance, or unresolved stability;
3. **Start due review** — preferably a short coherent review session, not one card at a time from an endless queue;
4. **Coming soon** — collapsed/secondary forecast;
5. **Recently demonstrated / resolved** — evidence that the system is retiring work rather than accumulating a permanent debt;
6. link to the associated weakness detail.

### Rules

- Do not foreground total “cards”, deck size, daily quota, or completion percentage.
- Natural valid practice can clear a due obligation automatically, so the queue may shrink without the learner visiting Review.
- Missed days do not generate a punitive pile. The coach reprioritizes the backlog and surfaces the highest-value subset.
- Repeated failure routes back into Diagnose/Repair rather than scheduling identical drills indefinitely.
- Productive claims are reviewed productively; listening claims use audio; interaction claims require partner turns.

---

## 4.8 Skill / Weakness detail

### Job

Weakness detail answers: **“What exactly is this problem, why does the coach care, what evidence supports it, and what will fix or verify it?”**

This is an actionable coaching view, not a raw learner-model inspector.

### Information hierarchy

1. **Plain-language weakness name** and current lifecycle state: candidate when shown, active, repairing, repaired/monitoring, resolved, or reopened.
2. **Exam relevance** — where this pattern costs or protects points.
3. **What the evidence shows**
   - recurring manifestations;
   - direct evidence lane(s);
   - assistance/timing condition when material;
   - confidence/uncertainty.
4. **Recent evidence timeline** — meaningful episodes only, not every click.
5. **Repair history** — what has been tried and whether fresh transfer succeeded.
6. **Next check / due state**.
7. **Recommended action** — work on weakness, do a fresh check, or leave it to natural practice.

### Rules

- Do not expose a false precise mastery percentage if the underlying model uses evidence-aware bands.
- Cross-modal relationships may be explained, but evidence from one modality must not be shown as mastery in another.
- An isolated mistake should not be presented with the same visual/semantic weight as a recurring known weakness.
- Resolved weaknesses remain inspectable in history but do not clutter the active list.

---

## 4.9 Mock Exam area

### Job

Mock Exam makes realistic measurement discoverable while protecting the learner from unnecessary full mocks and preserving validity semantics.

### Landing hierarchy

1. **Coach recommendation**
   - whether a mock is useful now;
   - recommended mode;
   - why now / why not now.
2. **Mock modes**
   - Mini-mock;
   - Section / component mock;
   - Full mock;
   - each shows scope, expected commitment, evidence claim, and equipment need.
3. **Readiness relationship**
   - what the recommended mock can clarify;
   - no secret “mock bonus”.
4. **Recent mocks**
   - result;
   - clean/modified/partial/pending validity in learner language;
   - direct link to post-mock analysis.
5. **Consistency / Ready-to-Book context**
   - when relevant, show the missing full/component confirmation from Stage 17.

### Mock preflight

Before Start, show:

- exact scope;
- estimated/target time and preparation commitment;
- timing/playback/notes/help/pause rules;
- current target blueprint status;
- audio/microphone needs;
- what happens if the learner stops;
- what result the mock can and cannot support.

### During mock

- exam-focused shell;
- no coaching between items or target measured blocks;
- only controls permitted by the active mock contract;
- clear stop/technical-failure handling.

### After mock

1. validity and pending-evaluation state;
2. written/oral or scoped result;
3. whether the relevant pass gate was cleared;
4. readiness/evidence impact without double-counting;
5. at most two immediate priorities;
6. drill-down to sections, items, or weaknesses;
7. next recommended repair/retest rather than an automatic “take another full mock”.

---

## 4.10 Goal / Exam Date

### Job

Goal makes the target and deadline explicit and shows how they change planning without pretending they change demonstrated ability.

### Information hierarchy

1. **Target:** Zertifikat Deutsch / telc Deutsch B1 at launch.
2. **Exam status:** not booked / considering date / booked / completed / result recorded where later journey stages require it.
3. **Date** and countdown when known.
4. **Current booking recommendation:** preparing, close but not ready, Ready to Book, or booked despite remaining risk.
5. **Plan consequence:** normal coaching, 21-day mode, 7-day mode, maintenance, or post-exam state as defined by Stage 17/Stage 02.
6. **Current main risk** relative to the deadline.
7. **Primary action:** set/change date, mark booked, or return to recommended preparation.

### Rules

- Changing a date triggers replanning, not a readiness increase or history reset.
- Booking early is accepted neutrally; the screen shows remaining risk honestly.
- Ready-to-Book is advisory. Bestehen does not claim official booking availability or automatically book an exam in Stage 19.
- Multi-exam switching is not a launch requirement.

---

## 4.11 Progress / History

### Job

Progress shows **meaningful evidence-backed change over time**. It is not an activity leaderboard and does not compete with Readiness as the current-state metric.

### Information hierarchy

1. **Meaningful recent changes**
   - readiness band/index changes when valid;
   - confidence/evidence coverage changes;
   - weakness repaired/reopened;
   - first/renewed target-condition evidence;
   - mock outcomes.
2. **Readiness trend**
   - Written and Oral remain distinguishable;
   - uncertainty/withheld periods stay visible rather than backfilled.
3. **Skill/section progression**
   - improvement in support independence, realism, or capability bands;
   - not a conventional course-level completion chart.
4. **Mock history** with validity and scoped result.
5. **Session / attempt history** as secondary evidence chronology.
6. **Resolved weaknesses / retention wins**.

### Rules

- Avoid centering time spent, question count, streak length, or total exercise completion.
- A tiny noisy readiness movement should not become a celebratory event.
- Historical values are interpreted against the target blueprint/evaluator version that produced them when relevant.
- Filters may expose skill, section, mock, or time period, but the default view remains a concise narrative of material change.

Stage 20 owns whether streaks, achievements, or other motivation mechanics appear as secondary signals.

---

## 4.12 Settings

### Job

Settings contains stable preferences and equipment/support configuration. It must not become a back door for changing evidence truth or editing the learner model.

### Stage-19-defined settings groups

1. **Coaching preferences**
   - normal daily session duration from Stage 06;
   - preferred explanation language / language-support preference from Stage 18;
   - learner-controlled preferences that affect presentation rather than target validity.
2. **Audio & Speaking setup**
   - microphone/audio test;
   - playback/output preference where it does not change the active task rule.
3. **Goal shortcut**
   - link to Goal / Exam Date rather than duplicating the goal state.
4. **Notifications** — placeholder/category only until Stage 23 defines actual reminder settings.
5. **Account, data & privacy** — placeholder/category only until Stage 24 defines the product contract.
6. **Accessibility & device** — placeholder/category only until Stage 25 defines the policy.

### Rules

- Target-condition timing, replay, reference, and no-help rules are **not preferences** the learner can disable while keeping the same evidence claim.
- The learner cannot directly edit mastery, weakness lifecycle, readiness, or evidence confidence.
- A learner can change explanation language without changing the German difficulty of measured content.
- Settings must not require AI generation merely to display or save preferences.

---

## 5. Cross-Screen Navigation and State Rules

## 5.1 One state, many entry points

Readiness, weakness, mock, and attempt results must have one underlying learner-facing state even when reached from multiple routes.

Examples:

- tapping a blocker on Home and tapping the same weakness inside Readiness open the same Weakness detail;
- a mock result opened from Progress and from Mock Exam shows the same validity/result state;
- a due obligation opened from Review and encountered naturally inside Today’s Session resolves the same review obligation.

This prevents contradictory copies of the learner model from emerging in different parts of the IA.

## 5.2 Contextual deep links should preserve the coach’s reason

When a learner drills from a recommendation into detail, the context should remain understandable. For example:

- Coach → “Speaking is the booking blocker” → Oral Readiness → S3 interaction weakness;
- Mock result → Writing failure → missed content-point weakness → targeted repair;
- Review → due listening-recognition obligation → fresh audio check.

The learner can move back to the decision that led them there rather than being dropped into a generic library.

## 5.3 Resume behavior

The product distinguishes:

- **resumable coaching flow** — Today’s Session at a meaningful block boundary;
- **resumable non-measured work** — ordinary practice where resumption does not corrupt evidence;
- **measured target-condition block** — follows Stage 16/Stage 07 pause/stop validity rules;
- **pending productive evaluation** — original response remains immutable while the learner may continue elsewhere when allowed.

Home always knows the highest-value unresolved commitment and can make it the primary CTA.

---

## 6. Corpus / Source Information Visible to Learners

### Decision

**Learners see source information only when it improves trust, legal/attribution clarity, or understanding of why a task matters. They do not see raw Corpus internals.**

### Default visibility

Do **not** expose by default:

- Corpus source IDs;
- authenticity/confidence scores;
- ingestion metadata;
- duplicate clusters;
- source-rights review states;
- raw frequency tables;
- internal TELC-relevance coefficients;
- prompt/generation provenance chains;
- a browseable Corpus source library.

### What learners may see

1. **Practice origin label**
   - “Original Bestehen practice” or equivalent when useful;
   - never imply official TELC authorship or endorsement.
2. **Reference/source attribution**
   - when exact reusable material requires or benefits from attribution;
   - show provider/source identity and appropriate attribution in a lightweight details area.
3. **Why this matters**
   - learner-friendly evidence translation such as “This task trains a common target pattern” or “This pattern appears often in relevant B1 exam material,” only when supported by Corpus evidence.
4. **Target-format status**
   - mocks/target-condition tasks can state they follow the current approved TELC B1 blueprint without claiming official affiliation.
5. **Content-quality uncertainty**
   - low-confidence or unresolved Corpus evidence should normally be filtered before learner use; the learner should not be asked to interpret internal confidence scores to decide whether a task is trustworthy.

Stage 21 owns generalized attribution rules and Stage 22 owns the exact Corpus → App contract. Stage 19 locks only the learner-facing principle: **translate Corpus intelligence into coaching; do not expose Corpus as a second product.**

---

## 7. Responsive and Mobile Priorities

Stage 25 will decide final launch-platform and accessibility expectations. Stage 19 nevertheless locks the information hierarchy so it can survive narrow screens and different input modes.

### 7.1 Narrow-screen priority order

On a narrow/mobile layout:

1. primary current action;
2. current readiness/pass-risk summary;
3. blocker/reason;
4. secondary detail and history.

Analytics never push the recommended action below a large dashboard merely because a wide desktop layout had room for both.

### 7.2 Primary navigation behavior

- The four destinations remain reachable with one persistent compact navigation model.
- Goal and Settings stay utilities rather than consuming scarce primary-nav positions.
- Deep screens use contextual back navigation without losing the originating coaching reason.

Exact bottom-tab, sidebar, or header treatment is visual/platform design and remains open.

### 7.3 Screen-specific responsive rules

- **Home:** stack the recommended action before readiness cards and history.
- **Readiness:** Written and Oral stack rather than shrinking into unreadable side-by-side analytics; the weaker component remains visually first/clear.
- **Today’s Session:** one block at a time; plan overview can collapse during execution.
- **Attempt:** use a focused full-screen experience. Reading passages and response choices must remain usable without forcing a desktop layout assumption.
- **Writing:** prioritize the prompt/content points and learner editor; secondary coaching chrome stays out of the measured response area.
- **Speaking/Listening:** playback/record/partner-state controls remain primary and stable; transcript/help is secondary and condition-dependent.
- **Diagnosis/Repair:** fact → meaning → next action is visible before optional detailed explanation.
- **Mocks:** rules and commitment are readable before Start; during measurement, nonessential navigation is suppressed regardless of device.
- **Progress:** charts degrade to concise summaries/timelines rather than requiring a wide multi-series dashboard.

### 7.4 Device does not change evidence semantics

A smaller screen, alternate navigation shell, or input method must not silently change whether evidence is assisted, timed, target-condition, paused, or valid. If a device constraint makes a fair target-condition attempt impossible, Bestehen labels the limitation and offers a suitable practice alternative rather than pretending equivalent evidence.

---

## 8. Edge Cases / Failure or Uncertainty Handling

## 8.1 Not enough evidence

- Home says Evidence building and recommends the highest-value missing sample.
- Readiness withholds unsupported numbers.
- Train remains available for learner choice.
- Progress shows what has actually been observed without backfilling missing history.

## 8.2 Productive evaluation pending

- Attempt becomes immutable once submitted.
- The learner sees **Evaluation pending**, not a guessed result.
- Home/session may continue with independent valid work.
- When the result arrives, diagnosis and any affected readiness change appear as one coherent update rather than silently changing history.

## 8.3 Technical failure

- The affected Attempt/Mock unit is labelled invalid or modified according to earlier stage rules.
- It is not presented as learner failure.
- The primary action becomes retry under valid conditions or continue with unaffected work.

## 8.4 Long absence or stale evidence

- Home leads with a short return/recheck plan.
- Readiness explains which claims are stale.
- Review does not dump every missed obligation at once.
- Progress remains intact; the learner is not “reset.”

## 8.5 Learner ignores the recommended plan

- Train permits a useful alternative.
- The coach does not shame or repeatedly demand confirmation.
- Valid self-selected evidence still updates the model.
- Home recomputes the next recommendation from the new state.

## 8.6 Ready-to-Book becomes invalid

- Readiness changes from Ready-to-Book status to the appropriate current state with a concrete reason.
- Goal does not hide this merely because an exam is booked.
- Home’s primary action becomes the highest-value risk/evidence repair.

## 8.7 Review backlog grows

- Review shows a prioritized subset, not all overdue items.
- Natural practice can satisfy obligations.
- Repeated failure redirects into diagnosis/repair.

## 8.8 Mock interrupted or modified

- Completed defensible units remain visible where Stage 16 allows.
- Overall mock validity is shown clearly.
- Progress history preserves the attempt; Readiness uses only valid evidence.
- The next CTA is based on what information is still missing, not automatically “restart full mock.”

## 8.9 Diagnosis is uncertain

- Weakness detail may show a candidate/possible pattern rather than a known weakness.
- Diagnosis/Repair offers a clarifying probe or broader practice.
- Home avoids presenting a speculative cause as the learner’s primary long-term blocker unless the evidence supports it.

## 8.10 Goal/date changes

- Goal updates planning context.
- Home and Today’s Session replan.
- Readiness history is preserved and not artificially boosted.
- If the date becomes very close, Stage 17 final-preparation behavior controls priority, not a new IA state.

---

## 9. Relationship to Other Bestehen Stages

### Earlier stages this IA operationalizes

- **Stages 01–02:** Coach is the default destination; the end-to-end journey maps cleanly onto Home, Readiness, Goal, Mocks, and post-exam states.
- **Stage 03:** diagnostic/resume and first readiness snapshot use the same Coach and Readiness surfaces rather than a disconnected onboarding product.
- **Stages 04–05:** learner-model and mistake states are progressively disclosed through Readiness, Weakness detail, Review, and Progress; raw internals stay hidden.
- **Stage 06:** Today’s Session and Home are direct surfaces for the Daily Coaching Engine.
- **Stage 07:** Attempt and Diagnosis/Repair preserve the semantic learning loop while allowing UI compression.
- **Stage 08:** support/realism condition is visible where it changes attempt meaning; progression does not become a course map.
- **Stages 09–13:** modality-specific attempt behavior fits inside one shared Attempt/Diagnosis IA.
- **Stage 14:** Review remains a secondary obligation area blended into coaching.
- **Stage 15:** Readiness is the dedicated evidence dashboard and remains separate from Progress/history.
- **Stages 16–17:** Mock Exam and Goal/Readiness expose target-condition validity and Ready-to-Book logic without creating a second score.
- **Stage 18:** one Bestehen voice and fact → meaning → next action hierarchy applies across all screens.

### Later-stage handoffs

- **Stage 20 — Progress and Motivation:** decide secondary streak/achievement/milestone mechanics without changing the Progress/Readiness responsibility split.
- **Stage 21 — Content Strategy:** define detailed origin labels, generation QA, and attribution behavior within the learner-facing source-visibility boundary here.
- **Stage 22 — Corpus → App Contract:** provide the structured data needed by Readiness, skill detail, recommendation reasons, and “why this matters”.
- **Stage 23 — Notifications:** define reminders and scheduling settings surfaced through Settings/Goal/Coach.
- **Stage 24 — Account/Data:** define account and data controls surfaced through Settings and history/export areas.
- **Stage 25 — Accessibility/Device:** choose platform priorities and accessibility requirements while preserving this screen hierarchy and evidence semantics.
- **Stage 26 — Analytics:** instrument navigation, coaching decisions, attempt flows, and readiness interactions without turning analytics into learner-facing clutter.
- **Stage 28 — Final Spec:** use this document as the authoritative IA/screen map.

---

## 10. Cost Notes

### 10.1 Stage 19 has low direct recurring-cost impact

Information architecture itself does not require meaningful recurring compute spend. The recommended low-cost default is that screen state, navigation, summaries, readiness displays, due-review state, mock history, and recommendation reasons are rendered from already-computed learner/evidence state.

### 10.2 Do not make Home a live AI chat

A conversational coach surface that calls a premium model every time Home opens would add cost without improving the core IA. Home should use deterministic/cached structured reasons and Stage 18 message templates for routine orientation.

AI remains justified where earlier stages already established real quality value:

- evaluating open Writing;
- evaluating Speaking;
- adaptive Speaking interaction where a fixed partner is insufficient;
- rare high-impact ambiguous evaluation escalation.

No extra model call is required merely to render Home, Readiness, Review, Weakness detail, Progress, or a post-attempt summary when existing structured outputs can explain the state.

### 10.3 Source transparency should be precomputed

Corpus-derived “why this matters,” source attribution, target-format version, and practice-origin labels should be carried as content metadata. Do not query or summarize the Corpus live on every learner screen.

### 10.4 Upgrade trigger

A richer generated coach narrative is justified later only if user testing shows structured deterministic explanations are materially insufficient for comprehension or trust. Even then, generate on meaningful state changes and cache/reuse the result rather than paying on every navigation event.

---

## 11. Decisions Made

1. Primary navigation is **Coach, Readiness, Train, Progress**; Goal and Settings are utilities.
2. **Coach/Home is the default route** and normally exposes one dominant Start/Continue action.
3. Train is a **curated secondary choice hub**, not a giant exercise catalog.
4. Review and Mocks remain reachable but do not become primary navigation destinations.
5. Readiness owns the current pass picture; Progress owns historical change.
6. Readiness preserves separate Written/Oral pass risk, confidence, evidence gaps, and Ready-to-Book status.
7. Today’s Session represents one coherent coaching commitment, not a playlist.
8. Attempt is a focused evidence-capture surface; target-condition attempts suppress distracting navigation/coaching.
9. Diagnosis/Repair uses **outcome → evidence → cause → repair → fresh check → what changed**, with details progressively disclosed.
10. Review exposes due obligations without decks, card counts, or punitive backlogs.
11. Weakness detail is actionable and evidence-backed, not a raw learner-model inspector.
12. Mock Exam leads with the coach’s recommendation, explicit scope/rules, and validity; it does not encourage unnecessary full mocks.
13. Goal/Exam Date changes urgency and planning, never readiness itself.
14. Progress highlights meaningful readiness/evidence/weakness changes rather than engagement volume.
15. Settings contains stable preferences and future stage-owned categories, but cannot override evidence truth or target-condition rules.
16. Learners see only **translated, useful source transparency**; raw Corpus internals remain hidden.
17. Responsive hierarchy always puts the current action and pass risk ahead of analytics; device changes do not change evidence semantics.
18. Routine IA rendering requires no new premium AI dependency.

---

## 12. Open Questions / Deferred Decisions

### No owner-blocking questions

No Stage 19 decision requires owner preference or legal-risk input to proceed. The IA can be shaped responsibly from the established exam-coach principles.

### Deliberately deferred to later stages

- Whether launch is phone-first, desktop-first, or equal priority — Stage 25.
- Exact bottom-navigation, sidebar, header, breakpoint, and visual layout treatment — design/Stage 25, not product IA.
- Whether streaks, achievements, or other secondary motivation elements appear on Home/Progress — Stage 20.
- Exact source-attribution text and when specific reused assets require attribution — Stage 21 plus rights metadata.
- Exact reminder, quiet-hour, and study-schedule settings — Stage 23.
- Account, sync, export, deletion, privacy, and data-retention controls — Stage 24.
- Accessibility mechanics and accommodation treatment for measured evidence — Stage 25.
- Analytics event taxonomy — Stage 26.

These are not missing Stage 19 product decisions; they are intentionally owned by later checklist stages.

---

## 13. Definition of Done Check

- [x] Primary navigation is defined and keeps Coach as the default destination.
- [x] Home / Coach responsibility, hierarchy, and primary action are defined.
- [x] Readiness dashboard hierarchy and drill-down behavior are defined.
- [x] Today’s Session is defined as a coherent coach-led commitment.
- [x] Attempt behavior is defined across ordinary and measured modes.
- [x] Diagnosis / Repair hierarchy and fresh-check behavior are defined.
- [x] Review is defined without creating a separate flashcard product.
- [x] Skill / Weakness detail is actionable and evidence-backed.
- [x] Mock Exam selection, preflight, measured state, and result navigation are defined.
- [x] Goal / Exam Date responsibilities and booking context are defined.
- [x] Progress / History is separated from current Readiness and from engagement metrics.
- [x] Settings responsibilities and stage-owned deferrals are defined.
- [x] Learner-facing Corpus/source visibility is explicitly bounded.
- [x] Responsive/mobile information priorities are defined without pre-empting Stage 25 platform choices.
- [x] Edge cases and uncertainty handling are defined.
- [x] Cost impact and low-cost defaults are explicit.
- [x] “What should I do today?” remains the dominant product journey.

**Stage 19 is product-complete when the live checklist reflects these decisions.**
