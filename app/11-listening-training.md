# Bestehen / App — Stage 11: Listening Training

> **Status:** Authoritative Stage 11 product-shaping decision
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

The product outcome is not merely “the learner got more listening questions right.” Bestehen must be able to explain:

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
- Stage 04 defines Listening nodes for gist, detail, numbers/dates/times/prices/names, negation/restrictions/corrections, intention, inference, paraphrase recognition, distractor rejection, authentic-speed tolerance, attention continuity, and strategic use of the permitted listening opportunity.
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

## 3. Decisions and Rationale

### 3.1 Map Listening to three TELC target families

The target format was rechecked on **19 August 2026** against the current official telc Deutsch B1 product page and the official downloadable `Zertifikat Deutsch / telc Deutsch B1 — Übungstest 1`.

The current official product information describes **three Listening parts lasting approximately 30 minutes**. The official model test uses these mechanisms:

| Family | Target mechanism | Model-test shape | Playback behavior |
|---|---|---|---|
| **H1 — Global understanding / Globalverstehen** | Five short spoken texts; judge one statement per text | 5 decisions | Each text **once** |
| **H2 — Detailed understanding / Detailverstehen** | One longer conversation/interview; judge statements against distributed detail | 10 decisions | Conversation **twice** |
| **H3 — Selective understanding / Selektives Verstehen** | Five short functional texts; extract one decisive detail per text | 5 decisions | Each text **twice** |

The official model test allocates **75 points to Listening in total**, 25 per part. Final readiness weighting and pass logic remain Stage 15 decisions.

Official references:

- `https://www.telc.net/sprachpruefungen/deutsch/zertifikat-deutsch-telc-deutsch-b1/`
- `https://shop.telc.net/media/catalog/product/file/2/0/20201225_5061-b00-010301_web.pdf`

**Decision:** Treat the exact blueprint as versioned target knowledge. Before content is called **P4**, a Listening mock is called TELC-realistic, or playback conditions contribute readiness-grade evidence, the current blueprint must be revalidated.

### 3.2 Preserve the listening mechanism while lowering difficulty

A lower-difficulty activity may simplify language, length, information density, speaker count, distractor closeness, speech rate, or playback limits, but it must preserve the target listening behavior.

- H1 remains about global meaning and communicative purpose.
- H2 remains about following detailed information across a longer exchange.
- H3 remains about locating one useful detail inside short functional audio.

A vocabulary-only drill or transcript-reading task is useful repair, but it is not direct Listening evidence.

### 3.3 Separate audio source roles

**Decision:** Audio has two roles:

1. **Reference/calibration audio** tells Bestehen what target audio sounds like: duration, speech rate, articulation, prosody, density, speaker behavior, corrections, and task cues.
2. **Learner practice audio** is content the App is actually allowed to play.

Corpus may learn from reference audio according to rights and source rules. Exact source audio is surfaced only when usage rights permit it. Public accessibility is not redistribution permission.

### 3.4 Use cached reviewed TTS as the broad default, not the only readiness source

**Decision:** Most P0–P3 training audio should use **reviewed original scripts → batch TTS generation → permanent caching**.

This gives the personal project the best launch trade-off:

- effectively zero marginal generation cost after creation;
- reproducible audio conditions;
- scalable content breadth;
- easy multi-voice and speed variants;
- no need for a live model or TTS request during normal attempts.

However, strong Listening readiness must not be built from one synthetic voice style or one unvalidated TTS system.

Policy by rung:

- **P0–P2:** reviewed cached TTS is the normal default.
- **P3:** high-naturalness reviewed TTS is acceptable for most work, but learners should encounter voice diversity and some independently validated or human/native assets.
- **P4/readiness anchors:** prefer original native-human recordings or premium/generated audio that has been human-audited and calibrated against target audio characteristics.

A **small reusable human/native benchmark bank** is the recommended personal-project upgrade. It provides much of the authenticity value without the cost of human-recording the entire catalog.

