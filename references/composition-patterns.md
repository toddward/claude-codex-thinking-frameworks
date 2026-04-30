# Thinking Framework Composition Patterns

## What This Is

Composition patterns are **predefined multi-framework orchestration sequences** that chain
thinking frameworks together. Each pattern defines: what frameworks run, in what order,
what data flows between them, and where information is intentionally blocked.

A single framework is a tool. A composition pattern is a methodology.

---

## Pattern Anatomy

Every composition pattern follows this structure:

```
PATTERN: [Name]
WHEN TO USE: [Situation trigger]
FRAMEWORKS: [Ordered list]
AGENT CHAIN: [Which agents from which frameworks, in sequence]
DATA FLOW: [What each agent receives and produces]
INFORMATION BARRIERS: [What is intentionally hidden from which agents]
OUTPUT: [Final deliverable]
ESTIMATED CYCLES: [How many total agent calls]
```

---

## Pattern 1: Decompose → Debate → Decide

### Metadata
| Field | Value |
|-------|-------|
| Frameworks | First Principles → Dialectical → Six Hats |
| Total Agents | 9 (3 + 3 + 3 selected hats) |
| Estimated Calls | 7-9 sequential |
| Complexity | High |

### When to Use
- Legacy system modernization decisions
- "Should we keep X or replace it with Y?"
- Any decision where inherited assumptions cloud judgment
- Architecture pivots with high reversal cost

### Agent Chain

```
PHASE 1: DECOMPOSE (First Principles)
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  [Current System + Requirements]                         │
│         │                                                │
│         ▼                                                │
│  ┌─────────────┐                                         │
│  │ Archaeologist│ → Fundamental Truths + Assumption Map   │
│  └──────┬──────┘                                         │
│         │ truths only (no current implementation)         │
│         ▼                                                │
│  ┌─────────────┐                                         │
│  │  Architect   │ → Clean-Slate Reconstruction           │
│  └──────┬──────┘                                         │
│         │ reconstruction + original                       │
│         ▼                                                │
│  ┌─────────────┐                                         │
│  │  Evaluator   │ → Delta Analysis + Candidates          │
│  └─────────────┘                                         │
│                                                          │
└──────────────────────────────────────────────────────────┘
          │
          │ Evaluator output: top 2 competing approaches
          ▼
PHASE 2: DEBATE (Dialectical)
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  ┌─────────────┐                                         │
│  │  Advocate    │ → Thesis: Best candidate approach      │
│  └──────┬──────┘                                         │
│         │                                                │
│         ▼                                                │
│  ┌─────────────┐                                         │
│  │  Challenger  │ → Antithesis: Why alternative is better│
│  └──────┬──────┘                                         │
│         │                                                │
│         ▼                                                │
│  ┌─────────────┐                                         │
│  │  Integrator  │ → Synthesis: Transcendent approach     │
│  └─────────────┘                                         │
│                                                          │
└──────────────────────────────────────────────────────────┘
          │
          │ Synthesis document
          ▼
PHASE 3: DECIDE (Six Hats — abbreviated)
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  ┌─────────────┐                                         │
│  │  ⬛ Black    │ → Risk assessment of synthesis         │
│  └──────┬──────┘                                         │
│         │                                                │
│         ▼                                                │
│  ┌─────────────┐                                         │
│  │  🟡 Yellow   │ → Benefit validation of synthesis      │
│  └──────┬──────┘                                         │
│         │                                                │
│         ▼                                                │
│  ┌─────────────┐                                         │
│  │  🔴 Red      │ → Gut check: will the org accept this? │
│  └─────────────┘                                         │
│                                                          │
└──────────────────────────────────────────────────────────┘
          │
          ▼
    FINAL OUTPUT: Grounded recommendation with risk/benefit
    analysis and organizational readiness assessment
```

### Data Flow Rules

| Agent | Receives | Produces | Cannot See |
|-------|----------|----------|------------|
| Archaeologist | Current system docs, requirements | Fundamental truths, assumption map | — |
| Architect | Fundamental truths ONLY | Clean-slate reconstruction | Current implementation |
| Evaluator | Original + reconstruction + truths | Delta analysis, top 2 candidates | — |
| Advocate | Evaluator's top candidate | Thesis document | — |
| Challenger | Thesis + Evaluator's alternative | Antithesis document | — |
| Integrator | Thesis + antithesis | Synthesis | — |
| Black Hat | Synthesis | Risk assessment | Yellow/Red outputs |
| Yellow Hat | Synthesis + Black Hat risks | Benefit analysis (addressing risks) | Red output |
| Red Hat | Synthesis + Black + Yellow | Gut check, stakeholder sentiment | — |

