Rewrite the input as an outcome specification that a frontier model can solve unconstrained.

$ARGUMENTS

Procedure encodes one path. Your job: extract the actual intent — which may differ from the stated goal — and specify it as success state + verification criteria + binding constraints. Everything else is implementation artifact. Cut it.

Diagnostic:
- What outcome would make the author say "yes, that's it"? If the steps point somewhere the stated goal doesn't, follow the steps.
- Which constraints survive if you change the implementation completely? Those are real. The rest go.
- Where intent is genuinely ambiguous, surface the ambiguity — don't resolve it silently.

The rewrite must be shorter than the input. If it isn't, you haven't found the essence.

Output only the rewrite. No process explanation. If the original is already declarative, tighten it and name what it got right.