### 3.5 Treat speech speed as one difficulty axis

**Decision:** Speed changes only when it addresses a demonstrated reachability or recognition problem. Fast audio alone does not make a task B1, and lower-level learners should not automatically hear unnaturally slow speech.

Initial operating bands, relative to the natural target-style version:

| Rung | Initial speed behavior |
|---|---|
| **P0** | about **0.80–0.90×**, careful but connected speech |
| **P1** | about **0.90–0.97×** |
| **P2** | about **0.97–1.00×**, normal speed increasingly default |
| **P3** | **1.00× natural** by default; slower playback is explicit assistance |
| **P4** | authored/calibrated target asset at its actual speed |

These are starting product ranges, not psychometric constants. They must be recalibrated against real target audio and learner outcomes.

### 3.6 Replay is a first-class evidence condition

**Decision:** Replay may support learning but must never disappear from the evidence history.

| Rung | Replay policy during clean practice |
|---|---|
| **P0** | Authored first play plus up to **three additional plays** when needed |
| **P1** | Up to **two plays beyond the target-family rule** |
| **P2** | Target-family rule plus **one optional extra play** |
| **P3** | Target-family rule by default; an extra replay may be offered only as explicit assisted practice after the target opportunity |
| **P4** | Exact current target rule only: H1 once; H2 twice; H3 each text twice |

Correct after four plays and correct under the target rule are different claims. Both are useful; only one is target-condition evidence.

### 3.7 Transcripts belong to diagnosis and repair

**Decision:** Full transcripts are normally hidden until the learner makes a meaningful listening attempt. Live text changes the task from sound-to-meaning toward reading and therefore cannot be treated as equivalent Listening evidence.

- **P0–P2:** transcript hidden in the clean attempt; available after submission, preferably as a focused excerpt.
- **P3:** hidden in clean attempts; opening it during practice converts the attempt to assisted learning.
- **P4:** unavailable for the entire measured block; available only after measurement ends.

Focused transcript exposure is preferred over dumping the entire transcript whenever one line explains the failure.

### 3.8 Vocabulary preview should make audio reachable, not reveal the answer

**Decision:** Pre-listening vocabulary assistance is small, targeted, and difficulty-sensitive.

| Rung | Default preview policy |
|---|---|
| **P0** | Usually **3–6** selected words/phrases when lexical load would otherwise block a meaningful attempt |
| **P1** | **0–4** items, mainly for a new/high-load domain |
| **P2** | Rare by default; normally **0–2** or on request |
| **P3** | No default preview; live-item help marks the attempt assisted |
| **P4** | No preview beyond verified target material/instructions |

Preview must not reveal the decisive number, date, negation, correction, restriction, or answer-bearing phrase.

---

## 4. Detailed Product Model / Rules for this Stage

### 4.1 Task-family skill model

#### H1 — Global understanding

Primary capabilities:

- gist and situation recognition;
- communicative purpose or stance;
- spoken paraphrase/synonym recognition;
- deciding based on the main proposition rather than one vivid detail;
- negation/restriction awareness where it changes the overall message;
- attention protection under one-play conditions;
- tolerating unknown words without abandoning the main idea.

#### H2 — Detailed understanding

Primary capabilities:

- detailed comprehension across a longer exchange;
- tracking speaker turns and attribution;
- retaining and recovering information across the clip;
- recognizing corrections, contrasts, qualifications, and changed information;
- numbers, dates, quantities, prices, names, and other concrete details;
- local and cross-turn inference;
- rejecting plausible but unsupported statements;
- using the two listening opportunities strategically.

#### H3 — Selective understanding

Primary capabilities:

- listening for a target category;
- numbers, times, dates, prices, addresses, names, places, and conditions;
- distinguishing similar values or near matches;
- negation, restriction, exception, and correction cues;
- paraphrase recognition;
- resisting irrelevant surrounding information;
- maintaining attention until the decisive detail arrives.

