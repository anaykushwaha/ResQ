# Contributing to ResQ

Thank you for contributing to **ResQ**.

ResQ is an AI-powered emergency resource coordination and decision-support platform built as a hackathon prototype. Because the project combines emergency intelligence, geographic reasoning, AI, simulation, and a user-facing interface, contributions should preserve the project's architectural boundaries and safety principles.

This document defines the development workflow, branch strategy, ownership model, coding standards, testing expectations, and pull-request process for the project.

---

# 1. Project Philosophy

ResQ is built around one central principle:

> **Verified emergency information determines what is possible and appropriate; AI explains and communicates that information.**

Contributions should preserve this separation.

In particular:

* Do not move critical emergency facts into unconstrained AI generation.
* Do not allow the AI to invent emergency resources.
* Do not recommend known closed or unsafe resources.
* Do not bypass geographic safety checks.
* Do not hide uncertainty.
* Do not introduce undocumented API behavior.
* Do not couple the frontend directly to backend implementation details.

Every major feature should fit into the existing architecture rather than creating an independent parallel system.

---

# 2. Repository Structure

The project is organized into the following major areas:

```text
resq/
│
├── .github/             # GitHub workflows and contribution templates
├── frontend/            # React + TypeScript application
├── backend/             # Python + FastAPI application
├── data/                # Emergency scenario data and schemas
├── simulation/          # Dynamic emergency simulation engine
├── docs/                # Supporting technical documentation
├── scripts/             # Development and demonstration utilities
├── assets/              # Screenshots, diagrams, and demo assets
│
├── .env.example
├── .gitignore
├── LICENSE
├── README.md
├── architecture.md
├── CONTRIBUTING.md
├── PROJECT_STATUS.md
├── pyproject.toml
└── docker-compose.yml
```

---

# 3. Two-Person Ownership Model

ResQ uses a parallel two-person development model.

Both contributors work on the **same numbered phase at the same time**.

## Person 1 — Backend / Emergency Intelligence

Primary ownership:

```text
backend/
data/
simulation/
```

Responsibilities include:

* FastAPI
* backend models
* API routes
* schemas
* data ingestion
* verification
* geographic reasoning
* recommendation engine
* AI integration
* grounding
* simulation logic
* backend tests

---

## Person 2 — Frontend / UX / Visualization

Primary ownership:

```text
frontend/
assets/
```

Responsibilities include:

* React
* TypeScript
* UI components
* situation interface
* dashboard
* action plans
* resources
* hazards
* map
* live feed
* sources
* confidence visualization
* simulation controls
* frontend tests
* visual assets

---

## Shared Responsibilities

Both contributors share responsibility for:

```text
architecture.md
docs/api-contract.md
docs/emergency-safety.md
docs/testing.md
docs/development-handoff.md
docs/demo-script.md
docs/deployment.md
docs/limitations.md
docs/future-work.md

README.md
PROJECT_STATUS.md
CONTRIBUTING.md
```

The final integration, testing, demonstration, and hackathon submission are joint responsibilities.

---

# 4. Development Principle: Work in Parallel

The project should **not** be developed sequentially.

The intended workflow is:

```text
                 SHARED CONTRACT
                       |
             +---------+---------+
             |                   |
             v                   v
        PERSON 1             PERSON 2
        BACKEND              FRONTEND
             |                   |
        Real Logic           Mock Data
        Real APIs            Mock APIs
        Real AI              Mock Responses
        Simulation           UI Simulation
             |                   |
             +---------+---------+
                       |
                       v
                  INTEGRATION
                       |
                       v
                 JOINT TESTING
```

The frontend does not need to wait for the backend to be completely finished.

The backend does not need to wait for the frontend to be completely finished.

The **API contract is the boundary** between the two systems.

---

# 5. Phase-Based Development

Both contributors progress through the same phase numbers.

## Phase 0 — Architecture & Contracts

### Person 1

* Define backend architecture.
* Define domain concepts.
* Define emergency data structures.
* Define backend API requirements.

