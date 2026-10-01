# Passia Mobile

> **Cross-platform Flutter architecture case study focused on mobile engineering, scalable architecture, security, geolocation, automated testing and high-quality user experience.**

**Passia** is a portfolio project for pet walking and safe pet transportation.

The mobile application was designed as more than a collection of screens: it is an engineering and product architecture case study demonstrating how **Mobile Architecture, Product Design, UX, security, location services, API integration and software quality** can be combined into a maintainable cross-platform application.

Built with **Flutter and Dart**, the architecture targets:

- Android;
- iOS;
- Web.

from a shared product and engineering foundation.

🌐 **Project website:** https://www.passia.com.br

---

> **Project status:** Development is currently paused due to a temporary health-related leave by its creator.
>
> This repository is preserved as a **mobile architecture, engineering and Product Design portfolio case study**.
>
> The complete application and its external development services should not currently be considered operational.
>
> **Last active development checkpoint:** October 2026.

---

# Product Preview

## Application

> **Screenshot placeholder — Main application experience**
>
> Replace this block with a composition containing 3–5 mobile screens.
>
> Suggested file:
>
> `docs/images/passia-app-overview.png`

<!--
![Passia App](docs/images/passia-app-overview.png)
-->

---

## Product Design

The application experience was designed before implementation through a structured Product Design process, including:

- user flow definition;
- information architecture;
- visual identity;
- color system;
- interaction patterns;
- reusable UI concepts;
- navigation flows;
- prototyping;
- mobile usability decisions;
- architecture feasibility analysis before implementation.

> **Image placeholder — Figma / Product Design**
>
> Suggested composition:
>
> `docs/images/passia-figma-product-design.png`

<!--
![Passia Product Design](docs/images/passia-figma-product-design.png)
-->

### Figma Project

```text
[FIGMA PROJECT LINK]
```

---

## Website

The product also includes a dedicated landing page and digital identity.

🌐 **https://www.passia.com.br**

> **Image placeholder — Passia Website**
>
> Suggested file:
>
> `docs/images/passia-website.png`

<!--
![Passia Website](docs/images/passia-website.png)
-->

---

# Executive Summary

Passia Mobile is built with **Flutter** to provide a shared architecture across Android, iOS and Web while preserving platform-specific capabilities when required.

The mobile architecture prioritizes:

- separation of concerns;
- feature-oriented organization;
- testability;
- predictable state management;
- secure authentication;
- reusable components;
- high UX consistency;
- responsive and fluid interfaces;
- fast perceived performance;
- location-aware experiences;
- controlled API integration;
- platform abstraction;
- evolutionary architecture.

Core technologies and concepts include:

```text
Flutter
Dart

Android
iOS
Web

Clean Architecture
Feature-oriented architecture
SOLID
Repository Pattern

BLoC / Cubit
Dependency abstraction

REST APIs
Dio

OAuth 2.0
OpenID Connect
Authorization Code + PKCE
JWT
Auth0

Geolocation
Maps
Places / Address Autocomplete
Reverse Geocoding

TDD
Unit Tests
Widget Tests
Integration Tests

Design System
Responsive UI
Reusable Components

Push Notification Architecture

CI/CD-ready architecture
Environment configuration
```

---

# Why Flutter?

Flutter was selected as a deliberate product and engineering decision.

The goal was not simply to reduce the amount of source code.

The main objective was to maintain a **shared product experience and architectural foundation across platforms** while retaining access to native capabilities.

```text
                   Shared Flutter Architecture
                              │
              ┌───────────────┼───────────────┐
              │               │               │
              ▼               ▼               ▼
          Android             iOS             Web
```

The approach provides:

- shared business logic;
- shared UI architecture;
- consistent Design System;
- common networking layer;
- reusable state management;
- shared automated tests;
- faster product iteration;
- lower feature divergence between platforms;
- centralized architectural governance.

Platform-specific integration can still be introduced through native APIs or platform channels when required.

---

# Multiplatform Strategy

Passia was architected with three delivery targets:

| Platform | Strategy |
|---|---|
| Android | Flutter application with Android platform integration |
| iOS | Flutter application with iOS platform integration |
| Web | Flutter Web from the shared product architecture |

