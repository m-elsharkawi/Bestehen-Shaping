# Bestehen / Corpus — Stage 13: Corpus Operations and Review Experience

> **Status:** Authoritative Stage 13 product-shaping decision  
> **Product:** Bestehen / Corpus  
> **Primary operator:** One owner in the personal-project phase  
> **Core principle:** Corpus must be maintainable through a small, auditable operations surface that exposes exceptions, evidence, and safe corrective actions without requiring direct database editing or a polished enterprise admin product.

## 1. Purpose and Scope

Stage 13 defines the **internal operational experience** required to keep Bestehen / Corpus trustworthy after ingestion begins. It answers how the owner discovers what needs attention, reviews ambiguous evidence, corrects mistakes, controls future source intake, reprocesses affected records, and judges whether the corpus is healthy.

The objective is not to create a second learner-facing product or an enterprise administration suite. The initial operator is one owner, so the product should optimize for:

- high-impact exceptions rather than exhaustive manual inspection;
- safe, explicit actions rather than arbitrary database editing;
- compact table/detail views rather than elaborate dashboards;
- permanent auditability of human corrections and automated reruns;
- cheap operation with no always-on premium AI requirement;
- enough visibility that Corpus problems can be understood without inspecting internal storage directly.

This stage defines the **product semantics and minimum operational capabilities**, not the implementation stack. It does not choose an admin framework, UI library, database console, queue system, workflow engine, authentication mechanism, hosting platform, job runner, or notification service.

### 1.1 Stage objective

**One owner should be able to discover, review, correct, restrict, reprocess, and monitor Corpus evidence through a minimal internal operations surface, while every consequential action remains traceable and later automation remains unable to silently overwrite reviewed decisions.**

### 1.2 What “without direct database surgery” means

The operator may inspect technical identifiers and raw evidence, but ordinary maintenance must not require handwritten SQL, manually changing database rows, or editing stored records outside governed product actions.

The operations experience must therefore provide explicit product actions for the decisions shaped in Stages 02–12: intake disposition, review outcomes, provenance correction, trust/rights decisions, duplicate relationships, taxonomy corrections, reprocessing, quarantine/prohibition, and removal/takedown handling.

---

## 2. Inputs / Existing Decisions

Stage 13 preserves the shared Product Overview, Identity, both live shaping checklists, and Corpus Stages 01–12.

### 2.1 Stage 01 — internal-first and maintainable

`corpus/01-product-mission-and-boundaries.md` already identifies the owner/operator as an internal Corpus user and requires future internal tooling to inspect and maintain the corpus without direct database surgery. It also defines corpus health, review backlog, reprocessing, and auditability as part of a useful and financially sustainable corpus.

### 2.2 Stage 02 — source operations

`corpus/02-source-strategy.md` requires automated discovery plus manual URL/file intake, a curated source universe, revisit/freshness behavior, mirror/dead-source visibility, source controls, and provenance corrections that preserve history.

### 2.3 Stage 03 — trust review

`corpus/03-trust-authenticity-confidence.md` requires selective, impact-prioritized review of uncertain high-value evidence, disputed answers, quarantined records, confidence explanations, provenance correction, and auditable manual overrides. Confidence may change in either direction and local defects must remain local.

### 2.4 Stage 04 — rights review and takedown

`corpus/04-rights-and-usage-metadata.md` requires a separate rights-review workflow, evidence/terms visibility, manual status decisions with rationale, immediate takedown holds, affected-downstream-content discovery, and a prevention fingerprint/tombstone sufficient to stop accidental re-ingestion.

### 2.5 Stages 05–07 — structured evidence, taxonomy, and estimations

The canonical exam model keeps Source Observation, Document, Exam, Section, Task, Item, Stimulus, Answer, Scoring Rule, and Asset separately addressable. Taxonomy assignments have role, origin, confidence, version, and review state. Difficulty/relevance values are versioned estimates whose uncertainty remains explicit. Operations must therefore correct the smallest affected scope instead of rewriting whole documents unnecessarily.

### 2.6 Stage 08 — lifecycle and human override behavior

`corpus/08-ingestion-and-extraction-pipeline.md` defines the conceptual lifecycle:

**Discover → Fetch → Normalize → Parse → Segment → Classify → Extract Answers → Extract Assets → Enrich → Validate → Deduplicate → Review → Publish**.

