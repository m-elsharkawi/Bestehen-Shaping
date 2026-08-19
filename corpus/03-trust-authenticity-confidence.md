# Bestehen / Corpus — Stage 03: Trust, Authenticity, and Confidence

> **Status:** Authoritative Stage 03 product-shaping decision  
> **Product:** Bestehen / Corpus  
> **Initial domain:** German A2–B1 exam and exam-style material  
> **Primary downstream customer:** Bestehen / App  
> **Core principle:** Broad evidence is useful only when the strength, origin, uncertainty, and allowed downstream influence of that evidence remain explicit

## 1. Purpose and Scope

This stage defines how Bestehen / Corpus decides **how much to trust exam material as evidence** without excluding useful unofficial material or pretending that all accepted material is equally reliable.

The model must solve several related but distinct questions:

- Is the material genuinely official, clearly third-party, merely claimed to be official, or of uncertain origin?
- How strongly should Corpus rely on it as evidence of A2/B1 exam behavior?
- Which parts of the material are trustworthy if a document is only partially sound?
- Can it influence aggregate analytics, difficulty, App learning priorities, or exercise generation?
- Is it reliable enough to be shown directly to a learner if rights later permit that use?
- What happens when answer keys conflict, the exam is malformed, the claimed origin looks fake, or new evidence changes the conclusion?

The model deliberately **does not decide usage rights**. A document can be highly authentic but legally/reference-only, or freely reusable but weak exam evidence. Stage 04 defines rights and usage independently.

This is product shaping, not implementation architecture. It defines the information, states, decision rules, thresholds, and operator behavior the product requires. It does not choose a database schema, classifier, model vendor, review UI, or storage mechanism.

### 1.1 Stage objective

**Bestehen / Corpus should preserve broad official and unofficial evidence while making every downstream use proportional to the evidence quality actually demonstrated, localizing uncertainty to the smallest affected unit, and never converting resemblance, popularity, or public availability into false certainty.**

### 1.2 Product invariants

1. **Authenticity, evidence confidence, and usage rights are different concepts.**
2. **Inclusion is not endorsement.** Material may be retained while having zero analytical influence.
3. **Confidence is contextual.** A document can be good evidence of task structure but poor evidence of correct answers.
4. **The most local relevant confidence wins for high-risk use.** A trusted document does not rescue a disputed item.
5. **Unknown remains unknown.** Missing evidence does not become a positive score merely because the rest looks plausible.
6. **Independent corroboration can increase confidence; mirrors cannot manufacture it.**
7. **A conflict is preserved, not silently averaged away.**
8. **Quarantine is reversible.** Suspected fake/malformed material may later be reclassified if better evidence appears.
9. **Confidence can move both up and down.** New evidence, corrections, conflicts, or provenance discoveries may change a tier.
10. **Rights always remain a separate downstream gate.** Even Tier A evidence may be reference-only.

---

## 2. Inputs / Existing Decisions

This stage preserves and extends the established baseline from the product overview, identity, Corpus Stage 01, Corpus Stage 02, and the live Corpus checklist.

### 2.1 Decisions inherited from Stage 01

`corpus/01-product-mission-and-boundaries.md` established that:

- Corpus is an exam-data and intelligence product whose primary customer is Bestehen / App.
- TELC B1 is the strongest target signal, while the corpus remains broader than TELC.
- Official and unofficial material may both contribute evidence.
- Authenticity/confidence and usage rights must remain independent.
- Corpus success requires explicit trust/provenance, not merely a large archive.
- Unknown confidence must remain unknown rather than being silently upgraded.
- Conclusions from low-confidence evidence must be limited or discounted.
- Conflicting answer keys must be preserved rather than silently resolved.
- Independent evidence, not mirror count, is the correct basis for frequency and corroboration.

### 2.2 Decisions inherited from Stage 02

`corpus/02-source-strategy.md` established that:

- source category/acquisition priority is **not** a confidence score;
- official providers, publishers, teachers/schools, repositories/archives, unofficial collections, forums/shared documents, and individual exercises are all potentially useful source classes;
- candidate, source observation, and underlying material are distinct concepts;
- mirrors and archive copies are separate observations but do not count as independent evidence by default;
- provenance corrections must not rewrite history;
- partial/incomplete material may remain useful;
- manual submissions are first-class but do not receive automatic trust;
- dead URLs do not erase provenance;
- discovery may be broad while downstream influence remains selective.

Stage 03 does not alter those decisions. It supplies the missing trust model they anticipated.

### 2.3 Relationship to the App identity

Bestehen / App is meant to be calm, evidence-driven, and transparent about uncertainty. Corpus therefore must not hand the App undifferentiated facts. Where Corpus intelligence materially affects what the learner studies, what difficulty the App assumes, or what answer it treats as correct, the supporting evidence quality must be strong enough to defend the decision.

---

## 3. Decisions and Rationale

### 3.1 Use a three-part trust model

**Decision:** Corpus represents trust through three independent concepts:

1. **Authenticity status** — what is currently known about the material's claimed origin and officiality.
2. **Evidence confidence** — how strongly Corpus should rely on this source/document/exam/task/item for analytical and product conclusions.
3. **Usage rights status** — what may legally/operationally be done with the original material, defined separately in Stage 04.

This separation is essential because “official” and “useful” are not synonyms.

Examples:

| Material | Authenticity status | Evidence confidence | Rights implication |
|---|---|---|---|
| Official TELC model test on a verified provider location | Verified official | Usually high, subject to local defects | Stage 04 decides reuse; high confidence does not grant redistribution rights |
| Teacher-authored B1 mock with excellent structure and a validated key | Verified third-party/mock | Can be high | May or may not be reusable depending on license/permission |
| PDF claiming to be a leaked “real TELC exam” with no provenance | Claimed official — unverified | Low/conditional until corroborated | Rights remain separately unknown/restricted |
| Openly licensed but poorly written worksheet | Verified third-party/mock | Low | Reusable rights would not make it trustworthy exam evidence |

