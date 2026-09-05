# ResQ — Project Status

> **When everything changes, know what to do next.**

This document tracks the implementation status of the ResQ project.

ResQ is an AI-powered emergency resource coordination and decision-support prototype designed to combine verified emergency information, geographic reasoning, deterministic recommendation logic, grounded AI, and dynamic emergency simulation.

---

# 1. Current Status

**Overall Status:** 🟡 In Development

**Project Type:** Hackathon Prototype

**Primary Scenario:** Harborview Hurricane

**Development Model:** Two-person parallel development

**Architecture:** React/TypeScript frontend + Python/FastAPI backend + structured emergency data + simulation engine + grounded AI layer

---

# 2. Project Objective

The objective of ResQ is to demonstrate that rapidly changing emergency information can be transformed into a personalized and prioritized action plan.

The system should allow a user to:

1. Describe their emergency situation.
2. View relevant verified emergency resources.
3. Understand hazards and geographic restrictions.
4. Receive a prioritized action plan.
5. Understand why recommendations were made.
6. See supporting sources and confidence.
7. Observe how recommendations change when emergency conditions change.

---

# 3. Core Architecture Status

| Component                   | Owner    | Status         |
| --------------------------- | -------- | -------------- |
| Repository structure        | Shared   | 🟢 Defined     |
| System architecture         | Shared   | 🟢 Defined     |
| API contract                | Shared   | 🟡 In Progress |
| Frontend architecture       | Person 2 | 🟢 Defined     |
| Backend architecture        | Person 1 | 🟢 Defined     |
| Emergency data architecture | Person 1 | 🟢 Defined     |
| Simulation architecture     | Person 1 | 🟢 Defined     |
| Map architecture            | Shared   | 🟢 Defined     |
| AI architecture             | Person 1 | 🟢 Defined     |
| Testing architecture        | Shared   | 🟢 Defined     |

---

# 4. Development Phases

## Phase 0 — Architecture & Contracts

**Status:** 🟡 In Progress

### Person 1 — Backend

Planned:

```text
backend/app/
data/
simulation/
```

Primary work:

* backend architecture
* domain concepts
* API requirements
* data structures
* simulation concepts

### Person 2 — Frontend

Primary work:

```text
frontend/src/
```

Primary work:

* page architecture
* UI architecture
* user workflow
* component structure
* frontend data requirements

### Shared Deliverables

```text
architecture.md
docs/api-contract.md
PROJECT_STATUS.md
```

### Exit Criteria

```text
[ ] Architecture agreed upon
[ ] API boundary defined
[ ] Situation structure defined
[ ] Recommendation structure defined
[ ] Resource structure defined
[ ] Geographic structure defined
[ ] Simulation events defined
[ ] AI response structure defined
```

---

# 5. Phase 1 — Foundations

**Status:** ⚪ Not Started

### Backend

```text
backend/app/main.py
backend/app/config.py
backend/app/dependencies.py
backend/app/api/routes/health.py
```

Goals:

* FastAPI starts
* health endpoint works
* configuration works
* CORS works
* error handling exists
* logging exists

### Frontend

```text
frontend/src/main.tsx
frontend/src/App.tsx
frontend/src/router.tsx
frontend/src/components/layout/*
frontend/src/components/common/*
```

Goals:

* React starts
* routing works
* application shell exists
* common components exist
* responsive foundation exists

### Intersection

```text
Frontend
   ↕
API conventions
   ↕
Backend
```

### Exit Criteria

```text
[ ] Backend launches
[ ] Frontend launches
[ ] Frontend can reach backend
[ ] Health endpoint works
[ ] Basic error handling works
```

---

# 6. Phase 2 — Models & Situation

**Status:** ⚪ Not Started

### Backend

```text
backend/app/models/*
backend/app/schemas/*
backend/app/services/situation_service.py
backend/app/api/routes/situation.py
```

### Frontend

```text
frontend/src/components/situation/*
frontend/src/pages/Situation.tsx
frontend/src/types/situation.ts
frontend/src/services/situationApi.ts
frontend/src/state/situationStore.ts
frontend/src/hooks/useSituation.ts
```

### Intersection

The frontend situation form must map directly to the backend situation schema.

### Exit Criteria

```text
[ ] Situation model exists
[ ] Situation API exists
[ ] Situation form works
[ ] Request validation works
[ ] Situation can be submitted
[ ] Response is rendered correctly
```

---

# 7. Phase 3 — Emergency Data & Resources

**Status:** ⚪ Not Started

### Backend

```text
data/scenarios/hurricane_harborview/*
data/schemas/*
backend/app/ingestion/*
backend/app/services/resource_service.py
backend/app/services/hazard_service.py
```

### Frontend

