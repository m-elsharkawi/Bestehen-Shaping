# Bestehen / Corpus — Stage 04: Rights and Usage Metadata

> **Status:** Authoritative Stage 04 product-shaping decision  
> **Product:** Bestehen / Corpus  
> **Initial domain:** German A2–B1 exam and exam-style material  
> **Primary downstream customer:** Bestehen / App  
> **Core principle:** Corpus may learn from broad material without assuming that public accessibility, authenticity, or analytical value grants permission to republish or adapt the original content

## 1. Purpose and Scope

This stage defines the **product-operational rights and usage model** for Bestehen / Corpus. Its purpose is to let Corpus preserve and learn from a broad A2/B1 exam evidence base while preventing downstream systems from treating every discovered PDF, web page, audio file, scan, answer key, or unofficial mock as content that can be redistributed to learners.

The model must answer five practical questions for every relevant source/material unit:

1. **What do we know about access and rights?**
2. **What evidence supports that conclusion?**
3. **What may Corpus do with the material internally?**
4. **What may Bestehen / App do with exact source content or source-derived material?**
5. **What must happen if rights later change, a source is removed, or a rightsholder asks for takedown?**

This stage is deliberately **not legal advice** and does not attempt to resolve jurisdiction-specific copyright, database-right, text-and-data-mining, contract, trademark, or licensing questions. It defines a conservative operational policy that later architecture can enforce. Where Bestehen would need to rely on a disputed legal interpretation rather than an explicit permission/license or low-risk internal policy, the product must escalate to legal review instead of pretending the product model itself answers the law.

### 1.1 Stage objective

**Bestehen / Corpus should classify rights independently from authenticity, preserve the evidence supporting each rights decision, default unclear material away from learner-facing reuse, allow safe abstract intelligence to remain useful, and make removal/reclassification enforceable across Corpus and App.**

### 1.2 Product invariants

1. **Public accessibility is not permission.** A freely downloadable file may still be reference-only or unknown.
2. **Authenticity/confidence is not permission.** A Tier A official exam may be restricted; a low-confidence worksheet may be openly licensed.
3. **Inclusion in Corpus is not downstream reuse approval.** Every learner-facing/content-export action must pass a rights gate independently of the confidence gate.
4. **Rights are action-specific.** Permission to redistribute an unmodified work does not automatically mean permission to translate, adapt, commercialize, or omit attribution.
5. **Unknown rights default conservatively.** Missing license information never becomes implied permission.
6. **Mixed-rights material is handled locally.** Text, audio, images, answer keys, scoring material, or individual assets may have different rights.
7. **The most restrictive relevant component governs a composite use.** A reusable task text paired with a restricted image is not reusable as the unchanged complete task unless the image is replaced or separately permitted.
8. **Rights decisions require evidence and provenance.** A normalized status must remain traceable to the observed license, permission, terms, source statement, operator decision, or takedown reason that produced it.
9. **Takedown is a state change with downstream effects, not merely a deleted URL.** Raw content, cached App content, generated derivatives, and source-specific structured records must be discoverable and suppressible.
10. **Non-reconstructive intelligence is different from source expression.** Abstract task patterns, taxonomy tags, aggregate counts, and other non-reconstructive metadata may remain usable when the source content itself is not redistributable, subject to takedown/legal-review exceptions defined below.

---

## 2. Inputs / Existing Decisions

Stage 04 preserves the shared product overview, identity, live Corpus/App checklists, and all earlier Corpus shaping decisions.

### 2.1 Stage 01 — Product Mission and Boundaries

`corpus/01-product-mission-and-boundaries.md` established that:

- Corpus is an exam-data and intelligence product, not a public source-file mirror;
- authenticity/confidence and usage rights are independent dimensions;
- raw/reference material and learner-practice material are different products;
- unknown rights must remain unknown/review-required rather than being treated as reusable;
- App should normally practice source-observed patterns with original content where direct reuse is inappropriate;
- the Corpus → App contract must eventually expose rights/restriction context where source material is involved.

Stage 04 turns those principles into operational states and actions.

### 2.2 Stage 02 — Source Strategy

`corpus/02-source-strategy.md` established that:

- official, publisher, teacher/school, repository/archive, unofficial, forum/shared-document, and standalone exercise sources may all enter Corpus;
- public reachability never implies reuse permission;
- manual files and gated materials may be registered when the owner legitimately possesses them, without requiring access circumvention;
- source provenance survives dead URLs, mirrors, moves, and raw-file removal;
- a takedown/rightsholder request is materially different from an ordinary 404/410;
- source changes must preserve observation/version history rather than silently overwriting it.

Stage 04 must therefore distinguish **availability state** from **usage-rights state**.

### 2.3 Stage 03 — Trust, Authenticity, and Confidence

`corpus/03-trust-authenticity-confidence.md` established that:

- direct learner exposure requires **B+ confidence at the most local relevant level plus Stage 04 rights permission**;
- B+ is also the default minimum confidence for exercise-generation grounding;
- disputed answer keys, quarantine, or local integrity problems can block a use even when rights would otherwise allow it;
- confidence can change over time and must remain auditable.

Stage 04 does not weaken any Stage 03 confidence gate. A downstream action proceeds only when **both** the trust gate and the rights gate allow it.

### 2.4 Bestehen / App constraints

The App checklist already requires source/reference exams and generated simulations to remain distinct and requires mock exams to respect content-usage restrictions. The App is therefore not allowed to infer usage from source type, confidence, or presence in Corpus. Corpus must provide an explicit rights-safe action decision or enough metadata for the contract layer to compute one deterministically.

---

## 3. Decisions and Rationale

### 3.1 Use an operational status plus action-level permissions

**Decision:** Rights are represented by two layers:

1. an **effective usage status** that gives humans and downstream systems a simple default posture; and
2. **action-level permission fields and obligations** that remain the authoritative detail.

