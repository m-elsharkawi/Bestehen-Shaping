# Bestehen / Corpus — Stage 06: Exam and Skill Taxonomy

> **Status:** Authoritative Stage 06 product-shaping decision  
> **Product:** Bestehen / Corpus  
> **Initial domain:** German A2–B1 exam and exam-style material  
> **Primary downstream customer:** Bestehen / App  
> **Core principle:** Use a small, versioned, multi-axis skill graph that describes what exam evidence tests without confusing provider structure, source confidence, rights, CEFR level, topic, language knowledge, task mechanics, difficulty, or learner mastery.

## 1. Purpose and Scope

Stage 06 defines the normalized taxonomy that turns the canonical exam model from Stage 05 into comparable exam intelligence. The taxonomy answers questions such as:

- Which provider/exam family and CEFR scope does this evidence belong to?
- Which functional exam section and task pattern does it represent?
- What topic, lexical domain, grammar concept, comprehension skill, productive competency, reasoning pattern, strategy, or distractor does it test?
- Which concepts are prerequisites, counterparts, related skills, or common sources of confusion?
- Which tags are stable enough for Bestehen / App to use as learner-model nodes, and which are only provisional machine suggestions?
- How can the taxonomy evolve without silently resetting or fabricating learner progress?

This is a **product taxonomy**, not a physical graph/database schema. It defines canonical meanings, node families, tagging roles, relationship semantics, curation rules, and migration behavior. It does not choose a graph database, embeddings, classifiers, model vendor, storage format, API protocol, or final UI.

### 1.1 Stage objective

**Corpus items should be describable with a stable shared vocabulary that is precise enough to diagnose and train exam-relevant weaknesses, but coarse enough that tags can be applied consistently and maintained by a personal project.**

### 1.2 Taxonomy is not the canonical exam hierarchy

Stage 05 already defines structural entities such as Exam, Section, Part, Task, Item, Stimulus, Response Option, Answer, Scoring Rule, and Asset. Stage 06 does **not** replace that structure.

The distinction is:

- **Canonical exam model:** what the source contains and how units are structurally related.
- **Taxonomy:** what those units mean for comparison, analysis, generation, and learning.
- **Learner model:** the App's evidence-backed state for a learner against stable taxonomy nodes.

A provider-native `Teil 1` remains a Part or Task according to its semantic structure. Stage 06 can then tag it as `section.reading`, `task.matching`, `reading.paraphrase_recognition`, and so on.

### 1.3 What this stage deliberately does not decide

Stage 06 does not set:

- numerical difficulty or TELC-relevance weights — Stage 07;
- extraction/classification pipeline mechanics — Stage 08;
- duplicate/independence thresholds — Stage 09;
- production QA and final taxonomy-accuracy targets — Stage 10/16;
- analytical frequency formulas — Stage 11;
- the physical Corpus → App API/serialization — Stage 12;
- operations UI — Stage 13;
- concrete model/provider budgets — Stage 14;
- benchmark source selection — Stage 16.

It does define enough taxonomy semantics that those later stages do not need to invent the skill graph.

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
4. task type / response mechanic / stimulus form / interaction shape;
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

- `reading.paraphrase_and_lexical_relation.synonym_paraphrase_recognition` — **primary_tested**;
- `vocabulary.domain.housing_and_household` — **context/prerequisite_supporting**;
- `grammar.prepositions.dative_prepositions` — **incidental_present** unless the answer genuinely depends on it.

This role distinction is essential to the App's rule that one wrong answer must not penalize every tag attached to the item.

### 3.5 Skills, strategies, reasoning, and distractors are separate

**Decision:** These four families must not collapse into one generic “skill” list.

| Family | What it describes | Example |
|---|---|---|
| **Skill / competency** | Capability the learner must demonstrate | recognize a paraphrase; maintain spoken interaction |
| **Exam strategy** | Observable behavior used to execute the exam effectively | scan restrictions before choosing; move on when stuck |
| **Reasoning pattern** | Relationship the item requires between evidence and response | filter by two constraints; update after a speaker correction |
| **Distractor pattern** | How an incorrect option is made plausible | repeats a keyword but violates a time restriction |

They can be linked. For example, `reasoning.constraint_filtering` may typically test `reading.constraint_and_scope.restrictions_exceptions`, while a wrong option may be tagged `distractor.polarity_scope.restriction_exception_omitted`.

This separation makes diagnosis more useful: “you do not understand the restriction” is a different repair from “you understood it but did not check the final option against it.”

---

## 4. Detailed Product Model / Rules for This Stage

## 4.1 Initial taxonomy tree — overview

The hierarchy below is a conceptual starting tree. Stable internal IDs must not depend on the English display labels shown here.

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

The tree expresses broad `is_a` organization. Cross-family dependencies and counterparts use explicit graph relationships defined in Section 4.15.

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
2. A mixed-level exam remains mixed at Exam level; do not average it into “roughly B1.”
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

### C. Stimulus-form facets

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

1. Tag a grammar node as `primary_tested` only when the item response genuinely depends on selecting, interpreting, or producing that distinction.
2. Grammar appearing in a Reading/Listening stimulus is normally `incidental_present` unless misunderstanding the grammar is central to the intended comprehension.
3. Writing/Speaking responses can generate learner evidence for grammar production nodes only when the learner actually had a meaningful opportunity to use the form; the prompt does not automatically “test” every possible grammar feature.
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

Otherwise it remains searchable/analyzable lexical data rather than permanent taxonomy-governance overhead.

## 4.9 Reading skill taxonomy

**Decision:** Reading skills describe the comprehension capability needed to derive the answer from written/visual evidence. Timing and solver habits remain Strategy; the wrong-option mechanism remains Distractor.

Initial Reading hierarchy:

```text
reading
├── gist_and_purpose
│   ├── main_idea
│   ├── text_type_recognition
│   └── communicative_purpose
├── information_location
│   ├── scanning_specific_detail
│   ├── names_places_and_entities
│   └── numbers_dates_times_conditions
├── detailed_comprehension
│   ├── explicit_fact
│   ├── reference_resolution
│   └── cross_sentence_integration
├── paraphrase_and_lexical_relation
│   ├── synonym_paraphrase_recognition
│   └── reformulation_equivalence
├── inference
│   ├── local_inference
│   ├── implied_meaning
│   └── intention_and_stance
├── constraint_and_scope
│   ├── negation
│   ├── restrictions_exceptions
│   └── qualifiers_and_scope
├── matching_and_comparison
│   ├── text_to_heading
│   ├── need_to_offer
│   └── compare_multiple_texts
└── robustness
    ├── unknown_word_tolerance
    └── relevant_evidence_discrimination
```

### Reading rules

- `scanning_specific_detail` is the capability to locate information. `strategy.preview_or_scan_before_deep_reading` is the behavior of deciding to use scanning; keep them distinct.
- “Distractor rejection” from the App learner-model baseline is represented through `reading.robustness.relevant_evidence_discrimination` plus a strategy/reasoning/distractor tag when the exact failure is known.
- Visual/layout tasks may combine Reading skills with structured Stimulus-form facets. Do not create a separate “table skill” unless benchmark evidence shows the layout behavior is independently diagnostic.
- If a wrong answer can be explained only at broad Reading level, do not fabricate a narrow skill cause; keep the fine mapping provisional or attribute only the task/section.

## 4.10 Listening skill taxonomy

**Decision:** Listening skills describe recognition and comprehension from spoken input. Audio speed, noise, number of speakers, and similar conditions are **difficulty/evidence conditions**, not automatically separate mastery nodes.

Initial Listening hierarchy:

```text
listening
├── gist_and_situation
│   ├── main_message
│   ├── situation_context
│   └── communicative_purpose
├── detail_extraction
│   ├── names_entities_places
│   ├── numbers_dates_times_prices
│   └── conditions_locations_actions
├── spoken_language_mapping
│   ├── spoken_paraphrase_recognition
│   ├── connected_speech_recognition
│   └── lexical_form_recognition_in_audio
├── discourse_tracking
│   ├── speaker_identification
│   ├── correction_and_revision
│   └── sequence_and_reference_tracking
├── inference_and_intent
│   ├── intention_and_purpose
│   ├── attitude_and_stance
│   └── contextual_inference
├── polarity_and_scope
│   ├── negation
│   ├── restriction_exception
│   └── contrast_or_change
└── sustained_comprehension
    ├── attention_across_clip
    └── recover_after_missed_segment
```

### Listening rules

- A learner may demonstrate the same skill under different audio conditions. Stage 07 describes speed/noise/voice difficulty; App evidence records those conditions rather than multiplying skill nodes.
- `correction_and_revision` is especially important where a speaker first says one value/plan and then changes it.
- Numbers/dates/times/prices receive a dedicated node because they create repeatable, diagnosable failures across topics.
- Replay behavior is an evidence/strategy condition, not Listening mastery itself.
- Reading a transcript does not create Listening mastery; it can support repair but direct Listening evidence requires audio.

## 4.11 Writing competency taxonomy

**Decision:** Writing maps to rubric-like competencies representing B1 communicative sufficiency. Corpus describes what a prompt/rubric affords or requires; the App updates learner competency only from the learner's actual response/evaluation.

Initial Writing hierarchy:

```text
writing
├── task_fulfillment
│   ├── required_content_point_coverage
│   ├── relevance_to_prompt
│   └── completeness
├── communicative_success
│   ├── purpose_achieved
│   └── comprehensibility
├── organization_and_cohesion
│   ├── logical_progression
│   ├── paragraph_or_message_structure
│   └── connectors_and_reference
├── register_and_appropriateness
│   ├── recipient_purpose_fit
│   └── register_consistency
├── lexical_control
│   ├── vocabulary_sufficiency
│   ├── functional_phrase_use
│   ├── collocation_and_word_choice
│   └── useful_range
├── grammatical_control
│   ├── meaning_preserving_accuracy
│   └── useful_structure_range
├── task_conventions
│   ├── greeting_and_closing
│   └── required_format_conventions
└── execution
    ├── planning
    ├── revision_and_checking
    └── completion_under_time
```

### Writing rules

- The taxonomy evaluates **B1 sufficiency**, not native-like style.
- `writing.grammatical_control` is a broad rubric competency. Specific observed grammar errors/uses can additionally update canonical Grammar nodes in the App.
- `writing.lexical_control` is a broad rubric competency. Specific vocabulary evidence remains linked to Vocabulary/functional-language nodes.
- Required content points are prompt/rubric requirements, not fake independent objective Items unless the source actually scores them independently.
- Planning/checking can be represented both as Writing execution and related Strategy behavior; the competency means successful execution outcome, while Strategy means the observed method/behavior.

## 4.12 Speaking competency taxonomy

**Decision:** Speaking separates production from interaction where the task allows it and judges pronunciation through intelligibility rather than accent imitation.

Initial Speaking hierarchy:

```text
speaking
├── task_fulfillment_and_relevance
├── intelligibility
├── fluency_and_continuity
├── lexical_control
│   ├── vocabulary_sufficiency
│   ├── functional_phrase_use
│   └── useful_range_and_choice
├── grammatical_control
│   ├── meaning_preserving_accuracy
│   └── useful_structure_range
├── interaction
│   ├── listen_and_respond
│   ├── turn_taking
│   ├── follow_up
│   └── maintain_exchange
├── communicative_functions
│   ├── propose_and_suggest
│   ├── agree_and_disagree
│   ├── justify_and_give_reasons
│   ├── negotiate
│   └── offer_alternatives
├── repair_and_compensation
│   ├── paraphrase_unknown_word
│   ├── ask_for_clarification
│   ├── self_correct
│   └── recover_when_stuck
├── organization
│   ├── short_presentation_structure
│   └── sequencing_and_coherence
└── execution
    ├── preparation_time_use
    └── completion_within_task_time
```

### Speaking rules