### 3.2 Authenticity is categorical, not a synonym for the confidence score

**Decision:** The current authenticity status for an underlying document/exam should use the following product categories.

| Authenticity status | Meaning | Important rule |
|---|---|---|
| **Verified official** | The material is credibly established as material published/issued by the claimed exam provider or responsible authority | Officiality can anchor provider-specific facts, but local errors or outdated material can still reduce use-specific confidence |
| **Verified official-derived copy** | The material is a non-officially hosted copy that is credibly matched to verified official underlying material | The hosting source is not “official”; duplicate/mirror rules still prevent frequency inflation |
| **Verified third-party / mock** | Authorship/origin is reasonably established as non-official exam-prep material | Can still achieve strong evidence confidence for realistic patterns if quality and corroboration are high |
| **Claimed official — unverified** | The source claims official/real-exam origin, but Corpus cannot verify the claim | Never present the official claim as fact; confidence is bounded until provenance improves |
| **Origin uncertain** | Corpus cannot responsibly establish official or third-party origin | Preserve the uncertainty; the material may still be analytically useful at a bounded tier |
| **Suspected misrepresented / fake** | Evidence suggests the claimed origin or exam identity may be intentionally or materially false | Quarantine by default until review/reclassification |

**Authenticity rule:** Similarity to official material can increase evidence confidence but **cannot by itself convert a claim into “Verified official.”** Officiality requires provenance evidence, not visual resemblance or community repetition.

### 3.3 Confidence uses both dimensions and a simple tier

**Decision:** Evidence confidence is represented through:

- eight scored dimensions required by the Stage 03 checklist;
- a provisional normalized score from **0–100** for comparison and recalculation;
- an effective **A/B/C/D tier** for product decisions;
- explicit hard gates/caps for critical local problems;
- a review state explaining whether the tier is automatic/provisional, accepted, disputed, or quarantined.

The numeric score is an internal decision aid, not a claim of scientific precision. Downstream product rules should normally use tiers and use-specific gates rather than pretending that, for example, 78 is meaningfully different from 79.

### 3.4 Why a hybrid score + tier is preferred

Three alternatives were considered conceptually:

- **Category-only tiers:** simple, but too coarse to explain why an unofficial mock is trusted or why one official document has a bad local answer key.
- **Pure numeric score:** flexible, but encourages false precision and makes downstream rules harder to reason about.
- **Hybrid dimensions + score + tier:** preserves explainability, allows recalculation when evidence changes, and still gives later systems a small set of stable decision bands.

**Recommended default:** use the hybrid model.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Confidence dimensions

Each applicable dimension is rated on a **0–4 evidence scale**. A value can also be **Unknown** or **Not applicable**.

- **0** — evidence actively contradicts trust on this dimension.
- **1** — weak / serious concern.
- **2** — mixed / plausible but uncertain.
- **3** — strong.
- **4** — very strong / independently defensible.
- **Unknown** — insufficient evidence; it contributes no positive points but remains distinguishable from a demonstrated failure.
- **Not applicable** — the dimension genuinely does not apply and is removed from the denominator. This must not be used merely to avoid a low score.

For example, “answer-key presence” is **Not applicable** for a speaking prompt that appropriately has no single correct answer. It is **0/Unknown**, not N/A, for an objective reading test whose expected key is simply missing.

### 4.1.1 Recommended initial weights

The initial weights are intentionally simple and should be recalibrated against the Stage 16 benchmark corpus rather than treated as permanent truth.

| Dimension | Weight | What it measures | High-confidence evidence | Low-confidence evidence |
|---|---:|---|---|---|
| **Provider reputation / provenance quality** | **20%** | How credible and traceable the claimed provider/author/origin is | Verified official provenance; established publisher/institution/author; strong lineage | Anonymous origin; misleading attribution; unverifiable “real exam” claims |
| **Similarity to known exam structure** | **15%** | Whether sections, task forms, instructions, sequencing, timing/scoring context, and provider conventions resemble trusted A2/B1 material | Coherent match to known provider/level structure with explainable variations | Important structural contradictions or implausible exam format |
| **Language quality** | **10%** | Whether German usage, register, instructions, distractors, and level feel linguistically credible for the claimed exam context | Natural, accurate, level-appropriate language | Frequent errors, unnatural wording, incoherence, machine-like or non-exam language |
| **Answer-key presence** | **5%** | Whether expected objective answer material exists and is linkable to the correct items | Complete or intentionally scoped key clearly mapped to items | Missing, fragmentary, unlabeled, or detached key where one should exist |
| **Answer-key consistency** | **15%** | Whether the supplied/corroborated answers are internally and externally plausible | Answers fit the question/text/audio and agree with strong corroborating evidence | Contradictions, impossible answers, repeated mismatches, unresolved competing keys |
| **Similarity to trusted material** | **10%** | Whether the material's patterns, instructions, task behavior, difficulty cues, and conventions align with trusted examples | Strong alignment with known credible exam patterns without needing to be identical | Material behaves unlike trusted A2/B1 examples or conflicts with known conventions |
| **Internal structural consistency** | **10%** | Whether numbering, sections, page/task relationships, assets, instructions, answer references, and claimed completeness make sense together | Coherent structure with only minor harmless defects | Missing/reordered parts, impossible references, inconsistent numbering, tampering indicators |
| **Corroboration across independent sources** | **15%** | Whether independent evidence supports the material's origin, answer, structure, or claim | Multiple genuinely independent, credible confirmations; authoritative confirmation where applicable | Only mirrors/reposts, circular citations, or no independent support |