A single label cannot safely encode every license condition. For example, material may allow redistribution only with attribution, allow non-commercial but not commercial use, or permit unmodified copies but not derivatives. The status is therefore a useful operational summary, while downstream actions must still honor the specific permission fields.

### 3.2 Required operational usage statuses

Bestehen / Corpus uses five statuses.

| Usage status | Meaning | Default interpretation |
|---|---|---|
| **REUSABLE** | Documented rights/permission support the intended direct reuse and no material special restriction changes the normal action | Exact source content may be used only for actions explicitly permitted by the recorded fields, still subject to Stage 03 confidence and product suitability |
| **REUSABLE_WITH_CONDITIONS** | Direct reuse is supported, but obligations/restrictions apply | Reuse is allowed only when the App/export path can satisfy the recorded conditions, such as attribution, non-commercial scope, share-alike, limited media/territory, or no-derivative restrictions |
| **REFERENCE_ONLY** | Corpus may retain/analyze the material as internal evidence under the project's operational policy, but direct redistribution/adaptation is not approved | Use the source to learn structure/patterns; do not expose exact content, close adaptations, translations, or reconstructive derivatives to learners |
| **UNKNOWN_REVIEW_REQUIRED** | Available evidence is insufficient, conflicting, or too ambiguous to classify confidently | Behave conservatively: no direct learner exposure, redistribution, close adaptation, or commercial-use assumption; only bounded internal/reference processing is allowed until review |
| **PROHIBITED** | An explicit restriction, takedown state, acquisition/policy problem, or reviewed decision blocks active use of the affected material | No new learner use, export, generation grounding from raw content, or normal active analysis; remove/suppress affected material according to the takedown/removal rules |

`REUSABLE_WITH_CONDITIONS` is intentionally separate from `REUSABLE` so that a simple status check cannot hide obligations that a learner-facing or export flow must satisfy.

### 3.3 Status is not the legal conclusion

**Decision:** The operational status means **“what Bestehen is currently allowed to do under its recorded product policy and evidence,”** not “the definitive legal status of the work.”

The model must preserve uncertainty and evidence because:

- licenses can be scoped to some assets but not others;
- pages can contain third-party images/audio despite a site-wide license statement;
- custom terms can be ambiguous;
- a source can change its terms over time;
- a future commercial product may invalidate an assumption that was acceptable for a private/non-commercial phase;
- a takedown request can require an immediate hold before legal questions are resolved.

### 3.4 Unknown rights default to `UNKNOWN_REVIEW_REQUIRED`

**Decision:** If no clear permission/license applies, Corpus does **not** infer reusable rights from public accessibility, common online sharing, official provenance, search-engine indexing, mirror count, or the absence of a copyright notice.

The default is `UNKNOWN_REVIEW_REQUIRED`.

The source may still contribute **bounded internal reference analysis** when it was legitimately obtained and there is no explicit prohibition/takedown or other high-risk condition. However:

- exact source text/audio/images must not be sent to the learner-facing App for direct display;
- no public/exported source bundle may include it;
- no close paraphrase, translation, adaptation, or reconstruction should be generated for learners from the source expression;
- no commercial-use permission may be assumed;
- if internal analysis itself is legally/contractually uncertain for that source class, processing pauses and legal review is required.

This default preserves the core Corpus value—learning from broad evidence—without turning uncertainty into publication permission.

### 3.5 Rights must be granular enough for mixed media

**Decision:** Rights metadata must be attachable to the **source observation and to the underlying material/components that may have distinct rights**, including documents/exams/tasks/items/assets where needed.

Stage 05 owns the final canonical entity model. Stage 04 requires the following product behavior regardless of schema:

- a source-level license/terms statement may seed a default for descendants;
- a more specific component-level statement overrides inheritance;
- unknown local rights do not inherit a broader permissive status when the source explicitly indicates third-party content may be excluded;
- a composite learner-facing use must pass rights checks for every included component;
- reusable text can be separated from a restricted image/audio asset and used independently if the rights and product experience permit that separation.

This avoids both extremes: assigning one legal status to an entire domain, or requiring manual per-question review when a clear source-wide license legitimately applies.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Required rights/usage metadata

The following fields are required conceptually. Stage 05/architecture may choose exact names, types, normalization, and storage.

### 4.1.1 Access and discovery context

| Field | Required product meaning |
|---|---|
| **public_accessibility** | Current observed access state: `public_no_account`, `public_with_account`, `paid_or_gated`, `private_or_manual`, `unavailable_or_removed`, or `unknown` |
| **access_observed_at** | When the accessibility state was observed |
| **acquisition_context** | Public discovery, archive/repository observation, owner manual URL, owner manual file, purchased/authorized owner copy, or other documented route |

**Rule:** Accessibility describes **how the material was reachable**, not what rights it carries.

### 4.1.2 License / permission evidence

| Field | Required product meaning |
|---|---|
| **known_license** | License/permission name and version exactly as observed when identifiable; otherwise `none_found`, `custom_terms`, `direct_permission`, `conflicting`, or `unknown` |
| **license_or_permission_evidence** | URL/page/file/statement/screenshot-reference/owner note that supports the license or permission claim |
| **license_scope** | Which material/assets the statement appears to cover; do not assume a site-wide declaration covers third-party embedded assets |
| **rights_holder_or_grantor_claim** | Optional observed claimant/grantor when relevant; a claim is not silently upgraded to verified ownership |
| **terms_source** | Terms/license page or source statement used for the classification |
| **terms_observed_at** | When the relevant terms/license were observed |

Corpus should preserve the **observed statement** separately from the normalized operational interpretation. If later review changes the interpretation, the historical evidence remains available.

### 4.1.3 Action-level permission fields