```text
frontend/src/components/resources/*
frontend/src/components/hazards/*
frontend/src/types/resource.ts
frontend/src/types/hazard.ts
frontend/src/services/resourceApi.ts
```

### Intersection

Backend resource and hazard structures become frontend display data.

### Exit Criteria

```text
[ ] Harborview scenario loads
[ ] Resources load
[ ] Shelters load
[ ] Hazards load
[ ] Resource statuses display
[ ] Accessibility information displays
[ ] Capacity information displays
```

---

# 8. Phase 4 — Verification & Geography

**Status:** ⚪ Not Started

### Backend

```text
backend/app/services/verification_service.py
backend/app/services/geographic_service.py
backend/app/services/route_service.py
backend/app/core/confidence.py
backend/app/utils/distance.py
```

### Frontend

```text
frontend/src/components/map/*
frontend/src/utils/distance.ts
frontend/src/styles/map.css
```

### Major Intersection

Geographic API contract.

Backend must provide sufficient data for:

```text
User location
Resources
Shelters
Hazards
Roads
Evacuation zones
Routes
```

Frontend must visualize:

```text
User marker
Resource markers
Hazard markers
Road closures
Evacuation zones
Recommended routes
```

### Exit Criteria

```text
[ ] Distance calculation works
[ ] Geographic filtering works
[ ] Hazard constraints work
[ ] Road restrictions work
[ ] Evacuation zones work
[ ] Route data is returned
[ ] Map displays backend geographic state
```

---

# 9. Phase 5 — Recommendation Engine

**Status:** ⚪ Not Started

### Backend

```text
backend/app/core/filtering.py
backend/app/core/scoring.py
backend/app/core/ranking.py
backend/app/services/recommendation_engine.py
backend/app/api/routes/recommendations.py
```

### Frontend

```text
frontend/src/components/plan/*
frontend/src/types/recommendation.ts
frontend/src/services/recommendationApi.ts
frontend/src/hooks/useRecommendations.ts
```

### Intersection

Recommendation API.

### Exit Criteria

```text
[ ] Candidates are discovered
[ ] Unsafe resources are filtered
[ ] Closed resources are filtered
[ ] User needs affect recommendations
[ ] Geographic constraints affect recommendations
[ ] Candidates are scored
[ ] Candidates are ranked
[ ] Action plan renders correctly
```

---

# 10. Phase 6 — AI & Grounding

**Status:** ⚪ Not Started

### Backend

```text
backend/app/services/context_builder.py
backend/app/services/ai_service.py
backend/app/services/response_validator.py
backend/app/services/grounding_service.py
```

### Frontend

```text
frontend/src/components/plan/PlanExplanation.tsx
frontend/src/components/plan/ActionReason.tsx
frontend/src/components/sources/*
frontend/src/types/source.ts
```

### Intersection

Grounded AI response contract.

### Exit Criteria

```text
[ ] Context is constructed from verified data
[ ] AI receives structured context
[ ] AI response is structured
[ ] Response validation works
[ ] Grounding validation works
[ ] Unsupported claims are rejected/fallback handled
[ ] Frontend displays explanations
[ ] Confidence/source information displays
```

---

# 11. Phase 7 — Simulation

**Status:** ⚪ Not Started

### Backend

```text
simulation/*
backend/app/api/routes/simulation.py
backend/app/schemas/simulation.py
```

### Frontend

```text
frontend/src/components/simulation/*
frontend/src/hooks/useSimulation.ts
frontend/src/services/simulationApi.ts
frontend/src/state/simulationStore.ts
frontend/src/types/simulation.ts
```

### Events

```text
CLOSE_SHELTER
FLOOD_ROAD
OPEN_RESOURCE
EXPAND_EVACUATION_ZONE
ADD_HAZARD
RESET
```

### Exit Criteria

```text
[ ] Events execute
[ ] State changes correctly
[ ] Recommendations recalculate
[ ] Map changes
[ ] Action plan changes
[ ] Live state changes
[ ] Reset works
```

---

# 12. Phase 8 — Unified Emergency Dashboard

**Status:** ⚪ Not Started

### Backend

Finalize:

```text
emergency_service.py
emergency.py
```

### Frontend

```text
frontend/src/components/emergency/*
frontend/src/components/feed/*
frontend/src/pages/Dashboard.tsx
frontend/src/pages/LiveFeed.tsx
frontend/src/state/emergencyStore.ts
frontend/src/hooks/useEmergencyState.ts
frontend/src/hooks/usePolling.ts
```

### Exit Criteria

```text
[ ] Emergency status displays
[ ] Risk level displays
[ ] Last-updated information displays
[ ] Live events display
[ ] Dashboard reflects backend state
[ ] Simulation changes appear in dashboard
```

