# Ashtavinayaka Realties CRM

> An enterprise-grade, AI-powered mobile CRM built exclusively for real estate sales teams.

![Platform](https://img.shields.io/badge/Platform-Android-3DDC84?logo=android&logoColor=white)
![Language](https://img.shields.io/badge/Language-Kotlin-7F52FF?logo=kotlin&logoColor=white)
![UI](https://img.shields.io/badge/UI-Jetpack%20Compose-4285F4?logo=jetpackcompose&logoColor=white)
![Backend](https://img.shields.io/badge/Backend-Firebase-FFCA28?logo=firebase&logoColor=black)
![AI](https://img.shields.io/badge/AI-Vertex%20AI%20%2F%20Gemini-4285F4?logo=google&logoColor=white)

---

## What It Is

Ashtavinayaka Realties CRM is a purpose-built mobile application for real estate developers and their sales teams. It covers the full plot-selling lifecycle — from interactive inventory browsing and lead tracking, to AI-assisted payment verification and real-time team dashboards — all within a single native Android app.

---

## Tech Stack

**Android**
- Kotlin · Jetpack Compose · Material Design 3
- MVVM + Repository pattern · Hilt (KSP) · Room Database

**Firebase**
- Firestore · Firebase Auth · Firebase Storage
- Cloud Functions (Node.js) · FCM · Cloud Scheduler

**AI & ML**
- Vertex AI — Gemini (payment OCR, chatbot, lead intelligence)
- Firebase Genkit (AI pipeline orchestration)
- FaceNet512 TFLite — on-device face recognition

**Other**
- MPAndroidChart · WorkManager · Custom Canvas SVG rendering engine

---

## Key Features

**Interactive Plot Inventory**
SVG-based plot map with real-time status colours. Tap any plot to view details, check availability, or initiate a booking — all driven by live data.

**AI Payment Verification**
Cash, cheque, and UPI payment proofs are verified using Gemini Vision via Cloud Functions. Structured confidence scores are returned per field with an escalation path for edge cases.

**Role-Based Access Control**
Six user roles — Admin, BOD, Team Lead, Sales Partner, Sales Executive, and Referral Partner — each with their own scoped data visibility, dashboard, and feature set. Access is enforced at the database level, not just in the UI.

**ASHAA — AI Sales Assistant**
An in-app conversational AI chatbot (Ashtavinayaka Smart Helper AI Assistant) powered by Gemini. Responds to natural language queries about leads, bookings, inventory, and team performance — scoped to the logged-in user's role and permissions.

**Face Recognition**
On-device face recognition using a TFLite FaceNet512 model for identity verification during field activities. Biometric data never leaves the device.

**Role-Specific Dashboards**
Six distinct dashboards — one per role — with live activity feeds, graph-based analytics, and a bento grid card layout.

**Lead Pipeline Management**
Full lead lifecycle from first contact to booking, with priority tagging, follow-up scheduling, and push notification reminders.

**Site Visit Logging**
Draft-first visit flow with geo-tag verification and face recognition confirmation on submission.

**Push Notifications**
FCM-based notification system with hierarchy-aware routing and Cloud Scheduler-triggered reminders.

**Call Logging**
Native dialer integration with structured post-call outcome logging for full team accountability.

---

## Multilingual Support

| Language | Code |
|---|---|
| English | `en` |
| Hindi | `hi` |

Fully localised UI — all strings are resource-managed with no hardcoded text. Language follows system preference.

---

## Theme & Design

The app ships with a **premium dark theme** built around a gold and charcoal palette — designed to reflect the luxury real estate segment the client operates in.

| Element | Detail |
|---|---|
| Primary background | Deep charcoal `#1C1C1E` |
| Accent | Gold `#C9A84C` |
| Typography | Inter |
| Loading states | Skeleton shimmer throughout |
| Charts | MPAndroidChart with custom gold styling |

A **light theme** variant is included for accessibility and user preference.

---

## Platform

**Phase 1:** Native Android (this repository)  
**Phase 2:** iOS — planned via Kotlin Multiplatform with a SwiftUI UI layer

---

## License

Private client project. All rights reserved.  
This repository is for portfolio showcase purposes only — source code is not distributed.