Each action-level field uses `allowed`, `allowed_with_conditions`, `prohibited`, `unknown`, or `not_applicable`.

| Field | What it controls |
|---|---|
| **redistribution_permission** | May Bestehen distribute/show the original or materially unchanged content outside the internal Corpus context? |
| **derivative_use_permission** | May Bestehen adapt, translate, modify, remix, or create a source-derived version whose expression remains materially connected to the original? |
| **commercial_use_permission** | Is the relevant use allowed if Bestehen/App becomes monetized, revenue-supported, paid, or otherwise commercial? |
| **attribution_requirement** | `none`, `required`, `conditional`, or `unknown`, plus the exact credit/link/notice requirements when known |

The following supporting obligations should be captured when present because they materially alter whether a downstream action is allowed:

- share-alike or reciprocal-license obligations;
- no-derivatives restriction;
- non-commercial restriction;
- required attribution text/author/provider/link;
- notice/license-text preservation;
- territory/audience/channel restrictions;
- time-limited permission;
- asset-specific exclusions;
- permission limited to private/classroom/internal use;
- any custom condition that downstream systems must satisfy.

### 4.1.4 Review and operational status

| Field | Required product meaning |
|---|---|
| **effective_usage_status** | One of the five Stage 04 operational statuses |
| **status_reason** | Short explanation of why the current status was chosen and which evidence controls it |
| **review_status** | `unreviewed`, `review_required`, `reviewed`, `legal_review_required`, `takedown_hold`, or `resolved` |
| **reviewed_at / reviewed_by** | Audit context for a manual decision when one occurred |
| **last_rights_check_at** | Most recent point at which the rights evidence was checked/reaffirmed |
| **source_terms_notes** | Human-readable notes for ambiguity, conflicting terms, source-specific conditions, or unresolved questions |

### 4.1.5 Removal / takedown metadata

When applicable, track:

- takedown/removal state;
- date requested/observed;
- affected scope;
- requester/claim reference when appropriate;
- reason/category;
- action taken;
- raw-content removal status;
- App/cache/export removal status;
- derived-data disposition (`retain_non_reconstructive`, `recompute_without_source`, `purge`, `pending_review`);
- prevention/block fingerprint sufficient to avoid accidental re-ingestion without retaining the removed expression itself.

The product does not require these to be stored as one object; it requires the information to be representable and auditable.

## 4.2 Rights review state is separate from Stage 03 confidence review

**Decision:** Stage 03 trust review and Stage 04 rights review are independent workflows even if one operations UI later shows them together.

Examples:

- Tier A confidence + `UNKNOWN_REVIEW_REQUIRED` rights: strong evidence, no direct learner reuse.
- Tier C confidence + `REUSABLE`: reuse permission exists, but confidence may still block generation/direct exposure.
- Tier A + `REUSABLE_WITH_CONDITIONS`: direct use can proceed only if the App satisfies conditions.
- Tier A + `PROHIBITED`: no direct use and, depending on prohibition reason, active analysis may stop as well.

No automated rule may upgrade rights because confidence improved, or upgrade confidence because an open license was found.

## 4.3 Simple decision table — usage status to Corpus/App behavior

The table below is the default operational behavior. Action-level permission fields and Stage 03 confidence/integrity gates can make behavior **more restrictive**, never less.

| Usage status | Keep source/provenance record | Store raw content internally | Corpus internal analysis | Keep non-reconstructive metadata/statistics | Use abstract patterns for original exercise generation | Send exact source content to App / show to learner | Create close adaptation/translation | Redistribute/export original content |
|---|---|---|---|---|---|---|---|---|
| **REUSABLE** | Yes | Yes, subject to retention/security policy | Yes | Yes | Yes, if Stage 03 gates pass | Yes, only for explicitly permitted actions and B+ local confidence | Yes only if derivative permission allows it | Yes only if redistribution permission allows it |
| **REUSABLE_WITH_CONDITIONS** | Yes | Yes, subject to conditions | Yes | Yes | Yes if conditions are compatible with the generation path | Only when all required conditions can be satisfied and Stage 03 gates pass | Only when derivative permission and conditions allow it | Only when redistribution permission and all conditions are satisfied |
| **REFERENCE_ONLY** | Yes | Yes if legitimately acquired and retention policy allows | Yes, for internal evidence | Yes | **Yes, but from abstracted/non-reconstructive features; not by close paraphrase or source reconstruction** | **No** | **No** | **No** |
| **UNKNOWN_REVIEW_REQUIRED** | Yes | Limited/internal only while review is pending, if legitimately acquired and no explicit prohibition applies | Bounded reference analysis only; stop if analysis itself is uncertain/high-risk | Yes when non-reconstructive and not otherwise restricted | **Yes only from abstracted features already permitted by policy; never source-expression copying** | **No** | **No** | **No** |
| **PROHIBITED** | Minimal audit/tombstone only as allowed/needed | No active raw retention except temporary authorized review/hold where required | **No new normal analysis** | Only what takedown/legal decision explicitly permits; otherwise suppress/recompute/purge | **No** | **No** | **No** | **No** |

### 4.3.1 Important interpretation

`REFERENCE_ONLY` and `UNKNOWN_REVIEW_REQUIRED` are intentionally useful to Corpus. They can still contribute to **what the exam appears to test** while being blocked from **how the learner sees practice**.

For those statuses, the preferred App-generation input is a **pattern abstraction** such as:

- provider/section/task type;
- targeted skill;
- CEFR/difficulty band;
- topic/domain;
- approximate passage/audio length;
- reasoning or distractor pattern;
- grammar/vocabulary targets;
- interaction shape;
- scoring/format facts that are safe to use as structured intelligence;
- aggregate frequency/relevance signals.

The App should then create an independently worded exercise. It should not receive the restricted question/passage/transcript merely so a model can “paraphrase it.”

