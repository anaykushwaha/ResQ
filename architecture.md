# ResQ — System Architecture

## 1. Overview

ResQ is an AI-powered emergency resource coordination and decision-support platform.

The system combines:

* structured emergency data
* verification
* geographic reasoning
* deterministic recommendation logic
* grounded LLM reasoning
* dynamic simulation
* interactive visualization

The architecture is deliberately designed around a separation between **emergency intelligence** and **AI-generated communication**.

The fundamental architectural principle is:

> **The system determines emergency facts deterministically; AI reasons over verified context and explains the resulting plan.**

ResQ is a hackathon prototype. Its emergency scenario uses simulated data and does not represent an authoritative emergency service.

---

# 2. Architectural Goals

The architecture is designed to achieve six primary goals.

### 2.1 Safety

The system must avoid generating unsupported emergency facts or recommending resources that the deterministic intelligence layer has determined to be unavailable or unsuitable.

### 2.2 Explainability

Recommendations should be accompanied by understandable reasons, supporting information, sources, confidence, and timestamps where applicable.

### 2.3 Geographic Awareness

Emergency recommendations must account for:

* distance
* hazards
* road conditions
* evacuation zones
* route accessibility
* resource location

### 2.4 Personalization

Recommendations should account for the user's specific circumstances.

### 2.5 Dynamic Adaptation

When emergency conditions change, the system must be capable of recalculating the resulting action plan.

### 2.6 Separation of Responsibilities

The frontend, backend intelligence layer, AI layer, data layer, and simulation layer should have clear boundaries.

---

# 3. High-Level Architecture

```text
                         RESQ
                           |
             +-------------+-------------+
             |                           |
             v                           v
         FRONTEND                     BACKEND
             |                           |
             |                  +--------+--------+
             |                  |                 |
             |                  v                 v
             |            Emergency          AI Engine
             |            Intelligence
             |                  |
             |        +---------+---------+
             |        |         |         |
             |        v         v         v
             |   Verification Geography Recommendation
             |                           |
             |                           v
             |                      Action Plan
             |                           |
             +---------------------------+
                         |
                         v
                    User Interface
```

The frontend visualizes system state.

The backend determines emergency intelligence.

The AI layer explains structured intelligence.

The simulation layer changes emergency state.

---

# 4. Major System Components

ResQ contains six major logical subsystems.

```text
1. Frontend
2. Backend API
3. Emergency Intelligence Engine
4. AI / Grounding Layer
5. Data & Ingestion Layer
6. Simulation Engine
```

---

# 5. Frontend Architecture

The frontend is responsible for user interaction and visualization.

Location:

```text
frontend/
```

Technology:

* React
* TypeScript
* Vite

The frontend is divided into:

```text
components/
pages/
hooks/
services/
state/
types/
utils/
styles/
```

---

## 5.1 Pages

```text
frontend/src/pages/
```

Contains:

```text
Home.tsx
Situation.tsx
Dashboard.tsx
Map.tsx
LiveFeed.tsx
NotFound.tsx
```

Pages compose reusable components rather than containing the majority of domain logic.

---

## 5.2 Components

Components are grouped according to user-facing functionality.

```text
components/
├── layout/
├── emergency/
├── situation/
├── plan/
├── resources/
├── hazards/
├── map/
├── feed/
├── sources/
├── simulation/
└── common/
```

This organization keeps visual responsibilities separated.

---

# 6. Frontend State Management

The frontend maintains application state through dedicated stores.

```text
frontend/src/state/
```

Primary stores:

```text
emergencyStore.ts
situationStore.ts
simulationStore.ts
```

These represent:

### Situation State

The user's current emergency context.

### Emergency State

Current emergency conditions and available intelligence.

### Simulation State

Current simulation state and active simulation events.

---

# 7. Frontend Hooks

```text
frontend/src/hooks/
```

Hooks encapsulate reusable application behavior.

```text
useEmergencyState.ts
useSituation.ts
useRecommendations.ts
useSimulation.ts
usePolling.ts
```

Hooks should coordinate:

```text
UI
 |
v
Hook
 |
v
Service
 |
v
API
```

---

# 8. Frontend API Services

```text
frontend/src/services/
```

Services provide a boundary between UI logic and HTTP communication.

```text
api.ts
situationApi.ts
recommendationApi.ts
resourceApi.ts
simulationApi.ts
```