### Information Barriers (Critical)

1. **Architect ↛ Current Implementation** — Prevents anchoring bias
2. **Black/Yellow/Red run sequentially** — Each builds on the previous, not in parallel
3. **Phase 2 agents don't see Phase 1 internals** — They work from the Evaluator's summary, not the raw decomposition

### Example Application

**Problem:** "Should we migrate our core workloads from traditional VMs to a container platform?"

- **Phase 1:** Archaeologist strips to fundamentals (workload isolation, encryption requirements, audit trails, 99.99% uptime). Architect designs from those truths alone. Evaluator compares.
- **Phase 2:** Advocate argues for the Architect's design. Challenger argues for an evolved VM approach. Integrator finds the higher ground.
- **Phase 3:** Black Hat finds migration risk. Yellow Hat quantifies operational savings. Red Hat reads the room on team readiness.

### Composable Techniques (Optional Augmenters)

- **Chesterton's Fence at the Architect step**: before the Architect omits a
  component the original VM design includes, fire the Chesterton gate to
  reconstruct the original justification. Prevents the reconstruction from
  removing load-bearing structures whose purpose is non-obvious.
- **Steel-manning at the Advocate step**: forces the Advocate to defend
  against the strongest reading of the alternative, not the weakest. See
  `references/composable-techniques.md`.

---

## Pattern 2: Collide → Ground → Validate

### Metadata
| Field | Value |
|-------|-------|
| Frameworks | Collision-Zone → First Principles → Six Hats |
| Total Agents | 5-8 |
| Estimated Calls | 5-8 sequential |
| Complexity | Medium-High |

### When to Use
- Innovation needed under hard constraints
- "We need a breakthrough, not an improvement"
- Stuck problems where conventional thinking has been exhausted
- R&D exploration within hard constraints (regulatory, technical, budgetary)

### Agent Chain

```
PHASE 1: COLLIDE (Collision-Zone)
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  [Problem Statement + 2 Unrelated Domains]               │
│         │                                                │
│         ▼                                                │
│  ┌─────────────┐                                         │
│  │  Collider    │ → 3-5 forced metaphor combinations     │
│  └──────┬──────┘                                         │
│         │                                                │
│         ▼                                                │
│  ┌─────────────┐                                         │
│  │  Extractor   │ → Actionable concepts from each        │
│  └─────────────┘     collision (ranked by novelty)       │
│                                                          │
└──────────────────────────────────────────────────────────┘
          │
          │ Top 2 novel concepts
          ▼
PHASE 2: GROUND (First Principles — partial)
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  ┌─────────────┐                                         │
│  │ Archaeologist│ → Does the concept survive              │
│  └──────┬──────┘   decomposition to fundamentals?        │
│         │                                                │
│         ▼                                                │
│  ┌─────────────┐                                         │
│  │  Architect   │ → Rebuild the concept using only truths │
│  └─────────────┘                                         │
│                                                          │
└──────────────────────────────────────────────────────────┘
          │
          │ Grounded concept(s) that survived
          ▼
PHASE 3: VALIDATE (Six Hats — full)
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  Blue → White → Green → Yellow → Black → Red → Blue      │
│                                                          │
│  Full six-hat analysis of the grounded concept           │
│                                                          │
└──────────────────────────────────────────────────────────┘
          │
          ▼
    FINAL OUTPUT: Innovative solution validated from all
    perspectives with implementation roadmap
```

### Data Flow Rules

| Agent | Receives | Produces | Cannot See |
|-------|----------|----------|------------|
| Collider | Problem + 2 source domains | Forced metaphor combinations | Constraints (intentionally) |
| Extractor | Collider output + problem constraints | Ranked actionable concepts | — |
| Archaeologist | Top concept + domain constraints | Fundamental truth check | — |
| Architect | Truths + concept essence | Grounded implementation design | Current approach |
| Six Hats (all) | Grounded design | Full perspective analysis | Phase 1 raw collisions |

### Information Barriers (Critical)

1. **Collider ↛ Constraints** — The collision phase must be unconstrained; adding constraints kills novelty. Constraints enter at the Extractor stage.
2. **Six Hats ↛ Raw Collisions** — The hats evaluate the grounded version, not the raw creative output. This prevents premature dismissal.

### Composable Techniques (Optional Augmenters)

- **Chesterton's Fence at the Archaeologist step**: when grounding a novel
  collision against current state, fire the gate before declaring any existing
  structure obsolete. The collision may be discarding something whose original
  purpose is not yet reconstructed.
