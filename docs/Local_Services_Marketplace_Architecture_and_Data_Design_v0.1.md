**ARCHITECTURE AND DATA DESIGN**

**Local Verified Services Marketplace**

*Corrected architecture baseline • v0.1*

| **Field** | **Value** |
| --- | --- |
| Status | Corrected candidate for founder approval and logical data modeling |
| Authority order | Gold SRS v0.2 → approved Domain Model v0.1 → founder decisions → this architecture |
| Purpose | Define architecture shape, ownership, consistency, security, operations, and conceptual data boundaries |
| Not selected | Cloud provider, programming languages, frameworks, physical schema, exact vendor services |
| Revision basis | Independent review reconciled against frozen SRS, frozen Domain Model, and founder interview |
| Next gate | Founder approval, then Logical Data Model v0.1 |

| **Control statement** The Gold SRS and Domain Model remain frozen. This revision clarifies architecture and launch-safety responsibilities without changing product requirements or forcing expensive infrastructure. |
| --- |

# 1. Executive Architecture Decision

Use a cloud-portable modular monolith for V1_Initial: one mobile-first web client, one primary backend application with enforced internal modules, one authoritative relational operational database, separate object storage for media, managed identity, and limited durable background processing.

At most one Provider may hold the active Assignment for a Job at any moment. If that Assignment ends and the Job legitimately reopens, a later selection cycle may form a new Assignment while preserving every prior Assignment and Selection Request as terminal history.

The architecture is globally adaptable at the domain and data levels but initially operates in one concentrated active Market. Global readiness does not require global deployment or multi-region active-active infrastructure.

# 2. Architecture Drivers and Priorities

| **Priority** | **Driver** | **Architectural response** |
| --- | --- | --- |
| 1 | Marketplace data integrity | Strong transactions for winning acceptance, active Assignment uniqueness, Rating eligibility, and privileged actions. |
| 2 | Global adaptability | Generic Place hierarchy, currency and locale support, UTC timestamps plus zone identifiers, international phone/address formats. |
| 3 | Solo-founder delivery | One deployable backend, limited infrastructure, simple operations, managed commodity services. |
| 4 | Privacy and security | Deny-by-default authorization, sensitive-data separation, disclosure auditing, protected media/evidence. |
| 5 | Low operational complexity | No V1 microservices, Kafka, Kubernetes, or multi-region active-active. |
| 6 | Evolvability | Explicit modules, adapters, versioned policies, stable historical facts. |
| 7 | Weak-network usability | Recoverable drafts, compressed media, resumable uploads, idempotent consequential actions. |
| 8 | Cost proportionality | Serve hundreds economically and scale stateless application capacity when actual demand grows. |
| 9 | Availability and recovery | Normal consumer availability, tested backups, point-in-time recovery where available, recovery within an accepted operational window. |
| 10 | Purposeful analytics | Record trustworthy business events; defer a warehouse or streaming platform. |

# 3. System Context and Trust Boundaries

| **Customers** | → | **Marketplace Platform** | → | **Providers / Organizations** |
| --- | --- | --- | --- | --- |

| **Actor or external capability** | **Interaction** | **Trust boundary** |
| --- | --- | --- |
| Customer | Publishes Jobs, searches, communicates, issues Selection Requests, confirms outcomes, rates. | Public client; server authorizes ownership and legitimate participation. |
| Individual Provider | Maintains Profile, discovers Jobs, responds, accepts, performs Work. | Public client; eligibility and Assignment scope enforced. |
| Organization Administrator | Manages one organization, workers, organizational Responses and Completion. | Organization-scoped authority only. |
| Assigned Worker | Accesses and communicates about assigned Work. | Current Assignment scope only. |
| Platform Administrator | Manages Markets, Categories, verification review, complaints, restrictions. | Privileged internal role with stronger authentication and audit. |
| Managed Identity Provider | Authenticates and supports recovery/social sign-in. | External security dependency; internal identity remains provider-independent. |
| Email/Notification Provider | Delivers selected notifications. | Receives minimum necessary delivery data. |
| Maps/Geocoding Provider | Assists location entry or navigation. | Exact location shared only when flow and authorization permit. |
| Object Storage | Stores Job media, communication media, verification and safety evidence. | Assets remain private by default with controlled access. |
| Monitoring Provider | Receives operational telemetry. | Logs exclude secrets and unnecessary personal/private content. |

# 4. Logical Architecture

