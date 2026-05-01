---
name: thinking-frameworks
description: >
  Multi-agent thinking frameworks for rigorous problem-solving and decision-making.
  Includes Dialectical (thesis-antithesis-synthesis), Six Thinking Hats, First
  Principles, Collision-Zone, Cynefin (problem classification), Pre-mortem (imagine
  failure modes), and Iceberg (events→patterns→structures→mental models), plus
  composition patterns and techniques like Steel-manning, Inversion, and
  Chesterton's Fence. Use whenever the user needs to evaluate competing approaches,
  make architecture decisions, challenge assumptions, modernize legacy systems,
  run post-mortems, classify ambiguous problems, or do multi-perspective analysis.
  Triggers on "think this through", "pros and cons", "tradeoffs", "should we use
  X or Y", "devil's advocate", "from all angles", "what are we missing", "first
  principles", "why do we do it this way", "go/no-go", "pre-mortem", "what could
  go wrong", "root cause", "this keeps happening", "steel-man", "invert the
  problem", "Chesterton's Fence", or any thinking framework reference.
---

# Thinking Frameworks for Agent Teams

## Overview

This skill implements structured thinking methodologies as multi-agent teams.
Each framework decomposes into specialized agent roles that produce stronger
outputs through cognitive diversity and structured tension.

**Seven frameworks, six composition patterns, three composable techniques, and a triage system.**

## Quick Selection: Which Framework?

Read this table first. Pick the framework, then read its reference file.

| Situation | Framework | Reference File |
|-----------|-----------|---------------|
| "Should we use X or Y?" | **Dialectical** | `references/dialectical.md` |
| "Evaluate this from every angle" | **Six Hats** | `references/six-hats.md` |
| "Why do we do it this way?" | **First Principles** | `references/first-principles.md` |
| "We're stuck, need a breakthrough" | **Collision-Zone** | (existing skill) |
| "What kind of problem is this even?" | **Cynefin** | `references/cynefin.md` |
| "What could go wrong before we commit?" | **Pre-mortem** | `references/pre-mortem.md` |
| "Why does this keep happening?" | **Iceberg** | `references/iceberg.md` |
| Sharpen advocate / fence-removal / inversion | **Composable techniques** | `references/composable-techniques.md` |
| Complex multi-phase analysis | **Composition Pattern** | `references/composition-patterns.md` |
| "I don't know which framework to use" | **Cynefin Triage** | `references/cynefin.md` |

### Decision Logic

```
Is the problem TYPE itself ambiguous? (don't know if it's a known-knowns
problem, an expert-analysis problem, or an emergent problem)
  YES → Cynefin (3 agents: Classifier → Domain Responder → Routing Synthesizer)

Is there a clear binary choice (X vs Y)?
  YES → Dialectical (3 agents: Advocate → Challenger → Integrator)

Do we need comprehensive, multi-stakeholder analysis?
  YES → Six Hats (7 agents: Blue orchestrator + 6 perspective agents)

Are we questioning inherited complexity or assumptions?
  YES → First Principles (3 agents: Archaeologist → Architect → Evaluator)

Are we stuck and need a creative breakthrough?
  YES → Collision-Zone (existing skill)

Are we about to commit to a high-stakes decision and want to imagine its
failure first?
  YES → Pre-mortem (3 phases: Narrator → parallel Cause Analysts → Mitigation Synthesizer)

Does the same surface symptom keep recurring? Are retros not producing change?
  YES → Iceberg (4 layers: Events → Patterns → Structures → Mental Models)

Is the problem too complex for a single framework?
  YES → Read composition-patterns.md for multi-framework orchestration

Want to sharpen an advocate role, gate a structural removal, or stress-test
forward thinking via inversion?
  → Layer in a composable technique from references/composable-techniques.md

Not sure what we're dealing with?
  → Cynefin Triage (entry point for ambiguous problems)
```

## Framework Summaries

### Dialectical Thinking (3 Agents)
**Core idea:** Truth emerges from structured intellectual conflict.

