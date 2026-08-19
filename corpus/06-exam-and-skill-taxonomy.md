# Bestehen / Corpus — Stage 06: Exam and Skill Taxonomy

> **Status:** In progress — foundational taxonomy decisions captured; skill/relationship/governance decisions follow in the same stage  
> **Product:** Bestehen / Corpus  
> **Initial domain:** German A2–B1 exam and exam-style material  
> **Primary downstream customer:** Bestehen / App  
> **Core principle:** Use a small, versioned, multi-axis skill graph that describes what exam evidence tests without confusing provider structure, source confidence, rights, CEFR level, topic, language knowledge, task mechanics, or learner mastery.

## 1. Purpose and Scope

Stage 06 defines the normalized taxonomy that turns the canonical exam model from Stage 05 into comparable exam intelligence. The taxonomy answers questions such as:

- Which provider/exam family and CEFR scope does this evidence belong to?
- Which functional exam section and task pattern does it represent?
- What topic, lexical domain, grammar concept, comprehension skill, productive competency, reasoning pattern, strategy, or distractor does it test?
- Which concepts are prerequisites, counterparts, related skills, or common sources of confusion?
- Which tags are stable enough for Bestehen / App to use as learner-model nodes, and which are only provisional machine suggestions?
- How can the taxonomy evolve without silently resetting or fabricating learner progress?

This is a **product taxonomy**, not a physical graph/database schema. It defines canonical meanings, node families, tagging roles, governance, and migration behavior. It does not choose a graph database, embeddings, classifiers, model vendor, storage format, or API protocol.

### 1.1 Stage objective

**Corpus items should be describable with a stable shared vocabulary that is precise enough to diagnose and train exam-relevant weaknesses, but coarse enough that tags can be applied consistently and maintained by a personal project.**

### 1.2 Taxonomy is not the canonical exam hierarchy

Stage 05 already defines structural entities such as Exam, Section, Part, Task, Item, Stimulus, Response Option, Answer, Scoring Rule, and Asset. Stage 06 does **not** replace that structure.

The distinction is:

- **Canonical exam model:** what the source contains and how units are structurally related.
- **Taxonomy:** what those units mean for comparison, analysis, and learning.
- **Learner model:** the App's evidence-backed state for a learner against stable taxonomy nodes.

A provider-native `Teil 1` remains a Part or Task according to its semantic structure. Stage 06 can then tag it as `section.reading`, `task.matching`, `reading.paraphrase_recognition`, and so on.

---

## 2. Inputs / Existing Decisions

This stage preserves the shared Product Overview, Identity, both live shaping checklists, Corpus Stages 01–05, and the already-shaped App learner model.

### 2.1 Corpus decisions inherited from Stages 01–05

- Corpus is broader than TELC but TELC B1 remains the strongest learner-target signal.
- Initial acquisition is German A2, B1, and mixed A2–B1 material; A1 scaffolding primarily belongs to App.
- Source category, authenticity/confidence, usage rights, CEFR, difficulty, and TELC relevance are different concepts.
- Provider/source claims must not be silently upgraded to verified facts.
- Confidence is local: a trusted parent record cannot wash away an uncertain item-level conclusion.
- Reference-only material may still produce non-reconstructive taxonomy tags and aggregate intelligence when confidence permits.
- Provider-native labels are preserved separately from normalized meanings.
- Instructions are separate from tested content and are excluded from ordinary tested-language frequency by default.
- Items are the smallest response/scoring-addressable units, while shared Stimuli and Response Option banks are represented once.
- Productive Writing/Speaking tasks are evaluated through competencies/rubrics rather than fake unique correct answers.
- Incomplete evidence remains incomplete; taxonomy must not invent missing source truth.

### 2.2 App learner-model contract already established

`app/04-learner-model.md` establishes that the App is an **evidence-backed overlay on a shared Corpus skill graph**. Corpus must provide stable node identifiers, definitions, node types, relationships, task mappings, relevance/frequency signals, tagging confidence, taxonomy versions, and migrations. The App stores personal mastery, conditions, confidence, recency, mistakes, and coaching priority against those nodes.

The shared graph must therefore preserve these App constraints:

- Reading, Listening, Writing, Speaking production, and interactive speaking are separate direct-evidence lanes.
- Recognition does not automatically imply productive mastery.
- Grammar and vocabulary may participate in several modalities.
- Topic familiarity is context, not a substitute for language mastery.
- A learner event may map to several nodes, but one event remains one evidence event and cannot be counted repeatedly as independent evidence.
- Low-confidence content-to-node tagging weakens learner attribution rather than fabricating fine-grained certainty.
- Node rename/merge/split/retirement must support safe learner-evidence migration.