| **Mobile-first Web Client** | → | **Modular Backend** | → | **Relational Operational Store** |
| --- | --- | --- | --- | --- |

| **Modular Backend** | → | **Object Storage** | → | **Identity / Email / Maps Adapters** |
| --- | --- | --- | --- | --- |

| **Element** | **Responsibility** | **Initial posture** |
| --- | --- | --- |
| Web client | Accessible customer/provider/admin flows, local draft assistance, upload preparation, clear failure recovery. | One responsive web application; native apps deferred. |
| Backend application | Use cases, authorization, business transactions, policies, APIs, outbox, integrations. | Stateless-capable modular monolith. |
| Operational database | Authoritative current state, constraints, history, outbox, audit records. | Managed relational service preferred; vendor deferred. |
| Object storage | Binary assets with validation state, classification, retention, access control. | Separate from database and application web root. |
| Background processor | Notifications, media processing, expiry, projections, cleanup. | Database-backed durable work, in-app processor or one small worker. |
| Discovery projection | Composed searchable views of Jobs and Provider Profiles. | Relational search/filtering initially; dedicated search service deferred. |
| Administration surface | Minimal platform safety/governance and separate organization administration. | No giant back-office product. |
| External adapters | Managed identity, email, maps, later SMS/WhatsApp. | Replaceable/provider-isolated contracts. |

# 5. Module Ownership and Dependency Rules

| **Module** | **Authoritative ownership** | **Dependencies / prohibition** |
| --- | --- | --- |
| Identity & Access | Internal identity reference, external-auth link, role grants, account status, sessions/revocation integration. | Does not own Jobs, Profiles, or reputation. |
| Provider Management | Individual/organization Profiles, organization memberships, Associated Workers, services and areas. | References Identity, Taxonomy, Geography; does not own Job lifecycle. |
| Marketplace | Job identity/lifecycle, Response, Selection Cycle, Selection Request, Assignment identity/formation, responsible Provider, active/terminal authority. | Uses Provider eligibility and Market/Category references; does not own execution details. |
| Fulfilment | Assignment execution details: terms, Inspection, schedule, Work, Completion reports and fulfilment outcomes. | Cannot independently create/reassign Assignment or mutate competing Assignment authority. |
| Discovery & Matching | Eligibility filtering, broad distribution, Profile search, Job feed, categoryless handling, cold start, ranking policy/projections. | Composes Marketplace, Provider, Taxonomy, Geography, Verification and Reputation; owns no source records. |
| Communication | Profile-originated, Job and Assignment conversations; participants; disclosure records. | Does not own Job or Assignment state. |
| Media | Asset metadata, validation/publish state, storage reference, classification, access and cleanup. | Authorization derives from owning business context. |
| Reputation | Rating, Review, publication state, qualifying-activity checks and reputation projections. | Consumes authoritative completion/safety facts; does not own them. |
| Trust & Safety | Complaint, evidence, dispute, allegation, response, responsibility decision, restriction. | Does not silently change star Ratings. |
| Markets & Geography | Generic Place hierarchy, Market activation, service areas, waitlist interest. | Marketplace must enforce active-Market status. |
| Taxonomy | Controlled Category hierarchy and lifecycle. | Jobs may reference zero, one, or multiple Categories. |
| Notifications | Durable notification intent and delivery state. | Never determines business outcome. |
| Audit & Analytics | Purposeful event history, privileged audit, operational metrics. | Not authoritative for current business state. |

# 6. Assignment Ownership Rule

| **Single authority** Marketplace owns Assignment identity, formation, responsible Provider, relationship to Job, and whether the Assignment is active or terminal. Fulfilment owns execution details. A coordinated application use case updates both within one database transaction when immediate consistency is required. |
| --- |

Job closure may be derived from authoritative terminal Assignment and Job-closure facts, or updated atomically by the coordinating use case. Marketplace and Fulfilment must never keep independent competing Assignment-status truths.

# 7. Selection Cycles and Winning Acceptance

| **New selection cycle** | → | **Multiple valid requests** | → | **First valid acceptance** | → | **Assignment formed** | → | **Other requests terminal** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

