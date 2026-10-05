**DOMAIN MODEL**

**Local Verified Services Marketplace**

*Approved Strategic and Conceptual Domain Baseline v0.1*

| **Document field** | **Value** |
| --- | --- |
| Status | Approved domain baseline; frozen for architecture, conceptual data modeling, and MVP planning |
| Requirements authority | Local Services Marketplace Gold SRS v0.2 |
| Decision authority | Founder-approved clarifications made during domain modeling |
| Scope | Language, actors, workflows, lifecycle, events, invariants, subdomains, contexts, and conceptual model |
| Excluded | Database schema, APIs, UI design, infrastructure, framework selection, and detailed implementation decisions |
| Revision note | Corrected consistency issues without reopening or rewriting the Gold SRS |

| **Control rule** The Gold SRS remains authoritative for requirements. This document explains the domain. Implementation policies listed as unresolved must be decided during architecture, data modeling, or MVP planning without rewriting the SRS unless a genuine contradiction is discovered. |
| --- |

# 1. Purpose and Final Status

This document is the approved Domain Model v0.1 for the Local Verified Services Marketplace. It translates the Gold SRS into business language, behavior, responsibilities, consistency rules, and logical boundaries. It is sufficiently complete to end the dedicated domain-modeling stage. Later implementation work may refine physical structures without changing the business meaning recorded here.

# 2. Executive Domain Summary

A Customer publishes a Job or discovers Provider Profiles. Providers submit flexible Responses. The Customer may issue Selection Requests to multiple eligible Providers. The first valid acceptance forms the single active Assignment and makes all competing Selection Requests unavailable. Price, scope, inspection findings, and schedule may continue to evolve after Assignment formation. Work may complete successfully, end without a broader deal after preliminary inspection, or end through withdrawal, cancellation, dispute, or another explicit outcome. Reputation is derived only from legitimate marketplace activity.

# 3. Modeling Guardrails

- Domain distinctions do not automatically require separate screens, tables, services, or microservices.

- The model preserves OPEN requirements as implementation policy decisions.

- V1_Initial favors minimal cognitive and implementation complexity.

- Logical bounded contexts may be implemented together in a modular monolith.

- Database and architecture must enforce domain invariants rather than redefine them.

# 4. Approved Domain Principles

| **ID** | **Principle** | **Approved meaning** |
| --- | --- | --- |
| DP-01 | Job is not Work | A Job expresses demand. Work is actual service performance. |
| DP-02 | Flexible Response | A Response may be one-click interest or include message, price, inspection, availability, or schedule. |
| DP-03 | Selection is not Assignment | A Selection Request is an invitation to accept responsibility. Assignment begins only on valid Provider acceptance. |
| DP-04 | Multiple Selection Requests | A Customer may issue requests to multiple eligible Providers. |
| DP-05 | First valid acceptance wins | Exactly one valid acceptance forms the Assignment; all competing requests become unavailable. |
| DP-06 | One active Assignment | A Job may have sequential Assignments, but never more than one active Assignment. |
| DP-07 | Negotiation may continue | Final price, scope, and schedule need not be settled when Assignment begins. |
| DP-08 | Two inspection modes | Inspection may be the agreed service or a preliminary activity. |
| DP-09 | No deal after inspection | A preliminary inspection may end as Deal Not Made After Inspection, not automatically as cancellation. |
| DP-10 | Organizational accountability | The organization responds, accepts responsibility, assigns a worker, and formally reports completion. |
| DP-11 | Historical stability | Completed Jobs remain closed. A recurring issue creates a new Job; V1 requires no linkage. |
| DP-12 | V1 simplicity | Unrelated multi-trade work uses separate Jobs; V1 does not split Jobs automatically. |

# 5. Ubiquitous Language

