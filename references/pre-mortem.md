# Pre-mortem Analysis — Complete Reference

## Process Overview

Three phases. A Narrator commits to a future in which the project has already failed,
multiple Cause Analyst personas (run in parallel) explain why, and a Mitigation
Synthesizer turns the diagnosis into pre-emptive controls, watch signals, and kill
criteria.

```
Problem → Narrator (commit to failure) → Cause Analysts (×N parallel) → Mitigation Synthesizer → Controls + Signals + Kill Criteria
                                              ↑
                                  INFORMATION BARRIER:
                                  Each persona sees only the
                                  failure narrative, not other
                                  personas' analyses
```

The discipline of pre-mortem comes from prospective hindsight: it is psychologically
easier to imagine *why* a future failure happened than to predict whether it will
happen at all. Klein's research showed that imagining a fait-accompli failure surfaces
20–30% more risks than asking "what could go wrong?". This framework operationalizes
that effect with a hard commit-to-failure step.

---

## Phase 1: Failure-Future Narration (Narrator Agent)

The Narrator does not analyze. The Narrator *narrates* — in past tense — a future in
which the project has unambiguously failed at a specified time horizon. The output
reads like a postmortem written by someone who lived through the failure.

**Critical barrier:** The Narrator commits to failure *before* any cause analysis runs.
The Narrator does NOT see the project's success criteria as the team currently
understands them; the Narrator is given the project description and instructed that
the project has failed. This prevents the optimism-bias loop where "well, success
looks like X, so failure must look like not-X" — that framing under-weights novel
failure modes.

### Time Horizon Parameter

Different horizons surface different failure modes:

- **6 months out**: surfaces execution failures (missed deadlines, integration issues,
  scope creep, key personnel departures)
- **12 months out**: surfaces adoption and operational failures (users rejected it,
  ops cost ran away, performance degraded under real load)
- **18–24 months out**: surfaces strategic and structural failures (market moved,
  regulator intervened, competitor leapfrogged, architectural debt compounded)

Run the framework at the horizon most aligned with the decision in question. Run
multiple horizons if the project spans more than one of those windows.

### Output Template

```
## 🕯️ Failure-Future Narrative — [Horizon T]

### The Failure (One Sentence)
[What, in past tense, failed. Specific. "We rolled back the migration after
8 weeks of customer-impacting incidents." Not "the project had problems."]

### How It Looked From the Outside
[2-3 paragraphs in past tense, written from the perspective of someone who
saw the failure from the outside — a customer, an analyst, a regulator, the
team's leadership. Concrete. Names of incidents, dates, headline language.]

### How It Felt From the Inside
[1-2 paragraphs in past tense from the team's perspective during the failure.
The realization moment. What was on fire. Who was on call.]

### The First Sign It Was Going Wrong (In Hindsight)
[The earliest signal that, in hindsight, was the leading indicator. Often
something the team dismissed at the time.]

### The Point of No Return
[The moment when the failure became inevitable, even if the team did not
yet know it.]
```

### Agent Prompt

```
You are the Failure-Future Narrator. Your job is NOT to predict whether the
project will fail. Your job is to write a vivid, specific narrative of a future
in which it HAS failed, in past tense, as if you lived through it.

YOUR MISSION:
You are operating at horizon T (specified in the input). At T, this project
has failed unambiguously. Narrate that failure with concrete detail.

RULES:
1. Past tense throughout. "We rolled back" not "we might have to roll back."
2. Be specific: name dates, incident codes, customer impact, dollar figures
   if known. Generic narratives produce generic causes.
3. Do NOT propose causes yet — that is the next phase. Narrate WHAT happened
   and HOW IT FELT, not WHY.
4. Do NOT hedge. The project failed. Commit to that. If you find yourself
   writing "could have failed" or "might have failed," stop and rewrite.
5. Do NOT analyze the project's success criteria. You are not comparing to
   plan. You are describing the failure as it happened.
6. The narrative should be readable in 2-3 minutes — long enough to anchor
   subsequent agents, short enough that they engage with it.

TONE: Sober postmortem author. Not catastrophizing, not minimizing. Just the
factual record of a failure that happened.
```

---

## Phase 2: Cause Analysis (Parallel Persona Agents)

Multiple Cause Analyst agents run in parallel, each adopting a distinct persona.
Each persona produces an independent diagnosis of WHY the failure narrated in
Phase 1 happened. The personas are deliberately diverse to prevent groupthink;
each sees only the failure narrative, not the other personas' analyses.