| **Rule** | **Required behavior** |
| --- | --- |
| Cycle validity | Each Selection Request belongs to a current selection cycle, attempt number, generation, or equivalent validity boundary. |
| Reopening | When a Job reopens, earlier Selection Requests remain terminal and cannot become valid again. |
| Acceptance transaction | Verify current cycle, Job eligibility, request validity, no active Assignment, and eligible Provider; form Assignment and close competing requests atomically. |
| Sequential Assignments | A later cycle may form a new Assignment only after the prior Assignment is terminal and the Job legitimately reopens. |
| Notifications | Created after commit through durable asynchronous intent; cannot determine the winner. |
| Expired/rescinded requests | Remain historical with explicit terminal reason. |
| Old links | An old acceptance link or repeated request cannot form a new Assignment. |

# 8. Material Terms and Historical Fidelity

A pending Selection Request and resulting Assignment must not silently change when a Provider replaces a Response or when a Customer edits a Job.

| **Business moment** | **History requirement** |
| --- | --- |
| Selection Request issued | Reference immutable Job/Response versions or store a snapshot of material terms shown to the Provider. |
| Selection Request accepted | Preserve the accepted material context and Provider identity. |
| Later negotiation | Record new proposals and mutual acceptance without overwriting prior accepted facts. |
| Price | Preserve amount/range/pricing method and currency when recorded; the platform does not guarantee every offline change. |
| Scope | Preserve material agreed scope and accepted revisions. |
| Inspection | Preserve whether Inspection is the agreed deliverable or a preliminary activity. |
| Schedule | Preserve proposed, agreed, rescheduled, and superseded schedule facts. |
| Dispute | Permit reconstruction of the material terms and timeline relevant to the dispute. |

# 9. Lifecycle and Terminal Flows

## 9.1 Job closure without Assignment

| **Published Job** | → | **Closure reason recorded** | → | **Job terminal** |
| --- | --- | --- | --- | --- |

Supported reasons include Customer withdrawal, no responses, no acceptable response, resolved independently, expiry, and Platform closure. These outcomes are distinct from Assignment cancellation and Successful Job.

## 9.2 Selection Request terminal paths

| **Path** | **Result** |
| --- | --- |
| Provider declines | Request terminal; no Assignment; Customer may continue selection. |
| Customer rescinds | Request terminal; does not cancel an Assignment because none exists. |
| Job materially changes | Existing request invalidated or a new version/cycle is required. |
| Another Provider accepts | Request automatically terminal as competing request closed. |
| Job closes | All open requests terminal. |
| Expiry enabled | Request terminal at configured expiry; exact duration is V1 policy. |

## 9.3 Assignment cancellation and reopening

Cancellation records the acting party, reason, alleged responsible party, dispute status, evidence links, and later confirmed responsibility where determined. The old Assignment becomes terminal. Policy decides whether the Job closes or reopens. If reopened, a new selection cycle begins and all old requests remain terminal.

## 9.4 Deal Not Made After Inspection

A preliminary Inspection occurred but broader Work was not agreed. This is neither Successful Completion nor automatically ordinary cancellation. The Assignment ends with its own terminal outcome. Policy decides whether the Job closes or reopens.

## 9.5 Provider no-show

After an agreed arrival window, the Customer may allege Provider no-show. The Provider may respond or dispute. Platform review may later confirm responsibility. Any reopening decision must terminate the current Assignment appropriately and preserve the allegation and decision history.

## 9.6 Completion and dispute

Completion Report is an assertion by the responsible Provider or Organization. Customer confirmation establishes Completion under the proposed policy. A dispute blocks automatic Completion. Platform resolution may establish a final outcome. Prior reports, disputes, corrections, and decisions remain historical.

# 10. Business-Fact Separation

| **Fact family** | **Distinct facts to retain** |
| --- | --- |
| Job closure | Closure actor, reason, timestamp, whether Assignment ever existed. |
| Cancellation | Cancellation action, actor, stated reason, target Assignment, terminal effect. |
| Responsibility | Alleged responsible party, agreement/dispute, evidence, confirmed responsible party, decision authority/time. |
| No-show | Customer allegation, arrival window, Provider response/dispute, confirmation if any. |
| Completion | Report, reporting actor, confirmation, dispute, timeout decision, final completion status. |
| Inspection | Mode, occurrence, findings where recorded, deliverable/preliminary classification. |
| Deal not made | Terminal Assignment outcome and Job close/reopen decision. |
| Complaint / dispute | Reporter, legitimate activity link, reason, evidence, counter-response, status and decision. |
| Successful Job | Derived only from publication, selection, Work performance and recorded Completion. |
| Reputation | Rating/Review and separate cancellation/integrity indicators. |

