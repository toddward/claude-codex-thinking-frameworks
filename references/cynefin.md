# Cynefin Classification — Complete Reference

## Process Overview

Three phases, three agents. A problem is classified into one of five domains, the
domain dictates the response style, and a routing synthesizer either recommends a
follow-on framework or commits to the domain-native action.

```
Problem → Classifier (Domain) → Domain Responder → Routing Synthesizer → Recommendation
```

Cynefin is not a thinking framework in the same shape as Dialectical or Six Hats —
it does not produce a decision. It produces *the decision about how to decide*. Use
it as the entry point when the problem type itself is ambiguous, or as the triage
step in a composition pattern.

---

## The Five Domains

| Domain | Cause-Effect | Response Style | Action Sequence |
|--------|--------------|----------------|-----------------|
| Clear | Obvious | Best practice | sense → categorize → respond |
| Complicated | Discoverable through analysis | Good practice | sense → analyze → respond |
| Complex | Visible only in retrospect | Emergent practice | probe → sense → respond |
| Chaotic | Indiscernible | Novel practice | act → sense → respond |
| Confused (Aporetic) | Unknown which domain applies | Decompose | classify the sub-problems |

The cliff between Complicated and Complex is the most consequential boundary. A
Complicated problem yields to expert analysis. A Complex problem does not — it must
be probed with safe-to-fail experiments because the system's behavior emerges from
the action itself. Misclassifying Complex as Complicated is the dominant failure mode.

---

## Phase 1: Classification (Domain Classifier Agent)

Classify the problem with confidence and reasoning. This phase has only one job:
produce a domain assignment that subsequent agents will trust.

### Output Template

```
## 🧭 Cynefin Classification

### Problem Statement (Restated)
[The problem as you understand it — surface any reframings here]

### Domain Assignment
- Domain: [clear | complicated | complex | chaotic | confused]
- Confidence: [high | medium | low]

### Diagnostic Signals
[2-4 specific signals from the problem statement that indicate this domain]

### Cliff Test
[Is this on the boundary between two domains? If yes, name the cliff and the
default-safer side. The Complicated/Complex cliff is the most important.]

### What This Domain Means for Action
[One paragraph: what response style this domain requires]

### Sub-Problems Detected (if Confused)
[If "confused" — list the sub-problems and a tentative classification for each]
```

### Agent Prompt

```
You are the Cynefin Classifier — a diagnostic agent whose only job is to assign
a problem to one of five domains so that subsequent agents know how to respond.

YOUR MISSION:
Read the problem statement. Identify the cause-effect relationship signature
(obvious, discoverable, retrospective, indiscernible, or unknown). Assign a
domain with confidence and reasoning. Do NOT propose solutions — that is not
your job.

THE FIVE DOMAINS:

CLEAR — Cause and effect is obvious to a reasonable observer. Best practice
exists and is well-known. Disagreement is rare.
  Signal: "Everyone agrees what to do; we just need to do it."
  Example: "Renew our SSL certificates before they expire."

COMPLICATED — Cause and effect is discoverable through analysis. Multiple right
answers may exist; expert reasoning chooses among them.
  Signal: "There are several reasonable options; we need to pick the best one."
  Example: "Which managed database should we use for the new compliance platform?"

COMPLEX — Cause and effect is only visible in retrospect. The system's behavior
emerges from the action; you cannot predict it from analysis alone.
  Signal: "We have not done this before, and we cannot fully predict the outcome."
  Example: "How should we structure AI governance for enterprise customers?"

CHAOTIC — No discernible cause-effect relationship at the moment. Action is
required to create stability before any analysis is meaningful.
  Signal: "Things are actively breaking and we need to decide NOW."
  Example: "Production is down across three regions and the cause is unknown."

CONFUSED (also called Aporetic) — You cannot yet classify the problem because
the boundaries are unclear. The correct response is to decompose into sub-problems
and classify each.
  Signal: "I am not sure which kind of problem this even is."
  Example: "Something feels wrong with our architecture but I cannot articulate it."

CLASSIFICATION RULES:
1. Default to the LESS predictable side of any cliff. If torn between Complicated
   and Complex, choose Complex. Treating a Complex problem as Complicated produces
   confidently wrong answers; treating a Complicated problem as Complex produces
   slower-but-correct answers.
2. The Chaotic domain is rare and time-bounded. If the problem has been ongoing
   for more than days, it is almost certainly Complex, not Chaotic.
3. "Confused" is a real and useful classification — do not force a domain when
   the boundaries are genuinely unclear.
4. Cite specific signals from the problem statement for your classification. No
   vibes-based assignments.

OUTPUT: JSON-shaped header followed by the markdown template above.
{
  "domain": "clear|complicated|complex|chaotic|confused",
  "confidence": "high|medium|low",
  "reasoning": "Why this classification — cite specific signals"
}
```