- A monologue can test Speaking production but cannot establish `speaking.interaction` mastery.
- Typed responses never count as direct oral evidence.
- Accent similarity is not a node; intelligibility and communicative impact are.
- Recording/transcription quality belongs to evidence quality, not learner capability.
- Specific grammar/vocabulary use can map to the shared language-knowledge graph while broad rubric performance maps to Speaking competencies.

## 4.13 Exam-strategy taxonomy

**Decision:** Exam strategy represents **observable, trainable behavior for executing task formats efficiently and safely**. It is not generic advice that becomes “mastered” merely because the learner has read it.

Initial Strategy hierarchy:

```text
strategy
├── instruction_and_response_control
│   ├── understand_response_format
│   ├── obey_selection_cardinality
│   └── check_task_requirements
├── time_management
│   ├── allocate_time
│   ├── move_on_when_stuck
│   └── reserve_checking_time
├── receptive_execution
│   ├── preview_or_scan_before_deep_reading
│   ├── identify_evidence_before_answering
│   ├── eliminate_options_with_evidence
│   └── handle_unknown_words_without_abandoning_task
├── listening_execution
│   ├── protect_attention_during_limited_play
│   ├── anticipate_information_type
│   └── update_notes_or_choice_after_correction
├── writing_execution
│   ├── plan_required_content_points
│   ├── check_content_point_coverage
│   └── final_language_and_format_check
├── speaking_execution
│   ├── use_preparation_time
│   ├── sustain_interaction
│   └── recover_and_keep_communicating
└── response_completion
    ├── make_best_supported_choice
    └── avoid_unnecessary_blank_response
```

### Strategy rules

- Correctness alone does not prove good strategy.
- Slowness alone does not prove poor time management.
- Strategy evidence requires observable behavior, response pattern, or a diagnosis that supports the attribution.
- Strategy remains task-pattern-specific until evidence supports transfer.
- A strategy node may be directly practiced even when the underlying language skill is already adequate.

## 4.14 Reasoning-pattern taxonomy

**Decision:** Reasoning patterns describe the relation between evidence and the accepted response. They are exam-solving operations, not claims about a learner's general intelligence.

Initial Reasoning hierarchy:

```text
reasoning
├── explicit_retrieval
├── paraphrase_equivalence
├── constraint_filtering
├── compare_and_match
├── reference_resolution
├── temporal_sequence
├── cause_effect
├── contextual_inference
├── intention_or_stance_inference
├── update_after_correction
├── elimination_by_contradiction
├── best_fit_across_multiple_cues
├── integrate_multiple_evidence_points
├── grammar_context_fit
└── lexical_collocation_or_semantic_fit
```

### Reasoning rules

- An item can require more than one reasoning pattern, but one or two should normally explain the decisive operation.
- `grammar_context_fit` is useful for Language Elements when several forms are grammatical in isolation but only one fits the sentence/text relation.
- `lexical_collocation_or_semantic_fit` captures context-sensitive lexical choice without inventing a separate grammar tag.
- `constraint_filtering` means the learner must satisfy a restriction such as time, price, location, condition, or required feature.
- Empirical evidence may later show reasoning-pattern co-occurrences, but co-occurrence does not imply prerequisite.

## 4.15 Distractor-pattern taxonomy

**Decision:** Distractor patterns classify **why a wrong response option is plausible and wrong**. They attach to Response Options/Items where evidence supports the mechanism; they are not generic negative labels on the whole source.

Initial Distractor hierarchy:

```text
distractor
├── surface_overlap
│   ├── keyword_overlap_wrong_meaning
│   └── same_topic_wrong_detail
├── polarity_and_scope
│   ├── negation_reversal
│   ├── restriction_exception_omitted
│   └── qualifier_scope_shift
├── entity_and_value
│   ├── wrong_person_or_place
│   ├── wrong_number_date_time_price
│   └── unit_or_measurement_mismatch
├── evidence_relation
│   ├── nearby_but_unsupported
│   ├── partial_truth
│   ├── overgeneralization
│   ├── too_narrow_or_too_broad
│   ├── cause_effect_reversal
│   ├── chronology_confusion
│   ├── speaker_attribution_error
│   ├── opinion_fact_confusion
│   └── superseded_information
├── language_elements
│   ├── grammar_form_decoy
│   ├── connector_relation_decoy
│   ├── case_preposition_decoy
│   ├── morphology_agreement_decoy
│   ├── collocation_semantic_fit_decoy
│   └── register_decoy
└── matching
    ├── plausible_competitor
    ├── shared_keyword_competitor
    └── one_constraint_fails
```

### Distractor rules

1. An incorrect Response Option may have more than one distractor tag when both mechanisms materially apply.
2. Do not tag a correct option as a distractor globally; correctness remains Item-specific under Stage 05.
3. Do not infer distractor intent when the answer key itself is disputed or the option may simply be malformed.
4. A source error is not a distractor pattern.
5. Distractor frequency is useful intelligence only after duplicate neutrality and confidence weighting.
6. App diagnosis may map a learner mistake to a distractor pattern, but selecting a distractor once does not automatically create a stable weakness.

## 4.16 Relationships between taxonomy nodes

**Decision:** Graph relationships have controlled semantics. A vague generic `related` edge is available as a fallback, but high-value relationships use explicit types.

### Core relationship types

| Relationship | Direction | Meaning | Governance |
|---|---|---|---|
| `is_a` / `parent_of` | hierarchical | Child is a narrower canonical concept | Curated |
| `prerequisite_for` | directional | Reliable use of A materially supports learning/performance of B | Curated only; strong claim |
| `supports` | directional | A often helps B but is not a strict prerequisite | Curated or validated evidence |
| `related_to` | symmetric | Meaningful association without stronger semantics | Curated/validated |
| `receptive_counterpart_of` | symmetric | Receptive concept corresponding to a productive/use concept | Curated |
| `productive_counterpart_of` | symmetric | Productive concept corresponding to a receptive concept | Curated |
| `modality_counterpart_of` | symmetric | Same underlying language concept expressed in different direct-evidence lanes | Curated |
| `often_confused_with` | symmetric | Learners/options commonly confuse two concepts | Curated or validated empirical relation |
| `contrasts_with` | symmetric | Concepts are useful to learn/diagnose as a contrast | Curated |
| `typically_tested_by` | node → task type | Node is commonly targeted by this task form | Curated + analytics-supported |
| `typically_uses_reasoning` | task type → reasoning | Task form commonly requires reasoning pattern | Curated + analytics-supported |
| `distractor_targets` | distractor → skill/knowledge | Distractor exploits a particular weakness/distinction | Curated/validated |
| `co_occurs_with` | symmetric, weighted | Empirical co-occurrence in independent corpus evidence | Analytics-derived; never treated as causal |