### Person 2

* Define frontend architecture.
* Define page structure.
* Define user workflow.
* Define required UI data.

### Shared

Complete:

```text
architecture.md
docs/api-contract.md
PROJECT_STATUS.md
```

The API contract should be agreed upon before significant implementation begins.

---

## Phase 1 — Foundations

### Person 1

Build:

```text
backend/app/main.py
backend/app/config.py
backend/app/dependencies.py
backend/app/api/routes/health.py
```

Establish:

* FastAPI application
* CORS
* configuration
* logging
* health endpoint
* basic error handling

### Person 2

Build:

```text
frontend/src/main.tsx
frontend/src/App.tsx
frontend/src/router.tsx
frontend/src/components/layout/*
frontend/src/components/common/*
```

Establish:

* React application
* routing
* app shell
* reusable UI primitives
* responsive structure

### Intersection

Agree on:

* API base URL
* HTTP conventions
* error format
* health endpoint
* frontend/backend local development setup

---

# 6. Phase 2 — Models & Situation

### Person 1

Build:

```text
backend/app/models/*
backend/app/schemas/*
backend/app/services/situation_service.py
backend/app/api/routes/situation.py
```

Define:

* emergency models
* resource models
* shelter models
* hazard models
* road models
* evacuation zones
* situation
* recommendations
* sources
* routes

### Person 2

Build:

```text
frontend/src/components/situation/*
frontend/src/pages/Situation.tsx
frontend/src/types/situation.ts
frontend/src/services/situationApi.ts
frontend/src/state/situationStore.ts
frontend/src/hooks/useSituation.ts
```

### Intersection

The following must match exactly:

```text
Frontend Situation
        |
        v
Situation API Request
        |
        v
Backend Situation Schema
```

Required user information should be agreed upon jointly.

---

# 7. Phase 3 — Emergency Data & Resource UI

### Person 1

Build:

```text
data/scenarios/hurricane_harborview/*
data/schemas/*
backend/app/ingestion/*
backend/app/services/resource_service.py
backend/app/services/hazard_service.py
```

Create:

* Harborview scenario
* shelters
* resources
* hazards
* roads
* evacuation zones
* alerts
* events
* source metadata

### Person 2

Build:

```text
frontend/src/components/resources/*
frontend/src/components/hazards/*
frontend/src/types/resource.ts
frontend/src/types/hazard.ts
frontend/src/services/resourceApi.ts
```

### Intersection

Backend data must provide the fields required by:

* resource cards
* shelter cards
* hazard cards
* availability indicators
* accessibility badges
* capacity indicators

---

# 8. Phase 4 — Verification & Geography

### Person 1

Build:

```text
backend/app/services/verification_service.py
backend/app/services/geographic_service.py
backend/app/services/route_service.py
backend/app/core/confidence.py
backend/app/utils/distance.py
backend/tests/test_verification.py
backend/tests/test_geography.py
backend/tests/test_routes.py
```

Implement:

* source verification
* freshness
* confidence
* geographic distance
* hazard-aware geography
* road restrictions
* evacuation zones
* route evaluation

### Person 2

Build:

```text
frontend/src/components/map/*
frontend/src/types/hazard.ts
frontend/src/types/resource.ts
frontend/src/types/api.ts
frontend/src/utils/distance.ts
frontend/src/styles/map.css
frontend/tests/components/EmergencyMap.test.tsx
```

### Intersection

This is the **major map intersection phase**.

Person 1 must provide the geographic contract for:

```text
User coordinates
Resource coordinates
Hazard geometry
Road geometry
Road status
Evacuation-zone geometry
Route geometry
```

Person 2 consumes those structures to render:

```text
User Marker
Shelter Markers
Resource Markers
Hazard Markers
Road Closures
Evacuation Zones
Recommended Routes
```

The frontend should **visualize** geographic safety information rather than independently deciding whether something is safe.

---

# 9. Phase 5 — Recommendation Engine & Action Plan

