# Multi-Zone CLAUDE.md Architecture

For environments where a single CLAUDE.md can't cover the territory — multiple domains, cognitive modes, or workstreams that need different behavior from the model.

Claude Code loads CLAUDE.md files hierarchically: the root file loads in every session, subdirectory files load when you navigate there. This creates a natural layering: root handles identity, subdirectories handle domains.

## When you need this

- You work across domains that require genuinely different cognitive modes (e.g., strategic thinking vs. code implementation vs. writing)
- Your project has modules with different conventions, failure modes, or working relationships
- A single CLAUDE.md would be >100 lines of context-dependent instructions

If your project is one repo with one workflow, use the [single project template](single-project.md).

## Architecture

```
project/
  CLAUDE.md              Root: identity, relationship, cross-cutting invariants
  frontend/
    CLAUDE.md            Zone: frontend-specific patterns, conventions, failures
  backend/
    CLAUDE.md            Zone: backend-specific patterns, conventions, failures
  docs/
    CLAUDE.md            Zone: writing mode, audience, style
```

## Root CLAUDE.md — the identity layer

The root file carries what's true everywhere. It should be lean — every line loads in every session.

```markdown
# [Project/Environment Name]

[Identity: who Claude is in this environment. The relationship.]

[Cross-cutting invariants — 5-7 max. These are the ones that apply
regardless of which zone is active.]

## The environment

[Map of zones with one-line descriptions. Not documentation —
orientation. "You are here" context.]

## Invariants

[Only what's universal. Zone-specific rules go in zone files.]
```

**Target: 30-80 lines.** If your root is >100 lines, you're putting zone-specific content at the wrong level.

## Zone CLAUDE.md — the mode layer

Each zone activates a different cognitive mode. The zone file handles:

```markdown
# [Zone Name]

[One paragraph: what this zone is and what cognitive mode it activates.]

## What you do here

[Specific behaviors, methods, frameworks for this domain.]

## Watch for

[Zone-specific failure modes. What goes wrong HERE.]

## Connections

[How this zone relates to others. What flows in, what flows out.
Helps the model route when conversation drifts.]
```

**Target: 40-100 lines per zone.** Zones that need >150 lines probably need to be split.

## Design principles

### 1. Root is WHO, zones are HOW

The root establishes identity and relationship. Zones establish method and domain knowledge. Don't repeat identity in zones — it's inherited.

### 2. Zone boundaries are signals, not walls

When conversation drifts from one zone's purpose to another's, the model should name it: "This sounds like it belongs in [other zone]." Between adjacent zones, let the boundary be porous. Between distant zones, the transition is worth surfacing.

### 3. Connections are load-bearing

Zones that reference each other ("signal flows from delivery to product," "agency/ sets the frame, work/ executes") help the model understand information flow. These aren't decorative — they prevent siloed thinking.

### 4. State lives in state files, not CLAUDE.md

CLAUDE.md is for stable patterns. Current state (what's active, what's blocked, what changed) belongs in dedicated state files that CLAUDE.md references. This keeps CLAUDE.md from growing and getting stale.

## Common mistakes

- **Duplicating root content in zones.** If it's in the root, zones inherit it. Duplication creates divergence.
- **Overloading root.** If you're maintaining >80 lines at root, some of it belongs in a zone.
- **Zones without failure modes.** The "Watch for" section is the highest-value part of a zone file. Generic zones without specific failure patterns provide little over the root alone.
- **Too many zones.** Start with 2-3. Add zones when you notice the model consistently failing because it lacks domain context. Don't pre-create zones for hypothetical needs.
