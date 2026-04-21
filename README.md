# Ashtavinayaka Realties CRM

> Enterprise-grade, AI-powered mobile CRM built ground-up for Indian real estate plot sales.

![Platform](https://img.shields.io/badge/Platform-Android-3DDC84?logo=android&logoColor=white)
![Language](https://img.shields.io/badge/Language-Kotlin-7F52FF?logo=kotlin&logoColor=white)
![UI](https://img.shields.io/badge/UI-Jetpack%20Compose-4285F4?logo=jetpackcompose&logoColor=white)
![Backend](https://img.shields.io/badge/Backend-Firebase-FFCA28?logo=firebase&logoColor=black)
![AI](https://img.shields.io/badge/AI-Vertex%20AI%20%2F%20Gemini-4285F4?logo=google&logoColor=white)
![Status](https://img.shields.io/badge/Status-Active%20Development-C9A84C)

---

## Overview

Ashtavinayaka Realties CRM is not a generic CRM adapted for real estate. It is engineered specifically for the **Indian real estate plot-selling lifecycle** — from interactive SVG-based plot inventory and a 13-step booking flow, to AI-powered payment verification using Gemini Vision and a 6-tier role hierarchy that mirrors how Indian builder sales teams actually operate.

**186 screens. 10 core modules. One codebase.**

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Kotlin (Native Android) |
| UI | Jetpack Compose + Material Design 3 |
| Architecture | MVVM + Repository pattern |
| Dependency Injection | Hilt (KSP) |
| Local Cache | Room Database |
| Database | Firebase Firestore (NoSQL, real-time) |
| Backend Logic | Firebase Cloud Functions (Node.js) |
| File Storage | Firebase Storage |
| Authentication | Firebase Auth |
| Push Notifications | Firebase Cloud Messaging (FCM) |
| AI — Complex tasks | Vertex AI — Gemini 2.5 Flash |
| AI — OCR & Verification | Vertex AI — Gemini Flash |
| AI — Chatbot pipeline | Firebase Genkit |
| Face Recognition | FaceNet512 (TFLite, on-device) |
| Charts | MPAndroidChart |
| Plot Rendering | Custom Canvas SVG engine |
| Firebase Region | asia-south1 (Mumbai) |

All AI calls are **server-side via Cloud Functions** — no API key exposure on the Android client.

---

## Role Hierarchy

The app enforces a strict 6-level hierarchy at both the UI and Firestore Security Rules level. Every Firestore document embeds `bodId`, `tlId`, `spId`, `seId` for single-query role-scoped reads.

```
Admin → BOD → Team Lead (TL) → Sales Partner (SP) → Sales Executive (SE) → Referral Partner (RP)
```

| Role | Responsibility |
|---|---|
| **Admin** | Full system control — user management, inventory, escalations, global reports |
| **BOD** | Team oversight, all payment approvals, registration approvals |
| **TL** | Team pipeline visibility, lead reassignment, booking tracking |
| **SP** | Lead & booking management — own leads + SEs under them |
| **SE** | Field sales — own assigned leads, site visits, follow-ups |
| **RP** | Referral submission and commission tracking only |

- BOD is the highest **payment authority** — Admin cannot submit payments
- No cross-BOD data visibility — each BOD's scope is completely isolated
- BOD accounts are created by Admin only — no self-registration

---

## Core Modules

### ✅ Module 1 — Authentication & User Management
- Email/password login with Firebase Auth
- Role-specific registration with BOD approval flow
- Biometric app lock (strict/lenient modes)
- Face embedding enrollment for field verification

### ✅ Module 2 — Lead Management
- Full lead CRUD with 7-stage pipeline (`New → Contacted → Visit Scheduled → Visit Done → Negotiation → Booked → Lost`)
- Priority tagging: Hot / Warm / Cold
- Scoped visibility enforced by role — SE sees only own leads; TL sees full team pipeline
- Follow-up scheduler with FCM-triggered reminders

### ✅ Module 3 — Site Visit Management
- Draft-first visit flow (saves offline, submits on connectivity)
- Geo-tag verification at submission
- On-device face recognition using FaceNet512 TFLite — selfie matched against enrolled embedding
- 90-day visit record lock (DPDP Act 2023 compliance)

### ✅ Module 4 — Inventory & SVG Plot System
- Interactive SVG-based plot map with runtime color injection by status
- Plot status: Available / On Hold / Blocked (verified) / Blocked (unverified) / Reserved / Sold
- 13-step guided booking flow
- 7-day auto-release hold system enforced via Cloud Scheduler

### ✅ Module 5 — AI Payment Verification
- Gemini Flash Vision via Cloud Functions — zero client-side API exposure
- Supports: Cash (face + amount verification), Cheque OCR (amount/date/payee/MICR), UPI (transaction ID extraction)
- Structured confidence score returned per field
- Escalation flow to BOD for low-confidence or disputed payments

### ✅ Module 6 — Role-Specific Dashboards
- Six distinct dashboard layouts — one per role
- Bento grid card system with MPAndroidChart graphs
- Live activity feed with real-time Firestore listeners
- Gold/black premium UI with skeleton shimmer loading (no `CircularProgressIndicator`)

### ✅ Module 7 — ASHAA AI Chatbot
- **A**shtavinayaka **S**mart **H**elper **A**I **A**ssistant
- Gemini 2.5 Flash via Vertex AI with Genkit function-calling pipeline
- Role-scoped tool access enforced in Cloud Function — not in prompts
- 30 messages/user/hour rate limiting with IST timezone context injection
- Floating bubble + contextual entry points + ModalBottomSheet UI pattern

### ✅ Module 9 — Notifications
- FCM with full hierarchy routing — notification flows up the chain on action triggers
- Mandatory (blocking) vs optional (dismissible) notification types
- Cloud Scheduler-triggered follow-up reminders and hold expiry alerts

### ✅ Module 10 — Reports & Analytics
- Role-scoped report access with drill-down system
- MPAndroidChart bar, line, pie, and donut graphs
- Bento grid layout for visual density without overdraw

### ✅ Module 11 — Call Logging
- Native Android dialer (`tel:` Intent) — no BSP dependency in Phase 1
- Post-call bottom sheet: outcome, duration, note logging
- Skipped calls logged as `outcome: "skipped"` for BOD accountability

### ✅ Localisation
- English and Hindi (`en` / `hi`) via Android string resources
- Full string extraction — no hardcoded UI text

---

## Design System

Gold and black — locked across all 186 screens.

| Token | Value | Usage |
|---|---|---|
| Background Primary | `#1C1C1E` | App background |
| Background Surface | `#2C2C2E` | Cards |
| Background Elevated | `#3A3A3C` | Bottom sheets, dialogs |
| Gold Primary | `#C9A84C` | CTAs, active states, headings |
| Gold Light | `#F5D483` | Highlights |
| Gold Dark | `#A67C2E` | Pressed states |
| Navy Primary | `#1B3A6B` | Buttons, icons |
| Text Primary | `#FFFFFF` | — |
| Text Secondary | `#8E8E93` | — |

**Font:** Inter throughout. No other typeface in the project.

**Loading pattern:** Skeleton shimmer on every data-loading state. `CircularProgressIndicator` is banned.

---

## Architecture

```
┌─────────────────────────────────────┐
│           Jetpack Compose UI         │
│    (186 screens, 62–72 layouts)      │
└────────────────┬────────────────────┘
                 │ collectAsState()
┌────────────────▼────────────────────┐
│         ViewModels (Hilt)            │
│   StateFlow / SharedFlow            │
└────────────────┬────────────────────┘
                 │
┌────────────────▼────────────────────┐
│         Repository Layer             │
│  (Firestore + Room stale-while-     │
│   revalidate pattern)               │
└────┬───────────────────┬────────────┘
     │                   │
┌────▼─────┐      ┌──────▼──────┐
│  Room DB  │      │  Firestore  │
│ (cache)   │      │ (primary)   │
└───────────┘      └──────┬──────┘
                          │
               ┌──────────▼──────────┐
               │  Cloud Functions    │
               │  (Node.js,          │
               │  asia-south1)       │
               │  ┌────────────────┐ │
               │  │  Vertex AI     │ │
               │  │  Gemini Flash  │ │
               │  └────────────────┘ │
               └─────────────────────┘
```

**Key architecture rules:**
- ViewModels never touch Firestore directly
- All AI calls are server-side — no Vertex AI SDK on the Android client
- Room DB reduces Firestore reads by 60–70% (cache-only, Firestore offline persistence disabled)
- Real-time Firestore listeners detached in `onCleared()` — prevents read accumulation on navigation
- `bodId`, `tlId`, `spId`, `seId` embedded in every Firestore document written — enables single-query role-scoped reads without server-side joins

---

## SVG Plot Map

The plot inventory system uses a **custom Canvas-based SVG rendering engine**. Each plot element in the SVG file carries an `id="plot-NNN"` attribute. At runtime, the engine:

1. Reads Firestore plot status for the project
2. Injects the appropriate status color per plot element
3. Renders an interactive, tap-to-select plot map

Standard CAD-to-SVG converters (Acme, etc.) produce anonymous `<path>` elements with no IDs. All SVG assets are prepared with layer isolation in CAD software or via `ezdxf` Python scripting on the source DXF to produce discrete, named polygons.

---

## Security & Compliance

- **Firestore Security Rules** enforce the full role hierarchy at the database level — UI-level hiding is not the security boundary
- **DPDP Act 2023** compliance: biometric consent at enrollment, 90-day visit record lock, WhatsApp DND list handling, unsubscribe in emails
- **Face recognition** runs on-device (FaceNet512 TFLite) — biometric embeddings are never sent to a third-party API
- **No API keys on the Android client** — all Vertex AI and Cloud Vision calls are proxied through Cloud Functions with Google Cloud IAM service authentication

---

## Cost Architecture

Optimized for Indian real estate SME scale:

| Scenario | Monthly Cost (INR) |
|---|---|
| Optimized (200–300 DAU) | ~₹13,500 |
| Optimized (with full module set) | ~₹20,500–₹27,500 |
| Unoptimized baseline | ~₹52,000–₹65,000 |

**Optimization levers:**
- Gemini Flash for OCR/verification (8–10× cheaper than Pro)
- Room DB cache — 60–70% Firestore read reduction
- Real-time listener detach on navigation
- Firebase Storage URLs passed directly to Vertex AI (no egress)
- Cloud Functions `minInstances=1` on critical paths (cold start elimination)
- asia-south1 region for India egress cost reduction

---

## Live Projects

| Project | Plots | Status |
|---|---|---|
| Gulmohar Greens | 158 plots | Active — SVG map live |
| Green Golfs | — | Active |

---

## Repository Structure

```
app/
├── src/main/java/com/ashtavinayaka/crm/
│   ├── data/               # Firestore repositories, Room DAOs, data models
│   ├── di/                 # Hilt modules (AppModule, DatabaseModule)
│   ├── domain/             # Domain models, enums (UserRole, PlotStatus, etc.)
│   ├── ui/
│   │   ├── auth/           # Login, registration, approval flow
│   │   ├── dashboard/      # 6 role-specific dashboard screens
│   │   ├── leads/          # Lead list, detail, follow-up sheets
│   │   ├── inventory/      # SVG map, plot detail, booking flow
│   │   ├── payments/       # Payment submission, AI verification
│   │   ├── visits/         # Site visit draft, geo-tag, face capture
│   │   ├── chatbot/        # ASHAA floating bubble + bottom sheet
│   │   ├── notifications/  # Notification center, badge
│   │   ├── reports/        # Analytics screens per role
│   │   └── common/         # Shared composables, design system tokens
│   └── workers/            # WorkManager background tasks
├── src/main/res/
│   ├── raw/                # SVG layout files
│   └── values/             # strings.xml (EN + HI)
functions/                  # Firebase Cloud Functions (Node.js)
│   ├── src/
│   │   ├── ai/             # Gemini payment verification, ASHAA tools
│   │   ├── notifications/  # FCM dispatch, hierarchy routing
│   │   └── pdf/            # Cost sheet + report generation
```

---

## Phase 2 Roadmap

| Feature | Area |
|---|---|
| Exotel IVR + call recording | Telephony |
| WhatsApp BSP integration (AiSensy/Interakt) | Marketing |
| AI lead scoring (Gemini) | Leads |
| Bulk lead import (CSV) | Leads |
| GPS check-in verification | Site Visits |
| Bank statement auto-reconciliation | Payments |
| GST invoice generation | Payments |
| Demand heatmap overlay on SVG | Inventory |
| Plot comparison tool | Inventory |
| Firebase Vector Search (semantic) | Search |
| Hindi/Marathi chatbot support | ASHAA |
| iOS port via Kotlin Multiplatform | Platform |

---

## License

Private repository. All rights reserved — Ashtavinayaka Realties Pvt. Ltd.

Not open source. This README is for showcase and documentation purposes only.