Total when all dimensions apply: **100%**.

### 4.1.2 Score calculation

The provisional score is the weighted percentage of demonstrated evidence:

**Confidence score = weighted achieved points / weighted maximum for applicable dimensions × 100.**

Rules:

- **Not applicable** dimensions are removed from both numerator and denominator.
- **Unknown** dimensions remain in the denominator and contribute no positive points until evidence exists. This keeps new/opaque material conservatively scored while preserving “unknown” as distinct metadata.
- Inherited context may seed a lower-level dimension, but direct local evidence should replace inheritance when available.
- A reviewer may apply a documented **tier cap/override** where hard evidence warrants it; the raw dimension score must remain visible rather than being silently edited to force the desired tier.

This model intentionally rewards unofficial material that demonstrates quality and corroboration while preventing opaque material from earning high confidence merely because it looks polished.

## 4.2 Confidence tiers

| Tier | Initial score band | Product meaning | Default downstream posture |
|---|---:|---|---|
| **A — Anchor** | **85–100** | Strongly defensible evidence with no unresolved critical integrity issue | Can anchor analytics and product conclusions, subject to relevance, deduplication, local gates, and rights |
| **B — Trusted** | **70–84** | Reliable evidence suitable for most analytical uses and supporting product decisions | Can influence analytics, difficulty, learning priorities, and generation when additional use-specific gates are met |
| **C — Conditional** | **50–69** | Useful evidence with meaningful uncertainty or incompleteness | May contribute bounded/supporting analytics; cannot be the sole basis for learner-critical conclusions |
| **D — Weak** | **0–49** | Insufficiently trustworthy for normal analytical influence | Retain for provenance, discovery, comparison, or review; zero published aggregate influence by default |

**Quarantine is a review/state flag, not a fifth score tier.** A quarantined record has zero downstream influence regardless of its provisional numeric score until the issue is resolved.

### 4.2.1 Tier A requires established origin quality

A record cannot become Tier A while its material origin is still **Claimed official — unverified**, **Origin uncertain**, or **Suspected misrepresented/fake**. Strong content quality may make such material useful Tier B evidence, but Anchor status requires defensible provenance/origin as well as a high score.

A verified third-party mock **can** be Tier A if authorship is established and the material is exceptionally strong, consistent, and independently corroborated. Tier A means “anchor-quality evidence,” not “official-only.”

## 4.3 Critical dimension gates and caps

The overall tier is not a permission slip for every use. Critical local issues override the aggregate score.

| Condition | Required product behavior |
|---|---|
| **Suspected fake/tampered/misrepresented exam identity** | Quarantine the affected document/exam; zero downstream influence until review |
| **Answer-key consistency 0–1 for an objective item/task** | Block correctness-dependent analytics, answer-grounded generation, learner scoring reference, and direct surfacing of that answer; affected item/task cannot be treated above C for correctness use until resolved |
| **Expected answer key missing** | The task may remain useful for structure/topic/language evidence, but cannot ground correctness-dependent use merely because the parent document is trusted |
| **Language quality 0–1 at task/item level** | Prevent the affected content from grounding target-language generation/difficulty conclusions; local task/item effective tier is capped at C for language-content use |
| **Internal structural consistency 0–1 at exam/document level** | Whole-exam structure conclusions are capped at C or quarantined depending on severity; intact locally verifiable tasks may still earn higher local confidence |
| **Claimed official but unverified** | Never label as verified official; Tier A unavailable until provenance is established |
| **Unresolved high-impact conflict between strong sources** | Mark the affected claim/item disputed and remove it from high-risk use until resolved; do not select the numerically higher score automatically |

These gates let Corpus salvage valid parts of imperfect material rather than either trusting or discarding a whole document as one unit.

## 4.4 Levels at which confidence is stored

**Decision:** Confidence must exist at **source, document, exam/test-set, task, and item/question levels**. The exact physical schema is a Stage 05/architecture decision, but the product needs all five levels because uncertainty appears at different scopes.

| Level | What confidence answers | Typical evidence/problems |
|---|---|---|
| **Source** | How much should we trust this source observation/source family as a provenance signal? | Official domain, established publisher, anonymous upload, history of misleading claims, archive/mirror relationship |
| **Document** | How trustworthy is this concrete file/page/version as a coherent artifact? | Tampering, incomplete scans, missing pages, version mismatch, claimed authorship, damaged extraction-independent structure |
| **Exam / Test Set** | How strongly does this material represent the claimed exam/provider/level and whole-test structure? | Correct section composition, timing/scoring claims, complete mock vs mixed worksheet bundle |
| **Task** | How trustworthy is this task's instruction, passage/audio relation, task type, and local structure? | One malformed listening task inside an otherwise strong exam; unclear instructions; missing asset |
| **Item / Question** | How trustworthy is this exact question, choice set, answer/key relation, or scoring claim? | One wrong key, ambiguous distractor, OCR-corrupted choice, mismatched answer number |

### 4.4.1 Inheritance is a prior, not a ceiling

Lower levels may inherit context from their parents as a starting point, but confidence must be allowed to diverge when local evidence exists.

Examples:

- A Tier A official document may contain one disputed item that is locally C/Disputed.
- A low-reputation mirror source may host a byte-for-byte verified official document whose underlying document/exam confidence is A while the source-host confidence remains lower.
- An incomplete C-level exam can contain several intact B-level tasks suitable for limited analytics.