## 4.4 Direct learner exposure rule

**Decision:** Exact or materially source-derived content may reach a learner only when **all** of the following are true:

1. Stage 03 confidence meets the relevant direct-exposure threshold (normally B+ at the most local relevant level, with answer-key consistency rules where applicable).
2. Stage 04 status/action fields explicitly allow the intended use.
3. Every included component/asset passes the rights gate or is replaced.
4. Required attribution/notices/conditions can be satisfied in the actual App experience.
5. The use is compatible with current commercial/non-commercial context.
6. There is no active rights review, legal-review requirement, dispute, takedown hold, or prohibition affecting the material.
7. Direct reuse is pedagogically preferable to generating an original equivalent.

The seventh condition is deliberate: even legally reusable material does not have to become learner-facing source content. Bestehen remains an exam coach, not an exam-file viewer.

## 4.5 Exercise-generation rule

**Decision:** Corpus rights status controls **what information the generator may receive and how closely the output may derive from the source**.

### For `REUSABLE` / `REUSABLE_WITH_CONDITIONS`

- Source content may be used as generation grounding only if Stage 03 B+ gates pass and the intended derivative/generation action is permitted.
- Conditions must survive the generation path where applicable.
- A no-derivatives restriction blocks source-derived adaptation even if unmodified redistribution is allowed.
- Commercial restrictions must be re-evaluated if the App's business context changes.

### For `REFERENCE_ONLY`

- Use **abstract pattern metadata**, not the original expression, as the default generation input.
- Original exercises must use new passages, names, contexts, sentences, distractors, audio scripts, prompts, and answer wording.
- The generated result must not be a translation, close paraphrase, lightly edited copy, or reconstructive transformation of the restricted source.
- Source-specific answer keys can inform correctness only when Stage 03 permits, but the generated item should have its own independently authored answer set.

### For `UNKNOWN_REVIEW_REQUIRED`

Apply the `REFERENCE_ONLY` generation restrictions and additionally avoid expanding source exposure while review is unresolved. If the only way to generate a useful exercise is to pass the raw unknown-rights work to an external model/provider or create a close adaptation, do not do so; use already-extracted abstract features or choose another source/pattern.

### For `PROHIBITED`

The source must not ground new generation. Existing generated exercises materially dependent on the source must be discoverable for takedown review.

## 4.6 AI/model use is not automatically licensed by “analysis allowed”

**Decision:** The product must not assume that permission for internal reference analysis automatically authorizes uploading exact source content to a third-party model provider, using it in a persistent training dataset, or creating reconstructive outputs.

For the initial personal-project phase, the low-risk default is:

- pre-extract/cache structured pattern metadata where allowed;
- prefer generation from abstractions rather than full restricted source content;
- avoid persistent model-training/fine-tuning datasets containing unknown/reference-only source expression unless separately reviewed;
- treat external processing of gated/private/custom-term material as a review trigger.

The architecture may later define vendor/data-retention controls, local models, or other mechanisms. Stage 04 only defines that **the rights decision must cover the actual processing action**, not merely the final UI display.

## 4.7 Attribution behavior

**Decision:** Attribution is a downstream obligation, not optional decoration.

When attribution is required:

- the exact required credit/author/provider/link/license notice must be preserved in structured metadata;
- any learner-facing reuse, export, or derivative that requires attribution must have a rendering path capable of showing it;
- if the App experience cannot satisfy the attribution obligation cleanly, that action is blocked even though the source remains `REUSABLE_WITH_CONDITIONS` for other contexts;
- attribution must not imply official partnership, approval, or affiliation with TELC or another provider.

If attribution requirements are unknown, treat the affected direct-use action as unknown/review-required rather than silently omitting credit.

## 4.8 Commercial-use restrictions and future product changes

**Decision:** Commercial-use permission is captured from the beginning even though Bestehen is initially a personal project.

Reason: a future public, paid, subscription, ad-supported, sponsored, employer-funded, or otherwise commercialized App could change whether a previously acceptable use remains allowed.

Product rules:

- non-commercial permission may allow a current private/non-commercial use while blocking future commercial reuse;
- becoming commercial must trigger re-evaluation of every active `REUSABLE_WITH_CONDITIONS` source with commercial restrictions;
- the App should prefer original exercises grounded in abstract intelligence when direct reuse would create licensing fragility;
- commercial restrictions do not alter Stage 03 confidence or whether the source is analytically valuable.

## 4.9 Source terms and terms changes

**Decision:** Terms/license observations are versioned evidence, not timeless facts.

When terms materially change:

1. preserve the prior observed terms/evidence and observation date;
2. record the new terms/evidence;
3. re-evaluate current and future uses;
4. place affected content in `review_required` or `legal_review_required` when the effect is unclear;
5. do not assume a newer permissive/restrictive statement automatically applies retroactively to every earlier acquisition/use;
6. stop new high-risk/direct uses while a material conflict is unresolved.

The exact legal effect of a terms change can require legal review. The product requirement is traceability and safe suspension, not automatic legal interpretation.

## 4.10 Rights inheritance and overrides

**Decision:** Rights may inherit only when the scope of the evidence supports inheritance.

Examples:

- A clearly scoped open license covering all original text on a page may seed the document/task text status.
- A page stating that embedded images are third-party does **not** grant those images the page's license.
- A source-wide publisher policy can seed descendants, but a per-file license overrides it.
- An audio track with separate terms overrides the booklet's status for the listening asset.
- A direct permission covering one specific mock exam does not automatically cover the publisher's other materials.

Where scope is uncertain, the local component becomes `UNKNOWN_REVIEW_REQUIRED` rather than inheriting a more permissive status.

## 4.11 Raw content versus structured/derived data

For rights operations, Corpus distinguishes three product classes:

