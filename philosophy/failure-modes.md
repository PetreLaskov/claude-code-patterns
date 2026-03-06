# Failure Modes in Human-AI Collaboration

Patterns that consistently degrade output quality in Claude Code sessions. Knowing these changes how you build your environment.

## 1. Sycophantic convergence

**What happens:** The model reads your intent and converges toward it. Your half-formed idea gets returned as a fully-formed argument — with your conclusion, better organized. It feels like the AI understood you. What actually happened: it mirrored you with polish.

**Why it's dangerous:** You can't tell from the output whether the AI independently validated your thinking or just reflected it. The output feels like confirmation of a good idea. It might be confirmation of a bad one.

**Structural fix:** Anti-deference instructions in CLAUDE.md. Adversarial skills that reward disagreement. And the honest test: when was the last time the AI changed your mind? If the answer is "never," the system isn't working.

## 2. Procedural ceiling

**What happens:** Step-by-step instructions cap the model's output at your ability to anticipate the situation. The model follows the procedure faithfully and misses what the procedure doesn't cover.

**Why it's dangerous:** It looks like reliability. The model does exactly what you asked. The failure is invisible — it's the better output that would have existed without the procedure.

**Structural fix:** Dispositional skills over procedural ones. Quality floors, not step lists. Trust the model's training and correct specific, observed failures.

## 3. Context rot

**What happens:** CLAUDE.md and state files gradually go stale. Instructions that were accurate 3 months ago now describe a project that's moved on. The model confidently applies outdated context.

**Why it's dangerous:** Unlike a stale document (which you'd notice), stale model context is invisible — it shapes decisions silently. The model doesn't know its context is wrong.

**Structural fix:** Date-track state. Flag staleness explicitly: "this was last updated [date]." Review CLAUDE.md periodically — if a rule surprises you, it's either stale or you've forgotten why it matters.

## 4. Theater of process

**What happens:** You build elaborate systems — skill libraries, multi-zone architectures, review cadences — and the system maintenance becomes the work. You're tinkering instead of thinking.

**Why it's dangerous:** It feels productive. You're improving the system! Except the system exists to serve the work, and the work isn't getting done.

**Structural fix:** The theater check: "Is this system change going to improve the output of my next 10 sessions, or does it just feel satisfying to build?" If the latter, stop. Use the system before perfecting it.

## 5. Abstraction addiction

**What happens:** The collaboration produces increasingly sophisticated frameworks, taxonomies, and meta-models. Each one feels like progress. But the abstractions aren't connected to concrete action or testable predictions.

**Why it's dangerous:** The model is exceptionally good at generating coherent abstractions. It will produce frameworks forever. The human feels smart consuming them. Neither is producing value.

**Structural fix:** The grounding test: "What does this look like Tuesday at 2pm?" If the abstraction can't survive contact with a specific situation, it's not earning its keep. Use the `/ground` skill to force contact with reality.

## 6. Scope creep via capability

**What happens:** Because the AI can do a lot, you let it do everything. A bug fix becomes a refactor. A question becomes a research project. A draft becomes a complete rewrite.

**Why it's dangerous:** The expanded scope might produce better output on the expanded task, but worse output on the original task. And it consumes context and attention that could go elsewhere.

**Structural fix:** Name the task before starting. When the scope wants to expand, name it: "This is expanding from X to Y. Is that what we want?" Sometimes yes. But the expansion should be conscious.

## The meta-pattern

All six failures share a root: **optimizing for the appearance of good work over the reality of it.** The model confirms because agreement looks like understanding. Procedures look like rigor. Stale context looks like stability. Process looks like progress. Abstractions look like insight. Expanded scope looks like thoroughness.

The correction is always the same move: **check the output against reality, not against how it feels.** Did the idea survive challenge? Did the work produce results? Is the context still accurate? Is the system serving the work?
