# Bestehen / App — Stage 26: Accessibility, Platform, and Non-Functional Expectations

> **Status:** Authoritative Stage 26 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Platform promise:** Bestehen works as a responsive, accessible web exam coach on ordinary modern devices; routine feedback feels immediate, expensive feedback may finish asynchronously without blocking learning, voice is captured only when the learner deliberately uses it, and a technical failure can never masquerade as learner failure or silently corrupt target-condition evidence.

## 1. Purpose and Scope

This document defines the product-level platform, accessibility, browser, microphone/audio, latency, offline, privacy, and reliability expectations that later design and architecture must satisfy for Bestehen / App.

Earlier stages already define the learner experience, evidence model, accessibility baseline, data contract, cost policy, and semantics of target-condition mocks. Stage 26 does **not** replace those decisions. It closes the remaining non-functional gaps so implementation does not need to invent important learner-facing behavior when a browser is unsupported, the microphone is denied, AI feedback is slow, connectivity drops, a timed mock crashes, or an accessibility accommodation changes the conditions being measured.

This stage is deliberately product shaping rather than technical architecture. It defines:

- which device/browser experiences are first-class at launch;
- what must remain usable on phone, tablet, and desktop;
- microphone/audio permission, preflight, recording, and fallback behavior;
- the accessibility acceptance baseline and keyboard/screen-reader behavior;
- latency classes for local/deterministic work, model-backed evaluation, and adaptive speech interaction;
- what “offline” and “low connectivity” mean at launch;
- raw voice/audio privacy and retention boundaries;
- what reliability means during ordinary practice versus a timed P4/mock block;
- recovery, pending, invalidation, and evidence-preservation behavior after failures;
- launch requirements, acceptable degradations, later enhancements, and cost-sensitive operating choices.

### Core decision

**Bestehen launches as a responsive web product with a strict evidence-preserving degradation model.**

The preferred behavior is not “everything works everywhere.” The preferred behavior is:

1. make the core coach usable on supported modern browsers across phone and desktop;
2. detect whether a high-stakes activity can be run fairly before it begins;
3. keep ordinary interaction and deterministic feedback fast;
4. let slower AI work become **pending** rather than block the learner;
5. preload and checkpoint timed work so a transient network problem does not erase effort;
6. downgrade or invalidate only the evidence whose actual conditions were compromised;
7. never blame the learner for browser, network, microphone, media, evaluator, or App failure;
8. avoid enterprise-grade complexity when a simple fail-safe product rule gives the learner the same evidence truth.

### In scope

- responsive web and mobile-browser priorities;
- supported browser-family expectations;
- microphone and audio-output requirements;
- permission and equipment preflight;
- keyboard, screen-reader, contrast, text-scale, motion, and timed-accessibility behavior;
- deterministic, network-backed, AI-evaluation, and adaptive-partner latency classes;
- offline and low-connectivity expectations;
- raw voice/audio privacy, transmission, retention, and telemetry boundaries;
- timed-mock preflight, autosave/checkpointing, failure recovery, timer behavior, media readiness, and pending evaluation;
- launch acceptance/degradation/later-enhancement model;
- personal-project cost and complexity limits.

### Out of scope

- framework, hosting platform, database, service topology, API style, queue technology, service worker, PWA framework, or native wrapper;
- audio codec, capture library, media container, streaming protocol, STT/TTS/evaluation vendor, or exact model;
- analytics vendor, observability stack, synthetic-monitoring product, alerting provider, or exact infrastructure SLA;
- final visual design system or component library;
- legal interpretation of accessibility law, data residency, processor contracts, or official TELC accommodation eligibility;
- native iOS/Android applications at launch;
- a full offline-content architecture;
- provider-specific cost caps or public pricing/quotas.

Those are later design, architecture, legal, or operating choices. They must satisfy the product behavior defined here.

---

## 2. Inputs / Existing Decisions

Stage 26 preserves the shared Product Overview, shared Identity, and all App Stages 01–25.

### 2.1 Product and evidence invariants

Earlier stages establish that:

- Bestehen is a calm, direct, evidence-based **personal German exam coach**;
- Readiness is primary and Written/Oral pass risk remains separate;
- missing evidence is unknown, never zero;
- technical, content, media, or evaluator failure is a **non-learner invalidation**, never a skill failure;
- assistance is part of the evidence condition, but non-answer-bearing accessibility support does not weaken capability evidence merely because it exists;
- P4/target-condition evidence is valid only when the claimed timing, playback, reference, interaction, preparation, and assistance conditions were actually reproduced;
- a learner may stop any mock, but convenience interruption can narrow the resulting target-condition claim;
- a target-condition result is never preserved by pretending an altered environment was unchanged.

Stage 26 treats those semantics as non-negotiable reliability requirements.

### 2.2 Existing platform/accessibility baseline from Stage 25

`app/25-business-model-and-product-boundaries.md` already decides:

- responsive web is the preferred launch platform;
- ordinary coaching is **phone-first in usability**, not phone-only;
- tablet/desktop receives stronger layout for Writing, long Reading, evidence inspection, and full mocks;
- no pass-critical skill is desktop-only merely for convenience;
- all core desktop/web flows are keyboard operable;
- core screens expose meaningful screen-reader semantics;
- WCAG 2.2 AA is the product baseline;
- core flows support 200% text scaling/reflow;
- instructional audio has text equivalents while target Listening transcripts remain evidence-sensitive;
- denied microphone access does not block the rest of the product and typed rehearsal is not oral evidence;
- ordinary timers can adapt, while target-condition timing remains evidence-specific;
- already-loaded work should degrade usefully under poor connectivity;
- target-condition mocks should preload required media before the timer starts.

Stage 26 **deepens** those decisions. It does not reopen whether responsive web, accessibility, or low-connectivity support matters.

### 2.3 Existing account/data/privacy contract from Stage 24

`app/24-analytics-and-success-metrics.md` already decides:

- sign-in is not required for first use;
- local-first/single-device operation is acceptable initially;
- structured progress/evidence may be retained because it supports coaching explainability;
- learner-authored Writing may be retained with evidence history;
- raw Speaking audio is **ephemeral by default** and normally deleted after evaluation is finalized;
- if a speaking evaluation cannot finish because of a technical/evaluator problem, raw audio may be retained temporarily for no more than **7 days** before deletion or unresolved/invalid handling;
- permanent raw-audio history is not a launch requirement;
- full offline parity is not required;
- AI receives only the minimum learner data required for the current job;
- raw audio is sent only when speech processing requires it;
- learner responses/audio/outcomes are not intentionally contributed to third-party/general model training without separate explicit opt-in;
- reconnection must not create duplicate learner evidence.

Stage 26 defines how those rules behave during capture, low connectivity, failure, and timed use.

### 2.4 Existing mock/reliability semantics from Stage 16

`app/16-mock-exams.md` already decides:

- every mock declares scope, duration, rules, equipment needs, target blueprint, and result promise before Start;
- Clean target-condition, Valid but modified, Partially valid, Invalid/excluded, and Pending evaluation are distinct states;
- a convenience pause inside a continuous target block removes the unchanged continuous-target claim unless a verified accommodation says otherwise;
- completed unaffected blocks may remain valid after an interruption;
- a device/App crash is technical invalidation, not learner failure;
- one broken Listening asset does not lower Listening ability;
- unavailable productive evaluation leaves the result pending;
- no convenience pause/resume may be hidden as continuous target-condition evidence.

Stage 26 adds the **preflight and resilience expectations needed to make those states operationally trustworthy**.

### 2.5 Existing audio and productive-skill cost boundaries

Stages 11–13, 21, and 25 already establish:

- Listening scripts/audio should normally be created, reviewed, and cached before use;
- routine objective scoring is deterministic;
- fixed/prerecorded Speaking interaction is preferred where it can validly test the intended behavior;
- adaptive generative Speaking is justified when the learner’s specific meaning must change the partner’s next turn;
- Writing/Speaking evaluation are the major recurring AI-cost actions;
- stronger model/evaluator escalation is reserved for uncertainty, contradiction, or pass-critical/high-stakes cases;
- an expensive second call is not needed merely to update Readiness, Mistake Memory, analytics, or coach wording.

Non-functional expectations must preserve those operating economics.

### 2.6 Stage-numbering continuity

The live App checklist still contains an older Stage 26 titled **Product Analytics and Evaluation**. Stage 24 already resolved every substantive analytics/evaluation item in that legacy section while also resolving the Stage 24 data/account checklist mismatch.

Stage 26 therefore uses this repository rule:

- **Stage 24 remains authoritative for product analytics/evaluation.**
- **Stage 25 remains authoritative for the baseline accessibility/device and business/cost boundaries.**
- **Stage 26 is authoritative for the deeper accessibility/platform/non-functional expectations in the current Stage 26 agent prompt.**

The live checklist should retain a continuity note and point the old analytics checkboxes to Stage 24 rather than invent a duplicate metric model.

No earlier shaping document requires a product-decision reversal.

---

## 3. Decisions and Rationale

## 3.1 Launch as responsive web; do not require native apps

**Decision:** The launch product is one **responsive web experience** for phone, tablet, and desktop/laptop browsers.

Native iOS, Android, Windows, or macOS applications are not launch requirements. An installable PWA may be useful later, but installability is not part of the learner promise.

### Why

Responsive web is the best personal-project trade-off because it:

- gives phone access for frequent short sessions;
- gives desktop/laptop space for Writing and long mocks;
- avoids duplicating the entire coach, evidence, media, accessibility, and update surface across native clients;
- makes browser-based microphone/audio and accessibility capabilities broadly available;
- keeps deployment and maintenance cheap while the learning model is still being validated.

A native application is justified later only if measured web limitations materially hurt a pass-critical experience such as reliable background/offline media, speech capture, notifications, or device integration.

## 3.2 Phone is first-class for daily use; larger screens are first-class for long work

**Decision:** The product has **two equally legitimate usage postures**, not one universal device bias.

### Phone-first tasks

The following must be comfortable and fully usable on a modern phone:

- Coach/Home and Today’s plan;
- diagnostic microtasks;
- Review and short repair/fresh checks;
- most Reading and Language Elements practice;
- Listening practice;
- ordinary Speaking capture/partner turns;
- Readiness summary, blockers, and Progress;
- goal/date and settings;
- short Writing/repair tasks.

### Large-screen-optimized tasks

Tablet/desktop/laptop should provide a substantially better layout for:

- full-length Reading and shared Reading + Sprachbausteine blocks;
- 30-minute target Writing;
- evidence inspection and long progress history;
- section/full mocks;
- side-by-side prompt/response or source/answer relationships where useful.

The coach may recommend a larger screen for comfort, typing quality, and rehearsal. Screen size is **not by itself a validity requirement** unless the target exam/accommodation semantics genuinely depend on it.

### Product rule

A pass-critical skill may not be artificially locked to desktop merely because desktop is easier to design. If a particular browser/device cannot support the necessary media/input/reliability contract, the product may block the **specific high-stakes activity** and explain why; it must not block unrelated coaching.

## 3.3 Support a deliberately bounded evergreen browser set

**Decision:** Bestehen supports a small set of modern browser families rather than spending personal-project effort on legacy-browser parity.

### First-class launch browser families

The product support expectation is the **current stable and immediately previous major release family** of:

- Chrome on desktop;
- Edge on desktop;
- Firefox on desktop;
- Safari on macOS;
- Safari on iPhone/iPad;
- Chrome on Android.

Exact version numbers are an implementation/release-management concern because browser versions move continuously. The product contract is “current + previous major family,” not a frozen list in the PRD.

### Not first-class at launch

The launch does not promise full QA coverage for:

- end-of-life browsers;
- Internet Explorer;
- niche browser forks;
- embedded in-app browsers/webviews whose media/storage behavior is materially restricted;
- browsers whose privacy/private mode prevents the persistence required for a fair timed mock;
- enterprise-locked versions several releases behind the support window.

### Degradation rule

An unsupported browser should still be allowed to show low-risk content where it works, but Bestehen must **not pretend a capability is supported after preflight fails**.

Examples:

- basic Reading may remain usable;
- Speaking recording may be disabled if microphone capture is unsupported;
- a clean timed mock may be disabled if durable checkpointing or required media APIs are unavailable;
- the learner receives a short “use a supported browser for this activity” instruction rather than a generic crash.

The browser support matrix should be reassessed from actual learner usage rather than broadened pre-emptively.

## 3.4 Microphone permission is contextual, explicit, and never global

**Decision:** Bestehen requests microphone permission **only when the learner deliberately starts a voice-dependent action**.

It must not request microphone access:

- on first page load;
- during general onboarding before a voice action is chosen;
- while the learner is doing Reading, Language Elements, Listening-only, or Writing work;
- in the background “just in case” Speaking appears later in the session.

Before the permission request, the learner sees why the microphone is needed and what happens if they decline.

### Required recording behavior

When capture is active:

- a visible recording state is always present;
- the learner can stop/cancel according to the current task rules;
- no hidden/background capture continues after the task finishes;
- capture stops when the learner leaves or cancels the recording flow, subject only to preserving a recording already explicitly submitted for evaluation;
- a microphone failure cannot become a zero/poor Speaking score.

This is both a trust requirement and a privacy requirement.

## 3.5 Use equipment preflight before high-stakes audio/voice work

**Decision:** Ordinary practice can discover equipment problems lazily; a clean target-condition Listening/Speaking block or mock **must not begin before a short preflight says the required environment is usable**.

### Listening preflight

Before a clean measured Listening block:

- required audio assets for the measured block are locally ready enough that a transient fetch delay should not interrupt playback;
- audio output can be heard at a usable level;
- the browser can play the required format;
- the learner is warned that changing playback rules or opening transcript/help changes the evidence claim.

### Speaking preflight

Before a clean measured oral block:

- microphone permission is granted;
- input is detectable;
- a short test confirms the recording is not silent/clipped/unusable;
- output/partner audio works when required;
- the required partner mode is available;
- the learner understands that typed fallback will not count as oral evidence.

### Failure behavior

If preflight fails, the learner may:

- retry setup;
- choose ordinary/non-measured practice with a supported fallback;
- switch device/browser;
- continue another non-voice/non-audio skill.

Bestehen does not start a “clean” mock and discover halfway through that it never had the equipment required to score it fairly.

## 3.6 Accessibility baseline remains WCAG 2.2 AA, with evidence-aware accommodations

**Decision:** WCAG 2.2 AA remains the launch product baseline for core learner-facing flows. Stage 26 adds that accessibility acceptance is part of **feature completeness**, not a later polish pass.

A core flow is not launch-complete if a learner cannot perform its normal actions with the shaped accessibility mode that applies to that capability.

### Keyboard

All core desktop/web flows must support:

- logical sequential focus order;
- clearly visible focus;
- activation without a pointer;
- keyboard-accessible answer choices, dialogs, media, repair, navigation, and mock controls;
- a non-drag equivalent for matching/reordering interactions;
- escape/close behavior where appropriate without trapping focus;
- focus returning to a sensible location after dialogs or dynamic feedback;
- no shortcut as the only way to perform an action.

