# Service Platform — Mobile Application Development (MAD) Project

A cross-platform Flutter mobile application for connecting household clients with local service providers (electricians, plumbers, AC technicians, cleaners, and handymen).

---

## Project Structure

```text
service_platform/
├── AGENTS.md                            # Coding guidelines & architecture reference
├── docs/
│   ├── 01_PROJECT_PROPOSAL.md           # MAD Lab proposal, scope, and milestone plan
│   ├── 02_PRODUCT_REQUIREMENTS.md       # Functional requirements & app rules
│   ├── 03_DOMAIN_AND_DATA_MODEL.md      # Entities, fields, enums & state diagrams
│   └── 04_USER_FLOWS_AND_SCREENS.md     # Screen inventory, UI flows & form validations
├── mobile/                              # Flutter mobile client (Android & iOS)
└── backend/                             # Cloud database, auth & storage setup
```

---

## Core Workflow (`ServiceRequest -> Bid -> Booking -> Review`)

1. **Post a Service Request (`CLIENT`)**:
   - A client creates a request specifying the category, problem description, neighborhood/city, estimated budget, and optional photos.
2. **Submit a Bid (`PROVIDER`)**:
   - Local providers browse `OPEN` requests in their area and submit a `Bid` with their proposed price and note.
3. **Accept Bid & Create Booking (`CLIENT`)**:
   - The client compares bids, inspects provider profiles/ratings, and taps **Accept Bid** to immediately create a `CONFIRMED` `Booking`.
4. **In-App Chat & Completion (`CLIENT` & `PROVIDER`)**:
   - Both sides coordinate via in-app chat, the provider marks the job `WORK_DONE`, and the client confirms `COMPLETED`.
5. **Rating & Review (`CLIENT`)**:
   - After completion, the client leaves a `1–5` star review on the provider's profile.
