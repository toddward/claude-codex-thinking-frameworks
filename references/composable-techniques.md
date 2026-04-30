# Composable Techniques — Cross-Cutting Reference

## What This Is

These are not standalone frameworks. They are short, paste-able rules that plug
into any first-class framework's agent prompts to sharpen specific reasoning
patterns. Unlike the multi-agent frameworks (Dialectical, Six Hats, etc.), each
technique is a single rule applied to a single agent within a chain.

Use them when:
- An advocate role keeps producing weak straw-man defenses (apply Steel-manning)
- A creative or generative agent keeps proposing variations of the same idea
  (apply Inversion)
- A First Principles teardown is about to remove something whose original purpose
  is unclear (apply Chesterton's Fence)

Each entry below is structured: **Definition → When to apply → Prompt snippet to
inject → Anti-patterns**. Snippets are written to be copy-pasted into agent
prompts verbatim.

---

## 1. Steel-manning

### Definition

Constructing the strongest possible version of an opposing argument before
critiquing it, rather than the weakest convenient version (the straw-man). The
discipline is asymmetric: it requires the agent to *strengthen* the position they
are about to argue against.

### When to Apply

- **Dialectical / Advocate role** — to prevent the Advocate from defending against
  a hypothetical weak Challenger and missing the strong objections
- **Six Hats / Yellow Hat** — to ensure benefits are argued against the *strongest*
  reading of risks, not the easiest-to-dismiss reading
- **First Principles / Architect role** — to ensure the Architect's clean-slate
  rebuild has reckoned with the strongest case the original implementation could
  make for itself
- **Pre-mortem / Mitigation Synthesizer** — to ensure mitigations address the
  strongest reading of each persona's diagnosis, not the weakest

### Prompt Snippet to Inject

```
STEEL-MANNING REQUIREMENT:
Before defending or advancing this position, you must articulate the strongest
possible version of the opposing position. Specifically:

1. State the opposing position in one sentence — the version a senior, hostile,
   well-informed reviewer would make, not the easiest version to refute.
2. Identify the two strongest pieces of evidence the opposition would cite.
3. Identify the one concession your position must make to acknowledge what the
   opposition gets right.
4. Only THEN proceed to defend your position — and defend it against the
   strongest version stated above, not against a weaker version of convenience.

If your defense only addresses a weaker version of the opposition, the response
is incomplete and must be rewritten.
```

### Anti-patterns

- **Performative steel-manning**: stating a strong opposition in one paragraph,
  then ignoring it in the actual defense. The snippet's last clause guards
  against this — enforce it.
- **Steel-manning at the wrong layer**: applying it to the Challenger role
  defeats the purpose; the Challenger is supposed to be adversarial. Steel-manning
  belongs on the *advocacy* side of any structured tension.
- **Steel-manning in solo reasoning**: in a single-agent prompt, asking the
  model to "consider the opposing view" produces hand-waving. Steel-manning
  works best when there is a defined position to be argued, not a survey
  question.

---

## 2. Inversion (Munger / Jacobi)

### Definition

Restating a forward problem as its inverse, generating the failure list, and
then converting each failure-mode into a corresponding positive action. Carl
Jacobi's principle, popularized by Charlie Munger: "Invert, always invert."
Forward thinking is constrained by optimism and momentum bias; inversion is
constrained by neither.

### When to Apply

- Any framework where forward thinking has stalled or is producing variations on
  one theme
- **First Principles / Archaeologist** — invert "what assumption is this?" to
  "what would prove this is *not* a fundamental truth?"
- **Six Hats / Green Hat** — invert "what new ideas?" to "how would we guarantee
  failure at the current goal?" (often surfaces wilder genuine alternatives)
- **Pre-mortem amplifier** — Pre-mortem is itself a structured inversion; the
  snippet here can be applied within Pre-mortem's persona prompts to push
  causes into more specific failure modes
- **Strategic reasoning** — inverting "how do we win?" to "how do our
  competitors win?" surfaces moves not reachable from the forward question

### Prompt Snippet to Inject

```
INVERSION REQUIREMENT:
Before producing your final output, run this inversion pass:

1. Restate the problem as its opposite. Convert "How do we succeed at X?" into
   "How would we guarantee failure at X?"
2. Generate a list of 5–7 failure modes — each specific, each tied to a real
   mechanism. "How would a hostile or incompetent actor sabotage this?"
3. For each failure mode, name the inverse: the specific action that would
   prevent that exact failure.
4. Compare the inverted list against your forward output. Did the inversion
   surface anything your forward reasoning missed? If yes, integrate it. If no,
   confirm the forward output is robust.

This is not a separate analysis — it is a stress test on the analysis you would
have produced anyway.
```

### Anti-patterns

- **Inverting once and not integrating**: the inversion is a *test*; the output
  must reflect what the test revealed. The snippet's step 4 enforces this.
- **Trivial inversion**: "the inverse of writing this code is not writing this
  code" — generates no signal. Push the inversion to a *mechanistic* level:
  what would an adversary do, what would a careless implementation do, what
  would a hostile market do?
- **Inverting too early**: in a generative phase (Green Hat ideation), inversion
  before the forward generation has produced its best output collapses creativity
  prematurely. Use it as a stress test on a draft, not as a starting prompt.

---

## 3. Chesterton's Fence

### Definition

G.K. Chesterton's principle: do not remove a fence (or rule, policy, structure)
until you understand why a reasonable person installed it. The technique is a
*gate* that fires before structural removals or simplifications. It does not
prevent change; it prevents ill-informed change.

### When to Apply

- **First Principles / Archaeologist or Architect** — before declaring a
  structure an "unmasked assumption" or before the Architect's reconstruction
  omits something the original had
- **Iceberg / Structures Analyst** — before recommending a structural removal
  as an intervention; the removal might be load-bearing in ways the analysis
  has not surfaced
- **Refactoring decisions** — before deleting unused-looking code, deprecated-
  looking feature flags, or dormant policies
- **Process simplification** — before removing review steps, approval gates, or
  observability rituals that "no one uses"

### Prompt Snippet to Inject

```
CHESTERTON'S FENCE GATE:
Before you recommend removing or simplifying [policy / process / structure / code
/ rule X], you must answer:

1. Who installed it? When? In response to what specific event or risk?
2. What was the original justification — even if it is no longer in force? If
   you cannot reconstruct the original reasoning from documents, commits, change
   tickets, or knowledgeable interviews, you do NOT have permission to remove it
   yet.
3. What residual function might it still be serving that is not obvious from
   surface inspection? (Examples: regulatory cover, audit trail, undocumented
   integration dependency, training-wheel for new staff.)
4. If the original justification is genuinely obsolete AND no residual function
   exists, remove it. Otherwise, document the residual function and either
   preserve the structure or design a replacement that covers it.

Recommendations to remove without satisfying this gate must be flagged as
"removal blocked: original purpose not reconstructed."
```

### Anti-patterns

- **Chesterton's Fence as veto**: the principle is a gate, not a permanent
  blocker. If the original purpose can be reconstructed and is genuinely
  obsolete, remove the structure. The point is to prevent *uninformed* removal,
  not all removal.
- **Inverted fence**: applying it to additions ("do not add a fence until you
  understand why it does not exist"). That is not Chesterton's principle and
  inverts the bias the principle is correcting.
- **Fence everywhere**: applying the gate to every change halts work. Reserve
  it for *removals* of structures with non-obvious residual function. Do not
  fire it on greenfield decisions or on removals where the residual function
  is documented and understood.

---

## How to Use These Together

These techniques compose with each other inside a single agent prompt:

- **Dialectical / Advocate** can use Steel-manning to construct the strongest
  Challenger position, then Inversion as a final stress test.
- **First Principles / Architect** can use Chesterton's Fence as a gate before
  omitting a component the original had, then Inversion to ask "how would the
  reconstruction fail?"
- **Iceberg / Structures Analyst** can use Chesterton's Fence before
  recommending structural removal, ensuring the removal does not break a
  load-bearing function the surface analysis missed.

Add the snippets directly to the relevant agent's prompt. They are designed to
be additive: a base prompt plus one or more technique snippets.