The goal is **shared architecture, not platform blindness**.

Android and iOS continue to have different:

```text
permission models
application lifecycle
background execution constraints
notification behavior
secure storage
location behavior
release processes
store requirements
```

Those differences should remain isolated from the core application architecture whenever possible.

---

# Mobile Architecture

The application uses clear boundaries between presentation, application/data orchestration and infrastructure concerns.

Conceptually:

```text
┌─────────────────────────────────────┐
│                 UI                  │
│        Screens / Widgets            │
└─────────────────┬───────────────────┘
                  │
                  ▼
┌─────────────────────────────────────┐
│          State Management           │
│             Cubit / BLoC            │
└─────────────────┬───────────────────┘
                  │
                  ▼
┌─────────────────────────────────────┐
│             Repository              │
│        Application boundary         │
└─────────────────┬───────────────────┘
                  │
                  ▼
┌─────────────────────────────────────┐
│            Data Sources             │
│      REST / Device / Providers      │
└─────────────────┬───────────────────┘
                  │
          ┌───────┴────────┐
          ▼                ▼
     Passia API       Device APIs
```

---

# Architecture Diagram

> **Diagram placeholder — Mobile Architecture**
>
> Suggested file:
>
> `docs/images/01-mobile-architecture.png`

<!--
![Mobile Architecture](docs/images/01-mobile-architecture.png)
-->

---

# Architecture Principles

The application follows principles commonly associated with **Clean Architecture and SOLID**, adapted pragmatically to Flutter.

The purpose is not to reproduce theoretical layers mechanically.

The purpose is to ensure that:

```text
UI does not own business rules

Widgets do not perform infrastructure orchestration

HTTP implementation does not leak into presentation

External providers do not become domain models

Authentication details remain behind boundaries

Features can be tested independently

Platform-specific code remains isolated
```

---

# Feature-Oriented Architecture

The architecture favors organization around **product capabilities** rather than creating one global folder for every technical type.

A representative organization is:

```text
lib/
│
├── core/
│   ├── auth/
│   ├── config/
│   ├── network/
│   ├── routing/
│   ├── theme/
│   ├── errors/
│   └── widgets/
│
├── features/
│   │
│   ├── authentication/
│   │
│   ├── tutor/
│   │
│   ├── pets/
│   │
│   ├── walk/
│   │
│   ├── route/
│   │
│   ├── location/
│   │
│   ├── tracking/
│   │
│   └── notifications/
│
└── main.dart
```

Each feature can evolve with its own:

```text
presentation
state
repository
data sources
models
tests
```

without creating unnecessary coupling with unrelated areas.

---

# State Management

Passia uses **Cubit/BLoC-style state management**.

The objective is to make UI states explicit and predictable.

Example:

```text
Initial
   │
   ▼
Loading
   │
   ├───────────► Success
   │
   ├───────────► Empty
   │
   └───────────► Error
```

This avoids placing asynchronous orchestration directly inside widgets.

The UI reacts to state rather than controlling infrastructure.

---

# API Integration

Network communication is centralized around a reusable API client.

The current architecture uses:

```text
Dio
REST
JSON
Interceptors
Environment configuration
Timeouts
Error handling
Bearer authentication
```

Conceptually:

```text
UI
 │
 ▼
Cubit
 │
 ▼
Repository
 │
 ▼
Remote Data Source
 │
 ▼
ApiClient / Dio
 │
 ▼
Passia Backend
```

This makes networking independently testable and prevents HTTP concerns from spreading through presentation code.

---

# Environment Strategy

The API base URL is externally configurable.

Conceptually:

```text
local
development
production
```

through environment configuration instead of hard-coded infrastructure URLs.

Example:

```text
API_BASE_URL=<environment-api-url>
```

Secrets and environment-specific credentials must never be committed to the application repository.

---

# Authentication Architecture

Passia uses **Auth0 with OAuth 2.0 / OpenID Connect**.

Because a mobile application is a public client, no OAuth Client Secret is embedded in the app.

Authentication uses:

```text
Authorization Code
+
PKCE S256
```

with:

```text
openid
profile
email
offline_access
```

---