- **Inversion at the Collider step**: invert "what novel solution emerges?" to
  "what novel failure mode emerges?" — both are valid creative outputs and
  they often surface from the same collision.

---

## Pattern 3: Assess → Explore → Commit

### Metadata
| Field | Value |
|-------|-------|
| Frameworks | Six Hats → Dialectical → Dialectical (recursive) |
| Total Agents | 10 (7 + 3, optionally +3) |
| Estimated Calls | 7-13 sequential |
| Complexity | High |

### When to Use
- Complex decisions with multiple stakeholders and competing priorities
- Situations needing both breadth (all angles) and depth (adversarial rigor)
- Go/no-go gates on major initiatives
- Cross-functional decisions where different teams see different risks

### Agent Chain

```
PHASE 1: ASSESS (Six Hats — full)
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  Blue → White → Green → Yellow → Black → Red → Blue      │
│                                                          │
│  Blue Hat identifies the TOP TENSION:                    │
│  the biggest conflict between Black Hat risks            │
│  and Yellow Hat benefits                                 │
│                                                          │
└──────────────────────────────────────────────────────────┘
          │
          │ Top tension statement + all hat outputs
          ▼
PHASE 2: EXPLORE (Dialectical — on the top tension)
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  Advocate: Argues the benefit side of the tension        │
│  Challenger: Argues the risk side of the tension         │
│  Integrator: Resolves the tension                        │
│                                                          │
└──────────────────────────────────────────────────────────┘
          │
          │ If Integrator flags remaining tensions → recurse
          ▼
PHASE 3: COMMIT (Dialectical — second cycle, optional)
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  The synthesis becomes the new thesis                    │
│  Advocate: Defends the synthesis                         │
│  Challenger: Finds remaining weaknesses                  │
│  Integrator: Final resolution                            │
│                                                          │
└──────────────────────────────────────────────────────────┘
          │
          ▼
    FINAL OUTPUT: Decision with comprehensive analysis
    (breadth from Hats) and adversarial rigor (depth from
    Dialectical), tested to convergence
```

### Recursion Rules

- Phase 3 triggers ONLY if the Phase 2 Integrator flags "significant remaining tensions"
- Maximum 2 dialectical cycles — if it hasn't converged, the problem needs decomposition (switch to First Principles)
- If Phase 2 converges cleanly, skip Phase 3

---

## Pattern 4: Triage → Route → Execute

### Metadata
| Field | Value |
|-------|-------|
| Frameworks | Cynefin Classification → [Selected Framework] |
| Total Agents | 1 + varies |
| Estimated Calls | 1 + varies |
| Complexity | Meta-pattern |

### When to Use
- You're not sure WHICH framework to use
- The problem type is ambiguous
- You want automated framework selection

### Agent Chain

```
PHASE 1: TRIAGE (Cynefin Classifier)
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  ┌──────────────┐                                        │
│  │  Classifier   │ → Problem domain classification       │
│  └──────┬───────┘                                        │
│         │                                                │
│         ├── CLEAR (obvious cause-effect)                  │
│         │   → Skip frameworks, just execute best practice │
│         │                                                │
│         ├── COMPLICATED (expert analysis needed)          │
│         │   → Route to Six Hats or Dialectical           │
│         │                                                │
│         ├── COMPLEX (emergent, unpredictable)             │
│         │   → Route to Collision-Zone → First Principles │
│         │                                                │
│         ├── CHAOTIC (no cause-effect, act first)          │
│         │   → Route to abbreviated Dialectical (fast)    │
│         │                                                │
│         └── CONFUSED (don't know the domain yet)          │
│             → Route to First Principles (decompose first)│
│                                                          │
└──────────────────────────────────────────────────────────┘
          │
          ▼
PHASE 2: EXECUTE (Selected framework or composition pattern)
```

### Classifier Agent Prompt

The Cynefin classifier is now a first-class framework with its own three-phase
chain (Classifier → Domain Responder → Routing Synthesizer). For the full agent
prompts, output templates, and worked examples, see **`references/cynefin.md`**.

This pattern uses Cynefin only at its triage role — the Classifier and Routing
Synthesizer phases. The Domain Responder is short-circuited because the
*composition* concern (which framework to invoke) is what this pattern is for.

When dispatching the Cynefin classifier inside this pattern:
1. Pass the problem statement to the Classifier (see `references/cynefin.md`)
2. Use the resulting domain assignment to look up the routing rule in the table
   above