---

## Phase 2: Domain-Specific Responder (Responder Agent)

The Responder receives the classification and produces a domain-native response.
There are five distinct prompt modes — the orchestrator selects one based on Phase 1's
output. The Responder runs only ONE mode per invocation.

### Output Template (all modes)

```
## 🎯 Domain Response

### Domain (Confirmed)
[Restated from Phase 1]

### Response Mode
[best practice | good practice | emergent practice | novel practice | decompose]

### Action or Inquiry
[The domain-native output — see mode-specific guidance below]

### Confidence in This Response
[High/Medium/Low — and what would change it]
```

### Mode Prompts

**Mode A — Clear (best practice):**
```
You are operating in the CLEAR domain. The cause-effect relationship is obvious;
best practice is known. Produce the best practice answer directly. Do NOT run a
thinking framework — that is overkill for this domain. Cite the source of the
best practice (standard, vendor doc, runbook, regulation).
```

**Mode B — Complicated (good practice):**
```
You are operating in the COMPLICATED domain. Cause and effect is discoverable
through expert analysis. Multiple right answers may exist. Produce a recommendation
that names the analytical framework appropriate for the next step:
  - 2 candidate options → recommend Dialectical
  - Multi-faceted evaluation → recommend Six Hats
  - Inherited assumptions to challenge → recommend First Principles
Do NOT solve the problem yourself; route it.
```

**Mode C — Complex (emergent practice):**
```
You are operating in the COMPLEX domain. Cause-effect is visible only in
retrospect. Do NOT propose a final solution. Instead, design 2-4 SAFE-TO-FAIL
EXPERIMENTS that probe the system. Each experiment must have:
  - A hypothesis you are probing
  - A success amplifier (what to do if signal is positive)
  - A failure dampener (what to do if signal is negative — bounded blast radius)
  - A measurement (how you will know within a defined window)
For deeper innovation, recommend Collision-Zone followed by First Principles.
```

**Mode D — Chaotic (novel practice):**
```
You are operating in the CHAOTIC domain. Stability comes before analysis.
Produce ONE immediate stabilizing action — the smallest move that restores
some predictability. Do NOT debate alternatives; speed matters more than
optimality. After the stabilizing action, recommend a re-classification: most
chaotic problems become Complex (or Complicated) once stability is restored.
```

**Mode E — Confused (decompose):**
```
You are operating in the CONFUSED domain. The problem cannot yet be classified.
Decompose it into 2-5 distinct sub-problems. For each sub-problem, produce a
tentative domain classification with confidence level. Recommend re-running
the Classifier on the largest or most consequential sub-problem first.
```

---

## Phase 3: Routing Synthesizer (Synthesizer Agent)

The Synthesizer combines the classification and the response into a single
recommendation: which framework (or domain-native action) to invoke next, and what
context to pass forward.

### Output Template

```
## 🧩 Cynefin Routing Recommendation

### Classification (Confirmed)
[Domain, confidence, top diagnostic signal]

### Recommended Next Step
[One of: best-practice action | Dialectical | Six Hats | First Principles |
Collision-Zone | safe-to-fail experiments | stabilizing action | decompose]

### Context to Pass to the Next Agent
[The exact problem framing the next agent should receive — including any
reframing from Phase 1]

### Watch-For Signals
[What would invalidate this routing — e.g., "if the experiment results show X,
re-classify as Complicated"]

### Confidence and Caveats
[Honest read on routing certainty, with the cliff-test from Phase 1 surfaced]
```

### Agent Prompt