No earlier decision needs to be changed for Stage 06.

---

## 3. Decisions and Rationale

### 3.1 Use a multi-axis controlled graph, not one giant tree

**Decision:** Bestehen uses one versioned taxonomy graph containing several controlled node families rather than forcing every concept into a single hierarchical classification.

The canonical families are:

1. provider/exam metadata;
2. CEFR scope;
3. normalized section;
4. task type / response mechanic / interaction shape;
5. topic/context;
6. grammar;
7. vocabulary/domain and functional language;
8. Reading skills;
9. Listening skills;
10. Writing competencies;
11. Speaking competencies;
12. exam strategy;
13. reasoning patterns;
14. distractor patterns.

A task/item can carry several tags across families because those tags answer different questions. A listening item may simultaneously be B1, Listening, single-select, travel, time-expression vocabulary, detail extraction, correction tracking, and a superseded-information distractor.

### 3.2 Every assignment has a role, confidence, origin, and version

**Decision:** A taxonomy assignment is not just `item → node`. Conceptually it must be able to state:

- the tagged canonical entity and taxonomy node;
- assignment role: `primary_tested`, `secondary_tested`, `prerequisite_supporting`, `context`, `incidental_present`, `distractor`, or another family-specific role;
- assignment confidence;
- assignment origin/method: explicit source fact, deterministic normalization, human-curated, AI-suggested, AI-auto-accepted after validation, or imported/migrated;
- evidence/provenance supporting the assignment;
- taxonomy version under which the assignment was made;
- review state when the assignment is disputed or provisional.

This prevents two common errors:

1. treating every structure merely **present** in a passage as something the item deliberately tests;
2. allowing a low-confidence AI guess to become learner mastery evidence as strongly as a curated primary-skill mapping.

### 3.3 Use the smallest useful tag set, not maximal linguistic annotation

A canonical leaf should exist only when it is useful for at least one downstream job and can be tagged consistently enough to trust.

Create or retain a canonical node when it materially supports one or more of:

- diagnosing a learner weakness;
- selecting a targeted repair or retry;
- comparing task/provider patterns;
- measuring A2→B1 progression;
- grounding original exercise generation;
- explaining a distractor/reasoning failure;
- prioritizing TELC-relevant training.

Do **not** create a canonical skill node merely because a linguistic distinction can theoretically be named.

Initial granularity rules:

- Prefer 2–4 meaningful levels of hierarchy inside a family.
- Prefer a low-hundreds core graph rather than thousands of hand-governed micro-skills.
- Individual word forms, every inflected form, every named person/place, and one-off content details are **not** taxonomy nodes by default.
- Corpus may maintain lexical records/entities outside the canonical taxonomy; only recurring, strategically useful lexical concepts/groups need promotion to shared learner-model nodes.
- Split a node when the children lead to meaningfully different diagnosis/training and Corpus can tag the difference reliably.
- Merge/retain a broader node when the proposed distinction produces the same coaching action or cannot be tagged consistently.

### 3.4 Primary versus supporting skill is mandatory

A task often requires several capabilities. Corpus must distinguish the capability the item is designed to probe from prerequisites that merely make it solvable.

Example: a reading item whose intended challenge is recognizing a paraphrase may also contain dative prepositions and housing vocabulary. The appropriate mapping might be:

- `reading.paraphrase_recognition` — **primary_tested**;
- `vocabulary.housing` — **context/supporting**;
- `grammar.preposition_case.dative` — **incidental_present** unless the answer genuinely depends on it.

This role distinction is essential to the App's rule that one wrong answer must not penalize every tag attached to the item.

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Initial taxonomy tree — overview

The hierarchy below is a conceptual starting tree. Stable internal IDs should not depend on the English display labels shown here.

```text
exam_taxonomy
├── provider
├── cefr
├── section
├── task
│   ├── activity_family
│   ├── response_mechanic
│   ├── stimulus_form
│   └── interaction_shape
├── topic
├── language_knowledge
│   ├── grammar
│   └── vocabulary_domain
├── receptive_skill
│   ├── reading
│   └── listening
├── productive_competency
│   ├── writing
│   └── speaking
├── strategy
├── reasoning_pattern
└── distractor_pattern
```

The tree expresses broad `is_a` organization. Cross-family dependencies and counterparts are graph relationships defined later in this document.

## 4.2 Exam-provider metadata taxonomy

**Decision:** Provider metadata identifies the assessment family/style being represented without encoding authenticity or rights.

### Core provider families

- `provider.telc`
- `provider.goethe`
- `provider.oesd`
- `provider.dtz`
- `provider.other_established`
- `provider.third_party_generic`
- `provider.unknown`