| **Term** | **Business meaning** |
| --- | --- |
| Customer | Person or organization seeking service and controlling a Job. |
| Provider | Individual or organization offering supported local services. |
| Individual Provider | Person responding and accepting responsibility personally. |
| Organizational Provider | Shop, agency, or company responding and accepting responsibility as an organization. |
| Associated Worker | Person associated with an Organizational Provider. |
| Assigned Worker | Associated Worker designated to perform a specific organizational Assignment. |
| Provider Profile | Discoverable representation of Provider type, services, areas, verification, and legitimate history. |
| Job | Published Customer request for assistance, diagnosis, inspection, repair, installation, maintenance, or other supported service. |
| Response | Provider expression of interest, optionally containing proposals or operational information. |
| Selection Request | Customer request asking an eligible Provider to accept responsibility for a Job. |
| Assignment | Relationship formed when a Provider validly accepts a Selection Request. |
| Agreement | Mutual acceptance of particular terms such as scope, price, or schedule. |
| Inspection | Assessment that is either the agreed service or a preliminary activity. |
| Work | Actual performance of the requested or agreed service. |
| Completion | Recorded conclusion of Work under the configured confirmation policy. |
| Successful Job | Published Job with Provider selection, Work performance, and recorded Completion. |
| Deal Not Made After Inspection | Non-success outcome after preliminary inspection where broader Work is not agreed. |
| Job Withdrawal | Customer closure before Assignment. |
| Response Withdrawal | Provider removal or replacement of an unselected Response. |
| Selection Decline | Provider refusal of a Selection Request. |
| Assignment Cancellation | Termination of an active Assignment before successful Completion. |
| No-show Allegation | Customer claim that the Provider failed to arrive within an agreed arrival window; not confirmed misconduct by default. |
| Rating | Job-linked evaluative score from one party about the other. |
| Review | Written reputation feedback governed by publication policy. |
| Reputation | Broader legitimate marketplace history, not merely star ratings. |
| Complaint | Problem report connected to legitimate marketplace activity. |
| Dispute | Contested completion, cancellation responsibility, complaint matter, or other marketplace fact. |
| Service Category | Platform-governed classification used for discovery and matching. |
| Market | Geographic service area configured as active or inactive. |
| Verification | Progressive trust evidence, distinct from professional Certification. |

# 6. Actors and Responsibilities

| **Actor** | **Responsibilities** | **Restrictions** |
| --- | --- | --- |
| Customer | Publishes and withdraws Jobs; searches Profiles; communicates; issues Selection Requests; negotiates; confirms or disputes Completion; cancels; complains; rates qualifying Work. | No self-dealing, fabricated reputation, or unrelated private-data access. |
| Individual Provider | Maintains Profile; discovers Jobs; submits/replaces Responses; accepts or declines Selection Requests; performs Work; reports Completion; cancels; complains; rates. | No self-review, false certification, or premature access to protected details. |
| Organizational Provider | Responds and accepts responsibility; assigns worker; discloses Assigned Worker; manages commercial terms; formally reports Completion. | Associated Workers do not independently respond for the organization in the initial model. |
| Assigned Worker | Performs assigned Work and communicates operational information, arrival details, questions, and findings. | Does not own the organization Response or formal Completion claim. |
| Platform Governance | Governs categories and markets; facilitates complaints; applies policy; may restrict substantiated misconduct. | Does not guarantee payment, workmanship, compensation, refunds, or legal resolution. |
| Waitlist Registrant | Registers service interest in an inactive Market. | Cannot operate a live Job in an inactive Market. |

# 7. End-to-End Workflows

| **Workflow** | **Business flow** |
| --- | --- |
| Job-driven discovery | Publish Job in Active Market → eligible Providers discover → Responses submitted → Customer evaluates → one or more Selection Requests issued → first valid acceptance creates Assignment → competing requests close → terms/inspection/schedule/Work → Completion or explicit non-success outcome. |
| Profile-driven discovery | Customer searches Provider Profile → communicates, creates a lightweight Job, or invites Provider to existing Job. Any created Job follows the applicable visibility policy. Profile communication alone creates no completed history or Rating eligibility. |
| Organizational fulfilment | Organization responds → Customer issues Selection Request → organization accepts → Assignment forms → organization assigns worker → Customer is informed before arrival → worker performs and communicates → organization formally reports Completion. |
| Inspection-first | Inspection proposed and agreed → inspection performed → if inspection is the agreed service, Completion may follow → if preliminary, parties negotiate broader Work → agreement leads to Work; no agreement leads to Deal Not Made After Inspection and the Job may reopen. |
| Sequential Assignment | An active Assignment ends without success → Job may reopen → Customer may evaluate valid Responses or obtain new ones → new Selection Requests → later Assignment. Historical Assignments remain stable. |
| Completion and reputation | Provider or organization reports Completion → configured policy confirms or disputes → qualifying Completion records Successful Job → each party may create at most one active Rating of the other for that Job. |
| Inactive Market | Person cannot publish a live Job → may register waitlist or demand interest → future Market activation enables normal marketplace activity. |

