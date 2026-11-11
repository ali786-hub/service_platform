# Mobile Application Development (MAD) Lab — Project Proposal

**Project Title:** Service Platform — On-Demand Local Services App  
**Platform:** Android & iOS (Flutter + Cloud Backend)

---

## 1. Problem Statement

Household residents frequently struggle to find dependable local handymen, electricians, plumbers, and cleaners. Informal hiring through neighborhood groups or classifieds suffers from three practical problems:
1. **No Structured Bidding**: Clients have to call multiple providers one by one to ask for availability and price estimates.
2. **Unorganized Booking Status**: There is no single place to track whether a job is still open, booked, in progress, or finished.
3. **Lack of Verified Past Ratings**: Clients cannot easily see a technician's rating history from actual completed bookings.

## 2. Proposed Solution

We propose a cross-platform Flutter mobile application backed by a cloud database where:
- **Clients** post a `ServiceRequest` describing the task, category, location area, budget estimate, and photos.
- **Providers** browse open requests and submit a `Bid` with their price quote and message.
- **Direct Booking**: The client accepts the best `Bid` to create a `Booking`, chats with the provider in-app, confirms work completion, and leaves a `1–5` star review.

## 3. Scope of Features for MAD Lab

### Client Features
1. **Authentication & Role Toggle**: Sign up / sign in and switch between Client Mode and Provider Mode.
2. **Home & Category Browse**: View service categories (Electrical, Plumbing, AC Repair, Cleaning, Carpentry, Painting) and active requests.
3. **Post Service Request**: Form with title, description, category, neighborhood/location, optional budget, and photo upload.
4. **Compare Bids & Hire**: View incoming provider bids on an open request and tap **Accept Bid** to confirm a booking.
5. **Booking Tracking, Chat & Review**: Message the hired provider, confirm job completion, and rate the provider (`1–5` stars).

### Provider Features
1. **Provider Profile Setup**: Configure trade skills/categories, bio, and working city/areas.
2. **Open Requests Feed**: Browse `OPEN` service requests filtered by category and city/area.
3. **Submit Bid**: Send a price quote and short message on an open request.
4. **Manage Bookings**: View active bookings, chat with the client, and mark work as done (`WORK_DONE`).

## 4. Technology Stack

- **Mobile Framework**: **Flutter (Dart)** — Material 3 responsive mobile interface for Android & iOS.
- **Cloud Backend & Persistence**: Cloud-hosted authentication, real-time database, and cloud storage for request photos (e.g., Firebase or Supabase).
- **Development Tools**: Android Studio, Git, and GitHub.

## 5. Semester Milestone Plan

| Week / Phase | Milestone | Key Deliverables |
|---|---|---|
| **Phase 1** | Specification & UI Wireframing | Proposal, requirements, data model, and screen flow design |
| **Phase 2** | App Scaffold & Auth | Flutter structure, theme, navigation shell, and cloud authentication |
| **Phase 3** | Service Requests (`Client`) | Home screen, category grid, Post Service Request form, and photo upload |
| **Phase 4** | Provider Feed & Bidding (`Provider`) | Provider profile setup, open requests feed, and bid submission |
| **Phase 5** | Bookings, Chat & Reviews | Accepting a bid, booking status screen, in-app chat, and star ratings |
| **Phase 6** | Testing & Final Lab Demo | Multi-device cloud sync testing and final presentation |

## 6. Team Division of Work

- **Member 1 (Lead & Architecture)**: Project setup, data models, cloud service layer, and booking state integration.
- **Member 2 (Client Module)**: Client home screen, Post Service Request form, photo picker, and bid comparison screen.
- **Member 3 (Provider Module)**: Provider onboarding screen, Open Requests feed with filters, and Submit Bid modal.
- **Member 4 (Shared Features)**: Authentication screens, in-app chat screen, booking detail view, and rating dialog.
