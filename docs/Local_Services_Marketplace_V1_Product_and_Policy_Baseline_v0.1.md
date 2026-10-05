**V1 PRODUCT AND POLICY BASELINE**

**Local Verified Services Marketplace**

*Corrected coordinated candidate • v0.1*

| **Field** | **Value** |
| --- | --- |
| Status | Corrected coordinated candidate for joint approval with Logical Data Model |
| Authority | Gold SRS v0.2; Domain Model v0.1; Architecture and Data Design v0.1; founder decisions |
| Purpose | Implementation-ready but database-platform-independent design |
| Excluded | SQL, vendor types, indexes, triggers, cloud products, ORM mapping |
| Approval model | Coordinated candidate with V1 Product and Policy Baseline v0.1; approve together |

# 1. V1 Goal and Approval Order

V1 proves the complete marketplace spine with minimal friction and credible integrity: account entry, Job publication, discovery, Response, multiple Selection Requests, one winning active Assignment, communication, fulfilment, Completion or explicit non-success outcome, and legitimate reputation.

| **Joint approval** This V1 Policy Baseline and Logical Data Model v0.1 are coordinated candidates. Policy shapes the data model, and data modeling validates policy representability. Reconcile and approve them together; neither falsely claims the other was already final. |
| --- |

# 2. Founder-Approved V1 Decisions

| **Area** | **V1 rule** |
| --- | --- |
| Provider Profiles | One active Individual Provider Profile per Identity; multiple Categories/service areas. |
| Organization Workers | Organization-managed Worker may later claim/link a platform Identity. |
| Job edits | Minor edits allowed. Material edits create a new Version and invalidate affected Requests. |
| Worker replacement | Allowed with Customer notification before replacement arrives. |
| Organizations | Minimal V1 support: one administrator, Profile, workers, assignment and disclosure. |
| Profile-created Job | Normally published and automatically creates a Provider Invitation to the originating Provider. |
| Job expiry | Five days for a published unassigned Job; configurable. |
| Selection Request expiry | 48 hours unless terminal earlier. |
| Reviews | Immediate visibility when submitted, subject to moderation; no fourteen-day waiting rule. |
| Media | Images only in V1. Voice and short video deferred. |
| Payment | Optional price recording; no payment processing/guarantee. |

# 3. Seamless Progressive Onboarding

| **Stage** | **Required behavior** |
| --- | --- |
| Visitor | Public browsing where safe; no account. |
| Basic account | Managed email or Google sign-in, display name, locale, accepted terms. Minimal clicks and no mandatory government ID or phone OTP. |
| Customer action | Basic account plus Job-specific information and mandatory service area/approximate location. |
| Individual Provider activation | Provider Profile, Categories, service areas and operational contact; stronger proof only for Verification indicator, risk, or claimed certification. |
| Organization activation | Verified administrator Identity, Organization details and minimum organizational evidence. |
| Higher-risk action | Progressive phone/identity evidence when justified by policy or signals. |

| **Privacy boundary** Low-friction onboarding does not justify collecting every legally obtainable fact. Collect only information with a defined account, marketplace, safety, verification or analytical use. |
| --- |

# 4. Scope Classification

| **Classification** | **Capabilities** |
| --- | --- |
| Included | Managed identity; Customers; individual Providers; minimal Organizations; global geography; Active Market; Categories/Other; Jobs; images; discovery; Responses; Selection Cycles/Requests; Assignment; text communication; inspection/schedule; Completion; cancellation/no-show/dispute; Ratings/Reviews; minimum admin; durable outbox/audit. |
| Simplified/manual | Verification review, complaints, moderation, privacy requests, Discovery ranking, organization administration, operational analytics. |
| Deferred | Voice notes; short video; arbitrary files; SMS/WhatsApp; worker-level reputation; advanced emergency dispatch; sophisticated ranking; automated adjudication; self-service privacy center. |
| Excluded | Platform payments/escrow; AI categorization; microservices; Kafka; Kubernetes; multi-region active-active; warehouse/streaming platform. |

# 5. Job, Category, and Expiry Policy

