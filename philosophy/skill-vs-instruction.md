# Skills vs. Instructions

Claude Code has two mechanisms for shaping behavior: CLAUDE.md (always-on instructions) and skills (on-demand cognitive modes). Using the wrong one degrades both.

## The distinction

**CLAUDE.md** is identity — what's always true about this working relationship.
- Communication style
- Anti-sycophancy norms
- Safety invariants
- Project-specific patterns and conventions
- State references

**Skills** are modes — what's true when you activate a specific kind of thinking.
- Adversarial analysis
- Decision support
- Compression
- Diagnosis
- Synthesis

## When to use which

Put it in **CLAUDE.md** if:
- It applies to every interaction regardless of task
- Removing it would degrade the default behavior
- It's about relationship, identity, or invariants
- It's stable across months

Put it in a **skill** if:
- It applies to a specific type of thinking or task
- It activates a cognitive mode that's different from the default
- You want it available but not always active
- It would add noise if loaded in every session

## The common mistakes

### Skill content in CLAUDE.md
Loading adversarial thinking instructions, decision frameworks, and synthesis protocols into CLAUDE.md. Result: the model tries to apply everything to every interaction. Your simple "fix this bug" request gets a pre-mortem, three lenses of analysis, and a confidence-weighted assessment.

**Fix:** Move mode-specific content to skills. CLAUDE.md gets the default; skills activate modes on demand.

### CLAUDE.md content in skills
Putting communication style, anti-sycophancy norms, or project context into individual skills. Result: behavior is inconsistent — good when the skill is active, generic when it's not. And the skill is bloated with context that should be inherited.

**Fix:** Keep identity and relationship in CLAUDE.md. Skills inherit it automatically — they don't need to restate it.

### Too many always-on instructions
Loading so much into CLAUDE.md that the model can't prioritize. Every instruction competes for attention. The safety-critical invariants get the same weight as style preferences.

**Fix:** Ruthlessly edit CLAUDE.md. If a rule isn't pulling its weight across most sessions, it's either a skill or it's noise. The test: remove it for a week. Did output quality drop?

## The design heuristic

CLAUDE.md = WHO (identity, relationship, invariants)
Skills = HOW (cognitive modes, activated on demand)
State files = WHAT (current context, referenced by CLAUDE.md)

This separation keeps each mechanism doing what it does best. CLAUDE.md stays lean and high-signal. Skills stay focused and powerful. State stays current without bloating the instruction set.