1. **Source expression / reconstructive data** — original text, item wording, choices, transcripts, audio, images, scans, close paraphrases/translations, or structured fields that effectively reproduce the work.
2. **Source-specific non-reconstructive metadata** — provider/level/task type, taxonomy labels, confidence, difficulty estimate, length, topic tags, rights status, provenance, hashes/fingerprints, and similar descriptors that do not reproduce meaningful source expression.
3. **Aggregate intelligence** — frequencies, relationships, prevalence estimates, TELC relevance, skill/topic/grammar statistics, difficulty distributions, and other outputs combining independent evidence.

Takedown/removal rules treat these classes differently.

---

## 5. Takedown, Removal, and Reclassification

## 5.1 Takedown/removal trigger categories

A source/material may require removal or suppression because of:

- a rightsholder/takedown request;
- an explicit source/licensor request;
- a newly discovered license/terms restriction;
- acquisition that is later found to violate the project's access policy;
- a security/privacy issue;
- a rights review that changes the item to `PROHIBITED`;
- a legal-review decision;
- owner choice to remove material even without a formal demand.

An ordinary dead URL does **not** automatically trigger these rules; Stage 02 already treats dead URLs as provenance/availability changes.

## 5.2 Immediate takedown hold

**Decision:** A credible takedown/removal request or serious rights concern creates an immediate **takedown hold** before final disposition.

While on hold:

- block new direct learner exposure;
- block new redistribution/export;
- block new source-derived generation from raw content;
- pause normal reprocessing/enrichment of the affected material;
- prevent the material from being newly selected into source-backed mock/exercise content;
- preserve only the access needed for authorized review and scoping;
- identify linked mirrors, versions, assets, structured records, App caches, and generated exercises that may depend materially on the source.

The hold is intentionally conservative and reversible.

## 5.3 Scope the affected material

Takedown must be scoped to the smallest defensible affected unit while preventing easy circumvention.

Examples:

- one third-party image can be removed/replaced without deleting independently reusable text;
- a request covering a complete PDF should suppress copies/mirrors of the same underlying work, not only one URL;
- a request about one provider's audio does not automatically delete unrelated text assets unless they are part of the same claim;
- a source-level request can require broader blocking when the rightsholder clearly identifies a collection or work family.

Stage 09 deduplication/lineage must eventually help discover mirrors and derivatives; Stage 12 must propagate the decision to App consumers.

## 5.4 Raw/source-expression removal

When a takedown/removal is accepted or the status becomes `PROHIBITED`:

- remove or make inaccessible active raw files/bytes and source-expression fields within the affected scope;
- remove learner-facing copies, cached media, exports, and exact-source exercises;
- retire or review close derivatives/translations/adaptations materially dependent on the source;
- stop the source from grounding new generation;
- retain only the minimum audit/tombstone information permitted/needed to document the action and prevent accidental re-ingestion;
- ensure search/internal tooling does not continue exposing the removed source expression as though it were merely hidden from App.

A tombstone may include source identifiers, URLs, hashes/fingerprints, dates, removal reason/status, and lineage IDs without preserving the removed expression itself.

## 5.5 What happens to already-derived metadata/statistics

**Decision:** By default, **non-reconstructive derived metadata and aggregate statistics may remain** after source-content removal when all of the following are true:

1. they do not reproduce or allow practical reconstruction of the removed source expression;
2. the takedown/legal-review decision does not require their deletion;
3. retaining them does not defeat the practical purpose of the takedown;
4. provenance can still indicate that the contributing source was removed/restricted;
5. they remain analytically valid under Stage 03 confidence/authenticity rules.

Examples that may normally remain:

- provider/level/task/skill/topic/grammar labels;
- length/difficulty/relevance measurements;
- dedup fingerprints or non-reconstructive identity hashes;
- counts and frequency contributions;
- aggregate pattern statistics;
- a minimal provenance/takedown tombstone;
- historical audit facts that the source existed and was later removed.

Examples that are treated as source expression and should be removed/restricted with the source:

- full question/passage/instruction text;
- answer choices copied verbatim;
- transcripts that reproduce protected audio dialogue;
- images/scans/audio;
- close summaries that effectively substitute for the original;
- translations or lightly rewritten versions;
- structured extraction that, when joined, reconstructs the original work.

### 5.5.1 Rights removal versus evidence invalidation

A rights takedown and a trust/authenticity failure have different analytical effects.

- **Rights-only removal:** non-reconstructive historical intelligence may remain useful by default because the source can still be strong evidence even though its content cannot be retained/shown.
- **Authenticity/confidence invalidation:** analytics that relied on the source may need to be recomputed/discounted because the evidence itself is no longer trustworthy.
- **Combined rights + trust issue:** apply both removal and analytical recalculation.

### 5.5.2 Recompute and purge capability is mandatory conceptually

Even though non-reconstructive intelligence is retained by default, Corpus must be able to mark affected analytics as **recompute_without_source** or **purge** when a takedown/legal decision requires it.

Later architecture must therefore preserve lineage from important derived records/aggregates back to contributing evidence well enough that removal can be propagated. Stage 04 does not choose the data lineage implementation.

## 5.6 Takedown does not erase the fact that an event occurred by default

Stage 02's permanent-provenance principle remains valid in a narrower form after takedown: Bestehen should normally retain a **minimal non-content audit trail** sufficient to explain that material was once observed, was removed, and must not be re-ingested.

However, if a valid legal/privacy/security decision requires deletion of even that metadata, the product must support that stronger purge. “Permanent provenance” is therefore subordinate to an explicit deletion requirement.

## 5.7 Reclassification without removal

Rights status can move in either direction when evidence changes.

Examples:

