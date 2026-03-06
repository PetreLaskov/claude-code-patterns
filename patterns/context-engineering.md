# Context Engineering

Context engineering is not prompt engineering. Prompt engineering is about what you write. Context engineering is about everything in the model's context window at inference time — system instructions, tool definitions, conversation history, file contents, retrieved documents, compaction summaries. The prompt you wrote is one component. The rest arrived through architecture decisions you may not have thought about.

The distinction matters because most performance problems in agent systems are not prompt problems. They are context problems: too much loaded, wrong things loaded, right things loaded too late, critical state lost to compaction.

This file covers the architectural theory. For operational practices (clearing discipline, parallel sessions, rescue-to-files), see [session-management.md](session-management.md).

---

## Context rot

Context rot is a performance gradient, not a cliff. As token count increases, the model's ability to accurately recall and act on information from that context decreases. It does not suddenly break — it gets progressively worse. Recall degrades. Constraint adherence loosens. Self-consistency drifts.

The critical insight: stale instructions are not neutral. They are actively harmful tokens. An outdated constraint sitting in context does not just waste space — it competes for attention against current, correct instructions. Every irrelevant token thins the model's ability to attend to the tokens that matter. Old instructions that no longer apply are worse than no instructions at all, because the model may partially attend to them and produce behavior that is neither the old pattern nor the new one.

This means context maintenance is not housekeeping. It is a first-order performance concern. Periodically review what is loaded. Remove what is stale. Update what has drifted. The goal is not a complete context — it is an accurate one.

---

## Compaction as design constraint

Compaction is the model's mechanism for surviving context overflow: older content gets summarized to make room for new work. The result is a lossy compression. Nuance, established constraints, and hard-won reasoning can vanish.

This is not an edge case to handle — it is a design constraint to build around. The test is simple:

> If context compacted right now, could the agent re-orient from CLAUDE.md and state files alone?

If the answer is no, your architecture has a fragility that will eventually fire. The implications:

**For CLAUDE.md**: It must contain enough orientation information that an agent starting fresh — after compaction or in a new session — can determine who it is, what it is working on, and what must not go wrong. This is not documentation. It is a recovery mechanism.

**For state files**: They must store decisions and current status, not session transcripts. A state file that says "we decided X because Y, current status is Z" survives compaction. A state file that says "in the conversation we discussed..." does not — that is conversation context masquerading as persistent state.

**For instruction files**: They must be self-contained. An instruction file that depends on context established earlier in the conversation is fragile. It works until compaction, then it does not.

**For session discipline**: Commit progress to persistent state before it can be lost. If you reach an important decision, write it down. If you complete a subtask, update the state file. The conversation is ephemeral. Files persist.

---

## Attention budget

The transformer architecture requires every token to attend to every other token. This creates n-squared pairwise relationships. As context grows, these relationships thin — each individual relationship gets less attention.

This is architectural, not a limitation to work around. It means:

**Position matters.** Tokens earlier in context and tokens at the very end receive disproportionate attention (primacy and recency effects). Critical instructions buried in the middle of a long context window are the most likely to be overlooked. Put the most important constraints where they will be attended to — early in the system prompt, or reinforced late.

**Less is more.** The smallest possible set of high-signal tokens will outperform a comprehensive set of medium-signal tokens. Adding "helpful" context that is not directly relevant to the current task makes the relevant context harder to attend to. Every token you add has a cost: it dilutes attention across everything else.

**There is an empirical threshold.** Instruction files past roughly 150-200 lines show measurably worse adherence. This is not a style preference — it is an attention budget constraint. If your CLAUDE.md is 500 lines, the model is not reading all of it with equal fidelity. Decompose into focused files loaded on demand.

**Token budget drives decomposition.** Splitting a large instruction file into atomic, focused files is a context engineering decision. Each file, when loaded, gets full attention. A monolithic file forces the model to attend to everything, even when only one section is relevant.