The UI should not contain scattered raw HTTP requests.

Instead:

```text
Component
   |
   v
Hook
   |
   v
API Service
   |
   v
Backend
```

---

# 9. Backend Architecture

The backend is responsible for emergency intelligence, domain logic, AI orchestration, data processing, and simulation integration.

Location:

```text
backend/
```

Technology:

* Python
* FastAPI
* Pytest

The application is organized into:

```text
api/
models/
schemas/
services/
ingestion/
core/
utils/
```

---

# 10. API Layer

Location:

```text
backend/app/api/routes/
```

Routes include:

```text
health.py
situation.py
recommendations.py
resources.py
hazards.py
emergency.py
simulation.py
```

The API layer should remain relatively thin.

Its responsibilities are:

* receive requests
* validate input
* invoke appropriate services
* return structured responses
* handle HTTP-level errors

Business logic should live in services and core modules rather than route functions.

---

# 11. Domain Models

Location:

```text
backend/app/models/
```

Models represent core emergency concepts:

```text
Emergency
Resource
Shelter
Hazard
Road
EvacuationZone
Situation
Recommendation
Source
Route
```

These objects form the domain vocabulary of ResQ.

---

# 12. Schemas

Location:

```text
backend/app/schemas/
```

Schemas define API-facing structures.

Important schemas include:

```text
Emergency
Resource
Shelter
Hazard
Situation
Recommendation
Simulation
API
```

Schemas create an explicit contract between the frontend and backend.

---

# 13. Emergency Intelligence Layer

The emergency intelligence layer is the core deterministic reasoning system.

Important services:

```text
emergency_service.py
resource_service.py
hazard_service.py
situation_service.py
verification_service.py
geographic_service.py
route_service.py
recommendation_engine.py
```

The intelligence pipeline is:

```text
Situation
   |
   v
Candidate Discovery
   |
   v
Verification
   |
   v
Safety Filtering
   |
   v
Geographic Filtering
   |
   v
Need Matching
   |
   v
Scoring
   |
   v
Ranking
   |
   v
Recommendation
```

---

# 14. Verification Architecture

Location:

```text
backend/app/services/verification_service.py
backend/app/core/confidence.py
```

Verification evaluates factors such as:

* source reliability
* freshness
* verification status
* confidence

The verification layer exists to prevent unverified information from being treated as equally trustworthy.

Conceptually:

```text
Raw Data
   |
   v
Source Metadata
   |
   v
Reliability
   +
Freshness
   +
Verification
   |
   v
Confidence
```

---

# 15. Geographic Reasoning

Location:

```text
backend/app/services/geographic_service.py
backend/app/services/route_service.py
backend/app/utils/distance.py
```

Geographic reasoning considers:

* user location
* resource location
* distance
* hazards
* road status
* evacuation zones
* route geometry

The geographic engine determines whether a resource or route is geographically appropriate.

The frontend does not independently determine emergency safety.

---

# 16. Recommendation Engine

Location:

```text
backend/app/services/recommendation_engine.py
backend/app/core/filtering.py
backend/app/core/scoring.py
backend/app/core/ranking.py
```

The recommendation engine transforms emergency state into an ordered action plan.

```text
User Situation
      +
Emergency State
      |
      v
Candidate Resources
      |
      v
Filtering
      |
      v
Scoring
      |
      v
Ranking
      |
      v
Prioritized Plan
```

Filtering occurs before ranking.

A resource that is known to be unusable should not simply receive a lower score; it should generally be removed from the candidate set.

---

# 17. Core Filtering

Location:

```text
backend/app/core/filtering.py
```

Potential filtering conditions include:

* closed resource
* unavailable resource
* unsafe location
* evacuation-zone conflict
* blocked road
* incompatible accessibility
* unreachable route
* invalid or insufficient verification

The purpose of filtering is to establish a safe candidate set before ranking.

---

# 18. Scoring and Ranking

Location:

```text
backend/app/core/scoring.py
backend/app/core/ranking.py
```

Candidates can be evaluated using factors such as:

* relevance to user needs
* urgency
* distance
* accessibility
* availability
* capacity
* geographic safety
* confidence
* transportation compatibility

The exact weighting should remain explicit and testable.

---

# 19. AI Architecture

The AI system consists of four major services:

```text
context_builder.py
ai_service.py
response_validator.py
grounding_service.py
```

Pipeline:

```text
Verified Emergency Data
          +
User Situation
          +
Recommendation Results
          |
          v
   Context Builder
          |
          v
       AI Model
          |
          v
 Structured Response
          |
          v
 Response Validator
          |
          v
 Grounding Validator
          |
          v
      Frontend
```

---

# 20. Context Builder

Location:

```text
backend/app/services/context_builder.py
```

The context builder creates the structured information supplied to the AI.

It should include only information that the system has intentionally selected for reasoning.

Potential context:

```text
user situation
current emergency state
verified resources
hazards
roads
evacuation zones
recommendations
sources
confidence
timestamps
```

The context builder is a major defense against uncontrolled AI generation.

---

# 21. AI Service

Location:

```text
backend/app/services/ai_service.py
```

The AI service is responsible for communicating with the selected LLM provider.

The AI should primarily perform:

* explanation
* summarization
* communication
* structured reasoning over supplied context

It should not be treated as the authoritative emergency database.

---

# 22. Response Validation

Location:

```text
backend/app/services/response_validator.py
```

AI output should be validated before being presented to the user.

Validation should check:

* response structure
* required fields
* supported claims
* expected types
* invalid or malformed output

Invalid responses should not silently become trusted emergency information.

---

# 23. Grounding Service

Location:

```text
backend/app/services/grounding_service.py
```

Grounding verifies that important AI claims are supported by the context supplied by the system.

Conceptually:

```text
AI Claim
   |
   v
Search Supporting Context
   |
   +---- Found ----> Accept
   |
   +---- Not Found -> Reject / Fallback
```

This creates a boundary between:

```text
Verified Emergency Fact
```

and:

```text
AI Explanation
```

---

# 24. Data Architecture

Location:

```text
data/
```

The prototype uses structured JSON emergency data.

Primary scenario:

```text
data/scenarios/hurricane_harborview/
```

Files:

```text
scenario.json
shelters.json
resources.json
hazards.json
roads.json
evacuation_zones.json
alerts.json
emergency_events.json
sources.json
```

---

# 25. Data Schemas

Location:

```text
data/schemas/
```

Schemas include:

```text
emergency-event.schema.json
resource.schema.json
shelter.schema.json
hazard.schema.json
road.schema.json
scenario.schema.json
```

These define expected structures for the scenario data.

---

# 26. Ingestion Architecture

Location:

```text
backend/app/ingestion/
```

Files:

```text
loader.py
normalizer.py
validators.py
registry.py
```

Pipeline:

```text
Raw Source
    |
    v
Loader
    |
    v
Normalizer
    |
    v
Validator
    |
    v
Registry
    |
    v
Emergency Intelligence
```

The architecture is designed so future real data sources can be incorporated without fundamentally changing the recommendation engine.

The prototype itself uses simulated Harborview data.

---

# 27. Simulation Architecture

Location:

```text
simulation/
```

Files:

```text
engine.py
events.py
scenarios.py
state_manager.py
event_registry.py
transition.py
```

The simulation engine represents controlled changes to the emergency environment.

Supported events:

```text
CLOSE_SHELTER
FLOOD_ROAD
OPEN_RESOURCE
EXPAND_EVACUATION_ZONE
ADD_HAZARD
RESET
```

---

# 28. Simulation Data Flow

```text
Frontend Event
      |
      v
Simulation API
      |
      v
Simulation Engine
      |
      v
State Manager
      |
      v
State Transition
      |
      v
Emergency State
      |
      v
Recommendation Engine
      |
      v
New Action Plan
      |
      v
Frontend
```

The important architectural property is that simulation events do not manually rewrite the frontend.

They change backend state.

The backend then recalculates the resulting intelligence.

---

# 29. Map Architecture

The map belongs primarily to the frontend visualization layer, but depends heavily on backend geographic intelligence.

Frontend files:

```text
frontend/src/components/map/
```

include:

```text
EmergencyMap.tsx
MapControls.tsx
UserMarker.tsx
ShelterMarker.tsx
ResourceMarker.tsx
HazardMarker.tsx
RoadClosureLayer.tsx
EvacuationZoneLayer.tsx
RecommendedRoute.tsx
```

Backend provides:

```text
resource coordinates
hazard geometry
road geometry
road status
evacuation-zone geometry
route geometry
```

The relationship is:

```text
             BACKEND
                 |
        Geographic Intelligence
                 |
                 v
          Geographic API
                 |
                 v
             FRONTEND
                 |
                 v
              Map UI
```

The frontend visualizes geographic facts rather than independently determining emergency safety.

---

# 30. API Contract Boundary

The API contract is the primary boundary between the two development tracks.

```text
             API CONTRACT
                  |
        +---------+---------+
        |                   |
        v                   v
    BACKEND             FRONTEND
        |                   |
    Real Data            UI Logic
    Real AI              Visualization
    Simulation           Interaction
```

The API contract defines:

* endpoints
* methods
* requests
* responses
* field names
* types
* errors
* status codes
* timestamps
* confidence
* source information

Canonical documentation:

```text
docs/api-contract.md
```

---

# 31. Two-Person Development Architecture

ResQ is intentionally structured for parallel development.

## Person 1

Owns:

```text
backend/
data/
simulation/
```

Primary responsibility:

> **Determine what ResQ knows and how ResQ reasons about emergency conditions.**

---

## Person 2

Owns:

```text
frontend/
assets/
```

Primary responsibility:

> **Determine how users interact with and understand what ResQ knows.**

---

## Shared Boundary

The intersection is:

```text
API Contract
Data Schemas
Geographic Structures
Recommendation Structures
AI Response Structures
Simulation Events
```

---

# 32. Parallel Development Model

The project uses phase-aligned parallel development.

```text
Phase 0
   |
   +--> Backend
   |
   +--> Frontend
   |
   +--> Shared Contract
   |
   v
Phase 1
   |
   +--> Backend
   |
   +--> Frontend
   |
   +--> Shared Intersection
   |
   v
Phase 2
   |
   ...
```

Neither contributor needs to finish their entire system before the other begins.

Frontend development can use mock responses while backend functionality is under development.

Backend development can be tested directly using structured requests without the completed frontend.

---

# 33. Phase-by-Phase Architecture Intersections

## Phase 0

```text
Architecture
      |
      v
API Contract
```

Shared:

```text
docs/architecture.md
docs/api-contract.md
```

---

## Phase 1

```text
FastAPI
   +
React
   |
   v
API conventions
```

---

## Phase 2

```text
Backend Situation Schema
          |
          v
Frontend Situation Form
```

---

## Phase 3

```text
Emergency Dataset
          |
          v
Resource / Hazard UI
```

---

## Phase 4

```text
Geographic Engine
          |
          v
Geographic API
          |
          v
Emergency Map
```

---

## Phase 5

```text
Recommendation Engine
          |
          v
Recommendation API
          |
          v
Action Plan UI
```

---

## Phase 6

```text
Grounded AI Response
          |
          v
Explanation UI
```

---

## Phase 7

```text
Simulation Engine
          |
          v
Simulation API
          |
          v
Simulation Controls
```

---

## Phase 8

```text
Unified Emergency State
          |
          v
Dashboard + Live Feed
```

---

## Phase 9

```text
Real Backend
      +
Real Frontend
      |
      v
Full Integration
```

---

# 34. Safety Architecture

Safety-sensitive decisions should remain deterministic wherever practical.

The system should follow:

```text
Unverified Information
        |
        v
Verification
        |
        v
Safe Candidate Set
        |
        v
Geographic Constraints
        |
        v
Recommendation
        |
        v
AI Explanation
```

The reverse architecture should be avoided:

```text
User
 |
 v
LLM
 |
 v
Invented Emergency Information
```

---

# 35. Error Handling

Errors should be handled at multiple layers.

### Frontend

Handles:

* loading
* API failures
* empty results
* invalid user input
* unavailable data

### API

Handles:

* malformed requests
* validation errors
* resource errors
* server errors

### Services

Handle:

* unavailable data
* invalid state
* failed integrations
* recommendation failures

### AI

Handles:

* malformed model output
* unsupported claims
* grounding failures
* unavailable model provider

The system should prefer a transparent fallback over presenting unsupported information.

---

# 36. Testing Architecture

Backend tests:

```text
backend/tests/
```

Frontend tests:

```text
frontend/tests/
```

Testing occurs at several levels:

```text
Unit Tests
    |
    v
Service Tests
    |
    v
API Tests
    |
    v
Frontend Tests
    |
    v
Integration Tests
    |
    v
End-to-End Scenario
```

The simulation scenario is especially important because it tests whether changes in emergency state correctly propagate through the entire system.

---

# 37. End-to-End Architecture

The complete system can be represented as:

```text
                         USER
                           |
                           v
                    FRONTEND UI
                           |
                           v
                  Situation Request
                           |
                           v
                     FASTAPI
                           |
                           v
                  Situation Service
                           |
             +-------------+-------------+
             |             |             |
             v             v             v
          Data        Verification   Geography
             |             |             |
             +-------------+-------------+
                           |
                           v
                 Recommendation Engine
                           |
                           v
                    Prioritized Plan
                           |
                           v
                    Context Builder
                           |
                           v
                       LLM / AI
                           |
                           v
                 Response Validation
                           |
                           v
                    Grounding Check
                           |
                           v
                    Validated Result
                           |
             +-------------+-------------+
             |             |             |
             v             v             v
          Dashboard       Map        Live Feed
             |             |             |
             +-------------+-------------+
                           |
                           v
                    User understands
                    what to do next
```

---

# 38. Dynamic Update Architecture

When conditions change:

```text
Emergency Event
      |
      v
Simulation Engine
      |
      v
State Manager
      |
      v
Emergency State Updated
      |
      v
Recommendation Engine
      |
      v
New Priorities
      |
      v
New Routes
      |
      v
New Action Plan
      |
      v
Frontend Updates
```

This is the defining dynamic behavior of ResQ.

---

# 39. Example Dynamic Scenario

Initial:

```text
Shelter A = OPEN
Road A = OPEN
Water Center = CLOSED
Evacuation Zone = Zone 1
```

The user receives:

```text
1. Shelter A
2. Water Center later
3. Avoid Hazard B
```

Then:

```text
CLOSE_SHELTER
```

New state:

```text
Shelter A = CLOSED
```

The recommendation engine recalculates.

Then:

```text
FLOOD_ROAD
```

New state:

```text
Road A = BLOCKED
```

The geographic engine recalculates routes.

Then:

```text
EXPAND_EVACUATION_ZONE
```

The system evaluates affected resources and priorities again.

Finally:

```text
OPEN_RESOURCE
```

The newly available water center becomes eligible for recommendation.

---

# 40. Architectural Principles

ResQ follows these principles:

### Separation of Concerns

Each subsystem has a clearly defined responsibility.

### Deterministic Emergency Intelligence

Critical emergency facts should not depend on unconstrained language generation.

### Grounded AI

AI should reason over structured information supplied by the system.

### Explicit Contracts

Frontend and backend communicate through documented schemas.

### Geographic Awareness

Location and physical constraints influence recommendations.

### Explainability

Recommendations should have understandable supporting reasons.

### Dynamic Recalculation

Changing emergency conditions should produce changing recommendations.

### Fail Safely

When reliable information is unavailable, the system should surface uncertainty rather than fabricate an answer.

### Mock-First Parallel Development

Frontend and backend can progress independently using agreed contracts and mock responses.

### Testable Logic

Core emergency reasoning should be independently testable without requiring the complete frontend.

---

# 41. Architecture Summary

The ResQ architecture can ultimately be summarized as:

```text
             VERIFIED DATA
                    |
                    v
             EMERGENCY STATE
                    |
          +---------+---------+
          |         |         |
          v         v         v
     Verification Geography Hazards
          |         |         |
          +---------+---------+
                    |
                    v
          RECOMMENDATION ENGINE
                    |
                    v
             PRIORITIZED PLAN
                    |
                    v
              GROUNDED AI
                    |
                    v
          VALIDATED EXPLANATION
                    |
                    v
                FRONTEND
                    |
       +------------+------------+
       |            |            |
       v            v            v
     PLAN          MAP         FEED
       |            |            |
       +------------+------------+
                    |
                    v
                 USER
                    |
                    v
             "WHAT DO I DO?"
```

The fundamental ResQ architecture is therefore:

> **Verified emergency intelligence determines what is possible and appropriate. Geographic reasoning determines what is reachable. The recommendation engine determines what should be prioritized. Grounded AI explains the result. The frontend makes it understandable. The simulation engine demonstrates how the entire system adapts when the emergency changes.**

