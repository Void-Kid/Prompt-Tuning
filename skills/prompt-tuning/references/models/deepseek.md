# DeepSeek Prompt Guidance

## Prompt Implications

- Distinguish thinking and non-thinking modes before rewriting the prompt.
- Keep task instructions direct and place output constraints in stable prompt sections.
- Do not rely on sampling controls that the active thinking mode ignores.

## Tool And Structured Output Implications

- Use JSON/structured-output options when available, and include JSON wording only as a secondary aid.
- Preserve or strip tool and reasoning fields according to the exact DeepSeek API mode.

## Reasoning/Thinking State

- For older reasoner flows, remove `reasoning_content` before the next request when the API requires it.
- For thinking-mode flows that require continuity, follow the official replay rules rather than treating reasoning text as normal prompt context.

## Staleness Risk

- DeepSeek model names, thinking mode defaults, context windows, and `reasoning_content` handling are volatile. Verify current docs for concrete integration claims.
