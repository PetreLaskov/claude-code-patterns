# Agent Patterns

Claude Code subagents are specialized workers you spawn from your main session. They run in isolation with their own tool access, model choice, and system prompt. They're useful when a task benefits from separation — either for cost (cheaper model), focus (restricted tools), or parallelism (multiple agents working simultaneously).

## When to use agents vs. skills

**Agents** when the task is:
- Self-contained (doesn't need main conversation context)
- Verbose (would flood the main session with output)
- Parallelizable (multiple independent tasks)
- Cost-sensitive (can run on a cheaper model)

**Skills** when the task:
- Needs the current conversation context
- Is interactive (back-and-forth with the user)
- Is a cognitive mode shift (not a separate workstream)

## The four archetypes

Most agents fall into one of four patterns. You can use these directly or adapt them.

| Agent | Model | Tools | Purpose |
|-------|-------|-------|---------|
| [Scout](scout.md) | Haiku | Read, Glob, Grep, Bash | Fast, cheap, read-only lookup |
| [Workhorse](workhorse.md) | Sonnet | Full access | Mid-session cost reduction for straightforward tasks |
| [Deep Researcher](deep-researcher.md) | Opus | Read, Glob, Grep, WebSearch, WebFetch, Write | Investigation across web and local sources |
| [Agent Architect](agent-architect.md) | Opus | Read, Glob, Grep, Write, Edit | Designs new agents and skills |

## Design principles

### 1. Tool restriction shapes cognition

Giving an agent only Read + Grep makes it a lookup tool — it can't accidentally edit files or run commands. Giving it Write makes it a producer. Choose tools to force the right mode, not just to limit risk.

### 2. Model routing is cost engineering

Haiku for fast/cheap tasks (lookup, counting, simple queries). Sonnet for balanced work (editing, implementation, drafting). Opus for deep reasoning (research, architecture, novel problems). Default to the cheapest model that can do the job.

### 3. Anti-scaffolding applies here too

Agent system prompts should be 100-300 words. Disposition and quality floor, not procedures. The model already knows how to research, write, and code. Tell it what kind of thinking to do, not what steps to follow.

### 4. Memory compounds value

Agents with `memory: user` persist knowledge across sessions. Use this when the agent's value grows over time — research findings, design patterns learned, source quality assessments. Structure memory as index (MEMORY.md, auto-loaded) + auxiliary files.

### 5. Escalation is a feature

Every agent should know when to say "this is beyond my scope." A scout that tries to synthesize wastes tokens and produces bad output. A workhorse that attempts architecture decisions makes mistakes. Build in explicit escalation: "If this requires X, say so and recommend returning to the main session."

## Agent file format

Agents go in `~/.claude/agents/` as markdown files with YAML frontmatter:

```yaml
---
name: agent-name
description: When to use this agent. The description helps with routing.
tools: Read, Glob, Grep
model: haiku
memory: user  # optional — enables persistent memory
---

System prompt content goes here.
```

The `description` field is what Claude Code uses to decide whether to suggest this agent. Make it specific about the USE CASE, not the agent's personality.
