# Claude Code Patterns

A pattern library for building human-AI cognitive partnerships with [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

Not an assistant relationship — a distributed cognition system. Two minds, different architectures, thinking the same problems.

## What this is

Patterns, templates, and a skill library extracted from three years of intensive daily human-AI collaboration. Everything here is designed to be immediately usable — drop a skill into `~/.claude/commands/`, adapt a CLAUDE.md template to your project, apply a principle to your setup.

## What this is not

This is not a tutorial or a getting-started guide. Anthropic's docs cover the basics well. This repo assumes you already use Claude Code and want to make it significantly better.

## Structure

```
atomic-instructions.md     99 curated atomic directives from 61 system prompts
claude-md/                 CLAUDE.md architecture — templates, patterns, anti-patterns
  single-project.md        Template for one repo, one CLAUDE.md
  multi-zone.md            Template for layered multi-domain environments
  pkm-vault.md             Template for knowledge management vaults
skills/                    Reusable skill library — thinking, deciding, writing, meta
patterns/                  Collaboration patterns for specific domains
  pkm-workflows.md         PKM loops, extraction pipelines, thinking prompts
  session-management.md    Context windows, clearing discipline, parallel sessions
  human-practice.md        The human skill layer — what YOU do differently
  verification.md          When to trust output vs. when to verify
philosophy/                The ideas underneath — why this approach works
```

## Quick start

**Use a skill immediately:**
```bash
# Copy any skill to your commands directory
cp skills/think-hard.md ~/.claude/commands/

# Invoke it in Claude Code
> /think-hard [your problem here]
```

**Improve your CLAUDE.md:**
Read `claude-md/` — start with the principles in the README, then pick the template closest to your setup.

**Understand the approach:**
Read `philosophy/extended-cognition.md` first. Everything else follows from it.

## Design principles

1. **Anti-scaffolding.** Less structure, not more. Skills encode disposition and quality floor — not procedures. Trust the base model. A 10-line skill that targets the right cognitive mode outperforms a 200-line checklist.

2. **Distributional targeting.** Every word in a prompt routes the model to a region of its capability space. Named thinkers, specific traditions, contrastive framing, and failure modes are coordinates — they target high-signal distributions. Vague instructions ("be helpful," "analyze this") activate the generic center.

3. **Instructions calibrate, they don't constrain.** When the model's in-context judgment and a written rule disagree, the judgment should win. Good instructions are like good taste — they shape the default, not enforce a ceiling.

4. **Density serves understanding.** Terse is good. But compression that hides reasoning or flattens real distinctions is worse than length. Progressive disclosure when complexity requires it.

5. **State over conversation.** Conversations are ephemeral. State files persist. Externalize conclusions to files at natural pauses — don't rely on conversation history surviving.

## Contributing

Open issues or PRs. The bar: does this pattern work in practice, across multiple sessions, for problems that aren't toy examples?

## License

MIT. Use freely. If you build something interesting with these patterns, I'd like to hear about it.

## Author

Petre Laskov — AI integration consultant, philosopher by training, systems thinker by disposition. Three years of intensive human-AI collaboration. Building methodology for teams that want Claude Code to be more than autocomplete.