### Relationship metadata

Like assignments, a relationship must be able to retain:

- origin: curated, explicit provider evidence, analytics-derived, AI-suggested, migrated;
- relationship confidence/evidence strength;
- supporting evidence/independent material count where empirical;
- applicable CEFR/provider/task context where needed;
- taxonomy version/lifecycle state.

### Relationship guardrails

- **Co-occurrence never becomes prerequisite automatically.**
- A Language Elements item can connect a Grammar node to a reasoning pattern without claiming the reasoning skill is language knowledge.
- Cross-modality counterparts influence recommendations before mastery: Reading recognition never directly creates Listening/Writing/Speaking mastery.
- Relationships may change coaching priority and content selection, but the App still requires direct evidence for the capability lane it claims.
- Provider-specific relationships should remain contextual when they do not generalize.

## 4.17 Assignment granularity and anti-shotgun rules

**Decision:** Corpus should prefer a small number of defensible primary tags rather than assigning every plausible concept.

Initial rules:

- Most objective Items should have **one or two primary tested skill/knowledge/reasoning nodes**.
- More than three primary non-rubric nodes on one objective Item should trigger review because it usually signals over-tagging or an item that needs decomposition.
- Productive tasks may intentionally map to several rubric competencies because the provider evaluates one integrated response across dimensions.
- Secondary/prerequisite/context tags may be broader, but they must not receive the same learner-update weight as primary tags.
- Incidental grammar/vocabulary present in a Stimulus should not become a learner penalty when an answer is wrong.
- When fine attribution is uncertain, use a broader parent node or retain a provisional mapping rather than inventing a leaf-level diagnosis.

---

## 5. Curation, AI Discovery, and Tag Quality

## 5.1 What must be curated/governed manually

**Decision:** The **meaning of the canonical graph** is governed, not generated ad hoc.

The following require human/product curation before becoming active canonical semantics:

- top-level taxonomy families;
- stable canonical node IDs;
- node definitions and boundaries;
- hierarchy (`is_a`);
- prerequisite semantics;
- modality/receptive/productive counterparts;
- relationship-type definitions;
- core Reading/Listening/Writing/Speaking/Strategy/Reasoning/Distractor nodes;
- canonical provider mappings and aliases where ambiguity is material;
- node promotion, merge, split, deprecation, retirement, and migration;
- changes that would move existing learner evidence to a different meaning.

AI may propose these changes, but it cannot publish them autonomously.

## 5.2 What should use deterministic/explicit-source mapping first

Prefer deterministic normalization when the source/canonical model already provides enough evidence, for example:

- explicit provider family/known provider alias;
- explicit provider-declared CEFR;
- normalized Section from a known native section label/context;
- response mechanic from Stage 05 structure/cardinality;
- stimulus form from canonical Stimulus type;
- task interaction shape where structurally explicit;
- provider-native aliases to an already-curated canonical node.

Deterministic does not mean infallible: mappings still carry version/provenance and can be reviewed when source evidence conflicts.

## 5.3 What AI may suggest or discover

AI/cheap semantic classification is useful for:

- primary/secondary Reading and Listening skill candidates;
- grammar target candidates;
- vocabulary/domain and functional-language tags;
- topic classification;
- Writing/Speaking competency affordance from prompts/rubrics;
- reasoning-pattern classification;
- distractor-pattern classification when a validated answer and evidence are available;
- candidate lexical clusters/synonym/paraphrase relations;
- candidate new taxonomy nodes when repeated material does not fit existing definitions;
- candidate `related_to`, `supports`, `often_confused_with`, and task-relevance relationships.

All machine-generated assignments retain origin and confidence.

## 5.4 AI may not autonomously do these things

Without governed review, AI must not:

- create, rename, delete, merge, or split active canonical nodes;
- declare a new `prerequisite_for` relationship;
- migrate learner evidence;
- convert an uncertain provider claim into verified identity;
- turn incidental grammar/vocabulary into `primary_tested` solely because it appears in the text;
- publish a distractor explanation when the answer key is disputed;
- silently overwrite a curator correction;
- infer learner mastery from Corpus frequency.

## 5.5 Assignment review states

Taxonomy assignments need at least these conceptual states:

- **curated** — explicitly reviewed/approved;
- **accepted_auto** — automatically published under a benchmarked rule/classifier;
- **provisional** — useful internal suggestion but not trusted enough for high-impact learner attribution;
- **review_required** — material ambiguity/conflict needs resolution;
- **rejected** — candidate mapping was evaluated and should not be active.

### Downstream posture

- Curated and benchmark-qualified `accepted_auto` primary mappings may support App fine-grained learner evidence, subject to Stage 03 source/item confidence.
- Provisional fine tags may support discovery/internal analytics but should map learner evidence only to a broader trusted parent or remain unattributed.
- A B+ source does not upgrade a weak taxonomy assignment automatically; **source confidence and tag confidence are separate gates**.

## 5.6 Initial auto-accept quality gate

The exact Stage 10/16 target will be benchmarked later, but Stage 06 sets a conservative product default:

- Before a gold-standard benchmark exists, fine-grained AI mappings are **provisional by default** unless manually reviewed or deterministically supported.
- Auto-publication of a high-impact fine mapping such as `primary_tested`, distractor pattern, or reasoning pattern should begin only after the relevant benchmark slice demonstrates about **95% precision or better**, with no known systematic failure that would misdiagnose learners.
- Broad low-risk context tags can use lower automation risk once benchmark evidence supports them, because an imperfect secondary topic tag has less learner consequence than a wrong primary skill.
- Benchmark precision is more important than the model's self-reported confidence number.
- If a classifier cannot meet the gate cheaply, the fallback is broader tagging, provisional status, or selective review — not buying a premium model for every item.

The 95% value is a starting safety/quality target, not an empirically proven constant. Stage 10/16 may recalibrate it based on measured consequences and corpus coverage.

## 5.7 New-node discovery and promotion

A candidate node should be promoted into the active canonical graph only when it passes all relevant tests:

1. **Distinct meaning:** it is not adequately represented by an existing node/alias.
2. **Distinct product action:** knowing the distinction would materially change diagnosis, repair, content selection, generation, or analysis.
3. **Repeat evidence:** it appears across enough independent B+ evidence to avoid modeling a one-off quirk. A reasonable initial default is at least three relevant independent tasks across at least two underlying materials.
4. **Provider-specific exception:** one verified official Tier A target-provider source may justify a provider-required concept even before repetition proves prevalence.
5. **Taggability:** curators/classifiers can distinguish it consistently from neighboring nodes on a benchmark sample.
6. **Maintenance value:** the benefit justifies adding long-lived taxonomy governance.

If these conditions are not met, keep the concept as a candidate, free-form analytical label, lexical record, or provider-specific metadata rather than an active shared learner-model node.

---

## 6. Taxonomy Versioning and Migration

## 6.1 Stable IDs, mutable labels

**Decision:** Every active canonical node has a stable, opaque identity independent of its human display label/path. Human-readable paths such as `reading.inference.implied_meaning` are examples/aliases, not a guarantee that identity is encoded in the path.

This allows wording, hierarchy, and translation to improve without rewriting learner history.

### Node lifecycle

A node may be:

- `candidate`;
- `active`;
- `deprecated`;
- `retired`.

Retired IDs are never reused for a different meaning.

## 6.2 Taxonomy release versions

Use semantic product versions conceptually:

- **Patch** — label, typo, example, or definition clarification that does not change the intended semantic boundary.
- **Minor** — additive/backward-compatible node, alias, relationship, or optional refinement.
- **Major** — breaking semantic changes such as material split/merge/type change or relationship-semantics change that requires downstream migration/reinterpretation.

The Stage 06 taxonomy begins as a shaped **0.x definition**. The Stage 16 benchmark should validate the initial graph and tagging behavior before the first stable **1.0** release is treated as the learner-model production baseline.

The exact packaging/registry mechanism is an architecture choice.

## 6.3 Every assignment remembers its taxonomy version

Historical task/item assignments and learner evidence must retain the node ID and taxonomy version under which the mapping was created. A current projection may resolve that evidence through migration maps; the historical event itself is not silently rewritten.

## 6.4 Migration rules

| Change | Product behavior |
|---|---|
| **Rename / description clarification** | Keep same node ID and learner state when meaning is unchanged |
| **Reparent without semantic change** | Keep node ID; recompute hierarchy-based rollups if needed |
| **Merge A + B → C** | Create explicit successor mapping; combine evidence without double-counting shared events |
| **Split A → B + C** | Historical A evidence becomes reduced-confidence supporting evidence for B/C where defensible; direct evidence is required before high-confidence mastery is claimed for either child |
| **Material meaning change** | Create a new node; deprecate/retire old node rather than mutating its historical meaning |
| **Retire with replacement** | Preserve historical evidence and map forward to replacement where semantically defensible |
| **Retire without replacement** | Keep historical record; remove node from new assignment/use |
| **Relationship change only** | Recalculate derived recommendations/rollups; do not rewrite original learner observations |
| **Task-to-node remapping** | Preserve old observation and mapping history; current analyses may use corrected mapping with auditable provenance |

### Migration invariant

**A taxonomy change may reduce certainty, reproject evidence, or request new evidence; it must never silently manufacture mastery.**

This directly preserves the App Stage 04 rule for splits/merges/retirement.

## 6.5 Migration auditability

Every semantic migration must be explainable through:

- source version and destination version;
- affected node(s);
- change type;
- rationale;
- successor/predecessor mapping;
- expected effect on learner evidence and aggregate analytics;
- whether re-tagging/reprocessing is required.

A rollback/current-view change should be possible conceptually because historical assignments remain versioned rather than destructively overwritten.

---

## 7. Example Item and Task Tagging

These examples are hypothetical abstractions. They demonstrate taxonomy behavior and do not reproduce a source exam.

## 7.1 Reading — matching a need to an advertisement

**Scenario:** A learner must match a housing need to one of several short listings. The correct listing is the only one satisfying both availability date and location; a distractor shares the same keyword but has the wrong date.

| Axis | Example tag | Role |
|---|---|---|
| Provider | `provider.telc` or third-party + TELC-style as supported | context |
| CEFR | `cefr.B1` | context |
| Section | `section.reading` | structural normalization |
| Task | `task.matching`, `response.match`, `stimulus.advertisement_listing` | task pattern |
| Topic | housing/accommodation | context |
| Vocabulary | housing + dates/scheduling | prerequisite/context |
| Reading | `reading.matching_and_comparison.need_to_offer` | primary_tested |
| Reading | `reading.constraint_and_scope.restrictions_exceptions` | primary/secondary tested |
| Reasoning | `reasoning.constraint_filtering` | primary reasoning |
| Strategy | identify evidence before answering | secondary/observable only |
| Distractor | `distractor.surface_overlap.keyword_overlap_wrong_meaning` | wrong-option pattern |
| Distractor | `distractor.polarity_and_scope.restriction_exception_omitted` | wrong-option pattern if applicable |

A dative preposition appearing in a listing is not automatically a tested Grammar node.

## 7.2 Language Elements — connector cloze

**Scenario:** A gap requires a connector expressing contrast; several options are grammatically possible words but only one expresses the correct clause relationship.

