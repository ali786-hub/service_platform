**LOGICAL DATA MODEL**

**Local Verified Services Marketplace**

*Corrected coordinated candidate • v0.1*

| **Field** | **Value** |
| --- | --- |
| Status | Corrected coordinated candidate for joint approval with V1 Policy Baseline |
| Authority | Gold SRS v0.2; Domain Model v0.1; Architecture and Data Design v0.1; founder decisions |
| Purpose | Implementation-ready but database-platform-independent design |
| Excluded | SQL, vendor types, indexes, triggers, cloud products, ORM mapping |
| Approval model | Coordinated candidate with V1 Product and Policy Baseline v0.1; approve together |

# 1. Modeling Rules

- Every authoritative fact has one logical owner.

- Current state and historical evidence are both represented where integrity or disputes require them.

- Generic references have documented target sets; physical design may replace them with explicit foreign keys or association records.

- Binary media is outside the relational store; metadata, validation, authorization, evidence classification and lifecycle are inside.

- The model is globally adaptable and does not hard-code one country’s geography, currency, phone, time or address structure.

# 2. Exhaustive Ownership Catalogue

| **Owner package** | **Authoritative logical records** |
| --- | --- |
| Identity & Access | Identity; Authentication Link; Contact Point; Customer Participation; Role Grant; Platform Privilege; Account Closure Request. |
| Provider Management | Provider Profile; Organization; Organization Membership; Worker Record; Provider Category; Provider Service Area. |
| Markets & Taxonomy | Place; Market; Market Coverage; Service Area; Waitlist Interest; Service Category. |
| Marketplace | Job; Job Origin; Job Version; Job Service Location; Job Category; Provider Invitation; Response; Response Version; Selection Cycle; Selection Request; Selection Acceptance; Assignment; Job Closure. |
| Fulfilment | Worker Assignment; Assignment Address Association; Assignment Terms Version; Inspection; Schedule Proposal; Agreed Schedule; Work Status Event; Completion Report; Completion Dispute; Completion Decision; Deal Not Made Outcome. |
| Communication & Media | Conversation; Conversation Participant; Message; Media Asset; Media Link; Disclosure Record. |
| Reputation | Rating; Review. Publication status is an attribute of Review, not a separate record. |
| Trust & Safety | Assignment Cancellation; Responsibility Allegation; Responsibility Decision; Provider No-show Allegation; Complaint; Case Response; Evidence Link; Restriction; Safety/Legal Hold. |
| Operations | Notification Intent; Delivery Attempt; Outbox Work Item; Business Event; Privileged Audit Event; Data Export/Delete Request. |

# 3. Identity, Contact, and Participation Records

| **Record** | **ID** | **Core attributes** | **Rule** |
| --- | --- | --- | --- |
| Identity | identity_id | status; display_name; preferred_locale; created_at; closed_at? | One human identity where possible. |
| Authentication Link | auth_link_id | identity_id; provider_type; provider_subject; linked_at; status | Unique external subject link; not the operational contact store. |
| Contact Point | contact_point_id | owner_type; owner_id; contact_type; contact_value; verification_status; purpose; is_primary; valid_from; valid_to?; status | Owner is Identity, Organization, or Worker Record. Operational contact authority. |
| Customer Participation | customer_id | identity_id; status; created_at | At most one active Customer participation per Identity. |
| Role Grant | role_grant_id | identity_id; role_type; scope_type; scope_id?; status; effective period | Platform and organization scope explicit. |
| Platform Privilege | platform_privilege_id | identity_id; privilege_type; reason; status; effective period | Separate from Organization Administrator. |
| Account Closure Request | closure_request_id | identity_id; requested_at; status; hold_reason?; completed_at? | Admin-assisted V1 privacy process. |

# 4. Provider and Organization Records

| **Record** | **ID** | **Core attributes** | **Rule** |
| --- | --- | --- | --- |
| Provider Profile | provider_id | owner_kind; individual_identity_id?; organization_id?; display_name; description; status; visibility | One active individual Profile per Identity; exactly one owner kind. |
| Organization | organization_id | legal_name; display_name; organization_type; status; verification_state | Separate legal/business subject. |
| Organization Membership | membership_id | organization_id; identity_id?; worker_id?; role; status; joined_at; ended_at? | Worker may begin unmanaged by platform identity and later claim/link. |
| Worker Record | worker_id | organization_id; name; status; claimed_identity_id? | Organization-managed performer. |
| Provider Category | provider_id + category_id | source; status; effective period | Many Categories per Provider. |
| Provider Service Area | provider_service_area_id | provider_id; service_area_id; coverage_kind; status | Global service coverage. |

