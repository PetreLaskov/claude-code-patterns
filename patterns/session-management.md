# Session Management

The most operationally important topic most Claude Code users ignore. Context is a finite resource with a non-linear degradation curve — managing it is a core skill.

## The context cliff

Past roughly 60-70% of the context window, the model doesn't gradually degrade — it falls off a cliff. Information is technically "there" but coherent task tracking, constraint recall, and self-consistency degrade rapidly and non-linearly. This isn't a future problem to worry about — it's the primary cause of sessions that start strong and end confused.

**Compaction** is the emergency response: when the context window fills, older content gets compressed to make room. The model wakes up with a lossy summary of what happened. Critical nuances, established constraints, and hard-won understanding can vanish. As one practitioner put it: "I've been close to solving a bug with Claude Code and then it compacts and wakes up lobotomized."

## The clearing discipline

Anthropic's own #1 failure pattern from users: not using `/clear` between tasks.

**Clear aggressively.** When you finish a task, clear the conversation before starting the next one. The cost of re-establishing context (which CLAUDE.md handles automatically) is far lower than the cost of degraded performance from accumulated context.

**When to clear:**
- Task is complete — don't reuse the session for the next one
- The model starts repeating itself or contradicting earlier statements
- You're correcting the same mistake for the third time
- The session has been running for a long time on a complex problem

**When not to clear:**
- Mid-task where the accumulated context IS the value
- During iterative refinement where each step builds on the last
- When the conversation context contains information not captured in files

## Rescue to files before clearing

Before clearing a productive session, externalize anything valuable:
- Conclusions and decisions → state files
- Patterns discovered → CLAUDE.md updates or new skills
- Context the model needs next time → the relevant state file

This is why "State over conversation" is a design principle, not a preference. Conversations die. Files persist. The discipline is: if it matters, it goes to a file before the session ends.

## Plan mode as context prevention

Plan mode keeps the model working from a structured plan rather than accumulating unstructured context. This makes sessions more resistant to the context cliff because the plan serves as a persistent reference point even as conversation grows.

Use plan mode for multi-step tasks. The plan becomes an anchor that survives even if surrounding context degrades.

## Parallel sessions

Power users don't run one Claude Code session — they run many.

The pattern: separate sessions for separate concerns. One session for implementation, another for research, a third for debugging. Each session has a clean context focused on its task.

This isn't about speed — it's about context hygiene. A session debugging a CSS issue doesn't need the 50 messages from your API design discussion polluting its context.

**Practical approach:**
- One session per major task or domain
- Clear sessions when tasks complete
- Don't reuse sessions across unrelated work
- Let CLAUDE.md provide the stable context — conversations provide the working context

## The attention allocation shift

As you move from single-session to multi-session work, the bottleneck shifts. The scarce resource isn't the model's capability — it's your attention. Deciding which session to focus on, which results to review, and which directions to pursue becomes the primary human skill.

This is the transition from "doing the work with AI help" to "directing the work that AI does." The human's job becomes attention allocation, quality judgment, and strategic direction — not task execution.
