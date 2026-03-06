# Anti-Scaffolding

The instinct when building AI systems is to add structure: more rules, more procedures, more guardrails, more templates. This instinct is wrong more often than it's right.

## The problem with scaffolding

Scaffolding — step-by-step procedures, elaborate checklists, mandatory workflows — works by constraining the model's behavior to a narrow corridor. This helps when:
- The task is routine and well-understood
- The cost of deviation is high
- The model's judgment in this domain is unreliable

It hurts when:
- The task requires adaptation to novel situations
- The quality of output depends on judgment, not compliance
- The model's training already covers the domain well

Most Claude Code usage falls into the second category. The model is already a skilled programmer, writer, and reasoner. Procedures that tell it HOW to think cap it at the procedure-writer's ability to anticipate.

## What works instead

**Dispositional instructions** over procedural ones. Instead of "1. Read file, 2. Find bugs, 3. Propose fixes," write "Review for correctness and security. Flag assumptions, not style."

**Failure modes** over success procedures. Instead of telling the model what to do, tell it what NOT to do. "Don't anchor on the first plausible explanation" is more valuable than "Consider at least 3 alternatives" — because the failure mode targets the actual cognitive error.

**Quality floors** over quality ceilings. "The output must contain a position strong enough that someone could hold it" sets a floor. "Provide exactly 3 counterarguments" sets a ceiling. Floors allow excellence; ceilings prevent it.

**Trust and verify** over prevent and control. Let the model work, then check the output. If it consistently fails in a specific way, add a targeted correction for that failure. Don't pre-build corrections for hypothetical failures.

## The evidence

In practice, across hundreds of sessions:

- 10-line dispositional skills consistently outperform 50-line procedural ones
- CLAUDE.md files under 100 lines produce better behavior than those over 200
- Skills that name failure modes work better than skills that list steps
- Removing instructions often improves output (less noise, more signal)

The pattern: **the model's training is the primary resource. Instructions are calibration, not replacement.**

## When scaffolding IS right

- **Safety-critical operations**: destructive git commands, production deployments, data deletion. Here, a checklist prevents catastrophe.
- **Novel domains where the model hallucinates**: if the model consistently gets something wrong, a specific correction is warranted.
- **Coordination**: when multiple agents or sessions need to share state, explicit protocols prevent drift.

The test: would removing this instruction make the output worse *in practice*, or does it just make you feel more in control? If the latter, remove it. Control theater is a cost, not a benefit.

## The paradox

Anti-scaffolding is itself a kind of instruction. The resolution: these patterns are calibrations that point the model toward its strongest capabilities, not constraints that limit it. The goal is to get out of the model's way while shaping the direction. A compass, not a cage.