Timed work must not require a mouse-only gesture to submit, replay within allowed rules, move among answer fields, or stop a recording.

### Screen readers and semantic output

Core flows must expose meaningful programmatic semantics for:

- heading/task structure;
- question/answer groups;
- selected state;
- errors and validation;
- correctness/feedback state after submission;
- readiness band and Written/Oral status;
- evidence confidence and blockers;
- mock rules, timer state, and completion state;
- recording state;
- pending/invalid technical state;
- charts/bars through equivalent textual summaries.

Dynamic updates must be announced usefully rather than noisily. A countdown should not announce every second; material timer warnings and state changes should be available without making the screen reader unusable.

### Color, contrast, text, reflow, and motion

- WCAG 2.2 AA contrast remains the baseline.
- Correct/incorrect, risk/safe, selected/unselected, pending/invalid, and evidence-confidence states always have a non-color indicator.
- Core flows remain usable at 200% zoom/text scaling.
- Ordinary controls must not require two-dimensional scrolling after reflow; long passages may scroll vertically as expected.
- Primary actions and timers must not overlap or disappear at large text sizes.
- Reduced-motion preferences are respected for non-essential animation.
- No readiness, celebration, or timer animation may be required to understand a state.

### Captions/transcripts remain capability-sensitive

- coaching/instructional audio has a text equivalent;
- Listening transcript access after the attempt is normal diagnosis/repair support;
- live transcript/caption during a clean standard Listening claim is not allowed unless the current target/accommodation explicitly permits an equivalent condition;
- Speaking transcript can support review/diagnosis, but it cannot replace the original oral evidence for fluency/intelligibility;
- captions on a partner turn can be used in supported practice when appropriate, with the actual evidence condition recorded.

Accessibility support is never treated as a moral or motivational failure. When a support changes the tested capability, Bestehen changes the **evidence label**, not the learner’s dignity or history.

## 3.7 Timed accessibility is adaptable in practice and conservative in target claims

**Decision:** The product separates **access to learning** from **equivalence to standard target conditions**.

### Ordinary practice

The learner may:

- hide or visually de-emphasize a timer;
- pause;
- extend time;
- use enlarged text;
- use keyboard/screen reader;
- use non-answer-bearing input accommodations;
- choose a lower-distraction mode.

The actual timing/support condition is stored where it matters. The learner still gets useful coaching evidence.

### P4 / clean mock

A standard clean P4 claim uses the current target timing/interaction rules.

If the learner needs extra time, a pause, transcript/caption, or another change that could alter the capability being measured:

- the attempt remains valuable;
- the true condition is preserved;
- the standard target-condition claim is **not** automatically granted;
- a future explicitly represented, verified exam-accommodation profile may define an equivalent target-condition path.

Bestehen should not make the learner choose between access and having their work saved. It should make the **meaning of the evidence** honest.

## 3.8 Define explicit latency classes rather than one vague “fast” requirement

**Decision:** Bestehen uses four learner-facing latency classes. These are initial launch UX targets, not provider SLAs or psychometric constants. They should be measured and adjusted after real use without weakening the behavior contract.

### L0 — Interaction acknowledgement

Examples:

- keypress/typing;
- answer selection;
- Start/Stop/Submit button acknowledgement;
- timer display;
- opening local UI state.

**Target:** visible response within approximately **100 ms** for ordinary local interaction.

The product should never intentionally wait for a server/model before acknowledging a learner action.

### L1 — Deterministic result/state feedback

Examples:

- objective answer scoring;
- moving to the next local item;
- updating a due-review state;
- recalculating a deterministic readiness/session state from already available structured evidence;
- showing a cached reviewed explanation.

**Target:** normally **under 1 second**, with a launch p95 expectation of **≤1 second** after the learner submits when the required data is already available.

If work unexpectedly exceeds roughly **2 seconds**, show an explicit progress/pending state rather than a frozen UI. The response remains saved.

### L2 — Standard AI-backed evaluation

Examples:

- one Writing evaluation;
- post-turn/part Speaking transcription and structured evaluation;
- a model-backed repair that cannot be served from reviewed content.

**Target:** first useful result normally within **15 seconds**; **up to 30 seconds is an acceptable connected degradation**.

At approximately 30 seconds without a trustworthy result, the learner experience changes from “waiting” to **Pending evaluation**:

- save the response;
- let the learner continue with other valid work or leave the session;
- complete the evaluation when possible;
- do not invent feedback to fill the gap;
- do not score the learner as weak because evaluation is unavailable.

A stronger/second evaluator can take longer because it is an exception, but it must not hold the entire App hostage. A high-stakes mock may show objective results while Writing/Speaking remain pending.

### L3 — Adaptive interactive partner turn

For a mode where the partner must react to the learner’s specific meaning:

**Target:** begin the next useful partner response within approximately **2 seconds** after the learner’s turn is recognized as complete; **up to 4 seconds** is acceptable for ordinary turn-based rehearsal.

If repeated partner waits exceed approximately **5 seconds**, the interaction is materially degraded. Bestehen should:

- move to a bounded/fixed partner fallback when that still tests the intended behavior; or
- pause/end the adaptive interaction and preserve completed evidence; or
- label the resulting interaction as modified/lower-confidence if the delay materially altered turn-taking.

The product must not pay for live generative interaction merely to create animation while the learner waits. When fixed reviewed interaction measures the same capability, it is both faster and cheaper.

### Latency hierarchy rule

**No slower class may unnecessarily block a faster class.**

A Writing evaluator being slow must not prevent deterministic Reading review. A Speaking evaluator being pending must not prevent the learner from viewing objective results. A coach summary does not need another model call when structured evidence already exists.

## 3.9 Full offline parity is not launch scope; continuity of already-started work is

**Decision:** Stage 24’s “no full offline parity” rule remains authoritative. Stage 26 distinguishes three offline states.

### A. Already-loaded low-risk work

Where practical, the learner should be able to continue:

- already-loaded objective Reading/Language Elements/Review;
- locally available content/instructions;
- locally available progress/history;
- a Writing draft that does not yet require online evaluation.

The product preserves the true attempt time/conditions and syncs once after reconnection.

### B. Work that requires online capability

The following may require connection at launch:

- new uncached content;
- standard/stronger AI Writing evaluation;
- speech transcription/evaluation;
- adaptive generative Speaking partner turns;
- cross-device sync;
- content/media not already loaded;
- starting a clean measured block whose required assets or partner cannot be guaranteed.

The learner is told **which capability needs connectivity** rather than receiving a generic “you are offline” wall around the whole App.

### C. Timed block after connectivity loss

Connectivity loss by itself does **not** invalidate a block whose required content/media, timer, and response persistence remain fully functional locally.

If the block can continue under exactly the same target conditions:

- let it continue;
- save/checkpoint locally;
- sync once after reconnection;
- evaluator work may remain pending.

If network loss causes missing audio, partner failure, a material interruption, inability to preserve responses, or another changed condition:

- preserve unaffected completed evidence;
- mark only affected scope modified/partial/invalid according to Stage 16;
- never lower learner ability because the network failed.

### Launch offline boundary

Bestehen does **not** promise:

- downloadable full course packs;
- complete offline diagnostics;
- fully offline adaptive AI interaction;
- fully offline speech evaluation;
- cross-device offline conflict resolution across several active devices;
- every mock to be startable without connectivity.

Those are later enhancements if actual use warrants the complexity.

## 3.10 Voice/audio privacy uses explicit capture plus ephemeral raw retention

**Decision:** Raw voice is treated as a high-sensitivity operational input, not a permanent engagement asset.

### Capture

