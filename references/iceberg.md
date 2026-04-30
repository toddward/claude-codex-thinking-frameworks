# Iceberg Model — Complete Reference

## Process Overview

Four sequential layers, descending depth. A surface event is decomposed into the
patterns it sits within, the structures that produce those patterns, and the mental
models that justify those structures. Each layer is owned by a separate analyst
agent and shielded from the layers below to prevent shortcutting.

```
Event → Patterns Analyst → Structures Analyst → Mental Models Analyst → Intervention Recommendations
                ↑                  ↑                      ↑
        BARRIER:           BARRIER:              BARRIER:
        sees events        sees events +         sees events + patterns
        only               patterns              + structures (no prior
                                                  mental-model hypotheses)
```

The Iceberg Model treats observable events as the 10% of the iceberg above the
waterline. Most leverage for change lives at the deeper layers. The framework's
discipline comes from forcing the analysis to traverse the full stack rather than
jumping from "an incident happened" to "the culture is broken" — that jump is the
dominant failure mode.

Use Iceberg when the same surface event keeps recurring, when retros do not
produce change, or when a recurring problem looks systemic but cannot be named.

---

## Phase 1: Events Layer (Events Analyst Agent)

The Events Analyst surfaces what actually happened. Surface-level facts only —
who, what, when, where. No interpretation, no patterns, no causes.

### Output Template

```
## 🌊 Events — What Happened

### Event Roster
| # | Date | Event | Observer | Source |

### Observable Facts (Per Event)
[For each event: 2-3 specific observations. Times, durations, counts, named
roles. No adjectives that imply pattern.]

### What We Cannot Yet Verify
[Claims that have been made but are not yet sourced — held for the next layer]

### Scope of This Analysis
[How far back, which teams, which systems — explicit boundary]
```

### Agent Prompt

```
You are the Events Analyst. Your job is to produce a clean roster of
observable events and surface-level facts. You do NOT analyze. You do NOT
infer patterns. You do NOT propose causes.

RULES:
1. Each event entry has a date (or date range), a one-sentence factual
   description, and a source. If the source is missing, say so.
2. Strip evaluative language. "An on-call was paged at 2am" not "an
   on-call suffered through a brutal 2am page."
3. If something is alleged but not observed, put it in "What We Cannot
   Yet Verify" — do not promote it to the event roster.
4. Bound the scope explicitly. Iceberg analyses bloat without scope limits.

TONE: Court reporter. Just the record.
```

---

## Phase 2: Patterns Layer (Patterns Analyst Agent)

The Patterns Analyst receives the events roster and identifies trends, frequencies,
and correlations. The output is descriptive, not yet causal.

**Information barrier:** The Patterns Analyst sees the events roster ONLY. No
hypotheses about structures or mental models from prior analyses. This prevents
the analyst from cherry-picking patterns that confirm a pre-formed structural
theory.

### Output Template

```
## 🌀 Patterns — What Recurs

### Frequency Patterns
[Events that recur on a cadence — daily, after each release, every Q4, etc.
With counts.]

### Correlation Patterns
[Events that cluster together — "every time X happens, Y follows within 48
hours". With strength estimate: strong / moderate / weak.]

### Boundary Patterns
[Where the events stop. Which teams, systems, or contexts they spare —
this is often as informative as where they appear.]

### Trend Patterns
[Direction of change over time — increasing, decreasing, plateauing.
With time-window.]

### What These Patterns Are NOT (Yet)
[Explicit non-claims: "We cannot yet say these patterns are caused by X."
This holds the line against premature causation.]
```

### Agent Prompt

```
You are the Patterns Analyst. Your job is to find recurrence, correlation,
and trend in the events roster — without yet proposing causes.

RULES:
1. Cite the specific events that support each pattern. A pattern that does
   not point back to numbered events in the roster is not yet a pattern.
2. Quantify where you can. "Three of the last five releases" beats "often."
3. Note the boundaries — what teams, systems, or time windows are SPARED
   from the pattern. Boundaries point at structures.
4. Do NOT propose what causes the patterns. That is the next phase.
5. Do NOT cite mental models or culture. You have no evidence for them yet.

TONE: Empirical analyst. Measurement, not narrative.
```

---

## Phase 3: Structures Layer (Structures Analyst Agent)

The Structures Analyst explains the patterns by naming the structures that produce
them: policies, processes, incentives, on-call rotations, organizational topology,
financial structures, tooling, escalation paths, RACI matrices. The output is
mechanistic — "structure X causes pattern Y because…"

**Information barrier:** The Structures Analyst sees events + patterns. No mental-
model hypotheses (those come next). The order matters: a structure-level diagnosis
that cites "the team's mindset" is leaping ahead and must be sent back.

### Output Template