# 8. Lifecycle Model

## 8.1 Job lifecycle

| **State** | **Meaning** |
| --- | --- |
| Draft | Customer is preparing the Job. |
| Published | Live and discoverable under Market, category, relevance, and visibility policy. |
| Selection Pending | One or more Selection Requests are open; no Assignment yet. |
| Assigned | One Provider has accepted and exactly one active Assignment exists. |
| Reopened | Prior Assignment ended without success and Job is available again. |
| Completed | Qualifying Work has been completed and recorded. |
| Closed Without Assignment | Withdrawn, expired, resolved independently, no response, no acceptable response, or platform closed. |
| Disputed | A material outcome is contested and must not silently count as success. |

## 8.2 Assignment lifecycle

| **State** | **Meaning** |
| --- | --- |
| Active | Provider accepted responsibility; terms may still be open. |
| Inspection Planned | Preliminary or deliverable inspection agreed. |
| Work Scheduled | Schedule or arrival window agreed. |
| In Progress | Inspection or Work is being performed. |
| Completion Reported | Provider or organization claims Work is complete. |
| Completed | Completion recorded under configured policy. |
| Cancelled | Assignment terminated with actor, reason, allegation, and attribution history. |
| Deal Not Made After Inspection | Preliminary inspection occurred but broader Work was not agreed. |
| Disputed | Completion, cancellation responsibility, no-show, or complaint is contested. |

| **Selection coordination** Multiple Selection Requests may be open simultaneously. Only the first valid acceptance may form the Assignment. This coordination is a domain responsibility; later design will decide whether it lives inside Job, Assignment formation logic, or another physical structure. |
| --- |

# 9. Command Catalogue

| **Command** | **Initiator** | **Target** |
| --- | --- | --- |
| Publish Job | Customer | Job |
| Withdraw Job | Customer | Job |
| Submit Response | Provider | Job |
| Replace Active Response | Provider | Response |
| Withdraw Response | Provider | Response |
| Invite Provider | Customer | Provider + existing Job |
| Create Job from Profile | Customer | Provider Profile |
| Issue Selection Request | Customer | Eligible Provider associated with Job |
| Accept Selection Request | Provider | Valid Selection Request |
| Decline Selection Request | Provider | Selection Request |
| Assign Worker | Organizational Provider | Assignment |
| Propose / Accept Terms | Customer or Provider | Scope, price, or schedule |
| Propose Inspection | Customer or Provider | Assignment |
| Reschedule | Customer or Provider | Schedule |
| Report Completion | Provider or Organization | Assignment |
| Confirm / Dispute Completion | Customer | Assignment |
| Cancel Assignment | Customer, Provider, or Governance | Assignment |
| Report Provider No-show | Customer | Assignment |
| Dispute No-show Allegation | Provider | No-show Allegation |
| Submit / Respond to Complaint | Customer or Provider | Complaint |
| Submit Rating | Customer or Provider | Qualifying Completed Job |
| Govern Category | Platform Governance | Service Category |
| Activate / Deactivate Market | Platform Governance | Market |

# 10. Domain Event Catalogue

| **Event** | **Business significance** |
| --- | --- |
| JobPublished | Customer demand becomes live. |
| JobWithdrawn | Customer ended Job before Assignment. |
| JobExpired | Job closed under configured stale-job policy. |
| ResponseSubmitted | Provider expressed interest. |
| ResponseReplaced | Earlier active Response was superseded. |
| ResponseWithdrawn | Provider removed an unselected Response. |
| SelectionRequestIssued | Customer asked an eligible Provider to accept responsibility. |
| SelectionRequestAccepted | Provider accepted while request remained valid. |
| SelectionRequestDeclined | Provider declined without Assignment. |
| CompetingSelectionRequestsClosed | Winning acceptance made remaining requests unavailable. |
| AssignmentFormed | Single active Provider responsibility began. |
| WorkerAssigned | Organization designated performer. |
| AssignedWorkerDisclosed | Customer was informed before arrival. |
| InspectionAgreed | Parties accepted inspection terms. |
| InspectionCompleted | Assessment was performed. |
| TermsAgreed | Parties mutually accepted specified terms. |
| AssignmentRescheduled | Schedule changed without cancellation. |
| WorkStarted | Actual service performance began. |
| CompletionReported | Provider or organization claimed Completion. |
| CompletionConfirmed | Configured policy established Completion. |
| CompletionDisputed | Completion became contested. |
| SuccessfulJobRecorded | Business success criteria were satisfied. |
| AssignmentCancelled | Active Assignment terminated. |
| DealNotMadeAfterInspection | Preliminary inspection ended without broader agreement. |
| JobReopened | Job became available after non-success Assignment. |
| ProviderNoShowAlleged | Customer alleged Provider absence after agreed arrival window. |
| ProviderNoShowDisputed | Provider contested the allegation. |
| CancellationResponsibilityConfirmed | Configured policy established attribution. |
| ComplaintSubmitted | Problem report entered review. |
| ComplaintResponseSubmitted | Counterparty responded. |
| RatingSubmitted | Qualifying job-linked reputation input was created. |
| MarketActivated | Live marketplace enabled in area. |
| MarketDeactivated | New live marketplace interaction disabled in area. |

