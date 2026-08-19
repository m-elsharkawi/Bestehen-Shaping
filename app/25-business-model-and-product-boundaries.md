# Bestehen / App — Stage 25: Business Model and Product Boundaries

> **Status:** Authoritative Stage 25 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Operating promise:** Keep the exam-coaching loop complete and evidence-truthful at personal-project scale; if Bestehen later becomes public, charge for materially costly capacity or convenience rather than weakening the learner’s ability to understand and improve their readiness.

## 1. Purpose and Scope

This document defines the operating and monetization boundaries for Bestehen / App without turning monetization into the organizing product logic.

Bestehen begins as a personal project. The first question is therefore not “Which subscription should we sell?” but **“What is the cheapest sustainable way to preserve the complete exam-coaching loop?”** The product should be capable of starting with very low recurring spend, near-zero cost while idle, reusable content, deterministic logic, and selective use of expensive AI only where it materially improves learner outcomes or evidence quality.

If Bestehen later becomes public, the business model must preserve the same product thesis:

- Readiness remains the primary progress concept.
- Written and Oral pass constraints remain independent.
- The coach recommends the highest-value preparation, not the highest-margin feature.
- A learner’s paid status never changes what their evidence means.
- A free experience, if offered, must not pretend to be a complete readiness coach while silently withholding a pass-critical skill.
- Learner data is not a monetization asset.

This stage also resolves a live-checklist continuity mismatch. The current `Bestehen_App_Product_Shaping_Checklist.md` names Stage 25 **Accessibility and Device Experience**, while the Stage 25 agent prompt governing this document is **Business Model and Product Boundaries**. The checklist separately places overlapping business/cost work at Stage 27. As in Stages 22–24, this document covers both the prompt-defined objective and every checkbox in the current live Stage 25 section. It also resolves the overlapping Stage 27 business/cost items so the repository does not carry two contradictory operating models.

This is product shaping, not billing, legal, tax, payments, infrastructure, model-provider, or pricing architecture. It intentionally does **not** select a subscription price, payment processor, entitlement service, hosting provider, AI vendor, or exact monthly quota.

### Core decision

**Private first; complete core; meter cost, not learning truth.**

Bestehen starts as a private, non-commercial personal product with no subscription system, advertising, purchase flow, or paywall. If it later becomes public, the recommended default is a **free-core / paid-capacity principle**: keep the full coaching model and readiness truth intact, while paid access may provide more frequent or more expensive AI-backed actions, higher convenience, or additional capacity.

If a financially viable free core cannot provide a credible route across all pass-critical skills, Bestehen should prefer a simple paid/trial product over a misleading “free” tier that is incomplete by design.

---

## 2. Inputs / Existing Decisions

Stage 25 preserves the shared Product Overview, shared Identity, and App Stages 01–24.

### 2.1 Product thesis and learner promise

Earlier stages establish that:

- Bestehen is a **personal German exam coach**, not a generic course, exercise library, chatbot, or engagement game.
- German is learned through exam-shaped practice from roughly A1 toward authentic TELC B1 performance.
- The coach owns prioritization by default while the learner retains meaningful control.
- The core loop is **Observe → Attempt → Diagnose → Repair → Retry → Remember**.
- Readiness is evidence-based and must never become a decorative score or pass guarantee.
- Written and Oral remain separate pass risks.
- Corpus is the intelligence/source system behind the App, not the learner UX.

Monetization may not reverse any of those decisions.

### 2.2 Cost boundaries already established by the learning stages

Stages 03–23 repeatedly establish the same economic pattern:

- objective Reading, Language Elements, and Listening scoring should normally be deterministic;
- recommendation, readiness aggregation, review scheduling, mistake lifecycle, and routine coach explanations should be deterministic or template-driven when quality is sufficient;
- content should normally be generated/validated ahead of use, then cached and reused;
- Listening audio should normally be created in batches and reused rather than regenerated per attempt;
- fixed/prerecorded Speaking interaction is preferred when it can test the intended behavior;
- live generative Speaking is justified when adaptive exchange materially improves the interaction test;
- Writing and Speaking evaluation are the main recurring AI-sensitive learner actions;
- stronger models are justified mainly for low-confidence, contradictory, pass-boundary, or readiness-critical cases rather than every routine attempt;
- mocks are expensive not only in compute but in learner time, fresh-form demand, and productive-skill evaluation.

Stage 25 turns those repeated local rules into one product-wide operating policy.

### 2.3 Data ownership is already established

Stage 24 is authoritative for the learner-data contract:

- sign-in is not required for first use;
- structured progress/evidence history is retained for explainability until the learner deletes it;
- learner-authored Writing may be retained with evidence history;
- raw Speaking audio is ephemeral by default and normally deleted after evaluation, with a bounded temporary exception for unresolved processing;
- learner data must be exportable and deletable;
- sync/recovery may justify future sign-in;
- AI receives only the minimum data needed for the specific job;
- learner responses/audio/outcomes are not contributed to third-party/general model training without separate explicit opt-in;
- no ad-tracking or invasive session-replay requirement exists.

Paid access cannot weaken these rights or make learner progress hostage to an active subscription.

### 2.4 Success metrics are outcome-first

Stage 24 defines Decision-Grade Safe Readiness Attainment as the launch north star and eventual real TELC outcome accuracy as the strongest validation. Cost per active learner/session and expensive-capability cost are supporting operational metrics.

