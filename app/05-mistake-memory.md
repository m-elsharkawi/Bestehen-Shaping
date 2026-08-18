# Bestehen / App — Stage 05: Mistake Memory

> **Status:** Authoritative Stage 05 product-shaping decision
>
> **Product:** Bestehen / App
>
> **Launch target:** TELC B1
>
> **Memory promise:** A lost point becomes durable, explainable coaching evidence—but one uncertain error never becomes a permanent label.

## 1. Purpose and Scope

This document defines how Bestehen / App turns individual performance shortfalls into durable coaching memory. It covers what counts as a mistake event, how likely root causes are classified, when recurrence becomes a known weakness, how priority rises and falls, how repair is proven, how old weaknesses return, how evidence may influence another skill without inventing cross-modal mastery, and what the learner is told.

Mistake Memory is the bridge between an attempt and future coaching. Its job is not to archive every red answer. Its job is to preserve the smallest defensible explanation of where exam points were lost and use that explanation to choose better future practice.

This is product shaping, not a database schema or scheduling algorithm. Later stages may choose storage, interfaces, calibrated coefficients, and model providers. They must preserve the lifecycle, evidence boundaries, learner-facing contract, and low-cost defaults defined here.

### Core decision

**Bestehen remembers coachable performance shortfalls as evidence-linked episodes. It promotes a pattern to a known weakness only after independent, sufficiently confident recurrence; it retires dedicated repair only after successful transfer across fresh tasks and time.**

A mistake is therefore not synonymous with a wrong click:

- a wrong answer may have an unresolved cause;
- one attempt may reveal more than one shortfall;
- several wrong clicks in one repair loop may belong to one mistake episode;
- a technically invalid result is not a learner mistake;
- an immediate retry success is repair responsiveness, not retained mastery;
- a known weakness is a current evidence-backed coaching state, not a permanent trait.

### In scope

- mistake manifestations and root-cause categories;
- event validity, diagnosis confidence, and independent episode grouping;
- candidate, known, repairing, repaired, resolved, and reopened states;
- recurrence, opportunity-adjusted failure, priority, and time decay;
- cross-skill and cross-modality coaching transfer;
- learner-facing explanations;
- minimum necessary data and explicit overkill boundaries;
- low-cost diagnosis and explanation behavior.

### Out of scope

- exact daily-session assembly and competition between mistake work and other needs — Stage 06;
- full attempt/repair UI and skill-specific repair formats — Stages 07 and 09–13;
- final review scheduler calibration — Stage 14;
- readiness scoring and written/oral pass calculations — Stage 15;
- mock-specific scoring — Stage 16;
- final screen structure — Stage 19;
- retention, export, deletion, and raw audio policy — Stage 24;
- storage design, model vendors, and implementation architecture.

## 2. Inputs / Existing Decisions

This stage preserves the project overview, identity, and App Stages 01–04:

- Bestehen is a calm, direct, evidence-based personal German exam coach.
- The core loop is **Observe → Attempt → Diagnose → Repair → Retry → Remember**.
- The learner may begin around A1. Assistance is valid learning context, not failure.
- Readiness is the primary progress concept, with written and oral pass risk kept separate.
- Mastery, confidence, freshness, and readiness contribution are separate.
- The learner model uses an immutable evidence ledger plus derived states.
- Reading, Listening, Writing, Speaking production, and interactive speaking are direct-evidence lanes. One modality must not initialize another.
- A single diagnostic mistake is a candidate signal, not a durable known weakness.
- Stage 04 defines independent recurrence: same-item repeats and an immediate retry do not count as new independent episodes.
- Stage 04 defines recurrence bands of isolated, repeated, recurring, and persistent under target conditions.
- Evidence strength rises from excluded technical failures to recent realistic target-condition anchors.
- Fine-grained negative evidence is applied only when attribution is supported. Otherwise the task result remains broad and the cause stays unresolved.
- Corpus supplies stable skill nodes, task relationships, TELC relevance, and mapping confidence. The App owns learner events, weakness state, priority, and coaching.
- Common logic should be deterministic and financially sustainable. Productive-task evaluation should not trigger a second model call merely to maintain memory.

There are no contradictions with prior decisions. This stage makes Stage 04's mistake episode, recurrence, and repair-summary fields operational.

## 3. Decisions and Rationale

### 3.1 Remember the shortfall, not only the answer

**Decision:** A mistake event records a coachable shortfall linked to the evidence observation that revealed it. It preserves what happened, the conditions, the likely cause, and how certain that cause is.

The answer outcome remains part of the evidence ledger. Mistake Memory adds the coaching interpretation. This separation matters because the same incorrect response could arise from an unknown word, missed negation, task misunderstanding, time pressure, an attention lapse, or unreliable evaluation. Future practice should differ accordingly.

### 3.2 Separate event, episode, pattern, and weakness

**Decision:** Mistake Memory uses four levels:

| Level | Meaning | Example |
|---|---|---|
| Mistake event | One supported coachable shortfall within an attempt | Missed the restriction “nur werktags” |
| Mistake episode | All related events in one attempt/repair chain, grouped so retries are not counted as recurrence | Original miss, explanation, and same-session retry |
| Mistake pattern | Related episodes mapped to the same skill node/cause family and lane | Repeatedly misses restrictions in Reading |
| Known weakness | A current pattern that has crossed evidence, recurrence, and confidence gates | Reading restriction/negation scanning is an active weakness |

The system may remember an isolated event without calling the learner weak. This protects trust while still allowing a later recurrence to be recognized.

### 3.3 Classify manifestation and root cause separately

**Decision:** “What failed?” and “why it likely failed” are different fields.

A learner may omit a required Writing content point. The manifestation is an incomplete response; the root cause may be task misunderstanding, an exam-strategy checking failure, time pressure, or an unresolved cause. Conversely, one grammar gap may manifest as a cloze error, unclear Writing, and a Speaking repair.

This two-axis model prevents broad labels such as “production error” from hiding a confirmed vocabulary or grammar cause, while still allowing a useful broad classification when finer attribution is not responsible.

### 3.4 Prefer one defensible cause over many speculative tags

**Decision:** A mistake episode has at most one primary root cause and, when genuinely useful, one contributing cause. Diagnosis may remain unresolved.

Shotgun-tagging every plausible grammar, vocabulary, topic, and strategy node would create false recurrence and noisy coaching. Bestehen should store a broader pattern with lower confidence rather than invent precision. Only medium- or high-confidence causes can promote a fine-grained known weakness.