- **Advocate** builds the strongest case FOR a position
- **Challenger** systematically dismantles it and proposes an alternative
- **Integrator** transcends both into something stronger than either

Best for: binary decisions, architecture debates, RFP responses, technology selection.
Cycle time: fast (3 sequential agent calls).

**Read `references/dialectical.md` for the full process, output formats, and agent prompts.**

### Six Thinking Hats (7 Agents)
**Core idea:** Parallel thinking beats adversarial thinking for comprehensive coverage.

Six cognitive modes, each worn one at a time:
- 🔵 **Blue** (Process) — orchestrates the sequence, synthesizes results
- ⚪ **White** (Facts) — data, information gaps, confidence levels
- 🔴 **Red** (Intuition) — feelings, hunches, stakeholder sentiment
- ⬛ **Black** (Caution) — risks, failure modes, compliance gaps
- 🟡 **Yellow** (Optimism) — benefits, value, strategic positioning
- 🟢 **Green** (Creativity) — alternatives, wild cards, assumption challenges

Best for: go/no-go decisions, post-mortems, cross-functional analysis, project evaluation.
Cycle time: medium (7 sequential agent calls, some parallelizable).

**Read `references/six-hats.md` for hat sequences, output formats, and agent prompts.**

### First Principles Decomposition (3 Agents)
**Core idea:** Most complexity is inherited, not necessary. Strip to fundamentals, rebuild.

- **Archaeologist** digs through assumption layers to find bedrock truths
- **Architect** builds from ONLY those truths (never sees the original system)
- **Evaluator** compares the reconstruction against the original

The information barrier is critical: the Architect must never see the current
implementation. This prevents anchoring bias.

Best for: legacy modernization, architecture simplification, challenging "best practices."
Cycle time: medium (3 sequential, deep-thinking agent calls).

**Read `references/first-principles.md` for the full process, domain-specific patterns, and agent prompts.**

### Cynefin Classification (3 Agents)
**Core idea:** Different kinds of problems need different kinds of responses. Classify before reasoning.

- **Classifier** assigns the problem to one of five domains (Clear, Complicated, Complex, Chaotic, Confused)
- **Domain Responder** runs one of five domain-specific response modes (best practice / good practice / safe-to-fail experiments / stabilizing action / decompose)
- **Routing Synthesizer** produces an unambiguous next-step recommendation, including which downstream framework to invoke

The discipline is not solving the problem — it is deciding *how* to decide. Default to the less predictable side of any cliff (e.g., Complicated/Complex).

Best for: ambiguous problems, triage, choosing among other frameworks, escaping the trap of treating Complex problems as if they were Complicated.
Cycle time: fast (3 sequential agent calls; can short-circuit on Clear or Chaotic).

**Read `references/cynefin.md` for the five domain prompts, routing rules, and worked examples.**

### Pre-mortem Analysis (3 Phases, Multiple Parallel Agents)
**Core idea:** Imagining a future failure surfaces 20–30% more risks than asking "what could go wrong?" Commit to the failure first, then diagnose.