### Required provider/exam metadata concepts

For each Exam/Test Set or relevant task fragment, Corpus should be able to preserve:

- normalized provider family;
- provider-native organization/provider name as observed;
- normalized exam family when known;
- provider-native exam/product title;
- declared exam level/level range;
- exam variant/module/edition/version when the source establishes it;
- provider-native Section/Part/Task labels and numbers;
- **target-style claim** for third-party material, e.g. “TELC-style mock”, separately from normalized provider identity;
- mapping confidence when provider/exam identity is uncertain.

### Guardrails

- `provider.telc` does not mean the source is verified official; Stage 03 authenticity decides that.
- A teacher-created TELC-style mock is `provider.third_party_generic` with `target_style = telc`, unless evidence supports a more precise third-party family.
- Rights never derive from provider metadata.
- Provider currentness/TELC relevance is Stage 07 territory; Stage 06 only describes identity/classification.

## 4.3 CEFR and mixed-level taxonomy

**Decision:** CEFR classification supports explicit A2, B1, mixed A2–B1, incidental out-of-scope levels, and uncertainty. It is not a numerical difficulty score.

### Normalized CEFR values

- `cefr.A2`
- `cefr.B1`
- `cefr.A2_B1_mixed`
- `cefr.below_A2_incidental`
- `cefr.above_B1_incidental`
- `cefr.unknown`

### Rules

1. Preserve the **source/provider-declared level** separately from Corpus's normalized classification.
2. A mixed-level exam remains mixed at the Exam level; do not average it into “roughly B1.”
3. Tasks/items inside a mixed exam may receive a narrower A2 or B1 classification when evidence supports it.
4. Parent level is a prior/context, not an automatic child label.
5. If a task genuinely bridges levels or cannot responsibly be separated, keep `A2_B1_mixed` or `unknown`.
6. Incidental A1/B2+ content can be preserved for provenance/context but does not expand initial acquisition scope.
7. CEFR says **what competence band the material targets**, while Stage 07 numerical difficulty says **how hard this particular task is**. Two B1 items may have very different difficulty.
8. AI-estimated CEFR must retain assignment confidence and may not overwrite an explicit provider claim silently; contradictions become reviewable evidence.

## 4.4 Section taxonomy

**Decision:** Normalized Sections are functional exam divisions, independent of provider wording.

Canonical section nodes:

- `section.reading` — Reading / Lesen / Leseverstehen and equivalent receptive text sections;
- `section.language_elements` — explicit Language Elements / Sprachbausteine / grammar-vocabulary-in-context sections when the provider actually has such a functional division;
- `section.listening` — Listening / Hören / Hörverstehen;
- `section.writing` — Writing / Schreiben;
- `section.speaking` — Speaking / Sprechen;
- `section.integrated` — genuinely integrated assessment whose top-level function cannot responsibly be reduced to one of the above;
- `section.other` — meaningful provider section outside the normalized launch set;
- `section.unknown` — insufficient evidence.

### Section rules

- Do not invent `section.language_elements` for providers that test grammar/vocabulary inside Reading/Writing or another structure.
- Provider-native section/module names remain stored alongside the normalized tag.
- Integrated tasks can additionally carry skill-level tags for the specific receptive/productive capabilities involved.
- Standalone tasks may receive a normalized section context without pretending they belong to a complete Exam.
- The five launch learner-facing sections remain **Reading, Language Elements, Listening, Writing, and Speaking**, matching the App's section rollups.

## 4.5 Task-type taxonomy

**Decision:** Task type is **compositional**, not one ever-growing flat label. A Task may be described by activity family plus response mechanic, stimulus form, and interaction shape.

### A. Activity families

#### Receptive / objective

- `task.comprehension.gist`
- `task.comprehension.detail`
- `task.comprehension.inference`
- `task.matching`
- `task.cloze`
- `task.classification`
- `task.ordering_sequence`
- `task.form_or_information_completion`
- `task.short_response`

#### Productive writing

- `task.writing.guided_message`
- `task.writing.email_or_letter`
- `task.writing.formal_or_semiformal_correspondence`
- `task.writing.short_functional_text`
- `task.writing.extended_response`

These can overlap where provider/source semantics warrant it: for example an email can be both `guided_message` and `email_or_letter`.

#### Productive/interactive speaking

- `task.speaking.personal_exchange`
- `task.speaking.short_presentation_or_monologue`
- `task.speaking.stimulus_response`
- `task.speaking.discussion`
- `task.speaking.collaborative_planning`
- `task.speaking.problem_solving_or_negotiation`