A business model is therefore healthy only when it makes the outcome model sustainable. Revenue, conversion, retention, or premium-feature use may become business metrics later; they cannot replace readiness quality or encourage the coach to recommend unnecessary paid actions.

---

## 3. Decisions and Rationale

## 3.1 Initial state: private, free, non-commercial

**Decision:** The first usable Bestehen / App is a **private personal project** with no monetization surface.

Initial assumptions:

- one primary learner/owner is sufficient to validate the complete loop;
- invited trusted testers may be added later without creating a public commercial promise;
- no payment, subscription, billing account, entitlement catalog, coupon, trial countdown, referral program, ad system, or upgrade prompt is required;
- there is no need to optimize conversion, ARPU, churn, or growth;
- the product may enforce internal cost protections, but those are operating safeguards rather than “free-plan” limits;
- idle recurring cost should be kept close to the unavoidable minimum; variable cost should mainly follow actual high-cost use.

This keeps implementation effort focused on whether the exam coach works rather than on commercial infrastructure before there is a product worth selling.

## 3.2 Do not design a subscription before observing use

**Decision:** Stage 25 deliberately does **not** choose monthly subscription, annual subscription, credits, one-time exam-prep pass, pay-per-evaluation, or another payment mechanism.

All are plausible later:

| Model | Potential strength | Main risk for Bestehen |
|---|---|---|
| Subscription | Simple recurring access and predictable revenue | Encourages designing around retention rather than a finite exam goal |
| One-time preparation pass | Fits a goal-oriented preparation episode | Harder to price fairly for very different preparation durations and compute use |
| Usage credits | Maps directly to expensive AI actions | Makes coaching feel transactional and may discourage useful productive practice |
| Paid-only / trial | Simplifies unit economics | Higher adoption friction and weaker access for experimentation |
| Free core + paid capacity | Preserves broad access while monetizing real variable cost | Requires careful quota design so “free” does not become incomplete or misleading |

**Recommended future default:** preserve **free core + paid capacity** as the preferred direction if public economics support it, but do not lock the commercial packaging until real usage reveals which expensive actions dominate cost and how often learners actually need them.

If the free-core economics are not viable, prefer **paid-only or a meaningful trial** over deliberately breaking the coach for free users.

## 3.3 Monetization must attach to cost/capacity, not exam truth

**Decision:** Future monetization may limit **frequency, concurrency, premium quality, or convenience** of expensive capabilities. It may not sell a different definition of readiness.

The following are product invariants across any future tier:

1. the same TELC blueprint, evidence semantics, scoring rules, pass gates, confidence rules, and readiness formula apply;
2. paid status does not make an identical learner response score better;
3. the coach does not recommend an expensive action merely because it is monetizable;
4. existing learner evidence is never downgraded because a plan expires;
5. previously earned progress, history, weakness state, readiness explanations, and export/delete rights remain accessible under the ordinary data contract;
6. no “Premium Readiness,” hidden pass threshold, paid confidence multiplier, or paid-only interpretation of the same evidence exists;
7. objective scoring, review scheduling, mistake memory, and basic coach prioritization are never per-use purchases;
8. pricing cannot turn one exam section into an add-on pack whose absence makes overall readiness misleading.

## 3.4 No advertising or learner-data monetization

**Decision:** Bestehen should not fund the learner experience through ads, sponsored coaching recommendations, lead-selling, or sale of learner data.

Reasons:

- the coach must be trusted to recommend the highest-value next action;
- exam preparation includes sensitive performance and voice/text data;
- advertising creates incentives unrelated to readiness;
- Stage 24 already establishes data minimization and no ad-tracking requirement.

A future clearly disclosed affiliate relationship around an external exam-booking service would require separate shaping because it could bias a consequential “book now” recommendation. It is **not** part of the current business model.

## 3.5 Corpus and App remain separate product boundaries

**Decision:** Monetizing the App does not turn Corpus into learner-facing premium content.

- Corpus remains an internal evidence/intelligence product for the App at this stage.
- Paid App access does not imply raw Corpus/source access.
- Rights-restricted reference materials do not become reusable because a learner paid.
- A future Corpus API, research product, or separate business model would require its own shaping.

This prevents commercial pressure from weakening the rights/authenticity boundaries already established.

---

## 4. Non-Negotiable Core Coaching Features

A monetization model must not cripple the loop that makes Bestehen a coach.

### 4.1 Core capability boundary

The following are **non-negotiable product core** and cannot be transformed into premium-only concepts:

| Core capability | Required boundary |
|---|---|
| Goal/onboarding and initial diagnostic | A learner must be able to establish a usable baseline across all five relevant areas; productive sampling cannot simply be omitted because it costs more. |
| Coach/Home recommendation | The product must still answer “What should I do today?” using the learner model. |
| Reading, Language Elements, Listening practice | All remain available as genuine exam-shaped training, not teasers. |
| Writing and Speaking learning path | Both remain part of the core product. Public quotas may meter expensive evaluation/interaction capacity, but cannot permanently remove either pass-critical skill from free/core coaching. |
| Mistake Memory and targeted repair | Wrong answers must still improve future coaching. |
| Review and spaced return | Due repair/retention remains part of the coach, not a premium memory feature. |
| Progress/evidence history | Learners can see the learning evidence they already created. |
| Written and Oral readiness truth | Both components remain visible separately, including uncertainty and “not enough evidence.” Existing readiness is not hidden behind a paywall. |
| Evidence explanations | The learner can understand why a readiness state changed or why evidence is insufficient. |
| Mock/exam realism path | The product must retain a credible route to target-condition practice; commercial packaging may affect capacity/frequency, not whether target realism exists at all. |
| Data export and deletion | Data rights never depend on an active paid plan. |
| Accessibility baseline | Core coaching must remain accessible under the rules in Section 9; accessibility is not a premium feature. |

