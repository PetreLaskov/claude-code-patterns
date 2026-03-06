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