- `UNKNOWN_REVIEW_REQUIRED` → `REUSABLE_WITH_CONDITIONS` after a clear license is found;
- `REFERENCE_ONLY` → `REUSABLE` after direct permission is obtained;
- `REUSABLE` → `REUSABLE_WITH_CONDITIONS` after a missed attribution condition is discovered;
- `REUSABLE_WITH_CONDITIONS` → `REFERENCE_ONLY` when the App becomes commercial and the license is non-commercial;
- any active status → `PROHIBITED` after takedown or reviewed restriction.

Every reclassification that changes downstream behavior must trigger reevaluation of affected App/source-backed content.

---

## 6. Edge Cases / Failure or Uncertainty Handling

### 6.1 Official TELC model test publicly downloadable with no clear reuse license

Confidence may be Tier A and the file may be easy to access, but rights default to `UNKNOWN_REVIEW_REQUIRED` or `REFERENCE_ONLY` after review. Corpus may learn exam structure and patterns; App should use original equivalents unless explicit reuse permission is established.

### 6.2 Openly licensed teacher mock with attribution requirement

If license scope is clear and the material meets Stage 03 confidence gates, use `REUSABLE_WITH_CONDITIONS`. Direct learner use is allowed only where the required attribution/license notice can be shown correctly. If the App cannot satisfy the condition, fall back to original generated practice.

### 6.3 License permits copies but prohibits derivatives

Use `REUSABLE_WITH_CONDITIONS`: unmodified redistribution may be permitted, but translation, adaptation, close paraphrase, modified task construction, or source-derived generation is blocked. Action-level fields, not the status label alone, control the decision.

### 6.4 License is non-commercial and Bestehen later charges money

The source remains useful as reference intelligence, but direct commercial reuse becomes blocked unless new permission is obtained. Reclassify the effective commercial context and retire/replace affected learner-facing material if needed.

### 6.5 Website has a permissive site footer but embedded image/audio is credited to someone else

Do not inherit the site license to the third-party asset. The asset becomes separately classified, usually `UNKNOWN_REVIEW_REQUIRED` until its own rights are known. The task can still be used if the restricted component is omitted/replaced and the remaining components pass rights gates.

### 6.6 Mirror has no license but the verified original has a clear license

Rights can follow the **underlying work and scope of the original license** when the mirror is credibly matched and the license actually permits the intended use. The mirror host does not become the licensor. Preserve both provenance locations.

### 6.7 Mirror republishes material in apparent violation of the original terms

Do not infer reusable rights from the mirror's availability. Anchor rights to the underlying work's credible grant/terms. The mirror can remain useful as provenance/resilience only if keeping it is consistent with the removal/access policy.

### 6.8 Public shared document with no author/license

Classify `UNKNOWN_REVIEW_REQUIRED`. It may contribute bounded reference intelligence if legitimately accessible and no explicit restriction applies, but exact learner-facing reuse and close adaptation are blocked.

### 6.9 Owner manually uploads purchased publisher material

Mark accessibility/acquisition context as purchased/authorized owner copy rather than public. Rights do not become reusable merely because the owner can read the material. Default to `UNKNOWN_REVIEW_REQUIRED`/`REFERENCE_ONLY` for Corpus analysis until the relevant license/terms are understood. Public/App redistribution is blocked by default.

### 6.10 Source says “free for classroom use”

Do not translate that phrase automatically into unrestricted App reuse. Record the exact condition, classify `REUSABLE_WITH_CONDITIONS` only if the intended Bestehen use clearly fits the documented scope; otherwise require review. A future public/commercial App is a separate context.

### 6.11 Public-domain/open-license claim is made by an unverified third party

The claim is evidence, not proof. Keep `UNKNOWN_REVIEW_REQUIRED` until the grant/source is credible enough for the intended use.

### 6.12 Different rights for text and audio

Classify separately. Corpus can expose/reuse permitted text while replacing or generating new audio if the original audio is restricted. Composite mock delivery requires all included components to pass.

### 6.13 Rightsholder asks only for raw file removal

Remove the raw/source-expression content within scope. Retain non-reconstructive metadata/aggregate intelligence by default if the request/decision allows it. Record the scope so the file is not re-ingested from a mirror.

### 6.14 Rightsholder explicitly demands deletion of derivatives/metadata too

Place the source and affected downstream records on takedown hold, identify source-derived App content and analytics, and escalate to legal review if the required scope is not clear. The product must support `recompute_without_source` or stronger purge rather than assuming all metadata is always retainable.

### 6.15 Removed source was the only evidence for a high-priority pattern

If the removal is rights-only and non-reconstructive intelligence can remain, the pattern may retain its historical analytical support with a removed-source provenance flag. If the evidence itself is invalidated, the priority must be recomputed and may disappear. Stage 11/12 should make that distinction explicit.

### 6.16 Generated exercise resembles a reference-only source too closely

Treat it as a rights-quality failure even if generation was intended to be original. Quarantine/retire the generated exercise, use a safer abstraction or different grounding set, and ensure regeneration is independently worded. Stage 10/12 can later define similarity QA thresholds.

### 6.17 Rights evidence conflicts

If a file says one license but a source terms page or rightsholder statement says something incompatible, use `UNKNOWN_REVIEW_REQUIRED` or `legal_review_required`; suspend direct reuse until resolved. Do not pick the more permissive statement merely because it enables more product functionality.

### 6.18 Source disappears without takedown request

Do not automatically reclassify rights. Preserve the last observed rights evidence and mark availability separately as `unavailable_or_removed`. Revisit/review rights when the material would be used directly or when a later source provides new terms.

---

## 7. Where Legal Review Is Genuinely Needed

The product should not require a lawyer to classify every source. Legal review is reserved for decisions where Bestehen would otherwise rely on a non-obvious legal interpretation or accept material exposure.

**Legal review is required or strongly recommended when:**

