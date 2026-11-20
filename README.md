# Ashtavinayaka ONE

> An AI-powered native Android sales app built for real estate teams: leads, site visits, plot booking, payments and a live satellite plot map in one place.

![Platform](https://img.shields.io/badge/Platform-Android-3DDC84?logo=android&logoColor=white)
![Language](https://img.shields.io/badge/Language-Kotlin-7F52FF?logo=kotlin&logoColor=white)
![UI](https://img.shields.io/badge/UI-Jetpack%20Compose-4285F4?logo=jetpackcompose&logoColor=white)
![Backend](https://img.shields.io/badge/Backend-Firebase-FFCA28?logo=firebase&logoColor=black)
![AI](https://img.shields.io/badge/AI-Vertex%20AI%20%2F%20Gemini-4285F4?logo=google&logoColor=white)
![Map](https://img.shields.io/badge/Map-MapLibre%20GL-396CB2)

<p align="center">
  <img src="assets/screenshots/02-splash-screen.jpg" width="220" alt="Ashtavinayaka ONE launch screen" />
  &nbsp;
  <img src="assets/screenshots/09-map-satellite.jpg" width="220" alt="Satellite plot map" />
  &nbsp;
  <img src="assets/screenshots/03-dashboard-bod.jpg" width="220" alt="BOD dashboard" />
</p>

---

## What It Is

Ashtavinayaka ONE is a purpose-built mobile app for real estate developers and their sales teams. It covers the full plot-selling lifecycle: browsing live plot inventory on a satellite map, tracking leads, logging site visits with face verification, booking plots, and verifying payments with AI assistance, all in a single native Android app.

> Formerly released as *Ashtavinayaka Realties CRM*. The app was rebranded to **Ashtavinayaka ONE** (new icon, launch screen, theme and fonts) under the same package, so existing users received it as a normal update.

---

## Screenshots

### Brand & role dashboards

Each role lands on its own home screen with live stats, quick actions and an always-available ASHAA assistant button.

<table>
  <tr>
    <td align="center"><img src="assets/screenshots/03-dashboard-bod.jpg" width="200" /><br/><sub>BOD: team overview &amp; overdue-lead nudges</sub></td>
    <td align="center"><img src="assets/screenshots/04-dashboard-admin.jpg" width="200" /><br/><sub>Admin: system alerts &amp; plot holds</sub></td>
    <td align="center"><img src="assets/screenshots/05-dashboard-sales-executive.jpg" width="200" /><br/><sub>Sales Executive: leads &amp; tasks</sub></td>
    <td align="center"><img src="assets/screenshots/06-side-menu.jpg" width="200" /><br/><sub>Side menu</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="assets/screenshots/07-role-features.jpg" width="200" /><br/><sub>Role-specific features page</sub></td>
    <td align="center"><img src="assets/screenshots/08-leads-pipeline.jpg" width="200" /><br/><sub>Lead pipeline</sub></td>
    <td align="center"><img src="assets/screenshots/23-settings-fonts.jpg" width="200" /><br/><sub>Settings: theme &amp; font styles</sub></td>
    <td align="center"><img src="assets/screenshots/02-splash-screen.jpg" width="200" /><br/><sub>Launch screen</sub></td>
  </tr>
</table>

### Live satellite plot map

<table>
  <tr>
    <td align="center"><img src="assets/screenshots/09-map-satellite.jpg" width="200" /><br/><sub>Satellite view</sub></td>
    <td align="center"><img src="assets/screenshots/10-map-3d.jpg" width="200" /><br/><sub>3D view (illustrative)</sub></td>
    <td align="center"><img src="assets/screenshots/11-map-plot-numbers.jpg" width="200" /><br/><sub>Plot numbers &amp; live status counts</sub></td>
    <td align="center"><img src="assets/screenshots/12-nearby-places.jpg" width="200" /><br/><sub>Nearby places layer</sub></td>
  </tr>
  <tr>
    <td align="center"><img src="assets/screenshots/13-plot-booked.jpg" width="200" /><br/><sub>Plot sheet: Booked</sub></td>
    <td align="center"><img src="assets/screenshots/14-plot-mortgage.jpg" width="200" /><br/><sub>Plot sheet: Mortgage</sub></td>
    <td align="center"><img src="assets/screenshots/15-plot-status-map.jpg" width="200" /><br/><sub>Status colours on the map</sub></td>
    <td align="center"><img src="assets/screenshots/16-new-project-shivalaya.jpg" width="200" /><br/><sub>Light theme, newly added project</sub></td>
  </tr>
</table>

### Booking & payments

<table>
  <tr>
    <td align="center"><img src="assets/screenshots/17-booking-phone-country.jpg" width="200" /><br/><sub>Booking: country-code phone field</sub></td>
    <td align="center"><img src="assets/screenshots/18-booking-validation.jpg" width="200" /><br/><sub>Minimum booking amount check</sub></td>
    <td align="center"><img src="assets/screenshots/19-transactions.jpg" width="200" /><br/><sub>Transactions &amp; review queue</sub></td>
  </tr>
</table>

### Site visits

<table>
  <tr>
    <td align="center"><img src="assets/screenshots/20-site-visits.jpg" width="200" /><br/><sub>Visits &amp; drafts</sub></td>
    <td align="center"><img src="assets/screenshots/21-site-visit-form.jpg" width="200" /><br/><sub>Draft-first visit form</sub></td>
    <td align="center"><img src="assets/screenshots/22-identity-verified.jpg" width="200" /><br/><sub>On-device identity check</sub></td>
  </tr>
</table>

### Brand identity

<p align="center"><img src="assets/screenshots/01-brand-identity.jpg" width="420" alt="Ashtavinayaka ONE brand sheet" /></p>

> Screenshots are from test builds with test data. Personal details (faces, names, emails) have been blurred or removed.

---

## Key Features

**Interactive Satellite Plot Map**
A MapLibre GL map running in a WebView with 2D, satellite and 3D views, GPS location and a nearby-places layer. Plots are coloured by live status, and tapping a plot opens its details and the booking flow through a Kotlin-to-JS bridge.

**Five-State Plot Status**
Available, Reserved, Booked, Sold and Mortgage, one status per plot shared by the map, booking flow and dashboards. Admin tools allow marking plots as Sold or Mortgage, including multi-select.

**Booking & Payment Verification**
Cash, cheque, UPI and part payments follow one flow into an Admin review queue. A minimum booking amount is validated before anything is written or sent to AI. Gemini Vision reads payment proofs and escalates edge cases to a human.

**Role-Based Access Control**
Six roles (Admin, BOD, Team Lead, Sales Partner, Sales Executive and Referral Partner), each with a scoped dashboard, data visibility and feature set. Enforced in the backend, not only hidden in the UI.

**ASHAA: AI Sales Assistant**
An in-app conversational assistant (Ashtavinayaka Smart Helper AI Assistant) powered by Gemini via Cloud Functions, reachable from every home screen and scoped to the signed-in user's role.

**Site Visits with Face Verification**
Draft-first visit flow with geo-tagged photos, a blink check and on-device face matching to identify the salesperson and client. Visits save completely or not at all, and faces are never sent off the device for matching.

**Lead Pipeline & Follow-ups**
Lead lifecycle from first contact to booking, with status tracking, overdue indicators, nudges for managers and reminders for follow-ups.

**Push Notifications & Call Logging**
Role-aware FCM notifications, plus native dialer integration with structured post-call outcome logging.

---

## Tech Stack

**Android**
- Kotlin · Jetpack Compose · Material Design 3
- MVVM + Repository pattern · Hilt · Room · DataStore
- MapLibre GL JS in a WebView

**Backend**
- Firebase Auth · Firestore · Storage · Cloud Messaging
- Cloud Functions (Node.js) for privileged operations and AI calls

**AI & ML**
- Gemini via Vertex AI: payment proof OCR and the ASHAA assistant
- ML Kit + FaceNet (LiteRT): on-device face detection and matching

---

## Multilingual Support

| Language | Code |
|---|---|
| English | `en` |
| Hindi | `hi` |

All UI strings are resource-managed. Language follows system preference.

---

## Theme & Design

The app ships with a premium **gold-on-charcoal dark theme** reflecting the luxury real estate segment, with a light variant for accessibility and preference.

| Element | Detail |
|---|---|
| Primary background | Deep charcoal `#1C1C1E` |
| Accent | Gold |
| Font styles | Modern (Plus Jakarta Sans / Baloo 2), Elegant (Cormorant Garamond / Tiro Devanagari) or System; saved across restarts |
| Icon | Adaptive launcher icon, so the logo holds up on every launcher shape |

---

## Platform

**Phase 1:** Native Android (this showcase)
**Phase 2:** iOS, planned via Kotlin Multiplatform with a SwiftUI UI layer

---

## License

Private client project. All rights reserved.
This repository is for portfolio showcase purposes only. Source code is not distributed.
