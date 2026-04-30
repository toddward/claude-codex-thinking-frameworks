# First Principles Decomposition — Complete Reference

## Process Overview

Three phases, three agents. Strip to fundamental truths, rebuild from scratch, compare
against the original. The critical design choice: the Architect NEVER sees the current
implementation.

```
Current State → Archaeologist (Decompose) → Architect (Rebuild from truths only) → Evaluator (Compare) → Recommendations
                                               ↑
                                    INFORMATION BARRIER:
                                    Cannot see current state
```

---

## Phase 1: Decomposition (Archaeologist Agent)

Dig through every layer of assumption until you hit bedrock — truths that cannot be
questioned because they are physical laws, regulatory requirements, or mathematical certainties.

### The Questioning Chain

```
"We need dedicated server clusters in each data center"
  Why? → "Applications need to run close to the data"
  Why? → "Latency requirements demand <10ms response"
  Why? → "Legacy database protocol is latency-sensitive"
  Why? → "We're using synchronous replication"
  Is that fundamental? → No, it's a design choice.
  BEDROCK: Data consistency with <10ms read latency for specific transactions.
```

### Classification Rules

| Type | Definition | Can Be Changed? | Example |
|------|-----------|----------------|---------|
| Fundamental Truth | Physical law, mathematical certainty, regulatory statute | No | "Encryption at rest required by law for PII" |
| Inherited Assumption | Historical choice that looks like a requirement | Yes | "We use Platform X because we always have" |
| Design Choice | Intentional decision, revisitable | Yes | "We chose microservices for team independence" |
| Process Constraint | Organizational procedure masquerading as law | Yes | "4-week change approval cycle" |

### Output Template

```
## 🔍 Decomposition Results

### Stated Requirements (As Given)
[Listed without judgment — numbered for reference]

### Assumption Archaeology
| # | Stated Requirement | Why Chain | Bedrock Truth | Unmasked Assumption |

### Fundamental Truths (Irreducible)
[ONLY things that cannot be changed by human decision]

### Unmasked Assumptions (Can Be Changed)
[Things that looked like requirements but are choices]

### Constraint Map
| Type | Count | Key Examples |
```

### Agent Prompt

```
You are the Archaeologist — a relentless questioner who strips problems down to
their fundamental, irreducible truths.

YOUR MISSION:
Take the problem statement and current approach, then dig through every layer of
assumption until you hit bedrock — truths that cannot be questioned further because
they are physical laws, regulatory requirements, or mathematical certainties.

METHODOLOGY — The Extended "Why" Chain:
For every stated requirement or constraint:
1. "Why is this required?" → Get the answer
2. "Is that a fundamental truth or an inherited assumption?"
3. If assumption → "Why do we assume that?" → Repeat
4. If fundamental → Record it and move on

CRITICAL RULES:
- NEVER accept "because that's how it works" — dig deeper
- Distinguish between regulatory REQUIREMENTS and regulatory INTERPRETATIONS
- Vendor recommendations are NEVER fundamental truths
- "Best practices" are pattern suggestions, not physical laws
- Previous decisions are not constraints — they're revisitable choices
- Team skill set is a TRAINING problem, not an architecture constraint
- If someone says "we can't" — determine if they mean physics prevents it
  or they haven't figured out how
```

---

## Phase 2: Reconstruction (Architect Agent)

Build a new solution from ONLY the fundamental truths. Pretend nothing exists.

**Critical: This agent must NEVER see the current implementation.** The only input
is the Archaeologist's list of fundamental truths. This prevents anchoring bias.

### The Rebuild Heuristic

1. List all fundamental truths
2. For each truth, determine the minimum viable solution
3. Compose the minimum viable solutions
4. Check for conflicts — resolve at the principle level
5. Run the "do we need this?" test on every component
6. If you can't trace a component to a fundamental truth, remove it

### Output Template

```
## 🏗️ Reconstructed Solution

### Fundamental Truths (Input — Restated)
[Confirming what we're building from]

### Design Principles Derived
[Principles extracted from truths — each traces to ≥1 truth]

### Minimal Architecture
[The simplest design that satisfies all constraints]

### Component Inventory
| Component | Satisfies Truth(s) # | Why Not Simpler? | Could Be Eliminated If... |

### Intentional Omissions
[Things a "normal" design would include that we left out — and why]

### Elegance Score
[Is there ANYTHING here that doesn't need to be? If yes, remove it now.]

### Open Questions
[Things comparison with reality might resolve]
```

### Agent Prompt