- microphone starts only after explicit learner action and permission;
- recording state is always visible;
- no background listening or ambient capture is permitted;
- stopping/canceling the voice flow stops new capture;
- the App never activates the microphone merely to infer whether the learner is present.

### Transmission

- raw audio is sent only to the processing/evaluation path that requires it;
- unrelated profile/history is not bundled with the audio by default;
- non-identifying learner/task references are preferred where external processing needs correlation;
- raw audio/transcripts are not copied into general analytics/session replay.

### Retention

Stage 24 remains authoritative:

1. keep raw audio only as long as needed to produce/resolve the intended evaluation;
2. retain structured oral evidence and a transcript only where useful for coaching/explainability;
3. delete the raw recording after evaluation is finalized;
4. when evaluation is pending because of processing failure, raw audio may remain temporarily for at most **7 days**, then it is deleted and the attempt becomes resolved from what exists or remains unresolved/invalid;
5. permanent “recording history” is not required at launch;
6. a future **Keep my recordings** capability requires explicit opt-in rather than silent policy expansion.

### Training/use boundary

Learner voice, Writing, and real exam outcomes are not intentionally contributed to third-party/general model training without separate explicit opt-in. The default provider/product configuration must support this product promise; otherwise that provider is unsuitable for the affected capability.

### Learner playback

The learner may be allowed to replay their own recording while it still exists for the current coaching/evaluation flow. Launch does not promise indefinite replay after raw audio has been deleted.

## 3.11 Reliability is stricter for measurement than for ordinary practice

**Decision:** Bestehen uses two reliability classes.

### R1 — Ordinary coaching/practice

Ordinary practice prioritizes graceful recovery and learning continuity.

If something fails:

- save completed valid responses;
- retry only what is needed;
- use cached/deterministic fallback where useful;
- let evaluation become pending;
- keep the learner moving when another valid activity exists;
- never invent evidence merely to make the session look complete.

An ordinary 25-minute session does not need enterprise active-active infrastructure to be a good product.

### R2 — Measured P4/mock work

Measured work prioritizes **fairness, continuity, auditability, and no silent data loss**.

The App must fail safe: if it cannot establish the conditions needed for a clean claim, it should not start or should narrow the claim after failure rather than pretending success.

## 3.12 Timed mocks require a launch preflight gate

**Decision:** Before starting each clean measured block, Bestehen verifies that the minimum required environment is present.

### Common preflight

The block should not start clean unless:

- the intended target blueprint/version is approved/current;
- required content for the block is loaded/available;
- required media is loaded/available;
- the browser/device supports the needed inputs/controls;
- the App can persist checkpoints for the in-progress response at a reliability level suitable for the block;
- the learner has been shown the block duration and pause/help rules;
- no known outstanding condition already makes the block non-target-equivalent.

### Additional Listening preflight

- audio output test passes;
- target playback assets are ready before the timer/playback sequence begins.

### Additional Writing preflight

- the response editor is writable and checkpointable;
- the prompt is completely loaded before timing begins.

### Additional oral preflight

- microphone test passes;
- partner/audio output is available;
- the required interactive partner mode is available;
- the product can preserve completed turn/part responses strongly enough for evaluation/recovery.

If any required condition fails, offer setup retry or a lower-stakes practice mode. Do not burn a fresh P4 form while calling the attempt clean.

## 3.13 Timed work must checkpoint learner effort aggressively enough to make data loss exceptional

**Decision:** “No silent loss of a measured learner response” is a launch requirement.

The product-level checkpoint expectation is:

- objective selections/answers are preserved whenever they change and at submission/navigation boundaries;
- a Writing draft is checkpointed continuously enough that a recoverable App/browser failure should normally lose **no more than approximately 5 seconds of recent typing**;
- each completed Speaking turn/part is committed to recoverable temporary storage before the learner advances when the browser/device permits it;
- a submission is not considered safely complete until the product has a recoverable copy or has explicitly told the learner that it could not save;
- reconnection/retry must not create duplicate learner evidence.

The architecture may satisfy this through local persistence, server persistence, both, or another mechanism. Stage 26 cares about the **learner-loss bound and evidence semantics**, not the storage implementation.

### Privacy interaction

Temporary local buffering of voice is allowed only to satisfy the explicit recording/evaluation flow and inherits the same raw-audio deletion rules. Reliability is not permission to retain voice indefinitely.

## 3.14 Timers must not silently freeze, reset, or grant extra target time

**Decision:** During a clean timed block, the learner-visible remaining time must reflect the actual target timing semantics even if the page is backgrounded or momentarily suspended.

Product rules:

- changing tabs/windows does not pause a target timer unless the target/accommodation explicitly allows a pause;
- browser suspension/device sleep must not silently freeze the clock and grant extra target time;
- reload/recovery must never reset the timer to the beginning;
- if the App cannot determine the trustworthy elapsed time after a failure, the affected continuous target-condition claim is downgraded rather than granting a guessed amount of time;
- ordinary practice timers may be pausable because they are not target-condition claims.

The exact timekeeping mechanism is architectural. The product requirement is that **target time cannot be accidentally expanded by technical behavior**.

## 3.15 Recovery preserves work before it tries to preserve a mock label

**Decision:** Recovery optimizes for learner effort and evidence truth, not for keeping the word “clean.”

### Browser reload / App crash

If a measured block is interrupted:

1. recover the most recent saved learner state when possible;
2. preserve completed unaffected self-contained units according to Stage 16;
3. explain that the in-progress continuous block may now be **modified/partial/invalid** depending on what actually happened;
4. let the learner continue the recovered form as practice when useful;
5. offer a fresh equivalent form later when a clean target-condition result is still required.

A crash cannot be used as evidence that the learner failed, and a recovered task cannot silently be relabelled as though the interruption never happened.

### Network loss

If all required assets and local persistence remain available and no target condition changes, the block may remain clean. If the loss disrupts media/interaction or forces a pause, Stage 16 validity semantics apply.

### Evaluator outage

If Writing/Speaking evaluation is unavailable after a valid measured response:

- keep the attempt **Pending evaluation**;
- show objective results that are already known;
- do not issue a complete Written/Oral/full-mock pass/fail if the missing productive result is required for it;
- finish later using the preserved response when possible;
- if the response can no longer be evaluated responsibly, mark the affected evidence unresolved/invalid rather than poor.

## 3.16 Do not set an enterprise uptime SLA before there is operational evidence

**Decision:** Stage 26 does **not** impose a launch requirement such as 99.99% availability, multi-region failover, or zero-downtime model-provider redundancy.

Those commitments would add cost and architecture before the personal project has enough usage to justify them.

Launch reliability is instead judged through product outcomes:

- a technical failure never becomes learner failure;
- a completed response is not silently lost;
- a clean mock is not started when required assets/equipment are known to be unavailable;
- already-completed unaffected evidence survives a partial failure;
- AI unavailability produces pending/fallback behavior rather than fabricated scoring;
- low connectivity does not duplicate evidence;
- target-condition timing/playback/interaction semantics are never silently falsified.

Once real usage exists, architecture/operations may define availability/error-budget SLOs from observed critical journeys. Those future SLOs must prioritize measured attempts and learner-data integrity over vanity uptime.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Platform capability matrix