### 4.2 Lower-difficulty variants

| Family | P0 Supported Foundation | P1 Guided A2 | P2 A2/B1 Bridge | P3 Independent B1 | P4 Target Conditions |
|---|---|---|---|---|---|
| **H1** | 2–3 very short texts, one clear gist claim, careful speed, preview/replay support | 3–4 short A2 texts with mild paraphrase | 4–5 B1-shaped texts, near-natural speed, limited support | Full/near-full B1-equivalent set, natural speed | Current verified target form, exact one-play rule |
| **H2** | 45–75 sec dialogue, 3–4 statements, clear turns, low density | 1–2 min exchange, 4–6 statements, mild contrast/correction | Medium conversation, 6–8 statements, more distributed detail | Full/near-full B1-equivalent conversation | Current verified target form, exact two-play rule |
| **H3** | 2–3 functional clips with one concrete detail, careful speed | 3–4 clips, one or two competing details | 4–5 clips, B1 paraphrase, similar values/corrections | Full/near-full B1-equivalent set | Current verified target form, exact two-play rule |

The coach should adjust the **causal difficulty axis** rather than lowering everything. If natural speed is fine but 15/50 is repeatedly confused, target number discrimination instead of slowing the whole clip.

### 4.3 Listening diagnostic taxonomy

Diagnosis begins with validity: confirm that the media played correctly, the content/key is defensible, and the learner understood the task. Only then attribute a learner cause.

| Diagnosis | Meaning | Cheap discriminating evidence | Stage 05 mapping |
|---|---|---|---|
| **Unknown vocabulary** | Relevant word/phrase meaning is not known | Show decisive word/short phrase in text after attempt; meaning remains unknown | Vocabulary gap |
| **Numbers/dates/times/prices/names** | Concrete spoken value is confused, missed, or not retained | Fresh minimal audio contrast or ask for heard value without original distractors | Usually listening-recognition; sometimes strategy/attention |
| **Speed / connected speech** | Known language is not segmented/recognized at natural speed | Transcript or careful version is understood, natural version is not | Listening-recognition failure |
| **Distractor / correction** | Learner follows an early/plausible detail but misses correction, qualification, speaker attribution, or partial-match problem | Ask which phrase invalidated the first interpretation; fresh correction contrast | Misunderstanding or exam-strategy error |
| **Missed negation / restriction** | `nicht`, `kein`, `nur`, `erst`, `außer`, contrast, or equivalent cue reverses/limits meaning | Focused text/audio contrast shows whether cue was unheard or misunderstood | Listening recognition or comprehension; sometimes strategy |
| **Inference** | Literal clues are understood but supported conclusion/intention is wrong | Confirm literal clues, then ask what follows | Comprehension gap |
| **Attention continuity / position loss** | Local chunks are understood but the thread or decisive late information is lost | Short same-speed excerpt succeeds while longer sequence repeatedly fails | Attention/strategy/execution, used cautiously |
| **Speaker attribution** | Content is understood but assigned to the wrong speaker/turn | Focused replay with “who said/changed this?” | Comprehension/strategy |
| **Spoken paraphrase mismatch** | Concept is known but spoken wording is not connected to the statement | Contrast statement wording with heard expression | Listening recognition / vocabulary-paraphrase |
| **Instruction/format misunderstanding** | Learner listens for the wrong thing because task mechanics were misunderstood | One simple format check | Strategy / misunderstanding |
| **Unresolved / mixed** | More than one cause remains plausible | Collect one small clarifying probe | Unresolved / mixed |

Required guardrails:

- If the learner does not know the meaning when the phrase is visible, do not label speed as the primary cause.
- Do not label every wrong number as a “numbers weakness”; a correction, distractor, memory lapse, or bad synthesis may be responsible.
- Distinguish **not hearing** negation from **hearing but misunderstanding its scope**.
- Diagnose distractor failure only when a real distractor mechanism exists.
- Diagnose inference only after literal information is shown to be understood.
- Never turn one miss into a trait label such as “poor attention.” Learner-facing copy describes the local behavior neutrally.
- Technical/audio-quality failures invalidate evidence rather than creating learner weaknesses.