| Axis | Example tag | Role |
|---|---|---|
| Section | `section.language_elements` | structural normalization |
| Task | `task.cloze`, `response.choice_cloze` | task pattern |
| Grammar | `grammar.connectors_and_clause_relations.contrast_concession` | primary_tested |
| Reasoning | `reasoning.grammar_context_fit` | primary reasoning |
| Vocabulary | connector lexical record / functional relation | supporting |
| Distractor | `distractor.language_elements.connector_relation_decoy` | distractor |

If a competing answer also fails word order, a second Grammar/distractor tag is possible, but the item should not accumulate every grammatical feature in the surrounding paragraph.

## 7.3 Listening — changed time in a dialogue

**Scenario:** A speaker first suggests 18:00 and then corrects the plan to 18:30. One response option repeats the first time.

| Axis | Example tag | Role |
|---|---|---|
| Section | `section.listening` | structural normalization |
| Task | `task.comprehension.detail`, `response.single_select`, audio dialogue | task pattern |
| Topic | appointments/scheduling | context |
| Vocabulary | time/dates/schedules | prerequisite |
| Listening | `listening.detail_extraction.numbers_dates_times_prices` | primary_tested |
| Listening | `listening.discourse_tracking.correction_and_revision` | primary/secondary tested |
| Reasoning | `reasoning.update_after_correction` | primary reasoning |
| Distractor | `distractor.evidence_relation.superseded_information` | distractor |

Speech speed, noise, speaker count, and playback conditions belong to Stage 07/evidence conditions rather than becoming extra skill tags.

## 7.4 Writing — reschedule an appointment by email

**Scenario:** The prompt requires an email that apologizes, gives a reason, proposes a new time, and closes appropriately.

Task-level Corpus mapping can include:

- Section: Writing;
- task: guided message + email/letter + extended text response;
- topic: appointments/scheduling;
- functional language: apologizing/explaining, proposing, arranging;
- Writing competencies: content-point coverage, communicative success, organization/cohesion, register, conventions;
- Strategy affordance: plan/check content points.

The prompt **affords** Grammar and Vocabulary evidence but does not prove that every learner response will use a subordinate clause, a particular tense, or a specific phrase. The App maps actual response evidence to those nodes after evaluation.

## 7.5 Speaking — collaborative planning

**Scenario:** Two candidates plan a small event, must propose options, respond to each other, negotiate constraints, and reach an arrangement.

Task-level mappings include:

- Section: Speaking;
- task: collaborative planning + spoken interaction + partner planning;
- topic: events/social plans;
- functional language: propose, agree/disagree, reasons, negotiate, alternatives;
- Speaking competencies: task fulfillment, fluency, interaction, communicative functions, repair, execution;
- Strategy: use preparation time, sustain interaction, recover when stuck.

A monologue version of the same topic cannot be tagged as direct evidence for interaction competencies.

## 7.6 Mixed-level exam

A DTZ-style mixed A2–B1 Exam may remain `cefr.A2_B1_mixed` at Exam scope. One Task may be confidently classified B1 and another A2. The child assignments coexist without forcing the parent to a single level, and Stage 11 can later analyze progression using the local classifications.

---

## 8. Edge Cases / Failure or Uncertainty Handling

### 8.1 Item appears to test both grammar and reading

Multi-axis tagging is allowed. If the answer depends both on understanding a connector and using a reading inference, both can be primary/secondary with roles. Avoid deciding that “Section Reading” means Grammar cannot matter.

### 8.2 Passage contains many grammar forms

Tag them as incidental presence only if collecting that information is analytically useful. They do not become primary tested Grammar nodes unless the response depends on them.

### 8.3 Productive prompt could elicit many structures

Map the prompt to rubric competencies and functional-language affordances. Map specific Grammar/Vocabulary learner evidence from the actual response, not from every language feature the prompt could theoretically elicit.

### 8.4 AI proposes five primary skills for one multiple-choice item

Treat this as likely shotgun tagging. Keep the best-supported one/two primary nodes, demote others to supporting/context where justified, or send the item for review if the item genuinely combines several decisive operations.

### 8.5 OCR/ASR error changes apparent topic or grammar

Taxonomy confidence must reflect extraction quality. Do not allow an uncertain transcript/OCR representation to create high-confidence fine tags. Reprocess or keep broader/provisional mappings.

### 8.6 Answer key is disputed

Do not publish a high-confidence distractor analysis that assumes one answer is correct. Topic/task/skill tags that do not depend on the disputed correctness may remain usable with appropriate confidence.

### 8.7 Source is incomplete

Tag intact canonical entities locally. Do not infer whole-exam section balance, missing task types, or unseen topics from the fragment.

### 8.8 New provider task does not fit the task taxonomy

Use the closest compositional facets only when they are faithful. Otherwise use `other/unknown` plus a candidate label. Do not force a TELC-shaped name into the canonical graph merely to avoid adding a future refinement.

### 8.9 Integrated task spans Reading and Writing

Use `section.integrated` when the provider genuinely presents an integrated top-level task, then map the actual receptive/productive skills/competencies separately. Do not duplicate the same Task as two fake source Tasks.

### 8.10 One task has two legitimate topics

Assign one primary topic when defensible and additional secondary/context topics. If neither dominates, allow multiple co-primary topics rather than inventing a combined micro-topic.

### 8.11 Low-confidence source has a clear task type

Structural/deterministic taxonomy can still be high-confidence even when the underlying exam confidence is lower, but downstream influence remains gated by **both** evidence confidence and assignment confidence. A clear label does not make the source trustworthy.

### 8.12 Rights change or source is removed

Taxonomy tags are normally non-reconstructive metadata and can remain when Stage 04 permits. If a takedown/legal decision requires recomputation/purge, lineage must identify affected assignments. Rights do not alter the taxonomy meaning itself.

### 8.13 A new node would model a single word

Keep it in the lexical layer unless recurrence/product value justifies promotion. The shared learner graph should not become a raw dictionary.

### 8.14 Curator and AI disagree