---

# 13. Phase 9 — Full Integration

**Status:** ⚪ Not Started

The mock frontend responses are replaced with real backend responses.

Full flow:

```text
Situation Form
      ↓
Situation API
      ↓
Emergency Intelligence
      ↓
Recommendation Engine
      ↓
AI / Grounding
      ↓
Dashboard
      ↓
Map
      ↓
Simulation
      ↓
State Change
      ↓
Recommendation Recalculation
      ↓
Updated Dashboard
```

### Exit Criteria

```text
[ ] Real frontend/backend communication works
[ ] No critical mock data remains
[ ] API errors are handled
[ ] State synchronization works
[ ] Simulation updates propagate
```

---

# 14. Phase 10 — Testing

**Status:** ⚪ Not Started

### Backend

```text
backend/tests/*
```

### Frontend

```text
frontend/tests/*
```

### Shared

Test:

* API contract
* end-to-end flow
* safety behavior
* simulation behavior
* recommendation changes
* map updates
* AI grounding

### Exit Criteria

```text
[ ] Backend tests pass
[ ] Frontend tests pass
[ ] Integration tests pass
[ ] Critical safety cases pass
[ ] Simulation scenario passes
[ ] No critical regressions
```

---

# 15. Phase 11 — Documentation

**Status:** ⚪ Not Started

Documentation includes:

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

Documentation must describe the implemented system.

---

# 16. Phase 12 — Demo Preparation

**Status:** ⚪ Not Started

Primary demonstration:

## Harborview Hurricane

Sequence:

```text
1. Enter situation
2. Generate initial plan
3. Close shelter
4. Recalculate plan
5. Flood road
6. Recalculate route
7. Expand evacuation zone
8. Recalculate priorities
9. Open water resource
10. Display new resource
```

Required assets:

```text
assets/screenshots/*
assets/diagrams/*
assets/demo/*
```

---

# 17. Phase 13 — Final Submission

**Status:** ⚪ Not Started

Final tasks:

```text
[ ] Final README
[ ] Final architecture documentation
[ ] Final screenshots
[ ] Demo video
[ ] Demo script
[ ] Final testing
[ ] Final linting
[ ] Deployment verification
[ ] Repository cleanup
[ ] GitHub repository review
[ ] Hackathon submission
```

---

# 18. Critical System Requirements

The following are considered non-negotiable.

### Emergency Safety

```text
[ ] AI cannot invent emergency resources
[ ] Closed resources are not recommended
[ ] Blocked roads are not treated as usable
[ ] Geographic hazards affect recommendations
[ ] Evacuation zones affect recommendations
[ ] Uncertainty is surfaced
[ ] Sources are visible where applicable
[ ] Confidence is visible where applicable
```

### Dynamic Behavior

```text
[ ] Emergency state can change
[ ] Simulation events update state
[ ] Recommendations recalculate
[ ] Routes can change
[ ] Map can change
[ ] Dashboard can change
```

### Architecture

```text
[ ] Frontend remains presentation-focused
[ ] Backend owns emergency intelligence
[ ] AI operates on structured context
[ ] API contract remains explicit
[ ] Core logic is testable
```

---

# 19. Definition of MVP Complete

ResQ's MVP is complete when the following scenario works from beginning to end:

```text
User enters:
    Location
    Group size
    Household needs
    Transportation
    Current conditions
    Accessibility requirements

        ↓

Backend processes situation

        ↓

Verified emergency data is evaluated

        ↓

Geographic constraints are evaluated

        ↓

Unsafe/unavailable options are filtered

        ↓

Recommendations are scored and ranked

        ↓

Grounded AI explains the plan

        ↓

Frontend displays:
    Action Plan
    Resources
    Hazards
    Map
    Sources
    Confidence

        ↓

Simulation event occurs

        ↓

Emergency state changes

        ↓

Recommendations recalculate

        ↓

Frontend updates

        ↓

User receives a new prioritized plan
```

---

# 20. Status Legend

```text
🟢 Complete
🟡 In Progress
🔵 Blocked / Waiting
⚪ Not Started
🔴 Needs Major Attention
```

---

# 21. Current Priority

The immediate priority is:

```text
1. Finalize API contract
2. Finalize data structures
3. Complete Phase 0
4. Begin Phase 1 in parallel
5. Maintain synchronized phase progression
6. Integrate only after stable subsystem boundaries exist
```

---

# 22. Project Completion Standard

ResQ should not be considered finished because individual features work in isolation.

The project is complete when the **entire emergency decision loop works**:

> **Situation → Verified Intelligence → Geography → Recommendation → Grounded AI → Action Plan → Emergency Change → Recalculation → Updated Plan**

That loop is the core of the ResQ project.