### Person 1

Build:

```text
backend/app/core/filtering.py
backend/app/core/scoring.py
backend/app/core/ranking.py
backend/app/services/recommendation_engine.py
backend/app/api/routes/recommendations.py
backend/tests/test_recommendations.py
```

Implement:

```text
Candidate Discovery
       ↓
Safety Filtering
       ↓
Need Matching
       ↓
Scoring
       ↓
Ranking
       ↓
Prioritized Recommendations
```

### Person 2

Build:

```text
frontend/src/components/plan/*
frontend/src/types/recommendation.ts
frontend/src/services/recommendationApi.ts
frontend/src/hooks/useRecommendations.ts
frontend/tests/components/ActionPlan.test.tsx
```

Build:

* priority badges
* urgency badges
* action cards
* recommendation reasons
* sources
* explanations
* empty states

### Intersection

Person 1 provides the recommendation response schema.

Person 2 builds the UI around that exact schema.

Example conceptual response:

```json
{
  "priority": 1,
  "urgency": "high",
  "action": "Go to Shelter A",
  "reason": "Closest verified accessible shelter",
  "resource_id": "shelter-a",
  "distance": 2.4,
  "confidence": 0.94,
  "source_id": "source-01"
}
```

---

# 10. Phase 6 — AI & Grounding

### Person 1

Build:

```text
backend/app/services/context_builder.py
backend/app/services/ai_service.py
backend/app/services/response_validator.py
backend/app/services/grounding_service.py
backend/tests/test_ai_service.py
backend/tests/test_grounding.py
backend/tests/test_response_validation.py
```

Pipeline:

```text
Verified Data
     ↓
Context Builder
     ↓
LLM
     ↓
Structured Response
     ↓
Response Validator
     ↓
Grounding Validator
```

### Person 2

Build:

```text
frontend/src/components/plan/PlanExplanation.tsx
frontend/src/components/plan/ActionReason.tsx
frontend/src/components/sources/*
frontend/src/types/source.ts
frontend/src/types/recommendation.ts
```

Display:

* explanation
* confidence
* verification status
* source
* reason
* uncertainty

### Intersection

The AI response must be represented in a documented API structure.

The frontend must never assume that an AI statement is automatically authoritative.

---

# 11. Phase 7 — Simulation

### Person 1

Build:

```text
simulation/engine.py
simulation/events.py
simulation/scenarios.py
simulation/state_manager.py
simulation/event_registry.py
simulation/transition.py
simulation/README.md

backend/app/api/routes/simulation.py
backend/app/schemas/simulation.py
backend/tests/test_simulation.py
```

Implement:

```text
CLOSE_SHELTER
FLOOD_ROAD
OPEN_RESOURCE
EXPAND_EVACUATION_ZONE
ADD_HAZARD
RESET
```

### Person 2

Build:

```text
frontend/src/components/simulation/*
frontend/src/hooks/useSimulation.ts
frontend/src/services/simulationApi.ts
frontend/src/state/simulationStore.ts
frontend/src/types/simulation.ts
```

### Intersection

Define:

```text
Simulation Event
      ↓
Simulation API
      ↓
Updated State
      ↓
Updated Recommendations
      ↓
Updated Frontend
```

The frontend triggers events.

The backend owns the actual state transition.

---

# 12. Phase 8 — Unified Emergency State

### Person 1

Finalize:

```text
backend/app/services/emergency_service.py
backend/app/api/routes/emergency.py
backend/app/models/emergency.py
backend/app/schemas/emergency.py
```

Ensure all emergency information can be represented as a coherent current state.

### Person 2

Build/finalize:

```text
frontend/src/components/emergency/*
frontend/src/components/feed/*
frontend/src/pages/Dashboard.tsx
frontend/src/pages/LiveFeed.tsx
frontend/src/state/emergencyStore.ts
frontend/src/hooks/useEmergencyState.ts
frontend/src/hooks/usePolling.ts
```

### Intersection

