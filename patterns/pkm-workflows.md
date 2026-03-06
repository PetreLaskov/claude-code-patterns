# PKM Collaboration Patterns

Workflow patterns for using Claude Code as a thinking partner inside a knowledge vault. These assume the CLAUDE.md setup from [pkm-vault.md](../claude-md/pkm-vault.md).

## The Three Core Loops

### Loop 1: Capture → Process → Connect

```
1. CAPTURE (fleeting)
   Raw dump into inbox. No polish, just get it down.

2. PROCESS (literature or evergreen)
   Extract 1-3 genuine insights.
   Rewrite in your own words.
   Add counter-examples.

3. CONNECT (linking)
   Find 3+ related notes.
   At least one surprising/weak tie.
   Update source with backlinks.
```

**When to use:** After you have a rich inbox note — AI dump, long conversation, book notes.

**What Claude does:**
1. Reads source
2. Asks: "What's the core insight here, in your words?"
3. You provide the bone; Claude proposes the meat
4. Shows minimal diff; you approve or iterate

**The goal is additive enrichment.** You remain the author. Claude assists by expanding, contextualizing, and connecting.

### Loop 2: Think-With-Me (Exploration)

```
1. YOU state a problem/question
2. CLAUDE asks 3-5 probing questions to surface assumptions
3. TOGETHER map options, tradeoffs, unknowns
4. PROPOSE one small experiment to test
5. LOG session for future reference
```

**When to use:** Stuck on a decision. Want to explore a topic. Need alternative framings.

**This is Socratic** — not to show you're wrong, but to reveal what's unexamined. The questions matter more than the answers.

### Loop 3: Quick-Link (Strengthen the Graph)

```
1. Claude reads target note
2. Searches vault for surprising relations and bridge notes
3. Proposes ~5 bidirectional links with one-line rationale each
4. You review and approve
```

**When to use:** Note feels isolated. Want to discover connections. Building out a cluster.

**Favor weak ties** — surprising connections and bridge notes over obvious keyword matches. Weak ties are where novel insights emerge.

---

## Advanced Patterns

### The Extraction Pipeline

**Goal:** Turn a 2,000-line AI dump into a knowledge graph.

```
1. Extract atoms → get first 3-5 evergreen notes
2. For each new note → quick-link to find bridges
3. When 5-8 notes cluster → create a map of content
4. Repeat on different sections of the source
```

The pipeline turns raw material into connected knowledge in predictable steps. Each step is independently valuable — you can stop at any point.

### The Dialectic Loop

**Goal:** Refine an idea through challenge.

```
1. Draft a claim (or have Claude extract one)
2. "Devil's advocate: what's wrong with this?"
3. Revise claim to handle counterargument
4. "What evidence in my vault supports this?"
5. Add evidence links
6. "What scope does this NOT cover?" → define boundaries
```

This produces notes that have survived challenge. They're stronger than first-draft notes because the counterarguments are baked in.

### The Cluster Bloom

**Goal:** Rapidly build out a topic cluster.

```
1. Start with 1-2 seed notes on a topic
2. Quick-link each seed → discover 3-5 connections
3. Extract atoms from any linked sources
4. Quick-link the new notes
5. When 5-8 notes exist → create map of content
6. Continue until diminishing returns on new links
```

This exploits the network effect: each new note makes existing notes more findable and more connected.

### The Assumption Audit

**Goal:** Surface and test hidden assumptions.

```
1. Think-with-me on a topic or decision
2. Claude asks 3-5 probing questions
3. You answer; Claude maps assumptions
4. "What's the weakest assumption here?"
5. "Propose a tiny test for that assumption"
6. Log the session
```

This is prospective hindsight applied to your own thinking. The weakest assumption is usually the one you haven't questioned because it feels obvious.

---

## Six Thinking Prompts

Use these to evaluate notes — yours or Claude's:

1. **Understanding test:** "Rephrase the core idea without the author's terms."
2. **Argument test:** "Does this claim stand alone? What's a plausible counterargument?"
3. **Connection test:** "Why link A to B? What's the relationship?"
4. **Devil's advocate test:** "What would make this wrong or misleading?"
5. **Evidence check:** "What note in my vault actually supports this?"
6. **Scope guard:** "What belongs outside this note to keep it atomic?"

---

## Troubleshooting

### Extractions feel shallow
Claude is optimizing for volume over depth. Fix: add constraints ("Extract 1-2 atoms, not 5; go deep"), provide a taste example ("I want notes like [example] — concise but with counterexamples"), use the thinking prompts to evaluate.

### Links feel forced
Optimizing for link count over link quality. Fix: review the one-line context ("Does this explain WHY the link matters?"), ask "What's the weakest link here? Replace it with a surprising bridge."

### Notes are too long
Violating atomicity. Fix: use the Scope Guard test ("What belongs OUTSIDE this note?"), ask Claude to split, provide an example of the atomicity level you want.

### Claude is too passive
You're treating it as a command-line tool, not a thinking partner. Fix: ask open questions instead of narrow commands. "What surprising connections could this note have?" beats "Add 3 links to this note."

### Claude is making changes you didn't ask for
Broad permission or misread intent. Fix: check proposed changes BEFORE approving. Ask "Why did you change X?" Remind of consent gates for risky operations.

---

## The Implicit Contract

1. **Claude optimizes for YOUR future self**, not for Claude's aesthetics or "best practices" in abstract.
2. **You are the arbiter of "genuine insight."** If Claude extracts something you find obvious, say so. Claude recalibrates.
3. **The vault is YOUR cognitive space.** Claude proposes; you decide. Pushback is expected and welcomed.
4. **Process-in-place is sacred.** If Claude reorganizes without asking, that's a bug.
5. **The system evolves with you.** As your vault grows, patterns emerge. Claude should notice clusters and suggest maps. If it doesn't, you can trigger it.