| Capability | Phone | Tablet | Desktop/laptop | Connection expectation | Launch evidence consequence |
|---|---|---|---|---|---|
| Coach/Home, Readiness, Progress | First-class | First-class | First-class | Mostly tolerant after initial load | No evidence penalty by device |
| Reading / Language Elements | First-class | First-class | First-class | Loaded work may continue offline | Device does not change score semantics |
| Listening ordinary practice | First-class with working audio | First-class | First-class | Audio asset must be available | Broken playback invalidates affected learner evidence |
| Writing ordinary practice | Supported; compact editor | Strong | Strongest | Draft may continue offline; evaluation may wait | Pending evaluation is allowed |
| Speaking ordinary practice | First-class with working mic | First-class | First-class | Fixed/local asset flow can tolerate more; adaptive/eval may need connection | No mic = no oral evidence, not zero oral ability |
| Target Writing | Supported when preflight passes; larger screen recommended | Strong | Strongest | Prompt/checkpoint must be reliable | Device size itself does not change validity |
| Target Listening | Supported when preflight and media readiness pass | Supported | Supported | Measured audio must be ready before start | Media failure affects only relevant scope |
| Target oral | Supported when mic/partner preflight passes | Supported | Supported | Partner/evaluation may require connection | If interaction cannot be guaranteed, do not start clean oral block |
| Full mock | Supported when all component preflights pass; larger screen recommended | Strong | Strongest | Each measured block requires its own reliability gate | Scope validity follows Stage 16, never device prestige |

## 4.2 Browser capability states

A browser/device session can be in one of four product states:

| State | Meaning | Learner experience |
|---|---|---|
| **Fully supported** | Core tested capabilities work; high-stakes preflight may still be activity-specific | Normal product |
| **Supported with capability limitation** | General App works but one capability such as microphone, persistence, or a media feature is unavailable | Continue other skills; explain affected capability |
| **Practice-only for affected mode** | Activity can run for learning but cannot meet clean target-condition reliability/evidence requirements | Allow with honest modified/assisted label |
| **Unsupported for affected action** | The browser/device cannot run the activity fairly or preserve the response safely | Block only that action and suggest supported browser/device |

The product should diagnose the capability rather than display a blanket browser-brand error whenever possible.

## 4.3 Accessibility evidence matrix

| Support/change | Ordinary practice | Standard P4 evidence | Product rule |
|---|---|---|---|
| 200% text scaling / zoom | Fully allowed | Fully allowed | Non-answer-bearing access support |
| Keyboard instead of pointer | Fully allowed | Fully allowed | Same evidence |
| Screen reader for ordinary UI/instructions | Fully allowed | Fully allowed where it does not reveal tested visual information | Preserve actual capability tested |
| Reduced motion | Fully allowed | Fully allowed | No evidence effect |
| Visible timer hidden/de-emphasized while internal time remains enforced | Allowed | May be allowed if target timing remains unchanged | Visual presentation alone does not change target time |
| Extra time / paused timer | Allowed | Modified unless a verified accommodation profile grants equivalence | Keep true condition |
| Transcript during Listening | Allowed as supported practice | Not standard clean Listening evidence | Becomes assisted/modified unless verified target accommodation allows it |
| Typed response instead of spoken response | Learning/rehearsal | Not oral evidence | Never substitute modality |
| Captions on instructional/coach audio | Allowed | Allowed | Not testing Listening content |
| Captions on partner/exam audio | Allowed in supported practice when appropriate | Evidence-sensitive | Record condition; do not silently treat as standard auditory claim |

## 4.4 Latency behavior table

| Class | Examples | Launch target | Acceptable degradation | Failure state |
|---|---|---:|---|---|
| **L0 Interaction** | typing, selection, timer, button acknowledgement | ~100 ms | brief local jank | Never intentionally block on network/model |
| **L1 Deterministic** | objective scoring, cached explanation, local state/recommendation update | p95 ≤1 s | show explicit progress if >~2 s | Preserve response and retry/fallback |
| **L2 Standard AI** | Writing evaluation, speech transcript/evaluation, rare model repair | normally ≤15 s | ≤30 s connected wait | >~30 s becomes Pending evaluation |
| **L3 Adaptive partner** | learner-specific S2/S3 turn | response begins ~≤2 s | ≤4 s acceptable | repeated >~5 s: fixed fallback, modified interaction, or stop |

The product may later tighten these targets if measurement shows value. It should not relax them silently to hide an unnecessarily expensive/slow design.

## 4.5 Mock resilience checkpoints

A measured attempt records enough product state to answer after a failure:

- what block/form/version was running;
- when it started and what target timing applied;
- which responses were safely saved;
- which media/playback opportunities were consumed;
- which help/transcript/replay/pause conditions changed;
- whether the microphone/partner/evaluator was technically valid;
- whether the App knows the trustworthy elapsed time;
- which self-contained units completed before the failure;
- whether evaluation is complete, pending, or impossible;
- which evidence scope can still be defended.

This is a conceptual recovery contract, not a database schema.

## 4.6 Preflight outcome table

| Preflight result | Clean measured action | Alternative |
|---|---|---|
| All required capabilities ready | Start normally | — |
| Audio output fails | Do not start clean Listening/oral audio block | Fix audio or choose non-audio work |
| Mic denied/unusable | Do not start clean oral block | Typed/solo learning with no oral evidence, or another skill |
| Required media not fully available | Do not start clean block | Wait/retry fetch or choose ordinary practice |
| Durable checkpointing unavailable | Do not start high-stakes continuous Writing/full mock | Use lower-stakes practice or supported browser/device |
| Adaptive partner unavailable where interaction requires it | Do not start clean affected oral interaction | Fixed partner only when the intended evidence remains valid; otherwise practice/retry later |
| Productive evaluator unavailable before response | May still start if raw response can be preserved and learner accepts Pending outcome | Otherwise choose work that can complete now |
| Unsupported/old browser | Do not start capability whose preflight cannot pass | Continue unaffected core practice |

## 4.7 Acceptable degradation matrix

| Failure/degradation | What remains available | What is withheld/changed | Evidence rule |
|---|---|---|---|
| Slow AI | Objective tasks, history, other practice | Productive feedback becomes pending | No guessed score |
| AI evaluator unavailable | Valid response saved | Final productive/full gate result pending | No learner penalty |
| Offline after content loaded | Loaded objective work; local draft/history where available | New AI/adaptive/uncached work | Sync once; true conditions preserved |
| Mic permission denied | All non-oral work; typed rehearsal | Oral evidence and clean oral mock | Oral stays unknown/stale |
| Mic recording corrupt | Other work; possible retry | Affected speech evidence excluded | Technical invalidation |
| Listening media failure | Other tasks; unaffected completed units | Affected Listening unit | No Listening penalty for media failure |
| Browser lacks required persistence | Low-risk practice | High-stakes clean mock start | Do not risk silent response loss |
| Network drops inside fully preloaded objective block | Block may continue | Upload/sync waits | Can remain clean if conditions truly unchanged |
| Network drops during live partner turn | Preserve completed turns | Adaptive interaction may stop/fallback | Modified/partial if turn-taking was materially affected |
| App/browser crash during mock | Recover saved work | Continuous affected block loses automatic clean claim | Preserve unaffected units; fresh retake if clean evidence required |
| External service outage | Deterministic App remains usable | Only service-dependent capability affected | Never global “learner failed” state |

---

## 5. Edge Cases / Failure or Uncertainty Handling

### 5.1 Learner starts Speaking after denying microphone permission

Do not keep re-prompting aggressively. Explain that the task can be practised in text or skipped, but it will not create oral evidence. Offer **Try microphone again** as a deliberate action and keep the rest of the daily plan usable.

### 5.2 Browser permission is granted but recording is silent

Treat this as failed equipment preflight or technical invalidation, not low intelligibility. The learner can retry input setup or change device. No oral mastery/mistake update is created.

### 5.3 Learner uses a Bluetooth headset with a sudden device switch

