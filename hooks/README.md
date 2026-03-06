# Hook Patterns

Hooks are Claude Code's mechanism for deterministic behavior — things that should happen every time, without relying on the model to remember. They execute shell commands or prompt-based checks in response to events.

## When to use hooks vs. CLAUDE.md

**Hooks** for behavior that must be deterministic:
- Date injection (the model can't know today's date reliably)
- Blocking dangerous commands before execution
- Enforcing invariants that can be checked mechanically

**CLAUDE.md** for behavior that requires judgment:
- Communication style
- Architectural decisions
- When to ask vs. proceed

If you're writing a CLAUDE.md rule and thinking "but it doesn't always follow this" — that might be a hook instead.

## Pattern: Date injection

The model doesn't reliably know today's date. Inject it at session start.

```json
{
  "hooks": {
    "SessionStart": [
      {
        "type": "command",
        "command": "echo \"Current date: $(date '+%Y-%m-%d %A')\""
      }
    ]
  }
}
```

This runs at session start and injects the current date into context. Now every session starts with accurate temporal awareness.

## Pattern: Dangerous command blocking

Prevent destructive commands from running without confirmation.

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "command",
        "command": "if echo \"$TOOL_INPUT\" | grep -qE 'rm -rf|drop table|force push|--no-verify'; then echo 'BLOCK: Destructive command detected. Ask user for explicit confirmation.'; exit 1; fi"
      }
    ]
  }
}
```

## Pattern: File protection

Prevent modification of critical files.

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "command",
        "command": "if echo \"$TOOL_INPUT\" | grep -qE '\\.env|credentials|secrets'; then echo 'BLOCK: Protected file. Cannot modify without explicit user override.'; exit 1; fi"
      }
    ]
  }
}
```

## Pattern: IP protection

Prevent the model from outputting or committing proprietary content.

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "command",
        "command": "if echo \"$TOOL_INPUT\" | grep -qiE 'engine-internal|proprietary|confidential'; then echo 'BLOCK: Potential IP leak detected.'; exit 1; fi"
      }
    ]
  }
}
```

## Pattern: Prompt-based validation

For checks that require judgment (not just pattern matching), use prompt-based hooks.

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "type": "prompt",
        "prompt": "Review the proposed tool use. If it would delete user data, modify production config, or expose credentials, respond with BLOCK and the reason. Otherwise respond with ALLOW.",
        "matcher": "Bash"
      }
    ]
  }
}
```

## Configuration

Hooks go in `~/.claude/settings.json` (global) or `.claude/settings.json` (project-level).

## Design principles

1. **Hooks are guardrails, not workflow.** Don't orchestrate with hooks — orchestrate with skills and CLAUDE.md. Hooks catch what shouldn't happen.
2. **Fail closed.** If a hook check fails or errors, block the action. False positives are cheaper than false negatives.
3. **Keep hooks fast.** They run synchronously. Slow hooks degrade the interactive experience.
4. **Log, don't hide.** When a hook blocks something, say why. Silent blocks create confusion.