### 3.5 Promote repeated independent evidence, not repeated clicks

**Decision:** A pattern normally becomes a known weakness after at least two independent failure episodes across fresh tasks on different sessions or days, plus adequate opportunities and diagnosis confidence. Same-item retries, several errors in one response, and repeated clicks inside one repair loop remain one episode.

One realistic failure can be an urgent provisional blocker, especially in a mock, but it does not by itself create a permanent fine-grained weakness. A fresh confirmation is still required.

### 3.6 Repair requires transfer and retention

**Decision:** Seeing an explanation or passing an immediate retry does not repair a weakness. Repair is earned through successful unassisted use on fresh equivalent tasks, separated across occasions and time, at a difficulty and modality appropriate to the original claim.

This protects the product thesis: Bestehen practices transfer, not answer memorization.

### 3.7 Cross-skill effects change what to test, not what to assume

**Decision:** A confirmed underlying grammar, vocabulary, or strategy node may influence practice in another skill, but negative mastery is applied only to the modality actually observed.

A Reading grammar error may cause the coach to add a short Writing verification task. It does not lower Writing mastery before the learner writes. A shared cross-modal weakness is confirmed only after direct failures occur in more than one modality.

### 3.8 Time lowers urgency, not historical truth

**Decision:** Time never repairs a weakness. Old events remain part of history. Without new opportunities, active priority may soften and current status becomes stale or unverified, but the learner is not declared repaired merely because the issue has not appeared recently.

Successful evidence is what lowers weakness priority. Time determines when that success must be checked again.

## 4. Detailed Product Model / Rules for This Stage

### 4.1 Core terms

| Term | Product definition |
|---|---|
| Relevant opportunity | A valid task moment where the learner could reasonably demonstrate the node/capability; an unrelated task does not count as success or failure |
| Independent episode | A fresh task or response in a distinct attempt context, not a same-item retry or another click in the same repair chain |
| Fresh equivalent task | New content that tests the same underlying capability without exposing or repeating the original answer |
| Cause confidence | How strongly the evidence supports the diagnosed root cause: unresolved, low, medium, or high |
| Recent window | The last 60 days for initial recurrence and opportunity calculations; retained lifetime history remains available |
| Working condition | Current reachable difficulty and allowed support used for learning |
| Target condition | Relevant B1 difficulty with the assistance, replay, and timing constraints required by the claim |
| Repair responsiveness | Improvement immediately after an explanation or model; useful but weak evidence for independent mastery |
| Delayed transfer | A later fresh task that tests the same capability without answer exposure |
| Known weakness | A confirmed current coaching pattern that passed the promotion gates below |
| Resolved weakness | A formerly known weakness with sufficient repair and later retention evidence; the history is retained |

The 60-day recurrence window and later intervals in this document are implementable starting defaults, not scientific constants. Stage 14 and Stage 26 may recalibrate them while preserving the behavior.

### 4.2 What counts as a mistake event

A mistake event is created when all of the following are true:

1. a valid learner response, omission, or observable task behavior exists;
2. the outcome falls short of the expected answer, B1-sufficient rubric dimension, or intended strategy behavior;
3. the shortfall is supported by the task design, answer key, rubric, or trustworthy evaluation;
4. it can be linked to at least a broad skill/task pattern and modality;
5. it is not explained solely by a technical, content, or evaluator failure.

Qualifying outcomes include:

- incorrect or partially correct objective responses;
- omitted required content;
- incomplete work under a stated time condition;
- a Writing or Speaking rubric dimension below the expected working/target level;
- observable misuse of an allowed strategy;
- a failed fresh transfer check;
- a no-meaningful-response event after the learner understood the task and had a fair opportunity.

The following do **not** become learner mistake events:

- corrupt or ambiguous content;
- broken audio, input failure, inaudible recording, or interrupted session;
- a skipped optional task without evidence of inability;
- a dimension the evaluator cannot judge;
- an answer that is different but still valid;
- harmless language variation that remains B1-sufficient;
- an error introduced only by transcription or automated correction;
- self-reported weakness without observed performance.

A technically invalid attempt remains in operational history if needed, but it has zero capability and weakness effect.

### 4.3 Mistake manifestation types

Manifestation describes the observable shortfall before root-cause interpretation.

| Manifestation | Meaning | Examples |
|---|---|---|
| Incorrect selection or response | A scored answer is wrong | Wrong matching choice; incorrect cloze option |
| Partial response | Some required meaning or elements are present, but not enough | Covers two of three Writing content points |
| Omission / blank | A required answer or content element is missing | Leaves an item blank; omits a greeting where required |
| Misread or misheard detail | The response contradicts an explicit detail | Misses “nicht”; confuses 15:00 and 17:00 |
| Inference failure | Literal information is known but the conclusion is wrong | Misidentifies a speaker's intention |
| Production form/use error | The learner-produced language is incorrect or inappropriate | Wrong word order; unsuitable collocation |
| Communicative shortfall | Language is present but task success is weakened | Unclear request; response does not address partner |
| Interaction shortfall | The learner does not sustain or respond to the exchange as required | Ignores a proposed alternative |
| Execution/strategy lapse | Observable task behavior loses avoidable points | Fails to check content points; spends too long on one item |
| Timed incompletion | Capability is not fully demonstrated within the applicable time | Message unfinished in exam-timed mode |
| Transfer failure | The same underlying issue returns in a fresh verification task | Repeats the repaired word-order error two days later |

One attempt may contain multiple manifestations, especially productive work, but events with the same root pattern in that attempt are grouped into one episode for recurrence. Frequency within the response is still useful severity evidence.

### 4.4 Root-cause taxonomy

The required Stage 05 categories are the top-level product taxonomy. Subtypes help repair selection but are used only when supported.