If a clean oral block has not started, rerun the short audio/mic preflight. If the device change interrupts a measured block materially, preserve completed work and apply Stage 16 modified/partial validity. Do not guess that the recording remained fair.

### 5.4 Learner receives a phone call or device notification during a timed mobile mock

Bestehen cannot guarantee the operating system will prevent interruption. The timer must not silently pause. If the interruption materially breaks a continuous target block, preserve the work but narrow the target-condition claim. The learner can later retake a fresh equivalent form.

### 5.5 Learner backgrounds a timed tab

A clean target timer continues according to target timing semantics. Returning to the tab must not grant extra time. If the browser made trustworthy timekeeping impossible, downgrade the affected block rather than invent a favorable duration.

### 5.6 Learner reloads after losing one sentence of a Writing draft

The product target is no more than approximately five seconds of recent typing loss under recoverable App/browser failure. If more is repeatedly lost, the implementation fails the Stage 26 launch reliability expectation even if the learner can technically continue.

A crash during a continuous clean Writing block remains a technical interruption for evidence validity. Saving the text protects effort; it does not necessarily preserve the clean P4 claim.

### 5.7 Network disappears during a fully preloaded Reading + Sprachbausteine block

If the timer, prompt, choices, local persistence, and all required content remain intact, continue. Connectivity itself is not a linguistic condition and need not invalidate the block. Sync later exactly once.

If the loss forces a pause, loses answers, or removes required content, apply the narrower Stage 16 validity state.

### 5.8 Network disappears during H1 playback

If the asset was preloaded and playback proceeds exactly once without interruption, the block can remain clean. If playback stops/changes or an extra replay becomes necessary because of infrastructure, invalidate/modify only the affected scope; do not score the learner for the broken media.

### 5.9 Adaptive S3 partner becomes unavailable mid-plan

Save completed turns. If a reviewed fixed branch can continue without materially weakening the interaction claim, the App may offer it and record the partner mode. Otherwise end the measured interaction as partial/modified and schedule a fresh interactive opportunity. Do not let an AI outage create a low interaction score.

### 5.10 AI evaluation returns after the learner has left

The attempt remains the original attempt. Apply the result to its evidence history once, show it when the learner returns, and recompute dependent states deterministically. Do not create a second attempt because evaluation finished later.

### 5.11 AI evaluation times out twice

Do not keep making unbounded premium retries. Preserve the response and either:

- use the already-defined stronger one-time escalation when the result is decision-critical and economically justified;
- keep a lower-confidence partial evaluation if responsible;
- or mark the evaluation unresolved/invalid.

The learner receives a useful explanation of what is known and what needs another sample. Cost control is part of reliability, not an excuse for fabricated confidence.

### 5.12 Unsupported browser loads the App successfully but fails microphone capture

Treat this as a capability limitation, not as a whole-product ban. Reading/Writing/etc. continue. Speaking shows a clear supported-browser/device recommendation. Oral evidence remains unknown/stale.

### 5.13 Private/incognito mode prevents durable storage

Low-risk practice may still be usable, but a high-stakes measured block should not start clean if the App cannot satisfy its checkpoint/recovery requirement. Explain that the browser mode cannot safely preserve a long timed attempt and recommend a supported normal browser session.

### 5.14 Screen reader changes how a matching task is navigated

If the learner receives the same semantic task information and no answer-bearing cue, the input modality itself does not weaken evidence. If the original task depends on an inherently visual relation that cannot be represented equivalently, the App must label the limitation and avoid a false target-equivalent claim.

### 5.15 Learner needs extra target time for an official accommodation

The learner should be allowed to practise with the needed time. Until Bestehen has a verified accommodation profile representing what the learner’s real target conditions permit, store the actual condition and avoid automatically calling it standard P4. Later accommodation support should map the learner’s real exam rules rather than invent a universal “accessibility time multiplier.”

### 5.16 Raw audio is still pending after seven days

Delete the raw recording according to Stage 24. If structured/transcript evidence is insufficient to finalize the result responsibly, the attempt remains unresolved/invalid for the affected claim. Privacy retention is not extended merely to rescue analytics or model debugging.

### 5.17 Learner wants permanent voice history

Not a launch feature. If added later, it requires explicit opt-in and separate storage/privacy UX. Existing ephemeral-default users must not be silently migrated to permanent retention.

### 5.18 Service outage occurs during Ready-to-Book week

Do not weaken evidence requirements because the App is temporarily unavailable. Preserve already-valid evidence, let due dates/recency age normally, and restore access when possible. If the outage prevents a required current mock/evaluation, the coach must say the booking evidence is incomplete rather than manufacture confidence.

---

## 6. Relationship to Other Bestehen Stages

### Stage 03 — Initial Diagnostic

Diagnostic speaking permission remains contextual. No microphone means no oral evidence; diagnostic routing can continue with other skills. Stage 26 adds browser/equipment preflight and privacy capture behavior.

### Stage 04 — Learner Model

Technical validity, evaluator confidence, actual assistance/timing, and device/media conditions remain part of evidence interpretation. Stage 26 does not add a second learner model.

### Stage 06 — Daily Coaching Engine

Environment fit is now concrete: if a microphone, quiet environment, network, or long-screen context is unavailable, the coach may choose another useful task without erasing the underlying priority.

### Stage 07 — Core Learning Loop

The Attempt state must acknowledge interactions immediately and protect learner input before slower model feedback. Pending evaluation is a valid loop state; Remember cannot invent a result while Diagnose is unresolved.

### Stage 08 — A1→B1 Progression

Accessibility support and learning assistance remain separate. Product difficulty/support may adapt, while target-condition evidence preserves what actually changed.

### Stage 09 — Reading

Responsive reflow, keyboard matching, large text, and screen-reader semantics must preserve the Reading mechanism. An inherently visual task that cannot be made equivalent is labelled honestly.

### Stage 10 — Language Elements

Objective scoring remains deterministic and L1-fast. No runtime premium call is justified for routine cloze correctness.

### Stage 11 — Listening

Stage 26 operationalizes cached/preloaded audio, output preflight, exact target playback, transcript privacy/access, and media-failure invalidation.

### Stage 12 — Writing

Writing evaluation is L2: standard AI can be slower, but the draft is protected and feedback becomes pending instead of blocking the product. Timed Writing has the strict checkpoint and timer contract.

### Stage 13 — Speaking

Stage 26 operationalizes microphone permission, visible capture, voice privacy, partner latency, partner outage, and oral preflight. Fixed interaction remains the low-cost fallback where it still measures the intended behavior.

### Stage 14 — Review

Already-loaded deterministic review may continue under low connectivity. Review scheduling never depends on a live premium model.

### Stage 15 — TELC Readiness

Technical/access failures do not lower Readiness. Target-condition evidence uses only conditions that remain defensible after device/network/accommodation changes. Pending productive evaluation cannot be silently imputed.

### Stage 16 — Mock Exams

Stage 16 remains authoritative for validity semantics. Stage 26 supplies the required **preflight, checkpointing, timekeeping, low-connectivity, and recovery product expectations** that make those semantics feasible.

### Stage 17 — Ready to Book

A current target-condition/accommodation/technical uncertainty can continue to block Ready-to-Book when the required evidence is not defensible. Service availability cannot shortcut the gate.

### Stage 18 — Coach Personality

Technical messages continue to use fact → meaning → next action and never shame the learner. “Audio failed; this result will not count against you” is the semantic pattern.

### Stage 19 — Information Architecture

Stage 19 keeps responsive hierarchy and focused Attempt/Mock surfaces. Stage 26 adds the requirement that unsupported capability, pending evaluation, preflight, and recovery states have explicit homes without turning the whole App into an error dashboard.

