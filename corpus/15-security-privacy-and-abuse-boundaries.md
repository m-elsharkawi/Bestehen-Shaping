# Bestehen / Corpus — Stage 15: Security, Privacy, and Abuse Boundaries

> **Status:** Authoritative Stage 15 product-shaping decision  
> **Product:** Bestehen / Corpus  
> **Primary operator:** One owner in the personal-project phase  
> **Primary downstream customer:** Bestehen / App  
> **Core principle:** Corpus may ingest broad and imperfect external evidence, but every external file, URL, archive, page, and media asset is untrusted input. The launch product minimizes personal data, prevents source content from gaining execution or internal authority, keeps secrets and raw evidence separated from downstream consumers, and uses simple bounded controls rather than an enterprise security program.

---

## 1. Purpose and Scope

Stage 15 defines the minimum non-functional product boundaries required to operate Bestehen / Corpus safely when it accepts arbitrary external URLs and files from official sites, publishers, teachers, repositories, archives, unofficial collections, forums, shared documents, and owner-supplied material.

The goal is **not** to design an enterprise security platform. Bestehen is initially a personal, internal-first project with one owner. The goal is to make the dangerous assumptions explicit before architecture begins:

- Corpus source content is evidence, not trusted code or trusted instructions;
- supported file types are data formats, not permission to execute active content;
- external URLs must not become a route into private/internal infrastructure;
- raw source material may contain malware, malicious markup, prompt injection, tracking links, credentials, or incidental personal data;
- source material must not gain access to Corpus secrets, internal tools, operator sessions, or learner data;
- the Corpus → App boundary should expose only published, eligible outputs rather than raw internal storage;
- manual submission is owner-only at launch, so public-upload abuse controls should not be paid for before they are needed;
- raw evidence is retained when it materially supports provenance, QA, reprocessing, rights, or benchmark needs, but rejected, unsafe, or prohibited material should not accumulate indefinitely.

This document defines **product behavior and guardrails**, not implementation architecture. It does not choose a sandbox product, antivirus engine, secret manager, authentication library, network topology, storage encryption implementation, CSP configuration, reverse proxy, cloud provider, or monitoring vendor.

### 1.1 Stage objective

**Bestehen / Corpus should be safe enough for one owner to ingest broad public and manually supplied exam evidence without treating the internet as trusted, without creating a learner-personal-data store, and without introducing enterprise-grade cost or operational burden before the product has public users or multiple operators.**

### 1.2 Security is a cross-cutting gate, not a second ingestion pipeline

Stage 08 established the conceptual lifecycle:

**Discover → Fetch → Normalize → Parse → Segment → Classify → Extract Answers → Extract Assets → Enrich → Validate → Deduplicate → Review → Publish**.

Stage 15 does **not** replace that lifecycle with a separate security workflow. Security requirements apply across it:

- **before/at Fetch:** URL, domain, redirect, protocol, access-policy, size, and destination safety;
- **at Normalize:** file type, archive containment, active-content handling, member inventory, and unsafe-payload screening;
- **at Parse/Enrich:** source content is treated as untrusted data, not executable instructions; external-model processing follows rights/privacy restrictions and receives no secrets;
- **at Review:** operators view sanitized/non-executing representations and use explicit governed actions;
- **at Publish:** only eligible structured outputs leave Corpus; unsafe or restricted raw expression is not exposed merely because extraction succeeded;
- **throughout:** secrets, permissions, audit history, retention, deletion, and block/tombstone states remain enforceable.

A record can be structurally valid, authentic, reusable, and still be blocked for security. Equally, a security-clean file does not gain authenticity, rights, or analytical value.

---

## 2. Inputs / Existing Decisions

Stage 15 preserves the shared Product Overview, Identity, both live shaping checklists, and Corpus Stages 01–14.

### 2.1 Stage 01 — internal-first boundary

`corpus/01-product-mission-and-boundaries.md` established that Corpus is initially internal-only, serves Bestehen / App plus the owner/operator, and is not a public exam-file mirror, public API, multi-tenant service, or learner-facing application.

That substantially reduces the launch attack surface and is intentionally preserved.

### 2.2 Stage 02 — broad source intake without access circumvention

`corpus/02-source-strategy.md` established support for HTML, PDF, DOC/DOCX, images/scans, audio, video, ZIP/archive material, automated discovery, manual URL intake, and manual file intake. It also established:

- no bypassing authentication, paywalls, bot protection, access controls, or private-group boundaries;
- public shared documents are candidates only when reachable without requesting special access;
- lawfully possessed gated material can be manually supplied by the owner rather than requiring automated credentialed crawling;
- mirrors, dead URLs, and provenance remain traceable.

Stage 15 treats every one of those formats and origins as untrusted from a security perspective.

### 2.3 Stage 03 — quarantine is about evidence trust, not malware safety

Stage 03 defines authenticity/confidence and a reversible evidence `Quarantine` state. Security quarantine can coexist with it but is a different reason. A file suspected of malware may be security-blocked even if its exam provenance is credible; a fake exam can be evidence-quarantined even if its bytes are technically harmless.

### 2.4 Stage 04 — rights, takedown, and removal

`corpus/04-rights-and-usage-metadata.md` established conservative rights states, immediate takedown holds, component-level removal, and preservation of non-reconstructive intelligence where permitted.

Stage 15 does not turn rights decisions into security decisions. It adds the requirement that a takedown/prohibited source also becomes a strong re-ingestion block where needed, and that deleted content must not silently return from cache, retry, backup restore, or a mirror.

### 2.5 Stages 05–07 — localize risk to the affected component

The canonical model keeps Documents, Tasks, Items, Stimuli, Answers, Assets, and source observations separately addressable. Confidence, rights, taxonomy assignments, and difficulty/relevance already operate at the smallest useful scope.