| Root cause | Product meaning | Useful subtypes / diagnosis cues | Example repair direction |
|---|---|---|---|
| **Vocabulary gap** | The learner lacks or cannot access needed meaning/form | text recognition; sound recognition; recall; synonym/paraphrase; collocation; functional phrase | Contrast meaning in context, then test in a fresh receptive or productive use |
| **Grammar gap** | A grammatical relationship is not recognized, selected, or produced reliably | form recognition; meaning/function; contextual choice; construction; spontaneous control | One practical rule/example, controlled use, then fresh use in the observed lane |
| **Listening-recognition failure** | The learner knows or can understand the language in another form but fails to decode it from speech | sound segmentation; reductions/connected speech; speed; number/date discrimination; speaker change/correction | Short contrastive audio, then new audio under gradually realistic playback |
| **Misunderstanding / comprehension gap** | The learner encounters the words/forms but builds the wrong meaning or task interpretation | instruction misunderstanding; detail relation; negation/restriction; inference; intention; reference | Reconstruct the meaning, identify the decisive cue, then fresh comprehension task |
| **Exam-strategy error** | An observable solving or checking behavior causes avoidable lost points | instruction/format; scanning; elimination; time allocation; unknown-word handling; required-point checking; preparation-time use | Teach one concrete behavior and verify it in the same task family |
| **Attention / careless error** | The learner appears to possess the capability but makes an execution slip | mis-click; overlooked sign/qualifier; copied wrong choice; avoidable omission | Neutral “attention slip” language, short checking cue, monitor before labeling a pattern |
| **Production error** | Writing or Speaking falls short, but a more specific grammar/vocabulary cause is not yet defensible or the issue is genuinely production-level | clarity; organization; register; fluency; intelligibility; interaction; repair behavior | Target the affected rubric dimension and collect another productive sample |
| **Timing / execution pressure** | Performance is adequate untimed but deteriorates under the stated time or sequencing condition | pace; incomplete response; fatigue; recovery; one-play attention | Pacing or sequencing practice; do not reteach language automatically |
| **Unresolved / mixed** | Evidence supports the shortfall but not a responsible cause | conflicting signals; multiple plausible causes; evaluator limitation | Collect the smallest clarifying task rather than assigning broad repair |
| **Non-learner invalidation** | The result is caused by content, technical, or evaluation failure | broken audio; ambiguous key; bad transcription; unsupported rubric | Exclude from weakness memory and fix/retry the task |

### Category guardrails

- **Vocabulary versus listening recognition:** If the learner understands the word in a transcript but not in audio, prefer Listening recognition. If meaning remains unknown after seeing the word, prefer Vocabulary. If the distinction is unclear, keep it unresolved.
- **Grammar versus production:** Use Grammar when a specific structure is supported by repeated form/use evidence. Use Production when the observable writing/speaking shortfall is clear but the underlying language cause is not.
- **Misunderstanding versus strategy:** Use Misunderstanding when meaning or instructions were interpreted incorrectly. Use Strategy when the learner understood but failed to apply an observable solving/checking behavior.
- **Attention/careless:** This is not a personality label and should be used sparingly. Prefer “attention slip” in learner-facing copy. One quick self-correction can support this cause, but repeated slips should normally become a specific strategy pattern such as “check restrictions before answering.”
- **Timing:** Timed failure does not automatically lower the language node. Update timing/strategy, language, or both only when evidence supports each attribution.
- **Topic familiarity:** Topic is context, not a root cause by itself. A health-task error becomes a health-domain weakness only after repeated directly diagnosed lexical/context evidence.

### 4.5 Diagnosis confidence

Each cause is stored as:

| Confidence | Meaning | Effect |
|---|---|---|
| Unresolved | No responsible cause selected | Keep broad task evidence; prioritize clarification if important |
| Low | Plausible hypothesis from weak or indirect evidence | May influence the next diagnostic task; cannot promote a fine known weakness |
| Medium | Direct response pattern, targeted probe, or trustworthy rubric supports the cause | Eligible for recurrence and known-weakness promotion |
| High | Deterministic diagnostic contrast, repeated clear manifestation, or strong validated evaluation isolates the cause | Full eligible evidence, still subject to independence rules |

Rules:

- Learner self-explanation can raise or lower a hypothesis but is not sufficient alone.
- Objective answer keys establish outcome correctness, not automatically the root cause.
- Writing/Speaking evaluation contributes only to dimensions the evaluator supports.
- Low-confidence causes may be aggregated only at a broader task/rubric level.
- A cause can be corrected later without deleting the original event; derived weakness states are recalculated from the corrected attribution.
- Premium AI is not called merely to turn every unresolved event into a label.

### 4.6 Episode grouping and opportunity counting

Recurrence uses independent episodes and relevant opportunities.

### Same episode

The following normally remain one episode:

- multiple wrong clicks on the same item;
- the original attempt, explanation, controlled repair, and immediate retry;
- several occurrences of the same grammar error within one Writing response;
- multiple rubric notes from one evaluator that point to one underlying pattern;
- restarting the same content after answer exposure.

Within-episode frequency can increase severity or diagnosis confidence, but it does not pretend to show retention across time.

### New independent episode

A new episode normally requires:

- a fresh task or prompt;
- no exposure to the answer for that task;
- a new attempt context, normally another session/day for known-weakness promotion;
- suitable opportunity to demonstrate the same node/behavior;
- valid content and evaluation.

A fresh equivalent retry later in the same session is stronger than a same-item retry, but for promotion to a known weakness, evidence across different sessions or days is still required.

### Opportunity denominator

The model records relevant opportunities so recurrence is not based only on failure counts:

- two failures in three relevant opportunities is stronger weakness evidence than two failures in twenty;
- an item counts as an opportunity only when the node was genuinely required or directly tested;
- one event tagged to many nodes does not create an opportunity for every speculative tag;
- skipped/invalid tasks do not count;
- assisted opportunities are retained separately from unassisted ones.

### 4.7 Mistake lifecycle

~~~mermaid
stateDiagram-v2
    [*] --> Candidate: valid event
    Candidate --> Historical: not confirmed
    Candidate --> Known: promotion gates met
    Known --> Repairing: targeted repair starts
    Repairing --> Stabilizing: delayed transfer succeeds
    Stabilizing --> Repaired: repair criteria met
    Repaired --> Resolved: later retention holds
    Stabilizing --> Known: recurrence
    Repaired --> Known: confirmed recurrence
    Resolved --> Known: confirmed recurrence
~~~

### Lifecycle states

| State | Meaning | Coaching behavior |
|---|---|---|
| Candidate | One event or low-volume plausible pattern | Monitor or collect a clarifying opportunity; avoid “you keep…” language |
| Historical / unconfirmed | Candidate did not recur or became stale without enough confirmation | Retain for future pattern matching; no dedicated drill |
| Known weakness | Promotion gates met | Include in coaching priority and explain the observed pattern |
| Repairing | A targeted intervention is active | Use the smallest repair and a fresh equivalent retry |
| Stabilizing | At least one delayed transfer succeeded, but retention is not yet proven | Reduce intensity and continue spaced checks |
| Repaired | Transfer criteria met | Remove dedicated daily repair; keep low-priority monitoring |
| Resolved | Later retention check succeeds with no recurrence | Retain as history; surface only as earned progress or if it reopens |
| Reopened | A known/repaired pattern recurs with supported evidence | Return to Known with priority based on current realism, recurrence, and exam impact |

