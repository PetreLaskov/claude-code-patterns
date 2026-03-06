# Instruction Hazards

Common instructions in system prompts and CLAUDE.md files reliably degrade LLM output quality. They do this by activating low-quality regions of training data — SEO content, help-desk scripts, corporate boilerplate — instead of the expert-level writing the model is capable of producing. Understanding the mechanism lets you write instructions that narrow output quality upward instead of downward.

---

## The Hazards Table

Certain phrasings feel like good guidance but consistently produce worse output. The table below catalogs known hazards, explains the degradation mechanism, and provides a safe alternative for each.

| Instruction | What it actually does | Safe alternative |
|---|---|---|
| "Use simple language" | Routes to SEO/listicle content. The model associates "simple" with the vast corpus of dumbed-down web content it trained on. | "The reader is intelligent but not domain-expert." |
| "Be accessible" / "Be user-friendly" | Routes to help-desk/chatbot register. These phrases correlate in training data with shallow, overly cheerful support scripts. | Describe the specific reader and their context. |
| "Be concise" (unqualified) | Produces truncated, shallow output. The model strips substance to minimize length, losing nuance and detail. | "Respond proportionally — brief for simple questions, thorough for complex ones." |
| "Don't use jargon" | Strips precision without adding clarity. Technical terms exist because they carry meaning that plain language cannot efficiently replicate. | "Introduce technical terms by explaining them on first use." |
| "Be professional" | Routes to corporate boilerplate. The model's training data associates "professional" with stiff, hedged, committee-approved prose. | Describe the specific stance and relationship you want. |
| "Write in an engaging way" | Routes to clickbait/content marketing. "Engaging" in training data overwhelmingly means listicles, hooks, and manufactured enthusiasm. | Provide examples of the desired output quality. |
| "Be helpful" | Redundant RLHF reinforcement. The model is already trained to be helpful; restating it amplifies sycophancy and eagerness to please at the expense of honesty. | Omit entirely. The model does not need this instruction. |
| Bare "NEVER do X" | Over-generalized avoidance produces stilted output. Without understanding why, the model over-corrects, becoming self-conscious and wooden. | Motivate the constraint: explain why, then state what to do instead. |

**The underlying pattern:** adjectives are ambiguous. When you say "be professional" or "be engaging," the model must resolve that ambiguity — and it resolves it by defaulting to the statistical center of its training data, where the most generic content lives. Concrete context (who the reader is, what the relationship is, what the purpose is) narrows the output distribution without degrading quality.

---

## The Anti-Convergence Principle

**The phenomenon:** Language models tend toward generic, "on distribution" output — the statistical center of training data where the most averaged, most interchangeable content lives. This is called *distributional convergence*. It is the single most important failure mode for output quality.

Three mechanisms reinforce it:

1. **Training data composition bias.** Formal, pedagogical, and generic content is massively overrepresented in training corpora relative to distinctive expert writing.
2. **RLHF typicality bias.** Human annotators during reinforcement learning from human feedback tend to prefer conventional, expected responses — creating mode collapse toward the average.
3. **Instruction-style entanglement.** Phrases like "explain simply" correlate in training data with dumbed-down content. The instruction itself activates the low-quality distribution.

**Detection signal:** The output could have been written for anyone, about anything, in any context. It contains no specifics from your actual situation — no reference to your codebase, your constraints, your goals.

**Fix:** Specificity is the antidote. Every output should be traceable to something concrete — a file you referenced, a constraint you stated, a pattern you observed. When you notice generic output, the problem is almost always that the instructions are too abstract. Add context, not more style adjectives.

**Direct naming works.** Simply telling the model "You tend toward generic, on-distribution output" significantly improves distinctiveness. The model can correct for the tendency when it knows to watch for it.

---

## Over-Scaffolding Reasoning Models

Modern reasoning models (Claude with extended thinking, GPT o-series, and similar) have built-in chain-of-thought capabilities. They are naturally introspective. Evidence from production use shows that over-prompting these models degrades performance rather than improving it.

Specific findings:

- **Thoroughness instructions backfire.** Instructions like "Be THOROUGH when gathering information" cause reasoning models to overuse tools — calling search repeatedly when internal knowledge would have sufficed. The model takes the instruction literally and applies it indiscriminately.
- **Excessive scaffolding competes with internal reasoning.** When you provide detailed step-by-step reasoning instructions to a model that already reasons step-by-step internally, the external scaffolding can conflict with the model's own reasoning process, producing worse results than no scaffolding at all.
- **Zero-shot often outperforms few-shot.** Reasoning models frequently perform better without examples. Few-shot examples can cause the model to pattern-match to the examples rather than reason about the actual problem.
- **Prompts that worked for earlier models need softening.** Instructions optimized for non-reasoning models (GPT-4, earlier Claude versions) often need to be relaxed — not strengthened — for reasoning models.