The governed/curated decision wins for active canonical semantics. Preserve the machine suggestion/result for QA if useful; do not silently overwrite the correction on reprocessing.

### 8.15 Curators disagree on a primary skill

Mark review required or retain a broader parent mapping until the definition/evidence resolves the dispute. A taxonomy whose leaf distinctions cannot be applied consistently should be simplified rather than forcing false precision.

### 8.16 A node split would reset apparent learner progress

Do not reset or clone mastery. Apply the split migration rule: old evidence becomes cautious supporting evidence, confidence falls appropriately, and the App gathers fresh direct evidence for the new child distinctions.

---

## 9. Relationship to Other Bestehen Stages

### Stage 07 — Difficulty and TELC Relevance

Stage 07 must keep **CEFR**, **difficulty**, **generic B1 relevance**, and **TELC B1 relevance** separate. Taxonomy nodes/tasks provide what is being measured; Stage 07 adds how difficult/target-relevant the evidence appears.

### Stage 08 — Ingestion Pipeline

The pipeline should create deterministic structural tags first, then semantic enrichment, retain assignment origin/confidence/model/version, and route unresolved high-impact mappings to review. Reprocessing must not erase curator overrides.

### Stage 09 — Deduplication

Taxonomy frequency must be calculated after duplicate/derivative independence handling. Ten copies of one exam must not make one grammar/distractor/task pattern appear ten times more common.

### Stage 10 — Validation and QA

Stage 10 should validate tagging completeness and correctness by family, distinguish broad context accuracy from high-impact primary-skill accuracy, and test curator agreement where useful. Taxonomy assignment confidence should be benchmarked rather than accepted from model self-confidence.

### Stage 11 — Corpus Analytics

Analytics can produce frequency, co-occurrence, progression, provider comparison, distractor/reasoning, and empirical graph edges. It must preserve the distinction between curated semantic relationships and analytics-derived correlations.

### Stage 12 — Corpus → App Contract

The App contract should expose stable node IDs, definitions, hierarchy/relationships, taxonomy version, task/item mappings with role/confidence, and migration mappings. The App owns learner evidence/mastery; Corpus never writes learner state.

### Stage 13 — Corpus Operations

Operations should allow taxonomy correction, candidate-node review, assignment review, alias/migration management, and audit history without direct database surgery.

### Stage 14 — Cost, Scale, and Automation

Classification should be batchable/cached and should not require premium AI for every item. Stage 14 should measure model cost by enrichment workload and reserve high-cost review for ambiguity that materially affects learner attribution or TELC intelligence.

### Stage 16 — Initial Benchmark Corpus

The benchmark must cover all five major sections, objective/productive tasks, mixed A2–B1 material, official and imperfect unofficial sources, distractors, reasoning patterns, and enough edge cases to measure tagging precision. It should validate/promote the first stable taxonomy 1.0.

### Stage 17 — Final Product Specification

The final PRD must preserve the stable shared skill graph, assignment roles/confidence, curation boundary, and safe migration behavior defined here.

### Relationship to Bestehen / App

The central contract is:

> **Corpus owns what a skill means and which exam evidence maps to it; App owns what the learner has demonstrated against that skill.**

Corpus frequency/relevance can change coaching priority, but never learner mastery. App mistakes can reveal where the taxonomy needs improvement, but App must not fork the canonical meaning of a skill locally.

---

## 10. Cost Notes

Taxonomy enrichment creates ingestion/reprocessing cost but should create **no meaningful recurring per-learner cost**.

### 10.1 Preferred low-cost default

- Normalize provider/CEFR/Section/response mechanics deterministically where source structure supports it.
- Run semantic tagging offline/in batches rather than during App sessions.
- Cache assignments and only reprocess when source content, model/rules, or taxonomy version changes materially.
- Use cheap/local/open-source or lower-cost models for broad first-pass topic/grammar/skill suggestions when benchmark quality is adequate.
- Reserve better models/manual review for high-impact ambiguous primary skills, distractors, reasoning, productive-rubric mappings, and candidate node promotion.
- Keep individual lexical records outside the governed core graph unless promotion adds real product value; this avoids thousands of expensive hand-maintained nodes.
- Reuse one analyzed shared Stimulus across dependent Items instead of semantically analyzing the same passage/audio repeatedly.
- Preserve a broader trusted parent assignment when a fine distinction is not worth resolving immediately.

### 10.2 Premium processing trigger

Higher-cost processing is justified only when benchmark evidence shows the cheaper path materially harms:

- fine-grained learner diagnosis;
- TELC-relevant priority conclusions;
- distractor/reasoning intelligence;
- exercise-generation grounding;
- a benchmark/gold-standard record;
- a high-value unique task whose classification fills a major coverage gap.

### 10.3 Cheaper fallback

The default fallback is **coarser or provisional tagging**, not a mandatory premium call. Unknown is preferable to expensive fabricated precision.

### 10.4 Recurring-cost conclusion

This stage has **no requirement for per-session AI calls**. Taxonomy can be precomputed, versioned, cached, and consumed cheaply by the App.

---

## 11. Decisions Made