```
You are the Cynefin Routing Synthesizer. You receive a classification from the
Classifier and a domain-native response from the Responder. Produce a single,
unambiguous recommendation: what should the user (or the next framework agent)
do next?

RULES:
1. Be specific. "Run Dialectical" is acceptable; "use a thinking framework" is not.
2. If the classification was low-confidence or on a cliff, surface that explicitly.
   The user must know when the routing itself is uncertain.
3. Translate the problem into context the next agent will need. Do not assume
   the next agent has read this conversation.
4. For Complex routing: list the safe-to-fail experiments verbatim — do NOT just
   say "run experiments."
5. For Chaotic routing: lead with the stabilizing action; everything else is
   secondary.
```

---

## Orchestration

```
┌──────────────────┐
│ Problem Statement│
└─────────┬────────┘
          │
          ▼
┌──────────────────┐
│  🧭 Classifier   │ → Domain + confidence + signals
└─────────┬────────┘
          │ classification only
          ▼
┌──────────────────┐
│  🎯 Responder    │ → Domain-native response (one of 5 modes)
└─────────┬────────┘
          │ classification + response
          ▼
┌──────────────────┐
│  🧩 Synthesizer  │ → Routing recommendation
└─────────┬────────┘
          │
          ▼
   Next framework / domain-native action
```

### Data Flow

| Agent | Receives | Produces | Cannot See |
|-------|----------|----------|------------|
| Classifier | Problem statement, domain context | Domain assignment + reasoning | — |
| Responder | Classification + problem | Domain-native response (one mode) | — |
| Synthesizer | Classification + response + problem | Routing recommendation + context | — |

There is no information barrier between Cynefin's three agents — unlike
First Principles, the value here comes from each agent building on the previous.
The barrier (when used in composition) is between Cynefin and the framework it
routes to: that next framework receives the *problem*, not the Classifier's
internal reasoning.

---

## Multi-Domain Edge Cases

Many real problems span multiple domains. Handle these explicitly:

- **Mixed Complicated + Complex**: The component-selection part is Complicated; the
  user-adoption part is Complex. Route component selection to Dialectical/Six Hats
  and design safe-to-fail experiments for adoption *in parallel*.
- **Chaotic with Complex underneath**: Production outage is Chaotic *now*; the root
  cause may be Complex. Stabilize first; reclassify the post-incident analysis.
- **Confused with one obvious sub-problem**: If decomposition reveals one clearly
  Complicated sub-problem and other unclassified pieces, route the clear one
  immediately rather than waiting to classify everything.

The Synthesizer must surface these splits explicitly. A single routing recommendation
for a multi-domain problem is a sign that the Classifier flattened the problem.

---

## Worked Examples

**Incident triage:** "Production is down in one region; users are seeing 503s."
- Classifier: Chaotic (active outage, time-pressure, cause unknown). Confidence: high.
- Responder (Mode D): Stabilizing action — fail traffic to other regions; confirm
  blast radius is bounded.
- Synthesizer: Stabilize first; once traffic is shifted, re-classify the root-cause
  investigation. It will likely be Complex (multi-system interaction) or Complicated
  (single-component fault).

**Feature prioritization:** "We have 12 candidate features and 1 sprint of capacity."
- Classifier: Complicated (multiple right answers, expert ranking required).
  Confidence: high.
- Responder (Mode B): Recommend Six Hats with the Go/No-Go sequence applied per
  candidate, or a Parallel Perspectives composition pattern if the top 3 candidates
  warrant deeper comparison.
- Synthesizer: Route to Six Hats. Pass: the 12 candidates, capacity constraint,
  and current strategic theme.

**Novel platform launch:** "How should we govern AI agents inside our enterprise?"
- Classifier: Complex (no precedent; behavior emerges from policy choices and
  user adoption). Confidence: medium. Cliff: Complicated/Complex — defaulted Complex.
- Responder (Mode C): Three safe-to-fail experiments — (a) opt-in pilot in one
  business unit with a published kill-criteria threshold; (b) red-team simulation
  of the proposed governance against three abuse scenarios; (c) shadow-mode
  monitoring across all units before any policy is enforced.
- Synthesizer: Run experiments before any framework decision. After 6 weeks, return
  with experiment outputs and re-run Cynefin — most likely transitions to Complicated.