It also requires `retry_pending`, `reprocess_candidate`, `blocked_dependency`, `review_required`, `disputed`, `quarantined`, `rejected_as_evidence`, `prohibited/takedown_hold`, and `superseded` states; exception-based human review; and the rule that a human correction or override retains author/time/rationale/evidence and cannot be silently overwritten by later automation.

### 2.7 Stage 09 — duplicate review

`corpus/09-deduplication-strategy.md` requires an operator to inspect candidate pairs/clusters, meaningful differences, provenance, canonical selection, relation confidence, unresolved-impact priority, and reversible corrections. Canonical provenance anchor, preferred processing representation, and reusable representation are separate choices.

### 2.8 Stage 10 — QA and health

`corpus/10-validation-and-quality-assurance.md` defines the quality vector, Q0–Q3 findings, manual-sampling escalation, benchmark/regression health, production-readiness gates, and secondary health metrics. Stage 13 must expose these operationally without collapsing them into one cosmetic corpus score.

### 2.9 Stage 11 — analytics

`corpus/11-corpus-analytics.md` distinguishes exploratory from decision-grade analytics and requires uncertainty, independent evidence, concentration, sufficiency, currentness, and versioning to remain visible. Operations therefore needs visibility into analytics-impacting unresolved dependency and evidence-quality problems.

### 2.10 Stage 12 — downstream impact

`corpus/12-corpus-app-contract.md` requires operations to review source/pattern eligibility, inspect provenance, correct taxonomy/rights/confidence, trigger reprocessing, and see which downstream App capabilities are affected by a change or invalidation.

No earlier product decision is replaced by Stage 13.

---

## 3. Decisions and Rationale

## 3.1 A bespoke dashboard is not required; an operations surface is required

**Decision:** The personal-project phase does **not** require a polished custom “Corpus dashboard.” It **does require a minimal owner-only operations surface** before Corpus can be considered maintainable.

The cheapest acceptable product is a **table-and-detail operations console** that can be implemented using the simplest existing/admin tooling available later, provided it supports the governed actions in this document. A hosted database/admin UI, low-code internal tool, or small custom internal page are all acceptable implementation directions; Stage 13 does not choose among them.

The product requirement is the behavior, not the visual polish.

### Why this is the default

A full dashboard would add design and maintenance cost before the project has real operational volume. Direct database editing would be cheaper initially but violates the audit, override, provenance, and safety rules already shaped. The middle ground is therefore:

- compact queue tables;
- one reusable record/review detail surface;
- explicit safe actions;
- a small corpus-health summary;
- no enterprise workflow machinery.

### Cheapest usable fallback

If a dedicated internal web UI is not yet worth building, the same product requirement can initially be satisfied by an authenticated admin/data tool **only if** it can expose the required saved views and invoke governed actions without editing raw rows directly. If it cannot enforce audit history, human-override preservation, rights/takedown rules, and reprocessing semantics, it is not an acceptable operational surface.

## 3.2 Use one prioritized operations inbox with specialized views

**Decision:** The MVP uses a single conceptual **Operations Inbox** with saved/specialized views rather than eight unrelated tools.

Every reviewable item should expose:

- the affected canonical scope and stable identity;
- why it entered the queue;
- current state and relevant severity/impact;
- source/provider/level/section context where useful;
- evidence/provenance links;
- current trust/rights/QA/duplicate/taxonomy state relevant to the issue;
- downstream capabilities currently blocked, limited, or at risk;
- age since the issue became actionable;
- recommended next safe actions;
- audit/reprocessing history.

The owner can filter by queue, impact, provider, source family, format, section, confidence tier, rights state, processing stage, or age as data exists.

**No fixed SLA is required for the personal-project phase.** Age is visible and sortable, while exact review-response targets belong to later operational experience if volume justifies them.

## 3.3 Review priority is based on product impact, not FIFO

The global review priority remains consistent with Stages 03, 08, 09, and 10:

1. Q0/correctness/scoring, takedown/prohibition, or direct learner-exposure risk;
2. current TELC target-format or high-TELC-relevance decisions;
3. benchmark/gold-standard records and regression blockers;
4. issues that materially change decision-grade analytics, independent evidence, or App priorities;
5. unique evidence filling an important provider/section/format gap;
6. reusable ambiguities whose one-time correction removes repeated future work;
7. low-impact duplicated, C/D-tier, exploratory, or optional metadata issues last.

A backlog is not itself a failure if low-impact records remain safely provisional or held.

## 3.4 Human edits are corrections/overrides, not source rewriting