# 11. Business Invariants

| **ID** | **Invariant** |
| --- | --- |
| INV-01 | A live Job may be published only in an Active Market. |
| INV-02 | A Provider may have at most one active Response per Job. |
| INV-03 | A Customer may issue Selection Requests to multiple eligible Providers. |
| INV-04 | Only the first valid acceptance may create an Assignment. |
| INV-05 | A Job may have at most one active Assignment. |
| INV-06 | Winning acceptance makes competing Selection Requests unavailable. |
| INV-07 | Selection Request issuance alone does not create Assignment. |
| INV-08 | Assignment may exist before final price, scope, or schedule is agreed. |
| INV-09 | Preliminary inspection does not complete broader Work. |
| INV-10 | Inspection-as-deliverable may qualify as completed Work. |
| INV-11 | Deal Not Made After Inspection is distinct from Completion and ordinary cancellation. |
| INV-12 | A completed Job remains closed. |
| INV-13 | A Rating must reference one qualifying Completed Job and the counterparty. |
| INV-14 | Each party may maintain at most one active Rating of the other per Job. |
| INV-15 | Cancellation actor does not prove responsibility. |
| INV-16 | Disputed responsibility must not immediately damage public cancellation statistics. |
| INV-17 | Cancellation history remains separate from star Ratings. |
| INV-18 | The organization owns its Response and formal Completion report. |
| INV-19 | Assigned Worker identity must be disclosed before arrival. |
| INV-20 | Cross-role self-dealing and self-review are prohibited. |
| INV-21 | Profile communication without linked Job creates no completed history or Rating eligibility. |
| INV-22 | Exact address and contact details are not automatically visible to all discovering Providers. |
| INV-23 | V1 payment occurs independently; recorded price is not a payment guarantee. |
| INV-24 | Unrelated multi-trade service uses separate Jobs in V1_Initial. |

# 12. Implementation Decision Register

The following items are not reasons to rewrite the SRS or reopen domain discovery. They are implementation decisions that must be resolved at the indicated stage.

| **ID** | **Decision** | **Resolve during** |
| --- | --- | --- |
| ID-01 | Minimal persisted Job and Assignment lifecycle states | Architecture and conceptual/logical data modeling |
| ID-02 | Completion confirmation, dispute, timeout, and any auto-close behavior | MVP lifecycle design |
| ID-03 | Job expiry duration and whether expiry is automated in V1 | MVP operations and lifecycle design |
| ID-04 | Whether Selection Requests expire, and if so the duration | MVP lifecycle design |
| ID-05 | Contact and Exact Address disclosure stage and consent mechanism | Security, privacy, and UX design |
| ID-06 | Distribution of Jobs without Customer-selected categories | Discovery design |
| ID-07 | Basic Review publication timing and visibility | Reputation design |
| ID-08 | Minimum Customer, Provider, and Organization verification levels | Identity and security design |
| ID-09 | Simple cancellation, dispute, and Provider no-show recording and manual handling | Trust and safety design |
| ID-10 | Transactional enforcement of first valid acceptance and one active Assignment | Architecture, persistence, and concurrency design |

# 13. Subdomain Classification