# 5. Geography and Taxonomy Records

| **Record** | **ID** | **Core attributes** | **Rule** |
| --- | --- | --- | --- |
| Place | place_id | country_code; parent_place_id?; place_type; canonical/local name; timezone_id?; status | Arbitrary hierarchy. |
| Market | market_id | name; status; activation/deactivation times | Place existence does not imply activity. |
| Market Coverage | coverage_id | market_id; place_id; role; status | Market may include multiple Places. |
| Service Area | service_area_id | market_id; place_id?; label; geometry/reference?; status | Discovery-safe local area. |
| Waitlist Interest | interest_id | identity_id?; contact_point_id; place_id; category_id?; consent; created_at | Contact Point reference is authoritative. |
| Service Category | category_id | parent_category_id?; name; description?; status | Platform-governed hierarchy, including Other. |

# 6. Job, Origin, Location, and Versioning

| **Record** | **ID** | **Core attributes** | **Rule** |
| --- | --- | --- | --- |
| Job | job_id | customer_id; market_id; status; current_version_id; current_cycle_id?; active_assignment_id?; published_at?; expires_at? | Completed Job never reopens. |
| Job Origin | job_origin_id | job_id; origin_type; origin_provider_id?; origin_profile_version?; origin_conversation_id?; created_at | PROFILE origin retained when applicable. |
| Job Version | job_version_id | job_id; version_no; description; urgency; pricing/inspection/schedule intent; created_at; material_change | Immutable once referenced by Selection Request. |
| Job Service Location | job_location_id | job_id; service_area_id; approximate_label?; approximate_coordinates?; valid period | Discovery-safe location; separate from Exact Address. |
| Exact Address | address_id | owner_identity_id; country_code; structured parts; free_text?; coordinates?; valid period; status | Private reusable authoritative address. |
| Assignment Address Association | assignment_address_id | assignment_id; address_id; address_snapshot; provided_by; provided_at; confirmed_at?; status; superseded_at? | Supports post-Assignment capture without mutating Job Version. |
| Job Category | job_id + category_id | source CUSTOMER/SYSTEM/ADMIN; added_at | If none selected, SYSTEM assigns Other at publication. |
| Job Closure | job_closure_id | job_id; reason; actor; closed_at; details? | Unassigned terminal fact. |
| Provider Invitation | invitation_id | job_id; provider_id; source PROFILE/ACTION; status; issued_at; responded_at?; terminal_reason? | Requests a view/Response; never forms Assignment by itself. |

# 7. Response, Selection, and Assignment

| **Record** | **ID** | **Core attributes** | **Rule** |
| --- | --- | --- | --- |
| Response | response_id | job_id; provider_id; current_version_id; status; submitted/withdrawn times | One active Response per Provider/Job. |
| Response Version | response_version_id | response_id; version_no; message; price/schedule/inspection proposals; created_at | Immutable version. |
| Selection Cycle | cycle_id | job_id; cycle_no; status; opened_at; closed_at?; close_reason? | One open cycle per Job; old cycles never reopen. |
| Selection Request | request_id | cycle_id; job_id; provider_id; source_job_version_id; source_response_version_id?; terms_snapshot?; status; issued/expires times; terminal_reason? | Many pending allowed; fixed source context. |
| Selection Acceptance | acceptance_id | request_id; provider_id; accepted_at; idempotency_key; result | Provider must match request. |
| Assignment | assignment_id | job_id; cycle_id; winning_request_id; provider_id; organization_id?; status; formed/terminal times; terminal_reason? | Marketplace authoritative; one active per Job. |
| Worker Assignment | worker_assignment_id | assignment_id; worker_id; assigned/disclosed/ended times; change_reason? | One current Worker; replacement history retained. |

# 8. Fulfilment and Completion