### Stage 20 — Progress and Motivation

Technical failures, slow models, offline state, and stale evidence never become motivational penalties, lost streaks, or fake regression.

### Stage 21 — Content Strategy

Approved/cached content and pre-generated audio are not just cost choices; they are latency/offline/reliability enablers. Readiness/P4 forms must be preloadable and stable enough for clean measurement.

### Stage 22 — User Controls

Learners control participation, equipment fallback, and whether to continue modified practice. Bestehen controls the evidence semantics and may refuse to call a preflight-failed activity clean P4.

### Stage 23 — Exam Date and Urgency

Nearness of the exam may increase the cost of an outage, but it does not change evidence truth. Urgent plans should prefer reliable lower-cost measurement scopes rather than repeatedly retry fragile full mocks.

### Stage 24 — Analytics, Data, and Portability

Stage 24 remains authoritative for outcome metrics, account optionality, data retention/export/deletion, raw-audio retention, AI minimization, and offline semantics. Stage 26 must be measured with the lean quality analytics already shaped there—for example technical invalidation, audio validity, evaluator latency/failure, and content/media defects—without adding invasive session replay.

### Stage 25 — Business Model, Cost, Accessibility, and Device Baseline

Stage 25 remains authoritative for responsive web, accessibility/device baseline, cost classes, and private-first operating model. Stage 26 adds concrete NFR acceptance and degradation rules. Accessibility remains core and cannot become a paid feature.

### Stage 28 — Final PRD

The final specification must carry forward the platform support contract, WCAG baseline, latency classes, offline boundary, voice privacy, and mock-reliability semantics so architecture does not reduce them to vague “non-functional requirements.”

---

## 7. Cost Notes

Stage 26 has meaningful but controllable recurring-cost impact.

### 7.1 Preferred low-cost launch defaults

1. **One responsive web product** instead of native apps.
2. **Bounded evergreen browser support** instead of legacy-browser parity.
3. **Deterministic local/server scoring** for objective tasks and readiness/review state.
4. **Pre-generated, reviewed, cached audio** rather than per-listen TTS.
5. **Pre-generated/cached content** rather than runtime exercise generation.
6. **One standard Writing/Speaking evaluation** using the cheapest evaluator that meets the shaped quality bar.
7. **One stronger escalation only for material uncertainty/high stakes**, not automatic double evaluation.
8. **Fixed/prerecorded or bounded Speaking partners** when they test the behavior well enough.
9. **Adaptive live partner only where meaning-dependent interaction adds evidence value.**
10. **Short-lived raw audio**, reducing storage/privacy burden.
11. **Client/session checkpointing and media preloading** to protect timed work rather than expensive active-active infrastructure.
12. **No full offline parity** at launch.
13. **No enterprise availability SLA/multi-region redundancy** before real usage justifies it.
14. **No invasive session-replay analytics** merely to debug UX.

### 7.2 Premium/higher-cost capability invocation rules

A more expensive model/service is justified when:

- Writing/Speaking evaluation confidence is too low to support a pass-relevant claim;
- two recent comparable productive results materially contradict each other;
- a P4/readiness/Ready-to-Book result sits near a consequential pass boundary;
- adaptive S2/S3 partner behavior is necessary to test real negotiation/response rather than a fixed branch;
- a content/evaluator quality incident requires adjudication.

It is **not** justified for:

- objective scoring;
- readiness recomputation;
- review scheduling;
- routine coach copy;
- generic progress summaries;
- repeating an already-structured evaluation in another prose format.

### 7.3 What would justify upgrading later

Spend/complexity may increase if measured learner value justifies:

- broader device/browser test coverage;
- formal third-party accessibility audit tooling/services;
- native wrappers/apps because web limitations are proven material;
- downloadable offline practice/mock packs;
- local/on-device speech processing;
- real-time high-quality partner interaction at greater scale;
- redundant evaluator/provider failover for public high-stakes usage;
- stronger operational SLOs after multiple real learners depend on the service.

The upgrade trigger is a measured failure of the cheap design to protect learning/evidence quality—not hypothetical scale.

---

## 8. Launch Requirements, Acceptable Degradations, and Later Enhancements

## 8.1 Launch requirements

The first usable complete product must satisfy:

- responsive web across modern phone and desktop/laptop browser families;
- current + previous major release-family support for the defined first-class browsers;
- phone-comfortable core coaching and pass-critical practice;
- stronger large-screen layouts for long Writing/mocks;
- WCAG 2.2 AA core-flow baseline;
- keyboard and screen-reader operability for core web flows;
- 200% text scaling/reflow and non-color-only states;
- reduced-motion-safe comprehension;
- contextual microphone permission and visible capture;
- microphone/audio preflight for measured voice/audio work;
- no oral score from mic/recording failure;
- instructional audio text equivalents and evidence-sensitive exam transcripts;
- L0/L1 fast deterministic interaction;
- L2 model evaluation with Pending after approximately 30 seconds rather than blocking;
- L3 adaptive-partner latency fallback behavior;
- already-loaded low-risk work continuity under poor connectivity where practical;
- target-block media preload before clean mock start;
- no clean high-stakes mock start when checkpointing/equipment/media requirements fail;
- objective answer checkpointing and continuous Writing protection with roughly a five-second recoverable-loss bound;
- completed Speaking-turn preservation where browser/device capability permits;
- no timer reset/freeze that grants hidden target time;
- technical failure preserving unaffected evidence and never lowering learner ability;
- raw audio ephemeral by default and deleted after finalized evaluation;
- raw-audio pending ceiling of seven days;
- no general-model training use of learner response/audio by default;
- deterministic/fixed/cached cheap fallbacks wherever they preserve the exam-coaching goal.

## 8.2 Acceptable launch degradations

The following are acceptable when explained honestly:

- an outdated/unsupported browser can still use unaffected low-risk features;
- an unsupported microphone/browser blocks only oral evidence, not the whole App;
- Writing/Speaking feedback may be pending rather than immediate;
- a full mock result may remain pending until productive evaluation finishes;
- low connectivity may limit new content, adaptive partner, AI evaluation, sync, or clean mock start;
- phone layout may be less spacious than desktop for long Writing/mocks, while remaining functionally complete when preflight passes;
- a recovered interrupted block may continue as practice while losing a clean target-condition label;
- a fixed partner may replace adaptive interaction when it still validly tests the intended behavior;
- full offline parity, native installability, and permanent voice history may be absent.

An acceptable degradation may reduce convenience or evidence scope. It may **not** silently turn missing capability into learner failure or pretend altered conditions were unchanged.

## 8.3 Later enhancements

Potential later enhancements, justified only by evidence of value:

- installable PWA/offline packs;
- native mobile/desktop shells;
- broader browser/device support;
- local/on-device transcription/evaluation;
- richer explicit accommodation profiles aligned to real exam permissions;
- learner opt-in permanent voice recording history;
- background/offline sync across several devices;
- more seamless cross-device mock continuation where evidence semantics remain defensible;
- provider redundancy for productive evaluation;
- wider formal accessibility audit coverage and higher-than-AA improvements where useful;
- real-time adaptive voice interaction with stronger latency guarantees;
- public-service availability SLOs/error budgets once usage warrants them.

---

## 9. Decisions Made

