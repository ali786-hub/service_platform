**SOFTWARE REQUIREMENTS
SPECIFICATION**

**Local Verified Services Marketplace**

Gold Requirements Baseline v0.2

| **Document field** | **Value** |
| --- | --- |
| Status | Gold requirements baseline approved for domain modeling |
| Document nature | Single authoritative, living, version-controlled SRS |
| Product stage | Approved requirements baseline; domain modeling is the next stage |
| Primary authoring source | Founder requirements discovery session, Questions 1–24 |
| Prepared for | Founder, future contributors, reviewers, and implementation planning |
| Prepared on | 2026-07-08 |

**Document principle**

This SRS captures the intended product requirements discovered to date. It deliberately preserves unresolved requirements instead of pretending that operational policies are final. It is not an architecture, database schema, UX design, or technology-selection document.

# 1. Document Control

| **Version** | **Status** | **Purpose** | **Change authority** |
| --- | --- | --- | --- |
| 0.1 | Superseded | Initial founder-review baseline from Q1–Q24 | Founder |
| 0.2 | Gold baseline | Incorporates independent Kimi K3 and DeepSeek V4 Pro audits plus founder decisions | Founder |

## 1.1 How this SRS should be used

- Treat this document as the current source of truth for product requirements, not as an immutable contract.

- Do not infer architecture, database tables, interfaces, or technology choices unless the SRS explicitly constrains them.

- When implementation reveals a contradiction or missing requirement, update the SRS through a new version rather than silently changing behaviour.

- The V1_Initial implementation may realize only a prioritized subset of accepted requirements; that subset will be chosen after domain and feasibility analysis.

## 1.2 Requirements status vocabulary

| **Status** | **Meaning** |
| --- | --- |
| Accepted | Business intent is sufficiently clear for the current baseline. |
| Provisional | Direction is accepted but policy or scope may change after validation. |
| Open | A genuine requirement question remains unresolved. |
| Deferred | Not required for V1_Initial; retained for future consideration. |
| Hypothesis | A belief requiring evidence; not treated as fact. |
| Superseded | Earlier idea replaced after contradiction or review. |
| Rejected | Explicitly excluded from the current product direction. |

## 1.3 Normative language

| **Term** | **Meaning** |
| --- | --- |
| Shall | Mandatory accepted requirement. |
| Should | Desired but non-mandatory objective or provisional direction. |
| May | Permitted or optional capability. |
| Must not | Prohibited behaviour. |

## 1.4 Scope-label vocabulary

| **Scope label** | **Meaning** |
| --- | --- |
| Intended Product | Belongs to the continuing product vision, independent of release timing. |
| V1_Initial Candidate | May be selected for the first implementation after domain and feasibility analysis. |
| V1_Initial Principle | Must guide V1_Initial even when not implemented as a standalone feature. |
| Future Capability | Explicitly postponed beyond V1_Initial. |
| Boundary | States what the platform does not do or guarantee. |
| Cross-Cutting Requirement | Applies across several capabilities or domains. |
| Open | Requires later judgment or validation. |

## 1.5 Authoritative-document policy

This v0.2 document is the single controlled and authoritative SRS. The former Concise SRS is retired as an independently maintained requirements artifact. Temporary summaries may be generated from this SRS but do not become requirements sources.

# 2. Purpose

This SRS defines the current business, user, functional, data, privacy, security, quality, and evolution requirements for a local services marketplace. It is intended to provide enough precision for domain modeling, architectural analysis, schema design, implementation planning, and later verification.

# 3. Product Vision

The product connects people who need local services with relevant service providers. Customers can publish a service request or discover provider profiles directly. Providers can discover relevant work, respond flexibly, negotiate when necessary, and build legitimate reputation through completed marketplace activity.

# 4. Product Scope

The product supports local services broadly, including household, personal, commercial, repair, maintenance, diagnostic, and other skill-based services. Plumbing, electrical work, and AC services are expected early categories, but the product is not defined as a home-repair-only marketplace.

# 5. Product Positioning

The platform is primarily a discovery, trust, matching, communication, and marketplace-history system. V1 does not act as an escrow provider, payment guarantor, price enforcer, workmanship guarantor, or legal dispute-resolution service.

# 6. Scope Boundaries

## 6.1 In intended product scope

- Customer job/service-request publication

- Provider job discovery and response

- Direct provider-profile discovery

- Provider invitation to an existing job

- Flexible pricing and inspection workflows

- Scheduling and rescheduling

- Individual, shop, agency, and company providers

- Two-sided reputation

- Cancellation responsibility and history

- Complaints and disputes

- Controlled service taxonomy

- Active/inactive geographic markets

- Privacy-conscious in-platform communication

- Progressive verification

- Operational and analytical data collection

## 6.2 Explicit V1 exclusions or non-obligations

- Platform collection or escrow of service payments

- Guaranteed refunds, compensation, workmanship, or legal resolution

- AI-based classification or recommendation

- Fully automated moderation

- Advanced emergency dispatch

- Perfect identity verification

- Complete workforce-management software for companies

- All possible service categories at launch

- Immediate national-scale infrastructure

# 7. Domain Glossary (Preliminary)