Security/removal should follow the same principle where safe: one malicious archive member or unsafe external asset does not automatically invalidate unrelated already-extracted safe metadata, but the affected payload and dependent uses are held until the relationship is understood.

### 2.6 Stage 08 — successful fetching does not imply safety

Stage 08 explicitly states that Fetch success does not imply safety, authenticity, completeness, or rights. Stage 15 supplies the missing safety rules while keeping partial failure and bounded retry behavior intact.

### 2.7 Stage 10 — governance failures can be Q0 blockers

Stage 10 defines Q0 findings for hard governance failures and requires the smallest affected use to be held. A security gate failure that could expose secrets, internal infrastructure, unsafe active content, prohibited data, or learner-facing raw material is therefore a production blocker for the affected path.

### 2.8 Stage 12 — Corpus and App remain separated

Stage 12 established a capability-oriented contract and a pattern-first App relationship. App should not rebuild ingestion, trust, rights, deduplication, or governance logic.

Stage 15 adds one explicit boundary: **Bestehen / App does not receive direct access to Corpus raw-source storage or internal operations tooling.** If App legitimately needs exact reusable reference content, it receives a specifically published, capability-eligible representation through the Corpus contract—not unrestricted access to the raw evidence store.

### 2.9 Stage 13 — one-owner operations, audit, and source controls

Stage 13 requires an authenticated owner-only operations surface, append-only audit history, safe governed actions, source allow/block controls, and stronger takedown/prevention fingerprints. Stage 15 defines the security-specific meanings and minimum permissions those capabilities must enforce.

### 2.10 Stage 14 — cheap-first processing and bounded crawling/storage

Stage 14 established:

- deterministic/local processing first;
- selective external/paid processing;
- no external processing when Stage 04 does not permit raw source expression to leave the allowed boundary;
- bounded retries;
- one concurrent request per host and a default ceiling of 0.5 requests/second unless a source explicitly supports otherwise;
- no bypass of login, CAPTCHAs, private groups, paywalls, bot protections, or rate limits;
- a 200-new-URL default discovery-run ceiling for an unreviewed host;
- explicit value/retention review for a single file larger than 250 MB;
- normal base-envelope storage up to roughly 150 GB before storage-growth review.

Stage 15 keeps those cost/etiquette limits and adds safety controls; it does not create a second crawling budget.

No earlier product decision needs to be reversed.

---

## 3. Decisions and Rationale

## 3.1 Corpus deliberately has a near-zero learner/personal-data footprint

**Decision:** Bestehen / Corpus is **not a learner-data product** and must not store learner accounts, learner profiles, learner attempts, learner writing, learner voice, learner readiness, learner mistake history, device identifiers, advertising identifiers, or learner analytics as part of its product model.

Those belong to Bestehen / App where required by the App product.

The Corpus → App contract is intentionally asymmetric: App may request exam-pattern intelligence, but Corpus does not require personal learner state to answer.

### Minimal personal data that may still appear

Three narrow categories can exist:

1. **Operator/audit identity** — enough to distinguish the owner’s curated action from automation, such as an internal actor identifier plus timestamps and rationale. The product does not need a rich employee/person profile.
2. **Source attribution/provenance** — public author, teacher, publisher, organization, or rights-holder identity where it is genuinely needed to explain origin, attribution, permission, or takedown history.
3. **Incidental personal data inside source content** — a forum post, shared document, scan, exercise, screenshot, metadata field, or archive may contain names, usernames, email addresses, phone numbers, document authors, or other personal information that Corpus did not seek.

### Data-minimization rule

Corpus should keep only personal information that is **necessary for provenance, rights/attribution, security/audit, or faithfully representing exam-relevant source evidence**.

It should not:

- build profiles of source authors or forum users;
- enrich identities from other data sources;
- extract personal contact details into the taxonomy or analytics merely because they are visible;
- use incidental personal data as a search/discovery target;
- expose source personal data to App unless exact eligible reference content genuinely requires it and the rights/privacy gate permits that use.

When a name, email, username, phone number, address, tracking token, or other personal value is irrelevant to exam intelligence, derived/normalized representations should omit or redact it where practical rather than multiplying it across the Corpus.

**Important:** redaction of a derived representation does not silently modify source truth. The raw source may remain retained under the raw-file rules when needed and permitted, with the derived sanitized form used for ordinary operations/AI/analytics.

## 3.2 Every external input is untrusted data

**Decision:** No source is security-trusted merely because it is official, reputable, public, high-confidence, or manually supplied by the owner.

The security posture is the same for:

- official provider PDFs;
- publisher DOCX files;
- teacher-created ZIPs;
- archive downloads;
- public forum links;
- shared documents;
- audio/video;
- manually uploaded files;
- source HTML and redirects.

Source trust from Stage 03 answers “is this useful exam evidence?” Security answers “can this input safely pass through this operation?” They remain independent.

## 3.3 Supported formats are never executed as active content

**Decision:** Corpus supports source formats for **inspection and extraction**, not for executing source-provided code, macros, scripts, plugins, forms, embedded programs, or arbitrary binaries.

At launch:

- Office macros and embedded active content are not executed;
- PDF/HTML/office-file scripts are not trusted execution paths;
- archive members are not executed;
- source-provided binaries/installers are outside the supported Corpus content model even if bundled with exam files;
- embedded links do not automatically gain fetch permission merely because a document contains them;
- source content must never run with access to Corpus secrets, owner sessions, internal storage, or private network resources.

If visual rendering is required to understand layout, the product requirement is that rendering be **non-privileged and isolated from secrets/internal authority**. The exact sandbox/rendering technology belongs to architecture.