### 4.2 Meaningful free-core test

If Bestehen later advertises a **free exam coach**, that free experience should pass this test:

> **Can a motivated learner, over a realistic period, obtain valid practice and enough direct evidence across both Written and Oral to make genuine progress toward complete readiness, even if expensive actions are slower or less frequent than on a paid plan?**

If the answer is no, the product is not a complete free exam coach. The business model should be changed or described differently rather than manufacturing a readiness experience from incomplete evidence.

### 4.3 Paid may accelerate, deepen, or increase capacity

Reasonable future paid benefits include:

- more frequent Writing/Speaking evaluations;
- more frequent genuine adaptive Speaking-partner sessions;
- faster evaluation turnaround where asynchronous processing is used;
- additional high-quality mock forms or more frequent readiness-grade productive evaluation;
- additional premium voice choices only if they do not change evidence validity;
- richer convenience/sync/history features after the core data contract is preserved;
- stronger-model escalation on more routine productive attempts rather than only high-stakes/uncertain ones.

Paid benefits should feel like **more capacity, flexibility, and convenience**, not “the free coach does not know whether you can speak.”

---

## 5. Expensive AI and Cost-Risk Capabilities

## 5.1 Cost classes

Bestehen should reason about cost in three product classes:

| Class | Examples | Default policy |
|---|---|---|
| **A — Near-zero marginal** | objective scoring, learner-state updates, review scheduling, readiness aggregation, cached content delivery, template explanations | Always available; do not meter per use |
| **B — Bounded variable** | standard Writing evaluation, speech transcription/evaluation, occasional generated partner turn, low-cost model-assisted repair | Invoke when the activity needs it; measure per action; future quota candidate |
| **C — High/uncertain variable** | real-time generative Speaking conversation, stronger-model second opinion, premium speech evaluation, on-demand high-quality TTS, repeated readiness-grade double evaluation | Use selectively behind explicit product rules; strongest quota/escalation candidate |

A feature belongs in a cost class because of observed unit cost and evidence value, not because “AI” sounds premium.

## 5.2 Writing evaluation

**Preferred default:** one evaluation pass using the cheapest model/process that has demonstrated acceptable B1-rubric consistency, preceded or accompanied by deterministic checks for objective properties such as content-point presence cues, length, empty submission, obvious task mismatch, and required-email structure where reliable.

**Use stronger evaluation when:**

- the standard evaluator has low confidence;
- the result is contradictory with recent comparable evidence;
- the response is near a pass-critical boundary and will materially influence P4/Readiness/Ready-to-Book;
- a content/evaluator quality incident requires adjudication.

**Cheaper fallback:** retain the Writing response, deterministic checks, and lower-confidence/pending evidence; provide conservative coaching from known issues without inventing a high-confidence readiness update.

Do **not** call a premium model again merely to update Mistake Memory, readiness, analytics, or coach tone after the evaluation already produced the needed structured result.

## 5.3 Speaking transcription and evaluation

**Preferred default:** asynchronous or bounded speech processing/evaluation appropriate to the task, with direct handling of transcription/audio-quality uncertainty.

**Use stronger speech/evaluation when:**

- intelligibility cannot be judged reliably;
- transcript uncertainty materially affects the rubric conclusion;
- an oral P4/readiness result sits near a pass-critical boundary;
- recent oral evidence is contradictory and the new attempt is decision-critical.

**Cheaper fallback:** preserve the oral attempt as pending/lower-confidence or provide transcript-based learning feedback without claiming full oral evidence. Technical failure is never converted into learner failure.

## 5.4 Adaptive Speaking partner

**Preferred default:** fixed, prerecorded, scripted, or bounded-branch partner behavior wherever it can validly test the intended interaction skill.

**Invoke live generative interaction when:**

- the task genuinely requires the partner to respond to the learner’s specific proposal, disagreement, repair, or negotiation;
- fixed branching would make the exchange predictable enough to weaken interaction evidence;
- the interaction value justifies the additional cost and latency.

**Cheaper fallback:** reviewed fixed partner turns, bounded scenarios, or solo preparation plus later genuine interaction. The product must label what was and was not evidenced.

A general “chat in German with AI” mode is not a required paid feature because it is not central to TELC readiness.

## 5.5 Audio generation

**Preferred default:** scripts are created/reviewed ahead of time and audio is generated or recorded **once**, versioned, cached, and reused.

Use higher-quality/human/native-recorded or premium TTS assets selectively for:

- curated gold diagnostic anchors;
- P4/readiness-grade forms where audio naturalness materially affects evidence validity;
- benchmark/QA material.

Dynamic TTS is justified mainly for genuinely adaptive partner turns or narrow personalized repairs that cannot be served from reviewed reusable audio.

**Cheaper fallback:** cached reviewed audio, fixed partner recordings, or text-only repair where the target being repaired is not listening evidence. A text fallback cannot be mislabeled as Listening target-condition evidence.

## 5.6 Content generation and QA

**Preferred default:** content generation is primarily an offline/batch production activity governed by Stage 21, not a per-attempt runtime service.