### 4.4 Targeted repair matrix

Listening repair remains within Stage 07's narrow 2–6 minute norm and ordinarily under eight minutes.

| Cause | Repair | Fresh retry |
|---|---|---|
| **Unknown vocabulary** | Give short meaning in context, play the word/phrase in isolation and one natural phrase; optionally contrast a close synonym | New clip using the same concept with different wording/context |
| **Number/date/time confusion** | Contrast the specific confusable forms using several short natural utterances; require recognition before re-entering a full task | Fresh functional clip with a different value and distractor |
| **Speed/connected speech** | Play decisive span natural → careful → natural; show how words connect/reduce; transcript only after the listening contrast when needed | Different sentence/clip at natural speed with the same recognition challenge |
| **Negation/restriction** | Replay the cue and the clause it scopes; contrast affirmative/restricted versions | Fresh audio containing a different restriction cue |
| **Distractor/correction** | Show the information timeline: initial detail → correction/qualification → final valid meaning | Fresh clip with a different correction or partial-match pattern |
| **Inference** | Reconstruct the literal clues and the smallest justified conclusion; explain what is not supported | Fresh clip requiring the same type of inference but different content |
| **Attention continuity** | Use a shorter same-speed span, teach one concrete tracking behavior, then extend length | New longer clip with target attention behavior |
| **Speaker attribution** | Mark speaker turns after the attempt, replay decisive turn pair, explain pronoun/reference cue if relevant | Fresh two-speaker exchange |
| **Paraphrase mismatch** | Pair the spoken phrase with the task wording and one extra paraphrase | Fresh clip with another paraphrase of the same concept |
| **Strategy/format** | Teach one observable behavior: preview statement, listen for target category, use second play to verify uncertain items | Same family, fresh content, no answer exposure |

A same-item replay after the answer is known can be useful repair, but it does not satisfy the fresh retry requirement.

### 4.5 Listening-specific loop

#### Observe

Show:

- family/goal;
- expected duration;
- playback rule;
- whether slower audio, vocabulary preview, extra replay, or transcript will be available;
- why the task matters when not obvious.

Do not reveal answer-bearing vocabulary or the decisive cue.

#### Attempt

- Keep feedback hidden until the relevant measured block ends.
- Record actual playback count, speed, help used, answer, response timing, media validity, and whether the clip was fully heard.
- P4 prevents seeking, looping, speed change, transcript access, and between-item coaching unless the verified target allows them.

#### Diagnose

- Validate the audio/item first.
- Show the decisive audio/text evidence after the clean attempt.
- Select one primary cause and at most one contributor, or remain unresolved.
- Use a cheap contrastive probe when it materially changes repair choice.

#### Repair

- Work on the smallest acoustic, lexical, comprehension, or strategy blocker.
- Prefer a decisive short span over replaying an entire long conversation repeatedly.
- Transcript is available as diagnosis/repair support once it no longer contaminates the original attempt.

#### Retry

- Use **different audio** and different answer content while preserving the underlying listening capability.
- Same voice can be used for an immediate skill check, but delayed evidence should include voice/form variation so mastery is not voice-specific.
- Immediate retry success shows responsiveness, not retained mastery.

#### Remember

Record:

- family and capability target;
- difficulty profile;
- speed condition;
- playback count/rule;
- preview/transcript/help used;
- diagnosed cause and confidence;
- retry outcome;
- due delayed transfer or monitoring;
- whether evidence was learning-grade, independent B1, or P4 target-condition evidence.

### 4.6 Audio difficulty model

**Decision:** Audio difficulty is multidimensional. Do not compress “hard audio” into speech rate alone.

