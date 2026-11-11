# AGENTS.md — Development Guidelines (`service_platform`)

This file provides instructions for developers and AI coding assistants working on the **Service Platform** university Mobile Application Development (MAD) Lab project.

---

## 1. Source of Truth Documents

Always align code changes with the specifications in `docs/` in this order:
1. `docs/02_PRODUCT_REQUIREMENTS.md` — Functional scope and core rules.
2. `docs/03_DOMAIN_AND_DATA_MODEL.md` — Entities, fields, status enums, and state transitions (`ServiceRequest`, `Bid`, `Booking`, `ChatMessage`, `Review`).
3. `docs/04_USER_FLOWS_AND_SCREENS.md` — Mobile screens, navigation, and form validations.
4. `docs/01_PROJECT_PROPOSAL.md` — Lab milestones and team responsibilities.

---

## 2. Core Application Rules

1. **Two User Roles (`CLIENT` and `PROVIDER`)**:
   - Users sign up with a single account and can switch between **Client Mode** (posting service requests) and **Provider Mode** (sending bids and completing bookings).
   - A user cannot submit a `Bid` on their own `ServiceRequest`.
2. **Simple Hiring Flow (`ServiceRequest -> Bid -> Booking`)**:
   - A Client posts an `OPEN` `ServiceRequest` with a title, description, category, neighborhood/city, budget estimate, and optional photos.
   - Providers browse `OPEN` requests and submit a `Bid` containing a proposed price and message.
   - When the Client taps **Accept Bid** on a `PENDING` bid:
     - That `Bid` becomes `ACCEPTED` (all other pending bids on that request become `REJECTED`).
     - A `Booking` record (`CONFIRMED`) is immediately created linking the Client and Provider.
     - The `ServiceRequest` status updates to `BOOKED`.
3. **Execution & Completion**:
   - Inside an active `Booking`, the Client and Provider can exchange in-app `ChatMessage` messages and coordinate the service visit.
   - When the work is finished, the Provider marks the booking `WORK_DONE`, and the Client taps **Complete Booking** to mark both the `Booking` and `ServiceRequest` as `COMPLETED`.
4. **Reviews**:
   - Once a `Booking` reaches `COMPLETED`, the Client can submit a `1–5` star `Review` for the Provider (published immediately, updating the Provider's average rating).

---

## 3. Repository Structure

```text
service_platform/
├── AGENTS.md
├── README.md
├── docs/
│   ├── 01_PROJECT_PROPOSAL.md
│   ├── 02_PRODUCT_REQUIREMENTS.md
│   ├── 03_DOMAIN_AND_DATA_MODEL.md
│   └── 04_USER_FLOWS_AND_SCREENS.md
├── mobile/                          # Flutter mobile application (Android & iOS)
│   ├── pubspec.yaml
│   └── lib/
│       ├── main.dart
│       └── src/
│           ├── core/                # Theme, constants, router
│           ├── models/              # Data models matching 03_DOMAIN_AND_DATA_MODEL.md
│           ├── services/            # Cloud auth, database & storage repositories
│           └── features/            # Screens & widgets (auth, client, provider, chat, profile)
└── backend/                         # Cloud database schema & security rules
```