| **Policy area** | **V1 rule** |
| --- | --- |
| Categories | Customer may select zero, one or multiple Categories. |
| Zero selected | At publication, SYSTEM assigns the governed Other Category. The Job appears in the broad eligible local feed. |
| Category source | Record CUSTOMER, SYSTEM or PLATFORM_ADMIN so demand for Other can guide taxonomy expansion. |
| Published Job expiry | Five days after publication if still unassigned and non-terminal. |
| Material edit | Does not automatically reset expiry. Explicit republication may establish a new configured expiry window, subject to abuse controls. |
| Reopened Job | Begins a new Selection Cycle and receives a fresh configured expiry window when republished. |
| Reminder | Not required in V1. |
| Selection Request | Expires after 48 hours or earlier upon decline, rescission, invalidation, Job closure/change, cycle end, or another Provider winning. |

# 6. Profile-Originated Flow

- Profile-Originated Conversation may begin before a Job.

- Creating a Job from a Profile persists the originating Provider/Profile context.

- The Job follows normal publication.

- The system creates a Provider Invitation asking that Provider to view/respond.

- Provider Invitation is not a Selection Request and cannot form an Assignment.

- Only a later Selection Request and valid Provider acceptance can form Assignment.

# 7. Contact and Exact Address

| **Area** | **V1 rule** |
| --- | --- |
| Pre-Assignment contact | Hidden; in-platform communication used. |
| Post-Assignment contact | Customer and winning Provider may access the authorized operational Contact Points under the separate contact-disclosure policy. |
| Public location | Meaningful service area and approximate location are mandatory. |
| Exact address | May be supplied/confirmed after Assignment; not part of immutable public Job Version. |
| Disclosure | Exact address requires Assignment plus Customer confirmation. Disclosure records the specific address/contact value or protected snapshot, recipient, authority, policy version and time. |
| Cancellation/reassignment | Revoke future platform access and expire short-lived links; retain disclosure audit. Previously learned information cannot be erased. |

# 8. Completion Policy

| **Step** | **V1 rule** |
| --- | --- |
| Report | Responsible Provider or Organization reports Completion. |
| Persisted window | Store auto_confirmation_due_at and completion policy version when the report is created. |
| Customer response | Customer may confirm or dispute. |
| Dispute | Interim blocking fact; stops auto-confirmation and may later be resolved/superseded while history remains. |
| Auto-confirmation | After seven days only if eligible and no unresolved dispute exists. |
| Final decisions | Customer confirmed, auto-confirmed, Platform resolved, or rejected/withdrawn if supported; prior reports/disputes retained. |
| Inspection as deliverable | May complete Job. |
| Preliminary Inspection | Does not complete broader Job; no wider agreement may end as Deal Not Made After Inspection. |

# 9. Rating and Review Policy

- One star Rating and optional written Review per direction for a qualifying Completed Job.

- Each submitted Rating/Review becomes visible immediately, subject to moderation.

- No fourteen-day waiting rule.

- Preliminary Inspection, Response, messaging, cancellation or Profile contact alone creates no star-Rating eligibility.

- Cancellation/integrity history remains separate from stars.

# 10. Verification and Organization Policy

| **Subject** | **Minimum V1** |
| --- | --- |
| Customer | Verified managed email/social Identity and display name; stronger proof only when risk/action requires. |
| Individual Provider | Verified login, Provider Profile, Categories, service areas and operational Contact Point; stronger evidence for Verification indicator. |
| Certification claim | Supporting evidence required before presenting claim as verified. |
| Organization | Verified administrator Identity, Organization details and minimum organization evidence before organizational Verification. |
| Worker | Organization-managed record allowed; account linking optional initially. |
| Platform Administrator | Strong/step-up authentication and privileged audit. |

# 11. Self-Dealing and Abuse Policy

A Customer must not respond to the Customer’s own Job, receive or accept a Selection Request through the Customer’s own Provider Profile or controlled Organization, become assigned through a known controlled Provider, or create a Rating between subjects under the same known control.

