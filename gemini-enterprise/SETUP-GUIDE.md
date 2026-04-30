# Gemini Enterprise Setup Guide — Thinking Frameworks

## Agent Architecture

```
┌──────────────────────────────────────────────────────┐
│  Thinking Frameworks (Orchestrator)                  │
│  (Gemini 2.5 Pro)                                    │
│                                                      │
│  Classifies problems via Cynefin, selects frameworks,│
│  enforces information barriers, manages composition  │
│  patterns (composition lives in orchestrator)        │
└───┬────┬─────┬─────┬─────┬─────┬─────┬───────────────┘
    │    │     │     │     │     │     │
    ▼    ▼     ▼     ▼     ▼     ▼     ▼
┌───────┐┌────┐┌──────┐┌─────┐┌─────┐┌─────┐┌──────┐
│Dialec-││Six ││First ││Coll-││Cyne-││Pre- ││Iceb- │
│tical  ││Hats││Prin- ││ision││fin  ││mort-││erg   │
│Engine ││Eng-││ciples││-Zone││Eng- ││em   ││Engine│
│       ││ine ││Engine││Eng. ││ine  ││Eng. ││      │
└───────┘└────┘└──────┘└─────┘└─────┘└─────┘└──────┘
       ← Sub-Agents (all on Gemini 2.5 Pro) →
```

### How the Concepts Map

| Concept | Where It Lives |
|---------|---------------|
| 1. Dialectical | Sub-agent: Dialectical Engine |
| 2. Six Thinking Hats | Sub-agent: Six Thinking Hats Engine |
| 3. First Principles | Sub-agent: First Principles Engine |
| 4. Collision-Zone | Sub-agent: Collision-Zone Engine |
| 5. Cynefin | Sub-agent: Cynefin Engine (also default entry point for ambiguous problems) |
| 6. Pre-mortem | Sub-agent: Pre-mortem Engine |
| 7. Iceberg | Sub-agent: Iceberg Engine |
| 8. Composition Patterns | Orchestrator instructions (chains sub-agents in sequence) |
| 9. Composable Techniques | Orchestrator knowledge file (paste-able prompt snippets) |

## Setup Steps

### Step 1: Create the Parent Agent

Open Gemini Enterprise → Create Agent → Fill in fields from `00-orchestrator.md`:

| Field | Source |
|-------|--------|
| **Name** | `Thinking Frameworks` |
| **Description** | Copy the Description section |
| **Instructions** | Copy the Instructions section (the large block) |
| **Model** | Gemini 2.5 Pro |
| **Connectors** | Add Google Search |
| **Knowledge** | Upload all 8 reference files from `references/` |
| **Starter Prompts** | Add the 5 starter prompts listed |

### Step 2: Create Sub-Agent — Dialectical Engine

Click the `+` button on the parent agent to add a sub-agent → Fill from `01-dialectical-engine.md`:

| Field | Source |
|-------|--------|
| **Name** | `Dialectical Engine` |
| **Description** | Copy the Description section |
| **Instructions** | Copy the Instructions section |
| **Model** | Gemini 2.5 Pro |
| **Connectors** | Add Google Search |
| **Knowledge** | Upload `references/dialectical.md` |
| **Starter Prompts** | Leave empty (sub-agent) |

### Step 3: Create Sub-Agent — Six Thinking Hats Engine

Click `+` on the parent agent → Fill from `02-six-hats-engine.md`:

| Field | Source |
|-------|--------|
| **Name** | `Six Thinking Hats Engine` |
| **Description** | Copy the Description section |
| **Instructions** | Copy the Instructions section |
| **Model** | Gemini 2.5 Pro |
| **Connectors** | Add Google Search |
| **Knowledge** | Upload `references/six-hats.md` |
| **Starter Prompts** | Leave empty (sub-agent) |

### Step 4: Create Sub-Agent — First Principles Engine

Click `+` on the parent agent → Fill from `03-first-principles-engine.md`:

| Field | Source |
|-------|--------|
| **Name** | `First Principles Engine` |
| **Description** | Copy the Description section |
| **Instructions** | Copy the Instructions section |
| **Model** | Gemini 2.5 Pro |
| **Connectors** | Add Google Search |
| **Knowledge** | Upload `references/first-principles.md` |
| **Starter Prompts** | Leave empty (sub-agent) |

### Step 5: Create Sub-Agent — Collision-Zone Engine

Click `+` on the parent agent → Fill from `04-collision-zone-engine.md`:

| Field | Source |
|-------|--------|
| **Name** | `Collision-Zone Engine` |
| **Description** | Copy the Description section |
| **Instructions** | Copy the Instructions section |
| **Model** | Gemini 2.5 Pro |
| **Connectors** | Add Google Search |
| **Knowledge** | Optionally upload `references/composition-patterns.md` |
| **Starter Prompts** | Leave empty (sub-agent) |