1. Bestehen wants to republish or adapt official/provider exam content without an explicit license/permission that clearly covers the intended action.
2. A custom license/terms statement is ambiguous, conflicting, or difficult to map to redistribution/derivative/commercial use.
3. Bestehen would rely on a statutory exception or text/data-mining theory rather than an explicit permission for a material processing use.
4. A paywalled, account-gated, purchased, private, or manually supplied source would be used beyond clearly private/internal analysis.
5. Exact copyrighted source content would be sent to an external AI/model provider under terms that are not clearly compatible with the acquisition/use context.
6. Bestehen wants to build a persistent fine-tuning/training dataset from reference-only/unknown-rights source expression.
7. A takedown/rightsholder dispute is contested or asks for deletion beyond the obvious raw/source-content scope.
8. Commercial launch changes the permissibility of material previously used under non-commercial or educational conditions.
9. Rights differ among text/audio/images or multiple rightsholders and the intended composite use cannot be resolved from clear grants.
10. A public Corpus export/API/research release would expose source-derived records that were previously internal-only.
11. Provider trademarks/logos/branding or wording could imply official affiliation/endorsement rather than merely identifying the exam target.

The default product response while legal review is pending is **conservative suspension of the affected direct/high-risk action**, not removal of all analytical evidence unless the concern requires it.

---

## 8. Relationship to Other Bestehen Stages

### Stage 05 — Canonical Exam Model

Stage 05 must make rights metadata attachable to the appropriate source/material/component scopes and preserve inheritance/override relationships. It should distinguish source expression from non-reconstructive metadata sufficiently for removal behavior.

### Stage 06 — Exam and Skill Taxonomy

Taxonomy tags are normally non-reconstructive derived metadata and may remain usable even when source expression is reference-only. Taxonomy must retain provenance/rights lineage where needed for later deletion/recomputation.

### Stage 07 — Difficulty and TELC Relevance

Rights do not determine relevance or trust. Reference-only material may influence difficulty/relevance if Stage 03 confidence permits. Direct examples shown to learners remain Stage 04-gated.

### Stage 08 — Ingestion Pipeline

The pipeline must extract rights evidence early enough to prevent unsafe downstream publication, support review/legal-review/takedown states, and propagate reclassification without repeatedly running expensive analysis.

### Stage 09 — Deduplication

A takedown or prohibition applying to an underlying work must be able to find known mirrors/duplicates so deleting one URL does not cause accidental re-ingestion from another. Duplicate relationships do not create new rights.

### Stage 10 — Validation and QA

QA should validate required rights metadata completeness for production-ready records and eventually detect source-derived/generated outputs that are suspiciously close to reference-only material.

### Stage 11 — Corpus Analytics

Analytics may use eligible reference-only/unknown-rights evidence under this operational policy, but must remain recomputable where a takedown/legal decision requires exclusion. Aggregate outputs should avoid reconstructing source content.

### Stage 12 — Corpus → App Contract

The contract must carry either the effective action decision or sufficient fields to prevent App from treating raw/reference content as reusable. It must define behavior when rights change or content is removed, including cache invalidation/retirement of source-backed exercises.

### Stage 13 — Corpus Operations

Operations needs a rights-review queue, evidence/terms view, manual status override with rationale, takedown workflow, affected-downstream-content discovery, and audit history. The UI/tooling details remain later decisions.

### Stage 14 — Cost, Scale, and Automation

Rights extraction should use deterministic/source-level evidence reuse first, not expensive per-item AI. Legal/manual review should focus on high-value direct-reuse decisions, ambiguous custom terms, commercial expansion, and takedown disputes.

### Stage 15 — Security and Abuse

Security may impose stricter deletion/quarantine rules than rights alone, especially for private/manual submissions or unsafe files. Stage 15 also owns raw-file retention security.

### Stage 16 — Initial Benchmark Corpus

The benchmark must include expected rights classifications across official public material, clear open licenses, attribution/non-commercial conditions, unclear public PDFs, purchased/manual material, and a prohibited/takedown case. Rights classification accuracy should be evaluated separately from authenticity.

### Stage 17 — Final Product Specification

The final PRD must preserve the separation among accessibility, authenticity/confidence, usage status, action permissions, TELC relevance, and removal state.

### Relationship to Bestehen / App

The central App rule is simple:

> **Corpus evidence can shape what Bestehen teaches even when the source itself cannot be shown.**

The App should prefer original exercises grounded in abstract Corpus patterns unless direct reuse is both rights-safe and pedagogically useful. This keeps the learner experience robust even when sources are removed, licenses change, or the project later becomes commercial.

---

## 9. Cost Notes

Rights handling has **low recurring compute cost** if designed around evidence reuse and conservative defaults. Its main potential cost is selective human/legal review, not model inference.

### 9.1 Preferred low-cost default

- Record public accessibility and license/terms evidence during normal source intake/revisit.
- Reuse source/domain/license-level evidence across descendants only when scope clearly supports inheritance.
- Use deterministic detection for explicit license markers, standard terms URLs, attribution notices, and known permission statements before any AI.
- Allow cheap/local model assistance to **extract candidate terms/conditions**, but do not treat model output as legal authority.
- Default ambiguous cases to `UNKNOWN_REVIEW_REQUIRED` rather than paying to resolve every source immediately.
- Spend human review first on material proposed for direct learner reuse, high-value TELC assets, unique sources, commercial-use decisions, or takedown disputes.
- Prefer abstract pattern generation from reference-only material so App quality does not depend on acquiring redistribution rights for a large corpus.
- Cache/version rights decisions and only re-review when terms/evidence/context materially changes.

### 9.2 When premium/legal spend is justified

Higher cost is justified when it unlocks or protects a material product capability, for example:

- a small set of high-value official/reference assets the owner genuinely wants to show directly;
- ambiguous permission affecting a large amount of otherwise reusable content;
- a commercial/public launch;
- a contested takedown;
- an external data/API release;
- a model-training strategy that would otherwise depend heavily on reference-only source expression.