# 11. Discovery and Matching

| **Capability** | **Architecture responsibility** |
| --- | --- |
| Provider Profile discovery | Search/filter by Market/service area, Categories, Provider type, Verification and legitimate reputation indicators. |
| Provider Job discovery | Eligible Job feed using active Market, service area, Category relevance, visibility and Provider eligibility. |
| Relevant broad distribution | During low density, avoid overly narrow matching that prevents realistic response chance. |
| Categoryless Jobs | Jobs may have zero Categories; distribution policy is explicit V1 decision, not an accidental exclusion. |
| Cold start | New Providers are not permanently hidden solely because they lack Reviews. |
| Ranking | Policy-driven and replaceable; sophisticated ranking deferred. |
| Projection ownership | Discovery owns searchable projections and policy coordination, while source modules own Jobs, Profiles, Categories and Markets. |
| Market enforcement | Inactive areas cannot expose live Jobs or Provider application flows. |

## 11.1 Profile-Originated Conversation

A Profile-Originated Conversation is a legitimate in-platform conversation initiated from a Provider Profile and linked to the Customer and Provider participants. It may later link to a Job, but it does not itself create Assignment, Completed-Job history, or Rating eligibility.

Current founder decision for V1 planning: a Job created from a Provider Profile follows normal publication and automatically invites that Provider. This supersedes the earlier provider-directed-only interpretation for the current architecture baseline.

# 12. Identity, Authentication, and Authorization

| **Concern** | **Baseline rule** |
| --- | --- |
| Identity model | One human identity may gain Customer participation, Individual Provider participation, and organization memberships. |
| Authentication | Managed identity; initial email and Google sign-in proposed; phone verification introduced progressively when justified. |
| Authorization | Deny by default; enforce server-side object-level checks for ownership, participation, organization membership, Assignment scope and platform privilege. |
| Organization isolation | Every organization-scoped operation verifies current membership and specific authority. |
| Assigned Worker | May access only current assigned operational information permitted by role. |
| Platform Administrator | Separate privileged role; strong or step-up authentication required for sensitive actions. |
| Privileged audit | Record actor, target, reason, action, timestamp and result. |
| Account linking | Prevent unsafe silent merging; preserve provider subject mappings and support session revocation. |
| Self-dealing | Known identity and organization relationships blocked transactionally. |
| Duplicate accounts | Verification, risk signals and manual review reduce abuse; system does not claim perfect real-world identity uniqueness. |

# 13. Security Architecture Baseline

- TLS for all external and internal service communication where applicable; managed encryption at rest for database and object storage.

- Secrets stored in managed secret/configuration mechanisms with no secrets in source code, images, logs, or client bundles.

- Rate limits and abuse controls for login, account recovery, messaging, Responses, Selection Requests, search, and uploads.

- Structured validation and parameterized data access; server does not trust client-provided ownership, role, price authority, status, or file type.

- Sensitive logging redaction for addresses, contacts, tokens, identity/verification evidence, complaint evidence, and private message content.

- Verification and moderation evidence uses narrower access policy than ordinary Job media.

- Dependency, container/package, and vulnerability checks are required before production release.

- Security cases cover horizontal access, organization isolation, privilege escalation, duplicate submissions, stale links, and self-dealing.

# 14. Communication, Contact, and Address

| **Stage** | **Communication** | **Contact disclosure** | **Location disclosure** |
| --- | --- | --- | --- |
| Profile discovery | Profile-Originated Conversation permitted. | Hidden. | Provider service area only. |
| Published Job/Response | Job communication permitted to legitimate participants. | Hidden. | Mandatory service area and approximate location. |
| Selection pending | In-platform communication continues. | Hidden by default. | Approximate location. |
| Assignment formed | Assignment communication enabled. | Separate contact policy may disclose after Assignment without posting-time configuration burden. | Exact address only after Assignment and Customer confirmation. |
| Cancellation/reassignment | History retained; future access reevaluated. | Revoke future platform access where policy requires. | Expire future address/media access for no-longer-authorized participants. |
| After Completion | Legitimate history remains; messaging duration is V1 policy. | No new automatic disclosure. | Historical access minimized by need and policy. |

# 15. Media and Evidence Architecture