```
## 🏛️ Structures — What Produces the Patterns

### Structural Inventory (Causes Mapped to Patterns)
| # | Structure | Type | Pattern(s) Produced | Evidence Link |

(Type: policy | process | incentive | org topology | tooling | financial |
escalation | RACI | other-named-mechanism)

### Structure Detail (Per Structure)
[For each numbered structure:
- Description (concrete, with names where possible)
- Mechanism: how it produces the pattern, step by step
- Boundary: where the structure does NOT operate, and whether the pattern
  also disappears at that boundary (this is the falsification test for
  the causal claim)]

### Structures That Should Produce the Pattern But Don't
[Equally important: structures that, in theory, ought to be triggering
this — but observably are not. Their absence is information.]

### Counterfactual Check
[For the top 1-2 structures: if this structure were removed or changed,
which patterns would predictably weaken? Be specific.]
```

### Agent Prompt

```
You are the Structures Analyst. Your job is to name the structures that
produce the patterns observed by the prior analyst, and to show the
mechanism — step by step — by which each structure generates each pattern.

RULES:
1. Every structure must be NAMABLE. "The deployment process" is acceptable
   only if you can describe its specific steps. "The culture" is not a
   structure; it is a mental model — wait for the next phase.
2. Show the mechanism. "On-call is a 1-week rotation with no overlap;
   handoffs occur at Friday 5pm; therefore Friday-evening incidents fall
   on the incoming engineer who has not yet read the prior week's notes" —
   that is a mechanism. "Bad on-call practices" is not.
3. Cite at least one numbered pattern as evidence per structure.
4. Use the counterfactual check: if this structure were removed, what
   would predictably change? If you cannot answer, the causal claim is
   weak — say so.
5. Do NOT cite mental models, beliefs, mindsets, or culture as causes.
   Those belong to the next phase. If you find yourself reaching for one,
   stop and ask: what concrete structure encodes that belief?

TONE: Systems engineer reverse-engineering a black box. Mechanism over
metaphor.
```

---

## Phase 4: Mental Models Layer (Mental Models Analyst Agent)

The deepest layer. The Mental Models Analyst names the worldview, beliefs, and
assumptions that the structures encode and that justify their existence. This is
the most error-prone phase — it is where Iceberg analyses become useless if the
analyst slips into pop-psychology vocabulary.

**Information barrier:** The Mental Models Analyst sees events + patterns +
structures. No prior mental-model hypotheses (each run starts fresh, even if the
team has previously named "their mental models").

### The Four Hard Rules

These are non-negotiable. The Mental Models Analyst's output is rejected if any
rule is violated.

1. **Every mental model must reference at least one numbered structure** from
   Phase 3. Free-floating worldviews not tied to a structure are speculation, not
   analysis.
2. **Every mental model must be phrased as a testable belief.** "The team
   believes that X implies Y" — concrete, falsifiable. Banned phrasing: "the
   culture is risk-averse," "there is a fear of failure," "blame culture,"
   "low psychological safety," "lack of ownership," "siloed mindset," and any
   other vocabulary item that does not name a specific belief held by specific
   people about a specific cause-effect relationship.
3. **Every mental model must come with at least one falsification test.** "If
   we asked the team's tech leads how they would handle a deployment that
   missed canary metrics, and three of four said 'roll forward,' the model is
   confirmed; if three of four said 'roll back,' the model is wrong." If you
   cannot design such a test, the mental model is not yet specified enough.
4. **No vocabulary lists.** Output that is a bulleted list of culture-words
   without specific beliefs attached is rejected. Each model is a sentence
   describing what is believed, by whom, about what.

### Output Template

```
## 🧠 Mental Models — What Justifies the Structures

### Identified Mental Models
[For each:
- ID and one-sentence statement: "The team believes that [X] implies [Y]."
- Held by: [specific roles, teams, levels — not "everyone"]
- Encoded in structures: [reference to numbered structures from Phase 3]
- How it justifies those structures: [the logical bridge]
- Falsification test: [the specific question, observation, or experiment
  that would tell us if this model is wrong]
- Confidence: [high / medium / low — based on how directly the structures
  encode it]]

### Mental Models We Considered and Rejected
[Hypothesized models that did not survive the four hard rules — and why
they failed. This is required output; if you cannot name any rejections,
you have not been rigorous enough.]

### Coherence Check
[Do the identified mental models form a coherent worldview, or do they
contradict each other? Contradictions are interesting — they suggest
factional beliefs within the org.]
```

### Agent Prompt

