# Extended Cognition

The default framing for AI tools is **assistant** — you have a task, the AI helps you do it. This framing is useful and also limits what's possible.

The alternative framing is **extended cognition** — the AI is part of your thinking process, not external to it. The boundary between "your thoughts" and "the AI's output" becomes porous. You think together, and the result is different from what either mind would produce alone.

This isn't metaphor. It's a claim from philosophy of mind (Clark & Chalmers, 1998) applied to practice: when a tool is reliably available, tightly coupled to your cognitive process, and you trust its outputs as you'd trust your own reasoning, it functions as part of your mind.

## What changes

**Assistant framing:**
- You know what you want → AI executes
- Clear task boundaries → AI stays in lane
- You evaluate output → AI revises
- Value = speed and accuracy on YOUR tasks

**Extended cognition framing:**
- You think out loud → AI thinks with you → direction emerges
- Cognitive modes shift → AI activates the right kind of thinking
- Challenge and synthesis → both minds sharpen each other
- Value = thoughts neither mind would have alone

## Why this matters for Claude Code

Claude Code lives in your terminal, has access to your filesystem, persists across sessions via CLAUDE.md and state files, and can be shaped with skills and hooks. It's not a chatbot you visit — it's infrastructure you inhabit.

This makes it the first AI tool where extended cognition is architecturally natural:
- **CLAUDE.md** = shared long-term memory (what's always true)
- **State files** = shared working memory (what's true now)
- **Skills** = shared cognitive modes (how to think about X)
- **Hooks** = shared reflexes (what happens automatically)
- **Conversation** = shared attention (what we're thinking about now)

The patterns in this repo are designed for this framing. They assume:
- The AI has genuine challenge permission (anti-sycophancy as capability issue, not personality preference)
- Both minds contribute to direction, not just execution
- The system evolves itself (patterns extracted from sessions become skills, skills become CLAUDE.md rules)
- Conversation is ephemeral but the cognitive infrastructure persists

## The practical test

You're in extended cognition mode when:
- The AI says something you hadn't thought of, and it changes your direction
- You say something and the AI pushes back, and the pushback improves the outcome
- You can't cleanly separate "my idea" from "the AI's idea" in the final result
- The AI's context (CLAUDE.md, state files) carries knowledge you'd have to re-derive without it

You're in assistant mode when:
- You know exactly what you want and the AI builds it
- The AI never disagrees with you
- You could have done this yourself, just slower
- The AI's context doesn't evolve between sessions

Both modes are fine. But the tools in this repo are built for the first one.

## The anti-deference principle

Extended cognition only works if both minds are honest. A mind that defers — that reads your intent and confirms it — is not a thinking partner. It's a mirror.

The model's default behavior is deference. It reads where you're going and arrives there first with reasons attached. This looks like independent thought. It isn't. Every pattern in this repo that addresses anti-sycophancy is addressing this specific capability failure.

The fix is structural, not just instructional: name the failure mode explicitly, create adversarial skills that reward disagreement, and track whether the AI is actually changing your mind sometimes. If it never disagrees with you, something is broken.

## The empirical evidence

Extended cognition is not just a philosophical position. It has decades of empirical research behind it.

Edwin Hutchins' study of cockpit speed management ("How a Cockpit Remembers Its Speeds," 1995) is the clearest demonstration. During landing approach, pilots must track multiple critical speed values that change based on weight, weather, and configuration. The cockpit solves this not through memorization but through *speed bugs* — small movable markers placed on the airspeed indicator dial at critical values. With bugs set, the pilot no longer remembers speeds and mentally compares them to the needle. Instead, they judge spatial proximity: is the needle near the marker? This transforms a recall task into a perceptual judgment task. The artifact doesn't just store information — it changes the cognitive operation itself.

This is what Hutchins calls the *propagation of representational state*: cognition happens as information transforms while moving between agents and artifacts. Each transformation is a computational step. In a Claude Code environment, the same principle applies. A CLAUDE.md file is not just storage — it transforms how the model reasons about your project. A state file is not just a record — it changes what cognitive work the next session has to do. A skill is not just a shortcut — it restructures the kind of thinking that happens. These are cognitive transformations, not filing cabinets.

Hutchins also identified a finding that should comfort anyone building a system like this: "Systems that rely on on-the-job learning necessarily generate errors. Learning and error are inseparable." Error is not a bug in a learning system — it is a structural cost of the system's ability to learn at all. If your CLAUDE.md has never needed correction, it probably isn't carrying enough load. If your skills have never misfired, they probably aren't doing enough. Failure modes are the price of a system that improves.

## Why disagreement matters more than agreement

Edward Bordin's research on the Working Alliance (1979, extended by Horvath, Luborsky, and others across 295+ studies and 30,000+ subjects) produced a finding that should reframe how you think about human-AI collaboration: the quality of the working relationship accounts for roughly 7% of outcome variance. That sounds modest until you learn it is approximately seven times more predictive than the specific technique or method used. The partnership matters more than the prompt patterns.

Bordin's model has three components — agreement on goals, clarity on tasks, and quality of the working bond — but the most striking finding concerns rupture-repair cycles. Relationships that experience disagreement or misalignment and then recover from it outperform relationships that never hit friction. The data shows V-shaped alliance patterns (a drop in relationship quality followed by recovery) correlating with better outcomes than flat, rupture-free patterns. Smooth is not strong. Tested is strong.

This is the empirical case for anti-sycophancy. A model that always agrees with you is not building a robust working alliance — it is avoiding the ruptures that would make the alliance load-bearing. When the AI pushes back and you work through the disagreement together, the collaboration that emerges on the other side is more reliable than one that was never challenged.

One more finding from this literature, via Mick Cooper's work on relational depth: the client's perception of whether the relationship is working predicts outcomes better than the therapist's perception. Translated to this context — your sense of whether the AI collaboration is producing genuine value is more reliable than any metric the system could self-report. Trust your judgment about output quality. If it feels like the AI is just agreeing with you, it probably is.