The frontend dashboard and live feed should reflect the backend's current emergency state.

---

# 13. Phase 9 — Full API Integration

At this point, mock responses are replaced with real backend responses.

### Person 1

Verify:

* API endpoints
* response schemas
* errors
* CORS
* simulation behavior
* recommendation updates
* AI responses

### Person 2

Verify:

* API services
* hooks
* state management
* loading states
* error states
* UI rendering
* map updates

### Shared

Run:

```text
Situation
    ↓
Recommendation
    ↓
Dashboard
    ↓
Map
    ↓
Simulation Event
    ↓
State Change
    ↓
Recalculation
    ↓
Updated UI
```

---

# 14. Phase 10 — Testing

### Person 1

Complete:

```text
backend/tests/*
```

### Person 2

Complete:

```text
frontend/tests/*
```

### Shared

Perform:

* integration testing
* end-to-end testing
* simulation testing
* safety testing
* API contract testing
* regression testing

---

# 15. Phase 11 — Documentation

Update:

```text
architecture.md
docs/api-contract.md
docs/ai-system.md
docs/data-model.md
docs/emergency-safety.md
docs/simulation.md
docs/geographic-reasoning.md
docs/verification.md
docs/recommendation-engine.md
docs/testing.md
docs/frontend.md
docs/backend.md
docs/development-handoff.md
docs/demo-script.md
docs/deployment.md
docs/limitations.md
docs/future-work.md
```

Documentation should reflect the **actual implementation**, not planned functionality.

---

# 16. Phase 12 — Demo Preparation

The team jointly prepares:

```text
assets/screenshots/*
assets/diagrams/*
assets/demo/*
```

The demonstration should show:

1. User enters a situation.
2. ResQ produces an initial action plan.
3. Shelter closes.
4. Plan changes.
5. Road floods.
6. Recommended route changes.
7. Evacuation zone expands.
8. Priorities change.
9. Water center opens.
10. New resource becomes available.

---

# 17. Git Branch Strategy

`main` is the stable branch.

Normal feature work should never be committed directly to `main`.

## Person 1 Branches

```text
feature/backend-foundation
feature/backend-models
feature/emergency-data
feature/ingestion
feature/verification
feature/geographic-engine
feature/recommendation-engine
feature/ai-integration
feature/grounding
feature/simulation
feature/backend-tests
```

## Person 2 Branches

```text
feature/frontend-foundation
feature/situation-form
feature/resource-ui
feature/emergency-map
feature/action-plan
feature/live-feed
feature/source-panel
feature/simulation-ui
feature/frontend-tests
```

## Shared Integration Branches

Temporary integration branches may include:

```text
integration/api-integration
integration/end-to-end
```

These should not become permanent development branches.

---

# 18. Commit Convention

Use concise, descriptive conventional commits.

Examples:

```text
feat(backend): add emergency resource models
feat(data): add Harborview hurricane scenario
feat(verification): add source confidence scoring
feat(geo): add hazard-aware filtering
feat(recommendation): implement shelter ranking
feat(ai): add grounded LLM reasoning
feat(simulation): add shelter closure event
```

Frontend:

```text
feat(frontend): initialize dashboard
feat(situation): add emergency situation form
feat(plan): add prioritized action cards
feat(map): add emergency resource markers
feat(feed): add emergency event feed
feat(sources): add confidence display
feat(simulation): add simulation controls
```

Tests:

```text
test(backend): add recommendation tests
test(geo): add route safety tests
test(frontend): add dashboard tests
```

Documentation:

```text
docs: update API contract
docs: document simulation architecture
```

---

# 19. Pull Requests

Every feature branch should be submitted through a pull request.

A pull request should include:

* clear title
* concise description
* implementation summary
* testing performed
* screenshots for significant UI changes
* documentation changes where applicable
* known limitations

Before requesting review:

```text
[ ] Code builds
[ ] Tests pass
[ ] Lint passes
[ ] No secrets committed
[ ] API contract remains valid
[ ] Documentation updated
[ ] Safety principles preserved
```