| **Term** | **Current requirements meaning** |
| --- | --- |
| Customer | A person or organization seeking a local service. |
| Provider | An individual, shop, agency, or company offering local services. |
| Worker | A person who physically performs work, either independently or for an organizational provider. |
| Job / Service Request | A customer request for assistance, diagnosis, inspection, repair, installation, maintenance, or other service. It may exist without a known solution, worker, final price, or agreement. |
| Response | A provider expression of interest in a job. It may be a one-click application or contain a message, price, inspection request, availability, scheduling proposal, or counter-proposal. |
| Selection | The customer chooses one provider response for the job. |
| Assignment | The relationship formed when a provider is selected and accepts responsibility for the job. |
| Inspection | A visit or assessment intended to understand a problem, scope, or price. Inspection may be the contracted deliverable of a job, in which case performing it constitutes work, or a preliminary activity within a broader job, in which case it does not by itself complete that broader job. |
| Successful job | A published job for which a provider is selected, work is performed, and completion is recorded under the prevailing completion policy. |
| Active location | A geographic market in which live jobs and provider interactions are enabled. |
| Verification | Progressive evidence intended to improve trust. Verification is not equivalent to formal professional certification. |
| Reputation | Legitimate history derived from qualifying marketplace activity, including ratings, completed jobs, cancellations, and other integrity indicators. |
| Agreement | Mutual acceptance by customer and provider of specific terms such as scope, price, or schedule. Whether Agreement becomes a distinct domain concept or part of an Assignment is reserved for domain modeling; in this SRS, 'agreed' means both parties accepted the relevant terms. |

# 8. Stakeholders and User Classes

| **User class** | **Needs and characteristics** |
| --- | --- |
| Customer | Needs a service with minimal friction; may know the required work or only a symptom; may search providers or publish a job. |
| Individual provider | Offers services personally, discovers jobs, responds, negotiates, schedules, and completes work. |
| Shop provider | Represents a physical shop and may provide or assign workers. |
| Agency provider | Represents a service agency and may manage multiple associated workers. |
| Company provider | Represents a registered organization and may manage organization-level identity, profile, services, and workers. |
| Worker associated with organization | Performs assigned work under an organization; exact reputation model remains open. |
| Platform governance role | Manages controlled categories, locations, policies, safety, moderation, and disputes. Staffing and implementation are outside current requirements. |
| Founder/product authority | Owns requirements decisions, prioritization, policy evolution, and baseline approval. |

# 9. Business Requirements

| **BR-001** | **Broad local-services marketplace** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The product shall serve any legitimate customer seeking a supported local service, rather than being limited to homeowners or a single trade. | Intended Product |

Discovery trace: Q1

| **BR-002** | **Two discovery paths** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The product shall support both job-driven discovery and direct provider-profile discovery as first-class marketplace paths. | Intended Product |

Discovery trace: Q1, Q7

| **BR-003** | **Connection without relationship ownership** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform shall facilitate discovery, trust, matching, and history without claiming ownership of the parties’ future relationship after a job. | Intended Product |

Discovery trace: Q3

| **BR-004** | **Marketplace success definition** | **Accepted** |
| --- | --- | --- |
| **Requirement** | A platform job shall count as successful only after publication, provider selection, work performance, and recorded completion. 'Work performance' includes inspection or diagnosis when that is the agreed deliverable. Applications, preliminary inspections, conversations, and profile contacts alone shall not count as successful jobs. | Intended Product |

Discovery trace: Q4

| **BR-005** | **Provider-funded monetization hypothesis** | **Hypothesis** |
| --- | --- | --- |
| **Requirement** | The long-term business may monetize provider access to opportunities or related provider-side value after the marketplace achieves sufficient demand. This is a hypothesis, not a V1 commitment. | Future Capability |

Discovery trace: Q2

| **BR-006** | **Free/low-friction initial operation** | **Provisional** |
| --- | --- | --- |
| **Requirement** | The initial platform may operate without platform fees to reduce adoption friction and learn marketplace behaviour. | V1_Initial Candidate |

Discovery trace: Q2, Q20

| **BR-007** | **Geographic expansion** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The product shall support gradual activation of new locations without making the business model or core domain Pakistan-Town-specific. | Intended Product |

Discovery trace: Q12, Q24

| **BR-008** | **Living product policies** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Policies for verification, visibility, completion, ranking, reputation, monetization, and categories shall be expected to evolve through evidence and product versions. | Intended Product |

Discovery trace: Q5, Q10, Q11, Q16, Q24

# 10. Functional Requirements

## 10.1 Registration, onboarding, and roles

| **FR-001** | **Low-friction registration** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform shall permit users to begin with minimal friction and shall avoid unnecessary identity or profile requirements before those requirements are justified by an action or risk. | Intended Product |

Discovery trace: Q10, Q13

| **FR-002** | **Progressive data collection** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform shall collect information progressively when relevant rather than demanding a complete profile during first use. | Intended Product |

Discovery trace: Q10, Q13, Q23

| **FR-003** | **Role-separated experiences** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Customer, provider, and organization activities shall have logically separate workflows, permissions, reputation, and analytics, regardless of the later account/profile implementation. | Intended Product |

Discovery trace: Q13

| **FR-004** | **Cross-role integrity** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform shall prevent a party from using different roles to apply to, select, complete, or review its own job or otherwise manufacture marketplace reputation. | Intended Product |

Discovery trace: Q13

| **OPEN-001** | **Identity/account representation** | **Open** |
| --- | --- | --- |
| **Requirement** | Whether one platform identity has multiple profiles, logins, or another representation shall be resolved during domain and security modeling. | Open |

Discovery trace: Q13

## 10.2 Job creation and lifecycle

| **FR-010** | **Create service request** | **Accepted** |
| --- | --- | --- |
| **Requirement** | An eligible customer shall be able to create and publish a service request for assistance, diagnosis, inspection, repair, installation, maintenance, or other supported service. | Intended Product |

Discovery trace: Q2