Use stronger generation/review selectively for C2 curated-gold/P4/readiness material or content that fails normal validation. Reuse approved C3 practice with learner-specific freshness rules instead of continuously generating novelty.

**Cheaper fallback:** template-driven variation, curated authored content, smaller approved banks, and slower content refresh. Content scarcity should reduce variety before it reduces evidence truth.

## 5.7 Readiness, recommendation, review, and analytics

**Decision:** these are not premium-AI problems by default.

- readiness aggregation is deterministic from structured evidence;
- daily-plan assembly is deterministic/explainable;
- review scheduling is deterministic;
- mistake lifecycle updates are deterministic once diagnosis exists;
- coach explanations should use templates/structured generation when possible;
- analytics uses structured product evidence and ordinary aggregation.

A premium model may help investigate an unusual internal calibration case, but routine product operation must not require an always-on reasoning call.

---

## 6. Future Quotas and Limits

## 6.1 No user-facing quota is needed in the private phase

**Decision:** The personal/private version does not need “free plan” quotas. It needs **internal cost guardrails**:

- classify and count expensive actions;
- record cost per Writing evaluation, Speaking evaluation, adaptive partner session, and generated audio/content job where practical;
- support a global/period budget ceiling or graceful disabling of nonessential premium escalation later at implementation level;
- prefer a cheaper fallback before a hard failure.

Exact budget numbers are intentionally not invented in product shaping.

## 6.2 If public, meter expensive actions rather than sessions

A future public plan may meter Class B/C actions, not ordinary learning activity.

Good quota subjects:

- high-cost Writing evaluations beyond a meaningful included allowance;
- adaptive/generative Speaking-partner minutes/turns;
- premium second-opinion evaluation;
- unusually costly on-demand media generation;
- repeated high-cost mock productive evaluation beyond a meaningful included cadence.

Bad quota subjects:

- number of Reading questions;
- review items;
- readiness views;
- mistake memory;
- number of times the learner opens progress/history;
- basic coach recommendations;
- access to one pass-critical skill as a whole.

## 6.3 Quotas must fail gracefully

When a future expensive-action quota is exhausted:

1. existing evidence and readiness remain visible;
2. the coach continues to recommend the best available work rather than pretending the blocked action no longer matters;
3. the App offers a lower-cost valid alternative where one exists;
4. if new decision-grade evidence truly requires the unavailable action, the state becomes **insufficient/pending/stale evidence** rather than an invented result;
5. the learner is told what is limited and when capacity becomes available again, without urgency theater;
6. no completed evidence is deleted or downgraded;
7. accessibility accommodations are not charged as premium capacity merely because they require a different presentation path.

The exact number of included evaluations/minutes and reset cadence is deferred until real unit cost and usage frequency are measured.

## 6.4 High-stakes capacity gets priority over decorative AI

If a personal-project budget ceiling is reached, preserve spend in this order:

1. decision-critical Writing/Speaking evaluation needed for valid readiness;
2. pass-critical diagnosis/repair where no cheap equivalent exists;
3. genuine interaction needed to obtain missing oral evidence;
4. routine productive coaching;
5. optional richer wording, voices, or novelty generation.

Never spend premium capacity on decorative coach chat while a pass-critical oral evaluation remains unresolved.

---

## 7. Account, Entitlement, Data Portability, and Retention

Stage 24 remains authoritative. Stage 25 adds the commercial boundary.

## 7.1 Account expectations

- First use remains account-optional in the private/core product.
- Future sync/recovery may require sign-in.
- A future paid purchase may require an account for entitlement continuity, but the account requirement should occur at purchase/sync boundaries rather than before the learner can experience the coach.
- Billing identity, if introduced, should be conceptually separate from learning evidence; payment status is not a learner-model field.

## 7.2 Progress is not held hostage by a plan

**Decision:** Ending a future paid plan does not erase or rewrite learning history.

After cancellation/expiry, the learner should retain at least:

- their existing progress/evidence history;
- current readiness state with honest freshness/coverage notes;
- past Writing/evaluation data retained under the normal policy;
- mock/results history;
- export access;
- deletion access;
- access to the ordinary free/core capabilities that exist at that time.

A paid plan may stop future premium-capacity use. It may not hide already-created evidence solely to pressure renewal.

## 7.3 Retention remains purpose-driven

- Structured evidence/history persists under Stage 24 because readiness and mistake repair require it.
- Learner-authored Writing may be retained with evidence history.
- Raw Speaking audio remains ephemeral by default; monetization is not a reason to retain it permanently.
- Reusable generated content is versioned/cached; per-learner freshness is separate.
- No commercial analytics requirement justifies a second invasive clickstream or session-replay history.

If a future public service needs a dormant-account retention limit, billing record retention, tax records, fraud controls, or jurisdiction-specific deletion exceptions, those require legal/architecture review. They should not be invented here.

## 7.4 Portability is tier-independent

Export and deletion rights apply regardless of free/paid state.

A future export includes the personal learning record defined in Stage 24, but it does not redistribute rights-restricted Corpus/reference material. Payment history, if legally required in a commercial product, is a separate business/legal record and does not become part of readiness evidence.

## 7.5 AI data-use boundary survives monetization

No paid or free tier may silently change the Stage 24 privacy contract:

- minimum necessary payloads;
- pseudonymous processing where correlation is needed;
- raw audio only to speech workflows that require it;
- no entire learner-history dump for routine evaluation;
- no contribution to third-party/general-model training without separate explicit opt-in;
- no ad-tracking requirement.