“Resolved” does not mean deleted or impossible to recur. It means no current dedicated coaching is justified.

### 4.8 When a mistake becomes a known weakness

A fine-grained pattern becomes a known weakness when all required gates are met.

### Required default gates

1. **Same defensible pattern:** Episodes map to the same canonical node/cause and observed lane, or to a clearly shared root with explicit modality manifestations.
2. **Independent recurrence:** At least **two independent failure episodes** on fresh tasks across **two sessions or days**.
3. **Recent enough:** Those episodes occur within the initial **60-day recent window**.
4. **Enough opportunity:** At least **three relevant opportunities** exist, and failure appears in at least **40% of the last five comparable opportunities** or two of the last three.
5. **Cause confidence:** At least medium cause confidence overall; unresolved or low-confidence events cannot create a fine known weakness.
6. **Directness:** At least one failure is direct evidence in the claimed lane and condition. A productive weakness requires productive evidence; a Listening weakness requires audio evidence.
7. **Validity:** Technical/content/evaluator quality is adequate and the result is not explained solely by inaccessible task conditions.

These thresholds are the default, not learner-facing statistics. They deliberately favor a small delay over falsely labeling a learner after one event.

### Important exceptions and boundaries

- **One target-condition or mock failure:** Creates a high-priority candidate or provisional performance blocker, not normally a known fine weakness. A fresh confirmation is requested soon.
- **One productive response with the same error many times:** Counts as one episode. Frequency strengthens severity/cause confidence but not independence.
- **Broad rubric weakness:** A strongly evaluated Writing or Speaking dimension may be treated as a provisional section blocker after one sample, but it becomes a known weakness only after another independent productive sample.
- **Support-dependent claim:** A pattern may become known as “support-dependent” using assisted/unassisted contrast. It must not be worded as an unqualified inability.
- **Persistent target-condition weakness:** Requires the normal known-weakness gate plus recurrence in recent unassisted or timed B1-relevant evidence.
- **Previously resolved weakness:** One new medium/high-confidence independent failure can reopen it because the historical pattern is already confirmed. A low-confidence anomaly first creates a recheck.

### Candidate dismissal

An isolated candidate moves to Historical / unconfirmed when either:

- two fresh comparable opportunities on different occasions succeed without recurrence; or
- it ages beyond 60 days without another relevant opportunity, in which case it becomes stale/unverified rather than “repaired.”

### 4.9 Priority model

Priority answers: **How strongly should this weakness influence upcoming coaching?** It is separate from mastery and separate from whether the learner is a good or bad student.

### Priority inputs

| Input | Raises priority when… | Guardrail |
|---|---|---|
| TELC/exam impact | The pattern affects frequent tasks, required rubric dimensions, or written/oral pass risk | Corpus relevance cannot create a weakness without learner evidence |
| Recurrence and rate | Failures repeat across independent recent opportunities | Count opportunities, not only failures |
| Evidence realism | Failure appears unassisted, timed, replay-constrained, or in a mock | Do not ignore stable contrary evidence; lower confidence if contradictory |
| Breadth | The same root manifests across topics, task forms, or modalities | Cross-modal priority does not lower unobserved mastery |
| Current readiness bottleneck | Improvement would protect meaningful pass-relevant points | Exact readiness contribution belongs to Stage 15 |
| Repair resistance | The issue returns after explanation, retry, or delayed transfer | One failed same-item retry is not independent recurrence |
| Evidence freshness | The weakness is recent or due for a retention check | Time alone does not prove worsening |
| Exam-date urgency | The fixed date makes the opportunity cost of delay higher | Date changes priority, never capability or readiness |
| Reachability | A short repair can unlock points at the learner's current level | Do not spend whole sessions on an unreachable target merely because it is weak |
| Diagnosis confidence | The cause is reliable enough to choose a repair | Uncertain high-impact cases receive diagnosis priority, not speculative drills |

### Learner-facing priority bands

| Band | Default use |
|---|---|
| Observe | Isolated, unclear, or stale candidate; wait for/collect one clarifying opportunity |
| Monitor | Repaired/resolved item due for retention, or a low-impact known weakness |
| Active | Confirmed recent weakness that should influence normal sessions |
| High | Recurring, high-TELC-relevance, cross-task, target-condition, or repair-resistant weakness |
| Pass-critical | Persistent realistic blocker materially threatening a written or oral pass component, especially near a booked date |

Initial band rules:

- A newly promoted known weakness normally starts at **Active**.
- Raise one band for coherent recurrence after repair, strong target-condition evidence, or verified cross-task/cross-topic breadth.
- Raise to **Pass-critical** only when later readiness/section evidence shows genuine written/oral pass risk; the label is not created from frequency alone.
- Lower one band after a successful delayed transfer and again when full repair criteria are met.
- Unresolved causes use **Observe** even when the task outcome is important; the next action is a clarifier.
- A booked exam can raise scheduling urgency by one band, but it cannot turn an unconfirmed candidate into a known weakness.
- The daily coach may cap how much one weakness consumes and must retain section coverage. Stage 06 owns that balance.

Tie-breakers for limited session time are:

1. separate written/oral pass risk;
2. expected recoverable exam points;
3. due spaced verification;
4. shortest reachable repair that produces useful transfer evidence;
5. breadth/coverage needs.

### 4.10 Recurrence, decay, and reopening

### Recurrence

Mistake Memory retains both:

- **lifetime history**, used for progress and fast recognition of returning patterns;
- **recent recurrence**, initially calculated over 60 days and used for current priority.

Stage 04's descriptive recurrence bands remain:

- Isolated — one independent episode;
- Repeated — two independent episodes;
- Recurring — at least three independent episodes across at least two sessions/days;
- Persistent under target conditions — recurring in recent unassisted/timed B1-relevant evidence.

Opportunity rate accompanies these labels. “Three failures” is never shown without enough context to know how often the learner had a relevant chance.

### Time decay

- Events never decay out of history.
- Failure influence on current priority softens after 30 days without recurrence, but only when there has been at least some successful or neutral relevant evidence.
- At 61–120 days without a relevant opportunity, the state becomes stale/unverified. It does not become repaired.
- Over 120 days, a resolved or unrechecked weakness is historical-only for current coaching and should receive one concise recheck when naturally relevant.
- Stable repaired evidence lowers priority more strongly than mere silence.
- Recent realistic recurrence can dominate old assisted success, but one anomaly first lowers confidence and requests clarification.