**Rule:** high-risk downstream use should consult the **most specific relevant confidence** plus any critical parent integrity flags. No parent tier may silently overwrite a local conflict.

### 4.4.2 Optional finer-grained overrides

Section, answer, asset, transcript, or scoring-rule confidence may later be stored explicitly when Stage 05/08 shows they need first-class entities. Until then, the product requirement is that they can carry local overrides through the nearest task/item/document context. This is a data-model detail, not a reason to defer the five mandatory confidence levels above.

## 4.5 Default influence weighting inside eligible analytics

For analytical uses that allow multiple tiers, the initial conservative default is:

| Tier | Default evidence weight inside eligible aggregate analytics |
|---|---:|
| **A** | **1.00** |
| **B** | **0.70** |
| **C** | **0.25** |
| **D** | **0.00** |
| **Quarantined** | **0.00** |

These are **initial product defaults**, not statistically calibrated constants. Stage 11 and the Stage 16 benchmark should test whether they cause distortion and adjust them if evidence supports a better model.

Crucially, this weighting is applied **after** duplicate/independence treatment. Ten mirrors of one C-tier mock must not become 10 × 0.25 evidence.

## 4.6 Thresholds by downstream use

Confidence gates differ because the cost of being wrong differs.

| Downstream use | Minimum confidence | Additional product rules |
|---|---|---|
| **Corpus inventory / provenance search** | Any tier, including D and quarantined | Retention is allowed for traceability; quarantine must remain visibly non-active |
| **Exploratory internal analytics** | C+ | C is down-weighted; D/quarantine cannot affect aggregate conclusions |
| **Published/decision-grade corpus analytics** | C+ contributions, but conclusions must be materially supported by A/B evidence | Never let a conclusion be driven primarily by C evidence; show evidence quality/uncertainty where material |
| **Difficulty-model influence / calibration** | **B+** | C may receive a provisional difficulty annotation for exploration but must not calibrate production difficulty aggregates; local language/structure integrity gates must pass |
| **Influence on App learning priorities** | **B+ as primary evidence** | C may only support an already corroborated signal. Relative priority/frequency changes require independent A/B evidence; one verified official TELC source may establish a required TELC format/skill, but not prevalence by itself |
| **Exercise-generation grounding** | **B+** | The grounding task/item must have no unresolved correctness/structure conflict relevant to what is being generated. C may contribute aggregate pattern hints only when corroborated by A/B evidence; it cannot be the sole semantic/answer/scoring ground truth |
| **Direct learner exposure of source-derived content** | **B+ at the most local relevant level** | Also requires the relevant Stage 04 rights status, no unresolved key/structure dispute, and pedagogical suitability. Confidence never overrides rights |
| **Direct learner exposure where a specific objective answer is treated as correct** | **B+ item confidence plus answer-key consistency ≥3/4** | If the answer remains disputed, do not expose it as authoritative even if the parent exam is A |

### 4.6.1 Learning-priority corroboration rule

Because Bestehen / App uses Corpus to decide what deserves learner time, a noisy unofficial collection must not distort priorities.

Initial rule:

- **Existence/requirement:** one verified official Tier A TELC specification/model source can establish that a provider-specific format, section, or requirement exists.
- **Relative frequency/priority:** changing how strongly the App prioritizes a pattern should normally require **at least two independent A/B underlying materials**, with at least one TELC-relevant evidence source for TELC-specific claims.
- **Cross-provider generic B1 priority:** multiple independent A/B sources across established providers can establish a broad B1 pattern even if it is not specifically TELC-heavy.
- **Tier C:** can corroborate or broaden examples but cannot create a high-priority signal by itself.

Stage 07 will add TELC relevance/provider weighting; Stage 11 will define analytics formulas. Stage 03 defines only the confidence floor.

## 4.7 Manual review and escalation flow

**Decision:** Corpus uses selective manual review for **uncertain but valuable** material rather than reviewing every record or automatically discarding everything below B.

### 4.7.1 Review states

The product must support at least these conceptual states:

| Review state | Meaning | Downstream posture |
|---|---|---|
| **Unreviewed / provisional** | Automated/initial assessment exists but no manual decision was needed or completed | Use only according to tier/gates; no implication of human endorsement |
| **Accepted** | Evidence is considered fit for the allowed uses at its effective tier | Normal tier-based influence |
| **Accepted with restrictions** | Material is useful, but one or more uses/regions are intentionally blocked | Only explicitly permitted uses proceed |
| **Review required** | A valuable uncertainty needs operator resolution | Conservative influence; high-risk uses blocked |
| **Disputed** | Strong evidence conflicts on a material claim such as an answer or provenance | Affected claim/item blocked from high-risk use |
| **Quarantined** | Serious fake/tamper/malformed/integrity concern | Zero downstream influence until resolved |
| **Rejected as evidence** | Material is retained only for audit/provenance or discarded according to later retention rules | Zero analytical/product influence |

### 4.7.2 What triggers manual review

Manual review is required or strongly preferred when any of the following is true:

1. A source claims to be **official/real exam material** but provenance is unverified and the claim would materially change interpretation.
2. Two plausible answer keys conflict for the same item.
3. A high-value TELC source lands near a decision boundary (especially C/B) and resolving it would materially affect analytics, learning priority, or generation grounding.
4. A unique or underrepresented source is low-confidence but could fill an important provider/section/format gap.
5. Structural anomalies suggest pages/tasks may be missing, reordered, combined from different exams, or tampered with.
6. Language quality or answer consistency is poor enough to contradict the claimed provider/level.
7. A source appears to be a fake or misrepresented “real exam,” but could still be salvageable as a third-party mock if reclassified.
8. A correction would change direct learner exposure or any answer treated as correct.
9. Strong independent sources disagree on provider identity, exam edition, scoring rule, or answer.
10. An automated confidence result conflicts with obvious high-quality provenance evidence and a simple manual check can resolve the issue cheaply.