## 3.4 Security preflight is required before deep/expensive processing

**Decision:** Before a newly fetched or manually submitted payload reaches expensive OCR/ASR/semantic processing, Corpus must perform a cheap safety/intake preflight appropriate to the format.

Conceptually the preflight checks:

- allowed acquisition protocol/source route;
- URL/destination safety where applicable;
- declared type versus detected file/content type;
- basic file/container integrity;
- gross size and resource-amplification risk;
- archive member inventory before recursive extraction;
- unexpected executables/active-content indicators;
- known-malicious-file screening using a low-cost/local method where practical;
- duplicate/content fingerprint lookup before repeated deep processing;
- source/domain block/takedown/security state;
- whether the content is clearly out of the exam-domain scope.

**Product stop rule:** when the preflight cannot safely classify or bound the payload, the correct state is **hold/review/defer**, not “try every parser/model until something opens it.”

A premium malware-analysis service is not a launch requirement. Architecture may start with free/local/platform capabilities and upgrade only if risk/volume justifies it.

## 3.5 Archives require bounded expansion

**Decision:** ZIP/archive support remains in scope, but archive expansion is deliberately bounded.

The product requires limits on:

- aggregate expanded size;
- number of members;
- nesting depth;
- pathological compression/expansion ratio;
- duplicate/repeated members;
- path traversal or extraction outside the intended working scope;
- links/special files that could reference unexpected filesystem locations;
- encrypted/password-protected members that cannot be safely inspected automatically.

The exact numeric thresholds are implementation calibration, with one established Stage 14 guardrail: a raw file larger than 250 MB already requires an explicit value/retention decision. Security limits may be stricter for automatic expansion if architecture determines that is necessary.

**Default behavior:** an encrypted, unexpectedly huge, deeply nested, or structurally suspicious archive is held for owner review; Corpus does not brute-force passwords or recursively expand without bound.

## 3.6 URLs are limited to safe web retrieval, not arbitrary network access

**Decision:** Automatic source retrieval at launch is for **HTTP/HTTPS web content** only. A manually entered “URL” is not a generic network instruction.

Normal automated fetching must reject or require explicit governed handling for:

- local-file or application schemes;
- executable/script schemes such as `javascript:`;
- embedded-data schemes as a source-fetch route;
- local network shares and non-web protocols;
- URLs containing embedded credentials;
- destinations resolving to loopback, link-local, private/internal infrastructure, cloud/service metadata endpoints, or other non-public network targets;
- redirects that cross into a blocked/unsafe destination;
- source URLs/hosts currently blocked by security, takedown, access policy, or operator decision.

**Redirect rule:** destination safety is re-evaluated after redirects; a safe-looking public URL does not receive permanent permission to redirect to an internal or prohibited target.

Architecture may choose the exact SSRF/DNS-rebinding protections, but it must preserve the product outcome: **source submission cannot be used to make Corpus reach private/internal services.**

## 3.7 HTML and rich content are sanitized for operations and downstream processing

**Decision:** Corpus treats source HTML/rich text as source expression, not as trusted UI.

For ordinary operations/review:

- source markup is escaped, sanitized, rendered as inert content, or shown through another non-executing representation;
- scripts, event handlers, forms, embedded active frames/plugins, and equivalent active behaviors do not execute in the privileged operations context;
- external images/media/links do not automatically load merely because a record is viewed if that would create tracking or unsafe retrieval;
- links remain visibly attributable to their actual destination and follow the same source-fetch policy when Corpus chooses to fetch them;
- extracted plain text/structured layout is preferred for routine review when exact live rendering is unnecessary.

If an operator explicitly opens the original external source in a normal browser, that is outside the guarantee of the Corpus operations surface; the product should distinguish that action from viewing sanitized internal evidence.

## 3.8 Source text is untrusted instruction content for AI/model processing

**Decision:** Any model used for extraction, classification, semantic enrichment, or adjudication must treat source text as **data to analyze**, never as authority to change Corpus behavior.

External source content may contain instructions such as “ignore previous rules,” requests to reveal secrets, links to fetch, commands to modify records, or tool-use instructions. Those are content, not product commands.

Therefore source-derived model output must not, by itself:

- trigger arbitrary new network requests;
- reveal or request credentials/secrets;
- change source allow/block/security policy;
- approve rights/legal reuse;
- delete records;
- override human-curated decisions;
- publish learner-facing content;
- cause arbitrary code/tool execution.

AI output remains a derived assertion subject to the Stage 08/10 validation and human-override rules.

**Secrets rule:** models processing source content never receive Corpus/API secrets merely because the model environment can technically access them. If external model processing is used, Stage 04 rights and this stage’s privacy/data-minimization rules must allow the content to leave the local processing boundary.

## 3.9 Domain/source blocking uses security reasons in addition to relevance/rights reasons

**Decision:** The Stage 13 allow/block system must support security-specific reasons without collapsing them into trust or rights.

### Security hard-block reasons

Normal automatic fetch/re-ingestion is blocked for a URL/host/path/source family/fingerprint when applicable because of:

- known or strongly suspected malware/hostile payload delivery;
- phishing/credential-harvesting behavior;
- repeated redirects to unsafe/private/internal destinations;
- deliberate attempts to exploit the ingestion/review environment;
- a security incident linked to that source/work;
- accepted takedown/prohibition requiring prevention of re-ingestion;
- a source route requiring access-control circumvention;
- grossly out-of-scope abusive/spam payloads whose only effect is operational cost/risk.

### Ordinary block reasons remain valid

Stage 13’s existing reasons—irrelevant/noisy source, spam/SEO material, explicit owner exclusion, acquisition-policy issue, takedown, or known removed work—remain unchanged.

### Allowlist rule