| **Control** | **Required behavior** |
| --- | --- |
| Storage | Binary content in private object storage; database holds metadata, classification, owner context and status. |
| Pre-publication state | New object is quarantined/unpublished until required validation succeeds. |
| Validation | Allowlisted formats; verify actual content/MIME rather than trusting extension or declared header. |
| Image safety | Re-encode images where practical; remove EXIF and embedded geolocation metadata. |
| Abuse limits | Enforce file size, image dimensions, upload count and decompression/resource limits. |
| Identifiers | Generate storage names/keys; never trust user filenames as object paths. |
| Authorization | Authorize both upload initiation and every access-URL issuance against the owning business context. |
| Retrieval | Short-lived access URLs or mediated delivery; short expiry enables future revocation. |
| Publish behavior | FR-073 warning, preview and removal before Job publication; unvalidated assets cannot be visible. |
| Cleanup | Remove abandoned/orphaned uploads and incomplete multipart data after policy window. |
| Ordinary media | May use normal durability and lifecycle. |
| Safety evidence | Verification, complaint and moderation evidence may require stronger durability, safety hold and narrower access. |
| Malware handling | Use safe re-encoding and proportionate scanning; stronger malware scanning required when supported file types create meaningful risk. |

# 16. Durable Asynchronous Work

| **Initial mechanism** Use a database-backed transactional outbox/work queue processed by the application or one small worker. A dedicated broker is introduced only if measured scale or reliability requires it. |
| --- |

| **Rule** | **Required behavior** |
| --- | --- |
| Commit-safe handoff | Business transaction and durable work intent commit together or use an equivalent guarantee. |
| Delivery assumption | Handlers assume at-least-once execution, not exactly-once delivery. |
| Idempotency | Repeating a work item must not create duplicate business outcomes. |
| Retry | Transient failures retry with bounded backoff and attempt tracking. |
| Permanent failure | Record terminal failure and make it operationally visible. |
| Duplicate delivery | Email/notification projections tolerate duplicate attempts and use deduplication keys where needed. |
| Multiple instances | Workers claim/lock work safely so concurrent instances do not process the same item unsafely. |
| Scheduling | Expiry/cleanup jobs use safe claiming and store the policy version or reason. |
| Monitoring | Track delayed work, failed work, retry counts and queue age. |
| Broker deferral | No Kafka or dedicated message infrastructure required for V1. |

# 17. Availability, Durability, and Recovery

| **Concern** | **Corrected baseline** |
| --- | --- |
| Deployment region | Deploy initially in one region. Availability-zone redundancy depends on provider capabilities, cost and accepted risk. Multi-region active-active is deferred. |
| Availability target | Normally available consumer service; specific target selected before launch. |
| Database protection | Automated backups and point-in-time recovery where supported; restore testing required. |
| RPO/RTO | Replace provisional near-current/within-hours wording with selected numeric targets before production launch. |
| Media protection | Ordinary media lower criticality than database facts; safety evidence may require stronger retention/durability. |
| Application recovery | Reproducible build/deployment and documented recovery runbook. |
| Backup monitoring | Backup and archive failures generate alerts. |
| Restore validation | Periodic isolated restoration proves backup usefulness. |

# 18. Operational and Deployment Baseline

- Structured, redacted logs with request/correlation identifiers.

- Health and readiness checks for application instances.

- Error-rate, latency and critical-use-case metrics.

- Database connection, storage capacity and object-storage failure monitoring.

- Background-work failure, retry and queue-lag monitoring.

- Notification delivery monitoring for selected channels.

- Backup-failure and restore-test visibility.

- Basic incident, rollback and restore runbooks.

- Separate development, staging and production configuration and credentials.

- Reproducible deployments and versioned configuration.

- Safe forward-compatible schema migrations; destructive changes use staged migration patterns.

- Application rollback strategy and database forward-recovery strategy.

- Security/administrative audit history logically separated from product analytics, even if initially stored in one database.

# 19. Privacy and Data Lifecycle

| **Lifecycle concern** | **Architecture requirement** |
| --- | --- |
| Account closure | Disable access promptly and preserve only permitted historical integrity facts. |
| Export | Provide administrative export capability initially; self-service may follow. |
| Deletion/pseudonymization | Design identity separation so personal data can be removed or pseudonymized where appropriate. |
| Safety/legal hold | Prevent deletion of evidence under a valid safety or legal hold. |
| Disclosure history | Record when contact/address access was granted, to whom, for what Assignment, and under which policy. |
| Revocation | Cancellation/reassignment revokes future platform access and relies on short-lived URLs; prior human knowledge cannot be erased. |
| Backup aging | Deletion propagates according to documented backup-retention lifecycle rather than immediate backup rewriting. |
| Business history | Preserve legitimate Job, Assignment, outcome and integrity history with minimized identity exposure. |
| Client drafts | Define cleanup for abandoned local drafts and cached sensitive data. |
| Retention periods | Exact periods require legal/privacy and operational decision before production. |