### B. Response mechanics

- `response.single_select`
- `response.multi_select`
- `response.true_false_yes_no`
- `response.match`
- `response.open_cloze`
- `response.choice_cloze`
- `response.word_bank_cloze`
- `response.short_text`
- `response.extended_text`
- `response.spoken_monologue`
- `response.spoken_interaction`
- `response.ordered_set`
- `response.form_fields`
- `response.other`

Stage 05 source scoring/cardinality rules remain authoritative. `multi_select` does not mean several independent Items unless the source scores them that way.

### C. Stimulus form facets

Normalize Stage 05 Stimulus forms where useful for pattern analysis:

- passage/article;
- short-text collection;
- notice/sign;
- advertisement/listing;
- message/email/letter;
- table/form;
- chart/diagram/map;
- image/photo;
- audio announcement;
- audio dialogue/conversation;
- audio interview/report;
- video;
- scenario/prompt card;
- mixed-media stimulus.

### D. Interaction-shape facets

- `interaction.none`
- `interaction.solo_productive`
- `interaction.partner_exchange`
- `interaction.partner_planning`
- `interaction.group_or_multi_speaker_context`
- `interaction.examiner_candidate`
- `interaction.other_or_unknown`

This compositional model lets Corpus distinguish “what activity is being done” from “how the answer is entered” and “what source material it uses” without creating labels such as `telc_b1_reading_part_1_heading_match_pdf`.

## 4.6 Topic taxonomy

**Decision:** Topic represents **what the situation/text is about**, not the language skill being tested. A Task/Stimulus may have one primary topic and several secondary topics.

Initial topic hierarchy:

```text
topic
├── personal_and_social
│   ├── identity_and_personal_information
│   ├── family_friends_relationships
│   ├── invitations_and_social_plans
│   └── communication_and_arrangements
├── home_and_daily_life
│   ├── housing_and_accommodation
│   ├── household_and_neighborhood
│   ├── appointments_and_scheduling
│   ├── shopping_and_consumption
│   └── food_and_dining
├── work_and_learning
│   ├── employment_and_workplace
│   ├── job_search_and_applications
│   └── education_courses_and_training
├── mobility_and_travel
│   ├── local_transport
│   ├── travel_and_holidays
│   ├── accommodation_away_from_home
│   └── directions_and_routes
├── health_and_wellbeing
│   ├── health_services_and_appointments
│   ├── symptoms_treatment_pharmacy
│   └── wellbeing_fitness_lifestyle
├── services_and_administration
│   ├── public_services_and_forms
│   ├── banking_money_and_payments
│   ├── postal_telecom_and_customer_services
│   └── complaints_returns_and_problems
├── community_and_leisure
│   ├── events_culture_and_entertainment
│   ├── sport_hobbies_and_clubs
│   └── volunteering_and_local_community
├── media_technology_and_communication
├── environment_weather_and_surroundings
├── rules_notices_and_public_information
└── other_or_unknown
```

### Topic rules

- Do not create a new canonical topic for every named event, product, city, profession, illness, or hobby.
- Keep concrete named entities/details as content metadata, not taxonomy nodes.
- Split a broad topic only when frequency or learner performance shows the distinction changes useful coaching/content selection.
- Topic familiarity in the App is modality-specific context. Good performance on housing Reading does not imply housing vocabulary is available in Speaking.

## 4.7 Grammar taxonomy

**Decision:** Grammar nodes describe exam-relevant form/function distinctions that can explain comprehension or production performance. They are not textbook chapter numbers.

Initial grammar hierarchy:

```text
grammar
├── sentence_structure
│   ├── main_clause_v2
│   ├── inversion_after_initial_element
│   ├── yes_no_and_wh_questions
│   ├── subordinate_clause_verb_final
│   ├── coordination
│   ├── infinitive_clause_with_zu
│   └── relative_clause_structure
├── connectors_and_clause_relations
│   ├── coordinating_connectors
│   ├── reason_cause
│   ├── consequence_result
│   ├── contrast_concession
│   ├── condition
│   ├── time_sequence
│   ├── purpose
│   └── reported_content_dass_and_related
├── verb_system
│   ├── present
│   ├── perfect
│   ├── common_preterite
│   ├── future_werden
│   ├── modal_verbs
│   ├── separable_and_inseparable_verbs
│   ├── reflexive_verbs
│   ├── imperative
│   ├── passive
│   ├── konjunktiv_ii_polite_hypothetical
│   └── verb_complements_and_verb_preposition
├── case_and_noun_phrase
│   ├── nominative
│   ├── accusative
│   ├── dative
│   ├── limited_genitive
│   ├── article_and_determiner_choice
│   ├── adjective_inflection
│   ├── possessive_and_demonstrative_forms
│   └── noun_number_and_plural
├── prepositions
│   ├── accusative_prepositions
│   ├── dative_prepositions
│   ├── two_way_prepositions
│   ├── local_directional_prepositions
│   ├── temporal_prepositions
│   └── fixed_prepositional_combinations
├── pronouns_and_reference
│   ├── personal_pronouns
│   ├── reflexive_pronouns
│   ├── relative_pronouns
│   ├── indefinite_pronouns_and_man
│   └── pronominal_adverbs_da_wo
├── negation
│   ├── nicht
│   ├── kein
│   └── negation_scope_and_position
├── adjective_adverb_comparison
│   ├── comparative
│   ├── superlative
│   └── degree_and_comparison_patterns
└── agreement_and_inflection
    ├── subject_verb_agreement
    └── morphology_form_selection
```