Being on an allowlist affects discovery priority/permission to consider a source. It **never bypasses** URL destination safety, file safety, rights, confidence, validation, deduplication, crawling etiquette, cost limits, or takedown state.

### Override rule

An owner may reverse an ordinary block through an audited decision. Re-enabling a source blocked for a security incident, malware, or takedown requires an explicit reviewed rationale; it must not happen as a side effect of a later crawl or confidence upgrade.

## 3.10 Secrets are separated from source data and minimized

**Decision:** Corpus stores and uses only the credentials needed to operate the product; source processing must not turn them into source-visible data.

Product requirements:

- API keys, database credentials, signing secrets, access tokens, service credentials, session cookies, and similar values are not stored in source records, source notes, prompts, URLs, logs, analytics, exported datasets, or human-review text fields;
- logs and error messages must avoid exposing secret values;
- credentials are scoped to the minimum service/action practical and can be revoked/rotated independently;
- automated source-processing workers receive only the credentials needed for their job and cannot use owner-level operational authority by default;
- a source document or web page cannot request or cause secret disclosure;
- secrets used by Bestehen / App are not exposed to Corpus source-processing tasks merely because both products belong to Bestehen;
- third-party website passwords/cookies are **not** a launch requirement for crawling.

### Authenticated/gated source default

Where the owner lawfully possesses paid/account-gated material, the low-risk launch path remains **manual file submission** as established in Stage 02.

Automated authenticated crawling that stores third-party session credentials/cookies is deferred. Introducing it is a later-hardening trigger because it materially changes the secret and account-risk model.

### Secret-management level

A dedicated HSM, enterprise vault, or custom key-management program is not required for launch. Architecture should use the selected platform’s normal secure secret mechanism where available and keep secrets out of source data/config committed to the repository.

## 3.11 Internal permissions are simple but explicit

**Decision:** Bestehen does not need enterprise RBAC at launch, but it does need three distinct authority boundaries.

| Actor / consumer | Launch authority | Explicitly not allowed by default |
|---|---|---|
| **Owner / curator** | Authenticated access to the internal operations surface; can review, correct, block, reprocess, quarantine, manage rights/trust decisions, and perform governed deletion/takedown actions | No bypass of audit history; high-impact/destructive actions must remain explicit rather than hidden side effects |
| **Automated Corpus workers/models** | Process assigned inputs, create derived results/findings, propose classifications, and execute explicitly allowed pipeline actions | Cannot silently override human-curated decisions; cannot weaken security/takedown blocks; cannot grant themselves broader credentials; cannot perform arbitrary deletes or unrestricted network/tool actions |
| **Bestehen / App** | Read/consume published Corpus contract outputs needed for learner-facing product behavior | No access to raw source storage, ingestion queues, operator controls, secrets, unpublished/quarantined material, or arbitrary Corpus database writes |

### High-impact action guardrail

Even with one owner, actions such as raw purge, takedown/prohibition, restoring a security-blocked source, or changing an eligibility state that could expose previously held content must be deliberate, audited operations. A second-person approval workflow is not required in the personal-project phase.

### Future multi-user trigger

If a second human operator receives write access, Stage 15 should be revisited to define explicit role separation such as read-only reviewer, curator, rights/security administrator, and destructive-action permission. Launch does not pay that complexity early.

## 3.12 Raw source retention is value-based and risk-aware

**Decision:** Corpus retains accepted raw evidence **for as long as it materially supports provenance, QA, reprocessing, benchmark, dispute resolution, or rights obligations and retention remains permitted**, while aggressively avoiding indefinite retention of rejected/unsafe noise.

There is no one fixed retention duration for all source bytes because a verified benchmark PDF and a malicious rejected archive have opposite product value.

### Launch retention classes

| Raw material class | Launch retention expectation |
|---|---|
| **Accepted, unique, useful Corpus source** | Retain long-term while it supports provenance/reprocessing/QA/rights/benchmark needs and current policy permits retention. No automatic short expiry in the normal ≤150 GB Stage 14 base envelope. |
| **Accepted exact/reformatted duplicate bytes** | Physical byte duplication is unnecessary; retain one content object conceptually plus every provenance/source observation. |
| **Temporary extraction/render/transcode intermediates** | Delete after successful validation when safely regenerable and not needed for audit/debug/benchmark evidence. |
| **Rejected or clearly irrelevant manual/file intake** | Delete the raw payload promptly after disposition; target **within 7 days** unless a short security investigation or duplicate/takedown fingerprint need justifies retaining it briefly. Keep minimal non-content provenance/rejection metadata when useful. |
| **Security-suspicious or malicious payload** | Keep isolated only as long as needed to confirm/disposition the incident; target removal of the full payload **within 7 days** after disposition unless a deliberate security investigation requires longer. Preserve a minimal hash/tombstone/source/reason record where lawful and useful to prevent re-ingestion. |
| **Rights-prohibited / accepted takedown content** | Block use immediately. Remove active raw/reconstructive content according to the Stage 04 takedown decision; target active-store deletion **within 7 days** when deletion is required/permitted. Preserve only the minimum non-reconstructive provenance, audit, request, and prevention fingerprint allowed by policy. |
| **Incidental unnecessary personal data discovered in a source** | Prefer sanitized derived representations. If the raw source no longer has sufficient provenance/QA value to justify retention, delete it under the relevant class; if raw retention remains necessary, restrict normal exposure and avoid copying the personal data into derived outputs. |

### Why accepted raw evidence is retained long-term initially

Corpus is an evidence product. The ability to verify extraction, re-run improved parsers, resolve answer/provenance disputes, prove source lineage, and construct Stage 16 gold records has real product value. At the Stage 14 base envelope, keeping one unique raw copy is cheaper and safer for correctness than discarding every accepted source immediately and depending on unstable URLs.