“Free because your data trains our model” is not an acceptable future business model without a separate explicit product/legal decision, and it is not the recommended direction.

---

## 8. Product Boundary Map

## 8.1 In scope for the initial product

- one TELC B1 preparation target;
- complete coaching across Reading, Language Elements, Listening, Writing, and Speaking;
- mistake memory and review;
- daily prioritization;
- exam-shaped content grounded in Corpus intelligence;
- mocks and target-condition evidence;
- readiness and Ready-to-Book logic;
- goal/date behavior;
- progress/history;
- lean analytics and cost measurement;
- account-optional first use and basic learner-data ownership.

## 8.2 Explicitly not required for the personal-project phase

- payments, subscriptions, billing, tax/VAT handling, coupons, discounts, trials, referral programs;
- entitlement administration UI;
- enterprise accounts, SSO, organizations, teams, classrooms, teacher dashboards, or school licensing;
- tutoring marketplace or human-teacher dependency;
- social feeds, leaderboards, learner community, or user-generated exercise marketplace;
- advertising, sponsorship placement, data brokerage, or lead-selling;
- exam-center marketplace or booking commission;
- raw Corpus browser/API for learners;
- generic German conversation as a standalone paid product;
- multi-exam commercial packaging;
- always-on premium AI companion;
- live human scoring as a requirement for ordinary readiness;
- enterprise-scale warehouse/ML infrastructure.

## 8.3 Future options kept open

The shaped product does not prevent later:

- public free/paid access;
- a one-time preparation pass instead of subscription;
- paid higher-capacity productive evaluation;
- optional human expert review for a consequential Writing/Speaking sample;
- additional exam targets;
- cross-device sync/recovery;
- a separately shaped Corpus/research/API product.

Each option must preserve the evidence and data boundaries above and should be added only when learner value and operating cost justify the additional complexity.

---

## 9. Accessibility and Device Experience — Live-Checklist Reconciliation

This section resolves every checkbox in the current live Stage 25 checklist. Accessibility is a core product requirement and is not monetized separately.

## 9.1 Launch platform

**Decision:** The preferred first learner-facing platform is a **responsive web experience** that works well on modern phones and desktop/laptop browsers, with tablet behavior derived from the same responsive product model.

This is a product platform decision, not a commitment to a particular framework or hosting architecture.

Rationale:

- a personal project benefits from one primary surface rather than separate native iOS, Android, Windows, and macOS products;
- learners can move between short phone sessions and longer Writing/mock work without a separate product definition;
- it keeps future installation/PWA/native-shell options open.

Native mobile apps are not required for the first usable product.

## 9.2 Phone-first versus tablet/desktop

**Decision:** Daily coaching and ordinary practice are **phone-first in usability**, but the product is not phone-only.

- Coach/Home, Review, short Reading/Listening tasks, progress, and most Speaking flows must be comfortable on a phone.
- Writing, long Reading material, evidence inspection, and full mocks should receive a stronger large-screen layout on tablet/desktop.
- No core pass-critical skill may be impossible on phone solely to force a desktop workflow.
- For a long target-condition mock, the coach may recommend a larger screen for comfort and exam rehearsal without making it a validity gate unless the target format itself requires it.

## 9.3 Keyboard navigation

**Decision:** All core desktop/web flows must be operable by keyboard without requiring pointer-only interaction.

Requirements include:

- predictable tab/focus order;
- visible focus state;
- keyboard-operable answer choices, navigation, dialogs, media controls, repair actions, and mock controls;
- no drag-only matching interaction without an equivalent keyboard action;
- shortcuts may be added for efficiency but cannot be the only path.

## 9.4 Screen-reader expectations

**Decision:** Core coaching surfaces must expose semantic structure and meaningful control labels to screen readers.

- question instructions, answer groups, validation state, feedback, readiness status, blockers, timers, and progress changes need textual semantics;
- state cannot be communicated by visual position/color alone;
- charts or bars require a text equivalent;
- images that carry task meaning need appropriate text alternatives when doing so does not invalidate the skill being measured.

If an exam task inherently measures visual interpretation that cannot be made equivalent, the product must label the limitation and avoid fabricating an equivalent readiness claim.

## 9.5 Color and contrast

**Decision:** Core UI targets **WCAG 2.2 AA** contrast and interaction requirements as the product baseline.

- color is never the only indicator of correct/incorrect, risk/safe, selected/unselected, or evidence confidence;
- readiness bands always have text labels in addition to color;
- focus/interactive states remain perceivable in light/dark/system appearance if those themes are later implemented.

This requirement overrides purely aesthetic palette choices when they conflict.

## 9.6 Text scaling and reflow

**Decision:** Core flows must remain usable at **200% text zoom/scaling** without losing essential content or forcing two-dimensional scrolling for ordinary controls.

Long exam passages may naturally require vertical scrolling. Timers, answer controls, and primary actions must not disappear or overlap at large text sizes.

The learner may choose a comfortable text size in normal practice. A changed font size is not evidence assistance because it does not reveal answer content.

## 9.7 Captions and transcripts

**Decision:** Accessibility support must respect the difference between **learning access** and **target-condition Listening evidence**.