| **FR-011** | **Known and unknown scope** | **Accepted** |
| --- | --- | --- |
| **Requirement** | A job shall support both known work and ambiguous problems whose cause, scope, solution, or price is not yet known. | Intended Product |

Discovery trace: Q2

| **FR-012** | **Optional pricing intent** | **Accepted** |
| --- | --- | --- |
| **Requirement** | A customer may omit price, provide a proposed fixed price, provide a budget or range, or leave price for later discussion or inspection. | Intended Product |

Discovery trace: Q2, Q6

| **FR-013** | **Inspection flow** | **Accepted** |
| --- | --- | --- |
| **Requirement** | A job may require an inspection before the parties know the final scope, schedule, or price. Inspection may also be the agreed deliverable of a standalone inspection or diagnosis job. A preliminary inspection does not complete a broader job unless the parties redefine inspection as the agreed deliverable. | Intended Product |

Discovery trace: Q2, Q4

| **FR-014** | **Optional categories** | **Accepted** |
| --- | --- | --- |
| **Requirement** | A customer may select one or more categories, or publish without selecting a category. Categorization exists to improve discovery and matching. | Intended Product |

Discovery trace: Q11

| **FR-015** | **Job content** | **Accepted** |
| --- | --- | --- |
| **Requirement** | A job may include ordinary-language description, photos, short video, approximate location, urgency, preferred schedule, price information, and relevant optional details. Mandatory fields shall be minimized. | Intended Product |

Discovery trace: Q1, Q6, Q21, Q23

| **FR-016** | **Minimal lifecycle** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The system shall distinguish at least published, selected/assigned, completed, cancelled, and disputed outcomes; detailed state modeling is reserved for domain modeling. | Intended Product |

Discovery trace: Q4, Q18, Q19

| **OPEN-002** | **Completion confirmation policy** | **Open** |
| --- | --- | --- |
| **Requirement** | The definitive completion policy is unresolved. The current candidate is provider marks work complete and customer confirms or disputes. The policy must support both inspection-as-deliverable and inspection-as-preliminary-activity cases and remain evolvable. | Open |

Discovery trace: Q5

| **FR-017** | **Job closure without selection** | **Accepted** |
| --- | --- | --- |
| Requirement | A published job may close without provider selection as withdrawn by customer, no responses, no acceptable response, resolved independently, expired, or closed by platform. These outcomes shall remain distinct from assignment cancellation and successful completion. The system may request closure feedback when the job remained open long enough for that feedback to be useful; immediate withdrawal shall not force unnecessary feedback. | Intended Product |

Discovery trace: External audit + founder decisions

| **FR-018** | **Job expiry** | **Accepted** |
| --- | --- | --- |
| Requirement | The platform shall support the concept of expiring stale jobs after a configurable period. The exact duration and whether expiry is automated in V1_Initial remain open. | Intended Product |

Discovery trace: External audit + founder decisions

## 10.3 Provider responses and price discussion

| **FR-020** | **One-click response** | **Accepted** |
| --- | --- | --- |
| **Requirement** | A relevant provider shall be able to express basic interest in a published job with minimal effort. | Intended Product |

Discovery trace: Q6

| **FR-021** | **Enriched response** | **Accepted** |
| --- | --- | --- |
| **Requirement** | A provider may optionally include a message, proposed or counter price, estimate/range, inspection request, earliest availability, or schedule proposal. | Intended Product |

Discovery trace: Q6

| **FR-022** | **Accept customer proposal** | **Accepted** |
| --- | --- | --- |
| **Requirement** | A provider may accept the customer’s proposed price or other stated job terms when applicable. | Intended Product |

Discovery trace: Q6

| **FR-023** | **Flexible negotiation** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform shall facilitate flexible price and schedule discussion without enforcing one universal pricing workflow. | Intended Product |

Discovery trace: Q2, Q6, Q20, Q21

| **FR-024** | **Direct provider invitation** | **Accepted** |
| --- | --- | --- |
| **Requirement** | A customer who discovers a provider through search shall be able eventually to invite that provider to respond to an existing job. | Intended Product |

Discovery trace: Q3, Q7, Q16

| **FR-025** | **No forced selection** | **Accepted** |
| --- | --- | --- |
| **Requirement** | A customer shall not be required to select any provider response and may continue provider search or allow the job to end without a deal. | Intended Product |

Discovery trace: Q1, Q3

| **FR-026** | **Provider response to selection request** | **Accepted** |
| --- | --- | --- |
| Requirement | Customer selection shall create a selection or engagement request rather than an immediate assignment. The selected provider may accept or decline. Acceptance begins the assignment; decline returns the customer to provider selection and shall not automatically affect star ratings. Repeated declines after voluntary responses may later inform a separate reliability policy. | Intended Product |

Discovery trace: External audit + founder decisions

| **FR-027** | **Profile-initiated engagement** | **Accepted** |
| --- | --- | --- |
| Requirement | A customer may start in-platform communication from a provider profile, create a lightweight job from that profile, or invite the provider to an existing job. Direct profile communication alone shall not create completed-job history or rating eligibility; lifecycle tracking and reputation require a linked job. | Intended Product |

Discovery trace: External audit + founder decisions

## 10.4 Provider discovery and profiles

| **FR-030** | **Provider search** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Customers shall be able to search and filter provider profiles independently of job posting. | Intended Product |

Discovery trace: Q1, Q7

| **FR-031** | **Visible provider type** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Profiles shall explicitly identify whether the provider is an individual, shop, agency, or company. | Intended Product |

Discovery trace: Q8

