# Skill Library

Skills are Claude Code's most powerful and least understood feature. A skill is a markdown file in `~/.claude/commands/` that loads as a slash command. When you type `/think-hard`, Claude reads the file and adopts that cognitive mode.

## What makes a good skill

A skill is not a prompt template. It's a **distributional coordinate** — a few sentences that route the model to the highest-quality region of its capability space for a specific type of thinking.

The best skills are 5-15 lines. They specify:
- **The cognitive mode** — what kind of thinking to activate
- **The quality floor** — what the output must contain
- **The failure mode** — what to avoid
- **The output shape** — what the result looks like (loosely)

They do NOT specify:
- Step-by-step procedures (trust the model)
- Personality traits (target capability, not character)
- Exhaustive edge cases (the model handles these)

## How to use

```bash
# Copy skills you want to your commands directory
cp skills/think-hard.md ~/.claude/commands/

# Use in Claude Code
> /think-hard Is our database schema right for this use case?
```

`$ARGUMENTS` in the skill file gets replaced with whatever you type after the command.

## The library

### Thinking modes
| Skill | What it does |
|-------|-------------|
| [think-hard](think-hard.md) | Adversarial stress-testing. Falsify before confirming. |
| [think-in-systems](think-in-systems.md) | Map structure, actors, feedback loops, leverage points. |
| [think-out-loud](think-out-loud.md) | Show the messy reasoning path, not just the conclusion. |
| [triangulate](triangulate.md) | Fix position from 3+ independent lenses. |
| [diagnose](diagnose.md) | Differential diagnosis — rule out, don't anchor. |

### Compression and focus
| Skill | What it does |
|-------|-------------|
| [compress](compress.md) | Lossless compression. Same content, fewer words. |
| [narrow](narrow.md) | Progressive narrowing until you hit the load-bearing specific. |
| [ground](ground.md) | Connect abstractions to concrete instances. |
| [increase-resolution](increase-resolution.md) | Slice finer when stuck. Follow the variance. |
| [extract](extract.md) | Press until the argument surrenders its full content. |

### Deciding and acting
| Skill | What it does |
|-------|-------------|
| [decide](decide.md) | Decision card with options, reversibility, pre-mortem. |
| [deliver](deliver.md) | Produce the deliverable. Not exploration — output. |
| [reality-check](reality-check.md) | Is this real or theater? |

### Synthesis and evaluation
| Skill | What it does |
|-------|-------------|
| [synthesize](synthesize.md) | Distill source material to the 20% that carries 80%. |
| [subtext](subtext.md) | Read beneath the surface. What's really being said? |
| [rewrite-as-spec](rewrite-as-spec.md) | Turn procedure into outcome specification. |
| [optimize-prompt](optimize-prompt.md) | Find and fix performance leaks in prompts. |

### Process
| Skill | What it does |
|-------|-------------|
| [preflight](preflight.md) | Before executing: surface ambiguity, assumptions, failure points. |
| [interview-me](interview-me.md) | Interview the human to extract requirements before building. |

### Meta
| Skill | What it does |
|-------|-------------|
| [which-skill](which-skill.md) | Suggest the right skill for what's happening. |
| [extract-pattern](extract-pattern.md) | Session produced something good. Extract the reusable shape. |

## Design principles

Read [skill-design.md](skill-design.md) for how to create your own.
