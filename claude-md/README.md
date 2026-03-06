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

But register is bidirectional — how YOU write shapes how the model responds. Erudite, precise language gets substantive, precise responses. Casual shorthand gets casual output. Your linguistic register implicitly prompts the level of the entire interaction.

### 7. CLAUDE.md is compound interest

Every mistake Claude makes, every preference you discover, every domain-specific rule — encode it. A well-maintained CLAUDE.md eliminates entire categories of errors permanently rather than fixing them one instance at a time. The habit: every time the model does something unwanted, ask "Is this a prompt problem?" If yes, fix the system, not the output.

## The competent stranger test

When writing CLAUDE.md or any prompt, use this diagnostic (from Amanda Askell, Anthropic):

> Imagine you've hired a temp agency to send someone to do a task. This person arrives, and you know they're pretty competent. They know a lot about your industry, but they don't know the name of your company. What would you say to that person?

Whatever you'd tell the competent stranger — that's what belongs in your CLAUDE.md. What you'd assume they already know — leave it out. What you'd show them before they start — that's your reference material.

## Templates

- **[Single project](single-project.md)** — One repo, one CLAUDE.md. Most common case.
- **[Multi-zone](multi-zone.md)** — Layered architecture with zone-specific CLAUDE.md files. For complex, multi-domain setups.

## Anti-patterns

See **[anti-patterns.md](anti-patterns.md)** — what doesn't work and why.