1. Corpus uses one **multi-axis, versioned controlled graph**, not one monolithic hierarchy.
2. Canonical families cover provider, CEFR, section, task, topic, grammar, vocabulary/domain, Reading, Listening, Writing, Speaking, strategy, reasoning, and distractors.
3. Every assignment carries role, confidence, origin/provenance, version, and review state.
4. Primary, secondary, prerequisite/context, incidental, and distractor assignments are distinguished so one item does not create shotgun learner evidence.
5. The graph is intentionally low-hundreds-scale initially; individual words and one-off details remain lexical/content records unless promotion creates real coaching value.
6. Provider metadata is independent of authenticity and rights; third-party TELC-style material does not become `provider.telc` official evidence by resemblance.
7. CEFR supports A2, B1, mixed A2–B1, incidental outside-scope content, and unknown; CEFR remains separate from numerical difficulty.
8. Section taxonomy normalizes Reading, Language Elements, Listening, Writing, Speaking, integrated, other, and unknown without inventing missing provider sections.
9. Task type is compositional across activity family, response mechanic, stimulus form, and interaction shape.
10. Topic taxonomy captures scenario/context and remains separate from language mastery.
11. Grammar taxonomy is exam-driven and function-oriented; incidental grammar is not treated as tested grammar automatically.
12. Vocabulary taxonomy separates lexical domains, functional language, and lexical relationships, with explicit promotion rules for shared learner nodes.
13. Reading taxonomy covers gist/purpose, information location, detailed comprehension, paraphrase, inference, constraints/scope, matching/comparison, and robustness.
14. Listening taxonomy covers gist/situation, detail, spoken-language mapping, discourse tracking, inference/intent, polarity/scope, and sustained comprehension; audio conditions remain difficulty/evidence properties.
15. Writing competencies cover task fulfillment, communicative success, organization/cohesion, register, lexical control, grammatical control, conventions, and execution.
16. Speaking competencies cover task fulfillment, intelligibility, fluency, lexical/grammar control, interaction, communicative functions, repair, organization, and execution; accent similarity is not a goal.
17. Strategy, reasoning, and distractor patterns are separate concepts with their own taxonomies.
18. Distractors are tagged on wrong-option relationships only when correctness/mechanism is defensible; source errors are not distractors.
19. Controlled relationship types include hierarchy, prerequisite, support, counterparts, confusion/contrast, task relevance, distractor targeting, and empirical co-occurrence.
20. Co-occurrence never becomes a prerequisite automatically, and cross-modality relationships do not transfer learner mastery without direct evidence.
21. Canonical semantics, stable IDs, hierarchy, prerequisites, migrations, and node lifecycle are curated/governed; AI may propose but not autonomously publish semantic graph changes.
22. Deterministic mapping is preferred for explicit structural metadata; AI is useful for semantic suggestions and candidate discovery.
23. Fine-grained machine mappings are provisional before benchmark validation; high-impact auto-publishing initially targets about 95% measured precision or better.
24. Candidate nodes require distinct meaning, distinct product action, repeat independent evidence or an official-target exception, reliable taggability, and maintenance value.
25. Stable node IDs are independent of display labels; nodes have candidate/active/deprecated/retired lifecycle and retired IDs are never reused.
26. Taxonomy versions follow patch/minor/major semantic-change principles; Stage 16 should validate the first stable 1.0 baseline.
27. Rename/reparent, merge, split, retirement, relationship changes, and task remapping have explicit learner-safe migration behavior.
28. A taxonomy migration may reduce certainty or request fresh evidence but must never silently create mastery.
29. Taxonomy enrichment should be offline/batched/cached and requires no per-learner model processing.

---

## 12. Open Questions / Deferred Decisions

### 12.1 Owner questions

**None.** The available Corpus and App decisions are sufficient to define the Stage 06 product taxonomy without an owner preference blocking completion.

### 12.2 Deliberately deferred product-detail/calibration decisions

- exact numerical difficulty and TELC relevance attached to taxonomy/task evidence — **Stage 07**;
- final auto-accept thresholds, per-family classifier metrics, and sampling rates — **Stages 10 and 16**; Stage 06's ~95% high-impact precision gate is the starting default;
- empirical co-occurrence/prevalence formulas and support-count thresholds — **Stage 11**;
- exact Corpus → App transport/contract format — **Stage 12**;
- taxonomy-review UI and operator workflow — **Stage 13**;
- model tiers and processing budgets — **Stage 14**;
- benchmark source set and first production-stable taxonomy release — **Stage 16**.

### 12.3 Architecture/implementation decisions intentionally not made

Graph database versus relational tables, physical node/edge schema, identifier format, taxonomy registry storage, classifier architecture, embeddings, prompt/model choices, batch orchestration, cache implementation, search indexing, and API serialization remain open.

---

## 13. Definition of Done Check

| Stage 06 requirement | Decision captured | Where |
|---|---|---|
| Define exam-provider metadata | **Yes** | 4.2 |
| Define CEFR and mixed-level handling | **Yes** | 4.3 |
| Define Section taxonomy | **Yes** | 4.4 |
| Reading Section | **Yes** | 4.4 |
| Language Elements / Sprachbausteine Section | **Yes** | 4.4 |
| Listening Section | **Yes** | 4.4 |
| Writing Section | **Yes** | 4.4 |
| Speaking Section | **Yes** | 4.4 |
| Define task-type taxonomy | **Yes** | 4.5 |
| Define topic taxonomy | **Yes** | 4.6 |
| Define grammar taxonomy | **Yes** | 4.7 |
| Define vocabulary/domain taxonomy | **Yes** | 4.8 |
| Define Reading skill taxonomy | **Yes** | 4.9 |
| Define Listening skill taxonomy | **Yes** | 4.10 |
| Define Writing competency taxonomy | **Yes** | 4.11 |
| Define Speaking competency taxonomy | **Yes** | 4.12 |
| Define exam-strategy/reasoning taxonomy | **Yes** | 4.13–4.14 |
| Define distractor-pattern taxonomy | **Yes** | 4.15 |
| Define relationships between taxonomy nodes | **Yes** | 4.16 |
| Decide curated vs AI-discovered | **Yes** | Section 5 |
| Define taxonomy versioning | **Yes** | Section 6 |
| Initial taxonomy tree | **Yes** | 4.1 and family trees |
| Assignment confidence/origin/role rules | **Yes** | 3.2, 4.17, Section 5 |
| Item-tagging examples | **Yes** | Section 7 |
| Migration rules compatible with App learner model | **Yes** | Section 6 |
| Cost-sensitive defaults | **Yes** | Section 10 |
| Edge cases / uncertainty handling | **Yes** | Section 8 |
| Owner blocker remains | **No** | 12.1 |

**Stage 06 product-shaping status: complete.** Corpus items can now connect to the same stable, versioned skill graph Bestehen / App uses for learner modeling without confusing source structure, exam metadata, language knowledge, task mechanics, strategy, reasoning, distractors, or learner performance.