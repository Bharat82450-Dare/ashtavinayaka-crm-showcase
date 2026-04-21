# Ashtavinayaka Realties CRM

> A production Android CRM platform for real estate lead management — built with Kotlin, Jetpack Compose, Firebase, and Vertex AI.

---

## Overview

Ashtavinayaka Realties CRM is a live client project developed for **Radhaswami Developers / Ashtavinayaka Realties**, Raipur, India. It is a full-featured Android application managing **6,000–7,000 real estate leads** across a structured four-tier role hierarchy, with AI-powered lead scoring, biometric client identification, and automated payment verification.

> This repository serves as a public showcase. Source code is proprietary and kept private per client agreement.

---

## Screenshots

### Dashboard & Lead Management
<!-- Add screenshot here -->
> `[Dashboard Screenshot]`

### Role Hierarchy & Access Control
<!-- Add screenshot here -->
> `[Role Management Screenshot]`

### AI Lead Scoring (Vertex AI)
<!-- Add screenshot here -->
> `[Lead Scoring Screenshot]`

### Face Recognition — Biometric Client ID
<!-- Add screenshot here -->
> `[Face Recognition Screenshot]`

### Payment Receipt OCR Verification
<!-- Add screenshot here -->
> `[OCR Payment Verification Screenshot]`

### Agent View — Lead Pipeline
<!-- Add screenshot here -->
> `[Agent Pipeline Screenshot]`

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Language | Kotlin |
| UI | Jetpack Compose + Material 3 |
| Architecture | MVVM + Repository Pattern |
| Backend | Firebase Firestore, Firebase Auth, Firebase Storage, FCM |
| AI / ML | Vertex AI (lead scoring), MediaPipe (face embeddings), Cloud Vision OCR |
| Automation | WhatsApp Cloud API integration |
| IDE | Google Antigravity IDE (VS Code-based, agent-first) |
| Build | Gradle (Kotlin DSL) |

---

## Key Features

### Role-Based Access Control
Four-tier hierarchy with scoped permissions:
- **Admin** — full system access, user management, analytics
- **Manager** — team oversight, lead assignment, report generation
- **Agent** — lead pipeline, client interactions, follow-up tracking
- **Viewer** — read-only dashboard access

### AI-Powered Lead Scoring
Integrated **Vertex AI** to score and prioritize incoming leads based on engagement signals, property interest, and behavioral data — reducing manual triage effort for the sales team.

### Biometric Client Identification
On-device **MediaPipe face embeddings** for client recognition during site visits — enabling agents to instantly pull up a returning client's profile without manual search.

### Cloud Vision OCR — Payment Verification
Automated **Cloud Vision OCR pipeline** that reads and validates payment receipts uploaded by clients — eliminating manual review for the finance workflow and reducing verification time significantly.

### WhatsApp Automation
Integrated **WhatsApp Cloud API** for bulk and targeted messaging to leads — enabling campaign-level outreach directly from the CRM dashboard.

### Firestore Data Architecture
Carefully modelled Firestore schema featuring:
- `Long` type for all monetary values (stored in paise to avoid floating point errors)
- Sealed classes for all status fields (lead status, payment status, role type)
- Firestore transactions for all counter fields (lead counts, agent assignments)
- Denormalized collections for read-heavy agent dashboard queries

---

## Architecture

```
app/
├── data/
│   ├── model/          # Data classes, sealed status classes
│   ├── repository/     # Repository implementations
│   └── remote/         # Firestore, Firebase Auth, Storage sources
├── domain/
│   └── usecase/        # Business logic layer
├── presentation/
│   ├── viewmodel/      # ViewModels (Hilt-injected)
│   └── ui/
│       ├── dashboard/
│       ├── leads/
│       ├── clients/
│       ├── payments/
│       └── admin/
├── ai/
│   ├── vertexai/       # Lead scoring integration
│   ├── mediapipe/      # Face embedding pipeline
│   └── ocr/            # Cloud Vision OCR pipeline
└── util/
    └── whatsapp/       # WhatsApp Cloud API integration
```

---

## Development Context

| Detail | Info |
|--------|------|
| Team Size | 2 developers |
| My Role | Co-developer — Android application layer, Firebase backend, all AI feature integration |
| Client | Radhaswami Developers / Ashtavinayaka Realties, Raipur, India |
| Duration | Jan 2025 – Apr 2026 |
| Status | Live client deployment |
| Leads Managed | ~6,000 – 7,000 |

---

## Technical Specification

A detailed 14-section technical specification document was co-authored covering:

- System architecture and role hierarchy design
- Firestore data model (collections, subcollections, indexing strategy)
- MVVM + Repository implementation guide
- AI module integration (Vertex AI, MediaPipe, Cloud Vision)
- RAG-based WhatsApp agent design
- Security rules and role-scoped Firestore access
- Phased development roadmap

---

## Developer

**Bharat N. Sarkar (Aman)**
Pre-final year B.Tech Computer Engineering — MIT Academy of Engineering, Pune

- GitHub: [github.com/Bharat82450-Dare](https://github.com/Bharat82450-Dare)
- LinkedIn: [linkedin.com/in/bharat-sarkar82450](https://linkedin.com/in/bharat-sarkar82450)

---

> *Source code is private. For technical discussion or collaboration inquiries, reach out via LinkedIn.*