The application enforces known Identity, Provider, Organization and Membership relationships. Duplicate-account evasion is addressed through progressive Verification, risk signals and manual review; perfect real-world identity uniqueness is not claimed.

# 12. Cancellation, No-show, Complaints, and Disputes

- Cancellation action, acting party, stated reason, alleged responsibility, dispute and confirmed responsibility are separate facts.

- Customer may allege Provider no-show after an agreed arrival window; Provider may respond/dispute.

- No automated guilt determination.

- Manual Platform review for reported, serious or repeated cases.

- Unconfirmed or disputed allegations do not enter public responsibility statistics.

- Platform does not guarantee refund, compensation, workmanship or legal resolution.

# 13. Communication and Media

| **Capability** | **V1 rule** |
| --- | --- |
| Text | Included for Profile, Job and Assignment contexts. |
| Images | Included with compression/resizing, preview/removal, retry, private storage, validation and EXIF/location stripping. |
| Short video | Deferred from V1. It is not an open V1 inclusion decision. |
| Voice notes | Deferred. |
| Arbitrary files | Deferred. |
| Media spike | Select only configurable image count, size, dimensions, compression and quality limits. |
| Evidence | Verification/complaint evidence receives narrower access and may receive safety hold/stronger retention. |

# 14. Manual Privacy Lifecycle

- Self-service privacy center is deferred.

- Admin-assisted account closure is a V1 operational requirement.

- Admin-assisted data export is supported.

- Admin-assisted deletion or anonymization requests are supported where appropriate.

- Legitimate safety, fraud, dispute, security or legal holds may delay/restrict deletion.

- Historical marketplace facts may be retained in minimized or pseudonymized form when justified.

- Privacy actions and decisions are privileged-audited.

# 15. Administration, Notifications, and Analytics

| **Area** | **V1 rule** |
| --- | --- |
| Platform Administration | Categories, Markets, verification, complaints/disputes, restrictions, reported content, privacy requests, basic metrics. |
| Organization Administration | Profile, Worker records, assignment/disclosure, organizational Responses and Completion. |
| Notifications | Durable in-app history and selected important email; SMS/WhatsApp deferred. |
| Analytics | Purposeful events for Jobs, Responses, Selection, Assignment, Completion/non-success, Ratings, Other-category demand, inactive-Market demand and operational health. |
| Data architecture | No V1 warehouse, streaming platform or speculative personal profiling. |

# 16. V1 Acceptance Boundaries

- Zero-category publication receives SYSTEM Other and enters eligible local discovery.

- Profile-created Job records origin and Provider Invitation without confusing it with Selection Request.

- Two simultaneous acceptances produce one active Assignment.

- Old cycle Requests and stale links cannot win.

- Material Job edits invalidate affected Requests without silently extending expiry.

- Exact address may be added after Assignment without mutating accepted Job history.

- Completion timeout remains stable under its recorded policy version and cannot override dispute.

- Known self-dealing is rejected.

- Admin-assisted closure/export/deletion requests have a safe audited path.

- Short video is absent; image limits remain configurable.

# 17. Remaining Implementation Decisions

| **Decision** | **Resolve during** |
| --- | --- |
| Image limits/compression quality | Media/frontend spike. |
| Organization/provider evidence checklist | Identity/security design. |
| Exact post-Assignment Contact Points disclosed | Privacy/UX design. |
| Material Job change classification | Backend/UX design. |
| RPO/RTO, retention and backup aging | Cloud/production design. |
| Technology stack and physical relational enforcement | Technology/physical design. |
| Rate limits and moderation escalation | Security/backend design. |
| Message retention/post-Completion communication | Privacy/UX design. |

# 18. Joint Approval

Approve this document together with Logical Data Model v0.1 after confirming their reconciliation. Joint approval freezes V1 behavior and its platform-independent representation for physical design and implementation planning.

| **Role** | **Decision** | **Date** |
| --- | --- | --- |
| Founder / Product and Data Authority | Approve both coordinated candidates / Revise |  |
| Consistency Review | Third-party findings reconciled and incorporated | 2026-07-08 |