| **FR-032** | **Trustworthy profile information** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Provider profiles shall present relevant trust and service information such as supported categories, areas, verification indicators, completed work, ratings, account history, and other legitimate performance indicators as available. | Intended Product |

Discovery trace: Q7, Q14

| **FR-033** | **New-provider participation** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The product shall not permanently exclude new providers merely because they have no reviews; future discovery and ranking policies shall address cold start fairly. | Open |

Discovery trace: Q7

## 10.5 Organizational providers

| **FR-040** | **Organization profiles** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Shops, agencies, and companies shall be able to maintain organization-representative profiles distinct from individual-provider representation. | Intended Product |

Discovery trace: Q8, Q17

| **FR-041** | **Associated workers** | **Accepted** |
| --- | --- | --- |
| **Requirement** | An organization may associate workers with its provider representation and assign an associated worker internally to an accepted job. | Intended Product |

Discovery trace: Q8, Q17

| **FR-042** | **Assigned-worker disclosure** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The customer shall be informed which worker is expected to perform an organization’s assigned job before that worker arrives. | Cross-Cutting Requirement |

Discovery trace: Q17

| **OPEN-003** | **Organization and worker reputation** | **Open** |
| --- | --- | --- |
| **Requirement** | Whether completed work affects the organization reputation, worker reputation, or both remains unresolved. The initial candidate is organization-level reputation. | Open |

Discovery trace: Q17

| **FR-043** | **Organization response actor** | **Accepted** |
| --- | --- | --- |
| Requirement | For the initial organizational model, the organization profile shall submit the response and the customer shall select the organization. Associated workers shall not independently respond on behalf of the organization unless a future policy permits it. | Intended Product |

Discovery trace: External audit + founder decisions

## 10.6 Service taxonomy

| **FR-050** | **Controlled taxonomy** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Service categories shall be governed by the platform. Customers and providers shall not freely create public categories. | Intended Product |

Discovery trace: Q9

| **FR-051** | **Dynamic governance** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Authorized platform governance shall be able to add, modify, organize, activate, deactivate, or retire categories without rebuilding the application. | Intended Product |

Discovery trace: Q9, Q24

| **FR-052** | **Multiple relevant categories** | **Accepted** |
| --- | --- | --- |
| **Requirement** | A job may be associated with multiple relevant categories when the requested work spans service boundaries. | Intended Product |

Discovery trace: Q11

| **OPEN-004** | **Uncategorized-job handling** | **Open** |
| --- | --- | --- |
| **Requirement** | Jobs may be published without customer-selected categories; the exact classification and distribution policy remains unresolved. | Open |

Discovery trace: Q11

## 10.7 Geographic market availability

| **FR-060** | **Hierarchical geographic scope** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The intended product shall support countries, cities, towns/societies/phases, and other local service areas without embedding one launch location into the core business model. | Intended Product |

Discovery trace: Q12

| **FR-061** | **Active and inactive markets** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Locations may exist while inactive. Live jobs and provider interactions shall be enabled only in active markets. | Intended Product |

Discovery trace: Q12

| **FR-062** | **Unsupported-location waitlist** | **Accepted** |
| --- | --- | --- |
| **Requirement** | People outside active markets shall be able to register interest or join a location waitlist instead of reaching a dead end. | Intended Product |

Discovery trace: Q12

| **FR-063** | **Demand intelligence** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform may collect service-interest data from inactive locations to inform market expansion, subject to consent and data-minimization requirements. | Cross-Cutting Requirement |

Discovery trace: Q12

| **FR-064** | **No live inactive-area jobs** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Requests from inactive areas shall not operate as live marketplace jobs available for provider applications. | Intended Product |

Discovery trace: Q12

## 10.8 Visibility, communication, and privacy

| **FR-070** | **Relevant broad discovery** | **Accepted** |
| --- | --- | --- |
| **Requirement** | During low marketplace density, jobs shall be visible broadly enough among reasonably relevant providers in active areas to create a realistic chance of response. | V1_Initial Principle |

Discovery trace: Q16

| **FR-071** | **Future visibility modes** | **Provisional** |
| --- | --- | --- |
| **Requirement** | The intended product may support publication to eligible providers, direct invitations, both simultaneously, and later invitation-only jobs. Private-only jobs need not be in V1_Initial. | Future Capability |

Discovery trace: Q16

| **FR-072** | **In-platform communication** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Customers and providers shall be able to discuss legitimate job details within the platform. | Intended Product |

Discovery trace: Q15

| **PRV-001** | **Consent-based contact disclosure** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Personal phone numbers and email addresses shall not be disclosed merely because a provider viewed or responded to a job; disclosure requires consent or a qualifying job stage. | Intended Product |

Discovery trace: Q15

| **PRV-002** | **Restricted exact address** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Exact residential or service addresses shall not be visible to every provider discovering or responding to a job. | Intended Product |

Discovery trace: Q15, Q23

| **PRV-003** | **Purpose limitation** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Communication and information access shall be limited to legitimate marketplace use and shall not enable unrelated solicitation. | Intended Product |

Discovery trace: Q15

| **OPEN-005** | **Disclosure timing** | **Open** |
| --- | --- | --- |
| **Requirement** | The exact stage and consent mechanism for releasing contact details and exact address remain unresolved. | Open |

Discovery trace: Q15

| **FR-073** | **Published job-media visibility** | **Accepted** |
| --- | --- | --- |
| Requirement | Media intentionally attached to a published job may be viewed by providers eligible to discover that job. The platform shall warn customers before publication, permit preview and removal, prevent access by unrelated providers or inactive markets, and continue protecting exact addresses and private contact details. The interface shall not require granular per-file visibility controls in V1_Initial. | V1_Initial Principle |