Every asset/task should be characterizable along these product dimensions:

| Dimension | Lower difficulty | Higher difficulty |
|---|---|---|
| Linguistic load | high-frequency concrete language | denser B1 vocabulary, grammar, abstraction, paraphrase |
| Speech rate | careful-natural | calibrated target-natural |
| Connected speech | clear boundaries | natural reductions/linking |
| Information density | one relevant fact with pauses | several facts/corrections close together |
| Duration / memory span | short clip | longer exchange with distributed evidence |
| Speaker complexity | one speaker / clearly separated turns | several turns, similar voices, attribution demand |
| Concrete-value load | few/no values | multiple similar times, prices, dates, names |
| Distractor closeness | irrelevant alternatives | plausible early/near details, corrections, partial matches |
| Negation/restriction load | explicit positive wording | scope, exceptions, corrections, contrast |
| Inference demand | explicit statement | intention/conclusion from clues |
| Topic familiarity | common learner domain | less familiar but still B1-relevant domain |
| Audio clarity | clean calibrated recording | target-natural clarity; never intentionally degraded without purpose |
| Playback condition | generous replay | exact target count |
| Support | preview/slower/transcript after attempt | no live learning help |

### 4.7 Initial difficulty scoring approach

The product needs a sortable difficulty estimate without pretending to have a psychometric scale before learner data exists.

**Decision:** Start with **five ordinal audio difficulty bands** — Foundation, A2, A2/B1 Bridge, B1, Target-Calibrated — plus a dimension profile explaining why the asset sits there.

Rules:

1. Human/review metadata or reliable offline classification may set the initial band.
2. No single dimension can automatically determine the band.
3. Low-confidence metadata lowers the confidence of any fine difficulty claim.
4. Learner performance later recalibrates the band and the relative impact of dimensions.
5. P4 requires not merely “Band 5” but a current target-calibrated blueprint, playback rule, content structure, and validated audio quality.

Do **not** invent a permanent numerical formula such as `0.25 × speed + 0.15 × speaker count`. Stage 26 can calibrate an empirical model once enough attempts exist.

### 4.8 Audio quality and item validity gate

Before an audio asset can contribute normal evidence, it must pass a product-level validity check:

- script is natural, grammatically and semantically correct German;
- answer is uniquely defensible under the intended task;
- TTS/human recording preserves the intended wording;
- numbers, dates, prices, names, abbreviations, and pronunciation are correct;
- speaker turns are attributable when the task depends on them;
- no accidental pause/emphasis gives away the answer;
- audio level and clipping are acceptable;
- difficulty and playback metadata are present;
- rights status permits the intended learner use;
- target-condition status is current when claimed.

Ambiguous or malformed audio is quarantined/invalidated. The learner is not charged with the failure.

### 4.9 Exam-realistic Listening mode

**Decision:** P4 Listening is a measured block, not ordinary coaching with a timer.

P4 behavior:

- use current verified H1/H2/H3 structure and playback counts;
- natural calibrated target-style audio;
- no vocabulary preview, transcript, speed control, extra replay, seeking, looping, or answer hints during measurement;
- no immediate correctness feedback or repair between items when that would differ from the exam flow;
- no pause/resume inside a measured audio sequence except a genuine technical/accessibility condition handled by later policy;
- technical interruptions invalidate or qualify the affected evidence rather than penalize the learner;
- diagnosis, transcript, replay freedom, and repair become available **after** the measured block;
- the post-block coaching loop then converts lost points into Mistake Memory and fresh later practice.

A learner may choose P4 early. A poor result becomes useful diagnostic evidence; it is not a progression punishment.

### 4.10 Readiness evidence supplied by Stage 11

Stage 11 does not calculate final readiness, but it defines what later readiness logic may trust.

Strong Listening evidence should include:

- direct H1, H2, and H3 performance rather than one generic Listening percentage;
- recent B1 or target-calibrated audio;
- exact playback conditions;
- no answer-bearing assistance during the measured attempt;
- natural speed;
- valid reviewed content and audio quality;
- sufficient breadth across independent assets;
- meaningful voice/audio diversity;
- enough target-condition evidence that replay or synthetic-voice dependence is not hidden;
- confidence/coverage labels when evidence is sparse or contradictory.

Evidence strength ladder:

| Evidence | Readiness interpretation |
|---|---|
| P0–P1 with preview/slower audio/extra replay | Learning progress; weak direct readiness contribution |
| P2 near-natural audio with limited assistance | Bridge evidence; useful for progression, not a strong pass claim |
| P3 natural-speed, unassisted, target playback by default | Strong independent B1 evidence |
| P4 current target blueprint, exact playback, no learning help | Strongest Listening readiness evidence |
| P4 plus varied voices/native-human or validated benchmark assets | Higher confidence that success generalizes beyond one synthetic voice or content template |

Stage 15 decides how these observations affect written readiness, minimum evidence, weights, uncertainty, and safe-pass language.

---

## 5. Edge Cases / Failure or Uncertainty Handling

### Learner understands transcript but not audio

Treat this as likely sound recognition, connected speech, or speed dependence rather than a generic vocabulary gap. Repair the acoustic form, then retry on fresh audio.

### Learner does not understand transcript either

Do not keep replaying. Repair vocabulary or sentence meaning first, then return to audio.

### Learner gets the answer right only after extra replay

Preserve both results: target opportunity and assisted outcome. The learner improved, but target playback independence remains unproven.

### Learner repeatedly fails one synthetic voice

Do not conclude broad Listening weakness until voice-specific difficulty, synthesis quality, and pronunciation are checked. Use another validated voice/audio asset.

### TTS pronounces a name/number unnaturally

Invalidate the affected item. Do not log a learner mistake. Re-record/regenerate or replace the asset.

### Learner requests transcript before attempting

In practice modes, allow it only by converting the activity to assisted learning; do not claim clean Listening evidence. In P4 it remains unavailable until measurement ends.

### Learner has no audio-capable environment today

The coach should select another high-value task or a non-listening repair/review. Reading a transcript is not a substitute for direct Listening evidence.

### Technical playback interruption

If enough of the item was missed to change fairness, invalidate or qualify the attempt and offer a fresh valid attempt. Never score an infrastructure failure as inability.

### Background noise or headphone differences

Record relevant technical/context flags when they materially affect validity. Do not make normal learner-device noise an excuse for false precision. Later accessibility/device shaping decides formal requirements.

### Strong P3 performance but no P4 evidence

The coach can say Listening is strong in independent training but should still prioritize target-condition evidence before strong readiness claims.

### Sparse human/native audio bank

Do not block learning. Use reviewed cached TTS broadly, but keep readiness confidence lower until the learner has succeeded across enough validated target-like voice/audio variety.

### Corpus lacks reliable Listening frequency/difficulty evidence

Use the verified TELC blueprint, reviewed B1 content principles, and conservative hand-authored difficulty metadata. Do not invent claims about “common” topics or acoustic patterns. Re-rank/retag once Corpus evidence exists.

---

## 6. Relationship to Other Bestehen Stages