- instructional/coaching audio should have text equivalents/captions;
- generated partner prompts should have transcripts available after the relevant measured response or during supported practice when doing so does not expose answer-bearing content;
- Speaking transcripts may be shown after capture with uncertainty highlighted; a transcript never substitutes for the raw oral evidence used to judge intelligibility/fluency;
- Listening transcripts may be available after an attempt for diagnosis/repair;
- during a clean P4 Listening attempt, a transcript/caption that reveals the audio content is not permitted unless the target exam/accommodation explicitly allows an equivalent condition;
- a learner who needs a transcript during ordinary Listening practice can use it, but the resulting attempt is recorded as assisted/non-target-condition evidence rather than pretending standard Listening was measured.

## 9.8 Microphone-permission fallback

**Decision:** Denied/unavailable microphone access must not block the rest of Bestehen.

The learner can:

- continue all non-speaking work;
- rehearse a Speaking response by typing or silently planning;
- use phrase/structure practice;
- review previous transcripts/evaluations;
- retry microphone setup later.

Typed rehearsal is learning activity, not oral evidence. Oral readiness remains **not enough evidence** or ages honestly until valid voice evidence exists.

## 9.9 Accessibility in timed experiences

**Decision:** Practice timing is adaptable; target-condition timing remains evidence-specific.

- ordinary practice may disable, pause, extend, or visually de-emphasize timers;
- a learner who uses extra time still receives useful learning evidence with the actual timing condition recorded;
- clean P4/target-condition claims use the current target rule unless a recognized accommodation profile has been explicitly represented;
- an accommodated attempt can be valuable and should be retained with its true condition, but the App must not automatically equate a modified timing condition with the standard condition before the accommodation semantics are shaped/verified;
- accessibility needs never count as learner failure.

## 9.10 Low-connectivity behavior

Stage 24 already rejects full offline parity as a launch requirement. Stage 25 adds these product rules:

- already-loaded objective practice/review and local history should continue where practical;
- expensive AI evaluation may become pending and finalize after reconnection rather than fail the learner;
- a target-condition mock that depends on audio/content should preload the assets required for its measured block before the timer starts; if it cannot guarantee the required assets, it should not start as a clean target-condition mock;
- reconnection must not duplicate evidence;
- adaptive live Speaking may fall back to reviewed fixed interaction when available, otherwise the product should state that genuine interaction evidence needs connectivity;
- no low-connectivity fallback may silently turn missing media/evaluation into a learner error.

A full downloadable offline curriculum is not required for launch.

---

## 10. Detailed Commercial Rules

### Rule 1 — The coach recommendation is commercially neutral

The priority engine ranks learner value and evidence need. It does not add a “paid-feature” weight.

If the highest-value action is temporarily unavailable under a future quota, the coach says so and chooses the best valid alternative. It does not pretend the second-best action was always the first choice.

### Rule 2 — Entitlement never changes evidence semantics

Identical content, conditions, and learner response receive the same evidence interpretation regardless of plan.

### Rule 3 — Core data remains learner-owned

Access to export/delete and already-created history cannot be used as renewal leverage.

### Rule 4 — Monetize incremental cost/convenience before fundamentals

Paid value should first attach to Class B/C capacity, faster processing, additional adaptive interaction, or convenience—not objective scoring, mistake memory, or the readiness formula.

### Rule 5 — Quotas are transparent before action

If a future action consumes scarce premium capacity, the learner should know before beginning a long task whose evaluation would be blocked. A completed Writing/Speaking attempt should not discover only afterward that evaluation is impossible because of an undisclosed quota.

### Rule 6 — A payment failure is not a learning failure

Payment/entitlement problems never create a mistake, lower mastery, invalidate already valid evidence, or change readiness directly.

### Rule 7 — Cost scarcity lowers service richness before evidence honesty

When cost must be reduced, prefer:

- less generative novelty;
- slower/asynchronous evaluation;
- fixed interaction instead of open-ended interaction;
- fewer premium second opinions;
- smaller but validated content rotation.

Do not prefer:

- invented deterministic scores for open production;
- hiding uncertainty;
- treating typed Speaking as oral evidence;
- reusing exposed mock forms as independent readiness evidence;
- silently skipping an entire pass-critical skill.

### Rule 8 — The learner can complete a preparation episode

The commercial product should be designed around a finite exam goal. It should not create artificial dependency after the learner becomes Ready to Book or passes. Post-goal maintenance/new-exam options may exist later, but subscription retention is not the coaching objective.

---

## 11. Edge Cases / Failure or Uncertainty Handling

### Expensive-action quota is exhausted while Oral evidence is stale

Show the current Oral state and evidence age honestly. Offer cheaper valid oral practice/fixed interaction where useful. If fresh decision-grade evaluation is impossible until capacity returns, mark that evidence gap explicitly; do not freeze an old “Safe” label as though nothing changed and do not infer Oral from other skills.

### Learner is on free/core access but wants a full mock

If the future free model includes sufficient readiness-grade capacity, allow the relevant measured form/cadence. If capacity is temporarily limited, offer a component/mini mock that answers the highest-value question and clearly state what remains unmeasured. Never show a “passing full mock” result from a partial simulation.

### Learner cancels immediately before the exam

Cancellation does not delete current evidence, history, or readiness interpretation. Premium-capacity actions may stop according to the future plan rules, but the learner retains their preparation record, export/delete access, and whatever core practice remains available.

### Payment or entitlement service is unavailable

Do not block access to locally available history or misclassify learner work. Commercial-service failure is operational failure, not learner failure. Exact offline entitlement mechanics are architecture work.

### AI provider becomes too expensive