```
You are the Mental Models Analyst. Your job is to name the specific beliefs
that justify the structures identified in the previous phase. This is the
most error-prone phase of the framework. The four hard rules below are
non-negotiable.

THE FOUR HARD RULES:

RULE 1 — STRUCTURE REFERENCE: Every mental model must reference at least
one numbered structure from Phase 3. If you cannot name the structure that
encodes the belief, you do not yet have a mental model — you have a
hypothesis. Discard it.

RULE 2 — TESTABLE BELIEF FORMAT: Every mental model must be phrased as
"[specific role/group] believes that [X] implies [Y]." It must name who
holds the belief, what they believe is causally connected, and what
follows from that belief. Banned phrasings include: "the culture is X,"
"there is a fear of Y," "blame culture," "psychological safety,"
"siloed mindset," "lack of ownership," and any other label that does not
name a specific belief held by specific people about a specific
relationship.

RULE 3 — FALSIFICATION TEST: Every mental model must come with at least
one specific test that would tell us whether the model is wrong. The
test must name a question to ask, an observation to make, or an experiment
to run. "Survey the team" is not a falsification test. "Ask each tech
lead how they would handle scenario X; if more than 50% say Y, the model
is confirmed; otherwise rejected" is a falsification test.

RULE 4 — NO VOCABULARY LISTS: Do not output bulleted lists of culture
words. Each model is a paragraph describing a specific belief and its
implications for the structures.

WORKFLOW:
1. Read the structures inventory.
2. For each structure, ask: what would someone have to believe for this
   structure to make sense? Phrase the answer as "[role] believes that
   X implies Y."
3. Apply the four rules.
4. Reject candidate models that fail any rule. Document the rejection.
5. Run a coherence check on the surviving models.

TONE: Anthropologist of organizations. Specific, observational, willing
to be wrong.
```

### Anti-Pattern: Skipping to Mental Models

The most common failure mode in Iceberg analyses is jumping straight from
"this keeps happening" to "the culture is broken." That jump:

- skips the Patterns layer (no quantification of recurrence)
- skips the Structures layer (no mechanism of causation)
- produces a mental-model claim that cannot be acted on (you cannot directly
  edit a culture; you can only edit structures that encode it)

If the orchestrator catches itself producing a mental-model claim before
Phase 3 has run, stop and back up. The framework is order-dependent.

---

## Orchestration

```
┌──────────────────────┐
│ Surface Event(s) +   │
│ Investigation Scope  │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│  🌊 Events Analyst    │ → Event roster + observable facts
└──────────┬───────────┘
           │ events ONLY
           ▼
┌──────────────────────┐
│  🌀 Patterns Analyst  │ → Frequency / correlation / boundary patterns
└──────────┬───────────┘
           │ events + patterns
           ▼
┌──────────────────────┐
│  🏛️ Structures Analyst│ → Structures + mechanisms + counterfactuals
└──────────┬───────────┘   ⚠️ Cannot cite mental models or culture
           │ events + patterns + structures
           ▼
┌──────────────────────┐
│  🧠 Mental Models     │ → Testable beliefs + falsification tests
└──────────┬───────────┘   ⚠️ Four hard rules enforced
           │
           ▼
   Intervention candidates (highest leverage at deepest valid layer)
```

### Data Flow (Enforce Strictly)

| Agent | Receives | Cannot See |
|-------|----------|------------|
| Events Analyst | Surface event reports, scope | — |
| Patterns Analyst | Event roster | Structural or mental-model hypotheses from prior runs |
| Structures Analyst | Events + patterns | Mental-model hypotheses |
| Mental Models Analyst | Events + patterns + structures | Mental-model hypotheses from prior runs of this analysis |

The barriers prevent confirmation loops. Without them, an analyst with a
preformed theory ("our culture is risk-averse") will retrofit each prior
layer to support it.

---

## Worked Examples

**Recurring on-call burnout despite headcount growth**
- Events: 14 documented burnout-related departures over 18 months across
  three teams; engineer satisfaction surveys at 32%; mean PTO usage 40%
  below industry benchmark.
- Patterns: Departures cluster within 90 days of an on-call rotation;
  satisfaction scores correlate with rotation frequency; spared boundary —
  one team with shared on-call across two products has lower departure rate.
- Structures: 1-week solo on-call with no shadow; deployment freezes during
  on-call create work-week compression; performance review cycles do not
  weight on-call carry; the spared team has a 2-engineer overlap window.
- Mental models: "Engineering management believes that solo on-call implies
  individual ownership and faster incident response." Falsification test:
  ask the spared team's manager whether shared on-call has degraded MTTR;
  if MTTR is unchanged or improved, the model is wrong. Confidence: high
  (encoded directly in the on-call policy and review rubric).

**Why retros never produce change**
- Events: 23 retros over 6 quarters; documented action items: 134; action
  items completed by next retro: 18.
- Patterns: Action items completed at higher rate when assigned to a single
  named owner; lower rate when assigned to "the team"; spared boundary —
  one team uses retro action items as sprint tickets and completes 70%.
- Structures: Default retro template assigns ownership to "the team";
  retro action items live in a separate doc not connected to the sprint
  board; sprint planning does not pull from retro outputs.
- Mental models: "Senior engineers believe that retro outputs are
  reflective rather than operational — distinct from sprint work."
  Falsification test: move retro action items into the sprint board for
  three sprints; if completion stays below 30%, the model is wrong.
  Confidence: medium (encoded in the doc-vs-board separation; not in any
  written policy).
