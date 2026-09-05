# ResQ

## AI-Powered Emergency Resource Coordination & Decision Support

> **When everything changes, know what to do next.**

ResQ is an AI-powered emergency decision-support platform designed to transform fragmented and rapidly changing emergency information into clear, prioritized, and personalized action plans.

During hurricanes, floods, wildfires, earthquakes, severe storms, and other emergencies, people may need to make critical decisions while information about shelters, roads, hazards, evacuation zones, medical resources, food, water, charging stations, and other services is constantly changing.

ResQ addresses this problem by combining:

* **Verified structured emergency data**
* **Geographic reasoning**
* **Safety and verification logic**
* **Personalized recommendation ranking**
* **Grounded LLM reasoning**
* **Dynamic emergency simulation**
* **Real-time-style emergency state updates**
* **Explainable recommendations**
* **Interactive geographic visualization**

The central idea behind ResQ is simple:

> **Don't ask AI to invent emergency information. Give it verified structured information and let it reason over the situation.**

ResQ is designed as a **hackathon prototype and decision-support demonstration**. It is not an official emergency service, emergency dispatch system, or replacement for government alerts, emergency responders, or professional medical assistance.

---

# 1. The Problem

During an emergency, information is often fragmented across many different sources.

A person may need to answer questions such as:

* Where should I go?
* Which shelter is actually open?
* Can my family safely reach it?
* Is the road there blocked?
* Is the shelter accessible?
* Is the shelter inside an evacuation zone?
* Where can I get water?
* Where can I charge my phone?
* Has the situation changed?
* What should I do first?
* What should I avoid?

Traditional search interfaces can provide individual pieces of information, but they generally do not transform those pieces into a **personalized, continuously updated action plan**.

The challenge becomes even harder when conditions change.

A shelter can close.

A road can flood.

An evacuation zone can expand.

A new resource can open.

A previously safe route can become unusable.

The user therefore needs more than information.

They need to know:

> **What should I do next, given everything that is currently known?**

---

# 2. The ResQ Solution

ResQ combines deterministic emergency intelligence with grounded AI reasoning.

The system accepts a user's situation, evaluates verified emergency information, performs geographic and safety analysis, ranks viable options, and produces an explainable action plan.

At a high level:

```text
User Situation
      |
      v
Verified Emergency Data
      |
      v
Verification & Safety Filtering
      |
      v
Geographic Reasoning
      |
      v
Recommendation Engine
      |
      v
Grounded AI Reasoning
      |
      v
Prioritized Action Plan
      |
      v
Interactive Dashboard
```

When emergency conditions change, ResQ recalculates the relevant state and produces a new plan.

```text
Emergency Event
      |
      v
Simulation / State Update
      |
      v
Emergency Intelligence
      |
      v
Recommendation Recalculation
      |
      v
Updated Action Plan
      |
      v
Updated Map + Dashboard
```

---

# 3. Core Concept

ResQ separates emergency intelligence from AI-generated explanation.

## Emergency Intelligence Engine

The deterministic backend is responsible for:

* emergency facts
* resource status
* shelter availability
* verification
* source reliability
* freshness
* geographic reasoning
* hazard detection
* evacuation-zone checks
* road restrictions
* route eligibility
* recommendation filtering
* scoring
* ranking
* simulation state

## AI Engine

The AI layer is responsible for:

* explaining recommendations
* communicating priorities
* summarizing relevant information
* turning structured results into understandable guidance

The AI layer does **not** serve as the authoritative source of emergency facts.

```text
              RESQ
                |
        +-------+-------+
        |               |
        v               v
Emergency           AI Engine
Intelligence
Engine                 |
        |              |
        |        Explanation
        |        Communication
        |
 Facts
 Safety
 Geography
 Verification
 Ranking
 Simulation
```

This separation is one of the most important architectural principles in ResQ.

---

# 4. Key Features

## Personalized Emergency Situations

Users can provide information such as:

* location
* group size
* children
* elderly people
* accessibility requirements
* transportation
* power outage
* flooding
* injury
* medical needs

ResQ uses this information when determining appropriate recommendations.

---

## Prioritized Action Plans