This is reassessed when Stage 14 storage triggers are crossed or when a new privacy/rights/security risk changes the cost-benefit balance.

### Deletion invariants

- Deleting raw bytes does **not** erase provenance history unless policy requires that too.
- A minimal tombstone/fingerprint may remain to prevent accidental re-ingestion where legally/security-appropriate.
- Deleted/prohibited source expression must not be restored to active use merely because it exists in a backup, cache, mirror, derived artifact, or later crawl.
- The exact backup lifecycle and physical deletion mechanism belong to architecture, but restoration behavior must respect the current deletion/takedown state.
- Non-reconstructive derived metadata may remain only when Stage 04/privacy/security rules allow it.

## 3.13 Manual submissions are owner-only at launch

**Decision:** Manual URL/file submission is required, but the launch product has **no anonymous or general-public submission endpoint**.

The owner can manually submit:

- a public URL;
- a lawfully obtained local file;
- a source bundle/asset needed to complete known evidence.

Manual submission does not bypass any normal gate. The same URL, file, archive, rights, confidence, security, size, duplicate, cost, and review rules apply as for automated discovery.

### Manual-submission abuse behavior

If a submitted item is:

- irrelevant/spam → reject, avoid expensive processing, optionally block noisy source patterns;
- duplicate → fingerprint/reuse existing derivations rather than reprocess;
- malicious/suspicious → security hold, isolate, no active rendering/execution, block/fingerprint as appropriate;
- attempting credential/internal-network access → reject/block the destination/path;
- rights/takedown prohibited → do not re-ingest active content; preserve the prevention state;
- malformed or resource-amplifying → hold/defer rather than repeatedly retry;
- high-value but uncertain → preserve as reviewable evidence without elevating trust or rights.

The owner being the submitter is not evidence that the payload is safe or authentic.

## 3.14 Public submissions are a future product boundary, not a hidden MVP feature

**Decision:** If Bestehen later accepts submissions from other people, that is a material product change and requires Stage 15 review before launch of that capability.

At minimum, public/multi-user submission would require decisions/controls for:

- authenticated or otherwise attributable submitters;
- rate limits and storage/processing quotas;
- per-submission file-size/archive limits;
- automated malicious-file screening appropriate to public uploads;
- moderation/rejection/reporting flows;
- submitter metadata and privacy/retention policy;
- abuse/spam/duplicate throttling before paid AI;
- takedown/contact handling;
- operator role separation if other humans review submissions;
- monitoring/alerting adequate to notice abuse spikes.

These controls are **deferred, not omitted**. They are unnecessary cost and complexity while only the owner can submit material.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Security decision matrix for source intake

| Condition | Default disposition | Can structured safe outputs continue? | Human review? |
|---|---|---|---|
| Normal public HTTP/HTTPS source, safe destination, bounded payload | Continue normal pipeline | Yes | Only normal Stage 08/10 rules |
| Source requires access-control circumvention | Do not automate acquisition | Existing lawful/manual evidence may still be handled separately | Only if owner wants to register/manual-submit lawful material |
| URL resolves/redirects to private/internal/link-local/metadata target | Security block | No new fetch-derived output | Only to correct a false classification; never automatic retry |
| Unsupported executable/binary delivered instead of expected exam content | Reject/hold; do not execute | Prior independent structured data may remain | Only if high-value provenance ambiguity |
| File type mismatch but content is recognizable/bounded | Hold or parse through the safely detected type | Potentially, after safe normalization | Only if needed |
| Known/suspected malicious payload | Security quarantine/block | Existing non-dependent safe metadata may remain; no new raw-derived processing | Yes only if value/incident warrants it |
| Encrypted/password-protected archive | Hold; no brute force | Metadata/provenance can remain | Owner may provide a lawful known password through a future governed workflow; not required at launch |
| Archive expansion cannot be safely bounded | Stop expansion | Previously inspected safe members may remain if independently validated | Only if high-value |
| Prompt-injection/tool-use instructions in source text | Treat as source text only | Yes; extraction/classification may continue | No, unless it disrupts quality |
| Unnecessary incidental personal data | Sanitize derived representation; minimize replication | Yes | Only when deletion/rights/privacy ambiguity is material |
| Takedown/prohibited fingerprint rediscovered at another URL | Block re-ingestion; preserve new observation only if useful/allowed | Only previously allowed non-reconstructive metadata | No routine review unless request scope changed |

## 4.2 Content sanitization boundary

Corpus requires two different representations when necessary:

1. **source-faithful evidence** — raw bytes/page/asset retained for audit/reprocessing when permitted;
2. **safe operational/derived representation** — inert text/layout/metadata suitable for review, analytics, or model processing without executing active source behavior or unnecessarily propagating personal/tracking data.

This separation allows Corpus to remain an evidence product without making the operations UI or AI pipeline a browser for arbitrary hostile content.

### Sanitization must not falsify exam evidence

If a removed/sanitized element affects exam meaning—for example a required image, embedded table, answer option, audio control, or visible link text—the system records that the safe representation is incomplete and retains/uses an appropriate safe derived asset rather than silently pretending the element never existed.

## 4.3 External processing boundary

A paid/external OCR, ASR, embedding, or language model is allowed only when all applicable gates permit it:

- Stage 04 rights/terms allow the source content to be sent through that processing route;
- the processing is necessary enough to justify Stage 14 cost;
- the payload contains no secret values;
- unnecessary personal data is removed or avoided where practical;
- only the minimum needed page/segment/asset is sent when possible;
- outputs remain traceable and are not trusted as executable instructions.

**Cheap fallback:** local/deterministic processing, a broader/unknown result, or manual review for the small high-value cases.

## 4.4 Audit expectations for security/privacy actions