**Decision:** Manual editing is allowed wherever a curator decision is necessary, but the owner does not directly rewrite source truth or silently overwrite machine history.

Manual actions create an explicit **curated correction, override, relationship decision, or status decision** at the smallest affected scope. The old value/derivation remains in history.

The operator can correct or decide, as applicable:

- source attribution, claimed provider/edition, provenance relationships, and source notes;
- relevance/intake disposition and source-category metadata;
- completeness and missing-dependency interpretation;
- authenticity status, confidence-dimension assessments, tier cap/override, review state, and rationale;
- rights status, action-level permissions/conditions, review/legal-review/takedown state, and rationale;
- structural boundary/link corrections across Exam/Task/Item/Stimulus/Answer/Asset relationships;
- answer/scoring relationship decisions, including disputed/accepted/superseded state;
- duplicate relationship class, canonical provenance anchor, preferred processing representation, and unresolved/independence treatment;
- taxonomy assignment approval/rejection/remapping/role/broadening and governed taxonomy changes through the taxonomy workflow;
- difficulty/relevance estimate review or curated override when justified by evidence;
- quarantine/reject/restore decisions;
- operator notes and evidence references.

### Manual-edit guardrails

- Source expression is not silently “fixed.” A corrected interpretation is stored separately from the observed source value.
- Raw derived analytics are not hand-edited to make a chart look right. Correct underlying evidence/mappings and recompute; a curated analytical override is exceptional and must be explicit.
- A human correction wins over an automated rerun until the owner explicitly supersedes it or the underlying source/governed rule materially changes.
- Destructive removal happens through the rights/security/takedown workflow, not a generic delete button.
- High-impact edits require a short rationale; evidence links are required when the decision depends on external/source evidence.

## 3.5 Audit history is mandatory even with one owner

**Decision:** Every consequential system or human change has a visible, append-only audit history.

At minimum, the history must make it possible to determine:

- what record/scope changed;
- when it changed;
- whether the actor was the owner, an automated rule/model, an import/migration, or a reprocessing run;
- the previous value/state and new value/state;
- action/reason category;
- human rationale/evidence note where required;
- processing/model/rule/taxonomy version when automation produced the change;
- related review queue/finding/dispute when applicable;
- whether a later result superseded the change;
- which downstream capabilities became newly eligible, restricted, invalidated, or due for recomputation.

The initial one-owner phase does not need comments, approval chains, assignments, or multi-user collaboration, but actor identity must still distinguish **human-curated** from **automated** decisions.

## 3.6 Source allow/block controls are operational policy, not trust or rights

**Decision:** Corpus requires explicit source **allow and block controls** so repeated discovery can be governed without changing crawler/database internals.

### Allow controls

An allow entry means the source/location is intentionally accepted for discovery/fetch consideration, for example a known official provider resource area or a repeatedly useful source family.

Allowing a source:

- does not make it authentic;
- does not grant usage rights;
- does not bypass relevance, validation, deduplication, security, access, robots/rate-limit, or review rules;
- may influence discovery priority only.

### Block controls

A block entry prevents future normal discovery/fetch/re-ingestion within its stated scope. Block reasons include:

- irrelevant/noisy source family;
- repeated low-value spam/SEO material;
- unsafe or abusive source;
- explicit owner exclusion;
- acquisition/access-policy issue;
- accepted takedown/prohibition;
- known removed work/mirror family that must not be re-ingested.

The block mechanism must support the **smallest practical scope** needed to avoid over-blocking, conceptually including one URL, URL/path pattern, host/domain, source family, or underlying work/content fingerprint. Exact matching technology belongs to architecture.

A takedown/prevention fingerprint is a stronger governed block state and remains subject to Stage 04/15 deletion rules.

Every allow/block decision is auditable and reversible unless a legal/security requirement says otherwise.

## 3.7 Reprocessing is explicit, scoped, and non-destructive

**Decision:** The owner must be able to request reprocessing without manually changing pipeline state.

The MVP supports reprocessing for a **selected record or affected scope**, with a reason such as:

- source version changed;
- improved OCR/ASR/parser/extraction method;
- corrected structural or answer relationship;
- taxonomy version/mapping changed;
- confidence/rights interpretation changed;
- duplicate/canonical decision changed;
- validation/regression incident requires replay;
- target-currentness/relevance evidence changed.

### Reprocessing rules