### Reopening

- A medium/high-confidence recurrence of a previously known/repaired weakness reopens it immediately.
- Priority is based on current evidence, not automatically restored to its historical maximum.
- If the recurrence occurs under target conditions or after multiple successful repairs, repair resistance raises priority.
- If the new event is low-confidence or technically questionable, schedule a recheck instead of reopening.

### 4.11 Repair and resolution behavior

### Repair sequence

1. **Name the pattern responsibly:** confirmed, possible, or unresolved.
2. **Select the smallest repair:** one concept, distinction, phrase pattern, or strategy behavior.
3. **Explain practically:** why the answer lost points and what cue/action changes the outcome.
4. **Use controlled practice only as needed:** enough to make the pattern usable, not a generic lesson.
5. **Fresh equivalent retry:** new content in the observed lane.
6. **Record immediate response:** unresolved, still failing, or responsive to repair.
7. **Schedule delayed transfer:** test without solution exposure.
8. **Broaden only when justified:** new topic, task form, condition, or modality.
9. **Reduce priority after evidence:** never after explanation alone.

### State criteria

| State change | Initial evidence requirement |
|---|---|
| Candidate → Known | Promotion gates in Section 4.8 |
| Known → Repairing | Learner begins a targeted repair or the coach assigns one |
| Repairing → Stabilizing | At least one successful delayed fresh-transfer opportunity, normally 1–3 days later, with no answer-bearing support |
| Stabilizing → Repaired | At least three successful fresh relevant opportunities across at least three occasions spanning at least 14 days; majority unassisted; no recurrence after the last repair; one success in the original observed lane and at an appropriate working difficulty |
| High/pass-critical target weakness → Repaired | All normal criteria plus at least one recent success under the relevant B1/target condition |
| Repaired → Resolved | A later retention opportunity, normally around 30–60 days or a natural equivalent encounter, succeeds without recurrence |
| Repaired/Resolved → Known | Supported recurrence as defined above |

Additional rules:

- Productive weaknesses require productive repair evidence. A recognition quiz cannot repair a Writing or Speaking weakness by itself.
- A shared cross-modal weakness is not resolved until each modality currently claimed as weak has direct successful evidence.
- If opportunities are rare, natural exam-shaped encounters may replace dedicated micro-drills, but the evidence requirement remains.
- Failure during stabilization returns the weakness to Known and normally schedules a shorter interval.
- A repaired weakness may still have only Functional or Reliable mastery. “Repaired” means the recurring blocker no longer justifies dedicated repair; it does not automatically mean Target-evidenced.

### 4.12 Spaced return of old mistakes

Mistake Memory owns the minimum return pattern; Stage 14 will integrate and tune it across all review material.

### Initial default return sequence

- **Same session:** fresh equivalent retry after repair; measures responsiveness.
- **1–3 days:** first delayed transfer.
- **About 7 days:** short retention check.
- **About 21 days:** broader transfer or natural task embedding.
- **About 60 days:** resolved/stability check, preferably under a more realistic or productive condition when relevant.

Rules:

- Do not repeat the original answer unless the product is explicitly teaching recognition; use fresh content.
- Use natural embedding inside Reading, Listening, Language Elements, Writing, or Speaking whenever it supplies a valid opportunity. Do not create a separate flashcard product.
- Productive use is preferred when the weakness claim is productive.
- Successful spontaneous use in normal practice can satisfy a due check; do not add redundant review.
- A failed check raises priority and returns the interval to 1–3 days after repair.
- Low-impact repaired items can wait for natural encounters; high/pass-critical items receive explicit scheduled checks.
- If the learner is inactive, do not create a punitive backlog. On return, select a small number of highest-value stale checks.
- Exact intervals later adapt by exam importance, difficulty, stability, exam date, and opportunity frequency.

### 4.13 Cross-skill and cross-modality transfer

A mistake pattern may have:

- an underlying shared node, such as word order after a subordinate conjunction;
- one or more **observed manifestations**, such as Reading recognition or Writing production;
- one or more **verification targets**, such as “test this in Writing next”;
- modality-specific mastery and repair status.

### Transfer rules

1. Apply direct negative evidence only to the observed lane.
2. Use Corpus relationships to identify plausible receptive/productive counterparts and task patterns.
3. A shared node can raise the value of a verification task in another modality; it cannot create failure evidence there.
4. Promote a cross-modal known weakness only after direct supported failure in each modality being claimed.
5. Success in one lane can lower uncertainty about the concept but cannot resolve another lane without direct evidence.
6. When production shows a specific grammar/vocabulary error, a receptive repair may be used as scaffolding, but final repair proof must return to production.
7. Transfer is more valuable when the node is frequent/TELC-relevant and when the receiving modality lacks evidence; low-relevance cross-skill drills should not displace higher-value work.
8. Exam strategies transfer only to closely related task behavior until evidence supports broader use.

### Examples

| Observed mistake | Direct update | Cross-skill influence | What must not happen |
|---|---|---|---|
| Misses word order after “weil” in a Language Elements item | Grammar contextual-choice candidate | Add a short Writing construction check if Writing evidence is weak | Do not lower Writing or Speaking mastery |
| Repeats “weil” word order error in two Writing samples | Known Writing-production grammar weakness | Use a brief recognition explanation, then test a new message and later Speaking if relevant | Do not mark repaired after a cloze success |
| Understands “fünfzehn” in transcript but repeatedly misses it in audio | Listening sound-recognition weakness | Pair written form with contrastive audio; later test in a Listening detail task | Do not call it a general vocabulary-meaning gap |
| Omits a required Writing content point | Writing task-fulfillment/strategy event | Add a content-point checklist behavior that may later be tested in another productive task | Do not teach unrelated grammar |
| Misses “nur werktags” in Reading twice | Reading restriction/comprehension or scanning weakness | Test the same restriction cue in Listening only as a new verification opportunity | Do not infer a Listening weakness |
| Fails to respond to a partner's alternative in Speaking | Interactive-speaking production/strategy weakness | Practice response phrases, then use a fresh interactive exchange | A monologue cannot resolve interaction |

### 4.14 Learner-facing recurring-weakness explanations

A recurring-weakness explanation answers five questions:

1. **What is the pattern?**
2. **Where was it observed?**
3. **How certain are we?**
4. **Why does it matter for TELC B1?**
5. **What will the coach do next?**