| **Subdomain** | **Type** | **Responsibility** |
| --- | --- | --- |
| Marketplace Engagement | Core | Jobs, Responses, Selection Requests, winning acceptance, Assignment formation, sequential attempts. |
| Provider Discovery | Core | Job discovery, Provider Profile discovery, relevance, eligibility, and cold-start fairness. |
| Trust and Reputation | Core | Two-sided Ratings, legitimate history, cancellation indicators, and integrity. |
| Provider and Organization Management | Supporting | Profiles, Provider type, worker association, assignment, and disclosure. |
| Service Fulfilment | Supporting | Inspection, Work, terms, scheduling, Completion, non-success outcomes. |
| Complaints and Disputes | Supporting | Complaints, evidence, contested outcomes, cancellation and no-show attribution. |
| Service Taxonomy | Supporting | Controlled category hierarchy and governance. |
| Geographic Markets | Supporting | Location hierarchy, Market activation, and inactive-area demand. |
| Identity and Verification | Generic/Supporting | Identity linkage, roles, progressive verification, abuse resilience. |
| Communication and Media | Generic/Supporting | In-platform conversations, Job media, privacy, and disclosure. |
| Notifications | Generic | Operational notifications and prompts. |
| Audit and Policy History | Cross-cutting | Trustworthy history for analytics and policy evolution. |

# 14. Candidate Bounded Contexts

| **Deployment warning** These are logical language and responsibility boundaries, not a microservice plan. V1_Initial may implement them in one modular application and one database. |
| --- |

| **Context** | **Owns** |
| --- | --- |
| Marketplace | Job, Response, Selection Request, selection coordination, Assignment formation, Job closure and reopening. |
| Provider | Provider Profile, Provider type, organization membership, Associated Worker, and Assigned Worker disclosure. |
| Service Fulfilment | Inspection, Work, agreed terms, schedule, Completion claims, cancellation outcome, and Deal Not Made outcome. |
| Reputation | Ratings, Reviews, cancellation indicators, reputation projections, and eligibility rules. |
| Trust and Safety | Complaints, disputes, allegations, evidence, responsibility confirmation, and restrictions. |
| Taxonomy | Controlled Service Categories and category lifecycle. |
| Market | Geographic hierarchy, active/inactive status, and waitlist demand. |
| Identity and Access | Real-world identity linkage, authentication, role grants, and Verification state. |
| Communication | Conversations, Job media access, and contact/address disclosure records. |

# 15. Context Relationships

| **Relationship** | **Meaning** |
| --- | --- |
| Market → Marketplace | Market status controls whether live Job publication is allowed. |
| Taxonomy → Marketplace | Marketplace references governed categories; Taxonomy does not own Jobs. |
| Provider → Marketplace | Marketplace references Provider eligibility and accepts Provider Responses. |
| Marketplace → Fulfilment | Assignment formation starts fulfilment responsibility. |
| Provider → Fulfilment | Provides responsible Provider and Assigned Worker information. |
| Fulfilment → Reputation | Qualifying Completion and explicit outcomes inform reputation. |
| Marketplace/Fulfilment → Trust and Safety | Jobs and Assignments provide the subject of complaints and disputes. |
| Trust and Safety → Reputation | Only confirmed/substantiated outcomes may affect integrity indicators. |
| Identity → all contexts | Supplies actor identity and roles without owning marketplace behavior. |
| Communication ↔ Marketplace/Fulfilment | Conversations link to Profiles, Jobs, or Assignments and obey disclosure policy. |

# 16. Conceptual Model and Aggregate Candidates

| **Provisional structure** Aggregate candidates indicate possible consistency boundaries. Architecture and data modeling may merge or reshape them while preserving the invariants. |
| --- |

| **Candidate** | **Conceptual responsibility** | **Assessment** |
| --- | --- | --- |
| Job | Customer demand, lifecycle, response/selection availability, active Assignment reference. | Well supported. |
| Response | Provider interest and optional proposals, including active/superseded status. | Well supported; exact persistence boundary remains open. |
| Selection Coordination | Multiple Selection Requests, winning acceptance, and closure of competing requests. | Necessary responsibility; separate object is not yet required. |
| Assignment | Responsible Provider, performer, terms, schedule, inspection/work state, and outcome. | Well supported. |
| Provider Profile | Provider type, services, areas, visibility, and trust-summary references. | Well supported. |
| Organization | Associated Workers and internal assignment authority. | Supported; implementation may be deferred from V1. |
| Reputation Record | Job-linked Ratings and derived Customer/Provider indicators. | Well supported. |
| Dispute Case | Complaint, allegation, evidence, responses, contested fact, and result. | Plausible; simple recording may precede full workflow. |
| Service Category | Governed category identity, hierarchy, status. | Well supported. |
| Market | Geographic area, activation status, and demand interest. | Well supported. |
| Conversation | Participants, link to Profile/Job/Assignment, messages, and disclosure status. | Well supported. |