## Authentication Flow

```text
User
 │
 ▼
Passia Mobile
 │
 │ Authorization Code + PKCE
 ▼
Auth0 Universal Login
 │
 │ Authorization Code
 ▼
Passia Mobile
 │
 │ Token exchange
 ▼
Access / Refresh Credentials
 │
 ▼
Credentials Manager
 │
 ▼
Authenticated API requests
```

> **Diagram placeholder — Authentication Sequence**
>
> Suggested file:
>
> `docs/images/02-authentication-flow.png`

<!--
![Authentication Flow](docs/images/02-authentication-flow.png)
-->

---

# Secure Session Management

The application uses the authentication SDK's credential management capabilities rather than implementing a custom token store.

The architecture avoids:

```text
tokens in plain preferences
credentials committed to source
token logging
manual OAuth implementation
embedded Client Secrets
```

Bearer tokens are resolved dynamically for authenticated API requests.

---

# Security Boundary

The mobile application is **not treated as a trusted authority**.

It cannot decide:

```text
which Tutor owns a Pet
which resources a user may access
whether a Walk transition is authorized
whether an authenticated identity represents a domain actor
```

Those rules belong to the backend.

This is an important architectural distinction:

```text
Mobile
   ↓
provides authenticated credentials

Backend
   ↓
validates identity

Backend
   ↓
enforces domain authorization
```

---

# Geolocation Architecture

Location is one of the core technical capabilities of Passia.

The architecture considers:

- operating-system permission handling;
- current device position;
- reverse geocoding;
- editable origin;
- destination search;
- address autocomplete;
- intermediate stops;
- map visualization;
- route representation;
- future background tracking;
- offline behavior;
- location privacy.

---

## Location UX

One product decision was to avoid exposing raw latitude/longitude coordinates to users whenever a human-readable address is available.

For example:

```text
Device GPS
    │
    ▼
Latitude / Longitude
    │
    ▼
Reverse Geocoding
    │
    ▼
Human-readable Address
```

This allows actions such as **Use current location** to behave like navigation applications instead of exposing implementation details.

---

# Route Experience

The route planning interface is designed around a familiar mental model:

```text
Origin
   │
   ├── Stop
   │
   ├── Stop
   │
   └── ...
   │
Destination
```

The architecture supports use cases such as:

```text
Home
  ↓
Pet Shop
  ↓
Park
  ↓
Home
```

without forcing origin and destination to be different.

---

## Map / Route Screenshot

> **Screenshot placeholder — Walk route planner**
>
> Suggested file:
>
> `docs/images/03-route-planner.png`

<!--
![Route Planner](docs/images/03-route-planner.png)
-->

---

# Location Permissions

The application follows an explicit permission flow rather than requesting location access without user context.

Conceptually:

```text
User selects
"Use current location"
        │
        ▼
Check permission
        │
     ┌──┴──┐
     │     │
 granted  missing
     │     │
     │     ▼
     │   Request OS permission
     │
     ▼
Read position
     │
     ▼
Reverse geocode
     │
     ▼
Display address
```

Platform-specific permission behavior remains an infrastructure concern.

---

# Offline-First Tracking Direction

Walking and pet transportation cannot assume permanent internet connectivity.

For that reason, tracking architecture is designed around the principle:

> **GPS availability and network availability are independent concerns.**

The intended flow is:

```text
GPS
 │
 ▼
Mobile tracking session
 │
 ▼
Local buffer
 │
 ├── network unavailable ──► retain points
 │
 └── network available
          │
          ▼
       Batch sync
          │
          ▼
      Passia Backend
```

Future tracking batches can support:

```text
sequence numbers
batch identifiers
retry
deduplication
late delivery
out-of-order arrival
acknowledgement
```

This prevents temporary connectivity loss from automatically meaning route data loss.

---

# Push Notification Architecture

Push notifications are part of the planned mobile integration architecture.

Typical future events include:

```text
walk scheduled
walk starting
walk started
route update
walk completed
important operational notification
```

The application architecture keeps push provider integration behind a boundary rather than coupling feature code directly to Firebase Cloud Messaging or another provider.

Conceptually:

```text
Passia Backend
      │
      ▼
Push Provider
      │
      ▼
Android / iOS
      │
      ▼
Notification Adapter
      │
      ▼
Feature / Navigation
```

This provides room for:

- notification permissions;
- token registration;
- token rotation;
- deep links;
- navigation from notifications;
- foreground handling;
- background handling;
- provider replacement.

> **Current status:** notification architecture is prepared as an evolution point; complete production push delivery is not claimed as implemented in this portfolio checkpoint.

---

# User Experience Engineering

UX quality is treated as an engineering concern, not only a visual design concern.

Passia prioritizes:

```text
fast interaction feedback
clear loading states
predictable navigation
minimal unnecessary input
touch-friendly controls
reusable UI components
consistent spacing
visual hierarchy
responsive layouts
familiar navigation patterns
human-readable error states
```

---

# Fluid Interfaces

The interface is designed to feel lightweight and responsive.

Engineering considerations include:

- avoiding unnecessary widget rebuilds;
- keeping state scoped to the appropriate feature;
- asynchronous work outside rendering paths;
- reusable visual components;
- controlled network loading states;
- predictable transitions;
- progressive feedback;
- avoiding blocking interactions;
- lightweight screen composition.

The objective is not simply benchmark performance.

It is **perceived performance**:

> users should always understand whether the application is responding to their action.

---

# Design System

The application maintains reusable visual primitives instead of duplicating styling across screens.

Examples include:

```text
colors
typography
spacing
buttons
form fields
cards
navigation elements
states
feedback components
```

Reusable components such as the application's custom form fields help keep interaction behavior and visual design consistent.

---

## UI Components

> **Image placeholder — Design System / Components**
>
> Suggested file:
>
> `docs/images/04-design-system.png`

<!--
![Passia Design System](docs/images/04-design-system.png)
-->

---

# Product Design → Engineering

An important part of the project is the connection between Product Design and implementation.

```text
Product Requirement
        │
        ▼
User Flow
        │
        ▼
Figma Prototype
        │
        ▼
Design System
        │
        ▼
Technical Design
        │
        ▼
Flutter Component
        │
        ▼
State / Integration
        │
        ▼
Automated Tests
```

This helps reduce the gap between design decisions and engineering implementation.

---

# Accessibility

The architecture considers accessibility as part of UI quality.

Relevant concerns include:

```text
semantic widgets
touch target size
text readability
contrast
responsive layouts
screen reader compatibility
clear form labels
error feedback
dynamic content states
```

Accessibility should evolve together with the Design System rather than be applied only after screens are complete.

---

# Responsive Design

Because Flutter is used across Android, iOS and Web, layouts should not depend on a single physical device size.

The architecture should account for:

```text
screen constraints
orientation
different pixel densities
safe areas
mobile vs web layouts
keyboard behavior
font scaling
```

Responsive behavior belongs to the presentation system rather than being solved by individual screens independently.

---

# Testing Strategy

Testing is treated as part of architecture.

Passia follows a **TDD-oriented engineering approach** where behavior is validated as close as possible to the layer that owns it.

The testing strategy includes:

```text
Unit Tests
Widget Tests
State Management Tests
Repository Tests
API Integration Tests
Authentication Tests
Navigation Tests
```

---

# Test Pyramid

```text
                    ┌─────────────┐
                    │ Integration │
                    ├─────────────┤
                    │   Widget    │
                    ├─────────────┤
                    │ State / App │
                    ├─────────────┤
                    │ Unit Tests  │
                    └─────────────┘
```

> **Diagram placeholder — Mobile Testing Strategy**
>
> Suggested file:
>
> `docs/images/05-testing-strategy.png`

---

# Test Coverage

For the currently implemented and measured portfolio scope, the project targets and maintains:

```text
100% automated test coverage
```

The objective is not coverage as a vanity metric.

Tests should validate behavior that protects architectural boundaries, including:

```text
state transitions
repositories
API result mapping
authentication behavior
error states
navigation decisions
feature orchestration
```

> Coverage should always be regenerated before publishing a new public project checkpoint so that the README reflects the repository state accurately.

---

# Quality Gates

A representative local quality pipeline includes:

```bash
flutter analyze
flutter test --coverage
flutter build apk --debug
```

The development checkpoint also validated:

```text
23 automated Flutter tests
flutter analyze successful
debug APK build successful
```

---

# TDD

Test-Driven Development is used as an engineering discipline where appropriate.

The intended cycle is:

```text
Requirement
    │
    ▼
Expected behavior
    │
    ▼
Test
    │
    ▼
Implementation
    │
    ▼
Refactor
```

The objective is to make architectural changes safer and discourage business logic from migrating into widgets or infrastructure classes.

---

# Error Handling

Errors should be transformed into states that make sense to the presentation layer.

```text
HTTP / SDK / Device Error
          │
          ▼
     Data Layer
          │
          ▼
   Repository Mapping
          │
          ▼
 Application State
          │
          ▼
 User-friendly UI
```

Raw infrastructure exceptions should not determine user-facing messages.

---

# Performance

Performance is considered across multiple layers:

### Rendering

```text
controlled rebuild scope
lightweight widgets
appropriate state ownership
efficient list rendering
```

### Networking

```text
timeouts
controlled retries
request cancellation when applicable
response mapping outside presentation
```

### Startup

```text
avoid unnecessary initialization
lazy-load noncritical services
restore session predictably
```

### Location

```text
appropriate GPS update frequency
avoid unnecessary geocoding
batch tracking synchronization
```

Performance optimizations should be based on profiling rather than assumptions.

---

# Mobile Observability

A production evolution may include:

```text
crash reporting
performance monitoring
structured application logs
startup metrics
network error rates
screen load latency
authentication failures
location permission failures
tracking synchronization failures
```

Providers such as Firebase Crashlytics or equivalent tooling can be integrated behind operational boundaries.

Observability should provide actionable information without collecting unnecessary personal or precise-location data.

---

# Privacy by Design

Location is a particularly sensitive category of product data.

The application architecture therefore considers:

- asking for permission in context;
- collecting only necessary information;
- avoiding precise coordinates in logs;
- not exposing tracking payloads in debug output;
- keeping authentication credentials out of application logs;
- sending sensitive information only over TLS;
- letting the backend remain the authority for data access.

---

# Native Platform Integration

Cross-platform architecture does not eliminate native platform knowledge.

The solution still accounts for:

### Android

```text
runtime permissions
application lifecycle
deep links / app links
background behavior
notification channels
signing
Play Store delivery
```

### iOS

```text
permission declarations
application lifecycle
Universal Links
background limitations
APNs integration
Keychain
App Store distribution
```

Platform channels remain available when a native capability cannot be modeled appropriately through the shared Flutter layer.

---

# Deep Linking

Authentication already requires understanding application links/callback behavior.

The same architecture can evolve to support product deep links such as:

```text
/passia/walk/{id}
/passia/pet/{id}
/passia/notification/{context}
```

Deep links should be mapped into application navigation instead of letting external providers directly control screens.

---

# Authentication Validation

The mobile Auth0 integration uses:

```text
auth0_flutter
Authorization Code + PKCE
Universal Login
Credentials Manager
OIDC scopes
Bearer access token
```

The Android callback/App Link configuration was validated during the development checkpoint.

The complete OIDC/JWT contract has also been tested against the published Passia backend using an OAuth test client.

Physical-device validation inside the Flutter application remains part of a future project checkpoint.

---

# Backend Integration

The mobile and backend architectures were designed together rather than independently.

```text
Passia Mobile
      │
      │ REST + JWT
      ▼
Passia Backend
      │
      ▼
Domain authorization
      │
      ▼
PostgreSQL
```

The mobile never owns security-critical backend rules.

For example:

```text
Pet ownership
Walk authorization
Domain identity
Lifecycle invariants
```

remain server-side concerns.

---

# Architecture vs Technology

The project distinguishes architectural capability from simply including dependencies.