Instead of simply displaying a list of resources, ResQ generates a prioritized plan.

Example:

```text
1. GO TO SHELTER A
   Highest Priority
   Verified open
   Accessible
   2.4 miles away

2. GET WATER
   Medium Priority
   Water Center B
   1.1 miles away

3. AVOID ROAD C
   High Urgency
   Flooding reported
```

Each recommendation can include:

* priority
* urgency
* reason
* resource
* distance
* status
* confidence
* source
* timestamp

---

## Geographic Emergency Intelligence

The interactive map can display:

* user location
* shelters
* emergency resources
* hazards
* road closures
* evacuation zones
* recommended routes

Geographic information is supplied by the backend rather than independently invented by the frontend.

---

## Verification & Confidence

ResQ tracks information such as:

* source
* verification status
* freshness
* confidence
* timestamp

The system is designed to make uncertainty visible rather than hiding it.

---

## Grounded AI

The LLM receives structured information produced by the emergency intelligence engine.

AI-generated explanations are validated against the available context.

Conceptually:

```text
AI Statement
     |
     v
Supported by Verified Context?
     |
   +---+---+
   |       |
  YES      NO
   |       |
Accept    Reject
```

---

## Dynamic Emergency Simulation

ResQ includes a simulation system for demonstrating changing emergency conditions.

Supported events include:

* `CLOSE_SHELTER`
* `FLOOD_ROAD`
* `OPEN_RESOURCE`
* `EXPAND_EVACUATION_ZONE`
* `ADD_HAZARD`
* `RESET`

Example:

```text
Initial State
     |
     v
Shelter A = OPEN
Road A = OPEN
     |
     v
CLOSE_SHELTER
     |
     v
Shelter A = CLOSED
     |
     v
Recommendation Engine
recalculates
     |
     v
Shelter B becomes
highest priority
```

This demonstrates ResQ's central capability:

> **When the world changes, the recommended plan changes with it.**

---

# 5. Demonstration Scenario

The primary demonstration uses a fictional emergency scenario:

## Harborview Hurricane

The initial environment contains:

* open shelters
* available emergency resources
* active hazards
* open roads
* evacuation zones
* verified sources

The demonstration then introduces a sequence of emergency events.

```text
Harborview Hurricane
        |
        v
User enters situation
        |
        v
Initial Action Plan
        |
        v
Shelter closes
        |
        v
Plan recalculates
        |
        v
Road floods
        |
        v
Recommended route changes
        |
        v
Evacuation zone expands
        |
        v
Priorities change
        |
        v
Water center opens
        |
        v
New resource becomes available
```

The simulation is deterministic and designed to make the system's reasoning visible during a hackathon demonstration.

---

# 6. Technology Stack

## Frontend

* React
* TypeScript
* Vite
* CSS
* Interactive mapping components

## Backend

* Python
* FastAPI
* Pydantic-style schemas
* Pytest

## AI

* Grounded LLM reasoning
* Structured AI responses
* Response validation
* Grounding verification

## Data

* JSON-based emergency scenario data
* Structured resource data
* Hazard data
* Road data
* Evacuation-zone data
* Source metadata

## Development

* Git
* GitHub
* VS Code
* npm
* Python virtual environments

---

# 7. Repository Structure

```text
resq/
│
├── .github/
│   ├── workflows/
│   │   ├── tests.yml
│   │   └── lint.yml
│   │
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   ├── feature_request.md
│   │   └── task.md
│   │
│   └── pull_request_template.md
│
├── frontend/
│   ├── public/
│   ├── src/
│   └── tests/
│
├── backend/
│   ├── app/
│   └── tests/
│
├── data/
│   ├── scenarios/
│   └── schemas/
│
├── simulation/
│
├── docs/
│
├── scripts/
│
├── assets/
│   ├── screenshots/
│   ├── diagrams/
│   └── demo/
│
├── .env.example
├── .gitignore
├── LICENSE
├── README.md
├── CONTRIBUTING.md
├── PROJECT_STATUS.md
├── pyproject.toml
└── docker-compose.yml
```

For the complete file-level architecture, see:

`docs/architecture.md`

---

# 8. System Architecture

At the highest level:

```text
                    RESQ
                      |
          +-----------+-----------+
          |                       |
          v                       v
      FRONTEND                 BACKEND
          |                       |
          |                 +-----+------+
          |                 |            |
          |                 v            v
          |            Emergency      AI Engine
          |            Intelligence
          |                 |
          |       +---------+---------+
          |       |         |         |
          |       v         v         v
          |   Verification Geography Recommendations
          |                           |
          |                           v
          |                      Action Plan
          |                           |
          +---------------------------+
                      |
                      v
                 Dashboard
```

For detailed architecture, see:

`docs/architecture.md`

---

# 9. Data Flow

```text
User
 |
 | Situation
 v
Frontend
 |
 | HTTP Request
 v
FastAPI
 |
 v
Situation Service
 |
 v
Emergency Intelligence
 |
 +--> Data Ingestion
 |
 +--> Verification
 |
 +--> Geographic Reasoning
 |
 +--> Safety Filtering
 |
 +--> Recommendation Engine
 |
 v
Grounded AI
 |
 v
Validated Response
 |
 v
Frontend
 |
 +--> Action Plan
 +--> Map
 +--> Resources
 +--> Hazards
 +--> Live Feed
 +--> Sources
```

---

# 10. Safety Principles

ResQ is designed around several safety principles.

### 1. Never invent emergency resources

The AI cannot create shelters, hospitals, roads, resources, or emergency alerts.

### 2. Never recommend known closed resources

Closed or unavailable resources are filtered before recommendation.

### 3. Never treat blocked routes as usable

Known road restrictions must influence geographic reasoning.

### 4. Account for evacuation zones

Resources or routes affected by evacuation conditions must be evaluated accordingly.

### 5. Make uncertainty visible

ResQ should surface confidence, verification, timestamps, and uncertainty where applicable.

### 6. Keep emergency facts deterministic

Critical emergency facts should come from structured system data rather than unconstrained AI generation.

### 7. Follow official emergency instructions

In real emergencies, users should follow official emergency alerts, local authorities, emergency responders, and professional medical guidance.

---

# 11. Prototype Data Disclaimer

The Harborview emergency scenario is fictional and uses simulated data for demonstration purposes.

The prototype does not claim to provide authoritative live emergency information.

A future production implementation could support real emergency feeds and authoritative data sources through the ingestion layer, but such integrations are outside the scope of this prototype unless explicitly implemented.

---

# 12. Development Model

ResQ is designed for parallel two-person development.

## Person 1 — Backend / Emergency Intelligence

Owns:

```text
backend/
data/
simulation/
```

Primary responsibilities:

* FastAPI
* domain models
* data ingestion
* verification
* geography
* recommendation engine
* AI
* grounding
* simulation
* backend tests

---

## Person 2 — Frontend / UX / Visualization

Owns:

```text
frontend/
assets/
```

Primary responsibilities:

* React
* UI
* situation interface
* dashboard
* action plan
* resources
* hazards
* map
* live feed
* sources
* simulation controls
* frontend tests

---

## Shared

Both contributors work together on:

```text
docs/architecture.md
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
```

Development follows:

```text
Shared Contract
       |
       +-------------------+
       |                   |
       v                   v
   Backend             Frontend
       |                   |
   Real Logic           Mock Data
       |                   |
       +---------+---------+
                 |
                 v
             Integration
                 |
                 v
            Joint Testing
                 |
                 v
             Final Demo
```

---

# 13. Development Phases

ResQ is developed in parallel phases.

| Phase | Backend                  | Frontend               | Intersection          |
| ----- | ------------------------ | ---------------------- | --------------------- |
| 0     | Architecture & contracts | UX architecture        | API contract          |
| 1     | FastAPI foundation       | React foundation       | API conventions       |
| 2     | Models & schemas         | Situation interface    | Situation schema      |
| 3     | Emergency data           | Resource/hazard UI     | Emergency data        |
| 4     | Verification & geography | Emergency map          | Geographic API        |
| 5     | Recommendation engine    | Action plan            | Recommendation schema |
| 6     | AI & grounding           | AI explanation UI      | Grounded AI response  |
| 7     | Simulation engine        | Simulation controls    | Simulation API        |
| 8     | Emergency state          | Dashboard & feed       | Unified state         |
| 9     | API integration          | API integration        | Full system           |
| 10    | Backend testing          | Frontend testing       | Joint testing         |
| 11    | Backend documentation    | Frontend documentation | System documentation  |
| 12    | Demo infrastructure      | Visual assets          | Final presentation    |
| 13    | Final backend polish     | Final UX polish        | Submission            |