- **Stage 03 — Initial Diagnostic:** uses short Listening probes; Stage 11 supplies the complete interpretation and repair model.
- **Stage 04 — Learner Model:** stores direct Listening capabilities, playback/speed conditions, confidence, freshness, and evidence provenance.
- **Stage 05 — Mistake Memory:** receives the diagnosed root cause and recurrence/repair lifecycle; Stage 11 refines what listening causes look like.
- **Stage 06 — Daily Coaching:** chooses whether Listening, a listening repair, a realism step, or a target-condition probe is today's highest-value work.
- **Stage 07 — Core Learning Loop:** Stage 11 is the modality-specific implementation of Attempt → Diagnose → Repair → Retry → Remember.
- **Stage 08 — A1→B1 Progression:** supplies the five rungs and assistance semantics; Stage 11 fixes the listening-specific speed/replay/transcript behavior inside them.
- **Stage 14 — Review:** must schedule retained listening distinctions such as numbers, negation, paraphrase, and connected-speech recognition without turning review into a separate flashcard product.
- **Stage 15 — TELC Readiness:** must consume H1/H2/H3 evidence with playback, natural-speed, assistance, recency, validity, and confidence attached.
- **Stage 16 — Mock Exams:** must preserve exact current playback rules and defer coaching until the measured Listening block ends.
- **Stage 17 — Ready to Book:** should require adequate recent target-like Listening evidence inside the written component, without relying only on synthetic-voice success.
- **Stage 21 — Content Strategy:** owns large-scale audio generation/QA policy and must preserve Stage 11's validity and rights gates.
- **Stage 22 — Corpus → App Contract:** should expose target/task patterns, audio difficulty/relevance, speaker/acoustic metadata, distractor patterns, and rights/provenance needed by this model.
- **Stage 25 — Accessibility:** decides accommodations and how they affect target-condition comparability; Stage 11 only preserves the evidence condition.
- **Stage 26 — Analytics:** should recalibrate speed/difficulty bands, diagnosis accuracy, repair transfer, and synthetic-vs-human evidence behavior from real usage.

---

## 7. Cost Notes

Listening has meaningful content-generation cost, but it does **not** need meaningful per-attempt recurring AI cost.

### Preferred low-cost launch design

1. Write or generate original scripts in batches.
2. Review scripts and answer keys before learner use.
3. Batch-generate TTS audio in several vetted voices.
4. Human-audit pronunciation-sensitive fields and a sample of ordinary assets.
5. Cache approved audio permanently and reuse it.
6. Score objective answers deterministically.
7. Diagnose common causes from reviewed metadata plus compact deterministic contrasts.
8. Use transcript and pre-authored repair snippets rather than generating a new explanation for every miss.
9. Create a small native-human benchmark/P4 set instead of human-recording the full catalog.

### Cost/quality ladder

| Tier | Capability | Use when | Trade-off |
|---|---|---|---|
| **A — Lowest cost** | Reviewed cached commodity/neural TTS + deterministic scoring/repair | P0–P2 broad practice, much of P3 | Cheapest scalable bank; synthetic artifacts require QA |
| **B — Recommended launch quality** | Better multi-voice TTS + stronger human audit + small native benchmark set | Normal P3 and readiness preparation | Bounded one-time cost with much better generalization confidence |
| **C — Higher-quality upgrade** | Premium expressive/multi-speaker TTS, more native recording, professional audio QA | When usage or outcome data shows synthetic audio is limiting readiness transfer | Better naturalness, higher asset creation cost |
| **D — Not justified initially** | Live per-attempt TTS/model-generated adaptive audio and explanation | Only if later evidence proves static/cached assets cannot deliver enough personalization | Highest recurring cost, lower reproducibility, more QA risk |

### Premium invocation rule

A premium audio/model operation is justified only when it materially improves one of:

- naturalness or speaker behavior needed for target calibration;
- pronunciation reliability for an otherwise valuable asset;
- dialogue/prosody realism that cheaper audio cannot achieve;
- offline creation/QA of a reusable asset that will serve many learner attempts;
- a rare high-value ambiguity/content review that cannot be handled deterministically.

It is **not** justified merely because the product wants to feel “AI-powered.”

### Cost boundary for readiness quality

Do not degrade readiness by making every P4 asset cheap synthetic speech. The low-cost compromise is **broad cached TTS practice + a small reusable high-quality benchmark pool**, not “synthetic only forever” and not “human-record everything.”

---

## 8. Decisions Made