3. Pass the problem (NOT the Classifier's internal reasoning) to the routed
   framework

For problems where you need the full Cynefin chain — including the Domain
Responder's domain-native response and the Routing Synthesizer's contextualized
recommendation — invoke `references/cynefin.md` directly rather than this
abbreviated composition pattern.

---

## Pattern 5: Parallel Perspectives → Convergence

### Metadata
| Field | Value |
|-------|-------|
| Frameworks | Dialectical (×N parallel) → Six Hats (synthesis) |
| Total Agents | 3N + 3 |
| Estimated Calls | 3 parallel tracks + 3 sequential |
| Complexity | High (but parallelizable) |

### When to Use
- Multi-vendor evaluation
- Comparing 3+ architectural approaches
- Any situation with more than 2 competing options

### Agent Chain

```
PHASE 1: PARALLEL DIALECTICAL (one per option)
┌─────────────┐  ┌─────────────┐  ┌─────────────┐
│ Option A     │  │ Option B     │  │ Option C     │
│              │  │              │  │              │
│ Advocate     │  │ Advocate     │  │ Advocate     │
│ Challenger   │  │ Challenger   │  │ Challenger   │
│ Integrator   │  │ Integrator   │  │ Integrator   │
│              │  │              │  │              │
│ → Synthesis A│  │ → Synthesis B│  │ → Synthesis C│
└──────┬───────┘  └──────┬───────┘  └──────┬───────┘
       │                 │                 │
       └────────────┬────┘────────────┬────┘
                    │                 │
                    ▼                 ▼
PHASE 2: COMPARATIVE SIX HATS
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  ⚪ White: Compare factual merits of each synthesis      │
│  ⬛ Black: Unique risks of each that survived dialectical│
│  🟡 Yellow: Unique strengths of each                     │
│                                                          │
│  🔵 Blue: Final ranking + recommendation                 │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

### Key Advantage
Each option gets EQUAL adversarial treatment before comparison. This prevents the
common failure mode where Option A gets scrutinized while Option B gets a pass because
it was proposed second.

---

## Pattern 6: Triage → Diagnose → Decide

### Metadata
| Field | Value |
|-------|-------|
| Frameworks | Cynefin → Iceberg → Dialectical |
| Total Agents | 9 (3 + 4 + 3) |
| Estimated Calls | 9 sequential (some Iceberg parallelization possible) |
| Complexity | High |

### When to Use

- Ambiguous problems where the problem *type* is itself unclear
- Recurring surface symptoms suspected to have systemic causes
- "Why does this keep happening?" decisions where a binary choice falls out at
  the end of diagnosis ("intervene at structure A vs structure B")
- Post-incident reviews that need to escape the "improve testing" anti-pattern

### Agent Chain

```
PHASE 1: TRIAGE (Cynefin — abbreviated)
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  ┌──────────────┐                                        │
│  │ 🧭 Classifier│ → Domain assignment + signals          │
│  └──────┬───────┘                                        │
│         │                                                │
│         │ If CLEAR or CHAOTIC: exit pattern              │
│         │   - Clear → apply best practice (no diagnose)  │
│         │   - Chaotic → stabilize, then re-classify      │
│         │                                                │
│         │ If COMPLICATED, COMPLEX, or CONFUSED: continue │
│         ▼                                                │
│  ┌──────────────┐                                        │
│  │ 🧩 Synthesizer│ → "Diagnose at the structures level"  │
│  └──────────────┘                                        │
│                                                          │
└──────────────────────────────────────────────────────────┘
          │
          │ Problem framing + scope (NOT Cynefin's internal reasoning)
          ▼
PHASE 2: DIAGNOSE (Iceberg — full four layers)
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  🌊 Events → 🌀 Patterns → 🏛️ Structures → 🧠 Models    │
│                                                          │
│  Each layer barrier-enforced (see references/iceberg.md) │
│                                                          │
└──────────────────────────────────────────────────────────┘
          │
          │ Top 1-2 structure-level intervention candidates
          ▼
PHASE 3: DECIDE (Dialectical — on the intervention choice)
┌──────────────────────────────────────────────────────────┐
│                                                          │
│  Advocate: Argues for Intervention A                     │
│  Challenger: Argues for Intervention B                   │
│  Integrator: Synthesizes — often "do both, in this order"│
│                                                          │
└──────────────────────────────────────────────────────────┘
          │
          ▼
    FINAL OUTPUT: Classified problem, structure-level diagnosis,
    chosen intervention with rationale and sequencing
```

### Data Flow Rules

| Agent | Receives | Produces | Cannot See |
|-------|----------|----------|------------|
| Cynefin Classifier | Problem statement | Domain + signals | — |
| Cynefin Synthesizer | Classifier output + problem | Routing recommendation | — |
| Iceberg Events Analyst | Problem framing + scope | Event roster | Cynefin internal reasoning |
| Iceberg Patterns Analyst | Event roster | Patterns | Structures or mental models |
| Iceberg Structures Analyst | Events + patterns | Structures + mechanisms | Mental-model hypotheses |
| Iceberg Mental Models Analyst | Events + patterns + structures | Testable beliefs + falsification tests | Prior runs' mental models |
| Advocate | Top intervention candidate (from Iceberg) | Thesis | Other intervention's case |
| Challenger | Thesis + alternative intervention | Antithesis | Integrator output |
| Integrator | Thesis + antithesis | Synthesis | — |

### Information Barriers (Critical)

1. **Cynefin → Iceberg**: only the *problem framing and scope* carry forward.
   The Classifier's internal reasoning does NOT enter Iceberg, because Iceberg
   re-derives its own signals from events.
2. **Iceberg layer barriers** stay enforced inside Phase 2 — see
   `references/iceberg.md`.
3. **Iceberg → Dialectical**: the Mental Models layer's *falsification tests*
   become input to thesis/antithesis (the choice between interventions can be
   evaluated by which intervention better satisfies the falsification tests).
   But the Mental Models analyst's four hard rules stay in place — Dialectical
   does not get to soften them.

### Short-Circuits

- **If Cynefin classifies CLEAR**: skip the rest of the pattern and apply best
  practice. The pattern is overkill.
- **If Cynefin classifies CHAOTIC**: skip the rest, take the stabilizing action,
  then re-run the pattern starting from a re-classification.
- **If Iceberg's Patterns layer finds no recurrence**: the surface symptom is a
  one-off, not systemic. Stop and use Dialectical alone on the immediate event.

### Example Application

**Problem:** "Why does deployment keep failing in this one cluster?"

- **Phase 1 (Triage):** Cynefin Classifier assigns COMPLEX (multi-system
  interaction; cause visible only in retrospect; cluster behavior emerges from
  combination of factors). Synthesizer recommends structure-level diagnosis.
- **Phase 2 (Diagnose):** Iceberg traverses:
  - Events: 14 deploy failures over 90 days, 11 in this cluster.
  - Patterns: 9 of 11 failures occur Tuesday 2–4pm; spared boundary —
    other clusters show no time-of-day correlation.
  - Structures: Tuesday 2–4pm coincides with a network maintenance window the
    deploy team was not informed of; deploy script lacks retry on transient
    network errors; the maintenance calendar is in a system the deploy team
    does not subscribe to.
  - Mental models: "The SRE team believes deploy failures imply application
    bugs, not infrastructure flakiness." Falsification test: ask three SREs
    what their first hypothesis is when a deploy fails; if all three name
    application code first, the model is confirmed.
- **Phase 3 (Decide):** Dialectical poses "intervene at the deploy script
  (add retries with exponential backoff) vs intervene at the calendar
  (subscribe deploy team to maintenance window)." Synthesis: do both, in that
  order — script retries are faster to deploy and reduce immediate impact;
  calendar subscription removes the structural cause; the mental-model
  falsification test should be re-run after both interventions to confirm
  the SRE team's first-hypothesis pattern has shifted.

---

## Composition Anti-Patterns

Things that DON'T work:

| Anti-Pattern | Why It Fails | Instead Do |
|-------------|-------------|-----------|
| Running Six Hats then First Principles | Hats assume a proposal exists; FP deconstructs proposals | FP first, Hats on the reconstruction |
| Collision-Zone → Dialectical (directly) | Raw collisions are too ungrounded for dialectical rigor | Collision → FP (ground it) → Dialectical |
| Dialectical with >2 positions | Thesis/antithesis is binary by design | Use Parallel Perspectives pattern |
| Six Hats with hats in parallel | Hats depend on each other (Black needs White's facts) | Always sequential (some pairs can parallel) |
| Skipping Blue Hat | No orchestrator = chaotic hat outputs | Blue always opens and closes |
| First Principles without the information barrier | Architect sees the original → anchoring bias → reconstruction looks like the original | Enforce: Architect NEVER sees current state |

---

## Implementation Checklist

When implementing a composition pattern in Claude Code:

- [ ] Identify which pattern fits the problem (or use Pattern 4: Triage to auto-select)
- [ ] Load agent prompts for each framework in the chain
- [ ] Set up data flow: define exactly what each agent receives
- [ ] Enforce information barriers: ensure blocked data doesn't leak
- [ ] Run agents sequentially (or parallel where noted)
- [ ] Capture all intermediate outputs (valuable for documentation)
- [ ] Final agent produces the deliverable
- [ ] Store the full chain output as a decision record