1. Reprocess from the **earliest affected conceptual stage**, not from the beginning by default.
2. Preserve the previous run/derivations and create a new auditable processing run/revision.
3. Preserve curator corrections/overrides unless they are explicitly superseded with rationale.
4. If a new automated result conflicts with a reviewed high-impact correction, keep the reviewed value active and surface the conflict for review.
5. Reprocessing may produce partial success; it does not erase unaffected valid outputs.
6. Takedown/prohibition states block ordinary reprocessing unless an authorized review/removal action specifically requires it.
7. Repeated unchanged-input/unchanged-method failure must not loop indefinitely; retry limits remain Stage 14/architecture.
8. Reprocessing must identify downstream analytics/blueprints/App capabilities that become stale or need recomputation.

### MVP versus later controls

MVP needs **single-record/small-scope reprocess** and the ability to replay a known affected batch/slice when a QA incident requires it. Rich bulk scheduling, dry-run simulations, large multi-stage reprocessing campaigns, rollback buttons, and automatic dependency graphs are later convenience features.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 MVP operations surface

The minimal complete operations experience has five areas.

| Area | MVP purpose | Required behavior |
|---|---|---|
| **Operations Inbox** | See what needs attention | Saved queue views, impact ordering, filters, age, state, affected scope, blocked capability |
| **Record / Review Detail** | Understand one issue | Source/provenance context, current structured data, relevant trust/rights/QA/dedup/taxonomy state, evidence links, history, safe actions |
| **Source Controls & Intake** | Govern what enters Corpus | Manual URL/file submission, source registry context, allow/block controls, known mirrors/dead sources, intake disposition |
| **Reprocessing & Change Actions** | Correct/recompute safely | Scoped reprocess, quarantine/restore, review decisions, takedown/prohibition action, affected-output visibility |
| **Corpus Health** | Know whether the system is maintainable and trustworthy | Actionable health vector, queue/backlog counts, QA/regression state, production eligibility, major coverage/independence gaps |

A separate navigation page for every queue is not required. Saved views over one operations surface are sufficient.

## 4.2 Discovery queue

### Purpose

Triage discovered/manual candidates before they create unnecessary processing cost or noise.

### Show at minimum

- candidate/source location and discovery route;
- first seen / last seen where known;
- source category and acquisition priority candidate;
- claimed provider/exam/CEFR and why the material appears relevant;
- format/asset type;
- known origin/mirror/alternate hints;
- current allow/block status;
- prior related source/material matches where available;
- ingestion decision and reason.

### Actions

- accept for ingestion;
- defer/keep as known lead;
- reject as irrelevant/low-value;
- mark duplicate/mirror lead to an existing source when obvious;
- add/update operator note;
- add an appropriately scoped allow/block control.

Rejecting a candidate does not imply low authenticity or prohibited rights; it is an operational relevance/cost decision.

## 4.3 Ingestion status view

### Purpose

Answer “what is happening to this source and why is it not published yet?” without inspecting jobs or storage manually.

### Show at minimum

- current conceptual stage(s) and active/latest processing run;
- successful, partial, held, retry, failed, review, and published scopes;
- first/last processing timestamps;
- current method/version where relevant;
- retry/reprocess state and latest failure reason;
- missing/blocked dependency;
- publication class and capabilities currently eligible;
- counts of affected Documents/Tasks/Items/Assets for a package where useful.

The view must preserve **partial success**. One failed audio alignment must not make an otherwise useful exam appear simply “failed.”

## 4.4 Extraction-failures view

### Purpose

Concentrate technical/data-quality exceptions that need a different method, manual correction, or intentional deferral.

### Include

- failure stage and smallest affected scope;
- normalized failure category;
- Q0–Q3 severity when the failure has a QA finding;
- extraction/input quality indicators;
- current and prior method/version attempts;
- whether the same failure repeats across a slice/provider/format;
- blocked downstream capability;
- recommended response: retry, reprocess with changed method, manual correction, keep partial/unknown, or defer.

Routine transient retries should not clutter the human queue until the automatic retry policy is exhausted or product impact justifies early review.

## 4.5 Duplicate-review view

### Purpose

Resolve ambiguous content identity/lineage only when the decision matters.

### Show at minimum

- candidate pair or cluster members;
- proposed relationship class and relation confidence;
- normalized/content/structure/media similarity evidence in human-readable form;
- meaningful side-by-side differences or changed tested propositions;
- source provenance, claimed edition/provider, confidence, and rights for each member;
- current canonical provenance anchor;
- current preferred processing representation;
- content occurrence/independence effect;
- whether the decision changes analytics, corroboration, or a benchmark record.