| **Record** | **ID** | **Core attributes** | **Rule** |
| --- | --- | --- | --- |
| Assignment Terms Version | terms_version_id | assignment_id; version_no; scope; price; currency; inspection_mode; proposal/acceptance facts; status | Accepted versions immutable. |
| Inspection | inspection_id | assignment_id; terms_version_id?; mode DELIVERABLE/PRELIMINARY; scheduled/performed times; findings?; status | Mode determines Completion eligibility. |
| Schedule Proposal | schedule_proposal_id | assignment_id; proposer; time/window; timezone_id; status; created_at | Historical proposals retained. |
| Agreed Schedule | agreed_schedule_id | assignment_id; source_proposal_id?; time/window; timezone_id; agreed_at; superseded_at? | One current schedule. |
| Completion Report | completion_report_id | assignment_id; reporter_provider_id; reported_at; note?; auto_confirmation_due_at; policy_version; auto_confirmation_eligible | Persists timeout facts at report time. |
| Completion Dispute | completion_dispute_id | report_id; customer_id; disputed_at; reason; status; resolved_at? | Interim blocking fact, not final decision. |
| Completion Decision | completion_decision_id | report_id; decision_type CONFIRMED/AUTO_CONFIRMED/PLATFORM_RESOLVED/REJECTED; decided_by; decided_at; reason?; supersedes_id? | Final/effective decisions only; history retained. |
| Deal Not Made Outcome | deal_not_made_id | assignment_id; inspection_id; recorded_at; reason?; job_disposition | Distinct non-success terminal outcome. |

# 9. Communication, Media, and Disclosure

| **Record** | **ID** | **Core attributes** | **Rule** |
| --- | --- | --- | --- |
| Conversation | conversation_id | origin PROFILE/JOB/ASSIGNMENT; provider_id?; job_id?; assignment_id?; status | Profile conversation is legitimate context but no Rating eligibility. |
| Conversation Participant | conversation_id + participant_type + participant_id | joined/left times; access_status | Allowed targets documented below. |
| Message | message_id | conversation_id; sender actor; kind; body?; sent_at; status | Text V1. |
| Media Asset | media_id | owner_context; storage_ref; kind; content_type; size; validation/publish status; sensitivity | Private until validated and authorized. |
| Disclosure Record | disclosure_id | assignment_id; disclosure_type CONTACT/ADDRESS; contact_point_id?; address_id?; disclosed_value_snapshot; disclosed_to_identity_id; authorized_by; policy_version; disclosed_at; access_expires_at?; revoked_at? | Exactly one subject; precise disclosed value reconstructable. |

# 10. Reputation, Safety, and Operations

| **Record family** | **ID** | **Core attributes** | **Rule** |
| --- | --- | --- | --- |
| Rating / Review | rating_id / review_id | job_id; assignment_id; author/subject; stars; text?; status; submitted_at; moderation/publication state | Immediate publication in V1 subject to moderation. |
| Cancellation | cancellation_id | assignment_id; actor; reason; cancelled_at; reopen decision | Separate from responsibility. |
| Responsibility Allegation / Decision | allegation_id / decision_id | assignment; alleged_by/party; reason; dispute; evidence; result; decision authority/time | Unconfirmed allegation never public fact. |
| Provider No-show Allegation | no_show_id | assignment_id; agreed_schedule_id; customer_id; alleged_at; provider response/dispute; status | Current V1 direction. |
| Complaint / Case Response | complaint_id / response_id | legitimate activity refs; parties; reason; evidence; status; response | Manual review for serious/reported cases. |
| Verification Case / Evidence | verification_id / evidence_id | subject target; level; status; evidence type/media; decision/expiry | Narrow sensitive access. |
| Notification / Attempt | notification_id / attempt_id | recipient; event/source; channel; dedupe; status; attempt result | Durable intent. |
| Outbox Work Item | work_item_id | work type; aggregate; payload; dedupe; available/lock times; attempts; status | At-least-once and idempotent. |
| Business / Privileged Event | event_id / audit_id | type/action; actor/admin; subject/target; reason; result; timestamp; correlation | Append-only; audit separate from analytics. |
| Data Export/Delete Request | privacy_request_id | identity_id; request_type; status; hold; decision; completed_at | Admin-assisted V1 privacy process. |

