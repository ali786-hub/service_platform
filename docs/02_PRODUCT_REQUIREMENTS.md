# Functional Requirements Specification

This document specifies the functional requirements for the **Service Platform** mobile application (`ServiceRequest -> Bid -> Booking -> Review`).

---

## 1. User Accounts & Role Switching

### FR-1.1 Registration & Authentication
- Users can create an account and sign in using Email/Password or Phone/Google authentication backed by the cloud auth service.
- Each account stores a `full_name`, `phone`, `city`, and current active mode (`CLIENT` or `PROVIDER`).

### FR-1.2 Client & Provider Mode Toggle
- Every registered user starts in **Client Mode** (`active_role = CLIENT`).
- A user can switch to **Provider Mode** (`active_role = PROVIDER`) from the Profile tab.
- The first time a user switches to Provider Mode, they complete a one-time **Provider Setup** form (selecting their trade categories, city/areas served, and short bio).

### FR-1.3 Self-Bidding Restriction
- A user cannot submit a `Bid` on a `ServiceRequest` that was created by their own `user_id`.

---

## 2. Service Requests (`Client` Flow)

### FR-2.1 Creating a Service Request
To post a new `ServiceRequest`, a Client provides:
- **Title**: Short summary of the task (`5–80` characters).
- **Category**: Chosen from predefined categories (`Electrical`, `Plumbing`, `AC Repair`, `Cleaning`, `Carpentry`, `Painting`, `General Handyman`).
- **Description**: Details of the issue or work needed (`10–1000` characters).
- **Location**: `city` and `area_name` (neighborhood/sector), plus an optional `address_notes` field visible once booked.
- **Budget (Optional)**: Indicative budget in PKR.
- **Photos (Optional)**: Up to `3` photos picked from the device camera or gallery and uploaded to cloud storage.

### FR-2.2 Managing Open Requests
- Newly submitted requests start in `OPEN` status.
- While a request is `OPEN`, the Client can view incoming `Bid` items from providers or cancel the request (`CANCELLED`).

---

## 3. Browsing & Bidding (`Provider` Flow)

### FR-3.1 Open Requests Feed
- In Provider Mode, the home tab displays a list of `OPEN` service requests sorted by newest first.
- Providers can filter the feed by `category` and `city`.

### FR-3.2 Submitting a Bid
- On any `OPEN` request (not posted by themselves), a Provider can submit one `Bid` containing:
  - `proposed_price` (numeric quote in PKR, required)
  - `message` (short note explaining availability/approach, required)
- A submitted bid starts with status `PENDING`.
- A Provider can withdraw or update their `PENDING` bid while the request is still `OPEN`.

---

## 4. Accepting a Bid & Booking Execution

### FR-4.1 Direct Bid Acceptance (`Client`)
- The Client views all `PENDING` bids on their `OPEN` request, including each provider's name, rating average, completed bookings count, proposed price, and message.
- When the Client taps **Accept Bid** on a chosen bid:
  1. The selected `Bid` status changes to `ACCEPTED`.
  2. All other `PENDING` bids on that `ServiceRequest` automatically change to `REJECTED`.
  3. The `ServiceRequest` status changes from `OPEN` to `BOOKED`.
  4. A new `Booking` record is created with status `CONFIRMED`.

### FR-4.2 Active Booking & In-App Chat
- Once a `Booking` is created, both Client and Provider can open the **Booking Detail Screen**:
  - View the agreed price (`agreed_price` from the accepted bid), service address details, and contact info.
  - Exchange real-time text messages in the booking's **In-App Chat** thread.

### FR-4.3 Marking Work Done & Completion
- When the provider finishes the job on-site, the Provider taps **Mark Work Done**, changing `Booking.status` from `CONFIRMED` to `WORK_DONE`.
- The Client then taps **Confirm & Complete**, which updates both `Booking.status` and `ServiceRequest.status` to `COMPLETED`.
- Either party can cancel an active booking before completion (`CANCELLED`), recording who cancelled.

---

## 5. Ratings & Reviews

### FR-5.1 Submitting a Review
- Once a `Booking` reaches `COMPLETED`, the Client is prompted to submit a `Review` for the Provider:
  - `rating` (`1` to `5` stars, required)
  - `comment` (optional written feedback)
- Only one review can be submitted per completed booking.

### FR-5.2 Immediate Publication & Rating Aggregation
- Submitted reviews are published immediately on the Provider's profile.
- The Provider's `rating_average`, `review_count`, and `completed_bookings_count` update automatically.