| Capability | Current approach |
|---|---|
| Cross-platform mobile | Flutter |
| Android | supported architecture target |
| iOS | supported architecture target |
| Web | supported architecture target |
| State management | Cubit / BLoC |
| API integration | Dio + REST |
| Authentication | Auth0 / OIDC / PKCE |
| Secure API access | JWT Bearer |
| Location | OS geolocation abstraction |
| Address UX | reverse geocoding |
| Places | autocomplete abstraction |
| Testing | unit/widget/integration strategy |
| Test coverage | 100% on measured current scope |
| UI consistency | reusable Design System |
| Offline tracking | architectural direction |
| Push notifications | prepared architecture / future integration |
| Observability | production evolution |
| CI/CD | architecture prepared for automation |
| Native integration | isolated platform capability |
| Android/iOS releases | future production pipeline |

---

# Staff / Mobile Architecture Perspective

The objective of this project is not only to demonstrate Flutter syntax.

It also demonstrates engineering concerns expected at **Senior, Staff and Mobile Architect** levels.

## Technical Direction

```text
architecture definition
technology trade-offs
feature boundaries
state management strategy
security boundaries
testing strategy
platform abstraction
API integration standards
```

## Engineering Governance

```text
reusable patterns
quality gates
design consistency
dependency boundaries
architecture documentation
testing expectations
security practices
```

## Product Engineering

```text
translate UX requirements into architecture
evaluate feasibility before implementation
balance product speed and maintainability
optimize perceived performance
design for future product evolution
```

## Cross-functional Architecture

```text
Mobile
Product
UX/UI
Backend
Security
Cloud
QA
DevOps
```

The project treats mobile architecture as part of the whole product system rather than an isolated frontend layer.

---

# Architecture Decision Examples

Important technical decisions include:

## ADR — Flutter for Multiplatform Delivery

**Decision**

Use Flutter as the shared application framework for Android, iOS and Web.

**Drivers**

```text
shared product experience
development efficiency
consistent Design System
shared test strategy
reusable business/application code
single architectural governance model
```

**Trade-off**

Platform-specific behavior must still be understood and isolated appropriately.

---

## ADR — Cubit/BLoC State Management

UI rendering remains separated from asynchronous feature orchestration.

The objective is deterministic state and testability rather than letting widgets become controllers.

---

## ADR — External Authentication

Credential authentication is delegated to an Identity Provider instead of implementing password security inside the mobile application.

---

## ADR — Authorization Remains Server-Side

The mobile client never becomes the authority for resource ownership.

---

## ADR — Offline-First Tracking Direction

GPS collection should not depend on continuous network availability.

---

## ADR — Provider-Neutral Location Architecture

Map, geocoding and routing provider models should not become Passia product models.

---

# Product UX Principles

```text
Clarity over density

Fast feedback over silent processing

Familiar interaction over unnecessary novelty

Progressive disclosure over overloaded screens

Reusable patterns over isolated UI decisions

Human-readable information over implementation details

Product consistency across platforms
```

---

# Main User Journey

A representative flow is:

```text
Launch
   │
   ▼
Authentication
   │
   ▼
Tutor Home
   │
   ▼
Select Pet
   │
   ▼
Select Walk Type
   │
   ▼
Select Professional / Option
   │
   ▼
Date & Time
   │
   ▼
Origin / Stops / Destination
   │
   ▼
Route Preview
   │
   ▼
Review
   │
   ▼
Walk
   │
   ▼
Tracking / Status
```

> **Diagram placeholder — Product User Flow**
>
> Suggested file:
>
> `docs/images/06-user-flow.png`

---

# Screens

## Onboarding

> **Image placeholder**

<!--
![Passia Onboarding](docs/images/screens/onboarding.png)
-->

---

## Pet Selection

> **Image placeholder**

<!--
![Pet Selection](docs/images/screens/pet-selection.png)
-->

---

## Professional Profile

> **Image placeholder**

<!--
![Professional Profile](docs/images/screens/professional-profile.png)
-->

---

## Walk Type

> **Image placeholder**

<!--
![Walk Type](docs/images/screens/walk-type.png)
-->

---

## Schedule

> **Image placeholder**

<!--
![Schedule](docs/images/screens/schedule.png)
-->

---

## Route Planner

> **Image placeholder**

<!--
![Route Planner](docs/images/screens/route-planner.png)
-->

---

## Order Review

> **Image placeholder**

<!--
![Order Review](docs/images/screens/order-review.png)
-->