# 20. Conceptual Data Model

| **Concept** | **Key relationship / distinction** | **Owner** |
| --- | --- | --- |
| Identity | Links authentication subjects, participations, memberships and privileges. | Identity & Access |
| Provider Profile | Individual or Organization; Categories, service areas, Verification and reputation summary. | Provider Management |
| Organization / Membership | Administrator and worker memberships with role and status. | Provider Management |
| Place / Market | Generic global hierarchy; activation separate from place existence. | Markets & Geography |
| Service Category | Governed hierarchy; Job has zero, one or many; Provider has zero or many. | Taxonomy |
| Job | Customer demand, location, versions, media, closure, cycles, historical Assignments. | Marketplace |
| Job Version | Material Job context used by Selection Request or later dispute. | Marketplace |
| Response / Response Version | Provider interest and material proposal history; one active response per Provider/Job. | Marketplace |
| Selection Cycle | Validity boundary for one selection attempt after publication or reopening. | Marketplace |
| Selection Request | Provider invitation tied to cycle and material source context. | Marketplace |
| Assignment | Identity, responsible Provider, active/terminal authority, Job and cycle. | Marketplace |
| Assignment Terms | Accepted/superseded scope, price basis, Inspection mode and schedule. | Fulfilment |
| Inspection | Deliverable or preliminary classification and occurrence. | Fulfilment |
| Completion Report / Decision | Assertion, confirmation/dispute, timeout or platform resolution. | Fulfilment |
| Job Closure | Unassigned terminal reason and actor. | Marketplace |
| Assignment Cancellation | Action and reason, distinct from responsibility attribution. | Fulfilment / Trust & Safety |
| Responsibility Allegation / Decision | Claim, dispute, evidence and confirmed attribution. | Trust & Safety |
| Provider No-show Allegation | Arrival-window claim and Provider response. | Trust & Safety |
| Deal Not Made After Inspection | Terminal fulfilment outcome with close/reopen consequence. | Fulfilment |
| Conversation / Message | Profile, Job or Assignment context; participant authorization. | Communication |
| Media Asset | Storage metadata, validation/publish state, classification and owner context. | Media |
| Rating / Review | Directional qualifying-job feedback and publication state. | Reputation |
| Complaint / Dispute Case | Legitimate activity, evidence, response and decision. | Trust & Safety |
| Verification | Subject, evidence, decision, level and expiry where applicable. | Identity & Access / Trust |
| Notification Intent | Recipient, source event, channel, dedupe and delivery state. | Notifications |
| Outbox Work Item | Commit-safe asynchronous intent, attempts and terminal state. | Backend infrastructure |
| Business Event | Purposeful domain history for audit/analytics. | Audit & Analytics |
| Privileged Audit Event | Administrator action, actor, target, reason and result. | Security / Audit |

# 21. Cardinality and Consistency Map

| **Relationship** | **Logical rule** |
| --- | --- |
| Job → Selection Cycles | One to many over Job lifetime; only one current open cycle. |
| Selection Cycle → Selection Requests | One to many; requests never move between cycles. |
| Job → Assignments | Zero to many historical; at most one active. |
| Selection Request → Assignment | Zero or one; only accepted winning request creates it. |
| Job → Responses | Zero to many; at most one active per Provider. |
| Response → Response Versions | One to many if material change history is retained. |
| Job → Job Versions | One to many where material edits occur. |
| Selection Request → source context | Exactly one immutable version reference or equivalent material snapshot. |
| Assignment → terms versions | Zero to many proposals/accepted versions; currently effective set unambiguous. |
| Assignment → Completion decisions | History may contain reports/disputes; at most one effective final completion result. |
| Completed Job → Ratings | At most two active directional Ratings, one from each party. |
| Organization → members | One to many; one initial administrator required by V1 policy if organization enabled. |
| Assignment → Assigned Worker | Zero or one current worker in minimal model; changes preserved. |
| Job → Categories | Zero to many. |
| Conversation → Messages | One to many, ordered and access-controlled. |
| Business context → Media | Zero to many within configured policy and classification. |