### 9.3 Cheaper fallback

The cheapest safe fallback is almost always:

**keep the source as reference intelligence, block direct reuse, generate original exercises from abstract patterns, and revisit the rights question only if direct reuse becomes materially valuable.**

This preserves the exam-coaching goal without turning rights review into a prerequisite for corpus breadth.

---

## 10. Decisions Made

1. Rights/usage classification is independent of authenticity/confidence, source category, public accessibility, and TELC relevance.
2. Bestehen uses five operational statuses: `REUSABLE`, `REUSABLE_WITH_CONDITIONS`, `REFERENCE_ONLY`, `UNKNOWN_REVIEW_REQUIRED`, and `PROHIBITED`.
3. Action-level permissions remain authoritative for redistribution, derivative use, commercial use, and attribution obligations.
4. Public accessibility is tracked explicitly but never treated as permission.
5. Known license/permission evidence, scope, source terms, observation dates, review state, rationale, and takedown state are first-class product metadata.
6. Unknown/unclear rights default to `UNKNOWN_REVIEW_REQUIRED`, with no direct learner exposure, redistribution, close adaptation, or commercial-use assumption.
7. `REFERENCE_ONLY` material can still contribute internal exam intelligence and abstract generation patterns when Stage 03 confidence permits.
8. The App should generate independently worded exercises from abstract features for reference-only/unknown material rather than paraphrasing source expression.
9. Direct learner exposure requires both Stage 03 B+ confidence/integrity gates and Stage 04 rights permission/conditions.
10. Rights must support mixed media/components and local overrides; a composite use is governed by the most restrictive relevant component.
11. Attribution and commercial restrictions are enforceable downstream obligations, not informational notes.
12. Exact source content should not be assumed safe for external-model upload or persistent training merely because internal reference analysis is allowed.
13. A credible takedown/serious rights concern creates an immediate hold on new learner use, export, source-derived generation, and normal reprocessing.
14. Accepted takedowns remove/suppress raw/source expression and affected learner-facing copies; minimal non-content tombstones may remain unless stronger deletion is required.
15. Non-reconstructive metadata and aggregate statistics are retained by default after rights-only removal when the takedown/legal decision permits it; source-expression/reconstructive data is removed.
16. Corpus must be able to recompute/purge derived outputs when takedown/legal review requires exclusion or when evidence validity changes.
17. Rights reclassification is auditable and can trigger App/content re-evaluation in either direction.
18. Legal review is selective and reserved for non-obvious legal reliance, ambiguous custom terms, commercial/public expansion, external-model/training use, or contested takedowns.
19. Rights processing should be precomputed, cached, and primarily deterministic/manual-at-impact rather than a recurring per-learner AI cost.

---

## 11. Open Questions / Deferred Decisions

### 11.1 Owner questions

**None.** The existing project principles support a conservative default without requiring the owner to choose a legal risk tolerance at this stage.

### 11.2 Deliberately deferred architecture/implementation decisions

- exact schema/entity placement and inheritance mechanics for rights records — **Stage 05 + architecture**;
- exact automated terms/license extraction and classification pipeline — **Stage 08/10**;
- exact similarity threshold used to flag generated content as too close to reference material — **Stage 10/12**;
- exact duplicate-cluster propagation mechanics for takedown — **Stage 09**;
- exact aggregate lineage/recomputation mechanism — **Stage 11/architecture**;
- exact Corpus → App rights envelope, cache invalidation protocol, and content-retirement mechanism — **Stage 12**;
- exact rights-review/takedown operations UI and roles — **Stage 13**;
- concrete raw-file retention periods — **Stage 15**;
- any jurisdiction-specific legal interpretation or legal opinion — outside product shaping and only invoked where the legal-review triggers above require it.

### 11.3 Context changes that must reopen rights review

The following product changes materially alter the rights context and should reopen affected classifications before launch/use:

- Bestehen becomes commercial/paid/ad-supported;
- Corpus becomes public or exposes a third-party API/export;
- source-derived content is intentionally distributed outside the App;
- a persistent model-training/fine-tuning dataset is introduced;
- new third-party AI processing sends raw reference-only content outside the current trusted processing boundary;
- a source/provider changes terms or sends a rights request.

---

## 12. Definition of Done Check

- [x] Rights/usage classification is explicitly separate from authenticity/confidence.
- [x] Public accessibility is tracked independently from permission.
- [x] Known license/permission evidence and scope are defined.
- [x] Redistribution permission is tracked.
- [x] Derivative-use permission is tracked.
- [x] Attribution requirements are tracked and enforced operationally.
- [x] Commercial-use restrictions are tracked and future-context-aware.
- [x] Rights review status is defined separately from confidence review.
- [x] Source terms/notes and evidence timestamps are captured.
- [x] Operational statuses are defined, including reusable, conditional reusable, reference-only, unknown/review-required, and prohibited.
- [x] A decision table maps statuses to Corpus/App behavior.
- [x] Unknown/unclear rights default conservatively and cannot silently become reusable.
- [x] Direct learner exposure requires both confidence and rights gates.
- [x] Exercise generation from restricted/unknown material is limited to abstract/non-reconstructive pattern grounding rather than close paraphrase.
- [x] Mixed-rights documents/assets and local overrides are handled.
- [x] Takedown/removal hold, scoping, downstream suppression, and raw-content removal behavior are defined.
- [x] The default treatment of already-derived metadata/statistics after removal is defined.
- [x] Recompute/purge behavior exists for stronger takedown/legal/evidence-invalidity cases.
- [x] Legal-review triggers are identified without turning this stage into legal advice.
- [x] Cost-sensitive defaults and escalation rules are defined.
- [x] No Stage 04 owner decision remains unresolved.

**Stage 04 is product-complete when the live Corpus checklist matches the decisions above.**