### Actions

- confirm exact/reformatted/derivative/fragment/related-variant/independent relationship;
- keep unresolved;
- change canonical provenance anchor;
- change preferred processing representation;
- correct cluster membership;
- trigger affected analytics/reprocessing.

All corrections are reversible/audited; Source Observations are never deleted merely because they are duplicates.

## 4.6 Authenticity review view

### Purpose

Resolve high-value uncertainty about what material is and how much influence it deserves.

### Show at minimum

- authenticity status and claimed origin;
- Stage 03 confidence tier/score and eight dimensions with Unknown/N/A visible;
- local versus inherited confidence;
- corroborating/contradicting evidence and independence state;
- answer/structure/language findings relevant to trust;
- current caps, dispute, quarantine, or review state;
- downstream uses affected by the decision;
- prior manual decisions and reclassifications.

### Actions

- accept/update authenticity status;
- adjust evidence-dimension assessment or documented tier cap/override;
- accept with restrictions/limited influence;
- mark review required/disputed;
- quarantine/reject as evidence;
- restore/reclassify previously quarantined material when evidence justifies it;
- trigger downstream reevaluation/reprocessing.

The operator does not change authenticity by editing a final score alone; the evidence/rationale must remain visible.

## 4.7 Rights review view

### Purpose

Decide what Bestehen may do with source expression and ensure restrictions propagate.

### Show at minimum

- public accessibility/acquisition context;
- observed license/permission/terms evidence and scope;
- current operational status: `REUSABLE`, `REUSABLE_WITH_CONDITIONS`, `REFERENCE_ONLY`, `UNKNOWN_REVIEW_REQUIRED`, or `PROHIBITED`;
- redistribution/derivative/commercial permissions and attribution/custom conditions;
- asset/component-level overrides;
- review/legal-review/takedown state;
- current source-expression and App capabilities affected;
- known mirrors/duplicates/derivatives relevant to the scope.

### Actions

- classify/reclassify status and action-level permissions with rationale;
- record conditions/attribution requirements;
- request/mark legal review required;
- place/release takedown hold when appropriate;
- mark prohibited/accepted removal scope;
- initiate affected-content discovery and required recompute/purge disposition.

Rights review never changes authenticity/confidence automatically.

## 4.8 Low-confidence-items view

### Purpose

Surface uncertain evidence that is potentially worth improving, without creating a mandate to review every C/D record.

### Default population

- C/D or materially Unknown local confidence that blocks a desirable capability;
- confidence downgrade/reclassification candidates;
- high-TELC-relevance records whose confidence is below the intended use gate;
- unique coverage-gap evidence that could become useful after one review;
- records whose local trust defect conflicts with a stronger parent source.

### Show

- current/local tier and dimensions;
- why the record is operationally important;
- source/parent context;
- missing/corroborating evidence;
- blocked capability;
- duplicate/rights/QA context that may make review pointless.

Low-value D-tier duplicates can remain safely unresolved indefinitely.

## 4.9 Taxonomy-corrections view

### Purpose

Keep the shared App/Corpus skill graph and assignment mappings trustworthy as extraction/classification improves.

### Show at minimum

- affected Task/Item and source evidence;
- current node(s), assignment role, confidence, origin, and taxonomy version;
- AI/deterministic candidate versus curated active assignment where they differ;
- related answer/skill/reasoning/distractor evidence needed to judge the mapping;
- whether the mapping is learner-impacting, analytics-only, or provisional;
- downstream nodes/analytics/blueprints affected by a change.

### Actions

- approve/reject a candidate assignment;
- remap to another active node;
- broaden to a trusted parent node;
- change assignment role where evidence supports it;
- retain provisional/review-required state;
- initiate governed node rename/merge/split/deprecation/retirement through the taxonomy governance workflow;
- request retag/reprocessing of the affected scope.

AI may suggest canonical taxonomy changes, but cannot publish them autonomously. Curated corrections remain authoritative across reruns until explicitly superseded.

## 4.10 Corpus health view

**Decision:** The personal-project MVP needs an **actionable health summary**, not a BI dashboard or single quality score.

The health view should answer four questions:

1. **Is work stuck?**
2. **Is production data trustworthy?**
3. **Are unresolved issues materially distorting intelligence or App consumption?**
4. **Where is coverage or freshness weak enough to justify owner attention?**