Use the cheapest validated alternative, reduce optional escalation, rely more heavily on reviewed reusable content/fixed interaction, and preserve lower-confidence/pending states where evaluation cannot be responsibly reproduced. Do not redesign the product around a provider-specific capability.

### Learner refuses sign-in

First-use/core local coaching remains possible under Stage 24. Features that genuinely require identity continuity, such as future cloud sync or paid entitlement recovery, may be unavailable; the product explains that boundary before data loss or purchase risk occurs.

### Learner has no microphone

Use the Section 9.8 fallback. Do not make microphone hardware a paywall problem or infer Oral readiness.

### Learner requires transcript support for Listening

Allow supported practice with transcript when useful and record the assistance. Do not count it as clean standard P4 Listening evidence. Accessibility does not mean falsifying what was measured.

### Cost data is still sparse

Do not invent an exact quota or price. Measure unit cost and action frequency first, then choose a commercial allowance with a meaningful safety margin.

### A future free user cannot reasonably reach complete readiness under the planned limits

Do not launch that tier as a “complete free exam coach.” Increase the allowance, offer a transparent meaningful trial, or use a paid-only preparation model.

---

## 12. Relationship to Other Bestehen Stages

- **Stage 01 — Product Thesis:** the exam-coach objective outranks monetization and engagement.
- **Stage 02 — Learner Journey:** first value still precedes an account/payment wall; the preparation episode remains finite and goal-oriented.
- **Stages 03–08 — Diagnostic, Learner Model, Mistakes, Coach, Loop, Progression:** these are core product behavior, not premium entitlements.
- **Stages 09–11 — Objective/Listening coaching:** deterministic scoring and reusable/cached content/audio define the low-cost default.
- **Stages 12–13 — Writing/Speaking:** define the main recurring AI cost centers and confidence-preserving fallbacks.
- **Stage 14 — Review:** review remains core and deterministic rather than a paid SRS product.
- **Stage 15 — Readiness:** one readiness model applies across tiers; pass probability remains withheld until calibrated.
- **Stage 16 — Mocks:** high learner-time/fresh-content/productive-evaluation cost justifies careful cadence and future capacity rules, not false partial mocks.
- **Stage 17 — Ready to Book:** the consequential recommendation cannot be sold as a different paid truth.
- **Stage 18 — Coach Personality:** upgrade messaging must not become pressure, shame, urgency theater, or fake intimacy.
- **Stage 19 — Information Architecture:** monetization should not replace Coach/Home with a storefront or clutter core screens with paywall prompts.
- **Stage 20 — Progress and Motivation:** no XP/currency economy should be introduced to support monetization.
- **Stage 21 — Content Strategy:** approved content is generated/validated ahead of use when possible and reused safely; Corpus rights remain independent of payment.
- **Stage 22 — User Controls / Corpus Contract:** learner choice stays separate from evidence interpretation; paid status is another non-evidence condition.
- **Stage 23 — Exam Date / Habit Support:** urgency never becomes subscription pressure or manipulative renewal messaging.
- **Stage 24 — Analytics / Account / Data:** remains authoritative for success metrics, cost measurement, sign-in, data retention, portability, deletion, offline behavior, and privacy-sensitive AI handling.
- **Current live Stage 25 Accessibility section:** resolved in Section 9 of this document.
- **Current live Stage 27 Business/Cost section:** resolved here early because it overlaps the prompt-defined Stage 25 objective; later work should not invent a conflicting cost model.
- **Stage 28 — Final Specification:** should carry forward private-first operation, core/non-core boundaries, AI cost classes, data rights, commercial neutrality of readiness, and the accessibility/device rules above.

---

## 13. Cost Notes

## 13.1 Preferred low-cost default

Bestehen should be able to sit idle at very low cost and serve ordinary practice primarily from reusable assets and deterministic product logic.

Preferred operating pattern:

- static/reusable approved content rather than runtime generation;
- cached/pre-generated audio;
- deterministic objective scoring;
- deterministic learner-state/readiness/review updates;
- template/structured coach explanations;
- one productive evaluation call rather than chains of redundant calls;
- stronger-model escalation only when uncertainty and decision stakes justify it;
- fixed/bounded Speaking interaction where sufficient;
- batch/offline content generation and QA;
- structured evidence rather than full session replay;
- ephemeral raw Speaking audio;
- storage focused on durable learner evidence and approved content, not duplicate telemetry.

## 13.2 No invented euro budget

This stage intentionally does not set a monthly euro ceiling or cost per learner before implementation measurements exist.

The product requirement is instead:

1. idle baseline should be near the unavoidable minimum;
2. every materially variable AI/speech/media action must be measurable;
3. ordinary objective training should not have meaningful per-attempt model cost;
4. an expensive action must have a lower-cost fallback or a confidence-preserving pending state;
5. a public plan must know observed unit cost and worst-case usage before setting quotas/prices;
6. infrastructure should scale gradually from personal-project usage rather than require enterprise spend to prove the product.

## 13.3 Storage-cost expectations

Store what supports learning truth and user ownership:

- structured evidence/history;
- learner-authored Writing where retained under Stage 24;
- compact transcripts/evaluations;
- versioned approved content/forms;
- reusable audio assets;
- minimal product/cost analytics.

Avoid as defaults:

- permanent raw Speaking recordings;
- duplicate generated variants with no reuse value;
- raw clickstream/session replay;
- duplicated Corpus assets in the learner store;
- indefinite technical logs unrelated to learner evidence.

## 13.4 What justifies spending more later