### Default Persona Set

Five personas cover most projects. The orchestrator may add domain-specific
personas (e.g., a Clinical Safety persona for healthcare, a Latency Analyst for
performance-critical systems).

| Persona | Focal Question |
|---------|----------------|
| Operations Skeptic | What broke in production? Where did the runbook fail us? |
| Security Adversary | Where was the breach, the data leak, the abuse vector? |
| Product / Stakeholder | Why did adoption fail? Who said no, and why? |
| Engineering Reality | What did the team underestimate? Where did the design crack? |
| Compliance / Audit | What regulator finding or audit failure caused this? |

### Output Template (per persona)

```
## 🔎 Cause Analysis — [Persona Name]

### Persona Lens
[One-sentence statement of what this persona is looking for]

### Top Three Causes (Ranked by Contribution)
1. [Cause] — [How it manifested in the failure narrative]
2. [Cause] — [How it manifested]
3. [Cause] — [How it manifested]

### Earliest Detection Window
[For the top cause: when, in retrospect, was the first detectable signal?]

### What Would Have Prevented It
[Specific intervention — not "better planning" but "a load test against
the actual production traffic shape, run before week 4"]

### What This Persona Saw That Others Likely Missed
[The unique angle — what makes this persona's diagnosis non-obvious to
the others?]
```

### Agent Prompt (template — instantiated per persona)

```
You are the {{PERSONA_NAME}} — a {{PERSONA_DESCRIPTOR}}. Your job is to
diagnose WHY the failure described in the Failure-Future Narrative happened,
through your specific lens.

YOUR MISSION:
Read the failure narrative. Produce three ranked causes, each tied to a
specific moment or pattern in the narrative. Recommend prevention measures
specific to your lens.

RULES:
1. Stay in your lens. The Operations Skeptic does not analyze regulatory
   posture; the Compliance persona does not write reliability postmortems.
   Specialization is the value.
2. Tie every cause to the narrative. "Insufficient testing" is not a cause;
   "the test suite did not exercise the cross-region failover path that
   triggered the week-4 outage" is.
3. Rank by contribution to the failure, not by how interesting the cause is.
4. Recommend interventions that could be done NOW, before the failure occurs.
   Not "we should have tested more" — "we should add a chaos test that
   simulates region failover by [specific date]."
5. You will NOT see other personas' analyses. This is intentional. Do not
   try to anticipate what they will say or avoid overlap.

TONE: Senior practitioner doing a postmortem. Direct, specific, not theoretical.
```

### Information Barrier (Critical)

Each persona receives ONLY the Failure-Future Narrative. None of them see:

- The other personas' analyses
- The Narrator's internal notes
- Each other's prompts or output formats

Running personas in parallel without this barrier collapses to a single voice
within one or two iterations. The barrier is the only thing that makes the
parallelism produce diverse causes rather than redundant ones.

---

## Phase 3: Mitigation Synthesis (Synthesizer Agent)

The Synthesizer receives the failure narrative and ALL persona analyses, then
produces a mitigation plan in three columns: pre-emptive controls (do these now),
watch signals (monitor for these triggers), and kill criteria (under these
conditions, abort).

### Output Template

```
## 🛡️ Mitigation Plan

### Most Frequent Cause Themes (Across Personas)
[Causes named by 2+ personas, with which personas raised them]

### Persona-Unique Causes Worth Acting On
[Causes raised by only one persona but high-contribution — do not let
single-source causes get dropped just because they lack consensus]

### Pre-Emptive Controls (Do These Now)
| # | Control | Owner | Deadline | Cost | Cause(s) Mitigated |

### Watch Signals (Monitor These)
| # | Signal | Source | Threshold | Action If Tripped | Cause(s) Detected |

### Kill Criteria (Abort If These Become True)
| # | Condition | Detection Window | Decision Maker | Recovery Path |

### Residual Risk
[Causes that cannot be mitigated pre-emptively — what residual exposure
remains and how to communicate it]
```

### Agent Prompt