### 4.7.3 Review priority

Manual-review effort should be ordered by **expected product impact**, not by queue age alone:

1. **Highest priority:** disputes that could make the App teach a wrong answer, use the wrong TELC format/requirement, or expose questionable content directly.
2. **High priority:** unique/high-value TELC or weak-coverage evidence whose resolution could materially change analytics or generation grounding.
3. **Medium priority:** C-tier material that would become useful if a narrow uncertainty is resolved.
4. **Low priority:** D-tier material that duplicates already strong coverage or has little expected information gain.

This prevents a personal project from spending human time proving that low-value noise is indeed low-value.

### 4.7.4 Allowed review outcomes

A reviewer may:

- accept the current tier;
- change one or more dimension assessments with rationale/evidence;
- apply a documented tier cap or effective-tier override;
- reclassify authenticity (for example, “claimed official” → “verified third-party/mock”);
- restrict only the affected task/item while leaving the rest active;
- resolve a disputed answer and record why;
- keep the conflict unresolved;
- quarantine the record;
- reject it as evidence;
- request/await more corroboration.

Every manual decision that changes effective trust must remain auditable. The product should preserve **what changed, why, and which evidence justified the change**, even if later architecture chooses the exact audit representation.

## 4.8 Conflicting answer keys

**Decision:** Conflicting answer keys are treated as a first-class dispute at the smallest affected scope, never as an invitation to silently choose the most common answer online.

### 4.8.1 Immediate behavior

When conflicting plausible keys are detected:

1. Preserve each candidate answer/key and its provenance.
2. Mark the affected item/task **Disputed**.
3. Exclude the affected answer from correctness-dependent analytics, difficulty calibration based on correctness, answer-grounded generation, learner scoring ground truth, and direct learner exposure as “the correct answer.”
4. Keep unaffected parts of the document/exam active if their confidence remains sufficient.
5. Do not let mirror count decide the winner.

### 4.8.2 Resolution evidence order

Review should prefer evidence in roughly this order, while still checking for edition/version mismatches:

1. explicit correction/erratum or current answer published by the responsible official provider for the same edition/item;
2. matching official answer material for the exact document/version;
3. another independent high-confidence authoritative/reputable source that demonstrably refers to the same item;
4. strong semantic validation against the source passage/audio plus independent corroboration;
5. consensus among genuinely independent, high-confidence secondary sources.

A majority of mirrors, reposts, or answer websites derived from one upstream key is **not** independent consensus.

### 4.8.3 Unresolved conflict

If no responsible resolution is possible, the item remains disputed indefinitely. It may still contribute to non-correctness uses such as topic, vocabulary, task-shape, or language-pattern analysis if those aspects are independently sound, but it must not be used as answer truth.

## 4.9 Likely fake, misrepresented, or malformed material

### 4.9.1 Suspected fake/misrepresented exam

**Decision:** Material suspected of falsely claiming official/real-exam status enters **Quarantine** with zero downstream influence until reviewed.

Signals can include:

- impossible or highly inconsistent provider branding/structure;
- claims that contradict known provider formats or dates;
- content stitched from unrelated sources while presented as one official exam;
- implausible answer/scoring patterns;
- repeated language errors inconsistent with the claimed provenance;
- deceptive provenance claims that cannot be reconciled with source history;
- evidence of tampering that changes meaning or answers.

A quarantine decision concerns the **claimed identity/integrity**, not necessarily the pedagogical usefulness of every sentence.

If review concludes that the content is a legitimate third-party mock falsely or mistakenly labeled as official, it may be reclassified as **Verified third-party/mock**, rescored, and admitted at the tier its actual quality supports. Corpus should preserve the provenance correction rather than permanently discarding useful exam-style evidence solely because the initial label was wrong.

### 4.9.2 Malformed or incomplete exam

Malformed material is handled proportionally:

- a missing answer key blocks answer-based use but may not block structure/content analysis;
- a missing page lowers document/exam structural confidence while intact tasks can remain useful;
- one broken item should be quarantined/restricted locally rather than invalidating the whole test;
- systematic incoherence, widespread missing dependencies, or evidence that multiple exams were incorrectly merged can quarantine the whole exam representation until split/repaired;
- Corpus must never invent missing pages, answers, or scoring rules merely to raise confidence.

The later canonical model and ingestion pipeline determine how partial records are represented. Stage 03 requires that confidence and review states can localize the damage.

## 4.10 How confidence changes over time

**Decision:** Confidence is recalculated when material evidence changes. It is not a permanent label assigned at ingestion.

Confidence can increase when:

- a claimed origin is verified;
- an official original corresponding to a mirror is found;
- an answer key is independently confirmed;
- multiple independent sources corroborate the same structure/answer/provenance claim;
- missing related assets are found and linked;
- a malformed-looking document is shown to be a legitimate edition/version difference;
- manual review resolves a narrow ambiguity.

Confidence can decrease when:

- an official correction contradicts the stored answer;
- a source is discovered to have misrepresented authorship/provider;
- two previously assumed independent sources are shown to be mirrors/derivatives;
- a document is found to combine mismatched editions;
- structural or language defects are discovered;
- a previously trusted key fails validation against the actual passage/audio;
- later provenance evidence reveals tampering.

**Audit rule:** recalculation must preserve prior decision history and reason for change. Downstream data derived from a materially changed confidence state must be eligible for re-evaluation in later pipeline/contract stages.

## 4.11 Independent corroboration and duplicate evidence