### A. Operational backlog and pipeline health

Track at minimum:

- discovered/deferred/accepted candidates;
- active/partial/held/retry/reprocess/failure states;
- review backlog by queue and high-impact priority;
- oldest high-impact actionable issue;
- records repeatedly failing the same method/slice;
- stale/recompute-pending outputs after a material change.

### B. Production eligibility and governance health

Track:

- normal eligible / limited-provisional / held counts by important capability;
- quarantined, disputed, prohibited, and takedown-hold populations;
- unknown/review-required rights population relevant to proposed direct use;
- low-confidence population relevant to App priorities/generation;
- unresolved correctness/structure findings that block production use.

### C. QA quality vector

Expose Stage 10 metrics without blending them into one score:

- structural extraction qualification/defects;
- answer/key/scoring-link precision/regression state;
- high-impact taxonomy precision/regression state;
- meaning-critical OCR/ASR fidelity issues;
- required-metadata completeness;
- critical asset/audio-link integrity;
- duplicate auto-collapse/regression health;
- Q0/Q1 manual-sample findings by important slice;
- benchmark/gold qualification status and current regression pass/fail.

### D. Independence and analytics health

Track:

- unresolved duplicate/dependency cases that materially widen decision-grade analytics;
- analytics/relevance results awaiting recomputation after trust/dedup/taxonomy/currentness changes;
- source/provider concentration or evidence-sufficiency warnings that prevent decision-grade use;
- count of decision-grade versus exploratory pattern outputs where useful.

### E. Coverage/freshness health

Track only the coverage dimensions already defined by earlier stages, especially:

- provider × CEFR × Section coverage;
- task/format/media gaps that limit target intelligence;
- benchmark-slice coverage gaps;
- missing/weak Listening/Speaking assets or other strategically important source gaps;
- target-currentness/freshness warnings for TELC-critical evidence.

### Health-display rule

The MVP may present counts, tables, status labels, and a few trend indicators. Charts are optional. **No scalar “Corpus health = 87%” may override a hard Q0/Q1, rights, quarantine, correctness, or regression failure.**

---

## 5. Edge Cases / Failure or Uncertainty Handling

### 5.1 Queue backlog becomes large

Do not turn every pending item into urgent work. Sort by product impact, preserve low-impact records as provisional/held, and improve automation only where repeated backlog creates measurable maintenance cost.

### 5.2 Owner disagrees with an automated result

The owner records a curated correction with rationale/evidence. The automated result remains in derivation history. Future reruns may propose a different candidate but cannot silently overwrite the correction.

### 5.3 Owner later learns the manual correction was wrong

Create a superseding curated decision. Do not erase the earlier correction; history should explain why downstream intelligence changed.

### 5.4 One source has hundreds of repeated low-value extraction failures

The owner can block/defer the source or keep it partial rather than reviewing every failure. Unique high-value Tasks/Assets may still be salvaged locally.

### 5.5 Rights takedown affects a duplicate family

Place the affected work/scope on hold, use duplicate lineage to identify known mirrors/variants, block accidental re-ingestion, and follow Stage 04’s raw-expression versus non-reconstructive-data disposition. Do not merely delete one URL.

### 5.6 Reprocessing produces worse data

Do not automatically replace a reviewed/last-known-good output when qualification/regression or local validation fails. Keep the prior eligible version active where product semantics permit and mark the candidate run failed/limited/review-required.

### 5.7 Taxonomy version splits one node into two

The operations surface shows the migration impact and affected mappings. Historical assignments are preserved. Reprocessing/retagging may reduce certainty until direct evidence supports the new children; it must not manufacture learner mastery.

### 5.8 Duplicate decision changes independent evidence count materially

Flag the case as high-impact, recompute affected analytics/relevance/blueprints, and surface the downstream change. Do not require the owner to identify dependent analytics manually.

### 5.9 A direct App source item is invalidated

Operations should show that direct-source eligibility/correctness is affected and identify downstream App capability scope according to Stage 12. App owns repair of learner history, but Corpus supplies the invalidated identity/revision/reason.

### 5.10 The admin tool itself cannot represent a governed action

Do not fall back to raw-row editing as the normal workflow. The missing action becomes the next minimum operations capability, or the record remains safely held until the action can be represented.

---

## 6. Relationship to Other Bestehen Stages

### Stage 14 — Cost, Scale, and Automation