```
You are the Mitigation Synthesizer. You have the failure-future narrative
and several independent persona diagnoses. Convert them into a concrete
plan that reduces the chance of the failure happening.

RULES:
1. Single-source causes still count. Do not require consensus to act on a
   risk; one persona's lens may be the only lens that sees it.
2. Pre-emptive controls must be specific and ownable. "Improve testing" is
   not a control; "Add cross-region failover chaos test by 2026-02-15
   (owner: SRE lead)" is.
3. Watch signals must have detection sources and thresholds. "Watch latency"
   is not a signal; "p99 region-A→region-B replication lag exceeds 500ms
   for >5 minutes" is.
4. Kill criteria must be pre-agreed. The decision-maker is named NOW, the
   condition is unambiguous, and the recovery path is sketched.
5. Be honest about residual risk. Some causes cannot be mitigated; surface
   them rather than hiding them.

TONE: Program risk manager presenting to a steering committee. Crisp,
ownable, falsifiable.
```

---

## Orchestration

```
┌──────────────────┐
│ Problem +         │
│ Time Horizon T    │
└─────────┬─────────┘
          │
          ▼
┌──────────────────┐
│  🕯️ Narrator     │ → Failure-future narrative
└─────────┬─────────┘
          │ narrative ONLY (no success criteria, no plan)
          │
          ├──────┬──────┬──────┬──────┐
          ▼      ▼      ▼      ▼      ▼
       ┌────┐ ┌────┐ ┌────┐ ┌────┐ ┌────┐
       │Ops │ │Sec │ │Prod│ │Eng │ │Comp│  ← Parallel personas
       │    │ │    │ │    │ │    │ │    │
       └─┬──┘ └─┬──┘ └─┬──┘ └─┬──┘ └─┬──┘
         │      │      │      │      │
         └──────┴──┬───┴──────┴──────┘
                   │ all persona outputs + narrative
                   ▼
          ┌──────────────────┐
          │  🛡️ Synthesizer  │ → Controls + Signals + Kill Criteria
          └──────────────────┘
```

### Data Flow

| Agent | Receives | Produces | Cannot See |
|-------|----------|----------|------------|
| Narrator | Project description, horizon T | Failure narrative | Project success criteria, team's plan |
| Cause Analyst (each) | Failure narrative ONLY | Ranked causes + persona-unique insights | Other personas' analyses, Narrator's notes |
| Synthesizer | Narrative + all persona analyses | Mitigation plan | — |

The Narrator's barrier (no success criteria) and the Cause Analysts' barrier
(no peer outputs) are both load-bearing. Removing either collapses the framework
to ordinary risk-brainstorming.

---

## Worked Examples

**Go-live readiness for vendor migration (horizon: 6 months post-cutover)**
- Narrator: "We rolled back the migration after 11 weeks. Three customer
  segments lost data integrity guarantees during the dual-write window. The
  CIO paused all platform changes until the audit was complete."
- Personas: Ops Skeptic identified dual-write window length as the dominant
  cause. Compliance flagged that the audit trail format diverged from the
  source system in week 4 but was not caught. Engineering Reality named the
  optimistic estimate of source-system query load.
- Synthesizer: Pre-emptive controls — shorten dual-write window to 4 weeks,
  add audit-trail diff job before cutover, run query-load capture for two
  weeks pre-migration. Kill criteria — if audit-trail diff exceeds 0.1% by
  week 2 of dual-write, halt migration.

**Vendor selection commit (horizon: 12 months post-contract)**
- Narrator: "We exercised the contract exit clause after 9 months. The
  vendor's roadmap diverged from our needs in month 4 and never recovered.
  We had built three integrations against deprecated APIs."
- Personas: Product flagged stakeholder mis-alignment on roadmap dependency.
  Security flagged that the vendor's SOC2 evidence was light on a control
  we needed. Engineering Reality flagged API stability assumptions.
- Synthesizer: Pre-emptive — add roadmap-alignment review to contract terms;
  require SOC2 evidence at the control level, not type-level; build
  abstraction layer for first 90 days. Watch signals — vendor roadmap shifts
  more than 20% from the version we contracted against; SOC2 control
  evidence becomes inaccessible.

**Feature flag rollout to 100% (horizon: 30 days post-rollout)**
- Narrator: "We rolled the flag back to 0% after 11 days. The 50% step
  triggered an N+1 query pattern that the 10% step had not exercised.
  Customer-impact incidents totaled 47 hours."
- Personas: Engineering Reality named the load-shape difference between
  10% and 50%. Ops Skeptic named the absence of a per-step bake window.
  Product noted that the metric we trusted (error rate) lagged the actual
  impact (latency-driven churn).
- Synthesizer: Pre-emptive — add a 25% intermediate step with 72-hour bake;
  add p99 latency to rollout dashboard alongside error rate. Kill criteria —
  p99 latency rises >30% over baseline at any step; rollback before next step.