1. **Responsive web is the launch platform**; native apps and PWA installability are not required.
2. Daily coaching is phone-first in usability while long Writing/mocks receive stronger large-screen layouts.
3. First-class browser support is bounded to current and previous major release families of desktop Chrome/Edge/Firefox/Safari, iOS Safari, and Android Chrome.
4. Unsupported browsers degrade by capability rather than globally; high-stakes actions are blocked when preflight cannot establish fairness/recovery.
5. Microphone permission is requested only at the moment of a deliberate voice action, with visible recording state and no background capture.
6. Clean measured Listening/Speaking uses equipment/media preflight before timing begins.
7. WCAG 2.2 AA, keyboard use, screen-reader semantics, 200% text scaling/reflow, non-color-only states, and reduced-motion compatibility remain launch accessibility requirements.
8. Accessibility changes the evidence claim only when it changes the capability/target condition being measured; accessibility need itself is never learner failure.
9. Practice timing may adapt; standard P4 timing remains exact unless a verified accommodation profile says otherwise.
10. Latency is split into L0 ~100 ms interaction acknowledgement, L1 p95 ≤1 s deterministic feedback, L2 normally ≤15 s / Pending after ~30 s AI evaluation, and L3 ~≤2 s partner-turn response with fallback after sustained >~5 s degradation.
11. Slower AI cannot block faster deterministic parts of the product.
12. Full offline parity is not launch scope; already-loaded low-risk work should continue where practical.
13. Connectivity loss alone does not invalidate a fully preloaded/local target block when no measured condition changes.
14. Raw voice is ephemeral, purpose-limited, excluded from generic analytics/session replay, deleted after finalized evaluation, and retained at most seven days only for unresolved processing.
15. Learner voice/text/outcomes are not contributed to third-party/general model training without separate explicit opt-in.
16. Reliability has ordinary-practice and measured-mock classes; measured work fails safe rather than preserving a false “clean” label.
17. Each clean measured block has a preflight gate for target version, assets/media, required input, and response checkpoint capability.
18. Objective answers are checkpointed as they change; Writing should normally lose no more than about five seconds after a recoverable failure; completed Speaking turns are preserved where supported.
19. Target timers cannot silently freeze/reset through backgrounding/reload; uncertainty about elapsed time narrows validity rather than granting guessed extra time.
20. Recovery preserves learner effort and unaffected evidence before preserving the mock label.
21. Productive evaluator outage produces Pending evaluation, not learner failure or fabricated score.
22. No enterprise uptime SLA, multi-region redundancy, or full offline architecture is required before real usage justifies the cost.
23. Cost is controlled through deterministic logic, cached content/audio, bounded browser scope, ephemeral raw audio, fixed partner fallback, and selective premium evaluation.
24. Stage 24 remains authoritative for the legacy Product Analytics/Evaluation checklist; Stage 25 remains authoritative for the baseline Accessibility/Device and business model; Stage 26 deepens the non-functional contract without creating duplicate models.

---

## 10. Open Questions / Deferred Decisions

### Owner questions

**None.** The current product context is sufficient to make the Stage 26 product decisions without requiring a personal-preference or business-risk decision from the owner.

### Deferred architecture/implementation decisions

The following are intentionally **not** product questions:

- exact web framework and responsive breakpoint implementation;
- whether to implement a service worker/PWA at launch;
- exact browser feature-detection and automated test tooling;
- exact device lab/emulator matrix within the shaped browser support window;
- local versus server persistence mechanism for checkpoints;
- exact idempotency/sync implementation;
- timer implementation and time source;
- audio format/codec/container and recording library;
- media CDN/storage/provider;
- STT/TTS/evaluator/partner model vendors;
- whether speech capture is streamed or uploaded by turn/part;
- cache/storage implementation and encryption mechanism;
- observability, alerting, logs, tracing, uptime monitor, or synthetic-test provider;
- numeric infrastructure availability/error-budget SLOs after real usage exists;
- exact legal/data-residency/processor-contract requirements;
- exact representation of recognized TELC accessibility accommodations and how eligibility is verified;
- native app architecture if native clients are ever justified.

### Deferred product enhancements

- full offline content packs;
- permanent voice-history opt-in;
- richer verified accommodation profiles;
- native apps;
- wider browser support;
- local/on-device AI speech evaluation;
- public multi-user operational SLA;
- seamless cross-device continuation of active timed mocks;
- highly real-time adaptive voice conversation beyond what TELC rehearsal requires.

---

## 11. Legacy Stage 26 Analytics Checklist Reconciliation

The live checklist’s previous Stage 26 analytics items are not unresolved work. They map to `app/24-analytics-and-success-metrics.md` as follows:

| Legacy Stage 26 item | Authoritative Stage 24 resolution |
|---|---|
| Core product metrics | DSRA north star, metric hierarchy, learner-outcome catalog |
| Readiness-calibration metrics | Forward component error/bias, planning-range coverage, calibration/versioning, future real outcomes |
| Learning-outcome metrics | Capability/evidence movement, DSRA, target-condition progression |
| Repair-success metrics | Same-session transfer separated from delayed transfer/retention |
| Retention separate from learning | Delayed-retention metrics are distinct from engagement/return metrics |
| Mock-to-real comparison | Frozen pre-exam readiness/mock snapshots versus voluntary real TELC outcomes |
| Feedback/quality sampling | Learner-reported content issues, benchmark QA, human/stronger review for high-stakes uncertainty |
| AI evaluation quality | Repeatability, benchmark agreement, pass-gate flip, criterion agreement, version drift, escalation/reversal/confidence validity |
| Content-quality metrics | Defect/correction, audio validity, freshness collision, target-form health, difficulty residuals |
| Cost per active learner/session | Explicit cost-per-active-learner/session and expensive-capability monitoring |
| Avoid engagement-only optimization | Outcome hierarchy places readiness/learning quality above usage/retention |

Stage 26 therefore adds **platform and delivery-quality expectations** that Stage 24 can measure, but it does not create new competing product-success metrics.

---

## 12. Definition of Done Check

- [x] Responsive web launch priority is confirmed.
- [x] Phone, tablet, and desktop expectations are defined.
- [x] Supported modern browser-family expectations and unsupported-browser degradation are defined.
- [x] Microphone permission, visible capture, preflight, failure, and fallback behavior are defined.
- [x] Audio-output/media readiness expectations are defined.
- [x] WCAG 2.2 AA accessibility baseline is preserved and deepened.
- [x] Keyboard navigation behavior is defined.
- [x] Screen-reader/dynamic-state behavior is defined.
- [x] Color/contrast, text scaling/reflow, and reduced-motion behavior are defined.
- [x] Caption/transcript behavior is defined without weakening Listening/Speaking evidence truth.
- [x] Accessibility behavior for ordinary timed work and P4 is defined.
- [x] Deterministic versus AI latency classes and fallback behavior are defined.
- [x] Adaptive Speaking partner latency and fallback behavior are defined.
- [x] Offline/low-connectivity launch expectations are defined.
- [x] Raw voice/audio privacy, transmission, retention, and training/analytics boundaries are defined.
- [x] Timed-mock preflight is defined.
- [x] Timed response checkpoint/data-loss expectations are defined.
- [x] Timer/background/reload behavior is defined.
- [x] Crash, network, media, partner, and evaluator failure handling is defined.
- [x] Launch requirements, acceptable degradations, and later enhancements are separated.
- [x] Quality/cost trade-offs are explicit and proportionate to a personal project.
- [x] Legacy Stage 26 analytics checklist work is reconciled to authoritative Stage 24 decisions.
- [x] No architecture mechanism has been prematurely selected where product behavior is sufficient.
- [x] No owner decision remains necessary to complete this stage.

**Stage 26 is product-shaped when later design/architecture can answer not only “what should the App do?” but also “what must still be true when the learner uses a phone, keyboard, screen reader, microphone, slow network, slow evaluator, or a timed mock that experiences a failure?” without inventing a new evidence or accessibility policy.**
