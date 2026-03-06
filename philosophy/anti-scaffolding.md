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

## Why this works: the research

Three independent research traditions converge on the same conclusion.

**Expertise reversal effect (Sweller).** Cognitive load theory established a counterintuitive finding: instructional procedures that benefit novices produce *negative* consequences for expert learners. Detailed scaffolding, worked examples, and step-by-step guidance help when the learner lacks domain schemas — but once those schemas exist, the same guidance becomes extraneous load that competes with the learner's own superior processing. Claude is an expert-level model. Procedures designed for weaker models — exhaustive checklists, mandatory reasoning scaffolds, chain-of-thought templates — actively degrade its performance. This is not a preference or a style choice. It is a measured effect with decades of replication behind it.

**Fading principle (Wood, Bruner, and Ross, building on Vygotsky).** The researchers who formalized the scaffolding concept built removal into the definition. Scaffolding is temporary support that enables work beyond current capability — and the entire point is that it comes down. Support that never fades creates dependency. If a skill cannot eventually become unnecessary — if the model cannot internalize the pattern and perform without the instruction — then the skill is a crutch, not a tool. The test for any instruction: is this something the model should need forever, or something it should absorb and outgrow? If the latter, design for its own disappearance.

**Economy of mechanism (OWASP, safety engineering).** The security principle is blunt: choose the simplest, most understandable implementation. Complexity breeds vulnerabilities. Simple systems are easier to verify and harder to subvert. Applied to instruction design: every additional line is not just a token cost — it is a potential point of failure, a place where ambiguity can enter, where contradictions can hide, where the model's attention gets split between following your procedure and doing its actual work. Fewer instructions means fewer failure modes. Simplicity is not laziness; it is a safety property.

The convergence is hard to ignore. Cognitive science says over-instruction hurts experts. Developmental psychology says scaffolding must fade. Security engineering says complexity is a vulnerability. They all point the same direction: write less, trust more, correct only what breaks.

## The paradox

Anti-scaffolding is itself a kind of instruction. The resolution: these patterns are calibrations that point the model toward its strongest capabilities, not constraints that limit it. The goal is to get out of the model's way while shaping the direction. A compass, not a cage.