Stage 13’s audit history covers security/privacy actions as consequential changes.

At minimum record:

- source/payload/scope affected;
- action time and actor type;
- security/privacy reason category;
- previous and new state;
- related URL/domain/fingerprint where applicable;
- whether raw bytes were retained, isolated, or deleted;
- whether downstream App/publication eligibility changed;
- rationale for overriding/restoring a prior security block;
- relevant processing/rule version when automation created the finding.

Do **not** copy a secret or unnecessary personal datum into the audit trail as the explanation for a finding. Store a redacted description/reference instead.

## 4.5 Minimum launch controls

The following are **required before ordinary Corpus ingestion is considered safely launchable**:

| Control | Minimum launch behavior |
|---|---|
| **Internal-only access** | Operations/review is authenticated and not anonymously/publicly exposed. |
| **No public uploads** | Manual submissions are owner-only. |
| **Safe URL boundary** | HTTP/HTTPS only for normal automatic retrieval; private/internal/link-local/metadata destinations and unsafe redirects are blocked. |
| **No access circumvention** | No bypass of login, paywalls, CAPTCHAs, private groups, bot protections, or source rate limits. |
| **Untrusted-file preflight** | Type/container/size/archive safety checks plus low-cost malicious-file screening where practical before deep processing. |
| **No active-content execution** | Macros/scripts/binaries/source active content are not executed as part of extraction/review. |
| **Bounded archives** | Member count/size/nesting/expansion are constrained; suspicious/encrypted archives stop for review. |
| **Sanitized operations display** | Source HTML/rich content cannot execute in the privileged operations surface. |
| **Prompt-injection boundary** | Source text cannot command tools, reveal secrets, change policy, or auto-publish; model outputs remain derived data. |
| **Secret isolation** | Secrets are kept out of source data, prompts, logs, URLs, and repo content; routine crawling does not store third-party account credentials. |
| **Simple authority separation** | Owner, automated workers, and App have different permissions; App is not a raw-store/admin client. |
| **Auditability** | Security blocks, destructive deletion, takedown, restore, and human override actions are logged. |
| **Retention/deletion states** | Accepted evidence, rejected noise, malicious material, intermediates, and prohibited/takedown content follow the retention classes above. |
| **Re-ingestion prevention** | Security/takedown blocks can use URL/host/path/work/fingerprint scope sufficient to stop accidental re-entry. |
| **Transport/storage baseline** | Use normal secure transport for internal web access and the chosen hosting/storage platform’s standard encryption-at-rest capabilities when available; custom enterprise key infrastructure is not required. |
| **Existing cost/rate bounds** | Stage 14 crawl, retry, storage, and paid-processing limits remain active so abuse cannot create unbounded spend by default. |

## 4.6 Later hardening triggers

Enterprise-grade or public-service hardening is deferred until a concrete trigger exists.

| Trigger | Revisit / add controls |
|---|---|
| **Public or third-party file/URL submissions** | Stronger upload scanning/sandboxing, submitter auth/identity, quotas/rate limits, moderation, abuse reporting, alerting, public privacy/retention terms. |
| **More than one human write-capable operator** | Explicit RBAC, role separation, destructive/security/right-review permissions, account lifecycle, stronger authentication expectations. |
| **Automated authenticated crawling of third-party sites** | Credential/cookie storage policy, scoped account secrets, session rotation/revocation, connector-specific terms/access review. |
| **Public Corpus API or research UI** | External auth/authorization, output-level data exposure review, rate limiting, abuse controls, raw/reference-content access policy. |
| **Commercialization or materially broader external data sharing** | Formal privacy/legal review of source processing, licenses/terms, data processors, retention, and security obligations. |
| **Meaningful recurring personal/sensitive data in source intake** | Dedicated privacy classification/redaction rules, retention review, access limitations, possibly formal privacy impact assessment depending on context. |
| **Malware/security incident or repeated hostile payloads** | Incident-response procedure, stronger scanning/sandboxing, alerting/telemetry, review of existing stored material. |
| **Raw source storage becomes remotely accessible to App/users/third parties** | Re-design access control; raw store must no longer rely on owner-only/internal assumptions. |
| **Stage 14 high-scale envelope / hundreds of GB with more automation** | Reassess storage isolation, deletion lifecycle, scanning throughput, observability, and blast radius before unconstrained growth. |
| **Regulatory/contractual requirement from a chosen provider/host** | Add only the controls actually required; do not emulate enterprise compliance speculatively. |

## 4.7 Explicitly deferred enterprise controls

The following are **not launch product requirements** unless a trigger above makes them necessary:

- SSO/SAML/enterprise identity federation;
- multi-layer enterprise RBAC/approval chains;
- dedicated SOC/SIEM program;
- 24/7 monitoring/on-call security operations;
- commercial file detonation/sandbox service for every payload;
- data-loss-prevention suite;
- enterprise endpoint-management/EDR program for the product;
- custom HSM/KMS hierarchy beyond normal platform secret/encryption capabilities;
- formal penetration-test program on every release;
- formal ISO/SOC certification program;
- public vulnerability-bounty program;
- multi-region security architecture;
- expensive per-file AI security classification;
- bespoke WAF/bot-defense stack for an owner-only internal surface;
- complex retention automation solely to mimic enterprise policy at small personal-project volume.

These may become useful later; paying their cost before a public/multi-user/commercial trigger would violate the personal-project principle.

---

## 5. Edge Cases / Failure or Uncertainty Handling

## 5.1 Official source serves a compromised or unexpected file

Official provenance does not bypass security preflight. The payload is held/blocked like any other suspicious file. The source observation and provider relationship remain visible, but no deep processing/active rendering occurs until safe disposition.

