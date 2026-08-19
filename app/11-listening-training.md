# Bestehen / App — Stage 11: Listening Training

> **Status:** Stage 11 product-shaping decision in progress
>
> **Product:** Bestehen / App
>
> **Launch target:** Zertifikat Deutsch / telc Deutsch B1
>
> **Listening promise:** Train the learner to understand the German TELC B1 actually requires, diagnose the specific reason audio was lost, repair that cause narrowly, and progressively remove playback and language support until performance is credible under target listening conditions.

## 1. Purpose and Scope

This document defines the complete learner-facing **Listening / Hörverstehen** coaching experience for Bestehen / App.

Listening is not treated as a generic library of audio clips followed by comprehension questions. It is a set of exam-relevant task families whose difficulty depends on several separable factors: linguistic load, speech rate and connected speech, information density, numbers and proper names, speaker changes and corrections, distractor design, inference demand, attention continuity, playback rules, and the learner's use of assistance.

Stage 11 applies the common product loop — **Observe → Attempt → Diagnose → Repair → Retry → Remember** — to Listening and makes the Stage 08 A1 → B1 progression concrete for the current TELC B1 listening format.

The product outcome is not merely “the learner got more listening questions right.” It is that Bestehen can explain:

- which listening decision failed;
- whether the failure was vocabulary, sound recognition, speed, numbers/dates/times, negation, distractor handling, inference, attention/execution, or still uncertain;
- which short repair is most likely to recover future points;
- whether the repair transfers to fresh audio;
- how much playback or language assistance was required;
- how strong the resulting evidence is for eventual TELC readiness.

This is product shaping, not implementation architecture. It defines learner behavior, coaching rules, audio/content policy, evidence requirements, uncertainty handling, cost boundaries, and the conceptual contract later stages must preserve. It does not choose a TTS vendor, storage format, CDN, audio codec, model provider, or final readiness coefficient.

### In scope

- current TELC B1 Listening task patterns;
- lower-difficulty P0–P4 variants;
- audio source strategy and rights-aware use;
- generated/TTS versus human/native-recorded policy;
- speech-speed progression;
- replay, transcript, and vocabulary-preview rules;
- listening-specific diagnosis, targeted repair, and fresh retry;
- audio and task difficulty dimensions;
- target-condition listening behavior;
- Listening evidence supplied to the learner model and later readiness stages;
- low-cost operating defaults and higher-quality upgrade paths.

### Out of scope

- final cross-skill review scheduling — Stage 14;
- final TELC readiness coefficients and pass prediction — Stage 15;
- complete mock cadence, scoring, and pause/resume policy — Stage 16;
- ready-to-book gates — Stage 17;
- final screen hierarchy and product copy — Stages 18–19;
- generalized content-generation QA across every skill — Stage 21;
- final Corpus → App technical contract — Stage 22;
- accessibility equivalence for target-condition evidence — Stage 25;
- calibrated thresholds from learner outcome data — Stage 26;
- audio generation, caching, storage, streaming, or model architecture.

---

## 2. Inputs / Existing Decisions

Stage 11 preserves the project overview, identity, and App Stages 01–10:

- Bestehen is a calm, direct, evidence-based **personal German exam coach**.
- TELC B1 is the launch target; a learner may begin around A1.
- German is learned through exam-shaped activity rather than a conventional course sequence.
- Readiness is primary, with written and oral pass risk kept separate.
- Listening is a direct-evidence lane. Reading recognition of a word does not prove sound-to-meaning recognition of that word.
- Mastery, confidence, freshness, assistance dependence, timing, playback conditions, and readiness contribution remain separate.
- Stage 03 samples Listening with two short clips and records gist/detail performance, replay dependence, and relevant numbers/dates/times signals.
- Stage 04 already defines Listening nodes for gist, detail, numbers/dates/times/prices/names, negation/restrictions/corrections, intention, inference, paraphrase recognition, distractor rejection, authentic-speed tolerance, attention continuity, and strategic use of the permitted listening opportunity.
- Stage 05 distinguishes **vocabulary gap**, **listening-recognition failure**, **misunderstanding/comprehension**, **exam strategy**, **attention slip**, **timing/execution pressure**, and unresolved causes. A transcript-success contrast may help distinguish vocabulary from sound recognition.
- A single wrong answer does not create a durable fine-grained weakness. Known weaknesses require sufficiently confident independent recurrence.
- Stage 06 prioritizes pass-critical evidence gaps, due repair, active weaknesses, realism progression, and coverage; it must not repeatedly serve cheap objective skills while under-sampling another pass-relevant area.
- Stage 07 requires narrow repair, normally about 2–6 minutes and ordinarily under eight minutes, followed by a **fresh equivalent retry** when useful. Same-item replay after answer exposure is not independent transfer.
- Stage 08 uses **P0 Supported Foundation → P1 Guided A2 → P2 A2/B1 Bridge → P3 Independent B1 Training → P4 Target Conditions** by task family, not one global learner level.
- Stage 08 already establishes the assistance direction: slowed/careful audio and generous replay may exist at lower rungs; transcript is normally post-attempt repair support; target-condition attempts remove learning assistance and use the exact target playback rule.
- Assistance offered but unused does not weaken evidence. Assistance actually used before submission remains attached to the attempt.
- Real/reference exams define what Listening must resemble. The App should normally serve original audio unless exact reuse is permitted by rights metadata.
- Objective answer scoring should be deterministic from reviewed keys. Runtime premium AI is not justified merely to score standard Listening items.
- Bestehen is initially a personal project, so reusable reviewed scripts, batch audio generation, caching, deterministic diagnosis, and selective human review are preferred to recurring per-attempt AI or audio-generation costs.

No earlier App product decision is materially changed by Stage 11.

---

## 3. Target-Format Verification

### 3.1 Current TELC B1 Listening blueprint

The target format was rechecked on **19 August 2026** against the current official telc Deutsch B1 product page and the official downloadable `Zertifikat Deutsch / telc Deutsch B1 — Übungstest 1`.

The current official product page states that **Hören has three parts and lasts approximately 30 minutes**. The official model test defines the three mechanisms below:

| Family | Official target intent | Current model-test mechanism | Current model-test size | Playback rule |
|---|---|---|---:|---|
| **H1 — Global understanding / Globalverstehen** | Understand the main message of short spoken texts | Five short texts; decide whether one statement per text is true or false | 5 decisions | Each text **once** |
| **H2 — Detailed understanding / Detailverstehen** | Follow details across a longer spoken exchange | One conversation/interview; decide whether ten statements are true or false | 10 decisions | Conversation **twice** |
| **H3 — Selective understanding / Selektives Verstehen** | Extract a specific useful detail from short functional audio | Five short texts; decide whether one statement per text is true or false | 5 decisions | Each text **twice** |

The same official model test assigns **25 points to each Listening part, 75 points total**, which is **25% of the full 300-point examination**. Final readiness weighting and pass logic still belong to Stage 15; Stage 11 uses this only to recognize that Listening is a material written-component evidence stream and that none of the three task families should be ignored.

Official references used for verification:

- [telc — Zertifikat Deutsch / telc Deutsch B1](https://www.telc.net/sprachpruefungen/deutsch/zertifikat-deutsch-telc-deutsch-b1/)
- [telc — Zertifikat Deutsch B1, Übungstest Version 1](https://shop.telc.net/media/catalog/product/file/2/0/20201225_5061-b00-010301_web.pdf)

**Product rule:** the exact target blueprint is versioned exam knowledge. Before content is labelled **P4**, a Listening mock is called TELC-realistic, or a playback rule contributes readiness-grade evidence, Bestehen must use a currently verified target blueprint. Older audio may remain useful skill evidence when the underlying listening behavior still transfers, but it must not silently retain current-target status after a material blueprint change.

### 3.2 Listening task-family model

#### H1 — Global understanding

The learner hears five independent short spoken texts and must decide whether a statement captures the relevant overall message. The decisive skill is not perfect word-by-word transcription. It is recognizing what the speaker is essentially saying despite paraphrase, unimportant details, and only one listening opportunity.

Primary capabilities:

- gist and situation recognition;
- communicative purpose or stance;
- paraphrase/synonym recognition in speech;
- identifying the main proposition rather than one vivid detail;
- negation/restriction awareness when it changes the overall claim;
- attention protection under one-play conditions;
- deciding without waiting for complete lexical understanding.

#### H2 — Detailed understanding

The learner hears one longer conversation/interview twice and evaluates ten statements against details distributed across the exchange.

Primary capabilities:

- detailed comprehension over a longer span;
- tracking speaker turns and who said what;
- retaining/recovering information across the clip;
- recognizing corrections, contrasts, qualifications, and changed information;
- numbers, dates, quantities, prices, names, and other concrete details where present;
- local and cross-turn inference;
- rejecting statements that are plausible but not supported;
- using the two listening opportunities strategically.

#### H3 — Selective understanding

The learner hears five short functional texts twice and extracts the one detail needed to judge each statement. Typical mechanisms include announcements, directions, weather/service information, travel information, offers, prices, schedules, or other everyday functional audio.

Primary capabilities:

- scanning in audio for a target category;
- numbers, times, dates, prices, addresses, names, places, and conditions;
- distinguishing similar values or near matches;
- negation, restriction, exception, and correction cues;
- paraphrase recognition;
- resisting irrelevant surrounding information;
- maintaining attention until the decisive detail arrives.

---

## 4. Lower-Difficulty Listening Variants

A lower-difficulty activity may simplify language, length, information density, speaker count, distractor closeness, speech rate, or playback limits, but it must preserve the target **listening behavior**. A vocabulary drill with no audio decision is repair support, not a lower-difficulty TELC Listening variant.

### 4.1 H1 progression

| Rung | Training variant | Main simplification | Evidence claim |
|---|---|---|---|
| **P0 Supported Foundation** | 2–3 very short monologues/dialogue turns with one clear gist statement each | Concrete A1/early-A2 language, careful-natural speed, small vocabulary preview, generous bounded replay | Supported gist recognition in audio |
| **P1 Guided A2** | 3–4 short texts with mild paraphrase and one distractor detail | Genuine A2 language, closer statement wording, selective/on-request help | Functional global listening at A2 |
| **P2 A2/B1 Bridge** | 4–5 short texts with B1-shaped paraphrase and controlled density | Near-natural speed, limited support, playback close to target | B1-shaped global listening with limited assistance |
| **P3 Independent B1** | Full or near-full original B1-equivalent set | Authentic B1 language and natural speech; no default help | Independent B1 H1 evidence |
| **P4 Target Conditions** | Current verified target-form set | No simplification | Readiness-grade H1 evidence under one-play rules |

### 4.2 H2 progression

| Rung | Training variant | Main simplification | Evidence claim |
|---|---|---|---|
| **P0** | 45–75 second dialogue/interview with 3–4 statements | Clear speaker turns, low information density, concrete details, generous replay | Supported detail tracking |
| **P1** | 1–2 minute dialogue with 4–6 statements | A2 language, mild corrections/contrast, selective support | Functional detail comprehension |
| **P2** | Medium conversation with 6–8 statements | More natural turn-taking, closer distractors, distributed evidence | B1-shaped detail listening |
| **P3** | Full or near-full original B1-equivalent conversation | Authentic B1 density and two-play default | Independent B1 H2 evidence |
| **P4** | Current verified target-form conversation | Exact target playback and sequencing | Readiness-grade H2 evidence |

### 4.3 H3 progression

| Rung | Training variant | Main simplification | Evidence claim |
|---|---|---|---|
| **P0** | 2–3 short functional announcements/messages with one concrete detail each | High-frequency domains, slower/careful speech, clear number/time/place contrasts, generous replay | Supported selective listening |
| **P1** | 3–4 functional clips | A2 language, one or two competing details, selective support | Functional selective comprehension |
| **P2** | 4–5 clips with B1-shaped paraphrase, corrections, or similar values | Near-natural speed, target-rule count plus limited extra replay | B1-shaped selective listening |
| **P3** | Full or near-full original B1-equivalent set | Authentic density and target playback by default | Independent B1 H3 evidence |
| **P4** | Current verified target-form set | Exact target playback/sequencing | Readiness-grade H3 evidence |

The coach should normally adjust the **causal difficulty axis** that blocked performance rather than making every axis easier at once. A learner who understands normal-speed audio but fails because numbers are confusable needs number discrimination, not universally slowed language.

---

## 5. Audio Source Strategy

### 5.1 Separate reference audio from learner audio

**Decision:** Audio is divided into two conceptual roles:

1. **Reference/calibration audio** tells Bestehen what the target sounds like: duration, speech rate, articulation, speaker patterns, prosody, information density, task cues, and distractor behavior.
2. **Learner practice audio** is what the App is allowed to play to the learner.

Official and other reference audio may be analyzed by Corpus when permitted, but exact audio is surfaced in the App only when rights metadata allows that use. Public availability is not treated as redistribution permission.

### 5.2 Preferred launch source mix

| Source class | Default role | Product strengths | Product limitations |
|---|---|---|---|
| **Reviewed original TTS, pre-generated and cached** | Default broad P0–P3 practice bank | Very low marginal cost, easy speed/voice variation, reproducible, scalable, supports large original exercise bank | Can sound too clean, mispronounce names/numbers, flatten conversational prosody, or create provider-specific artifacts |
| **Original native-human recording** | Small benchmark/P4 bank and calibration anchor | Natural reductions, timing, emphasis, repair, hesitation, and interaction; strongest defense against training only to synthetic speech | Highest authoring/coordination cost; slower to scale |
| **Premium expressive neural TTS** | Upgrade for dialogue/prosody-sensitive assets or scalable P3/P4-quality content after validation | Better naturalness and multi-speaker control than commodity TTS with still-low marginal cost after caching | Higher generation cost; quality still requires review; synthetic regularity can remain |
| **Local/on-device/basic TTS** | Optional fallback for repair snippets or very low-stakes generated examples | Near-zero provider cost and can work offline | Voice/device inconsistency; weaker standardization; not suitable as sole readiness evidence |
| **Rights-cleared official/reference audio** | Benchmark or learner content only when explicitly reusable | Closest possible target evidence | Usually scarce and rights-constrained; cannot be assumed available |

### 5.3 Low-cost default

**Decision:** The initial product should use **reviewed original scripts → batch TTS generation → permanent caching** for most training audio.

Normal learner attempts must not trigger fresh TTS generation. Audio variants are generated ahead of use or once and then cached. The same reviewed asset can serve many attempts with effectively zero marginal generation cost.

This preserves quality better than uncontrolled device TTS and cost better than recording every training item with humans. It also makes attempts reproducible: two learners hearing the same content can receive the same audio condition.

### 5.4 Generated versus human/native policy

**Decision:** Generated audio is acceptable for the majority of learning and evidence collection, but **strong Listening readiness must not be based solely on one synthetic voice style or one unvalidated TTS system**.

The policy is:

- **P0–P2:** reviewed cached TTS is the normal default. Human audio is optional rather than required.
- **P3:** reviewed high-naturalness TTS is acceptable for most practice, but the learner should encounter multiple voices and at least some human/native or separately validated high-naturalness assets so the skill does not become “understand this synthesizer.”
- **P4/readiness anchors:** prefer original native-human recordings or premium/generated audio that has been explicitly human-audited and calibrated against current target audio characteristics. A small native-human benchmark bank is the recommended personal-project default because its one-time creation cost is bounded and it materially improves confidence in readiness evidence.
- **Ready-to-book Listening evidence:** later Stage 15/17 logic should require variety across independent audio forms/voices and should not treat repeated success on one synthetic voice as equivalent to robust target listening.

This is a quality requirement, not a mandate to human-record the entire product. A small reusable benchmark set creates most of the value at far lower cost than a fully human-recorded catalog.

### 5.5 Voice and asset diversity rules

A Listening bank should vary what matters without adding artificial difficulty:

- multiple adult German-speaking voices rather than one permanent narrator;
- both single-speaker and multi-speaker audio where the task family requires it;
- male/female voice variety and a reasonable range of timbre/age presentation without stereotyping;
- natural conversational turn-taking for dialogue assets;
- standard intelligible German as the baseline, with mild natural voice variation before deliberate regional-accent difficulty is introduced;
- numbers, dates, prices, names, and functional expressions checked especially carefully because a single synthesis error can invalidate the item.

Artificial background noise is **not** a default difficulty lever. P4 should resemble the verified target audio environment, not be made harder for motivational effect. Noisy audio may be used later as robustness practice, but it is not automatically readiness-grade TELC evidence.

---

## 6. Speech-Speed Progression

### 6.1 Speed is one difficulty axis, not the definition of level

**Decision:** Bestehen changes speech rate only when it addresses a demonstrated reachability or recognition problem. It must not assume that every A1 learner needs uniformly slow audio or that fast audio alone makes a task B1.

The initial progression uses relative speed bands anchored to the natural target-style version of the same or equivalent content. Exact values are starting operating ranges to be calibrated against real audio and learner performance, not permanent psychometric thresholds.

| Rung | Initial speed behavior | Product intent |
|---|---|---|
| **P0** | Approximately **0.80–0.90×** natural target-style rate, with careful but still connected speech | Make segmentation possible without teaching robotic word-by-word German |
| **P1** | Approximately **0.90–0.97×** | Reduce speed assistance while keeping audio reachable |
| **P2** | Approximately **0.97–1.00×**, normal speed increasingly default | Bridge to natural target-like speech |
| **P3** | **1.00× natural** for normal attempts; slower playback exists only as explicit assistance in practice | Establish independent natural-speed capability |
| **P4** | Exact calibrated target asset at its authored speed | Preserve target-condition evidence |

Guardrails:

1. Do not stretch audio so far that prosody or consonant/vowel quality becomes unnatural.
2. Prefer a separately generated careful version when basic time-stretching materially degrades speech.
3. If a learner can read/understand the transcript but repeatedly fails normal-speed audio, speed/connected-speech recognition becomes a candidate cause.
4. If the learner still does not understand the transcript, slowing the audio is unlikely to repair the root cause; vocabulary/comprehension repair should come first.
5. P4 never exposes a learner-controlled speed slider during the measured attempt.

---

## 7. Replay Rules by Progression Stage

Replay is valid learning support but a first-class evidence condition. “Correct after four plays” and “correct under the target playback rule” are different capabilities.

| Rung | Replay behavior during a clean practice attempt | Evidence treatment |
|---|---|---|
| **P0** | Generous but bounded: normally the authored first play plus up to **three additional plays** per short clip/segment when needed | Valid supported Listening evidence; every play recorded |
| **P1** | Up to **two plays beyond the current target-family rule** | Assisted evidence; coach watches whether extra replay is still needed |
| **P2** | Current target-family rule plus **one optional extra play** | Near-target learning evidence; using the extra play marks the attempt assisted |
| **P3** | Current target-family rule by default. One explicit extra replay may be offered in ordinary practice after the target opportunity has been used | Result before extra replay is clean P3 evidence; result relying on the extra replay is assisted and cannot masquerade as target playback evidence |
| **P4** | **Exact current target rule only:** H1 once; H2 twice; H3 each short text twice | Strong target-condition playback evidence when the rest of the attempt is valid |

Additional rules:

- Replaying during **Repair** after the original attempt is not restricted by the attempt's evidence rule, but it is repair exposure rather than new readiness evidence.
- Scrubbing, seeking, looping the decisive second, or pausing inside a measured P4 clip is not allowed unless the verified target format permits it.
- If a technical interruption causes playback loss, the attempt is invalid or technically compromised; the learner is not penalized and the system does not pretend the original playback condition was preserved.
- Replay need is tracked by task family. A learner can be target-stable on H2 while still needing extra plays on H1.

---

## 8. Transcript Availability

### 8.1 Transcript is diagnosis/repair support, not routine in-attempt help

**Decision:** The full transcript is normally unavailable until the learner has made a meaningful listening attempt.

Showing live text during a Listening attempt changes the capability from sound-to-meaning recognition toward Reading and therefore cannot be treated as equivalent evidence.

| Rung | Transcript during attempt | Transcript after attempt |
|---|---|---|
| **P0** | Normally hidden. A transcript may be used only when the explicit exercise goal is no longer direct Listening evidence, e.g. a repair contrast | Available in Diagnose/Repair, preferably aligned to the relevant audio span |
| **P1** | Hidden | Available after the attempt for explanation/repair |
| **P2** | Hidden | Available after the attempt, often as a focused excerpt rather than full reveal |
| **P3** | Hidden in clean attempt; opening it converts the activity into assisted learning | Available after submission or target opportunity |
| **P4** | Unavailable for the entire measured block | Available only after the measured block ends |

The repair experience should prefer **focused transcript exposure**: show the decisive line or short span, replay it, and explain why the learner missed it. Full transcript reading is useful when necessary but should not become the default response to every wrong answer.

### 8.2 Transcript-based diagnosis

A transcript can isolate causes cheaply:

- understands the word/phrase in text but not audio → likely sound-recognition/speed/connected-speech issue;
- still does not understand it in text → vocabulary or broader comprehension issue;
- understands the decisive sentence but chose the wrong answer → distractor, inference, negation, strategy, or attention becomes more plausible;
- transcript itself reveals that the item or synthesized audio was wrong/ambiguous → invalidate content rather than diagnose the learner.

The learner's success **after** transcript exposure is repair evidence, not independent Listening mastery.

---

## 9. Pre-Listening Vocabulary Assistance

### 9.1 Targeted preview, never a hidden answer key

**Decision:** Vocabulary preview exists to make the audio reachable, not to remove the need to listen.

A preview may include a small number of high-value domain words, phrases, or sound forms needed to understand the setting. It must not reveal the decisive answer, exact number/date/time, negation, correction, or distinctive phrase that the live item is designed to test.

| Rung | Default preview policy |
|---|---|
| **P0** | Usually **3–6** carefully selected words/phrases when lexical load would otherwise block a meaningful attempt; include audio form plus short meaning/translation where useful |
| **P1** | **0–4** items, mainly for a new/high-load domain; otherwise on request |
| **P2** | Rare by default; normally **0–2** items or on request |
| **P3** | No default preview. On-request live-item vocabulary help makes the attempt assisted |
| **P4** | No vocabulary preview for the measured attempt beyond the verified target instructions/material |

Rules:

- A previewed word does not prove independent vocabulary mastery or sound recognition.
- Known learner vocabulary should not be previewed merely because it appears on a generic list.
- Corpus frequency and task relevance may help choose preview candidates, but learner evidence determines whether the support is actually needed.
- If too many words would require preview, the content is probably above the learner's reachable linguistic rung; choose a simpler original clip rather than displaying a glossary that turns Listening into assisted translation.

---

## 10. Listening Diagnostic Taxonomy

Listening diagnosis begins with the Stage 07 validity check: confirm that the asset played correctly, the learner understood the task, the answer key is defensible, and the audio itself is not malformed. Only then attribute a learner cause.

The following listening-specific patterns map into the broader Stage 05 root-cause taxonomy.

| Listening diagnosis | What it means | Cheap discriminating evidence | Mistake Memory mapping |
|---|---|---|---|
| **Unknown vocabulary** | The learner does not know the relevant word/phrase meaning | Show the decisive word/short phrase in text after the attempt; meaning remains unknown | Vocabulary gap |
| **Numbers / dates / times / prices / names** | The learner confuses or cannot retain a concrete spoken value | Replay a fresh minimal contrast or ask for the heard value without the original options | Usually listening-recognition; may be attention/strategy if value was heard correctly but applied wrongly |
| **Speed / connected-speech recognition** | Known language is not segmented/recognized at natural speed | Learner understands transcript and/or careful version but not natural version | Listening-recognition failure |
| **Distractor / correction failure** | Learner hears a plausible early or nearby detail but misses later correction, qualification, speaker attribution, or partial-match problem | Ask which phrase made the first interpretation invalid; use a short fresh correction contrast | Misunderstanding or exam-strategy error depending on behavior |
| **Missed negation / restriction / exception** | `nicht`, `kein`, `nur`, `erst`, `außer`, contrast, or equivalent cue reverses/limits meaning | Focused transcript/audio contrast shows whether cue was unheard or misunderstood | Listening-recognition or comprehension gap; strategy if repeatedly not checked |
| **Inference failure** | Explicit details were understood, but the supported conclusion/intention was not | Confirm literal clues first, then ask what follows from them | Misunderstanding/comprehension gap |
| **Attention continuity / position loss** | Learner can understand local chunks but loses the thread, item position, or decisive late information across a longer sequence | Short same-speed excerpt succeeds; longer span repeatedly fails without another language cause | Attention slip, exam strategy, or timing/execution pressure; use cautiously |
| **Speaker/source attribution** | Learner understands content but assigns it to the wrong speaker or turn | Ask who said/changed the relevant proposition using a focused replay | Comprehension/strategy |
| **Sound-form / paraphrase mismatch** | Learner knows the concept but does not connect the spoken form/paraphrase to the statement | Contrast statement wording with the heard expression | Listening recognition or vocabulary/paraphrase gap |
| **Instruction/format misunderstanding** | Learner listened to the wrong thing because the task rule was misunderstood | One simple format check before further language repair | Exam-strategy / misunderstanding |
| **Unresolved / mixed** | More than one cause remains plausible | Collect one small clarifying probe rather than assigning several weaknesses | Unresolved / mixed |

### 10.1 Required diagnosis guardrails

- **Unknown vocabulary vs speed:** if the learner does not know the meaning when the phrase is visible, do not label speed as the primary cause.
- **Numbers/dates/times:** do not automatically label every wrong value as “numbers weakness.” A close distractor, late correction, memory lapse, or synthesis problem may be the real cause.
- **Missed negation:** distinguish not hearing the cue from hearing it but misunderstanding its scope.
- **Distractors:** a distractor diagnosis requires a plausible competing cue in the audio/task design; do not use “distractor” as a generic explanation for any wrong answer.
- **Inference:** only diagnose inference after the relevant literal information is understood. Otherwise the repair should target the earlier comprehension failure.
- **Attention:** never turn one miss into a trait label such as “poor attention.” Learner-facing copy uses a neutral, local description such as “You lost the key detail after the speaker changed the plan.” Repeated independent episodes are needed before an attention/strategy pattern becomes a known weakness.
- **Technical/audio-quality failure:** invalidates the evidence rather than becoming a learner weakness.

### 10.2 Diagnosis confidence

Listening cause confidence follows Stage 05:

- **Unresolved:** keep broad H1/H2/H3 result and collect a natural clarifier later.
- **Low:** plausible cause may shape the next probe but cannot create a fine known weakness.
- **Medium:** direct transcript/audio contrast or repeated response pattern supports the cause; eligible for recurrence.
- **High:** a controlled contrast, strong reviewed distractor rationale, or repeated clear independent pattern isolates the cause.

The system should prefer one defensible primary cause and at most one material contributor rather than attaching every plausible Listening tag to the same wrong answer.