Corroboration is valuable only when it is genuinely independent for the claim being evaluated.

### 4.11.1 Corroboration dimension rubric

| Rating | Evidence pattern |
|---:|---|
| **0** | Contradicted by stronger independent evidence, or apparent support is shown to be circular/misleading |
| **1** | Only the originating source or obvious mirrors/reposts repeat the claim |
| **2** | One plausibly independent but limited/medium-confidence source supports the claim |
| **3** | At least two independent credible sources/materials support the claim, or one especially strong independent confirmation exists |
| **4** | Authoritative confirmation or multiple independent high-confidence confirmations strongly support the claim |

The exact independence-detection mechanics are deferred to Stage 09, but Stage 03 locks the product meaning: **a mirror is not corroboration merely because it has a different URL or domain**.

### 4.11.2 Claim-specific independence

Independence is evaluated against the claim being supported:

- Two mirrors of the same official PDF can corroborate historical availability/provenance context, but not create two independent examples of an exam pattern.
- Two independently authored mocks using the same task pattern are independent pattern evidence even if both imitate TELC.
- A forum answer copied from the same published key is not independent answer corroboration.
- A teacher's worked explanation that derives the answer from the passage may be independent semantic corroboration even if the original question is the same.

### 4.11.3 Corroboration cannot erase local contradictions

A large amount of weak agreement must not overpower one direct, authoritative contradiction without review. If a current official erratum changes an answer, twenty older mirrors of the wrong key do not win by count.

## 4.12 Confidence and duplication/frequency are separate

Confidence determines **how much to trust a unit of evidence**. Deduplication determines **how many independent evidence units exist**. Both are required before frequency analytics are defensible.

A single Tier A official exam mirrored 30 times still counts as one underlying exam for prevalence. Conversely, five independently authored Tier B exams can provide stronger frequency evidence than one Tier A example even though each individual source is less authoritative.

Stage 09 will define duplicate/derivative clusters. Stage 11 will define aggregate analytics. Stage 03 requires those later stages to consume confidence without multiplying it through mirrors.

## 4.13 Confidence does not automatically decay with age

Old evidence does not become untrustworthy merely because it is old. Confidence represents trust in what the material **is and says**. Current TELC relevance, format currency, and historical weighting are separate concerns for Stage 07/11.

An old official exam can remain Tier A as authentic evidence while receiving lower current-target relevance if the format changed.

## 4.14 Confidence must be explainable

For any source/document/exam/task/item that materially affects a product decision, Corpus should be able to answer:

- what its current authenticity status is;
- what confidence tier/score it has;
- which dimensions drove that result;
- which dimensions are unknown or not applicable;
- whether there are local caps, disputes, restrictions, or quarantine flags;
- what corroborating evidence exists;
- whether duplicates/mirrors were neutralized;
- whether a reviewer changed the effective result and why.

This explainability is a product requirement for later operations and App-contract design, not a requirement to expose raw internals to learners.

---

## 5. Edge Cases / Failure or Uncertainty Handling

### 5.1 Official provider source with a typo in one answer key

Keep the document/exam authenticity as Verified official and likely high-confidence overall. Mark only the affected item/key disputed or lower-confidence. If an official erratum exists, resolve against the corrected version and preserve the earlier conflict history.

**Do not downgrade the entire provider/source because one item is wrong.**

### 5.2 Excellent teacher-created mock

If authorship is established, structure/language/key quality are strong, and independent evidence supports its exam realism, it can reach Tier A or B despite being explicitly non-official. Its authenticity status remains Verified third-party/mock.

### 5.3 Anonymous PDF that exactly matches an official model test

The anonymous hosting source may remain low-confidence, but the underlying document can become Verified official-derived copy once a trustworthy match to the official material is established. It remains one exam evidence unit for frequency purposes.

### 5.4 Anonymous “real exam 2026” PDF that looks realistic but has no provenance

Mark authenticity as Claimed official — unverified. It may score into C/B as realistic exam-style evidence if quality is strong, but it cannot be Tier A or be presented as official. If fake/misrepresentation signals appear, quarantine it.

### 5.5 Objective test has no key

Answer-key presence is low/unknown rather than N/A. The test may contribute to task-shape, language, vocabulary, topic, and perhaps provisional difficulty analysis, but it cannot ground correct-answer behavior until the key is validated.

### 5.6 Speaking/writing prompt has no single answer key

Answer-key presence/consistency can be N/A where a single correct answer is genuinely inappropriate. Other evidence such as official rubric/scoring guidance may later be represented through scoring-rule confidence. Do not penalize productive tasks for lacking an objective key they should not have.

### 5.7 Two answer keys disagree because they refer to different editions

Do not treat the disagreement as a semantic conflict once the edition/version distinction is verified. Split/link the versions correctly, recalculate local confidence, and preserve the resolution history.

### 5.8 Document is missing two pages but remaining tasks are intact

Lower document/exam structural confidence and mark incompleteness. Preserve higher local confidence for intact tasks if they can be independently validated. Do not use the fragment to infer full-exam section balance.

### 5.9 Community consensus supports an answer, official key contradicts it

Treat the item as disputed until version/error context is checked. Community vote count is not enough to override an official exact-version key. If the official key is demonstrably erroneous, the resolution must be documented rather than silently switching to consensus.

### 5.10 Many sites host the same unofficial mock

Do not increase corroboration or frequency merely because it is widely mirrored. If all copies trace to the same underlying material/key, they remain one evidence unit.

### 5.11 Two independent schools publish near-identical tasks

Stage 09 must determine whether one copied/derived from the other. Until independence is established, do not treat them as two confirmations. If genuinely independent, they can corroborate the task pattern while still remaining separate third-party mocks.