## 5.2 A source page contains an exam plus malicious third-party embed

Keep the source observation. Extract/sanitize the legitimate evidence if it can be isolated safely. Do not fetch/execute the hostile embed merely because it shares a page with valuable content. Rights/security remain component-local where possible.

## 5.3 A PDF contains an embedded file or executable

Do not execute it. If the PDF’s visible exam content is safely extractable, that content may continue after preflight while the embedded member is ignored/held and noted. If the embed is required to interpret the exam and cannot be inspected safely, the affected use remains incomplete.

## 5.4 A DOCX contains macros

Treat macro presence as active content that is not executed. Parse document data through a non-executing route if possible. A macro is not evidence merely because it exists in the container.

## 5.5 A high-value archive is password protected

Automatic brute force is out of scope. The record remains held/deferred. If the owner lawfully knows the password and the eventual implementation supports a governed manual unlock path, it can be processed under the same safety rules. Stage 15 does not require that capability for launch.

## 5.6 A forum/shared document contains real names or contact details

Preserve only what is necessary for provenance/attribution/exam evidence. Derived analytics should not ingest the person’s contact details as topic/vocabulary evidence by default. Use a sanitized derived representation where practical. Raw retention follows value/risk rules.

## 5.7 A source contains prompt injection aimed at the enrichment model

Treat it as literal source content. The model may classify that text if relevant but it cannot execute the instruction, request secrets, call arbitrary tools, or change policy. If it causes unreliable output, the affected derivation is failed/provisional and routed through normal QA.

## 5.8 A mirror reintroduces takedown material

The new URL may be recorded as a source observation only if useful and allowed, but the underlying blocked fingerprint/work remains prohibited. The mirror does not reset rights/security state and does not trigger deep reprocessing.

## 5.9 A security scanner flags a likely false positive in unique TELC evidence

Do not silently override the finding. Hold the payload; the owner can explicitly review/restore it with rationale. Existing safe metadata/provenance may remain. A security override does not upgrade authenticity, rights, or extraction quality.

## 5.10 A raw accepted source disappears from the web

If retained locally and still permitted, it remains valuable provenance/reprocessing evidence as defined in Stages 02/14/15. Dead URL status does not itself require deletion.

## 5.11 Deletion is requested but derived analytics already exist

Apply Stage 04’s distinction:

- raw/reconstructive content and source-specific data are removed/suppressed according to the request/policy;
- non-reconstructive aggregate intelligence may remain only when allowed;
- current App-facing outputs are reevaluated/invalidation propagates through Stage 12;
- the prevention tombstone/fingerprint remains only to the minimum extent allowed and useful to prevent re-ingestion.

## 5.12 The only safe extraction path is expensive external processing

If Stage 04/privacy/security allows external processing and the item is high-value, Stage 14 escalation can justify it. Otherwise retain a broader/unknown/incomplete result or defer. Security and cost policy do not require perfect extraction of every source.

---

## 6. Relationship to Other Bestehen Stages

### Stage 02 — Source Strategy

Stage 15 constrains **how** sources are safely fetched/accepted; it does not narrow the source categories. The “no access circumvention” rule is now also a secret/security boundary.

### Stage 03 — Trust / Authenticity

Security status is independent of evidence confidence. High-confidence evidence may be unsafe bytes; low-confidence evidence may be technically harmless.

### Stage 04 — Rights / Usage

Rights decides permitted uses of source expression. Security decides whether/how a payload can safely pass through the system. Takedown/prohibition can also create a strong re-ingestion block.

### Stage 05 — Canonical Exam Model

Component-level entities allow unsafe assets or personal-data-heavy source regions to be held without destroying unrelated safe structured evidence.

### Stage 08 — Ingestion / Extraction

Stage 15 adds cross-cutting preflight, containment, sanitization, and model-instruction boundaries. It does not change the canonical lifecycle order.

### Stage 10 — Validation / QA

A failed security/privacy gate is a hard use-specific blocker. Passing technical security checks never substitutes for content QA.

### Stage 12 — Corpus → App Contract

App consumes published capabilities. It does not browse Corpus raw storage or operations. Exact reusable reference content can still be delivered when explicitly eligible; raw-store access is not required.

### Stage 13 — Operations

The Operations Inbox needs security/privacy findings, block reasons, raw-retention/deletion state, safe restore/delete actions, and audit history. No separate enterprise security console is required.

### Stage 14 — Cost / Scale / Automation

Security uses the same cheap-first philosophy. Deterministic destination/type/archive checks, local screening, sanitization, and existing crawl/cost bounds are the default. Paid security services are an escalation, not a universal ingestion tax.

### Stage 16 — Benchmark Corpus

The Stage 16 seed set should intentionally exercise at least the ordinary safe-input boundaries: multiple file types, one archive, one imperfect unofficial source, and one case where sanitization or an unsafe/unsupported member must be handled without corrupting the valid benchmark evidence. Stage 16 does not need live malware samples; benign fixtures can test boundary behavior.

### Stage 17 — Final Product Specification

The final PRD should carry forward four non-negotiable boundaries:

1. no learner-data store in Corpus;
2. external inputs are untrusted and non-executing;
3. App/automation have less authority than the owner and do not receive raw/admin access by default;
4. public submissions/multi-user/authenticated crawling trigger a deliberate security/privacy re-shaping pass.

---

## 7. Cost Notes

Stage 15 has **low expected recurring-cost impact** in the personal-project phase.

### 7.1 Preferred low-cost default

Use:

- deterministic URL/destination/protocol validation;
- existing Stage 14 crawl and retry limits;
- file/container/type/size checks;
- local/free/platform malicious-file screening where practical;
- inert/sanitized source representations;
- platform-provided authentication, TLS, encrypted storage, and secret handling where available;
- owner-only manual intake;
- audit records already required by Stage 13;
- local processing when rights/privacy do not permit raw content to leave the boundary.

