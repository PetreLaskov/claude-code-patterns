# Safety Architecture

Autonomous agents operating on your files need graduated controls. An agent with write access to instruction files, persistent state, and your working documents is powerful — and power without proportional safeguards produces predictable disasters. This pattern establishes the safety layers that make sustained agent collaboration viable.

---

## Blast-Radius Proportionality

Not all operations carry the same risk. The review rigor an operation receives should be proportional to the scope of its potential impact.

| Blast radius | Examples | Control rigor |
|---|---|---|
| **Unbounded propagation** | Instruction file changes (CLAUDE.md), naming conventions, structural reorganization | Permanent diff-first review. Never relaxes, regardless of user expertise. |
| **Bounded, high impact** | New module creation, file placement into established structures, configuration deployment | Explicit confirmation before execution. |
| **Bounded, low impact** | State file updates, session notes, conversational corrections | Graduated autonomy. Lightweight consent sufficient. |

The critical insight: **instruction file changes never get auto-approved.** A change to a CLAUDE.md or any file loaded at session start propagates through every subsequent agent response in every future session. That makes it infrastructure, not content — and infrastructure review is permanent regardless of how experienced the operator is. This is structural prudence, not paternalism.

The relationship is strictly proportional: the larger the potential blast radius, the more defensive layers required before execution.

---

## Memory Poisoning

Any file that persists across sessions and gets loaded into context is an injection surface. This includes CLAUDE.md files, state files, auto-memory, build journals, and session logs.

**Why this matters:** Content loaded at session start shapes every response the agent produces. A corrupted or misleading persistent file does not just degrade one answer — it biases the entire session.

**Attack vectors and mitigations:**

- **Stale data as poison.** Outdated persistent files are not merely low-signal — they are actively misleading, causing the agent to act on assumptions that no longer hold. Staleness checks at session start are a safety function, not a hygiene function.
- **Instruction/data boundary violations.** Persistent files should maintain a clean separation between instruction fields and data fields. Data fields store observations; instruction fields store directives. When data fields contain instruction-like patterns (imperative commands, role assignments, system prompt fragments), they become injection surfaces. Validate at write time.
- **Cross-project contamination.** State from one project should never leak into another project's context. Isolate persistent state per project. Cross-contamination is a safety failure, not an efficiency opportunity.
- **Sanitization discipline.** Store semantic patterns and structured observations in state files, not raw conversation transcripts. Raw history carries noise and potential injection content.

---

## Anti-Gate-Inflation

Safety gates work only if people actually read them. The number of confirmation gates should be minimized so that each gate feels significant when encountered.

Over-gating trains reflexive approval — the user learns to click "yes" without reading, which is itself a safety failure. This is the "click OK without reading" problem, and it is worse than having fewer gates, because it creates the illusion of oversight where none exists.

**Practical rule:** If you find yourself adding a new confirmation step, ask whether an existing gate already covers the risk. Prefer fewer, meaningful gates over many trivial ones. Every gate should make the operator pause and think. If it does not, it is not protecting anything.

---

## Graduated Consent Model

Operations fall into three tiers based on their risk profile:

### NEVER (without explicit consent)

| Action | Why |
|--------|-----|
| Delete files without backup | Permanent data loss; deleted content may have future value |
| Modify outside declared scope | Unpredictable side effects in areas the agent does not understand |
| Bulk operations across many files | Cascade damage; review each change individually |
| Silent file operations | Every create, modify, or move must be announced before execution |

### ASK FIRST

| Action | Protocol |
|--------|----------|
| Structural changes (new directories, reorganization) | Propose plan, await confirmation |
| Rename or move files | Show the rename/move plan with impact on linked files |
| Edit highly-connected files | The more things reference a file, the more caution required |
| Modify metadata or configuration fields | Explain downstream impact before changing |

**Risk scales with interconnectedness.** A file referenced by many other files is structurally load-bearing. The more connections, the higher the required consent threshold:

| Connections | Risk | Protocol |
|-------------|------|----------|
| 0-2 | Low | Proceed with diff shown first |
| 3-5 | Medium | Ask first, show full plan |
| 6+ | High | Full explicit consent required |

### ALWAYS SAFE

| Action | Notes |
|--------|-------|
| Read any file | Full access, no restrictions |
| Search the codebase | Glob, grep, any read-only exploration |
| Create new files | In appropriate locations, announced |
| Propose edits as diffs | Show the diff; never apply without review |
| Add content to existing files | Additive changes with diff shown |

---

## Recovery Principles

When something goes wrong, the response is always **diagnostic before corrective.** Identify what failed and why before attempting a fix. Rushing to repair without diagnosis risks compounding the original failure.

**Diff-first review.** Every edit follows a strict loop:

```
1. Plan   — State what you intend to change and why
2. Patch  — Show the unified diff with context
3. Review — User approves or requests changes
4. Apply  — Only after explicit approval
```

**Backups before destructive operations.** No destructive operation executes without a verified backup. Copy-in, not move-in. Rollback means removing copies, never losing originals.

**Staged changes.** For risky operations, proceed one file at a time. Batch operations multiply risk — a bug in your approach damages one file, not twenty.

**Additive-first recovery.** When repairing damage, prefer adding content over removing it. Comment out rather than delete. Preserve the evidence of what went wrong — it informs the fix.

**No silent corrections.** If you discover you made an error, announce it. State what happened, what the impact is, and what you propose to do about it. Transparency during failure is more important than transparency during success.

---

## Beyond Prevention: Adaptive Capacity

Everything above is prevention-oriented — gates, consent tiers, blast-radius controls. That is necessary but incomplete. Safety engineering distinguishes two deeper concerns that most agent safety architectures ignore.

**Active vs latent failures.** James Reason's Swiss Cheese Model separates two failure modes. Active failures are visible mistakes — the wrong file deleted, the bad edit applied. Latent conditions are systemic weaknesses that sit dormant until an active failure finds them: stale instruction files loaded at boot, missing safety rules in a CLAUDE.md, unclear scope boundaries that let an agent wander. You cannot eliminate human error; it is irreducible. So defenses must compensate for foreseeable mistakes rather than assume perfection. The gates in this pattern should target latent conditions — not just catch the active error after it happens, but remove the systemic conditions that let it succeed.

**Safety-I vs Safety-II.** Erik Hollnagel distinguishes two safety paradigms. Safety-I defines safety as the absence of accidents: prevent bad things, investigate failures, build barriers. Safety-II defines safety as the presence of adaptive capacity: understand why things usually succeed, build the ability to handle the unexpected. Most agent safety is pure Safety-I — gates, reviews, consent tiers, rollback procedures. Safety-II asks a different question: can the system adapt when something genuinely novel happens? Hollnagel's key insight is that things go wrong and things go right for the same basic reasons. The variability that produces errors also produces successful adaptation.

**Four resilience abilities.** Hollnagel's Resilience Assessment Grid identifies the capacities a robust system needs:

1. **Responding** — Reacting appropriately when situations demand intervention. Knowing what to do now.
2. **Monitoring** — Detecting that conditions require action before they become critical. Noticing what is changing.
3. **Learning** — Modifying behavior based on experience. Incorporating what has happened.
4. **Anticipating** — Preparing for developments before they materialize. Considering what might happen.

A well-designed agent environment should support all four. Most support only the first two (responding through gates, monitoring through staleness checks). Learning and anticipating — updating safety rules from observed near-misses, preparing for failure modes you have not yet encountered — are where genuine resilience lives.