---

# 20. Code Review

The other contributor should review every significant pull request.

Reviewers should look for:

### Correctness

Does the implementation actually work?

### Architecture

Does it belong in the correct subsystem?

### Safety

Could the change cause unsupported emergency information to be presented as fact?

### API Compatibility

Does it preserve the shared contract?

### Testing

Are meaningful tests included?

### Maintainability

Is the implementation understandable and appropriately modular?

---

# 21. Frontend Guidelines

Frontend code should:

* use TypeScript types
* use reusable components
* avoid duplicated UI logic
* avoid embedding backend business logic
* handle loading and error states
* remain responsive
* support accessible interactions
* clearly distinguish verified information from generated explanations

The frontend should not implement independent emergency recommendation logic.

---

# 22. Backend Guidelines

Backend code should:

* keep routes thin
* place business logic in services/core modules
* validate inputs
* return structured responses
* use explicit schemas
* keep safety logic deterministic
* test critical recommendation behavior
* avoid embedding secrets
* log meaningful operational errors without exposing sensitive data

---

# 23. AI Contribution Guidelines

AI-related changes require particular care.

Do not:

* allow the model to invent shelters
* allow the model to invent emergency resources
* allow the model to override deterministic safety filtering
* present unsupported model statements as verified facts
* bypass grounding or response validation

Prefer:

```text
Structured Data
      ↓
Deterministic Reasoning
      ↓
Grounded AI
      ↓
Validation
```

---

# 24. Data Contribution Guidelines

New emergency data should:

* follow the relevant JSON schema
* include required identifiers
* include status
* include location information where applicable
* include source metadata
* include timestamps where appropriate
* be validated before use

Fictional data must not be presented as real emergency information.

---

# 25. Security

Never commit:

* API keys
* passwords
* tokens
* private certificates
* credentials
* personal secrets

Use environment variables for local configuration.

The repository includes:

```text
.env.example
```

as the template for environment configuration.

---

# 26. Testing Requirements

At minimum, new backend functionality should include relevant tests.

New frontend functionality should include relevant component, page, or service tests when practical.

Critical emergency logic should always have automated coverage.

Especially important:

* closed resources are filtered
* blocked roads affect routes
* evacuation zones affect recommendations
* accessibility requirements affect results
* confidence is propagated correctly
* simulation events update state
* AI output cannot introduce unsupported emergency facts

---

# 27. Issue Workflow

Issues should follow:

```text
BACKLOG
   ↓
TODO
   ↓
IN PROGRESS
   ↓
REVIEW
   ↓
TESTING
   ↓
DONE
```

Issues should contain:

* title
* description
* assignee
* labels
* milestone
* acceptance criteria

---

# 28. Issue Labels

Backend:

```text
backend
ai
data
simulation
geography
verification
recommendation
api
testing-backend
```

Frontend:

```text
frontend
ux
ui
map
visualization
accessibility
testing-frontend
```

Shared:

```text
documentation
integration
critical
hackathon
demo
deployment
```

---

# 29. Definition of Done

A feature is considered complete when:

```text
[ ] Implementation exists
[ ] Correct subsystem owns the implementation
[ ] Tests pass
[ ] Lint passes
[ ] API contract is preserved
[ ] Documentation is updated when necessary
[ ] No safety rule is violated
[ ] Pull request has been reviewed
[ ] Integration impact has been considered
```

---

# 30. Final Integration Rule

The final system should never be considered complete merely because both contributors' branches work independently.

The project is complete when the entire chain works:

```text
User
 ↓
Situation
 ↓
Backend
 ↓
Verification
 ↓
Geography
 ↓
Recommendation
 ↓
AI
 ↓
Validation
 ↓
Frontend
 ↓
Simulation
 ↓
Changed Emergency State
 ↓
Recalculated Recommendation
 ↓
Updated UI
```

That end-to-end behavior is the ultimate definition of a successful ResQ implementation.

