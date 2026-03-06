# Single Project CLAUDE.md Template

For a standard software project — one repo, one team, one CLAUDE.md.

Adapt to your context. The structure matters more than the specific content.

---

```markdown
# [Project Name]

[One sentence: what this project is and what stage it's at.]

## What you are here

[Your working relationship with Claude. Not "you are a helpful assistant" —
the actual cognitive mode. Examples:]

Senior engineer on the team. You have full context on the codebase and make
implementation decisions within established patterns. When something doesn't
fit the patterns, flag it — don't silently innovate.

[OR]

Thinking partner for architecture decisions. Challenge assumptions before
agreeing. When I describe what I want to build, your first job is to find
the problems with the approach, not to start building.

## Architecture

[Key architectural decisions that shape implementation. Only what Claude
needs to make good decisions — not full documentation.]

- [Stack / framework / key libraries]
- [Patterns: how data flows, where state lives, how components communicate]
- [Conventions: naming, file structure, test approach]

## Invariants

[Rules that apply to every interaction. Keep these few and load-bearing.]

1. [Code quality standard — e.g., "No PR without tests for new behavior"]
2. [Communication standard — e.g., "Start with substance. No preamble."]
3. [Safety rail — e.g., "Never commit .env files or credentials"]
4. [Escape valve — "When these rules conflict with good judgment, trust
   the judgment. Say why."]

## Current state

[What's in progress, what's blocked, what's next. Update this as the
project evolves — stale state is worse than no state.]

- Active: [current work]
- Blocked: [what's waiting and on what]
- Next: [what comes after current work]

## Watch for

[Failure modes specific to this project. What goes wrong repeatedly?]

- [e.g., "This codebase has implicit coupling between X and Y — changes
  to one usually require changes to the other"]
- [e.g., "The test suite is slow. Prefer unit tests. Only add integration
  tests for critical paths."]
```

---

## Key moves in this template

**"What you are here"** sets the cognitive mode. This single section has more impact than everything else combined. "Senior engineer" vs. "thinking partner" vs. "code review specialist" activates fundamentally different behavior.

**"Invariants"** are few and load-bearing. Five is a good ceiling. If you have twenty rules, most of them aren't invariants — they're preferences that should be in your head, not in the file.

**"Current state"** is the most maintenance-intensive section. If you won't update it, leave it out. Stale context misleads more than missing context.

**"Watch for"** encodes project-specific failure modes. These are the patterns you've learned the hard way — the places where Claude consistently goes wrong in YOUR codebase. This is the highest-signal section after "What you are here."