# 11. Allowed Generic Reference Targets

| **Generic reference** | **Allowed targets** |
| --- | --- |
| owner_type + owner_id | Identity; Organization; Worker Record. |
| actor reference | Identity; Provider Profile; Organization acting through authorized Identity; Platform Administrator Identity. |
| conversation participant | Customer Participation; Individual Provider Profile; Organization; Worker Record or linked Identity; authorized Platform Administrator only for safety workflows. |
| reputation subject | Customer Participation; Individual Provider Profile; Organization. |
| verification subject | Identity; Individual Provider Profile; Organization; certification claim if later modeled. |
| business-event subject | Any documented authoritative business record; event type determines permitted set. |
| media owner context | Job; Message; Provider Profile; Complaint; Verification Case; other explicitly documented safety context. |
| notification source | Documented business event or authoritative record type permitted by notification type. |

# 12. Cross-Record and Self-Dealing Constraints

| **ID** | **Constraint** |
| --- | --- |
| X-01 | Selection Request.job_id equals Selection Cycle.job_id. |
| X-02 | Selection Acceptance.provider_id equals Selection Request.provider_id. |
| X-03 | Assignment job, cycle and Provider equal the winning Request’s job, cycle and Provider. |
| X-04 | Source Job Version belongs to Request Job. |
| X-05 | Source Response Version belongs to Request Job and Provider. |
| X-06 | Worker Assignment Worker belongs to Assignment’s responsible Organization. |
| X-07 | Completion reporter equals Assignment’s responsible Provider or authorized Organization. |
| X-08 | Rating author and subject equal eligible counterparties to the qualifying Assignment. |
| X-09 | Disclosure recipient is an authorized participant in the active/eligible Assignment. |
| X-10 | Address Association belongs to its Assignment and Customer-provided/confirmed address context. |
| X-11 | Customer cannot respond to, receive/accept selection through, be assigned through, or rate a Provider Profile or Organization under the same known control. |
| X-12 | Known self-dealing is enforced across Identity, Provider, Organization and Membership relationships; duplicate-account evasion remains a verification/risk/manual-review concern. |
| X-13 | One active Response per Provider/Job; one open Selection Cycle per Job; one active Assignment per Job. |
| X-14 | Old cycle Requests and stale acceptance links never reactivate. |
| X-15 | Completion Dispute blocks auto-confirmation until resolved. |

# 13. Transaction Boundaries

| **Transaction** | **Atomic/logical result** |
| --- | --- |
| Publish Job | Assign SYSTEM Other if zero Customer categories; set expiry; retain origin/invitation; create event/outbox. |
| Material Job edit | Create Job Version; invalidate affected Requests; do not automatically extend expiry; explicit republication may establish a new configured window. |
| Accept Request | Validate cross-record agreement/self-dealing/current cycle/no active Assignment; create winner; close competitors; create Assignment and outbox atomically. |
| Provide exact address | Create/choose Exact Address and Assignment Address Association; Customer confirms; disclosure separately audited. |
| Report Completion | Store policy_version and auto_confirmation_due_at with Report; create durable notification. |
| Dispute Completion | Create interim Completion Dispute and block scheduled auto-confirmation. |
| Resolve Completion | Create final Completion Decision; preserve dispute/report history; update Assignment/Job atomically. |
| Privacy request | Record request, check safety/legal hold, perform or deny administrative export/closure/deletion/pseudonymization with audit. |

# 14. Approval and Physical Handoff

This corrected Logical Data Model and the corrected V1 Product and Policy Baseline are coordinated candidates and must be approved together after reconciliation. Approval authorizes physical database, backend and API/UX design. It does not select a database vendor or SQL implementation.

- Choose exact data types, keys and foreign-key strategy.

- Replace generic references with explicit relational enforcement where practical.

- Implement active-record uniqueness and acceptance concurrency.

- Choose Job/Response snapshot representation.

- Choose indexes, geospatial representation, encryption, retention, migrations and outbox claiming.

| **Role** | **Decision** | **Date** |
| --- | --- | --- |
| Founder / Data and Product Authority | Approve both coordinated candidates / Revise |  |
| Consistency Review | Third-party findings reconciled and incorporated | 2026-07-08 |