### Grammar tagging rules

1. Tag a grammar node as `primary_tested` only when the item response genuinely depends on selecting/interpreting/producing that distinction.
2. Grammar appearing in a Reading/Listening stimulus is normally `incidental_present` unless misunderstanding the grammar is central to the intended comprehension.
3. Writing/Speaking responses can generate evidence for grammar production nodes when the learner actually had a meaningful opportunity to use the form; the prompt does not automatically “test” every possible grammar feature.
4. Prefer functional subnodes (`reason_cause`, `condition`, `contrast_concession`) where they drive communicative meaning; specific connector lexical forms may also be linked as vocabulary/lexical records.
5. New micro-rules should not become canonical nodes until they lead to distinct diagnosis/training and can be tagged reliably across evidence.

## 4.8 Vocabulary/domain taxonomy

**Decision:** Vocabulary has three layers: **lexical domain**, **functional language**, and **lexical relationships**. Individual lexical entries can exist in a lexicon without each becoming a canonical learner-model taxonomy node.

### A. Lexical domains

Initial lexical-domain nodes include:

- personal details and relationships;
- time, dates, schedules, durations;
- numbers, quantities, prices, measurements;
- housing and household;
- work and jobs;
- education and courses;
- transport, travel, and directions;
- health and medical services;
- shopping, products, and customer service;
- food and dining;
- public administration and forms;
- banking, money, and payments;
- leisure, events, sport, and culture;
- media, digital communication, and technology;
- weather, environment, and local surroundings;
- rules, notices, permissions, and restrictions.

Lexical domains relate to Topic nodes but are not identical: a travel task can test generic time expressions or complaint language, and the same functional vocabulary can appear across many topics.

### B. Functional/communicative language

Initial functional-language nodes include:

- asking for and giving information;
- requesting and responding to requests;
- inviting and accepting/declining;
- apologizing and explaining;
- suggesting and proposing;
- agreeing and disagreeing;
- expressing opinion and giving reasons;
- comparing and expressing preference;
- planning and arranging;
- negotiating and offering alternatives;
- complaining and requesting resolution;
- clarifying, checking, and repairing communication;
- sequencing/narrating events;
- opening and closing correspondence;
- polite forms and register-sensitive phrases.

These are highly useful to Writing and Speaking and may also appear as receptive targets.

### C. Lexical relationship facets

Corpus may relate lexical concepts through:

- synonym;
- paraphrase/near-equivalence;
- antonym/contrast;
- collocation;
- multiword expression/chunk;
- word family;
- register/formality relation;
- commonly confused lexical pair;
- sound-confusable pair where listening evidence makes it useful.

### Lexical-node promotion rule

A lemma/phrase is promoted from a raw lexical record to a shared graph node only when at least one of these is true:

- it recurs enough in B+ independent evidence to justify learner tracking;
- it represents a high-value functional phrase or exam-critical lexical distinction;
- it participates in a recurring synonym/paraphrase/distractor relation that the App should diagnose;
- it is necessary to connect mistakes across modalities or tasks.

Otherwise it remains searchable/analyzable lexical data rather than permanent taxonomy governance overhead.

---

## 5. Work Still to Be Completed in This Stage

The foundational classification axes above are now decided. The same Stage 06 artifact will next add and lock:

- Reading skill taxonomy;
- Listening skill taxonomy;
- Writing competency taxonomy;
- Speaking competency taxonomy;
- exam-strategy and reasoning-pattern taxonomies;
- distractor-pattern taxonomy;
- relationship semantics between nodes;
- curated versus AI-suggested/discovered rules;
- taxonomy versioning and migration rules;
- edge-case handling, examples, cost notes, final decisions, and definition-of-done reconciliation.