---

# Product Design Gallery

> **Figma placeholder — complete design board**
>
> Recommended: export one high-resolution board showing multiple screens and flows.

<!--
![Figma Product Design](docs/images/figma/passia-product-design.png)
-->

### Product Design

```text
Figma: [FIGMA PROJECT URL]
```

The design work includes:

```text
visual identity
color palette
component patterns
screen hierarchy
navigation flow
interaction design
route planning UX
responsive considerations
mobile usability
```

---

# Website

🌐 **https://www.passia.com.br**

The website represents the product's external identity and landing experience.

> **Website image placeholder**

<!--
![Passia Website](docs/images/passia-website.png)
-->

---

# Repository Structure

A public portfolio repository can evolve toward:

```text
.
├── docs/
│   ├── architecture/
│   │   ├── adr/
│   │   └── diagrams/
│   │
│   ├── design/
│   └── images/
│
├── lib/
│   ├── core/
│   ├── features/
│   └── main.dart
│
├── test/
│
├── integration_test/
│
├── pubspec.yaml
└── README.md
```

---

# Suggested Diagram Gallery

When preparing the public portfolio, I recommend adding these diagrams.

### 01 — Mobile Architecture

```text
docs/images/01-mobile-architecture.png
```

### 02 — Authentication Flow

```text
docs/images/02-authentication-flow.png
```

### 03 — Location Architecture

```text
docs/images/03-location-architecture.png
```

### 04 — Offline Tracking

```text
docs/images/04-offline-tracking.png
```

### 05 — Testing Strategy

```text
docs/images/05-testing-strategy.png
```

### 06 — Product User Flow

```text
docs/images/06-user-flow.png
```

---

# Engineering Quality

The project emphasizes:

```text
Clean Code
SOLID
separation of concerns
small reusable components
explicit application states
automated tests
static analysis
architecture documentation
environment isolation
secure authentication
code review readiness
```

---

# Evolution Roadmap

If development resumes, architectural evolution may include:

```text
physical-device authentication validation
full walk lifecycle
offline GPS tracking
tracking synchronization
push notifications
deep linking
mobile analytics
crash reporting
performance monitoring
CI/CD pipeline
automated store delivery
accessibility validation
golden tests
production observability
```

Each addition should be introduced because of a product or engineering requirement rather than merely to expand the technology list.

---

# Engineering Philosophy

```text
Product decisions inform architecture.

Architecture protects future product evolution.

Tests protect architecture.

Security belongs to system design.

Cross-platform does not mean ignoring platform behavior.

UX performance is part of software quality.

Infrastructure should be proportional to product maturity.

Technology choices should solve demonstrated problems.
```

---

# Portfolio Purpose

Passia Mobile was created to demonstrate the relationship between:

```text
Product Discovery
      │
      ▼
Product Design
      │
      ▼
Mobile Architecture
      │
      ▼
Flutter Engineering
      │
      ▼
API & Security Integration
      │
      ▼
Automated Testing
      │
      ▼
Platform Delivery
      │
      ▼
Product Evolution
```

The project is intended to demonstrate both **hands-on mobile engineering** and the architectural reasoning expected from senior technical leadership roles.

---

# Key Takeaway

> **Mobile architecture is not only about choosing a framework or state-management library.**
>
> It is about creating technical boundaries that allow Product, UX, Security, Backend and platform capabilities to evolve without turning the application into a collection of tightly coupled screens.

---

# Author

**Raquel Silva**

Mobile Architecture • Software Architecture • Staff Engineering • Technical Leadership • Flutter • Java • Product Engineering

Website: https://www.passia.com.br

Figma: `[updating]`

---

# Project Status

**Development paused — Portfolio / MVP**

Passia is currently paused due to a temporary health-related leave by its creator.

The repository is preserved as a **Mobile Architecture, Flutter Engineering and Product Design portfolio case study**, documenting the technical decisions, implemented components, UX work, automated testing strategy, security model and future evolution designed up to the current project checkpoint.

This repository should **not be considered a currently operational production application**.

The complete application and external development services may not currently be available.

Development may resume when circumstances allow.

**Last active development checkpoint: Jan 2026.**
