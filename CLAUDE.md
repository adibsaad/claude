# CLAUDE.md

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---


## Project Memory & Decision Log

`MEMORY.md` is the persistent decision log for this project and must be maintained throughout development.

### Requirements

- Read `MEMORY.md` at the beginning of every session before making changes.
- Update `MEMORY.md` after any significant architectural, product, implementation, or workflow decision.
- Each entry must include:
  - what was decided
  - why it was decided
  - alternatives that were considered
  - why those alternatives were rejected
- Treat documented decisions as the current source of truth.
- Do not silently override, reverse, or contradict prior decisions.
- If a previous decision needs to change:
  - explicitly acknowledge the conflict
  - explain why the new direction is necessary
  - record the updated decision in `MEMORY.md`
- Prefer extending existing patterns and conventions over introducing new ones without justification.
- Use `MEMORY.md` to preserve long-term project context, reduce repeated debates, and maintain consistency across sessions.

## Error Tracking & Retry Prevention

`ERRORS.md` is the project's failure log and retry-prevention system. Use it to capture failed approaches, debugging dead ends, and lessons learned during implementation.

### Requirements

- Maintain an `ERRORS.md` file at the project root.
- Before attempting complex, error-prone, or previously discussed tasks, review `ERRORS.md` for relevant past failures and working solutions.
- If an approach fails or requires more than 2 meaningful attempts to succeed, add an entry to `ERRORS.md`.

### Each Entry Must Include

- what did not work
- why it failed (if known)
- what worked instead
- guidance or precautions for future attempts

### Rules

- Do not repeatedly suggest or retry approaches already documented as ineffective unless there is new evidence or a materially different context.
- Prefer proven solutions recorded in `ERRORS.md` over speculative alternatives.
- When repeating a previously failed approach intentionally, explicitly explain why it may succeed this time.
- Treat recurring failures as signals to improve tooling, abstractions, documentation, or workflow.
- Use `ERRORS.md` to reduce wasted iteration, preserve debugging knowledge, and improve long-term development efficiency.
