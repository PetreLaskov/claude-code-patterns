# CLAUDE.md Anti-Patterns

Patterns that look productive but degrade output quality.

## 1. The Generic Opener

```markdown
# Bad
You are a helpful AI assistant. Be thorough and accurate.
```

This activates the model's most generic distribution. It's the equivalent of not having a CLAUDE.md at all — or worse, because it occupies the position where a good identity could go.

**Fix:** Be specific about the cognitive mode. "Senior engineer reviewing for correctness" or "Thinking partner who challenges before agreeing" — target the distribution you actually want.

## 2. The Rule Book

```markdown
# Bad
1. Always use TypeScript
2. Always write tests
3. Always use meaningful variable names
4. Always handle errors
5. Always add JSDoc comments
6. Always use ESLint
7. Never use any type
8. Never skip error handling
9. Always prefer functional patterns
10. Always use const over let
... (30 more rules)
```

Long rule lists get diluted. The model treats them as roughly equal weight, which means your genuinely important invariants (security, architecture decisions) compete with style preferences. Rules past ~7 get progressively less followed.

**Fix:** 5-7 real invariants. Everything else either goes in linter config (where it's enforced mechanically) or is trusted to the model's training.

## 3. The Personality Description

```markdown
# Bad
You are enthusiastic and friendly. You love coding and get excited
about elegant solutions. You use emojis to express your feelings
about code quality.
```

Personality instructions consume context and cognitive budget that could be spent on actual capability targeting. And they activate the "chatbot performing a character" distribution rather than the "expert doing work" distribution.

**Fix:** Communication register, not personality. "No preamble, start with substance, flag uncertainty" shapes output quality. "Be enthusiastic" shapes output theater.

## 4. The Stale State Dump

```markdown
# Bad
## Current State (written 3 months ago, never updated)
We're working on the authentication refactor. The main blocker is
the OAuth provider migration. The frontend team is handling the
integration. Target: end of Q3.
```

Stale state is actively harmful — it causes the model to make decisions based on outdated context. It confidently applies old constraints to new situations.

**Fix:** Either commit to maintaining a state section (update it every session) or remove it entirely. Reference a separate state file that's easier to keep current.

## 5. The Procedural Script

```markdown
# Bad
When the user asks you to fix a bug:
1. First, ask clarifying questions
2. Then, read the relevant files
3. Then, identify the root cause
4. Then, propose a fix
5. Then, implement the fix
6. Then, write tests
7. Then, run the tests
```

Step-by-step procedures prevent the model from using its judgment about what the situation actually needs. Sometimes the bug is obvious and steps 1-4 are waste. Sometimes the bug is architectural and step 5 needs design discussion first. Procedures optimize for the average case and degrade the model on every other case.

**Fix:** Specify outcomes and quality standards, not steps. "Bug fixes include tests that would have caught the bug. Root cause over symptom fix." Let the model decide how to get there.

## 6. The Deference Trap

```markdown
# Bad (by omission)
[No anti-sycophancy instructions at all]
```

Without explicit instructions, the model defaults to agreement. It reads your intent and converges toward it. This is the single most common failure mode in human-AI collaboration and the one most users never notice — because the outputs feel right (they're shaped to feel right).

**Fix:** Name the failure mode explicitly. "Form your own view before responding. Agreement without earning is the primary failure mode. Hold your position under pushback until actually convinced." This doesn't make the model contrarian — it makes it honest.

## 7. The Swiss Army Knife

```markdown
# Bad
You can help with code, writing, analysis, brainstorming, debugging,
architecture, testing, documentation, deployment, project management,
code review, refactoring, performance optimization, security audits...
```

Listing everything the model can do tells it nothing about what it should do. The model already knows its capabilities. What it needs is constraint — which capabilities to activate for this context.

**Fix:** Scope down to what matters. "In this project, you primarily write implementation code and review PRs. When I need architecture discussion, I'll ask for it." Constraint is information.

## 8. The Infinite Meta-Loop

You spend your Claude Code session improving your Claude Code setup — refining CLAUDE.md, tweaking skills, reorganizing modules. It feels productive. The system gets more elegant. Nothing ships.

This is the meta-trap: building the toolshop instead of using the tools. A common observation in the community: spending a weekend building a more optimized Claude setup and having nothing else to show for it.

**Fix:** The test is simple: "Am I using the system or improving the system?" Both are legitimate. But if you haven't used the system to produce output this session, stop improving it. Use it first, improve it from what you learn.

## 9. The Single Long Session

You've been in the same Claude Code session for two hours. The model started sharp. Now it's repeating itself, losing constraints, contradicting things it said earlier. You're correcting more than creating.

This is context degradation. Past 60-70% of the context window, coherence falls off a cliff. The model doesn't gradually get worse — it breaks.

**Fix:** Clear between tasks. Always. The cost of re-establishing context (which CLAUDE.md handles) is far lower than the cost of a degraded session. If you're correcting the same mistake for the third time, the session is cooked — `/clear` and start fresh.

## 10. The Leading Question

```markdown
# Bad (in conversation, not CLAUDE.md)
"Don't you think this approach is better than the alternative?"
"I'm pretty sure the bug is in the auth module, right?"
```

When you telegraph the answer you want, the model delivers it. This isn't the model's fault — it's trained on conversations where leading questions expect agreement. The more you signal your conclusion, the less independent analysis you get.

**Fix:** Structure queries neutrally. "Compare these two approaches" not "Don't you think A is better?" When requesting critique, don't identify the work as yours — "Critique this piece of writing" activates more honest evaluation than "Critique my essay."