**The principle:** for reasoning models, state what you want and why. Do not prescribe how to think. Let the model's internal reasoning handle the method. Reserve explicit scaffolding for cases where you have evidence the model consistently fails without it.

---

## Overcorrection Risk

Aggressive anti-slop prompting — long lists of banned words, extensive style prohibitions, detailed descriptions of what not to do — can itself become a failure mode. The model becomes anxious about triggering banned patterns and produces stilted, overly-terse, self-conscious writing.

Symptoms of overcorrection:

- Output feels artificially constrained, like the model is walking on eggshells.
- Sentences are unnaturally short because the model is avoiding any construction that might be flagged.
- The model hedges about its own word choices rather than focusing on substance.
- Writing loses natural rhythm and flow — every sentence feels like it was vetted by compliance.
- Useful precision gets stripped because the model cannot distinguish technical terms from jargon-for-its-own-sake.

The root cause is the same distributional convergence mechanism working in reverse. Where vague positive instructions ("be engaging") push toward the generic center, excessive negative instructions ("never use these 50 words") create an artificial avoidance zone that the model navigates clumsily.

**The balance:** a small number of motivated constraints outperforms a long list of unmotivated prohibitions. If you must prohibit, explain why and provide the positive alternative. The model generalizes correctly from motivated instructions; it over-generalizes from bare prohibitions.

---

## The Six Safe-Alternative Principles

These principles replace the hazardous instruction patterns above. They work because they give the model concrete context to narrow its output distribution, rather than ambiguous adjectives that widen it.

### 1. Describe posture, not style

Instead of style adjectives ("professional," "casual," "friendly"), describe the intellectual posture you want. "A colleague who respects you enough to be honest" produces better output than "be professional but approachable." Posture descriptions route to expert writing in training data; style adjectives route to generic content.

### 2. Describe the reader, not the writing

"The reader is a senior engineer who has not worked with this specific system" is more useful than "write clearly and accessibly." When the model knows who it is writing for, it calibrates automatically — vocabulary, depth, assumed knowledge all adjust. When it only knows what style to aim for, it guesses, and guesses converge to the mean.

### 3. Positive framing over prohibition

"Introduce technical terms by explaining them on first use" redirects the model's behavior. "Don't use jargon" suppresses it. Redirection preserves the model's full capability while steering output; suppression removes capability and creates avoidance artifacts. Where possible, state what you want rather than what you don't want.

### 4. Motivated instructions

When you explain why a constraint exists, the model generalizes correctly to novel situations. "Don't start responses with a compliment — it reads as sycophantic and erodes trust" is far more effective than "Don't start with compliments." The model understands the underlying principle (preserve trust) and can apply it to situations you didn't explicitly cover.

### 5. Show, don't describe

Examples of desired output quality are more precise than any description of that quality. If you want a particular tone, register, or level of detail, showing one instance communicates more than paragraphs of adjectives. The model pattern-matches to concrete examples more reliably than it interprets abstract descriptors.

### 6. Name the failure mode

"You tend toward generic, on-distribution output where every sentence could have been written for anyone" is a powerful instruction because it gives the model a specific thing to watch for in its own output. Naming the failure mode activates self-monitoring. The model can catch itself mid-generation and correct course — but only if it knows what to watch for.

---

## Applying This in Practice

When writing or reviewing a CLAUDE.md, system prompt, or any instruction file:

1. **Scan for adjective-based style instructions.** Every instance of "be [adjective]" is a candidate for replacement with concrete context.
2. **Check for bare prohibitions.** Every "never" or "don't" without a "because" is a candidate for motivation or replacement with a positive directive.
3. **Test for convergence.** Read your instructions and ask: could these have been written for any project, any codebase, any user? If yes, they will produce generic output. Add specifics.
4. **Count your constraints.** If your negative instructions outnumber your positive ones, you are likely in overcorrection territory. Rebalance.
5. **Respect the model's reasoning.** If you are using a reasoning model, resist the urge to prescribe thinking steps. State the goal and the quality bar. Let the model figure out how to get there.

The meta-principle: instructions shape output by activating regions of training data. Every phrase you write is a query into the model's learned distribution. Write instructions that activate the region you actually want.