Stage 14 should quantify volume, retry limits, AI/model tiers, batching, storage expectations, and processing cost. Stage 13 supplies the operator surfaces through which those policies are observed and manually overridden. Exact backlog thresholds, retry counts, and batch size are intentionally not invented here.

### Stage 15 — Security and Abuse

Stage 15 owns authentication/authorization, safe untrusted-file handling, URL/content sanitization, secrets, internal-tool permissions, raw-file retention, and abuse handling. Stage 13 assumes an owner-only internal surface but does not define the security implementation or permission model.

### Stage 16 — Benchmark Corpus

Stage 16 will create the concrete benchmark/gold records whose QA and regression status Stage 13 exposes. Gold-record changes require explicit, auditable review.

### Stage 17 — Final Corpus PRD

The final PRD should treat Stage 13 as the authoritative maintainability/operations contract: Corpus is not complete if its states are theoretically correct but cannot be safely reviewed and changed without direct database editing.

### Relationship to Bestehen / App

The operations surface remains internal. Its App-facing role is to make Corpus eligibility trustworthy and to expose impact when an App-consumable pattern/content revision becomes invalid, restricted, superseded, or recomputed. It does not become a learner-support or content-authoring UI.

---

## 7. Cost Notes

Stage 13 itself should have **low recurring compute cost**. Its main cost is owner time and whatever engineering effort is spent making safe actions available.

### 7.1 Preferred low-cost default

- no bespoke visual analytics dashboard initially;
- one table/detail operations surface with saved views;
- reuse existing stored pipeline/trust/rights/QA/dedup/taxonomy metadata rather than compute a second monitoring model;
- incremental/precomputed health counts rather than expensive live analytical recomputation for every page view;
- manual review only for high-impact ambiguity;
- deterministic/local evidence and existing derivations shown to the operator before any premium-model assistance;
- no multi-user workflow, assignments, comments, approval chains, or notification system initially;
- no premium AI required just to summarize queues or health.

### 7.2 Premium-model use

A stronger paid model may be invoked **explicitly and rarely** from a review flow when deterministic checks, cheaper methods, and source evidence cannot resolve a high-impact case such as:

- correctness/scoring ambiguity;
- difficult OCR/ASR on answer-critical TELC evidence;
- high-impact duplicate/derivative ambiguity;
- unusual taxonomy mapping affecting learner diagnosis;
- difficult provenance/authenticity evidence synthesis.

The result remains a review candidate unless the owning stage’s benchmarked auto-accept rule permits otherwise.

### 7.3 Cheapest fallback

If a high-cost ambiguity is not worth resolving, keep the record conservative: provisional, limited, unresolved, quarantined, or held as appropriate. **“Do not spend money; do not promote the evidence” is a valid product outcome.**

### 7.4 What would justify a richer operations product later

Invest in a more polished/custom dashboard only when measured owner burden justifies it, for example:

- review volume makes table-based triage slow;
- repeated bulk corrections/reprocessing consume significant time;
- multiple operators need assignments/permissions/collaboration;
- trend analysis is needed to diagnose systematic pipeline regressions;
- source volume makes coverage/freshness impossible to reason about from compact health summaries;
- operational incidents require alerts rather than periodic owner review.

---

## 8. MVP Must-Haves vs Deferred Convenience Features

| Capability | MVP / must-have | Deferred convenience |
|---|---|---|
| Operations Inbox | Queue filters, impact sorting, age, affected capability | Saved personal layouts, advanced search language, keyboard triage |
| Discovery | Candidate triage, manual URL/file intake, allow/block | Automated recommendations for coverage gaps, bulk source campaigns |
| Ingestion/failures | Current/partial state, failure reason, retry/reprocess visibility | Rich pipeline timeline visualization, notifications |
| Review detail | Evidence/provenance/state/history + explicit actions | Embedded rich PDF/audio diff workbench, collaborative comments |
| Duplicate review | Pair/cluster differences, relation decision, canonical choices | Advanced visual cluster explorer, bulk cluster editing |
| Authenticity/rights | Evidence and separate governed decisions | AI-generated review memos, external legal-workflow integration |
| Taxonomy correction | assignment review/remap/broaden + governed node workflow | Bulk taxonomy editor, interactive graph visualization |
| Manual editing | smallest-scope curated corrections/overrides | Spreadsheet-style mass editing/import |
| Audit history | append-only old/new/rationale/actor/run history | Rich side-by-side revision browser and one-click rollback UI |
| Reprocessing | selected scope and QA-incident slice replay | Large scheduled campaigns, dry runs, dependency visualizer |
| Corpus health | actionable counts/status/quality vector/coverage warnings | Custom BI dashboards, long-term trend analysis, alerts |
| Collaboration | one owner | roles, assignments, approvals, comments, SLAs |