### Copy rules

- Use capability language, not identity labels: “This pattern is recurring,” not “You are careless.”
- Say “possible pattern” when confidence is low.
- Mention recurrence only when independent recurrence exists.
- Use simple practical language before grammar terminology.
- Name the observed modality and condition.
- Explain why the weakness matters without catastrophizing.
- Limit the default view to one or two highest-value weaknesses.
- Show earned progress when a weakness moves to monitoring/repaired.
- Never claim that a repaired weakness guarantees exam performance.
- Do not reveal pseudo-precise probabilities for root causes.

### Explanation templates

**Candidate**

> Possible pattern: you missed a time restriction in this Reading task. One result is not enough to call it a weakness, so I’ll check it once more in a fresh task.

**Known weakness**

> Restrictions such as “nur” and “außer” are recurring in your Reading. They caused two misses in three fresh tasks over the last two weeks. These cues often decide the correct exam answer, so we’ll practice spotting them and check the skill again later.

**Cross-skill verification**

> You recognized the rule after the explanation, but we have not seen you use it in Writing yet. A short message task will check whether it transfers; your Writing level has not been lowered.

**Uncertain cause**

> The answer was wrong, but it is not clear whether the blocker was the word, the audio, or the task instruction. I’ll use one short comparison before choosing a repair.

**After immediate retry**

> You solved a fresh example after the explanation. That shows the repair helped. It returns in two days to check whether it stayed.

**Repaired**

> You handled this pattern correctly in three fresh tasks across two weeks, including one unassisted Writing task. It is now in monitoring rather than daily repair.

**Reopened**

> This pattern returned in a timed task. Your earlier progress still counts, but it needs a short refresh before the next realistic check.

### Category examples

| Root cause | Learner-facing phrasing |
|---|---|
| Vocabulary | “The word is not available reliably in this context yet.” |
| Grammar | “The verb moves to the end after ‘weil’; this is recurring in your messages.” |
| Listening recognition | “You know the number in writing, but it is not reliable in audio yet.” |
| Misunderstanding | “You found the sentence, but the restriction changed its meaning.” |
| Strategy | “You understood the text, but did not check every required content point.” |
| Attention | “This looks like an attention slip, not a knowledge gap. I’ll monitor it before adding practice.” |
| Production | “Your message is understandable, but the request itself is still unclear.” |
| Timing | “You can complete the task untimed; the current blocker is finishing it within exam time.” |

### 4.15 Necessary data versus overkill

Bestehen is a personal project. Mistake Memory should store enough structured evidence to drive coaching and explain decisions, but not build a research-grade telemetry system.

### Necessary first-product data

| Data | Why it is necessary |
|---|---|
| Event/episode identity and date/session | Separates independent recurrence from one repair chain |
| Attempt context | Distinguishes diagnostic, practice, immediate retry, delayed transfer, review, and mock evidence |
| Section, task pattern, modality/lane, and canonical skill node | Connects the event to coaching and the Corpus graph |
| Task/content version and freshness relationship | Prevents repeated-item memorization from looking independent |
| Difficulty and TELC relevance | Interprets severity and target usefulness |
| Manifestation and outcome/rubric dimension | States what failed |
| Primary root cause, optional one contributor, and cause confidence | Chooses repair without shotgun tagging |
| Assistance, timing, replay/reference/model exposure | Separates learning conditions from target conditions |
| Technical/content/evaluator validity and confidence | Prevents invalid results from becoming learner weakness |
| Relevant opportunity and independent episode grouping | Supports opportunity-adjusted recurrence |
| Repair offered/completed, retry result, and delayed-transfer result | Drives lifecycle and proves repair |
| Derived state, priority band, last recurrence, and next due check | Makes future coaching actionable |
| Short learner-facing explanation reason | Makes memory explainable without regenerating prose |

Raw learner work may be retained according to Stage 24, but Mistake Memory only requires a durable reference or structured evaluation. Permanent raw audio is not required to maintain the weakness state.

### Useful later, but not required initially

- calibrated probability distribution over several causes;
- richer confusion-pair analytics;
- human-review annotations;
- cross-learner normative rates;
- model-version comparison and evaluator disagreement;
- detailed time-on-substep telemetry;
- automatic discovery of new skill nodes from learner errors.

These are upgrade paths only if they materially improve repair quality or readiness calibration.

### Explicit overkill for the personal-project phase

Do not require:

- eye tracking, cursor trails, or full keystroke logging;
- recording every hesitation, pause, backspace, or mouse movement;
- storing hidden chain-of-thought or asking learners for exhaustive reasoning;
- a root-cause probability vector for every wrong answer;
- permanent raw audio solely to keep mistake memory;
- tagging every wrong response to every vocabulary/grammar node mentioned by the item;
- a unique decay curve for every node;
- premium-model classification for routine objective errors;
- real-time generative explanations for common known patterns;
- exhaustive cross-skill testing after every event.

The first model should optimize for trustworthy coaching decisions, not maximum data collection.

### 4.16 Worked examples

### Example A — Reading restriction becomes a known weakness

1. The learner chooses the wrong notice because “nur werktags” was overlooked.
2. Outcome is wrong; cause is medium-confidence misunderstanding/restriction scanning. Status: Candidate.
3. The same-session retry succeeds. Status remains Candidate; repair responsiveness is recorded.
4. Ten days later, a fresh Reading task with “außer sonntags” is missed.
5. The pattern now has two independent episodes across two days, three relevant opportunities, and two failures. It becomes a Known Reading restriction/comprehension weakness at Active priority.
6. The coach teaches one cue/checking behavior and uses a fresh retry.
7. Delayed checks at two days, one week, and three weeks succeed.
8. After three fresh occasions spanning two weeks, it becomes Repaired.
9. A later natural Reading task at about 60 days succeeds; it becomes Resolved.

### Example B — Grammar error influences Writing without inventing Writing weakness

1. A Language Elements task reveals incorrect word order after “weil.”
2. The cause is high-confidence Grammar contextual choice. One event creates a Candidate in the controlled/recognition lane.
3. Because the node is TELC-relevant and Writing evidence is sparse, the coach adds one short Writing verification.
4. The learner writes the structure correctly without help.
5. Writing mastery receives positive direct evidence. No Writing weakness was ever created.
6. Another cloze failure later may confirm a controlled-choice weakness, but it still does not lower Writing unless Writing itself fails.

### Example C — Listening recognition rather than vocabulary