# 17. V1_Initial Domain Cut

## 17.1 Essential

- Basic identity linkage with Customer and Provider roles

- Active Market gate

- Small controlled category set

- Individual Provider Profile

- Publish and discover Job with minimal details and optional media

- Discover Provider Profiles

- One active Response per Provider per Job

- Multiple Selection Requests with first valid acceptance

- Exactly one active Assignment

- Basic in-platform communication

- Optional price, schedule, and inspection proposals

- Completion, withdrawal, cancellation, and Deal Not Made outcomes

- Basic two-sided job-linked Ratings

- Simple privacy rules and event history

## 17.2 Candidate subject to feasibility

- Organizational Provider Profiles

- Associated Worker management

- Assigned Worker disclosure

- Automated Job expiry

- Automated Selection Request expiry

- No-show reminder automation

## 17.3 Simplify or defer

- Worker-level reputation

- Automated dispute adjudication

- Compensation points

- Advanced emergency eligibility and incentives

- Invitation-only Jobs

- Sophisticated ranking and behavioral personalization

- Payment processing and escrow

- Mandatory recurring-Job links

- Automatic multi-trade Job splitting

- Granular media visibility controls

# 18. Risks and Guardrails

| **Risk** | **Guardrail** |
| --- | --- |
| First-acceptance race | Architecture and persistence must enforce a single winner transactionally. |
| Overloaded Job concept | Keep Job, Assignment, Work, and Completion separate. |
| Organization complexity | Preserve the model but implement only if feasible for V1. |
| Reputation contamination | Do not rate contact, application, preliminary inspection, allegation, or dispute alone. |
| Policy hard-coding | Completion, expiry, disclosure, verification, review, and dispute rules remain configurable or explicitly decided. |
| Context overengineering | Do not create microservices merely because bounded contexts exist. |
| Privacy leakage | Discovery never implies unrestricted address or contact access. |
| Historical corruption | Completed Jobs and prior Assignments remain stable historical records. |

# 19. Requirements Traceability Summary

| **Domain area** | **Gold SRS references** |
| --- | --- |
| Marketplace Engagement | BR-001–004; FR-010–027; FR-070–071 |
| Provider and Organization | FR-030–043; OPEN-003 |
| Taxonomy | FR-014; FR-050–052; OPEN-004 |
| Markets | BR-007; FR-060–064 |
| Communication and Privacy | FR-072–073; PRV-001–003; OPEN-005; NFR-011 |
| Scheduling and Fulfilment | FR-080–090; OPEN-002 |
| Cancellation and Safety | FR-091–098; OPEN-006; BRL-001 |
| Reputation | FR-100–104; SEC-001; OPEN-007 |
| Pricing and Payment Boundary | FR-110; BRL-002; DEF-001 |
| Identity and Verification | FR-001–004; FR-120–122; SEC-002–003; OPEN-001/008 |
| Data and Evolution | DR-001–006; NFR-009–010 |
| V1_Initial | Gold SRS Section 13 plus approved founder clarifications |

# 20. Architecture and Data-Modeling Handoff

The dedicated domain-modeling stage ends with this document. Architecture, conceptual/logical data modeling, and MVP planning may proceed using the Gold SRS and this Domain Model together.

- Resolve the ten implementation decisions in Section 12 at their appropriate design stage.

- Preserve first-valid-acceptance and one-active-Assignment invariants.

- Keep logical context ownership even if all modules deploy together.

- Avoid treating conceptual entities and candidates as automatic tables.

- Do not re-open the SRS unless later work exposes a genuine requirements contradiction.

- Use targeted versioned amendments rather than broad rediscovery if a correction is needed.

# 21. Approval

Domain Model v0.1 is approved as the domain baseline. It is frozen for the next stage while remaining version-controlled and amendable if architecture, data modeling, implementation, or field evidence exposes a genuine domain defect.

| **Role** | **Decision** | **Date** |
| --- | --- | --- |
| Founder / Domain Authority | Approved / pending signature |  |
| Domain Model Review | Consistency corrections incorporated | 2026-07-08 |
