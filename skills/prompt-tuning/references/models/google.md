# Google Gemini Prompt Guidance

## Prompt Implications

- Gemini prompt design is iterative: start clear and direct, then refine against observed outputs.
- Gemini 3 style models respond well to concise instructions and may over-analyze legacy complex prompts.
- Use thinking controls and long-context guidance instead of adding process-heavy instructions.

## Tool And Structured Output Implications

- Use function calling and structured output features when available.
- In long-context prompts, state source priority, retrieval scope, and what evidence should be used.

## Reasoning/Thinking State

- In Gemini function-calling conversations with thinking enabled, preserve and return thought signatures when the API requires them.
- Treat thought signatures as context state, not user-visible prompt text.

## Staleness Risk

- Gemini thinking levels, thought signatures, long-context behavior, and optimizer features are provider-version sensitive. Check official docs for current behavior.

## 2026-06-16 Intervention Notes

- Gemini prompt design remains iterative: start clear, inspect outputs, then refine instructions, examples, context, or runtime settings.
- Function calling should be paired with clear function-use instructions, structured output when needed, and validation for consequential actions.
- In Gemini function-calling flows with thinking enabled, always preserve thought signatures according to the current API guidance.
- Treat thought signatures as provider state. Do not expose them as user-facing prompt text.