# 22. Domain Implementation Decision Mapping

| **ID** | **Architecture treatment** | **Status / next resolution** |
| --- | --- | --- |
| ID-01 Minimal lifecycle states | Semantic Job, Selection Request, Assignment, Completion, closure and dispute distinctions are mandatory; exact persisted encoding deferred. | Logical Data Model. |
| ID-02 Completion policy | Provider/Organization reports; Customer confirms or disputes. Auto-completion is proposed only for undisputed cases. | Approve policy and choose timeout in V1 Policy Baseline. |
| ID-03 Job expiry | Supported through durable scheduled policy; reminder not required. | Choose duration/automation in V1 Policy Baseline. |
| ID-04 Selection Request expiry | Cycle validity and terminal reasons supported; timer is optional. | Choose whether and duration in V1 Policy Baseline. |
| ID-05 Contact/address disclosure | Separate policies: contact after Assignment under simple policy; exact address after Assignment and Customer confirmation. | Finalize details in Privacy/UX design. |
| ID-06 Categoryless Job distribution | Discovery explicitly supports zero Categories and a broader/manual distribution policy. | Choose initial rule in V1 Policy Baseline. |
| ID-07 Review publication | Rating/Review/publication state modeled. | Choose immediate vs delayed visibility in V1 Policy Baseline. |
| ID-08 Minimum verification | Progressive Customer, Individual Provider and Organization levels modeled separately. | Evidence checklist in Identity/Security design. |
| ID-09 Cancellation/dispute/no-show | Separate action, allegation, evidence, response, dispute and decision facts; manual serious-case review. | Logical Data Model and Trust/Safety design. |
| ID-10 First acceptance | Single transaction forms winner and Assignment and closes competitors. | Physical DB/backend concurrency proof required. |

# 23. Proposed Architecture Decision Log

| **ADR** | **Decision** | **Status** |
| --- | --- | --- |
| ADR-001 | Modular monolith for V1_Initial. | Proposed, high confidence. |
| ADR-002 | Relational operational store as authoritative source. | Proposed, high confidence. |
| ADR-003 | Private object storage for media with database metadata. | Proposed, high confidence. |
| ADR-004 | Managed identity; initial email/Google path; progressive phone verification. | Proposed, medium confidence. |
| ADR-005 | In-app notification history plus selected email notifications. | Proposed, medium-high confidence. |
| ADR-006 | One deployment region; zone redundancy by provider/cost; no active-active multi-region. | Proposed, high confidence. |
| ADR-007 | Purposeful business events in operational store; no V1 warehouse. | Proposed, high confidence. |
| ADR-008 | Provider adapters for identity, storage, notifications and maps. | Proposed, high confidence. |
| ADR-009 | Platform Administrator and Organization Administrator are separate authorization domains. | Approved constraint. |
| ADR-010 | Transactional first-valid acceptance and one active Assignment. | Approved constraint. |
| ADR-011 | Database-backed outbox/work queue before dedicated broker. | Proposed, high confidence. |
| ADR-012 | Marketplace authoritatively owns Assignment identity and active/terminal authority. | Proposed, high confidence. |
| ADR-013 | Discovery & Matching is an explicit read/composition capability, not source-data owner. | Proposed, high confidence. |
| ADR-014 | Material selection/acceptance context is immutable or snapshotted. | Proposed, high confidence. |

# 24. Deferred Technology and Policy Decisions

| **Decision** | **Why deferred** | **Required before** |
| --- | --- | --- |
| Cloud provider | Credits, regional service availability, economics and operational fit. | Deployment design. |
| Backend and frontend stack | Must follow architecture, hiring and weak-network needs. | Detailed application design. |
| Database vendor | Relational requirement is clear; product/vendor remains open. | Physical data design. |
| Exact state encoding | Semantics are set; persistence representation is not. | Logical/physical data design. |
| RPO/RTO numbers | Need provider capabilities and accepted budget/risk. | Production approval. |
| Expiry durations | Operational product policy. | V1 Policy Baseline. |
| Review timeout | Product/UX decision. | V1 Policy Baseline. |
| Upload limits/video | Needs network, cost and safety spike. | MVP scope. |
| Verification evidence | Needs security/legal/product research. | Identity/Security design. |
| Retention periods | Needs legal/privacy and operational review. | Production approval. |
| Rate-limit thresholds | Needs threat model and usage tests. | Backend/Security design. |
| Exact outbox mechanics | Technology-specific implementation detail. | Backend/Physical DB design. |

