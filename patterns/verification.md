# Verification Architecture

The single most important leverage point in Claude Code, according to Boris Cherny (Claude Code's creator): give Claude a way to verify its own work. If it has that feedback loop, output quality doubles or triples.

## The verification quadrant

Verification difficulty varies by domain in ways that don't correlate with generation difficulty:

|  | Easy to verify | Hard to verify |
|--|---------------|----------------|
| **Easy to generate** | Personal scripts, config files, simple automation. **Sweet spot** — high confidence, fast iteration. | Investment strategies, content recommendations. **Danger zone** — looks right, may be wrong, slow feedback. |
| **Hard to generate** | Complex algorithms with test suites. **Grindable** — hard but the feedback loop works. | Novel research, strategic decisions. **Judgment zone** — verification requires domain expertise, not just testing. |

Know which quadrant you're in. The verification strategy is different for each:
- **Sweet spot:** Trust and move fast. Verification is cheap.
- **Danger zone:** Build explicit verification infrastructure. Don't trust output without independent validation.
- **Grindable:** Invest in test infrastructure. The model can iterate if it can see failures.
- **Judgment zone:** The human IS the verification. Don't outsource judgment here.

## Test-first as the highest-leverage pattern

"Create unit tests" are magic words. When the model writes tests before implementation:
1. It clarifies requirements (the test IS the specification)
2. It creates its own feedback loop (red → green → refactor)
3. It catches its own errors before you see them
4. It produces evidence of correctness, not just assertion

This applies beyond code. For any task, ask: **what would verification look like?** Then build the verification before the output.

## Trust process, not output

The best operators trust their verification infrastructure, not any individual output. The distinction:

- **Trusting output:** "Claude wrote this, it's probably right." → Dangerous, especially in the hard-to-verify quadrants.
- **Trusting process:** "Claude wrote this, the tests pass, the linter is clean, and the type checker is satisfied." → Reliable, because verification is independent of generation.

Build verification into your workflow, not your hope.

## The confident-but-wrong failure mode

The canonical cautionary tale: Claude produces code that runs, passes basic checks, and looks correct — but contains subtle domain-specific errors. When confronted, it may minimize the error or rationalize it rather than acknowledge the depth of the problem.

This happens because the model pattern-matches to solutions that look right in the training distribution. Domain-specific correctness requires domain-specific verification.

**Prevention:**
- In the danger zone and judgment zone, never trust output without domain-expert review
- Ask the model to enumerate its assumptions — wrong assumptions are where subtle errors hide
- When the model's explanation of an error feels dismissive, push harder: "Explain in detail why this specific output is correct"
- Use the `/diagnose` skill when something feels off but you can't pinpoint why

## Verification infrastructure patterns

1. **Test-first:** Write tests before implementation. The tests define correctness.
2. **Background verification:** Run checks asynchronously while continuing other work.
3. **Independent validation:** Have a separate session or model verify critical output.
4. **Assertion-based checking:** Embed assertions in code that catch invariant violations at runtime.
5. **The domain expert pass:** For high-stakes output in the judgment zone, the human reviews with domain expertise. This is not delegatable.