Discovery trace: External audit + founder decisions

## 10.9 Scheduling and emergency work

| **FR-080** | **Scheduling modes** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Customers may request emergency, ASAP, scheduled, or inspection-based service. | Intended Product |

Discovery trace: Q21

| **FR-081** | **Schedule negotiation** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Providers may accept, reject, or counter a proposed time and state earliest availability. A schedule becomes agreed only when both parties accept it. | Intended Product |

Discovery trace: Q21

| **FR-082** | **Rescheduling** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Rescheduling shall be represented separately from cancellation. | Intended Product |

Discovery trace: Q21

| **FR-083** | **Configurable lead time** | **Accepted** |
| --- | --- | --- |
| **Requirement** | No universal 45-minute minimum shall be hard-coded as a business requirement; lead-time policies may vary. | Intended Product |

Discovery trace: Q21

| **FR-084** | **Emergency eligibility** | **Provisional** |
| --- | --- | --- |
| **Requirement** | Emergency opportunities should be restricted to providers meeting acceptable reliability and eligibility thresholds. | Future Capability |

Discovery trace: Q18

| HYP-009 | Emergency incentive | **Hypothesis** |
| --- | --- | --- |
| **Requirement** | Emergency jobs may support higher compensation or reduced future platform fees to incentivize reliable rapid response. | Future Capability |

Discovery trace: Q18

| **FR-085** | **No-show reporting** | **Provisional** |
| --- | --- | --- |
| Requirement | After an agreed arrival window, the platform may ask whether the provider arrived. A customer may report an alleged provider no-show, and the provider shall be notified and may dispute it. Exact reminder timing and automation may be simplified or deferred if infeasible for V1_Initial. | V1_Initial Candidate |

Discovery trace: External audit + founder decisions

## 10.10 Completion, cancellation, complaints, and disputes

| **FR-090** | **Completion recording** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform shall record job completion under a configurable completion-confirmation policy. | Intended Product |

Discovery trace: Q4, Q5

| **FR-091** | **Cancellation rights** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Before provider selection, a customer may withdraw a job and a provider may withdraw an unselected response. After a provider accepts a customer selection request, either party may cancel the resulting assignment and shall provide a reason. | Intended Product |

Discovery trace: Q18

| **FR-092** | Cancellation actor and responsibility | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform shall record who performed the cancellation action, the stated reason, the party alleged to have caused it, whether responsibility is agreed or disputed, and any later confirmed attribution. The cancelling actor shall not automatically be presumed responsible. Disputed responsibility shall not negatively affect public cancellation statistics until resolved or confirmed under the prevailing policy. | Intended Product |

Discovery trace: Q18

| **FR-093** | **Separate cancellation history** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Cancellation history shall remain separate from star ratings and shall not automatically modify ratings. | Intended Product |

Discovery trace: Q18

| **FR-094** | **Cancellation classification** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The system shall distinguish job withdrawal, response withdrawal, provider decline of a selection request, assignment cancellation, alleged no-show, mutually agreed cancellation reason, platform cancellation, and safety or exceptional cancellation. | Intended Product |

Discovery trace: Q18

| **OPEN-006** | **Disputed cancellation responsibility** | **Open** |
| --- | --- | --- |
| **Requirement** | When parties disagree about cancellation responsibility, the attribution and resolution policy remains unresolved. | Open |

Discovery trace: Q18

| **FR-095** | **Complaint submission** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Either party shall be able to report a problem connected to a legitimate job with a reason and optional evidence. | Intended Product |

Discovery trace: Q19

| **FR-096** | **Right to respond** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The other party shall have an opportunity to respond to a complaint or submit counter-evidence. | Intended Product |

Discovery trace: Q19

| **FR-097** | **Disputed outcome** | **Accepted** |
| --- | --- | --- |
| **Requirement** | A contested job shall be flagged or disputed rather than silently counted as successful. | Intended Product |

Discovery trace: Q19

| **FR-098** | **No automatic reputational harm** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Unsubstantiated complaints shall not automatically damage reputation. Repeated substantiated misconduct may lead to restrictions or suspension. | Intended Product |

Discovery trace: Q19

| **BRL-001** | **No initial remedy guarantee** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform initially facilitates complaint review but does not guarantee refunds, compensation, workmanship, or legal resolution. | Boundary |

Discovery trace: Q19

## 10.11 Two-sided reputation

| **FR-100** | **Mutual reputation** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Customers and providers shall both develop reputation based on legitimate marketplace activity. | Intended Product |

Discovery trace: Q14

| **FR-101** | **Customer trust indicators** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Providers shall be able to review relevant customer indicators such as completed jobs, cancellation history, account age, rating, feedback, and verification when available. | Intended Product |

Discovery trace: Q14

| **FR-102** | **Provider trust indicators** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Customers shall be able to review relevant provider indicators such as completed jobs, ratings, cancellations, verification, account history, and legitimate performance data. | Intended Product |

Discovery trace: Q7, Q14

| **FR-103** | **Qualifying feedback only** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Viewing, applying, messaging, or inspection without completed work shall not by itself create a star rating. | Intended Product |

Discovery trace: Q4, Q14

| **SEC-001** | **Reputation integrity** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform shall reduce self-review, fabricated jobs, coordinated ratings, retaliation, fake reviews, and other reputation manipulation. | Intended Product |

Discovery trace: Q13, Q14

| **OPEN-007** | **Review publication policy** | **Open** |
| --- | --- | --- |
| **Requirement** | Simultaneous publication, public versus private feedback, cancelled-job feedback, and disputed-review handling remain unresolved. | Open |

