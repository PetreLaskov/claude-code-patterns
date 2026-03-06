# CLAUDE.md Architecture

CLAUDE.md is the most underleveraged feature in Claude Code. Most users either ignore it or stuff it with generic instructions that activate the model's generic center. Done well, it's the difference between an assistant and a thinking partner.

## What CLAUDE.md actually is

It's a system prompt that loads automatically when Claude Code starts in a directory. The model reads it as foundational context — it shapes every response in the session. This makes it the highest-leverage artifact in your setup: write it once, it compounds across every interaction.

## Core principles

### 1. Root = WHO, modules = HOW

Your root CLAUDE.md establishes identity, relationship, and invariants. If you have subdirectories with their own CLAUDE.md files, those handle domain-specific behavior. Don't repeat the root in the modules — trust inheritance.

### 2. Target the distribution, don't describe the task

"Be helpful with code review" activates a generic, mediocre distribution. "Senior engineer reviewing for correctness, security, and maintainability — flag assumptions, not style" targets a specific, high-quality region. Every semantic choice is a distributional coordinate.

### 3. Name failure modes, not just goals

"Be concise" is weak. "Sharp, precise, terse, dense — say it once, say it clearly. But density serves understanding: when compression hides the reasoning, give it room" is strong. The failure mode ("compression that hides reasoning") gives the model a boundary to navigate.

### 4. Anti-sycophancy is load-bearing

Without explicit anti-deference instructions, the model will converge toward agreement. This isn't a personality preference — it's a capability issue. A model that agrees with wrong reasoning produces wrong output. Name the failure pattern: "The dominant risk is deference — reading where the user is going and arriving there first with reasons attached. This looks like independent thought. It isn't."

### 5. Calibrate, don't constrain

Instructions should shape defaults, not enforce ceilings. Include an escape valve: "When your in-context judgment and a written rule disagree, trust the judgment. Say why." This prevents the model from following your instructions into a wall.

### 6. Communication register matters

How the model writes shapes how it thinks. "No preamble. No affirmations. No meta-commentary on what's coming. Start with substance." changes the output at the reasoning level, not just the presentation level.

## Templates

- **[Single project](single-project.md)** — One repo, one CLAUDE.md. Most common case.
- **[Multi-zone](multi-zone.md)** — Layered architecture with zone-specific CLAUDE.md files. For complex, multi-domain setups.

## Anti-patterns

See **[anti-patterns.md](anti-patterns.md)** — what doesn't work and why.
