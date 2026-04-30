# Claude/Codex Thinking Frameworks

Structured thinking frameworks for agent-assisted analysis, decision-making, and problem solving.

This repository contains a reusable skill definition plus reference material for running rigorous multi-perspective reasoning workflows. It also includes a Gemini Enterprise agent setup that maps the same frameworks into an orchestrator plus specialized sub-agents.

## What's Included

- `SKILL.md` - Source skill definition for Claude Code/Codex-style skill installation.
- `thinking-frameworks.skill` - Packaged skill artifact.
- `references/` - Complete framework references and prompt patterns.
- `gemini-enterprise/` - Gemini Enterprise orchestrator and sub-agent setup files.

## Frameworks

| Framework | Use When |
| --- | --- |
| Dialectical | You need to evaluate a binary choice, architecture debate, vendor selection, or competing approaches. |
| Six Thinking Hats | You need broad stakeholder-style perspective coverage for go/no-go decisions, post-mortems, or cross-functional analysis. |
| First Principles | You need to strip inherited assumptions and rebuild an approach from fundamentals. |
| Collision-Zone | You are stuck and need creative breakthroughs by combining distant domains. |
| Cynefin | You need to classify what kind of problem you have before choosing how to solve it. |
| Pre-mortem | You want to imagine a future failure before committing to a project, launch, or major decision. |
| Iceberg | You need to trace recurring incidents from events to patterns, structures, and mental models. |

The repo also includes composition patterns for chaining frameworks and composable techniques such as steel-manning, inversion, and Chesterton's Fence.

## Repository Layout

```text
.
├── SKILL.md
├── thinking-frameworks.skill
├── references/
│   ├── composable-techniques.md
│   ├── composition-patterns.md
│   ├── cynefin.md
│   ├── dialectical.md
│   ├── first-principles.md
│   ├── iceberg.md
│   ├── pre-mortem.md
│   └── six-hats.md
└── gemini-enterprise/
    ├── 00-orchestrator.md
    ├── 01-dialectical-engine.md
    ├── 02-six-hats-engine.md
    ├── 03-first-principles-engine.md
    ├── 04-collision-zone-engine.md
    ├── 05-cynefin-engine.md
    ├── 06-pre-mortem-engine.md
    ├── 07-iceberg-engine.md
    └── SETUP-GUIDE.md
```

## Using the Skill

Use `SKILL.md` as the source definition for local skill installation or development. The skill activates when a user asks for structured reasoning such as:

- "Think this through."
- "What are the tradeoffs?"
- "Run a pre-mortem."
- "Use first principles."
- "What are we missing?"
- "Why does this keep happening?"

The skill chooses an appropriate framework, or uses Cynefin triage when the problem type is ambiguous.

## Gemini Enterprise Setup

The `gemini-enterprise/` directory contains a manual setup for Gemini Enterprise:

1. Create the parent `Thinking Frameworks` agent from `00-orchestrator.md`.
2. Create each framework engine from `01-*.md` through `07-*.md`.
3. Upload the relevant files from `references/` as knowledge for the orchestrator and sub-agents.
4. Follow the full instructions in `gemini-enterprise/SETUP-GUIDE.md`.

The setup uses an orchestrator to classify requests, route work to specialized engines, enforce information barriers, and synthesize final recommendations.

## Development Notes

- Edit `SKILL.md` and the markdown files in `references/` as source material.
- Keep the Gemini Enterprise files aligned with framework changes when prompts or routing logic change.
- Regenerate or replace `thinking-frameworks.skill` when publishing a new packaged version.
- Preserve information barriers between framework phases; they are central to the quality of the analyses.

## License

No license file is currently included. Add one before distributing this repository broadly.