The two contributors work on the same phase number simultaneously.

---

# 14. Testing

Backend tests cover:

* API behavior
* emergency services
* recommendations
* verification
* geographic reasoning
* resources
* hazards
* routes
* AI
* grounding
* response validation
* ingestion
* simulation

Frontend tests cover:

* situation forms
* action plans
* resource cards
* maps
* pages
* API services

Testing also includes end-to-end scenarios where emergency conditions change.

---

# 15. Example End-to-End Workflow

```text
1. User opens ResQ
        ↓
2. User enters emergency situation
        ↓
3. Backend validates situation
        ↓
4. Emergency data is loaded
        ↓
5. Resources are verified
        ↓
6. Geographic constraints are evaluated
        ↓
7. Unsafe/unavailable candidates are filtered
        ↓
8. Remaining candidates are scored
        ↓
9. Action plan is generated
        ↓
10. AI explains the plan using grounded context
        ↓
11. Frontend displays:
        - priorities
        - resources
        - hazards
        - map
        - sources
        ↓
12. Emergency event occurs
        ↓
13. State changes
        ↓
14. Recommendation engine recalculates
        ↓
15. Dashboard updates
```

---

# 16. Running the Project

## Backend

Create a Python environment and install dependencies:

```bash
cd backend

python -m venv .venv
```

Activate the environment.

### Windows PowerShell

```powershell
.\.venv\Scripts\Activate.ps1
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Run the backend:

```bash
python -m uvicorn app.main:app --reload
```

---

## Frontend

```bash
cd frontend
npm install
npm run dev
```

---

## Tests

Backend:

```bash
cd backend
pytest
```

Frontend:

```bash
cd frontend
npm test
```

---

# 17. Environment Variables

Copy:

```text
.env.example
```

to an appropriate local environment configuration.

Never commit secrets, API keys, credentials, or private configuration to the repository.

---

# 18. Project Status

ResQ is a hackathon prototype focused on demonstrating:

* emergency decision support
* deterministic emergency intelligence
* geographic reasoning
* grounded AI
* explainable recommendations
* dynamic simulation
* human-centered emergency UX

The project intentionally prioritizes a strong, demonstrable architecture over pretending to be a production emergency-response platform.

---

# 19. Future Development

Potential future improvements include:

* authoritative live emergency feeds
* government alert integrations
* real-time weather data
* real routing providers
* real geographic datasets
* emergency-services integrations
* multilingual support
* offline capabilities
* mobile applications
* accessibility improvements
* stronger uncertainty modeling
* real-time notifications
* production-grade authentication and security
* large-scale infrastructure
* historical emergency analytics

These features are considered future work unless explicitly implemented.

---

# 20. Contributing

Contributions should follow the repository's development workflow.

Before submitting a pull request:

1. Create a feature branch.
2. Make focused changes.
3. Run relevant tests.
4. Run linting and formatting.
5. Update documentation when necessary.
6. Open a pull request.
7. Request review.
8. Resolve review comments.
9. Verify the final implementation.
10. Merge only after required checks pass.

See:

`CONTRIBUTING.md`

---

# 21. License

ResQ is released under the MIT License.

See:

`LICENSE`

---

# 22. Final Vision

ResQ is built around one fundamental idea:

> **Emergency information is only useful if people can understand what it means for them and what they should do next.**

Rather than asking an AI system to generate emergency facts, ResQ provides a structured, verified emergency environment and uses AI to reason over that information responsibly.

The result is a system that connects:

```text
Emergency Data
      +
Verification
      +
Geography
      +
Personal Context
      +
Recommendation Logic
      +
Grounded AI
      +
Dynamic Simulation
      =
Actionable Emergency Decision Support
```

**ResQ — When everything changes, know what to do next.**