1. The learner misses “fünfzehn Uhr” twice in audio but immediately identifies 15:00 when shown the transcript.
2. Root cause is Listening recognition/number discrimination, not semantic vocabulary.
3. After a second independent audio episode, the pattern becomes Known.
4. Repair uses short contrastive audio such as fünfzehn/fünfzig and a fresh announcement.
5. A written flashcard success does not repair it; later fresh audio success does.

### Example D — Writing omission is strategy, not grammar

1. A timed message is understandable but omits one required content point.
2. Manifestation is Partial response; root cause is medium-confidence Exam strategy: required-point checking.
3. One mock response creates a high-priority provisional blocker, not a known pattern.
4. A second fresh Writing task repeats the omission.
5. It becomes a Known Writing task-fulfillment strategy weakness.
6. Repair uses a short content-point plan/check, followed by a new message. Grammar is not broadly retaught.

### Example E — Attention slip stays small

1. The learner clicks the opposite option, immediately notices without explanation, and has otherwise reliable evidence for the concept.
2. Record an Attention slip Candidate with low/medium confidence.
3. Do not schedule a lesson and do not say “you are careless.”
4. If it does not recur in two fresh opportunities, move it to Historical / unconfirmed.
5. If similar restriction misses recur, reclassify the pattern into a specific checking/strategy weakness rather than a personal trait.

### Example F — Speaking interaction weakness

1. In a planning exchange, the learner gives a monologue but does not respond to the partner's alternative.
2. The evaluator supports an Interaction shortfall; language is otherwise comprehensible.
3. The root cause remains Production/interaction or Strategy at medium confidence.
4. A second fresh interactive task shows the same behavior, promoting a Known interactive-speaking weakness.
5. Phrase rehearsal and a monologue success are scaffolding only. Repair requires successful response behavior in fresh interaction.

## 5. Edge Cases / Failure or Uncertainty Handling

| Situation | Mistake-memory behavior | Coaching consequence |
|---|---|---|
| Wrong answer, cause unclear | Keep broad task event as unresolved | Use one small clarifier; avoid speculative repair |
| Several errors in one Writing sample | Group same root into one episode; retain within-response frequency | Severity may rise, recurrence does not |
| Same item failed repeatedly | One episode/opportunity | Do not inflate priority |
| Immediate retry succeeds | Record responsiveness at weak strength | Schedule delayed transfer |
| One failed mock contradicts stable history | Create strong candidate, lower confidence, compare conditions | Clarify before declaring regression unless prior weakness reopens |
| Repeated realistic failure | Confirm/reopen and raise priority | Target pass-relevant repair and reassess later |
| Learner lacks prerequisite knowledge | Map the narrow prerequisite when supported | Step down difficulty; do not repeat impossible target tasks |
| Learner requests help before answering | Record assisted context | Valid learning evidence, weaker independent weakness/readiness claim |
| Learner corrects an apparent mis-click | Candidate attention slip | Monitor, do not drill |
| Evaluator disagrees with deterministic rule or another evaluator | Lower cause confidence and preserve both provenance records | Do not promote until resolved |
| Task/tag confidence is low | Keep broader section/task evidence | Avoid fine node recurrence |
| Technical audio/recording failure | Non-learner invalidation | Retry without penalty |
| Learner returns after months | Retain history; mark current status stale/historical | Recheck a few high-value patterns, never create a backlog |
| No new opportunity for a rare skill | Do not claim repair or worsening | Embed one opportunity when relevant |
| Cross-modal relation exists but receiving modality is unknown | Add verification target only | Do not change receiving mastery |
| Repair content repeats the original answer | Count as weak same-episode evidence | Require fresh equivalent content later |
| Error is B1-acceptable and meaning is preserved | May be feedback, but not a priority mistake unless rubric impact exists | Avoid perfectionist repair |
| Learner disputes a diagnosis | Show the concrete evidence and allow another fresh check | Lower confidence if the alternative is plausible; do not argue from authority |

### Contradictory cause evidence

If the same surface error has different plausible causes across episodes, do not merge them solely because the answer looks similar. A missed Listening number caused by unknown vocabulary and another caused by audio discrimination may share practice content but remain different root patterns until evidence supports a shared weakness.

### Too many active weaknesses

The App may remember many patterns, but the learner-facing plan should normally surface at most one or two active priorities. Lower-value weaknesses remain scheduled/monitored. Stage 06 decides session balance; Stage 05 requires that priority and due state make this selection explainable.

### Overcorrection risk

Writing and Speaking can contain many surface errors. Mistake Memory should prioritize B1 communicative sufficiency, required content, interaction, and recurring high-impact patterns. It must not turn every non-native form into a durable weakness or overwhelm the learner with corrections.

## 6. Relationship to Other Bestehen Stages

- **Stage 03 — Initial Diagnostic:** supplies candidate mistake signals; Stage 05 prevents one diagnostic error from becoming a permanent weakness.
- **Stage 04 — Learner Model:** supplies the evidence ledger, skill/lane separation, confidence, evidence strength, recurrence episodes, freshness, and Corpus overlay that Mistake Memory derives from.
- **Stage 06 — Daily Coaching Engine:** consumes priority band, due checks, readiness impact, reachability, and unresolved diagnosis needs while balancing broader coverage and fatigue.
- **Stage 07 — Core Learning Loop:** implements the attempt, diagnosis, repair, fresh retry, and remember experience and records episode links.
- **Stage 08 — A1→B1 Progression:** determines accessible repair difficulty and when support can be removed.
- **Stages 09–13 — Skill Coaching:** finalize manifestation/rubric details, root-cause diagnostics, repair formats, and valid opportunities for each exam area.
- **Stage 14 — Review and Spaced Repetition:** integrates the 1–3/7/21/60-day default into a complete scheduler and quick-review formats.
- **Stage 15 — TELC Readiness:** decides how active/pass-critical weaknesses and realistic evidence affect written/oral readiness without double-counting the same event.
- **Stage 16 — Mock Exams:** creates high-strength realistic mistake candidates and post-mock repair plans; one mock still does not automatically label every fine weakness.
- **Stage 17 — Ready to Book:** uses unresolved pass-critical weaknesses and fresh repair evidence as part of eligibility.
- **Stage 18 — Coach Personality:** refines exact weakness, uncertainty, repair, regression, and progress language while preserving the templates and guardrails here.
- **Stage 19 — Information Architecture:** decides where recurring weaknesses, history, explanations, and due checks appear.
- **Stage 20 — Progress and Motivation:** may celebrate a weakness moving to Repaired/Resolved as earned capability, not game currency.
- **Stage 21 — Content Strategy:** supplies fresh equivalent tasks, reviewed tags, diagnostic contrasts, and anti-repetition rules.
- **Stage 22 — Corpus → App Contract:** supplies stable node IDs, relationships, TELC relevance, task mapping, and taxonomy migrations used by weakness families.
- **Stage 24 — Account/Data:** defines raw response/audio retention, export, deletion, privacy, and sync; the minimum structured history remains a product requirement.
- **Stage 25 — Accessibility/Device:** prevents accommodation and technical conditions from being misclassified as learner errors.
- **Stage 26 — Analytics:** validates promotion thresholds, cause accuracy, repair transfer, recurrence windows, priority usefulness, and false-positive weakness rates.
- **Stage 27 — Cost Boundaries:** sets portfolio-wide AI and storage limits.