- **Failure-Future Narrator** writes a vivid past-tense narrative in which the project has failed at horizon T (does NOT see the team's success criteria — anti-anchor)
- **Cause Analysts** run in parallel as distinct personas (Operations Skeptic, Security Adversary, Product/Stakeholder, Engineering Reality, Compliance/Audit) — each diagnoses the failure through one lens, blind to the others
- **Mitigation Synthesizer** converts diagnoses into pre-emptive controls, watch signals, and pre-agreed kill criteria

The information barrier (each persona sees only the narrative, not other personas' analyses) is what prevents groupthink consolidation around the first-flagged cause.

Best for: go/no-go gates on major commits, vendor-selection sign-off, feature flag rollouts, any high-stakes decision before contract or launch.
Cycle time: medium (1 sequential + N parallel + 1 sequential).

**Read `references/pre-mortem.md` for the persona prompts, time-horizon parameter, and worked examples.**

### Iceberg Model (4 Sequential Layers)
**Core idea:** Surface events sit on top of patterns, which sit on top of structures, which sit on top of mental models. Most leverage lives below the waterline. Traverse the full stack — do not skip to "the culture is broken."

- **Events Analyst** produces a clean roster of observable facts (no interpretation)
- **Patterns Analyst** identifies frequency, correlation, and boundary patterns (sees events ONLY)
- **Structures Analyst** names policies, processes, incentives, org topology that produce the patterns (sees events + patterns; cannot cite mental models)
- **Mental Models Analyst** names testable beliefs that justify the structures, with falsification tests (sees events + patterns + structures; bound by four hard rules to prevent pop-psychology mush)

The four hard rules on the Mental Models layer (must reference a numbered structure, must be testable, must include a falsification test, no vocabulary lists) are what keeps Iceberg analyses actionable rather than rhetorical.

Best for: recurring incidents, retros that don't produce change, "we keep solving this and it keeps coming back," systemic post-mortems.
Cycle time: slow (4 sequential layers; the Mental Models prompt is the most error-prone).

**Read `references/iceberg.md` for layer barriers, the four hard rules, and worked examples.**

### Composable Techniques (Cross-Cutting Augmenters)
**Core idea:** Three short rules that plug into any first-class framework's agent prompts to sharpen specific reasoning patterns. Not standalone frameworks — paste-able snippets.

- **Steel-manning** — forces an advocate to defend against the strongest version of the opposing position, not the weakest
- **Inversion** (Munger / Jacobi) — runs a final stress test on forward thinking by inverting the question
- **Chesterton's Fence** — gates structural removals until the original purpose is reconstructed

**Read `references/composable-techniques.md` for definitions, prompt snippets to inject, and anti-patterns.**

## Composition Patterns (Multi-Framework)

When a single framework isn't enough, composition patterns chain them together
with defined data flows and information barriers.

| Pattern | Sequence | Use When |
|---------|----------|----------|
| Decompose → Debate → Decide | FP → Dialectical → Six Hats | Legacy modernization |
| Collide → Ground → Validate | Collision → FP → Six Hats | Innovation under constraints |
| Assess → Explore → Commit | Six Hats → Dialectical (recursive) | Complex multi-stakeholder |
| Triage → Route → Execute | Cynefin → [auto-selected] | Don't know which framework |
| Parallel Perspectives | Dialectical (×N) → Six Hats | Comparing 3+ options fairly |
| Triage → Diagnose → Decide | Cynefin → Iceberg → Dialectical | Ambiguous problem type + recurring symptom + binary intervention |

**Read `references/composition-patterns.md` for complete orchestration specs, data flow
rules, information barriers, and anti-patterns.**

## Claude Code Implementation

### Spawning Agent Teams with Task

Each agent in a framework runs as a Claude Code `Task` (subagent). The orchestration
pattern is always:

1. Load the relevant reference file for agent prompts
2. Spawn each agent sequentially, passing outputs forward
3. Enforce information barriers (some agents must NOT see certain data)
4. Final agent produces the recommendation

### Basic Task Pattern

```python
# Dialectical example
thesis = Task(
    prompt=f"{advocate_prompt}\n\nPROBLEM: {problem}",
    description="Dialectical: Build thesis"
)

antithesis = Task(
    prompt=f"{challenger_prompt}\n\nTHESIS:\n{thesis}",
    description="Dialectical: Challenge thesis"
)

synthesis = Task(
    prompt=f"{integrator_prompt}\n\nTHESIS:\n{thesis}\n\nANTITHESIS:\n{antithesis}",
    description="Dialectical: Synthesize"
)
```

### CLAUDE.md Integration

Add this block to any project's CLAUDE.md to enable thinking framework agent teams:

```markdown
## Thinking Frameworks

For complex decisions, use the thinking-frameworks skill:
- "Use dialectical analysis for [problem]" → Advocate → Challenger → Integrator
- "Run six hats on [problem]" → Blue orchestrates 6 perspective agents
- "Apply first principles to [problem]" → Archaeologist → Architect → Evaluator
- "Classify this problem (Cynefin) for [problem]" → Classifier → Responder → Synthesizer
- "Run a pre-mortem on [decision] at horizon T" → Narrator → parallel personas → Mitigation
- "Iceberg this recurring incident" → Events → Patterns → Structures → Mental Models
- For multi-framework: read composition-patterns.md and select a pattern
- For technique injection: read composable-techniques.md (Steel-manning / Inversion / Chesterton's Fence)
```

### Context Management Rules

Each agent should receive:
1. Its role-specific system prompt (from the framework's reference file)
2. The problem statement
3. Outputs from previous agents in the chain
4. Optional domain context (project docs, policies, technical specs)

**Keep agent context intentionally focused.** What an agent CANNOT see is as important
as what it can see. The reference files specify information barriers for each framework.

## Practical Applications

| Application | Recommended Approach |
|------------|---------------------|
| Architecture Decision Records | Dialectical per ADR |
| Security & Compliance Planning | Six Hats: White→Black→Yellow→Green→Red |
| Legacy Modernization | Composition: Decompose → Debate → Decide |
| Incident Post-Mortems | Six Hats (Post-Mortem sequence) |
| Vendor Evaluation | Composition: Parallel Perspectives → Convergence |
| Challenging "Best Practices" | First Principles with domain-specific patterns |
| Innovation Under Constraint | Composition: Collide → Ground → Validate |
| Ambiguous Problem Triage | Cynefin (entry point; routes to other frameworks) |
| Go-Live Readiness / Pre-Commit | Pre-mortem at the relevant horizon |
| Recurring Incidents / Retro Failure | Iceberg full traversal |
| Deeply-rooted Recurring Decisions | Composition: Triage → Diagnose → Decide |

## Reference Files

Read the appropriate reference file BEFORE building agent prompts:

| File | Contents | When to Read |
|------|----------|-------------|
| `references/dialectical.md` | Full process, output templates, 3 agent prompts | Binary decisions, debates |
| `references/six-hats.md` | Hat details, sequences, 7 agent prompts | Comprehensive analysis |
| `references/first-principles.md` | Decomposition method, domain patterns, 3 agent prompts | Assumption challenging |
| `references/cynefin.md` | Five domains, classifier + responder + synthesizer prompts | Problem-type ambiguous; triage |
| `references/pre-mortem.md` | Failure-future narrator, parallel persona prompts, mitigation synthesis | High-stakes commits, go/no-go gates |
| `references/iceberg.md` | Four-layer prompts, four hard rules on Mental Models, falsification tests | Recurring symptoms, retro failures |
| `references/composable-techniques.md` | Steel-manning, Inversion, Chesterton's Fence — paste-able snippets | Sharpening any framework's agent prompts |
| `references/composition-patterns.md` | 6 patterns, data flows, barriers, anti-patterns | Multi-framework orchestration |

## Red Flags That a Thinking Framework Is Needed

- "We've already decided" → Dialectical (challenge the decision)
- "Everyone agrees" → Six Hats (find what's missing)
- "That's how it's always been done" → First Principles (strip assumptions)
- "We've tried everything" → Collision-Zone (force novel connections)
- "It's too complex to change" → First Principles (separate necessary from inherited)
- "I don't know where to start" → Cynefin (classify, then route)
- "Is this even the kind of problem I think it is?" → Cynefin (cliff-test the classification)
- "What could go wrong?" → Pre-mortem (commit to failure first, then diagnose)
- "Same incident keeps happening" → Iceberg (traverse from events through structures to mental models)
- "Our retros never produce change" → Iceberg (the action items are stuck at the events layer)
- About to remove a policy whose origin is unclear → Chesterton's Fence (composable technique)
- An advocate keeps producing weak straw-man defenses → Steel-manning (composable technique)
- Forward thinking is producing variations on one idea → Inversion (composable technique)