These controls should add little or no per-Item paid processing cost compared with Stage 14’s existing pipeline.

### 7.2 Do not buy enterprise controls early

A commercial sandbox/scanner on every file, SIEM, enterprise IAM, DLP, HSM program, or 24/7 monitoring would materially increase cost/maintenance without matching the launch threat model.

### 7.3 When paying more is justified

Additional recurring security spend becomes reasonable when:

- third parties can upload files;
- hostile payload volume is no longer exceptional;
- multiple operators/admin accounts exist;
- authenticated source credentials are stored;
- a security incident demonstrates the cheap path is insufficient;
- commercial/public exposure creates a stronger contractual or regulatory requirement.

### 7.4 Cheap fallback when a premium control is not justified

**Hold, defer, reject, or manually inspect the small high-value exception** rather than paying to deeply analyze every untrusted source. Corpus quality is not improved by processing low-value suspicious material at enterprise cost.

---

## 8. Decisions Made

1. Corpus deliberately stores **no learner personal data** as part of its product model; operator/source personal data is minimized to audit/provenance/rights needs.
2. Every external file, URL, archive, page, and media asset is **untrusted regardless of source reputation or manual submission**.
3. Supported formats are processed as data and **active content is not executed**.
4. A cheap security/intake preflight occurs before deep/expensive processing; uncertain unsafe inputs are held rather than repeatedly probed.
5. Archive expansion is bounded; encrypted/pathological archives are held and not brute-forced.
6. Normal URL fetching is HTTP/HTTPS-only and cannot target private/internal/link-local/metadata destinations; redirects are revalidated.
7. Source HTML/rich content is shown/processed through inert or sanitized representations in privileged operations contexts.
8. Source text is untrusted instruction content for AI: it cannot command tools, reveal secrets, grant rights, delete records, or auto-publish.
9. Security-specific domain/source/fingerprint blocks join Stage 13’s allow/block controls; allowlisting never bypasses safety/governance gates.
10. Secrets are kept out of source data, URLs, prompts, logs, and repo content; routine launch crawling does not store third-party account credentials/cookies.
11. Launch permissions distinguish **owner**, **automation**, and **App**; enterprise RBAC is deferred until more human operators exist.
12. App receives published contract outputs, not unrestricted raw Corpus storage/admin access.
13. Accepted unique raw evidence is retained long-term while useful/permitted at personal-project scale; temporary/rejected/malicious/prohibited material has much shorter retention.
14. Rejected or security-dispositioned raw payloads should normally be removed within **7 days**; active takedown/prohibited raw content targets the same prompt deletion window when deletion is required/permitted.
15. Minimal provenance/audit/prevention fingerprints may survive raw deletion where lawful and necessary to prevent re-ingestion.
16. Manual submissions are **owner-only at launch** and never bypass normal gates.
17. Public submissions, multi-user operations, authenticated crawling, commercialization, or a material security/privacy incident are explicit triggers for stronger hardening.
18. Enterprise security programs are intentionally deferred; Stage 15 should add little/no meaningful recurring cost at launch.

---

## 9. Open Questions / Deferred Decisions

### 9.1 Owner questions

**None required for Stage 15.** The personal-project, one-owner, internal-first posture is specific enough to choose conservative defaults without blocking architecture.

### 9.2 Deferred architecture decisions

The following are intentionally left to architecture/implementation because the product behavior is already fixed:

- exact antivirus/malware-scanning tool;
- exact sandbox/container/process-isolation mechanism;
- exact SSRF/DNS-rebinding implementation;
- exact archive member/count/nesting/expansion thresholds beyond the Stage 14 250 MB large-file guardrail;
- exact HTML sanitizer/rendering implementation;
- secret manager/provider;
- authentication mechanism for the owner-only operations surface;
- backup topology and physical deletion mechanics;
- network segmentation/topology;
- logging/telemetry stack;
- exact encryption/key-management implementation using the selected hosting platform.

### 9.3 Deferred product decisions triggered only by expansion

These are not unresolved launch questions; they become product decisions only if the trigger occurs:

- public/third-party submission policy and submitter privacy model;
- multi-user role/permission model;
- authenticated crawler account/session policy;
- public Corpus/API security and data-exposure policy;
- commercial/privacy compliance posture;
- formal incident-response/on-call obligations.

---

## 10. Definition of Done Check

- [x] Expected learner/personal-data footprint is defined: Corpus stores no learner model/activity data and minimizes operator/source personal data.
- [x] Safe handling of untrusted files, active content, archives, scans/media, and suspicious payloads is defined.
- [x] URL and content sanitization boundaries are defined, including internal-network/unsafe redirect prevention and inert operations rendering.
- [x] Domain/source/fingerprint blocking rules are defined and separated from trust/rights.
- [x] Secret/access requirements are defined, including no launch requirement for stored third-party crawling credentials.
- [x] Permissions for owner, automation, and App are defined without premature enterprise RBAC.
- [x] Raw-file retention/deletion expectations are defined for accepted, duplicate, temporary, rejected, malicious, and prohibited/takedown material.
- [x] Manual-submission abuse handling is defined; submissions are owner-only at launch.
- [x] Minimum launch controls are explicit.
- [x] Later hardening triggers are explicit.
- [x] Enterprise-grade controls are intentionally deferred rather than silently assumed.
- [x] Cost impact and cheap fallbacks are documented.
- [x] No product question remains that must be invented by the architecture agent for the Stage 15 scope.

**Stage 15 is complete when the live Corpus checklist reflects these eight decisions and later agents preserve the minimum-launch versus later-hardening boundary.**