### 5.12 A source is reclassified from “official” to “teacher mock”

Correct the authenticity status, recalculate the provider/provenance dimension and effective tier, preserve audit history, and trigger downstream re-evaluation where the old official assumption materially influenced conclusions.

### 5.13 Strong source reputation but poor local German

The local language-quality signal wins for language-content use. A reputable publisher/provider prior cannot force a broken item into generation or direct exposure.

### 5.14 Low-confidence source contains one independently validated item

Allow the item to exceed its parent source/document tier when direct local evidence justifies it. Parent context remains visible, but the system should not throw away a valid item simply because the host/source is weak.

### 5.15 High-confidence material with unknown rights

It may influence confidence-eligible analytics and internal intelligence, but direct learner exposure remains blocked until Stage 04 rights allow it. Trust does not imply permission.

### 5.16 Quarantined material later proves to be legitimate

Remove quarantine only after the triggering concern is resolved, then rescore/reclassify from evidence. Preserve the fact that it was previously quarantined and why.

---

## 6. Relationship to Other Bestehen Stages

### Stage 04 — Rights and Usage Metadata

Stage 04 must remain independent. It should not use A/B confidence as a proxy for permission. Direct learner exposure requires **both** Stage 03 confidence gates and Stage 04 rights permission.

### Stage 05 — Canonical Exam Model

The canonical model must support confidence/authenticity at source, document, exam/test-set, task, and item levels, plus local disputes/review state and provenance links. It may choose finer entities for answer keys/assets/scoring rules.

### Stage 06 — Exam and Skill Taxonomy

Taxonomy assignments derived from lower-confidence material should carry enough confidence/provenance context that later analytics can discount or review them. Stage 03 does not define taxonomy accuracy.

### Stage 07 — Difficulty and TELC Relevance

Stage 07 must use B+ evidence as the default production difficulty-calibration input and must keep **confidence** separate from **TELC relevance**. A Tier A Goethe task may be strong evidence but less TELC-specific than a Tier B TELC-like task.

### Stage 08 — Ingestion Pipeline

Stage 08 should define where dimension assessments are produced, when review is triggered, how reprocessing works, and how extraction confidence interacts with evidence confidence. Successful parsing must never imply trust automatically.

### Stage 09 — Duplicate / Near-Duplicate Detection

Stage 09 must implement the independence rules assumed here. It determines whether observations are mirrors, derivatives, or independent materials before corroboration and frequency weights are applied.

### Stage 10 — Validation and QA

Stage 10 provides deeper structural, answer-key, language, extraction, and asset validation that can change Stage 03 dimensions. Validation results must be able to raise/lower confidence and open/resolve disputes.

### Stage 11 — Corpus Analytics

Stage 11 must apply tier weights after duplicate neutralization, protect decision-grade conclusions from C-tier dominance, and expose confidence/evidence quality for important outputs.

### Stage 12 — Corpus → App Contract

The App contract must distinguish trusted intelligence from raw/reference content and should carry enough confidence/restriction metadata that App cannot accidentally use a C/D/disputed source as learner-facing ground truth.

### Stage 13 — Corpus Operations

Operations must support review queues for uncertain high-value material, disputed answers, quarantined records, confidence explanations, provenance correction, and auditable manual overrides.

### Stage 14 — Cost, Scale, and Automation

Stage 14 should optimize confidence assessment through deterministic/cheap preprocessing, batching/caching, and selective premium/manual escalation rather than expensive model calls for every record.

### Stage 16 — Initial Benchmark Corpus

The benchmark must include official and imperfect unofficial sources and evaluate whether the model ranks them sensibly, localizes defects, handles conflicting keys, and avoids mirror-based confidence inflation. It should be used to recalibrate weights/tier thresholds before treating the numbers as stable.

### Stage 17 — Final Product Specification

The final PRD must preserve the separation among authenticity, confidence, rights, relevance, and duplicate independence.

---

## 7. Cost Notes

Confidence assessment has recurring processing cost during ingestion/reprocessing, but it should **not** create recurring per-learner cost.

### 7.1 Preferred low-cost default

Use the cheapest method that provides adequate evidence for each dimension:

- provenance/domain/source-registry checks before model calls;
- deterministic checks for key presence, numbering, structural completeness, linked assets, exact official-file matches, and known duplicate relationships where possible;
- cached source reputation/provenance context reused across documents from the same source;
- batch or local/cheap-model language/structure assessment when deterministic checks are insufficient;
- confidence recalculation only when relevant evidence changes;
- human review only for high-impact ambiguity rather than blanket review;
- premium model review only when it can cheaply resolve a high-value case that deterministic checks/cheap models cannot, especially TELC-critical structure/language/key disputes.

### 7.2 When higher spend is justified

Higher-cost review is justified when a decision can materially affect:

- an answer shown/scored as correct for learners;
- a TELC-specific learning priority;
- a high-value generation grounding set;
- a benchmark/gold-standard record;
- a unique source covering a major corpus gap;
- a disputed official/provider rule or scoring interpretation.

Do not spend premium-model or human-review effort proving low-value D-tier duplicates are poor evidence when stronger coverage already exists.

### 7.3 Cheaper fallback

If automated confidence assessment is uncertain, the cheapest acceptable fallback is to **keep the record at a conservative tier/review state with limited influence** until enough evidence or manual attention becomes worthwhile. The product does not need to resolve every ambiguity immediately.

No exact per-1,000-item cost is defined here; Stage 14 owns that target.

---

## 8. Decisions Made