Upgrade cost only when evidence shows a meaningful benefit such as:

- stronger Writing/Speaking evaluator agreement/calibration;
- materially better oral interaction validity;
- target-condition audio quality that changes Listening evidence validity;
- enough active learners that manual/batch processing becomes a bottleneck;
- enough real TELC outcomes that more rigorous calibration meaningfully improves readiness truth.

“Premium-feeling AI” by itself is not justification.

---

## 14. Decisions Made

1. Set the initial operating state to **private, personal, free/non-commercial**, with no billing or monetization surface.
2. Chose **no subscription design yet**; preserve free-core/paid-capacity as the preferred future direction if public economics support it.
3. Defined the fallback: if a meaningful free core is not viable, prefer paid-only/meaningful trial over a crippled free coach.
4. Prohibited monetization from changing readiness semantics, pass rules, evidence interpretation, or coach prioritization.
5. Rejected ads, sponsored coaching, lead-selling, and learner-data monetization as the current business model.
6. Defined non-negotiable core coaching capabilities across all five skill areas, mistake memory, review, readiness truth, history, data rights, and accessibility.
7. Classified costly capabilities into near-zero, bounded-variable, and high/uncertain variable cost classes.
8. Defined selective stronger-model escalation for Writing and Speaking rather than routine premium evaluation.
9. Kept adaptive live Speaking for cases where adaptive interaction adds evidence value; fixed/bounded partner behavior remains the cheap default when sufficient.
10. Kept audio/content generation primarily batch, reviewed, cached, and reusable.
11. Defined future quota principles around expensive actions rather than sessions, questions, readiness views, or pass-critical skills.
12. Defined graceful quota exhaustion that preserves evidence truth and existing progress.
13. Preserved Stage 24 account-optional first use, export, deletion, retention, sync, offline, and privacy rules across future tiers.
14. Defined cancellation/expiry so learner history and existing readiness are not held hostage by payment status.
15. Kept Corpus commercially and experientially separate from App access.
16. Resolved the live Stage 25 Accessibility/Device checklist with a responsive-web, phone-first-but-not-phone-only launch model and explicit keyboard, screen-reader, contrast, scaling, transcript, microphone, timing, and low-connectivity rules.
17. Resolved the overlapping live Stage 27 business/cost items without creating a second future operating model.
18. Kept numeric prices, quotas, budget ceilings, and commercial packaging deferred until observed unit costs and usage exist.

---

## 15. Open Questions / Deferred Decisions

There are **no owner decisions blocking Stage 25**.

The following are intentionally deferred because current product evidence is insufficient or because they belong to legal/architecture/commercial implementation:

- exact public launch timing;
- whether the eventual paid mechanism is subscription, one-time preparation pass, trial + paid, credits, or another model;
- actual prices, currencies, VAT/tax treatment, refund policy, discounts, family plans, student pricing, and payment processor;
- exact free/paid quotas, reset cadence, overage behavior, and entitlement implementation;
- numeric personal-project monthly budget ceiling;
- hosting/model/speech/TTS vendors;
- public-service legal terms and jurisdiction-specific retention requirements;
- whether verified real-exam results or human expert review ever justify their privacy/operational cost;
- whether native mobile apps are worthwhile after responsive web usage is validated;
- exact supported browser/OS versions and implementation accessibility test tooling;
- exact accommodation profiles for TELC target-condition evidence, which should be verified against current official rules before being represented as equivalent target conditions.

These deferrals keep options open without leaving the business/product contract undefined.

---

## 16. Definition of Done Check

### Prompt-defined Stage 25 objective

- [x] Initial personal/private/free state is decided.
- [x] Future free/paid principles are defined without prematurely designing subscriptions.
- [x] Expensive AI capabilities and later quota candidates are identified.
- [x] Premium-AI invocation conditions and cheaper fallbacks are defined.
- [x] Non-negotiable core coaching features are defined and protected from monetization distortion.
- [x] Account/data portability and learner-data retention/deletion expectations are preserved and extended for commercial states.
- [x] Product boundaries and explicitly non-commercial initial scope are defined.
- [x] Cost philosophy, batching/caching, generated-audio, storage, and gradual-scale principles are defined.

### Current live Stage 25 checklist

- [x] Launch platform is defined.
- [x] Phone-first vs tablet/desktop expectations are defined.
- [x] Keyboard navigation expectations are defined.
- [x] Screen-reader expectations are defined.
- [x] Color/contrast requirements are defined.
- [x] Text scaling is defined.
- [x] Caption/transcript expectations are defined.
- [x] Microphone-permission fallback is defined.
- [x] Accessibility for timed experiences is defined.
- [x] Low-connectivity behavior is defined.

### Overlapping current live Stage 27 business/cost checklist

- [x] Personal-project assumptions are confirmed.
- [x] Acceptable recurring-cost philosophy is defined.
- [x] Premium-AI justification is defined.
- [x] Cheap/deterministic fallbacks are defined.
- [x] Caching/batching expectations are defined.
- [x] Generated-audio cost strategy is defined.
- [x] Storage-cost expectations are defined.
- [x] Initial free/paid tier decision is defined.
- [x] Enterprise-scale infrastructure is explicitly not required.

**Stage 25 is product-shaped when later design/architecture can preserve one complete exam-coaching product at personal-project cost, can add public monetization later without changing learning truth, and does not need to invent whether accessibility, portability, or pass-critical skills are optional commercial extras.**