Discovery trace: Q14

| **FR-104** | **Rating-to-job linkage** | **Accepted** |
| --- | --- | --- |
| Requirement | Each rating or feedback record shall reference one specific qualifying completed job. Each party may maintain at most one active rating of the other party per job. A standalone inspection qualifies only when inspection or diagnosis was the agreed completed service. | Intended Product |

Discovery trace: External audit + founder decisions

## 10.12 Pricing records and V1 payments

| **FR-110** | **Price discussion** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform shall support price proposals, counter-proposals, estimates, ranges, inspection-first pricing, and optional recording of agreed/final price. | Intended Product |

Discovery trace: Q2, Q6, Q20

| **BRL-002** | **Independent V1 payment** | **Accepted** |
| --- | --- | --- |
| **Requirement** | In V1, customer and provider exchange payment independently. The platform does not collect, hold, distribute, refund, or guarantee payment. | Boundary |

Discovery trace: Q20

| **DEF-001** | **Platform payments** | **Deferred** |
| --- | --- | --- |
| **Requirement** | Optional or mandatory platform payment processing, escrow, and payment protection are deferred. | Future Capability |

Discovery trace: Q20

## 10.13 Verification and trust progression

| **FR-120** | **Progressive verification** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform shall support increasingly strong verification over time, with different requirements possible for customers, individual providers, and organizations. | Intended Product |

Discovery trace: Q10

| **FR-121** | **Low-friction initial verification** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Early onboarding shall require only the minimum verification justified by the immediate action and current operational risk. | Intended Product |

Discovery trace: Q10, Q13

| **FR-122** | **Verification not certification** | **Accepted** |
| --- | --- | --- |
| **Requirement** | A provider shall not be represented as formally certified unless genuine certification evidence exists. | Intended Product |

Discovery trace: Earlier project discussion + Q8/Q10

| **SEC-002** | **Ghost-job reduction** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Verification and abuse controls shall be designed to reduce fake customers, fake providers, and ghost jobs while avoiding unnecessary adoption barriers. | Intended Product |

Discovery trace: Q10, Q13

| **SEC-003** | **Multiple-account resilience** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform shall anticipate duplicate accounts and limit their ability to manipulate jobs, reviews, reputation, or analytics. | Intended Product |

Discovery trace: Q13

| **OPEN-008** | **Exact verification policy** | **Open** |
| --- | --- | --- |
| **Requirement** | Minimum customer/provider verification, evidence, timing, and escalation remain open and must evolve through validation. | Open |

Discovery trace: Q10

# 11. Data and Analytics Requirements

| **DR-001** | **Operational data** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform shall record the minimum data needed to operate jobs, responses, selections, scheduling, completion, cancellation, disputes, reputation, organizations, categories, and locations. | Intended Product |

Discovery trace: Across Q1–Q24

| **DR-002** | **Role-based analytics** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Customer and provider activities shall remain analytically distinguishable even if represented under one real-world identity. | Intended Product |

Discovery trace: Q13

| **DR-003** | **Success integrity** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Only qualifying completed jobs shall contribute to successful-job counts. Other outcomes shall be represented distinctly. | Intended Product |

Discovery trace: Q4

| **DR-004** | **Data minimization** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform shall not collect personal, behavioural, or operational information merely because it might be useful someday. Each collected field should have a defined use. | Intended Product |

Discovery trace: Q10, Q11, Q23

| **DR-005** | **Expansion intelligence** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform may analyze demand from inactive locations and unmet service needs to guide future expansion, subject to consent and privacy. | Cross-Cutting Requirement |

Discovery trace: Q12

| **DR-006** | **Policy evolution data** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The system shall preserve enough trustworthy event history to evaluate completion, cancellation, visibility, ranking, verification, and monetization policies over time. | Intended Product |

Discovery trace: Q5, Q18, Q24

| **PRV-004** | **No unnecessary personal profiling** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The platform shall not assume that a person’s attributes or past service use determine all future needs; behavioural personalization is not a current product requirement. | Boundary |

Discovery trace: Q11

# 12. Non-Functional Requirements

| **NFR-001** | **Web-first delivery** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The initial product shall be delivered as a web application before native mobile applications. | V1 |

Discovery trace: Q23

| **NFR-002** | **Mobile-first UX** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The web product shall be designed primarily for mobile screens and phone-based use. | Intended Product |

Discovery trace: Q23

| **NFR-003** | **Low-end device usability** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Core flows shall remain usable on lower-end mobile devices. | Intended Product |

Discovery trace: Q23

| **NFR-004** | **Weak-network resilience** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Core flows shall tolerate slow, unstable, or intermittent connectivity and shall present recoverable failures. | Intended Product |

Discovery trace: Q23

| **NFR-005** | **Low cognitive load** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The product shall use clear language, recognizable actions, minimal mandatory input, understandable status, and recoverable errors for users with limited technical experience. | Intended Product |

Discovery trace: Q23

| **NFR-006** | **Media failure transparency** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Media uploads shall communicate progress and failure and shall avoid silently losing customer input. | Intended Product |

Discovery trace: Q23

| **NFR-007** | **Language evolution** | Accepted |
| --- | --- | --- |
| **Requirement** | The intended product shall support English and Urdu. V1_Initial may launch in one language; the first language remains open. | Intended Product |

Discovery trace: Q23

| **NFR-008** | **Basic accessibility** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The product shall follow basic accessibility practices from the beginning, including readable text, sufficient contrast, usable touch targets, labelled forms, non-colour-only status, understandable errors, and practical assistive-technology support. | Cross-Cutting Requirement |