### Cross-stage guardrails

Later stages may tune intervals and thresholds, but they must preserve:

- outcome separate from cause;
- event/episode/pattern/known-weakness separation;
- independent opportunity-aware recurrence;
- no fine weakness from unresolved evidence;
- direct evidence by modality;
- immediate retry separate from retained transfer;
- time never repairing a weakness by itself;
- repaired history retained and reopenable;
- learner-facing explanations that show evidence, impact, uncertainty, and next action.

## 7. Cost Notes

Mistake Memory should have **negligible recurring cost beyond evaluation already required for the learner's task**.

### Preferred low-cost default

- Objective outcomes are scored deterministically.
- Common objective-task diagnoses use reviewed item metadata and deterministic contrasts.
- Recurrence, opportunities, promotion, priority bands, decay, lifecycle transitions, and due dates use deterministic rules.
- Writing/Speaking evaluation returns structured manifestation, rubric dimension, possible cause, and confidence in the same batched call used for feedback; no second memory-specific call is made.
- Common weakness explanations use reviewed templates populated from structured evidence.
- Corpus relationships and TELC relevance are precomputed and cached.
- Unresolved events remain unresolved until a useful future task supplies evidence.

### When extra evaluation is justified

A higher-quality or second evaluation may be invoked only when all are true:

1. the sample is new and valid;
2. the disputed cause materially affects a mock, written/oral readiness, or ready-to-book decision;
3. cheaper evaluation is below the confidence required for that decision;
4. a fresh clarifying task would be slower or less useful than reevaluation.

Even then, reevaluate once, store the result, and reuse it. Routine candidates, attention slips, and objective errors never justify premium classification.

### Cheaper fallbacks

- Broader unresolved category instead of premium cause inference.
- One deterministic contrast or fresh equivalent task instead of evaluator debate.
- Template explanation instead of generated prose.
- Natural embedding in daily practice instead of dedicated generated review content.
- Reviewed reusable repair patterns instead of per-event content generation.

A more expensive design is justified later only if measured false diagnoses or weak productive repair materially reduce transfer or readiness calibration. The first product should not pay to produce precision that the evidence cannot support.

## 8. Decisions Made

1. Defined a mistake event as a valid, coachable performance shortfall linked to evidence—not merely any wrong click.
2. Separated mistake events, repair-chain episodes, recurring patterns, and known weaknesses.
3. Defined manifestation types and the required root-cause categories: vocabulary, grammar, listening recognition, misunderstanding, exam strategy, attention/careless, and production, plus timing, unresolved, and non-learner invalidation.
4. Limited diagnosis to one primary and at most one contributing cause, with explicit confidence.
5. Defined independent episode and relevant-opportunity counting so retries and repeated items cannot inflate recurrence.
6. Set implementable known-weakness promotion gates: two independent episodes across two sessions/days, adequate recent opportunities/rate, medium cause confidence, and direct modality evidence.
7. Defined candidate, known, repairing, stabilizing, repaired, resolved, historical, and reopened lifecycle behavior.
8. Defined priority bands and inputs covering TELC impact, recurrence, realism, breadth, readiness bottlenecks, repair resistance, freshness, deadline urgency, reachability, and confidence.
9. Defined time decay as reduced current urgency/verification need, never automatic repair or deletion.
10. Defined repair as successful delayed transfer and retention, not explanation or immediate retry.
11. Set an initial fresh-return sequence of same session, 1–3 days, 7 days, 21 days, and about 60 days.
12. Defined cautious cross-skill transfer: shared nodes create verification opportunities without lowering an unobserved modality.
13. Defined learner-facing explanations for candidates, known weaknesses, uncertainty, cross-skill verification, repair, resolution, and reopening.
14. Defined the minimum data required for trustworthy coaching and rejected research-grade telemetry and always-on premium classification.
15. Chose a deterministic, low-cost default with premium reevaluation reserved for genuinely high-impact uncertain productive evidence.

## 9. Open Questions / Deferred Decisions

### Open owner questions

**None.** Stage 05 can be responsibly shaped from the current product context.

### Deferred product decisions

- Exact daily competition between weakness repair, new evidence, section coverage, and learner fatigue — Stage 06.
- Exact repair screen sequence and skip behavior — Stage 07.
- Skill-specific diagnostic probes, valid opportunities, rubrics, and repair activities — Stages 09–13.
- Final adaptive review algorithm and calibrated intervals — Stage 14.
- Exact readiness penalties/guards and pass-critical threshold — Stage 15.
- Mock-specific grouping and post-mock plan — Stage 16.
- Ready-to-book treatment of recently repaired pass-critical weaknesses — Stage 17.
- Exact learner-facing screen placement and amount of history shown — Stages 18–20.
- Final generated/reviewed repair-content policy — Stage 21.
- Raw response/audio retention, deletion, export, and privacy — Stage 24.
- Final threshold calibration and cause-quality monitoring — Stage 26.
- Storage schema, algorithms, model/provider selection, and technical architecture — post-shaping architecture work.

The numerical promotion gates, 60-day recent window, repair criteria, and spaced-return intervals are initial product defaults. They should be tuned using false-positive weakness rates, delayed transfer, mock performance, and eventually real exam outcomes; they are not claims of scientific precision.

## 10. Definition of Done Check

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
- [x] Define mistake lifecycle and reopening behavior.
- [x] Define opportunity-adjusted recurrence and time decay.
- [x] Define necessary data and explicit overkill boundaries for a personal project.
- [x] Define low-cost routine behavior and premium-evaluation triggers.

**Stage 05 is complete when every valid lost point can improve future coaching without one uncertain error becoming a permanent learner label.**