1. Authenticity status, evidence confidence, and usage rights are three separate concepts.
2. Authenticity uses categorical states: Verified official, Verified official-derived copy, Verified third-party/mock, Claimed official — unverified, Origin uncertain, and Suspected misrepresented/fake.
3. Evidence confidence uses eight required dimensions, a provisional 0–100 roll-up, and A/B/C/D effective tiers.
4. The initial dimension weights are: provider/provenance 20%, exam-structure similarity 15%, language quality 10%, answer-key presence 5%, answer-key consistency 15%, similarity to trusted material 10%, internal structural consistency 10%, and independent corroboration 15%.
5. Unknown dimensions contribute no positive evidence but remain distinguishable from failed evidence; genuinely N/A dimensions are removed from the denominator.
6. Initial tiers are A 85–100, B 70–84, C 50–69, and D 0–49, with Quarantine as a separate zero-influence state.
7. Tier A requires established origin quality; unverified/uncertain origin cannot silently become Anchor-quality evidence.
8. Critical local defects override the aggregate tier for affected uses.
9. Confidence is required at source, document, exam/test-set, task, and item/question levels.
10. Parent confidence is a prior, not a ceiling or override; local evidence can raise or lower the most specific unit.
11. Initial aggregate weights are A 1.0, B 0.70, C 0.25, D 0, quarantine 0, applied only after duplicate/independence treatment.
12. C+ may contribute to bounded analytics; B+ is the default minimum for production difficulty influence, learning-priority evidence, generation grounding, and direct learner exposure.
13. Direct learner exposure additionally requires Stage 04 rights permission and no unresolved local key/structure dispute.
14. Learner-priority changes require independent A/B corroboration except that one verified official TELC source can establish an explicit provider requirement/format; prevalence still needs broader evidence.
15. Manual review is selective and impact-prioritized, with explicit Accepted, Restricted, Review Required, Disputed, Quarantined, and Rejected outcomes.
16. Conflicting answer keys are preserved at the smallest affected scope and blocked from correctness-dependent use until responsibly resolved.
17. Suspected fake/misrepresented exams are quarantined, but useful content may later be salvaged by reclassifying it as a third-party mock.
18. Malformed/incomplete material is handled proportionally; missing/broken parts do not automatically invalidate every intact task.
19. Confidence is recalculable and auditable as corroboration, provenance, corrections, conflicts, or duplicate relationships change.
20. Mirrors/reposts do not increase corroboration or frequency merely because they appear at multiple URLs.
21. Confidence does not automatically decay with age; current target relevance belongs to later TELC-relevance/analytics stages.
22. Confidence assessment should be precomputed/batched/cached and should not require per-learner model calls.

---

## 9. Open Questions / Deferred Decisions

### 9.1 Owner questions

**None.** The available project principles are sufficient to choose a conservative, low-cost confidence model without requiring an owner preference.

### 9.2 Deliberately deferred product-detail decisions

- exact rights classifications and downstream legal/use permissions — **Stage 04**;
- exact canonical entities/fields for confidence, answer keys, assets, and audit history — **Stage 05**;
- taxonomy-assignment confidence semantics — **Stage 06/10**;
- TELC relevance/provider weighting and numerical difficulty model — **Stage 07**;
- automated auto-accept thresholds, extraction-confidence mechanics, and reprocessing workflow — **Stage 08/10**;
- exact duplicate/derivative/independence thresholds — **Stage 09**;
- statistical formulas for aggregate confidence, prevalence, and decision-grade analytics — **Stage 11**;
- exact review UI, permissions, and operator tooling — **Stage 13**;
- concrete processing budgets, model tiers, and per-1,000-item cost target — **Stage 14**.

### 9.3 Calibration intentionally deferred, not unknown

The initial weights, score bands, and aggregate tier weights are **starting product defaults**. Stage 16 should test them against a manually annotated benchmark containing official, reputable unofficial, malformed, disputed-key, mirror, and suspected-fake cases.

Recalibrate when benchmark evidence shows a material misordering or unsafe threshold. Do not tune the score merely to make the distribution look balanced.

---

## 10. Definition of Done Check

- [x] A confidence model independent of usage rights is defined.
- [x] Provider reputation/provenance quality is defined as a confidence dimension.
- [x] Similarity to known exam structure is defined as a confidence dimension.
- [x] Language quality is defined as a confidence dimension.
- [x] Answer-key presence is defined as a confidence dimension with proper N/A handling.
- [x] Answer-key consistency is defined as a confidence dimension and local hard gate.
- [x] Similarity to trusted material is defined as a confidence dimension.
- [x] Internal structural consistency is defined as a confidence dimension.
- [x] Independent corroboration is defined as a confidence dimension.
- [x] A/B/C/D confidence tiers and provisional score bands are defined.
- [x] Confidence granularity is defined at source, document, exam, task, and item levels.
- [x] Thresholds for corpus analytics are defined.
- [x] Thresholds for difficulty estimation/model influence are defined.
- [x] Thresholds for App learning-priority influence are defined.
- [x] Thresholds for generation grounding are defined.
- [x] Thresholds for direct learner exposure are defined and explicitly remain rights-gated.
- [x] Manual-review states, triggers, priorities, and outcomes are defined.
- [x] Conflicting answer-key handling and resolution precedence are defined.
- [x] Quarantine behavior for likely fake/misrepresented material is defined.
- [x] Malformed/incomplete exam handling is defined proportionally.
- [x] Confidence increases/decreases under new evidence are defined.
- [x] Independent corroboration is distinguished from duplicate/mirror repetition.
- [x] Cost-sensitive defaults and premium/manual escalation conditions are defined.
- [x] No Stage 03 owner question remains unresolved.

**Stage 03 is product-complete when the live Corpus checklist matches the decisions above.**