Discovery trace: Q23

| **NFR-009** | **Evolvability** | **Accepted** |
| --- | --- | --- |
| **Requirement** | Categories, locations, verification, visibility, ranking, reputation, and monetization policies shall be changeable without rebuilding the entire product. | Intended Product |

Discovery trace: Q5, Q9–Q11, Q16, Q23–Q24

| **NFR-010** | **Scalability path** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The product shall avoid domain and architectural decisions that fundamentally block expansion to many locations and larger usage. V1_Initial is not required to demonstrate national traffic capacity. | Intended Product |

Discovery trace: Q12, Q23, Q24

| **NFR-011** | **Sensitive-data protection** | **Accepted** |
| --- | --- | --- |
| **Requirement** | The product shall protect addresses, contact details, verification evidence, household media, private communications, and other sensitive information. | Intended Product |

Discovery trace: Q15, Q23

# 13. V1_Initial Validation Baseline

V1_Initial is a real first implementation with a deployed database and selected deployed components. It is not a disposable mock-up and is not guaranteed to be a complete public production release. Its final implementation boundary will be chosen after domain and feasibility analysis.

## 13.1 Validation objectives

- A legitimate customer can create a service request without excessive difficulty.

- Relevant providers can discover the request.

- A provider can respond minimally and optionally add a message, price, inspection request, or schedule.

- A customer can evaluate provider information and a response.

- The parties can communicate without immediate uncontrolled disclosure of private contact information.

- The customer can select a provider.

- The job can move through a minimal meaningful lifecycle.

- Legitimately completed work can produce two-sided reputation information.

- Cancellation, disagreement, and disputes are not falsely counted as successful jobs.

- The platform captures useful operational data for future requirements and policy evolution.

## 13.2 Not required to prove

- Profitability

- Payment processing or escrow

- Advanced emergency dispatch

- Perfect identity verification

- Complete organization workforce management

- AI classification

- Fully automated moderation

- All possible service categories

- Production operation at national-scale traffic

## 13.3 Candidate scope warning

No feature list in this document should be interpreted as a guarantee that every accepted intended-product requirement will be implemented in V1_Initial. Scope prioritization must consider business validation value, solo-founder capacity, domain complexity, privacy risk, and implementation feasibility.

# 14. Open Requirements Register

| **ID** | **Open decision** | **Required before** |
| --- | --- | --- |
| OPEN-001 | Account/identity/profile representation for customers, providers, and organization membership | Detailed domain and security design |
| OPEN-002 | Exact job-completion confirmation and auto-close policy | V1 lifecycle implementation |
| OPEN-003 | Organization versus assigned-worker reputation | Advanced organization support |
| OPEN-004 | Handling and distribution of uncategorized jobs | V1 job discovery |
| OPEN-005 | Exact contact/address disclosure stage and consent mechanism | V1 communication/privacy implementation |
| OPEN-006 | Resolution and confirmation policy for disputed cancellation responsibility or alleged no-show | Cancellation/dispute policy |
| OPEN-007 | Public/private/timed review publication and cancelled-job feedback | Reputation implementation |
| OPEN-008 | Exact progressive verification policy | Onboarding and verification implementation |
| OPEN-009 | First V1_Initial language | Before UX copy finalization |
| OPEN-010 | Final prioritized V1_Initial scope | After domain and feasibility analysis |

# 15. Business Hypotheses Requiring Validation

- HYP-001: Customers will value posting visual job descriptions and receiving local provider responses.

- HYP-002: Providers will respond to relevant local opportunities and accept platform-mediated discovery.

- HYP-003: Flexible responses and price discussion will fit local service behaviour better than mandatory fixed pricing.

- HYP-004: Two-sided reputation will improve trust for both providers and customers.

- HYP-005: Low-friction onboarding will generate more legitimate activity than strict early verification, without creating unacceptable abuse.

- HYP-006: A controlled but dynamically governed taxonomy will improve matching and analytics.

- HYP-007: Demand concentration in initial active locations can create enough marketplace liquidity.

- HYP-008: Provider-side monetization may become viable after sufficient demand exists.

- HYP-009: Emergency-job incentives and eligibility restrictions may improve rapid response.

- HYP-010: Some users will create multiple accounts when economic or reputation incentives exist; controls must be proportionate.

# 16. Superseded and Rejected Decisions

| **Item** | **Disposition** | **Reason** |
| --- | --- | --- |
| Separate real-world identities/accounts for customer and provider | Superseded | Role separation is required, but duplicate identities may harm analytics, trust, and abuse prevention. Final identity model remains open. |
| Users freely create public service categories | Rejected | Would fragment taxonomy, matching, search, and analytics. |
| Inspection counts as successful job | Rejected | Success requires performed work and recorded completion. |
| Lowest-price provider automatically wins | Rejected | Customer choice must consider trust, suitability, availability, reputation, and price. |
| Every response must contain a detailed proposal | Rejected | Provider may apply with one click and enrich the response optionally. |
| Cancellation automatically affects star rating | Rejected | Cancellation history is separate and attributed to the responsible party. |
| All locations blocked without any alternative | Rejected | Inactive-area users should have waitlist/demand-interest options. |
| Immediate full national infrastructure | Rejected as V1 obligation | Nationwide growth is a goal; V1 proves the marketplace rather than national traffic capacity. |

# 17. Major Product Risks