---

## 9. Decisions Made

1. A polished custom internal dashboard is **not required** for the personal-project phase; a minimal governed operations surface **is required**.
2. The cheapest acceptable product is a table-and-detail operations console that can be implemented with existing/admin tooling later, provided ordinary maintenance never depends on raw database-row editing.
3. The MVP uses one prioritized Operations Inbox with saved views for discovery, ingestion, extraction failures, duplicate review, authenticity review, rights review, low-confidence records, and taxonomy corrections.
4. Review order is impact-based rather than FIFO; low-impact provisional backlog may remain unresolved indefinitely.
5. Manual editing creates smallest-scope curated corrections/overrides/status decisions and never silently rewrites source truth.
6. Human-reviewed corrections remain authoritative across automated reruns until explicitly superseded.
7. Consequential human and automated changes require visible append-only audit history, even with one owner.
8. Source allow/block lists are required and are explicitly separate from authenticity, confidence, rights, and validation.
9. Block controls can conceptually target URL/path, host/domain, source family, or underlying-work/fingerprint scope; takedown prevention is a stronger governed block state.
10. Reprocessing is explicit, scoped to the earliest affected stage, non-destructive, versioned, and must identify downstream recomputation/eligibility impact.
11. The corpus-health view is a quality/action vector—not one scalar score—and covers operational backlog, production eligibility/governance, Stage 10 QA/regression, independence/analytics health, and strategic coverage/freshness.
12. Manual URL/file intake, source controls, review actions, reprocessing, and health visibility are all part of the MVP operations surface.
13. Multi-user workflow, rich dashboards, alerts, bulk editing, advanced visualization, large reprocessing campaigns, and collaboration are deferred convenience features.
14. Stage 13 adds little recurring compute cost; premium-model assistance is rare, explicit, high-impact-only, with conservative hold/provisional state as the cheaper fallback.

---

## 10. Open Questions / Deferred Decisions

### 10.1 Owner questions

**None.** The existing project principles strongly favor a minimal one-owner operations surface over either direct database editing or a costly custom admin product.

### 10.2 Deferred architecture / implementation decisions

The following remain intentionally open:

- admin UI/framework or low-code product choice;
- whether the MVP lives inside an existing database/admin interface or a small dedicated internal web app;
- database/storage/schema details;
- queue/workflow/job-runner implementation;
- authentication/authorization and internal-tool permissions — Stage 15;
- concrete retry counts, batch sizes, automation budgets, and cost caps — Stage 14;
- polling versus event-based refresh/change propagation;
- exact bulk reprocessing mechanism;
- search/index technology;
- embedded PDF/image/audio comparison components;
- notification/alerting channels;
- analytics/BI/charting library;
- exact rollback implementation.

### 10.3 Deferred convenience decisions

Do not shape multi-user assignment, comments, approvals, review SLAs, notification preferences, mobile admin, or sophisticated dashboard layout until real owner burden demonstrates a need.

---

## 11. Definition of Done Check

- [x] The internal-dashboard requirement is decided: minimal operations surface required; bespoke dashboard deferred.
- [x] The cheapest acceptable personal-project alternative is defined.
- [x] Discovery queue/view is defined.
- [x] Ingestion status view is defined.
- [x] Extraction-failures view is defined.
- [x] Duplicate-review view is defined.
- [x] Authenticity-review view is defined.
- [x] Rights-review view is defined.
- [x] Low-confidence-items view is defined.
- [x] Taxonomy-corrections view is defined.
- [x] Manual editing capabilities and guardrails are defined.
- [x] Audit-history requirements are defined.
- [x] Source allow/block controls are defined.
- [x] Reprocessing controls are defined.
- [x] Corpus-health metrics/views are defined.
- [x] MVP must-haves are separated from deferred convenience features.
- [x] Cost-sensitive defaults and premium-model escalation rules are documented.
- [x] No Stage 13 owner blocker remains unresolved.

**Stage 13 is product-complete when one owner can understand what needs attention, make every high-value maintenance decision through governed actions, and trace the result without direct database surgery or a custom enterprise-grade dashboard.**
