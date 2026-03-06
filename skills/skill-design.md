# Designing Skills

How to create Claude Code skills that consistently produce high-quality output.

## The mechanism

A skill file at `~/.claude/commands/my-skill.md` becomes `/my-skill` in Claude Code. When invoked, the file content replaces the system context for that response. `$ARGUMENTS` gets replaced with whatever the user types after the command.

This means: your skill is a system prompt. Everything you know about good prompting applies.

## The anti-scaffolding principle

The most common mistake is writing procedural skills — step-by-step instructions that tell the model what to do. This caps the model at your ability to anticipate the situation.

Instead, write **dispositional** skills — describe the cognitive mode, the quality floor, and the failure mode. Let the model decide how to get there.

```markdown
# Bad: procedural
1. Read the user's input
2. Identify the main claim
3. List 3 counterarguments
4. Evaluate each counterargument
5. Synthesize a conclusion

# Good: dispositional
$ARGUMENTS

Adversarial collaboration, not consultation. Orthogonal hypotheses,
not variants. Everything falsifiable. Steelman the strongest counter;
the output must contain a position strong enough that someone could
hold it.
```

The procedural version produces uniform, predictable output. The dispositional version produces thinking that adapts to the actual content.

## Anatomy of a good skill

**Line 1-2:** The cognitive mode. What mental posture to adopt.
"Adversarial collaboration, not consultation."

**Core:** The quality standards. What the output must contain.
"The output must contain a position strong enough that someone could hold it."

**Failure mode:** What to avoid — named specifically.
"Follow anomalies over confirmations." (Implicitly: don't do confirmation bias.)

**Output shape (optional):** Loose guidance on form.
"Output: the map, then the single highest-leverage move."

## Length

5-15 lines is the sweet spot. Under 5, you're probably not targeting precisely enough. Over 15, you're probably procedural. Over 30, you're definitely procedural.

Exception: skills that need reference material (like a cheatsheet skill) can be longer, but the instructional core should still be short.

## Distributional targeting

Every word in a skill routes the model. Use this intentionally:

- **Named traditions** target expertise: "differential diagnosis" activates medical reasoning patterns. "Pre-mortem (Klein)" activates prospective hindsight.
- **Contrastive framing** excludes failure: "Lossless compression, not summarization" blocks the default summary mode.
- **Sensory language** targets concrete thinking: "What does it look like Tuesday at 2pm?" prevents abstract hand-waving.
- **Quality markers** set the floor: "A reader who sees only the compressed version loses nothing they'd act on."

## Testing

A skill works if:
1. Different inputs produce genuinely different outputs (not template-fill)
2. The output quality consistently beats what you'd get without the skill
3. The failure mode named in the skill is actually avoided
4. The skill is short enough to remember what it does from the name alone

## Naming

- Verb-first: `think-hard`, `decide`, `compress`, `diagnose`
- The name should predict the cognitive mode
- If you can't name it in 2-3 words, the skill might be doing too many things