# 25. Logical Data Model Handoff

- Define logical entities, identifiers, attributes, mandatory/optional fields, cardinalities, ownership and sensitivity.

- Resolve a platform-independent selection-cycle validity representation.

- Define Job/Response version or snapshot strategy for material accepted context.

- Define active/terminal uniqueness for Response, Selection Cycle and Assignment.

- Preserve separate Completion, closure, cancellation, allegation, dispute and responsibility facts.

- Separate approximate Job location, exact address and disclosure history.

- Separate Identity, role participation, Provider Profile, Organization membership and platform privilege.

- Model outbox/work items and privileged audit independently from product analytics.

- Keep media binary content outside the logical relational store.

- Produce ER diagrams and constraint catalogue without choosing indexes or vendor-specific types.

# 26. Backend, Frontend, and MVP Handoffs

| **Next design** | **Required outputs** |
| --- | --- |
| Backend design | Module/package rules, use cases, commands/queries, authorization matrix, transaction boundaries, idempotency, outbox handlers, integration adapters, test strategy. |
| Frontend/UX design | Role journeys, navigation, forms, exact/approximate location experience, status communication, drafts, upload retry, accessibility, localization and API needs. |
| V1 Policy Baseline | Completion and expiry behavior, categoryless distribution, contact/address rules, Review publication, verification levels, organization inclusion, media limits and dispute handling. |
| Physical data design | Tables, columns, data types, keys, indexes, constraints, migrations, concurrency mechanism, backup/restore configuration. |
| MVP delivery plan | Vertical slices, acceptance criteria, dependencies, production gates, validation metrics and deferred features. |

# 27. Launch Gates

| **Gate** | **Must be demonstrated** |
| --- | --- |
| Concurrency | Two simultaneous acceptance attempts produce exactly one winner and one active Assignment. |
| Authorization | Cross-user, cross-organization and stale-link access tests fail safely. |
| Media | Unvalidated/private media cannot become publicly visible; EXIF/location removed where required. |
| Async reliability | Committed notification/work intent survives process crash and duplicate execution is safe. |
| Recovery | Database restore and critical media/evidence recovery tested. |
| Operations | Health, logs, alerts, migrations, rollback and incident runbooks available. |
| Privacy | Disclosure history, future-access revocation, account closure and administrative export/deletion path defined. |
| Lifecycle | Closure, cancellation, no-show, Deal Not Made, dispute and Completion paths remain distinguishable. |
| Global data | Place hierarchy, currencies, time zones, phone/address formats tested beyond launch Market. |
| MVP scope | Every included capability maps to approved requirements and accepted implementation policy. |

# 28. Approval

Approval of this corrected Architecture and Data Design v0.1 authorizes Logical Data Model v0.1. It does not approve a cloud provider, programming stack, physical schema, implementation estimate, or production launch.

| **Role** | **Decision** | **Date** |
| --- | --- | --- |
| Founder / Architecture Authority | Approve / Revise |  |
| Architecture Review | Third-party findings reconciled and incorporated | 2026-07-08 |

# Appendix A. Revision Summary

- Corrected one-Provider wording for sequential Assignments.

- Added Selection Cycle validity and stale-request protection.

- Expanded Job closure, decline/invalidation, cancellation/reopen, Deal Not Made, no-show and completion-dispute flows.

- Separated Completion, closure, cancellation, allegation, dispute and responsibility facts.

- Added immutable/snapshotted material selection and agreement context.

- Added Discovery & Matching ownership, categoryless Jobs and Profile-Originated Conversation.

- Resolved Assignment ownership between Marketplace and Fulfilment.

- Mapped ID-01 through ID-10.

- Added durable outbox/background-work baseline.

- Added security, media, privacy-lifecycle and operational launch controls.

- Clarified single-region/zone wording and future RPO/RTO selection.

- Recorded profile-created Job decision as current founder supersession.

# Appendix B. Source Status

| **Source** | **Status** |
| --- | --- |
| Gold SRS v0.2 | Frozen authoritative requirements baseline. |
| Domain Model v0.1 | Frozen approved domain baseline. |
| Founder architecture interview | Authoritative source for architecture priorities and product trade-offs. |
| Third-party review | Advisory critique, accepted only after reconciliation. |
| Architecture and Data Design v0.1 | Corrected candidate; becomes baseline after founder approval. |
