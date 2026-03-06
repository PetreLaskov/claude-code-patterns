# Human Practice

The patterns in this repo are mostly AI-facing — how to configure the model, what instructions to give it, what skills to activate. This file covers the other side: how the human should work, experiment, and develop skill.

## Cognition is free. Attention is not.

The marginal cost of an LLM query is near zero. This should liberate experimentation — run more experiments than feels reasonable. Try three phrasings. Ask all available models. Test the weird approach alongside the sensible one.

But: a 40-page deep research report can be net-negative if it consumes more attention to process than the insight is worth. Generation is cheap. Your processing bandwidth is the bottleneck.

The practical implication: generate liberally, filter ruthlessly. Don't read everything the model produces — scan for signal, dig into what matters, discard the rest.

## The prompt-improvement habit loop

Every time the model does something you wouldn't have wanted it to, ask: **Is this a prompt problem?** Could a tweak to my system prompt, my phrasing, or my skill prevent this class of error permanently?

This is the core feedback mechanism. Most users fix individual outputs. Skilled users fix the system that produces outputs. The difference compounds: fixing one output saves minutes, fixing the prompt saves hours across future sessions.

The loop:
1. Model produces unwanted output
2. Ask: is this a prompt problem or a capability problem?
3. If prompt: what instruction, skill, or CLAUDE.md change would prevent it?
4. Implement the change
5. The error class is eliminated permanently

## The competent stranger test

When writing prompts or CLAUDE.md instructions, use this diagnostic from Amanda Askell (Anthropic):

> Imagine you've hired a temp agency to send someone to do a task. This person arrives, and you know they're pretty competent. They know a lot about your industry, but they don't know the name of your company. They show up and say, "Hey, I was told you had a job for me. Tell me about it." What would you say to that person?

Whatever you'd tell the competent stranger — that's what belongs in your prompt. What you'd assume they already know — leave it out. What you'd show them before they start — that's your reference material.

## Register is bidirectional

How you write to the model shapes how the model writes back. Erudite, precise language gets precise, substantive responses. Casual shorthand gets casual output. This isn't just about output styling — it's a capability routing mechanism. Your linguistic register implicitly prompts the level of the entire interaction.

If you want graduate-level analysis, write at a graduate level. If you want practitioner-grade output, write like a practitioner. The model matches the register it receives.

## Have the model interview you

The hardest part of any complex task is pulling the right information out of your own head. You forget constraints, skip assumptions, omit context that's obvious to you but invisible to the model.

The fix: instead of writing a complete prompt, tell the model to interview you first. "Interview me about what I want before building anything. Ask probing questions about requirements, constraints, edge cases, and things I might be forgetting."

This inverts the prompting relationship. Instead of you extracting what the model needs to know, the model extracts what it needs from you. It's better at asking systematic questions than you are at anticipating what it needs.

## Don't identify your work when requesting critique

When you ask the model to critique something you wrote, don't tell it you wrote it. "Critique my essay" activates the sycophantic circuit — the model knows criticism will be received personally. "Critique this piece of writing" doesn't carry that signal.

Similarly, avoid leading questions that telegraph the answer you want. "Don't you think this approach is better?" will get agreement. "Compare these two approaches" won't.

## Anonymize for honest baselines

When you need an unbiased read — on your writing, your code, your strategy — use a fresh session with no personal context. No CLAUDE.md, no conversation history. Just the artifact and the question. The output tells you what the model actually thinks without the accumulated context shaping it toward your preferences.

## Know when to stop grinding

If you're iterating on a prompt and not getting closer to what you want, the problem may not be your prompt — it may be the model's current capability boundary. The diagnostic: does the model "kind of get it"? Is it in the right zip code? If yes, keep refining. If no, you might be waiting for the next model generation rather than grinding on this one.

This is anti-scaffolding applied to your own iteration process. Sometimes the highest-leverage move is to stop and wait, not to try harder.

## Prompting as externalization

The deepest frame on what prompting actually is, from Amanda Askell:

> The skill is taking things that are in your brain, analyzing them enough to feel like you fully understand them, and then externalizing them for a reasonable person off the street.

This is why prompting improves your own thinking: the act of making your intent explicit enough for a capable stranger forces you to understand it yourself. The prompt is a byproduct of clarity, not a substitute for it.

## Reciprocity of informativeness

Every time you ask the model for something — an analysis, a review, a decision — pair it with something concrete from you. A file to look at. A constraint. A specific example. The model's output quality degrades when it's answering abstract questions in a vacuum and improves dramatically when it has specific artifacts to work with.

The ratio matters: never extract three times without delivering once. If you ask three questions in a row without giving the model new material to ground on, the answers get thinner, more generic, more likely to drift. Feed the conversation. The model's best outputs come from reacting to specific material, not generating from general knowledge.

## Artifact-grounded conversation

"Walk me through this file" produces richer, more accurate output than "Tell me about your architecture." Abstract questions produce abstract answers. Pointing the model at a specific file, function, or document forces specificity that abstract prompting cannot.

This applies especially when you need to surface tacit knowledge — decisions, conventions, patterns that aren't written down anywhere. The direct question ("What are your coding conventions?") gets a generic answer. The grounded question ("Look at this file and tell me what conventions you can infer") gets observations you can actually verify and build on.

When extracting knowledge that lives in your head rather than in documents, ask: "What do you know about this that isn't written here? If someone new took over, what would they miss?" These questions use the artifact as a launch point into the unwritten context surrounding it — which is usually where the most valuable information lives.