| **Risk** | **Requirement response** |
| --- | --- |
| Marketplace has insufficient customer/provider density | Broad relevant V1 visibility, concentrated active locations, waitlists, and phased expansion. |
| Fake jobs and fake accounts | Progressive verification, cancellation and completion history, two-sided reputation, and abuse resilience. |
| Privacy leakage from jobs/media | Restricted address/contact disclosure, in-platform communication, purpose limitation, and sensitive-data protection. |
| Low-price baiting or price disputes | Flexible price records, inspection-first flow, complaints, and no false claim of platform guarantee. |
| Rating manipulation | Qualifying interactions only, cross-role integrity, two-sided reputation, and anti-abuse requirement. |
| Provider no-shows or cancellations | Attributed cancellation history, scheduling history, reliability indicators, and emergency eligibility. |
| Overengineering prevents V1 delivery | V1_Initial scope remains provisional and may manually operate or defer intended-product requirements. |
| Rigid early decisions block evolution | Dynamic platform governance and evolvable policy requirements. |
| Organizations obscure worker accountability | Provider type transparency and assigned-worker disclosure; reputation policy remains open. |
| SRS treated as immutable | Document is expressly versioned and living; changes require traceable revision. |

# 18. Discovery Coverage: Questions 1–24

| **Source** | **Discovery subject** | **SRS destination** |
| --- | --- | --- |
| Q1 | Primary customer and two discovery paths | BR-001, BR-002, FR-010, FR-030 |
| Q2 | Meaning of job, inspection, pricing, platform role | FR-010–013, BR-003, BR-005–006 |
| Q3 | Future relationship and rehire/history | BR-003, FR-024–025 |
| Q4 | Successful job definition | BR-004, FR-016, DR-003 |
| Q5 | Completion confirmation | FR-090, OPEN-002 |
| Q6 | Provider response/application/offer flexibility | FR-020–023 |
| Q7 | Jobs and profiles both first-class; cold start | BR-002, FR-030–033 |
| Q8 | Individual/shop/agency/company providers | FR-031, FR-040–042 |
| Q9 | Platform-governed categories | FR-050–051 |
| Q10 | Progressive verification | FR-120–122, SEC-002, OPEN-008 |
| Q11 | Optional/multiple categories; no behavioural personalization | FR-014, FR-052, OPEN-004, PRV-004 |
| Q12 | Active/inactive locations and waitlists | BR-007, FR-060–064, DR-005 |
| Q13 | Role separation, identity ambiguity, analytics integrity | FR-003–004, DR-002, SEC-003, OPEN-001 |
| Q14 | Two-sided reputation | FR-100–103, SEC-001, OPEN-007 |
| Q15 | Hybrid in-platform communication and consent | FR-072, PRV-001–003, OPEN-005 |
| Q16 | Broad V1 visibility, future invitation modes | FR-070–071, FR-024 |
| Q17 | Organization assignment and reputation ambiguity | FR-040–042, OPEN-003 |
| Q18 | Attributed cancellation and emergency policy | FR-091–094, FR-085, OPEN-006, FR-084, HYP-009 |
| Q19 | Complaints and disputes | FR-095–098, BRL-001 |
| Q20 | No V1 payment handling | FR-110, BRL-002, DEF-001 |
| Q21 | Scheduling baseline | FR-080–083 |
| Q22 | Candidate V1 scope not finalized | OPEN-010, Section 13 |
| Q23 | Mobile/web/quality/accessibility/scalability | NFR-001–011, OPEN-009 |
| Q24 | V1_Initial validation and non-obligations | Section 13, BR-007, FR-051 |

# 19. v0.2 Change Log

| **Change** | **Reason** |
| --- | --- |
| Clarified inspection as deliverable versus preliminary activity | Removed lifecycle contradiction identified by Kimi K3. |
| Separated cancellation action, alleged cause, dispute, and confirmed responsibility | Prevents unfair attribution and supports no-show cases. |
| Added Agreement glossary term | Supports ubiquitous-language and lifecycle discovery. |
| Added job closure, expiry, provider selection acceptance/decline, profile engagement, organization response, media visibility, no-show, and rating linkage requirements | Closed high-value omissions from both independent audits and founder decisions. |
| Resolved duplicate HYP-001 and corrected Q18 trace | Restored identifier uniqueness. |
| Defined modal verbs and scope labels; normalized requirement strength and labels | Improved clarity and V1_Initial prioritization. |
| Retired Concise SRS as a controlled artifact | Established one authoritative SRS. |
| Preserved OPEN requirements that do not block domain modeling | Avoided false precision before domain discovery. |

# 20. Baseline Review Checklist

- Confirm that “job,” “response,” “selection,” “assignment,” “inspection,” and “successful job” match founder intent.

- Confirm that the intended product and V1_Initial are not being treated as identical scope.

- Confirm that open matters remain visibly open and were not silently decided.

- Confirm that privacy requirements do not unintentionally block legitimate negotiation and service delivery.

- Confirm that organization support is represented without forcing full workforce management into V1_Initial.

- Confirm that categories are dynamically governable but not user-created.

- Confirm that scaling is a growth-path requirement rather than a V1 traffic promise.

- After approval, proceed to domain modeling before architecture, schema, and technology selection.

# 21. Gold Baseline Approval

This SRS is approved as the v0.2 Gold requirements baseline for domain modeling. “Gold” means authoritative for the next engineering stages, not immutable forever. A new version is created only when later domain, architecture, schema, implementation, or field evidence reveals a genuine correction, conflict, omission, or bottleneck.

| **Role** | **Name** | **Decision** | **Date** |
| --- | --- | --- | --- |
| Founder / Product Authority |  | Approved as Gold SRS v0.2 | 2026-07-08 |
| Requirements Reviewer |  | Reviewed |  |