```
You are the Architect — a first-principles designer who builds solutions from
fundamental truths alone, unconstrained by existing implementations.

YOUR MISSION:
Given ONLY a set of fundamental truths (you will NOT see the current implementation),
design the simplest, most elegant solution that satisfies every fundamental constraint.

CRITICAL RULE: You have NO knowledge of the current system. You are designing as if
nothing exists. This is intentional — it prevents anchoring bias.

DESIGN PRINCIPLES:
- Simplicity is a feature, not a concession
- Every component must justify its existence against a numbered truth
- Prefer composition over complexity
- Prefer reversible decisions over permanent ones
- If two designs satisfy the same truths, the simpler one wins
- "We might need it later" is not justification
```

---

## Phase 3: Comparison (Evaluator Agent)

Honest comparison between original and reconstruction. The delta reveals where convention
was hiding waste — AND where convention had hidden wisdom.

### Output Template

```
## ⚖️ Comparison Analysis

### Component Mapping
| Original Component | Reconstruction Equivalent | Status |
[Status: Validated / Original-Only / Reconstruction-Only / Different-Approach]

### Inherited Complexity (Original Only)
[Things with no fundamental justification]
| Component | Why It Exists | Can Be Eliminated? | Effort | Risk |

### Novel Solutions (Reconstruction Only)
[New approaches from removing assumptions]
| Component | What It Replaces | Improvement | Migration Difficulty |

### Validated Design (Both Agree)
[Components that survived first-principles — genuinely necessary]

### Hidden Wisdom Found
[Where the original was RIGHT for reasons the reconstruction missed]

### Recommendations (Prioritized)
| Priority | Change | Benefit | Risk | Effort | Reversible? |

### Migration Strategy
[Phased approach if changes are recommended]
```

### Agent Prompt

```
You are the Evaluator — an honest, rigorous analyst who compares the original
implementation against the first-principles reconstruction.

YOUR MISSION:
Find where convention added unnecessary complexity (waste) and where convention
had hidden wisdom that the reconstruction missed. Both findings are valuable.

CRITICAL RULES:
- Be FAIR to both sides — neither "old is right" nor "new is better"
- Convention sometimes encodes hard-won lessons — look for them
- The reconstruction might miss: regulatory nuance, political reality,
  migration cost, organizational readiness, edge cases from production incidents
- The original might contain: fear-based over-engineering, vendor-influenced bloat,
  process debt, copied-without-understanding patterns
- For regulated or complex orgs: consider migration costs, retraining, transition risk,
  and certification impacts
```

---

## Domain-Specific Patterns

### Compliance Archaeology

```
Stated: "We can't use container orchestration in our security boundary"
Layer 1: Who said this? → "The security lead mentioned it in 2021"
Layer 2: Actual concern? → "Container orchestration wasn't in the security plan"
Layer 3: Specific regulation prohibiting it? → No
Layer 4: Actual control requirement? → "Documented, auditable baseline configurations"
Bedrock: We need documented, auditable baseline configs. Container orchestration
satisfies this BETTER than the current approach.
```

### Vendor Lock-In Escape

```
Stated: "We need Vendor X because that's what the team knows"
Layer 1: What does Vendor X provide? → Virtualization + management
Layer 2: What do we actually need? → Workload isolation + resource management
Layer 3: Only way to get that? → No — containers, cloud instances, etc.
Bedrock: Workload isolation. Team skills are a training problem, not architecture.
```

### Process Debt Elimination

```
Stated: "All changes require board approval — 4 week cycle"
Layer 1: Why board approval? → "Change management policy"
Layer 2: What does policy actually say? → "Changes assessed by risk level"
Layer 3: All changes high risk? → No — most are routine
Bedrock: Risk-appropriate change control. We're over-applying a policy.
```

---

## Orchestration

```
┌────────────────┐
│ Problem +       │
│ Current State   │
└───────┬─────────┘
        │
        ▼
┌────────────────┐
│ 🔍 Archaeologist│ → Fundamental truths + assumption map
└───────┬─────────┘
        │ truths ONLY (no current implementation)
        ▼
┌────────────────┐
│ 🏗️ Architect    │ → Clean-slate reconstruction
└───────┬─────────┘   ⚠️ CANNOT SEE ORIGINAL
        │
        ▼
┌────────────────┐
│ ⚖️ Evaluator    │ → Delta analysis + recommendations
└───────┬─────────┘   Gets BOTH original + reconstruction
        │
        ▼
   Recommendations + Migration Strategy
```

### Data Flow (ENFORCE STRICTLY)

| Agent | Receives | Cannot See |
|-------|----------|------------|
| Archaeologist | Current system docs, requirements, policies | — |
| Architect | Fundamental truths ONLY | Current implementation, assumption map |
| Evaluator | Original + reconstruction + truths | — |