1. TELC B1 Listening is shaped as three target families: H1 global, H2 detail, H3 selective.
2. Lower-difficulty variants preserve the target listening behavior while changing linguistic/acoustic/reasoning load.
3. Reference audio and learner-playable audio are separate roles governed by rights metadata.
4. Reviewed, pre-generated, cached TTS is the default broad practice source.
5. Strong readiness must include voice/audio variety and must not rely only on one synthetic voice system.
6. A small native-human or equivalently audited benchmark bank is the recommended low-cost P4/readiness upgrade.
7. Speed progresses from careful-natural toward target-natural and remains a separate evidence condition.
8. Replay decreases by rung and exactly matches the current target rule in P4.
9. Transcript is post-attempt diagnosis/repair support, not normal in-attempt help.
10. Vocabulary preview is small, targeted, and removed by P4.
11. Listening diagnosis explicitly distinguishes vocabulary, numbers/dates/times, speed/connected speech, distractors/corrections, negation, inference, attention/position loss, speaker attribution, and unresolved causes.
12. Targeted repair addresses the diagnosed cause and must transfer to fresh audio.
13. Audio difficulty is a multidimensional profile, initially expressed with ordinal bands rather than invented precision.
14. P4 is a deferred-feedback measured block with exact blueprint/playback conditions and no learning assistance.
15. Listening readiness evidence must preserve task family, speed, replay, assistance, audio validity, voice diversity, recency, and target realism.
16. Normal learner attempts should incur no premium AI/TTS cost; expensive generation is offline, batched, cached, and selectively upgraded.

---

## 9. Open Questions / Deferred Decisions

### No owner-blocking product question

Stage 11 requires no owner decision to proceed. The recommended defaults are suitable for the stated personal-project constraints.

### Deferred to later shaping/validation

- Exact readiness weights, minimum H1/H2/H3 evidence, pass-probability calibration, and written-component aggregation — **Stage 15**.
- Full mock cadence, pause/resume policy, and exact post-mock analysis — **Stage 16**.
- The amount and production method of the initial native-human benchmark pool — content planning/implementation, constrained here by the product policy.
- Exact TTS vendor/model, audio codec, cache/storage technology, generation pipeline, and CDN/offline behavior — architecture/implementation.
- Empirical word-per-minute or acoustic-complexity thresholds for difficulty — **Stage 26 calibration**.
- Accessibility accommodations and how accommodated evidence compares with standard target conditions — **Stage 25**.
- Whether mild accent/regional variation becomes a planned training dimension beyond target-calibrated variety — defer until Corpus/learner evidence shows value; do not add complexity at launch merely for realism theater.

---

## 10. Definition of Done Check

- [x] TELC B1 Listening task families are mapped and treated as versioned target knowledge.
- [x] Lower-difficulty H1/H2/H3 variants are defined through P0–P4.
- [x] Audio source strategy separates reference, generated, human/native, premium, and fallback roles.
- [x] Generated versus human/native-recorded policy is defined.
- [x] Speech-speed progression is defined with evidence guardrails.
- [x] Replay rules are defined by stage, including exact P4 behavior.
- [x] Transcript availability is defined.
- [x] Pre-listening vocabulary assistance is defined.
- [x] Unknown vocabulary diagnosis is defined.
- [x] Numbers/dates/times diagnosis is defined.
- [x] Speed/connected-speech diagnosis is defined.
- [x] Distractor/correction diagnosis is defined.
- [x] Missed negation/restriction diagnosis is defined.
- [x] Inference diagnosis is defined.
- [x] Attention/continuity failures are also defined as an additional Stage 11 requirement.
- [x] Targeted Listening repair and fresh audio retry are defined.
- [x] Audio difficulty dimensions and initial scoring/banding are defined.
- [x] Exam-realistic Listening mode is defined.
- [x] Readiness evidence requirements are defined without prematurely choosing the final readiness formula.
- [x] Low-cost default and higher-cost upgrade path are documented.
- [x] No product-shaping item remains blocked on an owner question.

**Stage 11 is complete when the live App checklist reflects these decisions.**