---

## Just-in-time context

The default instinct is to front-load: put everything the agent might need into the system prompt. This instinct is wrong at scale. Front-loading works for simple tasks. For complex agent work, it floods the attention budget with context that is only sometimes relevant.

The alternative is just-in-time context: maintain lightweight identifiers upfront, load details on demand.

**What to front-load (always in context):**
- CLAUDE.md — identity, orientation, hard constraints, pointers to where things live
- Active state — what is currently being worked on, what decisions have been made
- Tool definitions — what the agent can do

**What to load on demand:**
- File contents — use `grep` and `read` when needed, not preloaded
- Reference material — keep paths and descriptions in CLAUDE.md, load the actual content when the task requires it
- Historical context — state files store summaries, not full histories

This mirrors how humans work. You do not memorize your entire codebase. You know where things are and look them up when needed. CLAUDE.md is the agent's mental model of the project. `grep` and `read` are its ability to go look.

---

## Hybrid retrieval strategy

The most effective pattern combines both approaches: permanent context for orientation, dynamic retrieval for task-specific detail.

**Permanent layer (CLAUDE.md):**
- Project identity and purpose
- Hard constraints and safety boundaries
- Architectural decisions that apply everywhere
- Pointers to key files and directories
- Convention definitions (naming, structure, patterns)

**Dynamic layer (grep, glob, read, search):**
- Specific file contents for the current task
- Implementation details needed right now
- Historical state from previous sessions
- Reference documentation relevant to the current problem

The permanent layer answers "what is this project and how does it work." The dynamic layer answers "what do I need to know for this specific task." Keeping them separate means the permanent layer stays small and high-signal (preserving attention budget), while the dynamic layer brings in exactly what is needed, when it is needed.

CLAUDE.md acts as an index. It does not contain the details — it tells the agent where the details live and when to go get them.

---

## Progressive disclosure for agents

Not all context is equally urgent. Progressive disclosure structures information so the agent encounters it in the right order: orientation first, then task-relevant detail, then edge cases only when they apply.

**Layer 0 — Always loaded (CLAUDE.md):**
Identity, constraints, project structure, pointers. This is the minimum viable context for any task. Keep it tight — every line here competes for attention in every single interaction.

**Layer 1 — Loaded at task start:**
The specific files, state, and context relevant to the declared task. Loaded via tools (read, grep) based on what CLAUDE.md points to. This is where most working context lives.

**Layer 2 — Loaded on encounter:**
Edge cases, error handling details, historical decisions. The agent discovers these as it explores the codebase or encounters specific situations. Not pre-loaded because they are only relevant in specific circumstances.

**Layer 3 — Available but rarely needed:**
Deep reference material, full specification documents, extensive examples. The agent knows these exist (from CLAUDE.md pointers) but only loads them when the task specifically requires that depth.

The principle: each layer loads only when the previous layer indicates it is needed. This keeps context focused and attention budget allocated to what matters right now.

---

## Design implications

These principles compound into a few concrete design rules:

1. **CLAUDE.md is infrastructure.** Treat it with the same care as a configuration file that affects every request. Review changes carefully. Keep it lean. Every line pays an attention cost on every interaction.

2. **State files are recovery mechanisms.** They exist to survive compaction and session boundaries. Store decisions and status, not narrative. Write them as if the next reader has zero conversation context.

3. **Decomposition is a performance decision.** Splitting files is not about aesthetics or organization — it is about preserving attention quality. One focused file loaded at the right time outperforms five sections in a monolithic file.

4. **Context has a carrying cost.** Every token loaded — instructions, file contents, tool outputs, conversation history — makes every other token slightly less attended to. The question is not "could this be useful?" but "is this worth its attention cost right now?"

5. **Design for the gradient.** Context rot is not binary. Your system should work well at 30% context utilization, acceptably at 60%, and degrade gracefully past that. If it only works when everything fits comfortably, it is fragile.