### Step 6: Create Sub-Agent — Cynefin Engine

Click `+` on the parent agent → Fill from `05-cynefin-engine.md`:

| Field | Source |
|-------|--------|
| **Name** | `Cynefin Engine` |
| **Description** | Copy the Description section |
| **Instructions** | Copy the Instructions section |
| **Model** | Gemini 2.5 Pro |
| **Connectors** | Add Google Search |
| **Knowledge** | Upload `references/cynefin.md` |
| **Starter Prompts** | Leave empty (sub-agent) |

### Step 7: Create Sub-Agent — Pre-mortem Engine

Click `+` on the parent agent → Fill from `06-pre-mortem-engine.md`:

| Field | Source |
|-------|--------|
| **Name** | `Pre-mortem Engine` |
| **Description** | Copy the Description section |
| **Instructions** | Copy the Instructions section |
| **Model** | Gemini 2.5 Pro |
| **Connectors** | Add Google Search |
| **Knowledge** | Upload `references/pre-mortem.md` |
| **Starter Prompts** | Leave empty (sub-agent) |

### Step 8: Create Sub-Agent — Iceberg Engine

Click `+` on the parent agent → Fill from `07-iceberg-engine.md`:

| Field | Source |
|-------|--------|
| **Name** | `Iceberg Engine` |
| **Description** | Copy the Description section |
| **Instructions** | Copy the Instructions section |
| **Model** | Gemini 2.5 Pro |
| **Connectors** | Add Google Search |
| **Knowledge** | Upload `references/iceberg.md` |
| **Starter Prompts** | Leave empty (sub-agent) |

### Step 9: Verify the Flow

Your agent graph should look like:

```
                  Thinking Frameworks
        /     /      |       |       |     |       \
Dialectical Six Hats First   Coll-   Cyne- Pre-    Iceberg
  Engine    Engine   Princ.  ision   fin   mortem  Engine
                     Engine  -Zone   Eng.  Engine
                             Engine
```

## How It Works at Runtime

1. User asks the **Thinking Frameworks** parent agent a question
2. Orchestrator dispatches to **Cynefin Engine** by default to classify the problem (or short-circuits if the framework is obvious from the user's phrasing)
3. Cynefin returns a domain assignment + routing recommendation
4. Orchestrator dispatches to the appropriate sub-agent(s) with context
5. Sub-agent runs its internal phases (e.g., Thesis → Antithesis → Synthesis; Events → Patterns → Structures → Mental Models; Narrator → parallel personas → Mitigation)
6. Sub-agent returns its analysis to the orchestrator
7. For composition patterns, orchestrator chains multiple sub-agents
8. Orchestrator synthesizes and presents the final recommendation

## Information Barrier Enforcement

Gemini Enterprise handles sub-agent context automatically — each sub-agent only sees what the orchestrator sends it. This naturally enforces information barriers:

- **First Principles Engine** (Architect phase): The orchestrator should send ONLY fundamental truths, not current implementation details
- **Dialectical Engine**: The orchestrator sends the problem; the engine handles internal phase barriers
- **Six Hats Engine**: The engine handles hat sequencing internally
- **Cynefin Engine**: The engine handles its three phases (Classifier → Responder → Synthesizer) internally; no inter-agent barrier needed
- **Pre-mortem Engine** (Narrator phase): The orchestrator should send ONLY the project description and horizon T, NOT the team's success criteria or plan. The engine handles the parallel persona barriers internally.
- **Iceberg Engine**: The engine handles all four layer barriers internally (Patterns analyst sees only events; Structures analyst sees events + patterns; etc.). The orchestrator just sends the surface event(s) and scope.

For composition patterns, the orchestrator controls what flows between sub-agents by only passing synthesis outputs (not raw internals) from one sub-agent to the next. Specifically for Pattern 6 (Cynefin → Iceberg → Dialectical), pass only the *problem framing* from Cynefin to Iceberg, not Cynefin's internal classification reasoning.

## Knowledge Files to Prepare

Before setup, have these files ready to upload:

```
references/
├── dialectical.md           → Upload to Orchestrator + Dialectical Engine
├── six-hats.md              → Upload to Orchestrator + Six Hats Engine
├── first-principles.md      → Upload to Orchestrator + First Principles Engine
├── cynefin.md               → Upload to Orchestrator + Cynefin Engine
├── pre-mortem.md            → Upload to Orchestrator + Pre-mortem Engine
├── iceberg.md               → Upload to Orchestrator + Iceberg Engine
├── composable-techniques.md → Upload to Orchestrator only (cross-cutting snippets)
└── composition-patterns.md  → Upload to Orchestrator only
```
